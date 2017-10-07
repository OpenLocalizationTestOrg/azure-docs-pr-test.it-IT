---
title: aaaHow tooUse Cache Redis di Azure | Documenti Microsoft
description: Informazioni su come tooimprove hello prestazioni delle applicazioni Azure con Cache Redis di Azure
services: redis-cache,app-service
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: c502f74c-44de-4087-8303-1b1f43da12d5
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/27/2017
ms.author: sdanie
ms.openlocfilehash: 763d70c10972eec9a1885969e8da5bf1c4084727
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache"></a>La modalità di Cache Redis di Azure di tooUse
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.JS](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Questa guida illustra la modalità di avvio utilizzando tooget **Cache Redis di Azure**. Cache Redis di Microsoft Azure si basa su hello open source comuni Cache Redis. Consente di accedere a tooa sicura e dedicata cache Redis, gestita da Microsoft. Una cache creata usando Cache Redis di Azure sarà accessibile da qualsiasi applicazione all'interno di Microsoft Azure.

Cache Redis di Microsoft Azure è disponibile in hello livelli seguenti:

* **Basic**: singolo nodo. Più dimensioni too53 GB.
* **Standard**: principale/replica a due nodi. Più dimensioni too53 GB. Contratti di servizio del 99,9%.
* **Premium** : due nodi primario/Replica con backup too10 partizioni. Più dimensioni che vanno da 6 GB too530 GB. Supporto per tutte le funzionalità del piano Standard e altre, tra cui [cluster Redis](cache-how-to-premium-clustering.md), [persistenza Redis](cache-how-to-premium-persistence.md) e [Rete virtuale di Azure](cache-how-to-premium-vnet.md). Contratti di servizio del 99,9%.

Ogni livello presenta differenze in termini di funzionalità e prezzi. Per informazioni sui prezzi, vedere [Dettagli prezzi del servizio Cache][Cache Pricing Details].

Questa guida illustra come hello toouse [stackexchange. Redis] [ StackExchange.Redis] client utilizzando C\# codice. Hello scenari trattati includono **creazione e configurazione di una cache**, **configurazione i client della cache**, e **aggiungendo e rimuovendo oggetti dalla cache di hello**. Per altre informazioni sull'uso di Cache Redis di Azure, vedere i [Passaggi successivi][Next Steps]. Per un'esercitazione dettagliata della creazione di app web con Cache Redis di MVC ASP.NET, vedere [come un'App Web in Cache Redis toocreate](cache-web-app-howto.md).

<a name="getting-started-cache-service"></a>

## <a name="get-started-with-azure-redis-cache"></a>Introduzione all'uso di Cache Redis di Azure
Iniziare a usare Cache Redis di Azure è semplice. tooget avviato, per eseguire il provisioning e configurare una cache. Successivamente, configurare i client della cache di hello consentire l'accesso della cache di hello. Dopo aver configurati i client della cache di hello, è possibile iniziare loro utilizzo.

* [Creare una cache di hello][Create hello cache]
* [Configurare i client della cache di hello][Configure hello cache clients]

<a name="create-cache"></a>

## <a name="create-a-cache"></a>Creare una cache
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

### <a name="tooaccess-your-cache-after-its-created"></a>tooaccess viene creata la cache dopo di esso
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

Per ulteriori informazioni sulla configurazione di cache, vedere [come tooconfigure Cache Redis di Azure](cache-configure.md).

<a name="NuGet"></a>

## <a name="configure-hello-cache-clients"></a>Configurare i client della cache di hello
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

Dopo aver configurato il progetto client per la memorizzazione nella cache, è possibile utilizzare tecniche di hello descritte nelle seguenti sezioni per l'utilizzo con la cache di hello.

<a name="working-with-caches"></a>

## <a name="working-with-caches"></a>Utilizzo delle cache
Hello in questa sezione viene descritta la modalità di attività comuni di tooperform con Cache.

* [La connessione della cache toohello][Connect toohello cache]
* [Aggiungere e recuperare gli oggetti dalla cache di hello][Add and retrieve objects from hello cache]
* [Utilizzo di oggetti .NET nella cache di hello](#work-with-net-objects-in-the-cache)

<a name="connect-to-cache"></a>

## <a name="connect-toohello-cache"></a>La connessione della cache toohello
lavoro tooprogrammatically con una cache, è necessario che una cache toohello di riferimento. Aggiungere hello seguente toohello superiore di qualsiasi file da cui si desidera toouse hello Stackexchange client tooaccess Cache Redis di Azure.

    using StackExchange.Redis;

> [!NOTE]
> client stackexchange. Redis Hello richiede .NET Framework 4 o versione successiva.
> 
> 

Hello toohello connessione Cache Redis di Azure è gestita da hello `ConnectionMultiplexer` classe. Questa classe deve essere condivisa e riutilizzabile nell'applicazione client e non è necessario creare in ogni singola operazione toobe. 

tooconnect tooan Cache Redis di Azure e restituito un'istanza di un oggetto connesso `ConnectionMultiplexer`, chiamata hello statico `Connect` (metodo) e passare hello memorizzano nella cache dell'endpoint e la chiave. Utilizzo chiave hello generata dal portale di Azure come parametro di password hello hello.

    ConnectionMultiplexer connection = ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");

> [!IMPORTANT]
> Avviso: non archiviare mai le credenziali nel codice sorgente. tookeep questo semplice esempio, sono illustrati nel codice sorgente hello. Vedere [come le stringhe dell'applicazione e lavoro di stringhe di connessione] [ How Application Strings and Connection Strings Work] per informazioni su come toostore credenziali.
> 
> 

Se non si desidera toouse SSL, impostare `ssl=false` oppure omettere hello `ssl` parametro.

> [!NOTE]
> porta non SSL Hello è disabilitata per impostazione predefinita per le nuove cache. Per istruzioni sull'abilitazione di porta non SSL hello, vedere [porte di accesso](cache-configure.md#access-ports).
> 
> 

Un approccio toosharing un `ConnectionMultiplexer` istanza dell'applicazione è toohave una proprietà statica che restituisce un'istanza connessa, simile toohello esempio seguente. Questo approccio fornisce un modo thread-safe di tooinitialize solo una singola connessione `ConnectionMultiplexer` istanza. In questi esempi `abortConnect` è toofalse set, il che significa che la chiamata hello ha esito positivo anche se non viene stabilita una toohello connessione Cache Redis di Azure. Una caratteristica fondamentale di `ConnectionMultiplexer` è che viene ripristinata automaticamente cache toohello connettività quando vengono risolte i problemi di rete hello o altre cause.

    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        return ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");
    });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

Per altre informazioni sulle opzioni di configurazione avanzate per la connessione, vedere [Modello di configurazione di StackExchange.Redis][StackExchange.Redis configuration model].

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

Una volta stabilita la connessione hello, restituire un database di riferimento toohello redis cache dal chiamante hello `ConnectionMultiplexer.GetDatabase` metodo. oggetto Hello restituito da hello `GetDatabase` metodo è un oggetto passthrough semplice e non è necessario toobe archiviati.

    // Connection refers tooa property that returns a ConnectionMultiplexer
    // as shown in hello previous example.
    IDatabase cache = Connection.GetDatabase();

    // Perform cache operations using hello cache object...
    // Simple put of integral data types into hello cache
    cache.StringSet("key1", "value");
    cache.StringSet("key2", 25);

    // Simple get of data types from hello cache
    string key1 = cache.StringGet("key1");
    int key2 = (int)cache.StringGet("key2");

Cache Redis di Azure dispone di un numero configurabile di database (valore predefinito è 16) che possono essere utilizzati toologically hello separato dati all'interno di una cache Redis. Per altre informazioni, vedere [Informazioni sui database Redis](cache-faq.md#what-are-redis-databases) e [Configurazione predefinita del server Redis](cache-configure.md#default-redis-server-configuration).

Ora che è stato appreso come istanza di Cache Redis di Azure tooan tooconnect e restituire un riferimento di toohello memorizzano nella cache del database, si esaminerà l'utilizzo di cache di hello.

<a name="add-object"></a>

## <a name="add-and-retrieve-objects-from-hello-cache"></a>Aggiungere e recuperare gli oggetti dalla cache di hello
Gli elementi possono essere archiviati in e recuperati da una cache usando hello `StringSet` e `StringGet` metodi.

    // If key1 exists, it is overwritten.
    cache.StringSet("key1", "value1");

    string value = cache.StringGet("key1");

La maggior parte dei dati come stringhe di Redis, ma queste stringhe possono contenere molti tipi di dati, inclusi i dati binari serializzati, che possono essere utilizzati quando gli oggetti di archiviazione .NET nella cache di hello archivi di redis.

Quando si chiama `StringGet`, se l'oggetto hello esiste, viene restituito, e in caso contrario, `null` viene restituito. Se `null` viene restituito, è possibile recuperare il valore di hello dall'origine dati desiderata hello e memorizzarlo nella cache di hello per un utilizzo successivo. Questo modello di utilizzo è noto come modello cache-aside hello.

    string value = cache.StringGet("key1");
    if (value == null)
    {
        // hello item keyed by "key1" is not in hello cache. Obtain
        // it from hello desired data source and add it toohello cache.
        value = GetValueFromDataSource();

        cache.StringSet("key1", value);
    }

È inoltre possibile utilizzare `RedisValue`, come illustrato nell'esempio seguente hello. `RedisValue` ha operatori impliciti per l'uso di tipi di dati integrali e può essere utile se `null` è un valore previsto per un elemento memorizzato nella cache.


    RedisValue value = cache.StringGet("key1");
    if (!value.HasValue)
    {
        value = GetValueFromDataSource();
        cache.StringSet("key1", value);
    }


scadenza hello toospecify di un elemento nella cache di hello, utilizzare hello `TimeSpan` parametro di `StringSet`.

    cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));

## <a name="work-with-net-objects-in-hello-cache"></a>Utilizzo di oggetti .NET nella cache di hello
Cache Redis di Azure è in grado di memorizzare nella cache sia oggetti .NET che tipi di dati primitivi, ma prima della memorizzazione nella cache un oggetto .NET deve essere serializzato. La serializzazione di oggetti .NET hello responsabilità dello sviluppatore dell'applicazione hello e offre flessibilità di sviluppatore hello nella scelta di hello del serializzatore hello.

Un modo semplice tooserialize oggetti è hello toouse `JsonConvert` metodi di serializzazione in [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) e serializzare tooand da JSON. Hello esempio seguente viene illustrato un get e set utilizzando un `Employee` istanza dell'oggetto.

    class Employee
    {
        public int Id { get; set; }
        public string Name { get; set; }

        public Employee(int EmployeeId, string Name)
        {
            this.Id = EmployeeId;
            this.Name = Name;
        }
    }

    // Store toocache
    cache.StringSet("e25", JsonConvert.SerializeObject(new Employee(25, "Clayton Gragg")));

    // Retrieve from cache
    Employee e25 = JsonConvert.DeserializeObject<Employee>(cache.StringGet("e25"));

<a name="next-steps"></a>

## <a name="next-steps"></a>Passaggi successivi
Ora che si è appreso i concetti di base hello, seguire questi toolearn collegamenti ulteriori informazioni sulla Cache Redis di Azure.

* Estrarre hello provider ASP.NET per Cache Redis di Azure.
  * [Provider di stato della sessione Redis di Azure](cache-aspnet-session-state-provider.md)
  * [Provider di cache di output ASP.NET della Cache Redis di Azure](cache-aspnet-output-cache-provider.md)
* [Abilitare la diagnostica della cache](cache-how-to-monitor.md#enable-cache-diagnostics) in modo da poter [monitoraggio](cache-how-to-monitor.md) hello integrità della cache. È possibile visualizzare le metriche nel portale di Azure hello e si possono anche hello [scaricare ed esaminare](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) loro utilizzando gli strumenti di hello di propria scelta.
* Estrarre hello [documentazione relativa al client della cache stackexchange. Redis][StackExchange.Redis cache client documentation].
  * È possibile accedere a Cache Redis di Azure da numerosi linguaggi di sviluppo e client Redis. Per altre informazioni, vedere [http://redis.io/clients][http://redis.io/clients].
* È anche possibile usare Cache Redis di Azure con servizi e strumenti di terze parti come Redsmin e Redis Desktop Manager.
  * Per ulteriori informazioni su Redsmin, vedere [come tooretrieve una connessione di Azure Redis stringa e usarlo con Redsmin][How tooretrieve an Azure Redis connection string and use it with Redsmin].
  * Per accedere ai dati in Cache Redis di Azure e controllarli con una GUI, usare [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).
* Vedere hello [redis] [ redis] documentazione e informazioni [tipi di dati redis] [ redis data types] e [un'introduzione di 15 minuti tipi di dati tooRedis][a fifteen minute introduction tooRedis data types].

<!-- INTRA-TOPIC LINKS -->
[Next Steps]: #next-steps
[Introduction tooAzure Redis Cache (Video)]: #video
[What is Azure Redis Cache?]: #what-is
[Create an Azure Cache]: #create-cache
[Which type of caching is right for me?]: #choosing-cache
[Prepare Your Visual Studio Project tooUse Azure Caching]: #prepare-vs
[Configure Your Application tooUse Caching]: #configure-app
[Get Started with Azure Redis Cache]: #getting-started-cache-service
[Create hello cache]: #create-cache
[Configure hello cache]: #enable-caching
[Configure hello cache clients]: #NuGet
[Working with Caches]: #working-with-caches
[Connect toohello cache]: #connect-to-cache
[Add and retrieve objects from hello cache]: #add-object
[Specify hello expiration of an object in hello cache]: #specify-expiration
[Store ASP.NET session state in hello cache]: #store-session


<!-- IMAGES -->


[StackExchangeNuget]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-stackexchange-redis.png

[NuGetMenu]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-manage-nuget-menu.png

[CacheProperties]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-properties.png

[ManageKeys]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-manage-keys.png

[SessionStateNuGet]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-session-state-provider.png

[BrowseCaches]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-browse-caches.png

[Caches]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-caches.png







<!-- LINKS -->
[http://redis.io/clients]: http://redis.io/clients
[Develop in other languages for Azure Redis Cache]: http://msdn.microsoft.com/library/azure/dn690470.aspx
[How tooretrieve an Azure Redis connection string and use it with Redsmin]: https://redsmin.uservoice.com/knowledgebase/articles/485711-how-to-connect-redsmin-to-azure-redis-cache
[Azure Redis Session State Provider]: http://go.microsoft.com/fwlink/?LinkId=398249
[How to: Configure a Cache Client Programmatically]: http://msdn.microsoft.com/library/windowsazure/gg618003.aspx
[Session State Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320835
[Azure AppFabric Cache: Caching Session State]: http://www.microsoft.com/showcase/details.aspx?uuid=87c833e9-97a9-42b2-8bb1-7601f9b5ca20
[Output Cache Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320837
[Azure Shared Caching]: http://msdn.microsoft.com/library/windowsazure/gg278356.aspx
[Team Blog]: http://blogs.msdn.com/b/windowsazure/
[Azure Caching]: http://www.microsoft.com/showcase/Search.aspx?phrase=azure+caching
[How tooConfigure Virtual Machine Sizes]: http://go.microsoft.com/fwlink/?LinkId=164387
[Azure Caching Capacity Planning Considerations]: http://go.microsoft.com/fwlink/?LinkId=320167
[Azure Caching]: http://go.microsoft.com/fwlink/?LinkId=252658
[How to: Set hello Cacheability of an ASP.NET Page Declaratively]: http://msdn.microsoft.com/library/zd1ysf1y.aspx
[How to: Set a Page's Cacheability Programmatically]: http://msdn.microsoft.com/library/z852zf6b.aspx
[Configure a cache in Azure Redis Cache]: http://msdn.microsoft.com/library/azure/dn793612.aspx

[StackExchange.Redis configuration model]: https://stackexchange.github.io/StackExchange.Redis/Configuration

[Work with .NET objects in hello cache]: http://msdn.microsoft.com/library/dn690521.aspx#Objects


[NuGet Package Manager Installation]: http://go.microsoft.com/fwlink/?LinkId=240311
[Cache Pricing Details]: http://www.windowsazure.com/pricing/details/cache/
[Azure portal]: https://portal.azure.com/

[Overview of Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=320830
[Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=398247

[Migrate tooAzure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=317347
[Azure Redis Cache Samples]: http://go.microsoft.com/fwlink/?LinkId=320840
[Using Resource groups toomanage your Azure resources]: ../azure-resource-manager/resource-group-overview.md

[StackExchange.Redis]: http://github.com/StackExchange/StackExchange.Redis
[StackExchange.Redis cache client documentation]: http://github.com/StackExchange/StackExchange.Redis#documentation

[Redis]: http://redis.io/documentation
[Redis data types]: http://redis.io/topics/data-types
[a fifteen minute introduction tooRedis data types]: http://redis.io/topics/data-types-intro

[How Application Strings and Connection Strings Work]: http://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/


