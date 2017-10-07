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
# <a name="how-toouse-azure-redis-cache"></a><span data-ttu-id="8df76-103">La modalità di Cache Redis di Azure di tooUse</span><span class="sxs-lookup"><span data-stu-id="8df76-103">How tooUse Azure Redis Cache</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8df76-104">.NET</span><span class="sxs-lookup"><span data-stu-id="8df76-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="8df76-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8df76-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="8df76-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="8df76-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="8df76-107">Java</span><span class="sxs-lookup"><span data-stu-id="8df76-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="8df76-108">Python</span><span class="sxs-lookup"><span data-stu-id="8df76-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="8df76-109">Questa guida illustra la modalità di avvio utilizzando tooget **Cache Redis di Azure**.</span><span class="sxs-lookup"><span data-stu-id="8df76-109">This guide shows you how tooget started using **Azure Redis Cache**.</span></span> <span data-ttu-id="8df76-110">Cache Redis di Microsoft Azure si basa su hello open source comuni Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="8df76-110">Microsoft Azure Redis Cache is based on hello popular open source Redis Cache.</span></span> <span data-ttu-id="8df76-111">Consente di accedere a tooa sicura e dedicata cache Redis, gestita da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8df76-111">It gives you access tooa secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="8df76-112">Una cache creata usando Cache Redis di Azure sarà accessibile da qualsiasi applicazione all'interno di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="8df76-112">A cache created using Azure Redis Cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="8df76-113">Cache Redis di Microsoft Azure è disponibile in hello livelli seguenti:</span><span class="sxs-lookup"><span data-stu-id="8df76-113">Microsoft Azure Redis Cache is available in hello following tiers:</span></span>

* <span data-ttu-id="8df76-114">**Basic**: singolo nodo.</span><span class="sxs-lookup"><span data-stu-id="8df76-114">**Basic** – Single node.</span></span> <span data-ttu-id="8df76-115">Più dimensioni too53 GB.</span><span class="sxs-lookup"><span data-stu-id="8df76-115">Multiple sizes up too53 GB.</span></span>
* <span data-ttu-id="8df76-116">**Standard**: principale/replica a due nodi.</span><span class="sxs-lookup"><span data-stu-id="8df76-116">**Standard** – Two-node Primary/Replica.</span></span> <span data-ttu-id="8df76-117">Più dimensioni too53 GB.</span><span class="sxs-lookup"><span data-stu-id="8df76-117">Multiple sizes up too53 GB.</span></span> <span data-ttu-id="8df76-118">Contratti di servizio del 99,9%.</span><span class="sxs-lookup"><span data-stu-id="8df76-118">99.9% SLA.</span></span>
* <span data-ttu-id="8df76-119">**Premium** : due nodi primario/Replica con backup too10 partizioni.</span><span class="sxs-lookup"><span data-stu-id="8df76-119">**Premium** – Two-node Primary/Replica with up too10 shards.</span></span> <span data-ttu-id="8df76-120">Più dimensioni che vanno da 6 GB too530 GB.</span><span class="sxs-lookup"><span data-stu-id="8df76-120">Multiple sizes from 6 GB too530 GB.</span></span> <span data-ttu-id="8df76-121">Supporto per tutte le funzionalità del piano Standard e altre, tra cui [cluster Redis](cache-how-to-premium-clustering.md), [persistenza Redis](cache-how-to-premium-persistence.md) e [Rete virtuale di Azure](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="8df76-121">All Standard tier features and more including support for [Redis cluster](cache-how-to-premium-clustering.md), [Redis persistence](cache-how-to-premium-persistence.md), and [Azure Virtual Network](cache-how-to-premium-vnet.md).</span></span> <span data-ttu-id="8df76-122">Contratti di servizio del 99,9%.</span><span class="sxs-lookup"><span data-stu-id="8df76-122">99.9% SLA.</span></span>

<span data-ttu-id="8df76-123">Ogni livello presenta differenze in termini di funzionalità e prezzi.</span><span class="sxs-lookup"><span data-stu-id="8df76-123">Each tier differs in terms of features and pricing.</span></span> <span data-ttu-id="8df76-124">Per informazioni sui prezzi, vedere [Dettagli prezzi del servizio Cache][Cache Pricing Details].</span><span class="sxs-lookup"><span data-stu-id="8df76-124">For information on pricing, see [Cache Pricing Details][Cache Pricing Details].</span></span>

<span data-ttu-id="8df76-125">Questa guida illustra come hello toouse [stackexchange. Redis] [ StackExchange.Redis] client utilizzando C\# codice.</span><span class="sxs-lookup"><span data-stu-id="8df76-125">This guide shows you how toouse hello [StackExchange.Redis][StackExchange.Redis] client using C\# code.</span></span> <span data-ttu-id="8df76-126">Hello scenari trattati includono **creazione e configurazione di una cache**, **configurazione i client della cache**, e **aggiungendo e rimuovendo oggetti dalla cache di hello**.</span><span class="sxs-lookup"><span data-stu-id="8df76-126">hello scenarios covered include **creating and configuring a cache**, **configuring cache clients**, and **adding and removing objects from hello cache**.</span></span> <span data-ttu-id="8df76-127">Per altre informazioni sull'uso di Cache Redis di Azure, vedere i [Passaggi successivi][Next Steps].</span><span class="sxs-lookup"><span data-stu-id="8df76-127">For more information on using Azure Redis Cache, see [Next Steps][Next Steps].</span></span> <span data-ttu-id="8df76-128">Per un'esercitazione dettagliata della creazione di app web con Cache Redis di MVC ASP.NET, vedere [come un'App Web in Cache Redis toocreate](cache-web-app-howto.md).</span><span class="sxs-lookup"><span data-stu-id="8df76-128">For a step-by-step tutorial of building an ASP.NET MVC web app with Redis Cache, see [How toocreate a Web App with Redis Cache](cache-web-app-howto.md).</span></span>

<a name="getting-started-cache-service"></a>

## <a name="get-started-with-azure-redis-cache"></a><span data-ttu-id="8df76-129">Introduzione all'uso di Cache Redis di Azure</span><span class="sxs-lookup"><span data-stu-id="8df76-129">Get Started with Azure Redis Cache</span></span>
<span data-ttu-id="8df76-130">Iniziare a usare Cache Redis di Azure è semplice.</span><span class="sxs-lookup"><span data-stu-id="8df76-130">Getting started with Azure Redis Cache is easy.</span></span> <span data-ttu-id="8df76-131">tooget avviato, per eseguire il provisioning e configurare una cache.</span><span class="sxs-lookup"><span data-stu-id="8df76-131">tooget started, you provision and configure a cache.</span></span> <span data-ttu-id="8df76-132">Successivamente, configurare i client della cache di hello consentire l'accesso della cache di hello.</span><span class="sxs-lookup"><span data-stu-id="8df76-132">Next, you configure hello cache clients so they can access hello cache.</span></span> <span data-ttu-id="8df76-133">Dopo aver configurati i client della cache di hello, è possibile iniziare loro utilizzo.</span><span class="sxs-lookup"><span data-stu-id="8df76-133">Once hello cache clients are configured, you can begin working with them.</span></span>

* <span data-ttu-id="8df76-134">[Creare una cache di hello][Create hello cache]</span><span class="sxs-lookup"><span data-stu-id="8df76-134">[Create hello cache][Create hello cache]</span></span>
* <span data-ttu-id="8df76-135">[Configurare i client della cache di hello][Configure hello cache clients]</span><span class="sxs-lookup"><span data-stu-id="8df76-135">[Configure hello cache clients][Configure hello cache clients]</span></span>

<a name="create-cache"></a>

## <a name="create-a-cache"></a><span data-ttu-id="8df76-136">Creare una cache</span><span class="sxs-lookup"><span data-stu-id="8df76-136">Create a cache</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

### <a name="tooaccess-your-cache-after-its-created"></a><span data-ttu-id="8df76-137">tooaccess viene creata la cache dopo di esso</span><span class="sxs-lookup"><span data-stu-id="8df76-137">tooaccess your cache after it's created</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

<span data-ttu-id="8df76-138">Per ulteriori informazioni sulla configurazione di cache, vedere [come tooconfigure Cache Redis di Azure](cache-configure.md).</span><span class="sxs-lookup"><span data-stu-id="8df76-138">For more information about configuring your cache, see [How tooconfigure Azure Redis Cache](cache-configure.md).</span></span>

<a name="NuGet"></a>

## <a name="configure-hello-cache-clients"></a><span data-ttu-id="8df76-139">Configurare i client della cache di hello</span><span class="sxs-lookup"><span data-stu-id="8df76-139">Configure hello cache clients</span></span>
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

<span data-ttu-id="8df76-140">Dopo aver configurato il progetto client per la memorizzazione nella cache, è possibile utilizzare tecniche di hello descritte nelle seguenti sezioni per l'utilizzo con la cache di hello.</span><span class="sxs-lookup"><span data-stu-id="8df76-140">Once your client project is configured for caching, you can use hello techniques described in hello following sections for working with your cache.</span></span>

<a name="working-with-caches"></a>

## <a name="working-with-caches"></a><span data-ttu-id="8df76-141">Utilizzo delle cache</span><span class="sxs-lookup"><span data-stu-id="8df76-141">Working with Caches</span></span>
<span data-ttu-id="8df76-142">Hello in questa sezione viene descritta la modalità di attività comuni di tooperform con Cache.</span><span class="sxs-lookup"><span data-stu-id="8df76-142">hello steps in this section describe how tooperform common tasks with Cache.</span></span>

* <span data-ttu-id="8df76-143">[La connessione della cache toohello][Connect toohello cache]</span><span class="sxs-lookup"><span data-stu-id="8df76-143">[Connect toohello cache][Connect toohello cache]</span></span>
* <span data-ttu-id="8df76-144">[Aggiungere e recuperare gli oggetti dalla cache di hello][Add and retrieve objects from hello cache]</span><span class="sxs-lookup"><span data-stu-id="8df76-144">[Add and retrieve objects from hello cache][Add and retrieve objects from hello cache]</span></span>
* [<span data-ttu-id="8df76-145">Utilizzo di oggetti .NET nella cache di hello</span><span class="sxs-lookup"><span data-stu-id="8df76-145">Work with .NET objects in hello cache</span></span>](#work-with-net-objects-in-the-cache)

<a name="connect-to-cache"></a>

## <a name="connect-toohello-cache"></a><span data-ttu-id="8df76-146">La connessione della cache toohello</span><span class="sxs-lookup"><span data-stu-id="8df76-146">Connect toohello cache</span></span>
<span data-ttu-id="8df76-147">lavoro tooprogrammatically con una cache, è necessario che una cache toohello di riferimento.</span><span class="sxs-lookup"><span data-stu-id="8df76-147">tooprogrammatically work with a cache, you need a reference toohello cache.</span></span> <span data-ttu-id="8df76-148">Aggiungere hello seguente toohello superiore di qualsiasi file da cui si desidera toouse hello Stackexchange client tooaccess Cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="8df76-148">Add hello following toohello top of any file from which you want toouse hello StackExchange.Redis client tooaccess an Azure Redis Cache.</span></span>

    using StackExchange.Redis;

> [!NOTE]
> <span data-ttu-id="8df76-149">client stackexchange. Redis Hello richiede .NET Framework 4 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="8df76-149">hello StackExchange.Redis client requires .NET Framework 4 or higher.</span></span>
> 
> 

<span data-ttu-id="8df76-150">Hello toohello connessione Cache Redis di Azure è gestita da hello `ConnectionMultiplexer` classe.</span><span class="sxs-lookup"><span data-stu-id="8df76-150">hello connection toohello Azure Redis Cache is managed by hello `ConnectionMultiplexer` class.</span></span> <span data-ttu-id="8df76-151">Questa classe deve essere condivisa e riutilizzabile nell'applicazione client e non è necessario creare in ogni singola operazione toobe.</span><span class="sxs-lookup"><span data-stu-id="8df76-151">This class should be shared and reused throughout your client application, and does not need toobe created on a per operation basis.</span></span> 

<span data-ttu-id="8df76-152">tooconnect tooan Cache Redis di Azure e restituito un'istanza di un oggetto connesso `ConnectionMultiplexer`, chiamata hello statico `Connect` (metodo) e passare hello memorizzano nella cache dell'endpoint e la chiave.</span><span class="sxs-lookup"><span data-stu-id="8df76-152">tooconnect tooan Azure Redis Cache and be returned an instance of a connected `ConnectionMultiplexer`, call hello static `Connect` method and pass in hello cache endpoint and key.</span></span> <span data-ttu-id="8df76-153">Utilizzo chiave hello generata dal portale di Azure come parametro di password hello hello.</span><span class="sxs-lookup"><span data-stu-id="8df76-153">Use hello key generated from hello Azure portal as hello password parameter.</span></span>

    ConnectionMultiplexer connection = ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");

> [!IMPORTANT]
> <span data-ttu-id="8df76-154">Avviso: non archiviare mai le credenziali nel codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="8df76-154">Warning: Never store credentials in source code.</span></span> <span data-ttu-id="8df76-155">tookeep questo semplice esempio, sono illustrati nel codice sorgente hello.</span><span class="sxs-lookup"><span data-stu-id="8df76-155">tookeep this sample simple, I’m showing them in hello source code.</span></span> <span data-ttu-id="8df76-156">Vedere [come le stringhe dell'applicazione e lavoro di stringhe di connessione] [ How Application Strings and Connection Strings Work] per informazioni su come toostore credenziali.</span><span class="sxs-lookup"><span data-stu-id="8df76-156">See [How Application Strings and Connection Strings Work][How Application Strings and Connection Strings Work] for information on how toostore credentials.</span></span>
> 
> 

<span data-ttu-id="8df76-157">Se non si desidera toouse SSL, impostare `ssl=false` oppure omettere hello `ssl` parametro.</span><span class="sxs-lookup"><span data-stu-id="8df76-157">If you don't want toouse SSL, either set `ssl=false` or omit hello `ssl` parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="8df76-158">porta non SSL Hello è disabilitata per impostazione predefinita per le nuove cache.</span><span class="sxs-lookup"><span data-stu-id="8df76-158">hello non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="8df76-159">Per istruzioni sull'abilitazione di porta non SSL hello, vedere [porte di accesso](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="8df76-159">For instructions on enabling hello non-SSL port, see [Access Ports](cache-configure.md#access-ports).</span></span>
> 
> 

<span data-ttu-id="8df76-160">Un approccio toosharing un `ConnectionMultiplexer` istanza dell'applicazione è toohave una proprietà statica che restituisce un'istanza connessa, simile toohello esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="8df76-160">One approach toosharing a `ConnectionMultiplexer` instance in your application is toohave a static property that returns a connected instance, similar toohello following example.</span></span> <span data-ttu-id="8df76-161">Questo approccio fornisce un modo thread-safe di tooinitialize solo una singola connessione `ConnectionMultiplexer` istanza.</span><span class="sxs-lookup"><span data-stu-id="8df76-161">This approach provides a thread-safe way tooinitialize only a single connected `ConnectionMultiplexer` instance.</span></span> <span data-ttu-id="8df76-162">In questi esempi `abortConnect` è toofalse set, il che significa che la chiamata hello ha esito positivo anche se non viene stabilita una toohello connessione Cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="8df76-162">In these examples `abortConnect` is set toofalse, which means that hello call succeeds even if a connection toohello Azure Redis Cache is not established.</span></span> <span data-ttu-id="8df76-163">Una caratteristica fondamentale di `ConnectionMultiplexer` è che viene ripristinata automaticamente cache toohello connettività quando vengono risolte i problemi di rete hello o altre cause.</span><span class="sxs-lookup"><span data-stu-id="8df76-163">One key feature of `ConnectionMultiplexer` is that it automatically restores connectivity toohello cache once hello network issue or other causes are resolved.</span></span>

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

<span data-ttu-id="8df76-164">Per altre informazioni sulle opzioni di configurazione avanzate per la connessione, vedere [Modello di configurazione di StackExchange.Redis][StackExchange.Redis configuration model].</span><span class="sxs-lookup"><span data-stu-id="8df76-164">For more information on advanced connection configuration options, see [StackExchange.Redis configuration model][StackExchange.Redis configuration model].</span></span>

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

<span data-ttu-id="8df76-165">Una volta stabilita la connessione hello, restituire un database di riferimento toohello redis cache dal chiamante hello `ConnectionMultiplexer.GetDatabase` metodo.</span><span class="sxs-lookup"><span data-stu-id="8df76-165">Once hello connection is established, return a reference toohello redis cache database by calling hello `ConnectionMultiplexer.GetDatabase` method.</span></span> <span data-ttu-id="8df76-166">oggetto Hello restituito da hello `GetDatabase` metodo è un oggetto passthrough semplice e non è necessario toobe archiviati.</span><span class="sxs-lookup"><span data-stu-id="8df76-166">hello object returned from hello `GetDatabase` method is a lightweight pass-through object and does not need toobe stored.</span></span>

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

<span data-ttu-id="8df76-167">Cache Redis di Azure dispone di un numero configurabile di database (valore predefinito è 16) che possono essere utilizzati toologically hello separato dati all'interno di una cache Redis.</span><span class="sxs-lookup"><span data-stu-id="8df76-167">Azure Redis caches have a configurable number of databases (default of 16) that can be used toologically separate hello data within a Redis cache.</span></span> <span data-ttu-id="8df76-168">Per altre informazioni, vedere [Informazioni sui database Redis](cache-faq.md#what-are-redis-databases) e [Configurazione predefinita del server Redis](cache-configure.md#default-redis-server-configuration).</span><span class="sxs-lookup"><span data-stu-id="8df76-168">For more information, see [What are Redis databases?](cache-faq.md#what-are-redis-databases) and [Default Redis server configuration](cache-configure.md#default-redis-server-configuration).</span></span>

<span data-ttu-id="8df76-169">Ora che è stato appreso come istanza di Cache Redis di Azure tooan tooconnect e restituire un riferimento di toohello memorizzano nella cache del database, si esaminerà l'utilizzo di cache di hello.</span><span class="sxs-lookup"><span data-stu-id="8df76-169">Now that you know how tooconnect tooan Azure Redis Cache instance and return a reference toohello cache database, let's look at working with hello cache.</span></span>

<a name="add-object"></a>

## <a name="add-and-retrieve-objects-from-hello-cache"></a><span data-ttu-id="8df76-170">Aggiungere e recuperare gli oggetti dalla cache di hello</span><span class="sxs-lookup"><span data-stu-id="8df76-170">Add and retrieve objects from hello cache</span></span>
<span data-ttu-id="8df76-171">Gli elementi possono essere archiviati in e recuperati da una cache usando hello `StringSet` e `StringGet` metodi.</span><span class="sxs-lookup"><span data-stu-id="8df76-171">Items can be stored in and retrieved from a cache by using hello `StringSet` and `StringGet` methods.</span></span>

    // If key1 exists, it is overwritten.
    cache.StringSet("key1", "value1");

    string value = cache.StringGet("key1");

<span data-ttu-id="8df76-172">La maggior parte dei dati come stringhe di Redis, ma queste stringhe possono contenere molti tipi di dati, inclusi i dati binari serializzati, che possono essere utilizzati quando gli oggetti di archiviazione .NET nella cache di hello archivi di redis.</span><span class="sxs-lookup"><span data-stu-id="8df76-172">Redis stores most data as Redis strings, but these strings can contain many types of data, including serialized binary data, which can be used when storing .NET objects in hello cache.</span></span>

<span data-ttu-id="8df76-173">Quando si chiama `StringGet`, se l'oggetto hello esiste, viene restituito, e in caso contrario, `null` viene restituito.</span><span class="sxs-lookup"><span data-stu-id="8df76-173">When calling `StringGet`, if hello object exists, it is returned, and if it does not, `null` is returned.</span></span> <span data-ttu-id="8df76-174">Se `null` viene restituito, è possibile recuperare il valore di hello dall'origine dati desiderata hello e memorizzarlo nella cache di hello per un utilizzo successivo.</span><span class="sxs-lookup"><span data-stu-id="8df76-174">If `null` is returned, you can retrieve hello value from hello desired data source and store it in hello cache for subsequent use.</span></span> <span data-ttu-id="8df76-175">Questo modello di utilizzo è noto come modello cache-aside hello.</span><span class="sxs-lookup"><span data-stu-id="8df76-175">This usage pattern is known as hello cache-aside pattern.</span></span>

    string value = cache.StringGet("key1");
    if (value == null)
    {
        // hello item keyed by "key1" is not in hello cache. Obtain
        // it from hello desired data source and add it toohello cache.
        value = GetValueFromDataSource();

        cache.StringSet("key1", value);
    }

<span data-ttu-id="8df76-176">È inoltre possibile utilizzare `RedisValue`, come illustrato nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="8df76-176">You can also use `RedisValue`, as shown in hello following example.</span></span> <span data-ttu-id="8df76-177">`RedisValue` ha operatori impliciti per l'uso di tipi di dati integrali e può essere utile se `null` è un valore previsto per un elemento memorizzato nella cache.</span><span class="sxs-lookup"><span data-stu-id="8df76-177">`RedisValue` has implicit operators for working with integral data types, and can be useful if `null` is an expected value for a cached item.</span></span>


    RedisValue value = cache.StringGet("key1");
    if (!value.HasValue)
    {
        value = GetValueFromDataSource();
        cache.StringSet("key1", value);
    }


<span data-ttu-id="8df76-178">scadenza hello toospecify di un elemento nella cache di hello, utilizzare hello `TimeSpan` parametro di `StringSet`.</span><span class="sxs-lookup"><span data-stu-id="8df76-178">toospecify hello expiration of an item in hello cache, use hello `TimeSpan` parameter of `StringSet`.</span></span>

    cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));

## <a name="work-with-net-objects-in-hello-cache"></a><span data-ttu-id="8df76-179">Utilizzo di oggetti .NET nella cache di hello</span><span class="sxs-lookup"><span data-stu-id="8df76-179">Work with .NET objects in hello cache</span></span>
<span data-ttu-id="8df76-180">Cache Redis di Azure è in grado di memorizzare nella cache sia oggetti .NET che tipi di dati primitivi, ma prima della memorizzazione nella cache un oggetto .NET deve essere serializzato.</span><span class="sxs-lookup"><span data-stu-id="8df76-180">Azure Redis Cache can cache both .NET objects and primitive data types, but before a .NET object can be cached it must be serialized.</span></span> <span data-ttu-id="8df76-181">La serializzazione di oggetti .NET hello responsabilità dello sviluppatore dell'applicazione hello e offre flessibilità di sviluppatore hello nella scelta di hello del serializzatore hello.</span><span class="sxs-lookup"><span data-stu-id="8df76-181">This .NET object serialization is hello responsibility of hello application developer, and gives hello developer flexibility in hello choice of hello serializer.</span></span>

<span data-ttu-id="8df76-182">Un modo semplice tooserialize oggetti è hello toouse `JsonConvert` metodi di serializzazione in [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) e serializzare tooand da JSON.</span><span class="sxs-lookup"><span data-stu-id="8df76-182">One simple way tooserialize objects is toouse hello `JsonConvert` serialization methods in [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) and serialize tooand from JSON.</span></span> <span data-ttu-id="8df76-183">Hello esempio seguente viene illustrato un get e set utilizzando un `Employee` istanza dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="8df76-183">hello following example shows a get and set using an `Employee` object instance.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8df76-184">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8df76-184">Next Steps</span></span>
<span data-ttu-id="8df76-185">Ora che si è appreso i concetti di base hello, seguire questi toolearn collegamenti ulteriori informazioni sulla Cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="8df76-185">Now that you've learned hello basics, follow these links toolearn more about Azure Redis Cache.</span></span>

* <span data-ttu-id="8df76-186">Estrarre hello provider ASP.NET per Cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="8df76-186">Check out hello ASP.NET providers for Azure Redis Cache.</span></span>
  * [<span data-ttu-id="8df76-187">Provider di stato della sessione Redis di Azure</span><span class="sxs-lookup"><span data-stu-id="8df76-187">Azure Redis Session State Provider</span></span>](cache-aspnet-session-state-provider.md)
  * [<span data-ttu-id="8df76-188">Provider di cache di output ASP.NET della Cache Redis di Azure</span><span class="sxs-lookup"><span data-stu-id="8df76-188">Azure Redis Cache ASP.NET Output Cache Provider</span></span>](cache-aspnet-output-cache-provider.md)
* <span data-ttu-id="8df76-189">[Abilitare la diagnostica della cache](cache-how-to-monitor.md#enable-cache-diagnostics) in modo da poter [monitoraggio](cache-how-to-monitor.md) hello integrità della cache.</span><span class="sxs-lookup"><span data-stu-id="8df76-189">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) hello health of your cache.</span></span> <span data-ttu-id="8df76-190">È possibile visualizzare le metriche nel portale di Azure hello e si possono anche hello [scaricare ed esaminare](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) loro utilizzando gli strumenti di hello di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="8df76-190">You can view hello metrics in hello Azure portal and you can also [download and review](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) them using hello tools of your choice.</span></span>
* <span data-ttu-id="8df76-191">Estrarre hello [documentazione relativa al client della cache stackexchange. Redis][StackExchange.Redis cache client documentation].</span><span class="sxs-lookup"><span data-stu-id="8df76-191">Check out hello [StackExchange.Redis cache client documentation][StackExchange.Redis cache client documentation].</span></span>
  * <span data-ttu-id="8df76-192">È possibile accedere a Cache Redis di Azure da numerosi linguaggi di sviluppo e client Redis.</span><span class="sxs-lookup"><span data-stu-id="8df76-192">Azure Redis Cache can be accessed from many Redis clients and development languages.</span></span> <span data-ttu-id="8df76-193">Per altre informazioni, vedere [http://redis.io/clients][http://redis.io/clients].</span><span class="sxs-lookup"><span data-stu-id="8df76-193">For more information, see [http://redis.io/clients][http://redis.io/clients].</span></span>
* <span data-ttu-id="8df76-194">È anche possibile usare Cache Redis di Azure con servizi e strumenti di terze parti come Redsmin e Redis Desktop Manager.</span><span class="sxs-lookup"><span data-stu-id="8df76-194">Azure Redis Cache can also be used with third-party services and tools such as Redsmin and Redis Desktop Manager.</span></span>
  * <span data-ttu-id="8df76-195">Per ulteriori informazioni su Redsmin, vedere [come tooretrieve una connessione di Azure Redis stringa e usarlo con Redsmin][How tooretrieve an Azure Redis connection string and use it with Redsmin].</span><span class="sxs-lookup"><span data-stu-id="8df76-195">For more information about Redsmin, see [How tooretrieve an Azure Redis connection string and use it with Redsmin][How tooretrieve an Azure Redis connection string and use it with Redsmin].</span></span>
  * <span data-ttu-id="8df76-196">Per accedere ai dati in Cache Redis di Azure e controllarli con una GUI, usare [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).</span><span class="sxs-lookup"><span data-stu-id="8df76-196">Access and inspect your data in Azure Redis Cache with a GUI using [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).</span></span>
* <span data-ttu-id="8df76-197">Vedere hello [redis] [ redis] documentazione e informazioni [tipi di dati redis] [ redis data types] e [un'introduzione di 15 minuti tipi di dati tooRedis][a fifteen minute introduction tooRedis data types].</span><span class="sxs-lookup"><span data-stu-id="8df76-197">See hello [redis][redis] documentation and read about [redis data types][redis data types] and [a fifteen minute introduction tooRedis data types][a fifteen minute introduction tooRedis data types].</span></span>

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


