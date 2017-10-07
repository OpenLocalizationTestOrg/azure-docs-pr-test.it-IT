---
title: 'Esercitazione: App Web con database multi-tenant che usa Entity Framework e la sicurezza a livello di riga'
description: Informazioni su come toodevelop un MVC ASP.NET 5 web app con multi-tenant backent, Database SQL mediante Entity Framework e la sicurezza a livello di riga.
metakeywords: azure asp.net mvc entity framework multi tenant row level security rls sql database
services: app-service\web
documentationcenter: .net
manager: jeffreyg
author: tmullaney
ms.assetid: 8fdc47a5-6fc3-4d29-ab6a-33e79f50699f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/25/2016
ms.author: thmullan
ms.openlocfilehash: 1b715e01807032c3f6497c374ce427dd762af141
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-web-app-with-a-multi-tenant-database-using-entity-framework-and-row-level-security"></a><span data-ttu-id="8be2a-103">Esercitazione: App Web con database multi-tenant che usa Entity Framework e la sicurezza a livello di riga</span><span class="sxs-lookup"><span data-stu-id="8be2a-103">Tutorial: Web app with a multi-tenant database using Entity Framework and Row-Level Security</span></span>
<span data-ttu-id="8be2a-104">Questa esercitazione viene illustrato come toobuild multi-tenant web app con una "[database condiviso, schema condiviso](https://msdn.microsoft.com/library/aa479086.aspx)" modello di tenancy, mediante Entity Framework e [sicurezza a livello di riga](https://msdn.microsoft.com/library/dn765131.aspx).</span><span class="sxs-lookup"><span data-stu-id="8be2a-104">This tutorial shows how toobuild a multi-tenant web app with a "[shared database, shared schema](https://msdn.microsoft.com/library/aa479086.aspx)" tenancy model, using Entity Framework and [Row-Level Security](https://msdn.microsoft.com/library/dn765131.aspx).</span></span> <span data-ttu-id="8be2a-105">In questo modello un database singolo contiene dati per molti tenant e ogni riga in ogni tabella è associata a un "ID tenant".</span><span class="sxs-lookup"><span data-stu-id="8be2a-105">In this model, a single database contains data for many tenants, and each row in each table is associated with a "Tenant ID."</span></span> <span data-ttu-id="8be2a-106">Sicurezza a livello di riga (riga), una nuova funzionalità per il Database di SQL Azure, viene utilizzato tooprevent tenant l'accesso ai dati reciproci.</span><span class="sxs-lookup"><span data-stu-id="8be2a-106">Row-Level Security (RLS), a new feature for Azure SQL Database, is used tooprevent tenants from accessing each other's data.</span></span> <span data-ttu-id="8be2a-107">Ciò richiede solo una singola, applicazione di toohello di modifica di piccole dimensioni.</span><span class="sxs-lookup"><span data-stu-id="8be2a-107">This requires just a single, small change toohello application.</span></span> <span data-ttu-id="8be2a-108">Centralizzando hello tenant accesso logica all'interno di database hello stesso, riga semplifica il codice dell'applicazione hello e riduce il rischio di hello accidentale di perdita di dati tra i tenant.</span><span class="sxs-lookup"><span data-stu-id="8be2a-108">By centralizing hello tenant access logic within hello database itself, RLS simplifies hello application code and reduces hello risk of accidental data leakage between tenants.</span></span>

<span data-ttu-id="8be2a-109">Iniziamo con una semplice applicazione Contact Manager hello da [crea un'applicazione ASP.NET MVP con l'autenticazione e i database di SQL Server e distribuire App servizio tooAzure](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="8be2a-109">Let's start with hello simple Contact Manager application from [Create an ASP.NET MVP app with auth and SQL DB and deploy tooAzure App Service](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span></span> <span data-ttu-id="8be2a-110">Diritto a questo punto, un'applicazione hello consente tutti gli utenti (tenant) toosee tutti i contatti:</span><span class="sxs-lookup"><span data-stu-id="8be2a-110">Right now, hello application allows all users (tenants) toosee all contacts:</span></span>

![Applicazione Contact Manager prima dell'abilitazione della sicurezza a livello di riga](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-Before.png)

<span data-ttu-id="8be2a-112">Con poche modifiche di piccola, si verrà aggiunto il supporto per multi-tenancy, in modo che gli utenti siano in grado di toosee solo hello i contatti che appartengono toothem.</span><span class="sxs-lookup"><span data-stu-id="8be2a-112">With just a few small changes, we will add support for multi-tenancy, so that users are able toosee only hello contacts that belong toothem.</span></span>

## <a name="step-1-add-an-interceptor-class-in-hello-application-tooset-hello-sessioncontext"></a><span data-ttu-id="8be2a-113">Passaggio 1: Aggiungere una classe dell'intercettore in hello tooset di applicazione hello SESSION_CONTEXT</span><span class="sxs-lookup"><span data-stu-id="8be2a-113">Step 1: Add an Interceptor class in hello application tooset hello SESSION_CONTEXT</span></span>
<span data-ttu-id="8be2a-114">È presente una modifica applicazione dobbiamo toomake.</span><span class="sxs-lookup"><span data-stu-id="8be2a-114">There is one application change we need toomake.</span></span> <span data-ttu-id="8be2a-115">Perché tutti gli utenti dell'applicazione di connettersi utilizzando database toohello hello stessa stringa di connessione (ad esempio stesso account di accesso SQL), non è attualmente possibile per cui l'utente deve filtrare per un tooknow di criteri di riga.</span><span class="sxs-lookup"><span data-stu-id="8be2a-115">Because all application users connect toohello database using hello same connection string (i.e. same SQL login), there is currently no way for an RLS policy tooknow which user it should filter for.</span></span> <span data-ttu-id="8be2a-116">Questo approccio è molto comune nelle applicazioni web perché consente di pool di connessioni efficiente, ma significa che è necessario un altro modo tooidentify hello utente corrente dell'applicazione all'interno del database hello.</span><span class="sxs-lookup"><span data-stu-id="8be2a-116">This approach is very common in web applications because it enables efficient connection pooling, but it means we need another way tooidentify hello current application user within hello database.</span></span> <span data-ttu-id="8be2a-117">Hello soluzione è toohave hello applicazione set una coppia chiave-valore per hello UserId corrente in hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) immediatamente dopo l'apertura di una connessione, prima di eseguire le query.</span><span class="sxs-lookup"><span data-stu-id="8be2a-117">hello solution is toohave hello application set a key-value pair for hello current UserId in hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) immediately after opening a connection, before it executes any queries.</span></span> <span data-ttu-id="8be2a-118">SESSION_CONTEXT è un archivio chiave-valore con ambito sessione e i criteri di riga verranno utilizzati hello in essa archiviati UserId tooidentify utente corrente di hello.</span><span class="sxs-lookup"><span data-stu-id="8be2a-118">SESSION_CONTEXT is a session-scoped key-value store, and our RLS policy will use hello UserId stored in it tooidentify hello current user.</span></span>

<span data-ttu-id="8be2a-119">Si aggiungerà un [intercettore](https://msdn.microsoft.com/data/dn469464.aspx) (in particolare, un [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), una nuova funzionalità in Entity Framework (EF) 6, tooautomatically set hello UserId corrente in hello SESSION_CONTEXT eseguendo un Istruzione T-SQL ogni volta che EF apre una connessione.</span><span class="sxs-lookup"><span data-stu-id="8be2a-119">We will add an [interceptor](https://msdn.microsoft.com/data/dn469464.aspx) (in particular, a [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), a new feature in Entity Framework (EF) 6, tooautomatically set hello current UserId in hello SESSION_CONTEXT by executing a T-SQL statement whenever EF opens a connection.</span></span>

1. <span data-ttu-id="8be2a-120">Aprire il progetto di ContactManager hello in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8be2a-120">Open hello ContactManager project in Visual Studio.</span></span>
2. <span data-ttu-id="8be2a-121">Pulsante destro del mouse sulla cartella Modelli hello in hello Esplora soluzioni e scegliere Aggiungi > classe.</span><span class="sxs-lookup"><span data-stu-id="8be2a-121">Right-click on hello Models folder in hello Solution Explorer, and choose Add > Class.</span></span>
3. <span data-ttu-id="8be2a-122">Nome nuova classe hello "SessionContextInterceptor.cs" e fare clic su Aggiungi.</span><span class="sxs-lookup"><span data-stu-id="8be2a-122">Name hello new class "SessionContextInterceptor.cs" and click Add.</span></span>
4. <span data-ttu-id="8be2a-123">Sostituire il contenuto di hello del SessionContextInterceptor.cs con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="8be2a-123">Replace hello contents of SessionContextInterceptor.cs with hello following code.</span></span>

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Data.Common;
using System.Data.Entity;
using System.Data.Entity.Infrastructure.Interception;
using Microsoft.AspNet.Identity;

namespace ContactManager.Models
{
    public class SessionContextInterceptor : IDbConnectionInterceptor
    {
        public void Opened(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
            // Set SESSION_CONTEXT toocurrent UserId whenever EF opens a connection
            try
            {
                var userId = System.Web.HttpContext.Current.User.Identity.GetUserId();
                if (userId != null)
                {
                    DbCommand cmd = connection.CreateCommand();
                    cmd.CommandText = "EXEC sp_set_session_context @key=N'UserId', @value=@UserId";
                    DbParameter param = cmd.CreateParameter();
                    param.ParameterName = "@UserId";
                    param.Value = userId;
                    cmd.Parameters.Add(param);
                    cmd.ExecuteNonQuery();
                }
            }
            catch (System.NullReferenceException)
            {
                // If no user is logged in, leave SESSION_CONTEXT null (all rows will be filtered)
            }
        }

        public void Opening(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void BeganTransaction(DbConnection connection, BeginTransactionInterceptionContext interceptionContext)
        {
        }

        public void BeginningTransaction(DbConnection connection, BeginTransactionInterceptionContext interceptionContext)
        {
        }

        public void Closed(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void Closing(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void ConnectionStringGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionStringGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionStringSet(DbConnection connection, DbConnectionPropertyInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionStringSetting(DbConnection connection, DbConnectionPropertyInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionTimeoutGetting(DbConnection connection, DbConnectionInterceptionContext<int> interceptionContext)
        {
        }

        public void ConnectionTimeoutGot(DbConnection connection, DbConnectionInterceptionContext<int> interceptionContext)
        {
        }

        public void DataSourceGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void DataSourceGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void DatabaseGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void DatabaseGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void Disposed(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void Disposing(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void EnlistedTransaction(DbConnection connection, EnlistTransactionInterceptionContext interceptionContext)
        {
        }

        public void EnlistingTransaction(DbConnection connection, EnlistTransactionInterceptionContext interceptionContext)
        {
        }

        public void ServerVersionGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void ServerVersionGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void StateGetting(DbConnection connection, DbConnectionInterceptionContext<System.Data.ConnectionState> interceptionContext)
        {
        }

        public void StateGot(DbConnection connection, DbConnectionInterceptionContext<System.Data.ConnectionState> interceptionContext)
        {
        }
    }

    public class SessionContextConfiguration : DbConfiguration
    {
        public SessionContextConfiguration()
        {
            AddInterceptor(new SessionContextInterceptor());
        }
    }
}
```

<span data-ttu-id="8be2a-124">Che è richiesta di modifica di hello unica applicazione.</span><span class="sxs-lookup"><span data-stu-id="8be2a-124">That's hello only application change required.</span></span> <span data-ttu-id="8be2a-125">Vado avanti e compilare e pubblicare un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="8be2a-125">Go ahead and build and publish hello application.</span></span>

## <a name="step-2-add-a-userid-column-toohello-database-schema"></a><span data-ttu-id="8be2a-126">Passaggio 2: Aggiungere uno schema di database toohello colonna ID utente</span><span class="sxs-lookup"><span data-stu-id="8be2a-126">Step 2: Add a UserId column toohello database schema</span></span>
<span data-ttu-id="8be2a-127">Successivamente, è necessario un tooassociate tabella contatti di UserId colonna toohello tooadd ogni riga a un utente (tenant).</span><span class="sxs-lookup"><span data-stu-id="8be2a-127">Next, we need tooadd a UserId column toohello Contacts table tooassociate each row with a user (tenant).</span></span> <span data-ttu-id="8be2a-128">Si comporta la modifica dello schema hello direttamente nel database di hello, in modo che non abbiamo tooinclude questo campo nel nostro modello di dati di Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="8be2a-128">We will alter hello schema directly in hello database, so that we don't have tooinclude this field in our EF data model.</span></span>

<span data-ttu-id="8be2a-129">Connessione diretta, toohello database utilizzando SQL Server Management Studio o Visual Studio e quindi eseguire hello T-SQL seguente:</span><span class="sxs-lookup"><span data-stu-id="8be2a-129">Connect toohello database directly, using either SQL Server Management Studio or Visual Studio, and then execute hello following T-SQL:</span></span>

```
ALTER TABLE Contacts ADD UserId nvarchar(128)
    DEFAULT CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
```

<span data-ttu-id="8be2a-130">Aggiunge una tabella di contatti toohello colonna ID utente.</span><span class="sxs-lookup"><span data-stu-id="8be2a-130">This adds a UserId column toohello Contacts table.</span></span> <span data-ttu-id="8be2a-131">Utilizziamo hello hello nvarchar (128) dati tipo toomatch che degli ID utente archiviati nella tabella AspNetUsers hello e creare un vincolo DEFAULT che verrà impostato automaticamente hello UserId per le righe appena inserite toobe hello UserId attualmente archiviati nel SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="8be2a-131">We use hello nvarchar(128) data type toomatch hello UserIds stored in hello AspNetUsers table, and we create a DEFAULT constraint that will automatically set hello UserId for newly inserted rows toobe hello UserId currently stored in SESSION_CONTEXT.</span></span>

<span data-ttu-id="8be2a-132">Tabella hello ora simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="8be2a-132">Now hello table looks like this:</span></span>

![Tabella Contacts SSMS](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-Contacts.png)

<span data-ttu-id="8be2a-134">Quando vengono creati nuovi contatti, essi verrà assegnati automaticamente hello correggere UserId.</span><span class="sxs-lookup"><span data-stu-id="8be2a-134">When new contacts are created, they'll automatically be assigned hello correct UserId.</span></span> <span data-ttu-id="8be2a-135">A scopo dimostrativo, tuttavia, si assegna alcuni di questi tooan contatti esistenti utente esistente.</span><span class="sxs-lookup"><span data-stu-id="8be2a-135">For demo purposes, however, let's assign a few of these existing contacts tooan existing user.</span></span>

<span data-ttu-id="8be2a-136">Se sono stati creati alcuni utenti in un'applicazione hello già (ad esempio, utilizzo locale, Google o Facebook account), verranno visualizzati nella tabella AspNetUsers hello.</span><span class="sxs-lookup"><span data-stu-id="8be2a-136">If you've created a few users in hello application already (e.g., using local, Google, or Facebook accounts), you'll see them in hello AspNetUsers table.</span></span> <span data-ttu-id="8be2a-137">Schermata di hello riportata di seguito, prevede un solo utente finora.</span><span class="sxs-lookup"><span data-stu-id="8be2a-137">In hello screenshot below, there is only one user so far.</span></span>

![Tabella AspNetUsers SSMS](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-AspNetUsers.png)

<span data-ttu-id="8be2a-139">Hello copia Id per user1@contoso.come incollarlo in istruzione hello T-SQL riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="8be2a-139">Copy hello Id for user1@contoso.com, and paste it into hello T-SQL statement below.</span></span> <span data-ttu-id="8be2a-140">Eseguire questa istruzione tooassociate tre, di hello contatti con l'ID utente.</span><span class="sxs-lookup"><span data-stu-id="8be2a-140">Execute this statement tooassociate three of hello Contacts with this UserId.</span></span>

```
UPDATE Contacts SET UserId = '19bc9b0d-28dd-4510-bd5e-d6b6d445f511'
WHERE ContactId IN (1, 2, 5)
```

## <a name="step-3-create-a-row-level-security-policy-in-hello-database"></a><span data-ttu-id="8be2a-141">Passaggio 3: Creare un criterio di sicurezza a livello di riga nel database di hello</span><span class="sxs-lookup"><span data-stu-id="8be2a-141">Step 3: Create a Row-Level Security policy in hello database</span></span>
<span data-ttu-id="8be2a-142">passaggio finale Hello è toocreate un criterio di sicurezza che utilizza hello UserId SESSION_CONTEXT tooautomatically filtro hello risultati restituiti dalle query.</span><span class="sxs-lookup"><span data-stu-id="8be2a-142">hello final step is toocreate a security policy that uses hello UserId in SESSION_CONTEXT tooautomatically filter hello results returned by queries.</span></span>

<span data-ttu-id="8be2a-143">Mentre il database toohello ancora connessi, eseguire hello T-SQL seguente:</span><span class="sxs-lookup"><span data-stu-id="8be2a-143">While still connected toohello database, execute hello following T-SQL:</span></span>

```
CREATE SCHEMA Security
go

CREATE FUNCTION Security.userAccessPredicate(@UserId nvarchar(128))
    RETURNS TABLE
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS accessResult
    WHERE @UserId = CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
go

CREATE SECURITY POLICY Security.userSecurityPolicy
    ADD FILTER PREDICATE Security.userAccessPredicate(UserId) ON dbo.Contacts,
    ADD BLOCK PREDICATE Security.userAccessPredicate(UserId) ON dbo.Contacts
go

```

<span data-ttu-id="8be2a-144">Questo codice esegue tre operazioni.</span><span class="sxs-lookup"><span data-stu-id="8be2a-144">This code does three things.</span></span> <span data-ttu-id="8be2a-145">Viene innanzitutto creato un nuovo schema come procedura consigliata per la centralizzazione e limitare gli oggetti di access toohello di riga.</span><span class="sxs-lookup"><span data-stu-id="8be2a-145">First, it creates a new schema as a best practice for centralizing and limiting access toohello RLS objects.</span></span> <span data-ttu-id="8be2a-146">Successivamente, viene creata una funzione di predicato che restituisce '1' quando hello ID utente di una riga corrisponde hello UserId in SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="8be2a-146">Next, it creates a predicate function that will return '1' when hello UserId of a row matches hello UserId in SESSION_CONTEXT.</span></span> <span data-ttu-id="8be2a-147">Infine, viene creato un criterio di sicurezza che aggiunga questa funzione come predicato di un filtro e di blocco per la tabella Contacts hello.</span><span class="sxs-lookup"><span data-stu-id="8be2a-147">Finally, it creates a security policy that adds this function as both a filter and block predicate on hello Contacts table.</span></span> <span data-ttu-id="8be2a-148">predicato del filtro Hello determina tooreturn query solo le righe a cui appartengano l'utente corrente toohello predicato di blocco hello funge da un'applicazione di hello salvaguardia tooprevent mai accidentalmente inserire una riga per l'utente errato hello.</span><span class="sxs-lookup"><span data-stu-id="8be2a-148">hello filter predicate causes queries tooreturn only rows that belong toohello current user, and hello block predicate acts as a safeguard tooprevent hello application from ever accidentally inserting a row for hello wrong user.</span></span>

<span data-ttu-id="8be2a-149">Eseguire un'applicazione hello e accedere come user1@contoso.com. Questo utente viene visualizzata solo i contatti di hello è assegnato toothis UserId:</span><span class="sxs-lookup"><span data-stu-id="8be2a-149">Now run hello application, and sign in as user1@contoso.com. This user now sees only hello Contacts we assigned toothis UserId earlier:</span></span>

![Applicazione Contact Manager prima dell'abilitazione della sicurezza a livello di riga](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-After.png)

<span data-ttu-id="8be2a-151">toovalidate questo ulteriormente, provare a registrare un nuovo utente.</span><span class="sxs-lookup"><span data-stu-id="8be2a-151">toovalidate this further, try registering a new user.</span></span> <span data-ttu-id="8be2a-152">I contatti, non verranno visualizzati perché non sono stati assegnati toothem.</span><span class="sxs-lookup"><span data-stu-id="8be2a-152">They will see no contacts, because none have been assigned toothem.</span></span> <span data-ttu-id="8be2a-153">Se si crea un nuovo contatto, sarà assegnato toothem e solo saranno in grado di toosee è.</span><span class="sxs-lookup"><span data-stu-id="8be2a-153">If they create a new contact, it will be assigned toothem, and only they will be able toosee it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8be2a-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8be2a-154">Next steps</span></span>
<span data-ttu-id="8be2a-155">L'operazione è terminata.</span><span class="sxs-lookup"><span data-stu-id="8be2a-155">That's it!</span></span> <span data-ttu-id="8be2a-156">Hello semplice contattare Manager web app è stata convertita in un multi-tenant, uno in cui ogni utente dispone di un proprio elenco di contatti.</span><span class="sxs-lookup"><span data-stu-id="8be2a-156">hello simple Contact Manager web app has been converted into a multi-tenant one where each user has its own contact list.</span></span> <span data-ttu-id="8be2a-157">Tramite la sicurezza a livello di riga, è stata evitare complessità hello di applicare la logica di accesso ai tenant nel codice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8be2a-157">By using Row-Level Security, we've avoided hello complexity of enforcing tenant access logic in our application code.</span></span> <span data-ttu-id="8be2a-158">La trasparenza consente toofocus applicazione hello sul problema aziendale reale di hello in questione e riduce inoltre il rischio di hello della perdita accidentale di dati come un'applicazione hello codebase aumenta.</span><span class="sxs-lookup"><span data-stu-id="8be2a-158">This transparency allows hello application toofocus on hello real business problem at hand, and it also reduces hello risk of accidentally leaking data as hello application's codebase grows.</span></span>

<span data-ttu-id="8be2a-159">In questa esercitazione dispone solo area di hello graffiato di ciò che è possibile con una riga.</span><span class="sxs-lookup"><span data-stu-id="8be2a-159">This tutorial has only scratched hello surface of what's possible with RLS.</span></span> <span data-ttu-id="8be2a-160">Ad esempio, è possibile toohave più sofisticate o logica di accesso granulare e toostore possibili è molto più hello UserId corrente in hello SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="8be2a-160">For instance, it's possible toohave more sophisticated or granular access logic, and it's possible toostore more than just hello current UserId in hello SESSION_CONTEXT.</span></span> <span data-ttu-id="8be2a-161">È inoltre possibile troppo[integrare di riga con le librerie client gli strumenti di database elastico hello](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) toosupport partizioni di multi-tenant in un livello di dati di scalabilità orizzontale.</span><span class="sxs-lookup"><span data-stu-id="8be2a-161">It's also possible too[integrate RLS with hello elastic database tools client libraries](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) toosupport multi-tenant shards in a scale-out data tier.</span></span>

<span data-ttu-id="8be2a-162">Oltre a queste possibilità, stiamo lavorando anche toomake ancora migliore di riga.</span><span class="sxs-lookup"><span data-stu-id="8be2a-162">Beyond these possibilities, we're also working toomake RLS even better.</span></span> <span data-ttu-id="8be2a-163">Se si dispone di domande, suggerimenti o operazioni si desidera toosee, Saremmo lieti di sapere nei commenti hello.</span><span class="sxs-lookup"><span data-stu-id="8be2a-163">If you have any questions, ideas, or things you'd like toosee, please let us know in hello comments.</span></span> <span data-ttu-id="8be2a-164">I commenti e suggerimenti degli utenti sono molto apprezzati.</span><span class="sxs-lookup"><span data-stu-id="8be2a-164">We appreciate your feedback!</span></span>

