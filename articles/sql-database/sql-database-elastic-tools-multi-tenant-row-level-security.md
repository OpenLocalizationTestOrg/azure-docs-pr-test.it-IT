---
title: applicazioni aaaMulti tenant con strumenti di database elastico e la sicurezza a livello di riga
description: Informazioni su come gli strumenti di database elastico toouse assieme a livello di riga sicurezza toobuild un'applicazione con un livello di dati estremamente scalabile in Database SQL di Azure che supporta le partizioni di multi-tenant.
metakeywords: azure sql database elastic tools multi tenant row level security rls
services: sql-database
documentationcenter: 
manager: jhubbard
author: tmullaney
ms.assetid: e72d3cfe-e9be-4326-b776-9c6d96c0a18e
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: thmullan;torsteng
ms.openlocfilehash: e00076a8db4a295374993aedd49f2318bd4d701d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="multi-tenant-applications-with-elastic-database-tools-and-row-level-security"></a>Applicazioni multi-tenant con strumenti di database elastici e sicurezza a livello di riga
[Strumenti di database elastico](sql-database-elastic-scale-get-started.md) e [sicurezza a livello di riga](https://msdn.microsoft.com/library/dn765131) offre un potente set di funzionalità per il livello dati hello di un'applicazione multi-tenant con Database SQL di Azure di ridimensionamento in modo flessibile ed efficiente. Vedere [Schemi progettuali per applicazioni SaaS multi-tenant con il database SQL di Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md) . 

Questo articolo illustra come toouse questi toobuild insieme di tecnologie un'applicazione con un livello di dati estremamente scalabile che supporta le partizioni di multi-tenant, usando **ADO.NET SqlClient** e/o **diEntityFramework**.  

* **Strumenti di database elastico** consente agli sviluppatori tooscale orizzontalmente il livello dati hello di un'applicazione tramite procedure consigliate di partizionamento orizzontale standard di settore tramite un set di librerie .NET e i modelli di servizio di Azure. La gestione di partizioni con la libreria Client di Database elastico hello consente di automatizzare e semplificare molte attività hello infrastrutturale principale prevede in genere associata con il partizionamento orizzontale. 
* **Sicurezza a livello di riga** consente dati toostore gli sviluppatori per più tenant in hello stesso utilizzando toofilter di criteri di sicurezza le righe che non appartengono tenant toohello esegue una query di database. Centralizzando la logica di accesso con una riga all'interno del database hello, piuttosto che in un'applicazione hello, semplifica la manutenzione e riduce il rischio di hello di errore come un'applicazione codebase aumenta. 

Utilizzo di queste funzionalità insieme, un'applicazione può trarre vantaggio dal miglioramenti di risparmio e l'efficienza dei costi per l'archiviazione dei dati per più tenant in hello stesso database di partizione. Hello contemporaneamente, un'applicazione ancora ha toooffer flessibilità hello isolata, single-tenant partizioni per i tenant "premium" che richiedono più restrittive garantisce prestazioni poiché le partizioni di multi-tenant non garantiscono la distribuzione delle risorse di uguale tra tenant.  

In breve, hello della libreria client di database elastico [routing dipendente dai dati](sql-database-elastic-scale-data-dependent-routing.md) API automaticamente la connessione di database di partizione corretta toohello tenant che contiene la chiave di partizionamento orizzontale (in genere un "TenantId"). Una volta connesso, un criterio di sicurezza di riga all'interno del database hello assicura che i tenant possano accedere solo le righe che contengono i relativi ID tenant. Si presuppone che tutte le tabelle includono un tooindicate colonna TenantId quali righe appartengono tooeach tenant. 

![Architettura delle applicazioni di blog][1]

## <a name="download-hello-sample-project"></a>Scaricare il progetto di esempio hello
### <a name="prerequisites"></a>Prerequisiti
* Utilizzare Visual Studio (2012 o versione successiva) 
* Creare tre database SQL di Azure 
* Scaricare il progetto di esempio: [Strumenti di database elastici per SQL di Azure - Partizioni multi-tenant](http://go.microsoft.com/?linkid=9888163)
  * Immettere le informazioni di hello per i database all'inizio di hello della **Program.cs** 

Questo progetto estende hello quello descritto in [elastico strumenti DB per SQL Azure - integrazione di Entity Framework](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) aggiungendo il supporto per i database di partizione multi-tenant. Viene creata una semplice applicazione console per la creazione di blog e post, con quattro tenant e due database di partizione multi-tenant, come illustrato nell'hello diagramma. 

Compilare ed eseguire un'applicazione hello. Questo verrà avviare Gestore mappe partizioni degli strumenti di database elastico hello e hello esecuzione test seguenti: 

1. Utilizzando Entity Framework e LINQ, creare un nuovo blog e quindi visualizzare tutti i blog per ciascun tenant
2. Utilizzando ADO.NET SqlClient, visualizzare tutti i blog per un tenant
3. Provare a tooinsert blog per hello tenant errato tooverify che viene generato un errore  

Si noti che poiché riga non è ancora stato abilitato nel database di partizione hello, ciascuno di questi test rivela un problema: i tenant sono in grado di toosee blog che non appartengono toothem e un'applicazione hello non viene impedita l'inserimento di un blog per tenant errato hello. Hello parte restante di questo articolo viene descritto come tooresolve questi problemi tramite l'applicazione del tenant isolamento con una riga. Sono disponibili due passaggi: 

1. **Livello applicazione**: modificare il codice dell'applicazione hello tooalways set hello TenantId corrente in hello SESSION_CONTEXT dopo l'apertura di una connessione. progetto di esempio Hello ha già eseguito questa operazione. 
2. **Livello dati**: creare un criterio di sicurezza di riga in ogni toofilter di database di partizione in base a hello tenantid all'interno di righe archiviate in SESSION_CONTEXT. Sarà necessaria toodo per ognuno dei database di partizione, in caso contrario le righe in multi-tenant partizioni non verranno filtrate. 

## <a name="step-1-application-tier-set-tenantid-in-hello-sessioncontext"></a>Livello di applicazione al passaggio 1): impostare TenantId in hello SESSION_CONTEXT
Dopo la connessione database di partizione tooa utilizzando i dati della libreria di hello database elastico client che dipendenti API di routine, un'applicazione hello è ancora necessario database hello tootell quali TenantId utilizza la connessione in modo che un criterio di sicurezza di riga è possibile filtrare le righe appartenenti tooother tenant. Hello toopass consigliato queste informazioni sono toostore hello TenantId corrente per la connessione in hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx). (Nota: in alternativa, è possibile utilizzare [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx), ma SESSION_CONTEXT è preferibile perché è più facile toouse, restituisce NULL per impostazione predefinita e supporta le coppie chiave-valore.)

### <a name="entity-framework"></a>Entity Framework
Per le applicazioni usando Entity Framework, hello approccio più semplice è hello tooset SESSION_CONTEXT all'interno di hello ElasticScaleContext sostituzione descritto in [Routing dipendente dai dati tramite EF DbContext](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext). Prima di restituire connessione hello negoziata mediante il routing dipendente dai dati, è semplicemente creare ed eseguire un SqlCommand che imposta 'TenantId' in hello SESSION_CONTEXT toohello shardingKey specificato per tale connessione. In questo modo, è necessario solo codice toowrite una volta tooset hello SESSION_CONTEXT. 

```
// ElasticScaleContext.cs 
// ... 
// C'tor for data dependent routing. This call will open a validated connection routed toohello proper 
// shard by hello shard map manager. Note that hello base class c'tor call will fail for an open connection 
// if migrations need toobe done and SQL credentials are used. This is hello reason for hello  
// separation of c'tors into hello DDR case (this c'tor) and hello internal c'tor for new shards. 
public ElasticScaleContext(ShardMap shardMap, T shardingKey, string connectionStr)
    : base(OpenDDRConnection(shardMap, shardingKey, connectionStr), true /* contextOwnsConnection */)
{
}

public static SqlConnection OpenDDRConnection(ShardMap shardMap, T shardingKey, string connectionStr)
{
    // No initialization
    Database.SetInitializer<ElasticScaleContext<T>>(null);

    // Ask shard map toobroker a validated connection for hello given key
    SqlConnection conn = null;
    try
    {
        conn = shardMap.OpenConnectionForKey(shardingKey, connectionStr, ConnectionOptions.Validate);

        // Set TenantId in SESSION_CONTEXT tooshardingKey tooenable Row-Level Security filtering
        SqlCommand cmd = conn.CreateCommand();
        cmd.CommandText = @"exec sp_set_session_context @key=N'TenantId', @value=@shardingKey";
        cmd.Parameters.AddWithValue("@shardingKey", shardingKey);
        cmd.ExecuteNonQuery();

        return conn;
    }
    catch (Exception)
    {
        if (conn != null)
        {
            conn.Dispose();
        }

        throw;
    }
} 
// ... 
```

Ora viene impostata automaticamente hello SESSION_CONTEXT hello specificato TenantId ogni volta che viene richiamato ElasticScaleContext: 

```
// Program.cs 
SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() => 
{   
    using (var db = new ElasticScaleContext<int>(sharding.ShardMap, tenantId, connStrBldr.ConnectionString))   
    {     
        var query = from b in db.Blogs
                    orderby b.Name
                    select b;

        Console.WriteLine("All blogs for TenantId {0}:", tenantId);     
        foreach (var item in query)     
        {       
            Console.WriteLine(item.Name);     
        }   
    } 
}); 
```

### <a name="adonet-sqlclient"></a>ADO.NET SqlClient
Per applicazioni che usano ADO.NET SqlClient, hello approccio migliore consiste toocreate una funzione wrapper intorno ShardMap.OpenConnectionForKey() che imposta automaticamente 'TenantId' hello SESSION_CONTEXT toohello correggere TenantId prima di restituire un connessione. tooensure che SESSION_CONTEXT è sempre impostato, è consigliabile aprire solo le connessioni utilizzando questa funzione wrapper.

```
// Program.cs
// ...

// Wrapper function for ShardMap.OpenConnectionForKey() that automatically sets SESSION_CONTEXT with hello correct
// tenantId before returning a connection. As a best practice, you should only open connections using this 
// method tooensure that SESSION_CONTEXT is always set before executing a query.
public static SqlConnection OpenConnectionForTenant(ShardMap shardMap, int tenantId, string connectionStr)
{
    SqlConnection conn = null;
    try
    {
        // Ask shard map toobroker a validated connection for hello given key
        conn = shardMap.OpenConnectionForKey(tenantId, connectionStr, ConnectionOptions.Validate);

        // Set TenantId in SESSION_CONTEXT tooshardingKey tooenable Row-Level Security filtering
        SqlCommand cmd = conn.CreateCommand();
        cmd.CommandText = @"exec sp_set_session_context @key=N'TenantId', @value=@shardingKey";
        cmd.Parameters.AddWithValue("@shardingKey", tenantId);
        cmd.ExecuteNonQuery();

        return conn;
    }
    catch (Exception)
    {
        if (conn != null)
        {
            conn.Dispose();
        }

        throw;
    }
}

// ...

// Example query via ADO.NET SqlClient
// If row-level security is enabled, only Tenant 4's blogs will be listed
SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() =>
{
    using (SqlConnection conn = OpenConnectionForTenant(sharding.ShardMap, tenantId4, connStrBldr.ConnectionString))
    {
        SqlCommand cmd = conn.CreateCommand();
        cmd.CommandText = @"SELECT * FROM Blogs";

        Console.WriteLine("--\nAll blogs for TenantId {0} (using ADO.NET SqlClient):", tenantId4);
        SqlDataReader reader = cmd.ExecuteReader();
        while (reader.Read())
        {
            Console.WriteLine("{0}", reader["Name"]);
        }
    }
});

```

## <a name="step-2-data-tier-create-row-level-security-policy"></a>Passaggio 2) Livello dati: creare criteri di sicurezza a livello di riga
### <a name="create-a-security-policy-toofilter-hello-rows-each-tenant-can-access"></a>Creare un hello toofilter criteri di sicurezza ogni tenant può accedere alle righe
Ora che è l'impostazione SESSION_CONTEXT con un'applicazione hello hello TenantId corrente prima dell'esecuzione di query, è possibile filtrare le query ed escludere le righe che contengono un ID diverso tenant un criterio di sicurezza di riga.  

RIGA viene implementato in T-SQL: una funzione definita dall'utente definisce la logica di accesso hello e un criterio di sicurezza associa questo numero tooany funzione delle tabelle. Per questo progetto, la funzione hello semplicemente verificherà che hello applicazione (anziché un altro utente SQL) è connesso toohello database, e hello tenantid all'interno di una determinata riga corrisponde a tale hello 'TenantId' archiviato in hello SESSION_CONTEXT. Un predicato del filtro consentirà di righe che soddisfano queste condizioni toopass tramite filtro hello per le query SELECT, UPDATE e DELETE e un predicato block che impedisce le righe che violano tali condizioni viene inserita o aggiornata. Se SESSION_CONTEXT non è stato impostato, verrà restituito che null e nessuna riga sarà visibile o è in grado di toobe inserito. 

tooenable di riga, hello T-SQL seguente in tutte le partizioni utilizzando entrambi Visual Studio (SSDT), SQL Server Management Studio, eseguire o script di PowerShell incluso nel progetto hello hello (o se si utilizza [i processi di Database elastico](sql-database-elastic-jobs-overview.md), è possibile utilizzare tooautomate esecuzione Questo T-SQL in tutte le partizioni): 

```
CREATE SCHEMA rls -- separate schema tooorganize RLS objects 
GO

CREATE FUNCTION rls.fn_tenantAccessPredicate(@TenantId int)     
    RETURNS TABLE     
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS fn_accessResult          
        WHERE DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('dbo') -- hello user in your application’s connection string (dbo is only for demo purposes!)         
        AND CAST(SESSION_CONTEXT(N'TenantId') AS int) = @TenantId
GO

CREATE SECURITY POLICY rls.tenantAccessPolicy
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Blogs,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Blogs,
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Posts,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Posts
GO 
```

> [!TIP]
> Per i progetti più complessi che richiedono il predicato hello tooadd su centinaia di tabelle, è possibile utilizzare una stored procedure di supporto che genera automaticamente i criteri di sicurezza aggiungendo un predicato in tutte le tabelle in uno schema. Vedere [tabelle tooall Applica protezione a livello di riga - script di supporto (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script).  
> 
> 

Ora se si esegue l'applicazione di esempio hello nuovamente, i tenant verranno toosee in grado solo le righe che appartengono toothem. Inoltre, un'applicazione hello non è possibile inserire le righe che appartengono tootenants diverso da quello hello toohello attualmente connessa una partizione e non è possibile aggiornare righe visibili toohave un ID diverso tenant. Se un'applicazione hello tenta di toodo, verrà generato un DbUpdateException.

Se si aggiunge una nuova tabella in un secondo momento, semplicemente ALTER hello criteri di sicurezza e aggiungere i predicati di filtro e di blocco nella nuova tabella hello: 

```
ALTER SECURITY POLICY rls.tenantAccessPolicy     
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable
GO 
```

### <a name="add-default-constraints-tooautomatically-populate-tenantid-for-inserts"></a>Aggiungere l'impostazione predefinita i vincoli tooautomatically popolare TenantId per inserimenti
È possibile inserire un valore predefinito vincolo su ogni tooautomatically tabella popolare hello TenantId con hello valore attualmente archiviato in SESSION_CONTEXT durante l'inserimento di righe. ad esempio: 

```
-- Create default constraints tooauto-populate TenantId with hello value of SESSION_CONTEXT for inserts 
ALTER TABLE Blogs     
    ADD CONSTRAINT df_TenantId_Blogs      
    DEFAULT CAST(SESSION_CONTEXT(N'TenantId') AS int) FOR TenantId 
GO

ALTER TABLE Posts     
    ADD CONSTRAINT df_TenantId_Posts      
    DEFAULT CAST(SESSION_CONTEXT(N'TenantId') AS int) FOR TenantId 
GO 
```

Ora applicazione hello non è necessario un ID tenant toospecify durante l'inserimento di righe: 

```
SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() => 
{   
    using (var db = new ElasticScaleContext<int>(sharding.ShardMap, tenantId, connStrBldr.ConnectionString))
    {
        var blog = new Blog { Name = name }; // default constraint sets TenantId automatically     
        db.Blogs.Add(blog);     
        db.SaveChanges();   
    } 
}); 
```

> [!NOTE]
> Se si utilizzano vincoli predefiniti per un progetto Entity Framework, si consiglia di non includere colonne TenantId hello nel modello di dati Entity Framework. Questo avviene perché le query di Entity Framework forniscono automaticamente i valori predefiniti che eseguirà l'override vincoli predefiniti hello creati in T-SQL che utilizzano SESSION_CONTEXT. vincoli predefiniti toouse in hello il progetto di esempio, ad esempio, è necessario rimuovere TenantId da DataClasses.cs (e di eseguire Add-Migration nella Console di gestione pacchetti hello) e tooensure utilizzare T-SQL che hello campo esiste solo nelle tabelle di database hello. In questo modo, Entity Framework non fornirà automaticamente valori predefiniti errati durante l'inserimento dei dati. 
> 
> 

### <a name="optional-enable-a-superuser-tooaccess-all-rows"></a>(Facoltativo) Abilitare un tooaccess "avanzato" tutte le righe
Alcune applicazioni potrebbe essere necessario toocreate un utente "avanzato" che può accedere a tutte le righe, ad esempio, in ordine tooenable creazione di report tra tutti i tenant in tutte le partizioni o di operazioni di suddivisione/unione tooperform su partizioni che comportano lo spostamento di righe tenant tra database. tooenable, è necessario creare un nuovo utente SQL ("avanzato" in questo esempio) in ogni database di partizione. Quindi, modificare i criteri di sicurezza hello con una nuova funzione di predicato che consente questa tooaccess utente tutte le righe:

```
-- New predicate function that adds superuser logic
CREATE FUNCTION rls.fn_tenantAccessPredicateWithSuperUser(@TenantId int)
    RETURNS TABLE
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS fn_accessResult 
        WHERE 
        (
            DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('dbo') -- note, should not be dbo!
            AND CAST(SESSION_CONTEXT(N'TenantId') AS int) = @TenantId
        ) 
        OR
        (
            DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('superuser')
        )
GO

-- Atomically swap in hello new predicate function on each table
ALTER SECURITY POLICY rls.tenantAccessPolicy
    ALTER FILTER PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Blogs,
    ALTER BLOCK PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Blogs,
    ALTER FILTER PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Posts,
    ALTER BLOCK PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Posts
GO
```


### <a name="maintenance"></a>Manutenzione 
* **Aggiunta di nuove partizioni**: È necessario eseguire tooenable script hello T-SQL e su eventuali nuove partizioni, in caso contrario le query su queste partizioni non verranno filtrate.
* **Aggiunta di nuove tabelle**: È necessario aggiungere un filtro e bloccare i criteri di sicurezza toohello predicato in tutte le partizioni, ogni volta che viene creata una nuova tabella, in caso contrario le query su una nuova tabella hello non verranno filtrate. Si possono essere automatizzata tramite un trigger DDL, come descritto in [Applica protezione a livello di riga toonewly creato automaticamente tabelle (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx).

## <a name="summary"></a>Riepilogo
Strumenti di database elastico e sicurezza a livello di riga possono essere utilizzati insieme tooscale orizzontalmente il livello dati di un'applicazione con supporto per partizioni sia multi-tenant e single-tenant. Partizioni di multi-tenant possono essere utilizzato toostore dati in modo più efficiente (in particolare nei casi in cui un numero elevato di tenant hanno solo poche righe di dati), durante single-tenant partizioni possono essere utilizzati toosupport premium tenant con prestazioni e l'isolamento più restrittivo requisiti.  Per altre informazioni, vedere [Sicurezza a livello di riga](https://msdn.microsoft.com/library/dn765131). 

## <a name="additional-resources"></a>Risorse aggiuntive
* [Che cos'è un pool elastico di Azure?](sql-database-elastic-pool.md)
* [Aumento del numero di istanze con il database SQL di Azure](sql-database-elastic-scale-introduction.md)
* [Schemi progettuali per applicazioni SaaS multi-tenant con il database SQL di Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* [Authentication in multitenant apps, using Azure AD and OpenID Connect](../guidance/guidance-multitenant-identity-authenticate.md)
* [Informazioni sull'applicazione Tailspin Surveys](../guidance/guidance-multitenant-identity-tailspin.md)

## <a name="questions-and-feature-requests"></a>Domande e richieste di funzionalità
Per domande, rivolgersi toous su hello [forum di Database SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) e per le richieste di funzionalità, aggiungerli toohello [forum sul feedback su Database SQL](https://feedback.azure.com/forums/217321-sql-database/).

<!--Image references-->
[1]: ./media/sql-database-elastic-tools-multi-tenant-row-level-security/blogging-app.png
<!--anchors-->


