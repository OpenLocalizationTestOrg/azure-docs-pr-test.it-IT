---
title: 'Esercitazione: App Web con database multi-tenant che usa Entity Framework e la sicurezza a livello di riga'
description: Informazioni su come sviluppare un'app Web ASP.NET MVC 5 con un back-end del database SQL multi-tenant che usa Entity Framework e la sicurezza a livello di riga.
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
ms.openlocfilehash: ba1bb3d84b462dfebbb2564569517d7336bf54fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-web-app-with-a-multi-tenant-database-using-entity-framework-and-row-level-security"></a><span data-ttu-id="ea14e-103">Esercitazione: App Web con database multi-tenant che usa Entity Framework e la sicurezza a livello di riga</span><span class="sxs-lookup"><span data-stu-id="ea14e-103">Tutorial: Web app with a multi-tenant database using Entity Framework and Row-Level Security</span></span>
<span data-ttu-id="ea14e-104">Questa esercitazione illustra come sviluppare un'app Web multi-tenant con un modello di tenancy di tipo "[database condiviso, schema condiviso](https://msdn.microsoft.com/library/aa479086.aspx)" usando Entity Framework e la [sicurezza a livello di riga](https://msdn.microsoft.com/library/dn765131.aspx).</span><span class="sxs-lookup"><span data-stu-id="ea14e-104">This tutorial shows how to build a multi-tenant web app with a "[shared database, shared schema](https://msdn.microsoft.com/library/aa479086.aspx)" tenancy model, using Entity Framework and [Row-Level Security](https://msdn.microsoft.com/library/dn765131.aspx).</span></span> <span data-ttu-id="ea14e-105">In questo modello un database singolo contiene dati per molti tenant e ogni riga in ogni tabella è associata a un "ID tenant".</span><span class="sxs-lookup"><span data-stu-id="ea14e-105">In this model, a single database contains data for many tenants, and each row in each table is associated with a "Tenant ID."</span></span> <span data-ttu-id="ea14e-106">La sicurezza a livello di riga, una nuova funzionalità del database SQL di Azure, consente di impedire ai tenant di accedere ai dati degli altri tenant.</span><span class="sxs-lookup"><span data-stu-id="ea14e-106">Row-Level Security (RLS), a new feature for Azure SQL Database, is used to prevent tenants from accessing each other's data.</span></span> <span data-ttu-id="ea14e-107">È necessaria solo una piccola modifica all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ea14e-107">This requires just a single, small change to the application.</span></span> <span data-ttu-id="ea14e-108">Centralizzando la logica di accesso al tenant entro il database stesso, la sicurezza a livello di riga semplifica il codice dell'applicazione e riduce il rischio di diffusione accidentale dei dati tra i tenant.</span><span class="sxs-lookup"><span data-stu-id="ea14e-108">By centralizing the tenant access logic within the database itself, RLS simplifies the application code and reduces the risk of accidental data leakage between tenants.</span></span>

<span data-ttu-id="ea14e-109">È possibile iniziare con la semplice applicazione Contact Manager disponibile in [Creare un'app ASP.NET MVC con autenticazione e database SQL e distribuirla nel servizio app di Azure](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="ea14e-109">Let's start with the simple Contact Manager application from [Create an ASP.NET MVP app with auth and SQL DB and deploy to Azure App Service](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span></span> <span data-ttu-id="ea14e-110">L'applicazione consente attualmente a tutti gli utenti (tenant) di visualizzare tutti i contatti:</span><span class="sxs-lookup"><span data-stu-id="ea14e-110">Right now, the application allows all users (tenants) to see all contacts:</span></span>

![Applicazione Contact Manager prima dell'abilitazione della sicurezza a livello di riga](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-Before.png)

<span data-ttu-id="ea14e-112">Con qualche modifica è possibile aggiungere il supporto per il multi-tenancy, in modo che gli utenti possano visualizzare solo i propri contatti.</span><span class="sxs-lookup"><span data-stu-id="ea14e-112">With just a few small changes, we will add support for multi-tenancy, so that users are able to see only the contacts that belong to them.</span></span>

## <a name="step-1-add-an-interceptor-class-in-the-application-to-set-the-sessioncontext"></a><span data-ttu-id="ea14e-113">Passaggio 1: Aggiungere una classe Interceptor nell'applicazione per configurare SESSION_CONTEXT</span><span class="sxs-lookup"><span data-stu-id="ea14e-113">Step 1: Add an Interceptor class in the application to set the SESSION_CONTEXT</span></span>
<span data-ttu-id="ea14e-114">È necessario apportare una modifica all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ea14e-114">There is one application change we need to make.</span></span> <span data-ttu-id="ea14e-115">Poiché tutti gli utenti dell'applicazione si connettono al database usando la stessa stringa di connessione, ovvero lo stesso accesso SQL, non è attualmente possibile per un criterio di sicurezza a livello di riga conoscere l'utente in base a cui applicare il filtro.</span><span class="sxs-lookup"><span data-stu-id="ea14e-115">Because all application users connect to the database using the same connection string (i.e. same SQL login), there is currently no way for an RLS policy to know which user it should filter for.</span></span> <span data-ttu-id="ea14e-116">Questo approccio è molto comune in applicazioni Web perché consente il pooling efficiente delle connessioni, ma richiede un altro modo per identificare l'utente attuale dell'applicazione Web nel database.</span><span class="sxs-lookup"><span data-stu-id="ea14e-116">This approach is very common in web applications because it enables efficient connection pooling, but it means we need another way to identify the current application user within the database.</span></span> <span data-ttu-id="ea14e-117">La soluzione consiste nel fare in modo che l'applicazione configuri una coppia chiave-valore per l'UserId corrente in [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) immediatamente dopo l'apertura della connessione e prima dell'esecuzione di query.</span><span class="sxs-lookup"><span data-stu-id="ea14e-117">The solution is to have the application set a key-value pair for the current UserId in the [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) immediately after opening a connection, before it executes any queries.</span></span> <span data-ttu-id="ea14e-118">SESSION_CONTEXT è un archivio di coppie chiave-valore con ambito sessione e il criterio della sicurezza a livello di riga userà il valore UserId archiviato per identificare l'utente corrente.</span><span class="sxs-lookup"><span data-stu-id="ea14e-118">SESSION_CONTEXT is a session-scoped key-value store, and our RLS policy will use the UserId stored in it to identify the current user.</span></span>

<span data-ttu-id="ea14e-119">Verrà aggiunto un [intercettore](https://msdn.microsoft.com/data/dn469464.aspx), in particolare [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor), una nuova funzionalità di Entity Framework (EF) 6, per configurare automaticamente il valore UserId attuale in SESSION_CONTEXT eseguendo un'istruzione T-SQL ogni volta che EF apre una connessione.</span><span class="sxs-lookup"><span data-stu-id="ea14e-119">We will add an [interceptor](https://msdn.microsoft.com/data/dn469464.aspx) (in particular, a [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), a new feature in Entity Framework (EF) 6, to automatically set the current UserId in the SESSION_CONTEXT by executing a T-SQL statement whenever EF opens a connection.</span></span>

1. <span data-ttu-id="ea14e-120">Aprire il progetto ContactManager in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ea14e-120">Open the ContactManager project in Visual Studio.</span></span>
2. <span data-ttu-id="ea14e-121">Fare clic con il pulsante destro del mouse sulla cartella Modelli in Esplora soluzioni, quindi scegliere Aggiungi > Classe.</span><span class="sxs-lookup"><span data-stu-id="ea14e-121">Right-click on the Models folder in the Solution Explorer, and choose Add > Class.</span></span>
3. <span data-ttu-id="ea14e-122">Assegnare alla nuova classe il nome "SessionContextInterceptor.cs" e fare clic su Aggiungi.</span><span class="sxs-lookup"><span data-stu-id="ea14e-122">Name the new class "SessionContextInterceptor.cs" and click Add.</span></span>
4. <span data-ttu-id="ea14e-123">Sostituire i contenuti di SessionContextInterceptor.cs con il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="ea14e-123">Replace the contents of SessionContextInterceptor.cs with the following code.</span></span>

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
            // Set SESSION_CONTEXT to current UserId whenever EF opens a connection
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

<span data-ttu-id="ea14e-124">È necessaria solo una modifica all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ea14e-124">That's the only application change required.</span></span> <span data-ttu-id="ea14e-125">Sviluppare e pubblicare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ea14e-125">Go ahead and build and publish the application.</span></span>

## <a name="step-2-add-a-userid-column-to-the-database-schema"></a><span data-ttu-id="ea14e-126">Passaggio 2: Aggiungere una colonna UserId allo schema del database</span><span class="sxs-lookup"><span data-stu-id="ea14e-126">Step 2: Add a UserId column to the database schema</span></span>
<span data-ttu-id="ea14e-127">È ora necessario aggiungere una colonna UserId alla tabella Contacts per associare ogni riga a un utente (tenant).</span><span class="sxs-lookup"><span data-stu-id="ea14e-127">Next, we need to add a UserId column to the Contacts table to associate each row with a user (tenant).</span></span> <span data-ttu-id="ea14e-128">Lo schema verrà modificato direttamente nel database, quindi non è necessario includere questo campo nel modello di dati EF.</span><span class="sxs-lookup"><span data-stu-id="ea14e-128">We will alter the schema directly in the database, so that we don't have to include this field in our EF data model.</span></span>

<span data-ttu-id="ea14e-129">Connettersi direttamente al database, usando SQL Server Management Studio o Visual Studio, quindi eseguire l'istruzione T-SQL seguente:</span><span class="sxs-lookup"><span data-stu-id="ea14e-129">Connect to the database directly, using either SQL Server Management Studio or Visual Studio, and then execute the following T-SQL:</span></span>

```
ALTER TABLE Contacts ADD UserId nvarchar(128)
    DEFAULT CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
```

<span data-ttu-id="ea14e-130">Una colonna UserId verrà aggiunta alla tabella Contacts.</span><span class="sxs-lookup"><span data-stu-id="ea14e-130">This adds a UserId column to the Contacts table.</span></span> <span data-ttu-id="ea14e-131">Usare il tipo di dati nvarchar(128) per la corrispondenza con i valori UserId archiviati nella tabella AspNetUsers, quindi creare un vincolo DEFAULT che configurerà automaticamente l'UserId per le righe appena inserite in modo che corrisponda all'UserId attualmente archiviato in SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="ea14e-131">We use the nvarchar(128) data type to match the UserIds stored in the AspNetUsers table, and we create a DEFAULT constraint that will automatically set the UserId for newly inserted rows to be the UserId currently stored in SESSION_CONTEXT.</span></span>

<span data-ttu-id="ea14e-132">La tabella avrà un aspetto analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="ea14e-132">Now the table looks like this:</span></span>

![Tabella Contacts SSMS](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-Contacts.png)

<span data-ttu-id="ea14e-134">Quando vengono creati, ai nuovi contatti viene assegnato automaticamente il valore UserId corretto.</span><span class="sxs-lookup"><span data-stu-id="ea14e-134">When new contacts are created, they'll automatically be assigned the correct UserId.</span></span> <span data-ttu-id="ea14e-135">Per finalità di demo, assegnare tuttavia alcuni dei contatti esistenti a un utente esistente.</span><span class="sxs-lookup"><span data-stu-id="ea14e-135">For demo purposes, however, let's assign a few of these existing contacts to an existing user.</span></span>

<span data-ttu-id="ea14e-136">Se nell'applicazione sono già stati creati utenti, ad esempio tramite account locali, Google o Facebook, sarà possibile visualizzarli nella tabella AspNetUsers.</span><span class="sxs-lookup"><span data-stu-id="ea14e-136">If you've created a few users in the application already (e.g., using local, Google, or Facebook accounts), you'll see them in the AspNetUsers table.</span></span> <span data-ttu-id="ea14e-137">Nella schermata seguente è attualmente presente solo un utente.</span><span class="sxs-lookup"><span data-stu-id="ea14e-137">In the screenshot below, there is only one user so far.</span></span>

![Tabella AspNetUsers SSMS](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-AspNetUsers.png)

<span data-ttu-id="ea14e-139">Copiare l'ID per user1@contoso.com e incollarlo nell'istruzione T-SQL seguente.</span><span class="sxs-lookup"><span data-stu-id="ea14e-139">Copy the Id for user1@contoso.com, and paste it into the T-SQL statement below.</span></span> <span data-ttu-id="ea14e-140">Eseguire questa istruzione per associare tre contatti con l'UserId.</span><span class="sxs-lookup"><span data-stu-id="ea14e-140">Execute this statement to associate three of the Contacts with this UserId.</span></span>

```
UPDATE Contacts SET UserId = '19bc9b0d-28dd-4510-bd5e-d6b6d445f511'
WHERE ContactId IN (1, 2, 5)
```

## <a name="step-3-create-a-row-level-security-policy-in-the-database"></a><span data-ttu-id="ea14e-141">Passaggio 3: Creare un criterio di sicurezza a livello di riga nel database</span><span class="sxs-lookup"><span data-stu-id="ea14e-141">Step 3: Create a Row-Level Security policy in the database</span></span>
<span data-ttu-id="ea14e-142">Il passaggio finale consiste nel creare un criterio di sicurezza che usa il valore UserId in SESSION_CONTEXT per filtrare automaticamente i risultati restituiti dalle query.</span><span class="sxs-lookup"><span data-stu-id="ea14e-142">The final step is to create a security policy that uses the UserId in SESSION_CONTEXT to automatically filter the results returned by queries.</span></span>

<span data-ttu-id="ea14e-143">Mentre si è connessi al database, eseguire l'istruzione T-SQL seguente:</span><span class="sxs-lookup"><span data-stu-id="ea14e-143">While still connected to the database, execute the following T-SQL:</span></span>

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

<span data-ttu-id="ea14e-144">Questo codice esegue tre operazioni.</span><span class="sxs-lookup"><span data-stu-id="ea14e-144">This code does three things.</span></span> <span data-ttu-id="ea14e-145">Prima di tutto crea un nuovo schema, come procedura consigliata per centralizzare e limitare l'accesso agli oggetti del criterio di sicurezza a livello di riga.</span><span class="sxs-lookup"><span data-stu-id="ea14e-145">First, it creates a new schema as a best practice for centralizing and limiting access to the RLS objects.</span></span> <span data-ttu-id="ea14e-146">Quindi crea una funzione predicato che restituirà '1' quando il valore UserId di una riga corrisponde all'UserId in SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="ea14e-146">Next, it creates a predicate function that will return '1' when the UserId of a row matches the UserId in SESSION_CONTEXT.</span></span> <span data-ttu-id="ea14e-147">Crea infine un criterio di sicurezza che aggiunge questa funzione come filtro e come predicato di blocco nella tabella Contacts.</span><span class="sxs-lookup"><span data-stu-id="ea14e-147">Finally, it creates a security policy that adds this function as both a filter and block predicate on the Contacts table.</span></span> <span data-ttu-id="ea14e-148">Il predicato di filtro provoca la restituzione da parte delle query solo delle righe appartenenti all'utente corrente e il predicato di blocco funge da protezione per evitare che l'applicazione inserisca accidentalmente una riga per l'utente errato.</span><span class="sxs-lookup"><span data-stu-id="ea14e-148">The filter predicate causes queries to return only rows that belong to the current user, and the block predicate acts as a safeguard to prevent the application from ever accidentally inserting a row for the wrong user.</span></span>

<span data-ttu-id="ea14e-149">Eseguire l'applicazione e accedere come user1@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="ea14e-149">Now run the application, and sign in as user1@contoso.com.</span></span> <span data-ttu-id="ea14e-150">L'utente vede solo i contatti assegnati a questo UserId in precedenza:</span><span class="sxs-lookup"><span data-stu-id="ea14e-150">This user now sees only the Contacts we assigned to this UserId earlier:</span></span>

![Applicazione Contact Manager prima dell'abilitazione della sicurezza a livello di riga](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-After.png)

<span data-ttu-id="ea14e-152">Per una convalida aggiuntiva, provare a registrare un nuovo utente.</span><span class="sxs-lookup"><span data-stu-id="ea14e-152">To validate this further, try registering a new user.</span></span> <span data-ttu-id="ea14e-153">Il nuovo utente non vedrà alcun contatto, perché nessun contatto è stato assegnato a questo utente.</span><span class="sxs-lookup"><span data-stu-id="ea14e-153">They will see no contacts, because none have been assigned to them.</span></span> <span data-ttu-id="ea14e-154">Se l'utente crea un nuovo contatto, questo contatto gli verrà assegnato e potrà visualizzarlo.</span><span class="sxs-lookup"><span data-stu-id="ea14e-154">If they create a new contact, it will be assigned to them, and only they will be able to see it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea14e-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ea14e-155">Next steps</span></span>
<span data-ttu-id="ea14e-156">L'operazione è terminata.</span><span class="sxs-lookup"><span data-stu-id="ea14e-156">That's it!</span></span> <span data-ttu-id="ea14e-157">La semplice app Web Contact Manager è stata convertita in un multi-tenant in cui ogni utente ha il proprio elenco contatti.</span><span class="sxs-lookup"><span data-stu-id="ea14e-157">The simple Contact Manager web app has been converted into a multi-tenant one where each user has its own contact list.</span></span> <span data-ttu-id="ea14e-158">Usando la sicurezza a livello di riga si evita la complessità derivante dall'applicare la logica di accesso al tenant nel codice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ea14e-158">By using Row-Level Security, we've avoided the complexity of enforcing tenant access logic in our application code.</span></span> <span data-ttu-id="ea14e-159">Questa trasparenza consente all'applicazione di concentrarsi sul problema aziendale effettivo e riduce anche il rischio di divulgazione accidentale dei dati con la crescita della codebase dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ea14e-159">This transparency allows the application to focus on the real business problem at hand, and it also reduces the risk of accidentally leaking data as the application's codebase grows.</span></span>

<span data-ttu-id="ea14e-160">Questa esercitazione offre solo un'idea delle possibilità della sicurezza a livello di riga.</span><span class="sxs-lookup"><span data-stu-id="ea14e-160">This tutorial has only scratched the surface of what's possible with RLS.</span></span> <span data-ttu-id="ea14e-161">È ad esempio possibile avere una logica di accesso più avanzata o granulare e archiviare più del solo valore UserId corrente in SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="ea14e-161">For instance, it's possible to have more sophisticated or granular access logic, and it's possible to store more than just the current UserId in the SESSION_CONTEXT.</span></span> <span data-ttu-id="ea14e-162">È anche possibile [integrare la sicurezza a livello di riga con le librerie client del database elastico](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) per supportare partizioni multi-tenant in un livello dati con scalabilità orizzontale.</span><span class="sxs-lookup"><span data-stu-id="ea14e-162">It's also possible to [integrate RLS with the elastic database tools client libraries](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) to support multi-tenant shards in a scale-out data tier.</span></span>

<span data-ttu-id="ea14e-163">Microsoft si impegna anche a migliorare continuamente la sicurezza a livello di riga.</span><span class="sxs-lookup"><span data-stu-id="ea14e-163">Beyond these possibilities, we're also working to make RLS even better.</span></span> <span data-ttu-id="ea14e-164">In caso di domande, idee o suggerimenti, inviare commenti.</span><span class="sxs-lookup"><span data-stu-id="ea14e-164">If you have any questions, ideas, or things you'd like to see, please let us know in the comments.</span></span> <span data-ttu-id="ea14e-165">I commenti e suggerimenti degli utenti sono molto apprezzati.</span><span class="sxs-lookup"><span data-stu-id="ea14e-165">We appreciate your feedback!</span></span>

