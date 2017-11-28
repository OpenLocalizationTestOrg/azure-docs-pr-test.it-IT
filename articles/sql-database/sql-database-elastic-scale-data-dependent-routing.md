---
title: Routing dipendente dai dati con il database SQL di Azure | Documentazione Microsoft
description: "Come usare la classe ShardMapManager nelle app .NET per il routing dipendente dai dati, una funzionalità dei database partizionati del database SQL di Azure"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: cad09e15-5561-4448-aa18-b38f54cda004
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: ddove
ms.openlocfilehash: 6b68bbb0133afd1493acdb58f79f3eeaf6a8d7cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="data-dependent-routing"></a><span data-ttu-id="1f873-103">Routing dipendente dei dati</span><span class="sxs-lookup"><span data-stu-id="1f873-103">Data dependent routing</span></span>
<span data-ttu-id="1f873-104">**Routing dipendente dei dati** è la possibilità di usare i dati in una query per instradare la richiesta a un database appropriato.</span><span class="sxs-lookup"><span data-stu-id="1f873-104">**Data dependent routing** is the ability to use the data in a query to route the request to an appropriate database.</span></span> <span data-ttu-id="1f873-105">Questo costituisce un criterio fondamentale quando si usano database partizionati.</span><span class="sxs-lookup"><span data-stu-id="1f873-105">This is a fundamental pattern when working with sharded databases.</span></span> <span data-ttu-id="1f873-106">Per instradare la richiesta è anche possibile usare il contesto della richiesta stessa, soprattutto se la chiave di partizionamento orizzontale non fa parte della query.</span><span class="sxs-lookup"><span data-stu-id="1f873-106">The request context may also be used to route the request, especially if the sharding key is not part of the query.</span></span> <span data-ttu-id="1f873-107">Ogni query o transazione specifica in un'applicazione che usa il routing dipendente può accedere a un unico database per richiesta.</span><span class="sxs-lookup"><span data-stu-id="1f873-107">Each specific query or transaction in an application using data dependent routing is restricted to accessing a single database per request.</span></span> <span data-ttu-id="1f873-108">Per gli strumenti elastici del database SQL di Azure, il routing viene effettuato con la **[classe ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)** nelle applicazioni ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="1f873-108">For the Azure SQL Database Elastic tools, this routing is accomplished with the **[ShardMapManager class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)** in ADO.NET applications.</span></span>

<span data-ttu-id="1f873-109">Per l'applicazione non è necessario rilevare le diverse stringhe di connessione o i percorsi dei database associati a diverse sezioni di dati nell'ambiente partizionato.</span><span class="sxs-lookup"><span data-stu-id="1f873-109">The application does not need to track various connection strings or DB locations associated with different slices of data in the sharded environment.</span></span> <span data-ttu-id="1f873-110">È [Shard Map Manager](sql-database-elastic-scale-shard-map-management.md) che, quando necessario, apre le connessioni ai database corretti in base ai dati contenuti nella mappa partizioni e al valore della chiave di partizionamento orizzontale, che costituisce la destinazione della richiesta dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1f873-110">Instead, the [Shard Map Manager](sql-database-elastic-scale-shard-map-management.md) opens connections to the correct databases when needed, based on the data in the shard map and the value of the sharding key that is the target of the application’s request.</span></span> <span data-ttu-id="1f873-111">La chiave è in genere *customer_id*, *tenant_id*, *date_key* o un altro identificatore specifico che costituisce un parametro fondamentale della richiesta di database.</span><span class="sxs-lookup"><span data-stu-id="1f873-111">The key is typically the *customer_id*, *tenant_id*, *date_key*, or some other specific identifier that is a fundamental parameter of the database request).</span></span> 

<span data-ttu-id="1f873-112">Per altre informazioni, vedere la pagina relativa [all'aumento del numero di istanze di SQL Server con il routing dipendente dai dati](https://technet.microsoft.com/library/cc966448.aspx).</span><span class="sxs-lookup"><span data-stu-id="1f873-112">For more information, see [Scaling Out SQL Server with Data Dependent Routing](https://technet.microsoft.com/library/cc966448.aspx).</span></span>

## <a name="download-the-client-library"></a><span data-ttu-id="1f873-113">Scaricare la libreria client</span><span class="sxs-lookup"><span data-stu-id="1f873-113">Download the client library</span></span>
<span data-ttu-id="1f873-114">Per ottenere la classe, installare la [libreria client dei database elastici](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span><span class="sxs-lookup"><span data-stu-id="1f873-114">To get the class, install the [Elastic Database Client Library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span></span> 

## <a name="using-a-shardmapmanager-in-a-data-dependent-routing-application"></a><span data-ttu-id="1f873-115">Uso di ShardMapManager in un'applicazione di routing dipendente dai dati</span><span class="sxs-lookup"><span data-stu-id="1f873-115">Using a ShardMapManager in a data dependent routing application</span></span>
<span data-ttu-id="1f873-116">Le applicazioni devono creare un'istanza di **ShardMapManager** durante l'inizializzazione, tramite la chiamata alla factory **[GetSQLShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="1f873-116">Applications should instantiate the **ShardMapManager** during initialization, using the factory call **[GetSQLShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**.</span></span> <span data-ttu-id="1f873-117">In questo esempio, viene eseguita l'inizializzazione sia di **ShardMapManager** che una **ShardMap** specifica in essa contenuta.</span><span class="sxs-lookup"><span data-stu-id="1f873-117">In this example, both a **ShardMapManager** and a specific **ShardMap** that it contains are initialized.</span></span> <span data-ttu-id="1f873-118">Questo esempio illustra i metodi GetSqlShardMapManager e [GetRangeShardMap](https://msdn.microsoft.com/library/azure/dn824173.aspx) .</span><span class="sxs-lookup"><span data-stu-id="1f873-118">This example shows the GetSqlShardMapManager and [GetRangeShardMap](https://msdn.microsoft.com/library/azure/dn824173.aspx) methods.</span></span>

    ShardMapManager smm = ShardMapManagerFactory.GetSqlShardMapManager(smmConnnectionString, 
                      ShardMapManagerLoadPolicy.Lazy);
    RangeShardMap<int> customerShardMap = smm.GetRangeShardMap<int>("customerMap"); 

### <a name="use-lowest-privilege-credentials-possible-for-getting-the-shard-map"></a><span data-ttu-id="1f873-119">Usare credenziali con i privilegi più bassi possibile per ottenere la mappa partizioni</span><span class="sxs-lookup"><span data-stu-id="1f873-119">Use lowest privilege credentials possible for getting the shard map</span></span>
<span data-ttu-id="1f873-120">Se un'applicazione non gestisce direttamente la mappa partizioni, le credenziali usate nel metodo factory devono disporre solo di autorizzazioni di sola lettura per il database della **mappa globale partizioni** .</span><span class="sxs-lookup"><span data-stu-id="1f873-120">If an application is not manipulating the shard map itself, the credentials used in the factory method should have just read-only permissions on the **Global Shard Map** database.</span></span> <span data-ttu-id="1f873-121">Queste credenziali sono in genere diverse da quelle usate per aprire connessioni al gestore delle mappe partizioni.</span><span class="sxs-lookup"><span data-stu-id="1f873-121">These credentials are typically different from credentials used to open connections to the shard map manager.</span></span> <span data-ttu-id="1f873-122">Vedere anche [Credenziali usate per accedere alla libreria client dei database elastici](sql-database-elastic-scale-manage-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="1f873-122">See also [Credentials used to access the Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span> 

## <a name="call-the-openconnectionforkey-method"></a><span data-ttu-id="1f873-123">Chiamare il metodo OpenConnectionForKey</span><span class="sxs-lookup"><span data-stu-id="1f873-123">Call the OpenConnectionForKey method</span></span>
<span data-ttu-id="1f873-124">Il **[metodo ShardMap.OpenConnectionForKey](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)** restituisce una connessione ADO.Net pronta per l'invio di comandi al database appropriato in base al valore del parametro **key**.</span><span class="sxs-lookup"><span data-stu-id="1f873-124">The **[ShardMap.OpenConnectionForKey method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)** returns an ADO.Net connection ready for issuing commands to the appropriate database based on the value of the **key** parameter.</span></span> <span data-ttu-id="1f873-125">Le informazioni sulla partizione vengono memorizzate nella cache dell'applicazione tramite **ShardMapManager**, in modo che in genere tali richieste non comportino una ricerca di database sul database **Mappa globale partizioni**.</span><span class="sxs-lookup"><span data-stu-id="1f873-125">Shard information is cached in the application by the **ShardMapManager**, so these requests do not typically involve a database lookup against the **Global Shard Map** database.</span></span> 

    // Syntax: 
    public SqlConnection OpenConnectionForKey<TKey>(
        TKey key,
        string connectionString,
        ConnectionOptions options
    )


* <span data-ttu-id="1f873-126">Il parametro **key** viene usato come chiave di ricerca nella mappa partizioni per determinare il database appropriato per la richiesta.</span><span class="sxs-lookup"><span data-stu-id="1f873-126">The **key** parameter is used as a lookup key into the shard map to determine the appropriate database for the request.</span></span> 
* <span data-ttu-id="1f873-127">Il parametro **connectionString** viene usato per passare solo le credenziali utente per la connessione specifica.</span><span class="sxs-lookup"><span data-stu-id="1f873-127">The **connectionString** is used to pass only the user credentials for the desired connection.</span></span> <span data-ttu-id="1f873-128">Nel parametro *connectionString* non viene incluso il nome del database o del server, perché il metodo determina il database e il server usando **ShardMap**.</span><span class="sxs-lookup"><span data-stu-id="1f873-128">No database name or server name are included in this *connectionString* since the method will determine the database and server using the **ShardMap**.</span></span> 
* <span data-ttu-id="1f873-129">Il parametro **[connectionOptions](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.connectionoptions.aspx)** deve essere impostato su **ConnectionOptions.Validate** per un ambiente in cui le mappe partizioni possono cambiare e le righe possono passare ad altri database a seguito di operazioni di divisione o unione.</span><span class="sxs-lookup"><span data-stu-id="1f873-129">The **[connectionOptions](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.connectionoptions.aspx)** should be set to **ConnectionOptions.Validate** if an environment where shard maps may change and rows may move to other databases as a result of split or merge operations.</span></span> <span data-ttu-id="1f873-130">Ciò prevede una breve query sulla mappa locale partizioni nel database di destinazione (non sulla mappa globale partizioni) prima che la connessione venga fornita all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1f873-130">This involves a brief query to the local shard map on the target database (not to the global shard map) before the connection is delivered to the application.</span></span> 

<span data-ttu-id="1f873-131">Se la convalida della mappa locale partizioni non riesce (indicando che la cache non è corretta), tramite Gestore mappe partizioni viene eseguita una query sulla mappa globale partizioni per ottenere il nuovo valore corretto per la ricerca, aggiornare la cache e ottenere e restituire la connessione al database appropriato.</span><span class="sxs-lookup"><span data-stu-id="1f873-131">If the validation against the local shard map fails (indicating that the cache is incorrect), the Shard Map Manager will query the global shard map to obtain the new correct value for the lookup, update the cache, and obtain and return the appropriate database connection.</span></span> 

<span data-ttu-id="1f873-132">Usare **ConnectionOptions.None** solo se non sono previste modifiche al mapping delle partizioni mentre l'applicazione è online.</span><span class="sxs-lookup"><span data-stu-id="1f873-132">Use **ConnectionOptions.None** only when shard mapping changes are not expected while an application is online.</span></span> <span data-ttu-id="1f873-133">In tal caso, i valori memorizzati nella cache possono essere considerati sempre corretti e la chiamata di convalida round trip aggiuntiva al database di destinazione può essere tranquillamente ignorata.</span><span class="sxs-lookup"><span data-stu-id="1f873-133">In that case, the cached values can be assumed to always be correct, and the extra round-trip validation call to the target database can be safely skipped.</span></span> <span data-ttu-id="1f873-134">Ciò riduce il traffico del database.</span><span class="sxs-lookup"><span data-stu-id="1f873-134">That reduces database traffic.</span></span> <span data-ttu-id="1f873-135">L'enumerazione **connectionOptions** può anche essere impostata tramite un valore in un file di configurazione per indicare se le modifiche di partizionamento sono o meno previste durante un intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="1f873-135">The **connectionOptions** may also be set via a value in a configuration file to indicate whether sharding changes are expected or not during a period of time.</span></span>  

<span data-ttu-id="1f873-136">Questo esempio usa il valore di una chiave Integer **CustomerID**, tramite un oggetto **ShardMap** denominato **customerShardMap**.</span><span class="sxs-lookup"><span data-stu-id="1f873-136">This example uses the value of an integer key **CustomerID**, using a **ShardMap** object named **customerShardMap**.</span></span>  

    int customerId = 12345; 
    int newPersonId = 4321; 

    // Connect to the shard for that customer ID. No need to call a SqlConnection 
    // constructor followed by the Open method.
    using (SqlConnection conn = customerShardMap.OpenConnectionForKey(customerId, 
        Configuration.GetCredentialsConnectionString(), ConnectionOptions.Validate)) 
    { 
        // Execute a simple command. 
        SqlCommand cmd = conn.CreateCommand(); 
        cmd.CommandText = @"UPDATE Sales.Customer 
                            SET PersonID = @newPersonID 
                            WHERE CustomerID = @customerID"; 

        cmd.Parameters.AddWithValue("@customerID", customerId); 
        cmd.Parameters.AddWithValue("@newPersonID", newPersonId); 
        cmd.ExecuteNonQuery(); 
    }  

<span data-ttu-id="1f873-137">Il metodo **OpenConnectionForKey** restituisce una nuova connessione già aperta al database corretto.</span><span class="sxs-lookup"><span data-stu-id="1f873-137">The **OpenConnectionForKey** method returns a new already-open connection to the correct database.</span></span> <span data-ttu-id="1f873-138">Le connessioni usate in questo modo usufruiscono comunque del pool di connessioni ADO.Net.</span><span class="sxs-lookup"><span data-stu-id="1f873-138">Connections utilized in this way still take full advantage of ADO.Net connection pooling.</span></span> <span data-ttu-id="1f873-139">Fino a quando le transazioni e le richieste possono essere soddisfatti da una partizione alla volta, questa dovrebbe essere l'unica modifica necessaria in un'applicazione che già usa ADO.Net.</span><span class="sxs-lookup"><span data-stu-id="1f873-139">As long as transactions and requests can be satisfied by one shard at a time, this should be the only modification necessary in an application already using ADO.Net.</span></span> 

<span data-ttu-id="1f873-140">È disponibile anche il metodo **[OpenConnectionForKeyAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkeyasync.aspx)** se l'applicazione usa la programmazione asincrona con ADO.Net.</span><span class="sxs-lookup"><span data-stu-id="1f873-140">The **[OpenConnectionForKeyAsync method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkeyasync.aspx)** is also available if your application makes use asynchronous programming with ADO.Net.</span></span> <span data-ttu-id="1f873-141">Il comportamento di tale metodo è l'equivalente del routing dipendente da dati del metodo ADO.Net **[Connection.OpenAsync](https://msdn.microsoft.com/library/hh223688\(v=vs.110\).aspx)**.</span><span class="sxs-lookup"><span data-stu-id="1f873-141">Its behavior is the data dependent routing equivalent of ADO.Net's **[Connection.OpenAsync](https://msdn.microsoft.com/library/hh223688\(v=vs.110\).aspx)** method.</span></span>

## <a name="integrating-with-transient-fault-handling"></a><span data-ttu-id="1f873-142">Integrazione con la gestione degli errori temporanei</span><span class="sxs-lookup"><span data-stu-id="1f873-142">Integrating with transient fault handling</span></span>
<span data-ttu-id="1f873-143">Una procedura consigliata nello sviluppo di applicazioni di accesso ai dati nel cloud consiste nel garantire che gli errori temporanei vengano rilevati dall'app e che le operazioni vengano ripetute più volte prima di generare un errore.</span><span class="sxs-lookup"><span data-stu-id="1f873-143">A best practice in developing data access applications in the cloud is to ensure that transient faults are caught by the app, and that the operations are retried several times before throwing an error.</span></span> <span data-ttu-id="1f873-144">La gestione degli errori temporanei per le applicazioni cloud è illustrata nella pagina relativa alla [gestione degli errori temporanei](https://msdn.microsoft.com/library/dn440719\(v=pandp.60\).aspx).</span><span class="sxs-lookup"><span data-stu-id="1f873-144">Transient fault handling for cloud applications is discussed at [Transient Fault Handling](https://msdn.microsoft.com/library/dn440719\(v=pandp.60\).aspx).</span></span> 

<span data-ttu-id="1f873-145">La gestione degli errori temporanei può coesistere naturalmente con il modello di routing dipendente dai dati.</span><span class="sxs-lookup"><span data-stu-id="1f873-145">Transient fault handling can coexist naturally with the Data Dependent Routing pattern.</span></span> <span data-ttu-id="1f873-146">Il requisito principale consiste nel ripetere l'intera richiesta di accesso ai dati, incluso il blocco **using** che ha ottenuto la connessione di routing dipendente dai dati.</span><span class="sxs-lookup"><span data-stu-id="1f873-146">The key requirement is to retry the entire data access request including the **using** block that obtained the data-dependent routing connection.</span></span> <span data-ttu-id="1f873-147">L'esempio precedente potrebbe essere riscritto come riportato di seguito (notare la modifica evidenziata).</span><span class="sxs-lookup"><span data-stu-id="1f873-147">The example above could be rewritten as follows (note highlighted change).</span></span> 

### <a name="example---data-dependent-routing-with-transient-fault-handling"></a><span data-ttu-id="1f873-148">Esempio: routing dipendente dai dati con gestione degli errori temporanei</span><span class="sxs-lookup"><span data-stu-id="1f873-148">Example - data dependent routing with transient fault handling</span></span>
<pre><code>int customerId = 12345; 
int newPersonId = 4321; 

<span style="background-color:  #FFFF00">Configuration.SqlRetryPolicy.ExecuteAction(() =&gt; </span> 
<span style="background-color:  #FFFF00">    { </span>
        // Connect to the shard for a customer ID. 
        using (SqlConnection conn = customerShardMap.OpenConnectionForKey(customerId,  
        Configuration.GetCredentialsConnectionString(), ConnectionOptions.Validate)) 
        { 
            // Execute a simple command 
            SqlCommand cmd = conn.CreateCommand(); 

            cmd.CommandText = @&quot;UPDATE Sales.Customer 
                            SET PersonID = @newPersonID 
                            WHERE CustomerID = @customerID&quot;; 

            cmd.Parameters.AddWithValue(&quot;@customerID&quot;, customerId); 
            cmd.Parameters.AddWithValue(&quot;@newPersonID&quot;, newPersonId); 
            cmd.ExecuteNonQuery(); 

            Console.WriteLine(&quot;Update completed&quot;); 
        } 
<span style="background-color:  #FFFF00">    }); </span> 
</code></pre>


<span data-ttu-id="1f873-149">I pacchetti necessari per implementare la gestione degli errori temporanei vengono scaricati automaticamente quando si compila l'applicazione esempio dei database elastici.</span><span class="sxs-lookup"><span data-stu-id="1f873-149">Packages necessary to implement transient fault handling are downloaded automatically when you build the elastic database sample application.</span></span> <span data-ttu-id="1f873-150">I pacchetti sono disponibili anche separatamente nella pagina relativa al [blocco di applicazioni di gestione degli errori temporanei nella libreria Enterprise](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/).</span><span class="sxs-lookup"><span data-stu-id="1f873-150">Packages are also available separately at [Enterprise Library - Transient Fault Handling Application Block](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/).</span></span> <span data-ttu-id="1f873-151">Usare la versione 6.0 o successiva.</span><span class="sxs-lookup"><span data-stu-id="1f873-151">Use version 6.0 or later.</span></span> 

## <a name="transactional-consistency"></a><span data-ttu-id="1f873-152">Coerenza delle transazioni</span><span class="sxs-lookup"><span data-stu-id="1f873-152">Transactional consistency</span></span>
<span data-ttu-id="1f873-153">Le proprietà transazionali sono garantite per tutte le operazioni locali rispetto a una partizione.</span><span class="sxs-lookup"><span data-stu-id="1f873-153">Transactional properties are guaranteed for all operations local to a shard.</span></span> <span data-ttu-id="1f873-154">Ad esempio, le transazioni inviate tramite il routing dipendente dai dati vengono eseguite nell'ambito della partizione di destinazione per la connessione.</span><span class="sxs-lookup"><span data-stu-id="1f873-154">For example, transactions submitted through data-dependent routing execute within the scope of the target shard for the connection.</span></span> <span data-ttu-id="1f873-155">Al momento, non sono disponibili funzionalità per l'inserimento di più connessioni in una transazione e pertanto non esistono garanzie transazionale per le operazioni eseguite tra partizioni.</span><span class="sxs-lookup"><span data-stu-id="1f873-155">At this time, there are no capabilities provided for enlisting multiple connections into a transaction, and therefore there are no transactional guarantees for operations performed across shards.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f873-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1f873-156">Next steps</span></span>
<span data-ttu-id="1f873-157">Per disconnettere o riconnettere una partizione, vedere [Uso della classe RecoveryManager per correggere i problemi delle mappe partizioni](sql-database-elastic-database-recovery-manager.md)</span><span class="sxs-lookup"><span data-stu-id="1f873-157">To detach a shard, or to reattach a shard, see [Using the RecoveryManager class to fix shard map problems](sql-database-elastic-database-recovery-manager.md)</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

