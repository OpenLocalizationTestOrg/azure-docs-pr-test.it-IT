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
# <a name="tutorial-web-app-with-a-multi-tenant-database-using-entity-framework-and-row-level-security"></a>Esercitazione: App Web con database multi-tenant che usa Entity Framework e la sicurezza a livello di riga
Questa esercitazione viene illustrato come toobuild multi-tenant web app con una "[database condiviso, schema condiviso](https://msdn.microsoft.com/library/aa479086.aspx)" modello di tenancy, mediante Entity Framework e [sicurezza a livello di riga](https://msdn.microsoft.com/library/dn765131.aspx). In questo modello un database singolo contiene dati per molti tenant e ogni riga in ogni tabella è associata a un "ID tenant". Sicurezza a livello di riga (riga), una nuova funzionalità per il Database di SQL Azure, viene utilizzato tooprevent tenant l'accesso ai dati reciproci. Ciò richiede solo una singola, applicazione di toohello di modifica di piccole dimensioni. Centralizzando hello tenant accesso logica all'interno di database hello stesso, riga semplifica il codice dell'applicazione hello e riduce il rischio di hello accidentale di perdita di dati tra i tenant.

Iniziamo con una semplice applicazione Contact Manager hello da [crea un'applicazione ASP.NET MVP con l'autenticazione e i database di SQL Server e distribuire App servizio tooAzure](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md). Diritto a questo punto, un'applicazione hello consente tutti gli utenti (tenant) toosee tutti i contatti:

![Applicazione Contact Manager prima dell'abilitazione della sicurezza a livello di riga](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-Before.png)

Con poche modifiche di piccola, si verrà aggiunto il supporto per multi-tenancy, in modo che gli utenti siano in grado di toosee solo hello i contatti che appartengono toothem.

## <a name="step-1-add-an-interceptor-class-in-hello-application-tooset-hello-sessioncontext"></a>Passaggio 1: Aggiungere una classe dell'intercettore in hello tooset di applicazione hello SESSION_CONTEXT
È presente una modifica applicazione dobbiamo toomake. Perché tutti gli utenti dell'applicazione di connettersi utilizzando database toohello hello stessa stringa di connessione (ad esempio stesso account di accesso SQL), non è attualmente possibile per cui l'utente deve filtrare per un tooknow di criteri di riga. Questo approccio è molto comune nelle applicazioni web perché consente di pool di connessioni efficiente, ma significa che è necessario un altro modo tooidentify hello utente corrente dell'applicazione all'interno del database hello. Hello soluzione è toohave hello applicazione set una coppia chiave-valore per hello UserId corrente in hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) immediatamente dopo l'apertura di una connessione, prima di eseguire le query. SESSION_CONTEXT è un archivio chiave-valore con ambito sessione e i criteri di riga verranno utilizzati hello in essa archiviati UserId tooidentify utente corrente di hello.

Si aggiungerà un [intercettore](https://msdn.microsoft.com/data/dn469464.aspx) (in particolare, un [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), una nuova funzionalità in Entity Framework (EF) 6, tooautomatically set hello UserId corrente in hello SESSION_CONTEXT eseguendo un Istruzione T-SQL ogni volta che EF apre una connessione.

1. Aprire il progetto di ContactManager hello in Visual Studio.
2. Pulsante destro del mouse sulla cartella Modelli hello in hello Esplora soluzioni e scegliere Aggiungi > classe.
3. Nome nuova classe hello "SessionContextInterceptor.cs" e fare clic su Aggiungi.
4. Sostituire il contenuto di hello del SessionContextInterceptor.cs con hello seguente codice.

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

Che è richiesta di modifica di hello unica applicazione. Vado avanti e compilare e pubblicare un'applicazione hello.

## <a name="step-2-add-a-userid-column-toohello-database-schema"></a>Passaggio 2: Aggiungere uno schema di database toohello colonna ID utente
Successivamente, è necessario un tooassociate tabella contatti di UserId colonna toohello tooadd ogni riga a un utente (tenant). Si comporta la modifica dello schema hello direttamente nel database di hello, in modo che non abbiamo tooinclude questo campo nel nostro modello di dati di Entity Framework.

Connessione diretta, toohello database utilizzando SQL Server Management Studio o Visual Studio e quindi eseguire hello T-SQL seguente:

```
ALTER TABLE Contacts ADD UserId nvarchar(128)
    DEFAULT CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
```

Aggiunge una tabella di contatti toohello colonna ID utente. Utilizziamo hello hello nvarchar (128) dati tipo toomatch che degli ID utente archiviati nella tabella AspNetUsers hello e creare un vincolo DEFAULT che verrà impostato automaticamente hello UserId per le righe appena inserite toobe hello UserId attualmente archiviati nel SESSION_CONTEXT.

Tabella hello ora simile al seguente:

![Tabella Contacts SSMS](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-Contacts.png)

Quando vengono creati nuovi contatti, essi verrà assegnati automaticamente hello correggere UserId. A scopo dimostrativo, tuttavia, si assegna alcuni di questi tooan contatti esistenti utente esistente.

Se sono stati creati alcuni utenti in un'applicazione hello già (ad esempio, utilizzo locale, Google o Facebook account), verranno visualizzati nella tabella AspNetUsers hello. Schermata di hello riportata di seguito, prevede un solo utente finora.

![Tabella AspNetUsers SSMS](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-AspNetUsers.png)

Hello copia Id per user1@contoso.come incollarlo in istruzione hello T-SQL riportata di seguito. Eseguire questa istruzione tooassociate tre, di hello contatti con l'ID utente.

```
UPDATE Contacts SET UserId = '19bc9b0d-28dd-4510-bd5e-d6b6d445f511'
WHERE ContactId IN (1, 2, 5)
```

## <a name="step-3-create-a-row-level-security-policy-in-hello-database"></a>Passaggio 3: Creare un criterio di sicurezza a livello di riga nel database di hello
passaggio finale Hello è toocreate un criterio di sicurezza che utilizza hello UserId SESSION_CONTEXT tooautomatically filtro hello risultati restituiti dalle query.

Mentre il database toohello ancora connessi, eseguire hello T-SQL seguente:

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

Questo codice esegue tre operazioni. Viene innanzitutto creato un nuovo schema come procedura consigliata per la centralizzazione e limitare gli oggetti di access toohello di riga. Successivamente, viene creata una funzione di predicato che restituisce '1' quando hello ID utente di una riga corrisponde hello UserId in SESSION_CONTEXT. Infine, viene creato un criterio di sicurezza che aggiunga questa funzione come predicato di un filtro e di blocco per la tabella Contacts hello. predicato del filtro Hello determina tooreturn query solo le righe a cui appartengano l'utente corrente toohello predicato di blocco hello funge da un'applicazione di hello salvaguardia tooprevent mai accidentalmente inserire una riga per l'utente errato hello.

Eseguire un'applicazione hello e accedere come user1@contoso.com. Questo utente viene visualizzata solo i contatti di hello è assegnato toothis UserId:

![Applicazione Contact Manager prima dell'abilitazione della sicurezza a livello di riga](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-After.png)

toovalidate questo ulteriormente, provare a registrare un nuovo utente. I contatti, non verranno visualizzati perché non sono stati assegnati toothem. Se si crea un nuovo contatto, sarà assegnato toothem e solo saranno in grado di toosee è.

## <a name="next-steps"></a>Passaggi successivi
L'operazione è terminata. Hello semplice contattare Manager web app è stata convertita in un multi-tenant, uno in cui ogni utente dispone di un proprio elenco di contatti. Tramite la sicurezza a livello di riga, è stata evitare complessità hello di applicare la logica di accesso ai tenant nel codice dell'applicazione. La trasparenza consente toofocus applicazione hello sul problema aziendale reale di hello in questione e riduce inoltre il rischio di hello della perdita accidentale di dati come un'applicazione hello codebase aumenta.

In questa esercitazione dispone solo area di hello graffiato di ciò che è possibile con una riga. Ad esempio, è possibile toohave più sofisticate o logica di accesso granulare e toostore possibili è molto più hello UserId corrente in hello SESSION_CONTEXT. È inoltre possibile troppo[integrare di riga con le librerie client gli strumenti di database elastico hello](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) toosupport partizioni di multi-tenant in un livello di dati di scalabilità orizzontale.

Oltre a queste possibilità, stiamo lavorando anche toomake ancora migliore di riga. Se si dispone di domande, suggerimenti o operazioni si desidera toosee, Saremmo lieti di sapere nei commenti hello. I commenti e suggerimenti degli utenti sono molto apprezzati.

