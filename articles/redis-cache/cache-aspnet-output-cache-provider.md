---
title: aaaCache Provider della Cache di Output ASP.NET
description: Informazioni su come Output della pagina ASP.NET toocache usando Cache Redis di Azure
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 78469a66-0829-484f-8660-b2598ec60fbf
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/14/2017
ms.author: sdanie
ms.openlocfilehash: fc38cc657604b351f55ad8febac383783ac29700
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-output-cache-provider-for-azure-redis-cache"></a><span data-ttu-id="44705-103">Provider di cache di output ASP.NET per la Cache Redis di Azure</span><span class="sxs-lookup"><span data-stu-id="44705-103">ASP.NET Output Cache Provider for Azure Redis Cache</span></span>
<span data-ttu-id="44705-104">Hello redis-Provider della Cache di Output è un meccanismo di memorizzazione out-of-process per i dati della cache di output.</span><span class="sxs-lookup"><span data-stu-id="44705-104">hello Redis Output Cache Provider is an out-of-process storage mechanism for output cache data.</span></span> <span data-ttu-id="44705-105">Tali dati sono specificamente utilizzati per le risposte HTTP complete (memorizzazione nella cache di output delle pagine).</span><span class="sxs-lookup"><span data-stu-id="44705-105">This data is specifically for full HTTP responses (page output caching).</span></span> <span data-ttu-id="44705-106">Hello provider si collega hello nuovo output cache provider punto di estendibilità che è stato introdotto in ASP.NET 4.</span><span class="sxs-lookup"><span data-stu-id="44705-106">hello provider plugs into hello new output cache provider extensibility point that was introduced in ASP.NET 4.</span></span>

<span data-ttu-id="44705-107">Ciao toouse redis-Provider della Cache di Output, configurare prima la cache e quindi configurare l'applicazione ASP.NET mediante pacchetto NuGet del Provider della Cache Output Redis hello.</span><span class="sxs-lookup"><span data-stu-id="44705-107">toouse hello Redis Output Cache Provider, first configure your cache, and then configure your ASP.NET application using hello Redis Output Cache Provider NuGet package.</span></span> <span data-ttu-id="44705-108">Questo argomento fornisce indicazioni sulla configurazione del hello toouse applicazione redis-Provider della Cache di Output.</span><span class="sxs-lookup"><span data-stu-id="44705-108">This topic provides guidance on configuring your application toouse hello Redis Output Cache Provider.</span></span> <span data-ttu-id="44705-109">Per altre informazioni sulla creazione e sulla configurazione di un'istanza della Cache Redis di Azure, vedere [Creare una cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span><span class="sxs-lookup"><span data-stu-id="44705-109">For more information about creating and configuring an Azure Redis Cache instance, see [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span></span>

## <a name="store-aspnet-page-output-in-hello-cache"></a><span data-ttu-id="44705-110">Archiviare l'output delle pagine ASP.NET nella cache di hello</span><span class="sxs-lookup"><span data-stu-id="44705-110">Store ASP.NET page output in hello cache</span></span>
<span data-ttu-id="44705-111">Fare clic su un'applicazione client in Visual Studio usando pacchetto NuGet lo stato della sessione di Cache Redis hello, tooconfigure **Gestione pacchetti NuGet**, **Package Manager Console** da hello **strumenti** menu.</span><span class="sxs-lookup"><span data-stu-id="44705-111">tooconfigure a client application in Visual Studio using hello Redis Cache Session State NuGet package, click **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu.</span></span>

<span data-ttu-id="44705-112">Esecuzione hello il seguente comando da hello `Package Manager Console` finestra.</span><span class="sxs-lookup"><span data-stu-id="44705-112">Run hello following command from hello `Package Manager Console` window.</span></span>
    
```
Install-Package Microsoft.Web.RedisOutputCacheProvider
```

<span data-ttu-id="44705-113">pacchetto NuGet del Provider della Cache Output Redis Hello presenta una dipendenza sul pacchetto Stackexchange hello.</span><span class="sxs-lookup"><span data-stu-id="44705-113">hello Redis Output Cache Provider NuGet package has a dependency on hello StackExchange.Redis.StrongName package.</span></span> <span data-ttu-id="44705-114">Se il pacchetto di Stackexchange hello non è presente nel progetto, è installato.</span><span class="sxs-lookup"><span data-stu-id="44705-114">If hello StackExchange.Redis.StrongName package is not present in your project, it is installed.</span></span> <span data-ttu-id="44705-115">Per ulteriori informazioni sul pacchetto NuGet del Provider della Cache Redis Output di hello, vedere hello [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) pagina NuGet.</span><span class="sxs-lookup"><span data-stu-id="44705-115">For more information about hello Redis Output Cache Provider NuGet package, see hello [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) NuGet page.</span></span>

>[!NOTE]
><span data-ttu-id="44705-116">In aggiunta toohello sicuro Stackexchange pacchetto, è inoltre disponibile hello stackexchange. Redis non-versione di nome sicuro.</span><span class="sxs-lookup"><span data-stu-id="44705-116">In addition toohello strong-named StackExchange.Redis.StrongName package, there is also hello StackExchange.Redis non-strong-named version.</span></span> <span data-ttu-id="44705-117">Se il progetto utilizza hello sicuro-versione priva di nome stackexchange. Redis che è necessario disinstallarla, in caso contrario si conflitti di denominazione nel progetto.</span><span class="sxs-lookup"><span data-stu-id="44705-117">If your project is using hello non-strong-named StackExchange.Redis version you must uninstall it, otherwise you get naming conflicts in your project.</span></span> <span data-ttu-id="44705-118">Per altre informazioni su questi pacchetti, vedere [Configurare i client della cache .NET](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span><span class="sxs-lookup"><span data-stu-id="44705-118">For more information about these packages, see [Configure .NET cache clients](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span></span>
>
>

<span data-ttu-id="44705-119">Hello NuGet pacchetto Scarica e aggiunge hello necessari riferimenti ad assembly e aggiunge hello seguente sezione nel file Web. config.</span><span class="sxs-lookup"><span data-stu-id="44705-119">hello NuGet package downloads and adds hello required assembly references and adds hello following section into your web.config file.</span></span> <span data-ttu-id="44705-120">In questa sezione di configurazione necessari hello per hello di toouse l'applicazione ASP.NET redis-Provider della Cache di Output.</span><span class="sxs-lookup"><span data-stu-id="44705-120">This section contains hello required configuration for your ASP.NET application toouse hello Redis Output Cache Provider.</span></span>

```xml
<caching>
  <outputCachedefault Provider="MyRedisOutputCache">
    <providers>
      <!--
      <add name="MyRedisOutputCache"
        host = "127.0.0.1" [String]
        port = "" [number]
        accessKey = "" [String]
        ssl = "false" [true|false]
        databaseId = "0" [number]
        applicationName = "" [String]
        connectionTimeoutInMilliseconds = "5000" [number]
        operationTimeoutInMilliseconds = "5000" [number]
      />
      -->
      <add name="MyRedisOutputCache" type="Microsoft.Web.Redis.RedisOutputCacheProvider" host="127.0.0.1" accessKey="" ssl="false"/>
    </providers>
  </outputCache>
</caching>
```

<span data-ttu-id="44705-121">Hello commentato sezione viene fornito un esempio di attributi di hello e le impostazioni di esempio per ogni attributo.</span><span class="sxs-lookup"><span data-stu-id="44705-121">hello commented section provides an example of hello attributes and sample settings for each attribute.</span></span>

<span data-ttu-id="44705-122">Configurare gli attributi di hello con i valori hello del pannello della cache nel portale di Microsoft Azure hello e hello altri valori in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="44705-122">Configure hello attributes with hello values from your cache blade in hello Microsoft Azure portal, and configure hello other values as desired.</span></span> <span data-ttu-id="44705-123">Per istruzioni sull'accesso alle proprietà della cache, vedere [Configurare le impostazioni di Cache Redis di Azure](cache-configure.md#configure-redis-cache-settings).</span><span class="sxs-lookup"><span data-stu-id="44705-123">For instructions on accessing your cache properties, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

* <span data-ttu-id="44705-124">**host** : specificare l'endpoint della cache.</span><span class="sxs-lookup"><span data-stu-id="44705-124">**host** – specify your cache endpoint.</span></span>
* <span data-ttu-id="44705-125">**porta** : utilizzare la porta non SSL o la porta SSL, a seconda delle impostazioni ssl hello.</span><span class="sxs-lookup"><span data-stu-id="44705-125">**port** – use either your non-SSL port or your SSL port, depending on hello ssl settings.</span></span>
* <span data-ttu-id="44705-126">**accessKey** : utilizzare una chiave primaria o secondaria di hello per la cache.</span><span class="sxs-lookup"><span data-stu-id="44705-126">**accessKey** – use either hello primary or secondary key for your cache.</span></span>
* <span data-ttu-id="44705-127">**SSL** : true se si desidera toosecure di comunicazioni cache/client con ssl; in caso contrario, false.</span><span class="sxs-lookup"><span data-stu-id="44705-127">**ssl** – true if you want toosecure cache/client communications with ssl; otherwise false.</span></span> <span data-ttu-id="44705-128">Essere la porta corretta che toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="44705-128">Be sure toospecify hello correct port.</span></span>
  * <span data-ttu-id="44705-129">porta non SSL Hello è disabilitata per impostazione predefinita per le nuove cache.</span><span class="sxs-lookup"><span data-stu-id="44705-129">hello non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="44705-130">Specificare true per questo hello toouse impostazione porta SSL.</span><span class="sxs-lookup"><span data-stu-id="44705-130">Specify true for this setting toouse hello SSL port.</span></span> <span data-ttu-id="44705-131">Per ulteriori informazioni sull'abilitazione della porta non SSL hello, vedere hello [porte di accesso](cache-configure.md#access-ports) sezione hello [configurare una cache](cache-configure.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="44705-131">For more information about enabling hello non-SSL port, see hello [Access Ports](cache-configure.md#access-ports) section in hello [Configure a cache](cache-configure.md) topic.</span></span>
* <span data-ttu-id="44705-132">**databaseId** – toouse quali database per la cache di dati di output specificato.</span><span class="sxs-lookup"><span data-stu-id="44705-132">**databaseId** – Specified which database toouse for cache output data.</span></span> <span data-ttu-id="44705-133">Se non specificato, viene utilizzato il valore predefinito hello pari a 0.</span><span class="sxs-lookup"><span data-stu-id="44705-133">If not specified, hello default value of 0 is used.</span></span>
* <span data-ttu-id="44705-134">**applicationName**: le chiavi vengono archiviate in Redis come `<AppName>_<SessionId>_Data`.</span><span class="sxs-lookup"><span data-stu-id="44705-134">**applicationName** – Keys are stored in redis as `<AppName>_<SessionId>_Data`.</span></span> <span data-ttu-id="44705-135">Questo schema di denominazione consente più hello tooshare di applicazioni stessa chiave.</span><span class="sxs-lookup"><span data-stu-id="44705-135">This naming scheme enables multiple applications tooshare hello same key.</span></span> <span data-ttu-id="44705-136">Questo parametro è facoltativo e se non lo si specifica, verrà usato un valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="44705-136">This parameter is optional and if you do not provide it a default value is used.</span></span>
* <span data-ttu-id="44705-137">**connectionTimeoutInMilliseconds** : questa impostazione consente connectTimeout hello toooverride impostazione nel client stackexchange. Redis hello.</span><span class="sxs-lookup"><span data-stu-id="44705-137">**connectionTimeoutInMilliseconds** – This setting allows you toooverride hello connectTimeout setting in hello StackExchange.Redis client.</span></span> <span data-ttu-id="44705-138">Se non specificato, viene utilizzato connectTimeout impostazione hello pari a 5000.</span><span class="sxs-lookup"><span data-stu-id="44705-138">If not specified, hello default connectTimeout setting of 5000 is used.</span></span> <span data-ttu-id="44705-139">Per altre informazioni, vedere [Modello di configurazione StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).</span><span class="sxs-lookup"><span data-stu-id="44705-139">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>
* <span data-ttu-id="44705-140">**operationTimeoutInMilliseconds** : questa impostazione consente toooverride hello syncTimeout impostazione nel client stackexchange. Redis hello.</span><span class="sxs-lookup"><span data-stu-id="44705-140">**operationTimeoutInMilliseconds** – This setting allows you toooverride hello syncTimeout setting in hello StackExchange.Redis client.</span></span> <span data-ttu-id="44705-141">Se non specificato, viene utilizzato hello syncTimeout impostazione predefinita di 1000.</span><span class="sxs-lookup"><span data-stu-id="44705-141">If not specified, hello default syncTimeout setting of 1000 is used.</span></span> <span data-ttu-id="44705-142">Per altre informazioni, vedere [Modello di configurazione StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).</span><span class="sxs-lookup"><span data-stu-id="44705-142">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>

<span data-ttu-id="44705-143">Aggiungere una pagina tooeach direttiva OutputCache per i quali si desidera toocache output di hello.</span><span class="sxs-lookup"><span data-stu-id="44705-143">Add an OutputCache directive tooeach page for which you wish toocache hello output.</span></span>

```
<%@ OutputCache Duration="60" VaryByParam="*" %>
```

<span data-ttu-id="44705-144">Nell'esempio precedente hello hello memorizzati nella cache pagina dati restano nella cache di hello per 60 secondi, e una versione diversa della pagina hello viene memorizzato nella cache per ogni combinazione di parametri.</span><span class="sxs-lookup"><span data-stu-id="44705-144">In hello previous example, hello cached page data remains in hello cache for 60 seconds, and a different version of hello page is cached for each parameter combination.</span></span> <span data-ttu-id="44705-145">Per ulteriori informazioni sulla direttiva OutputCache hello, vedere [ @OutputCache ](http://go.microsoft.com/fwlink/?linkid=320837).</span><span class="sxs-lookup"><span data-stu-id="44705-145">For more information about hello OutputCache directive, see [@OutputCache](http://go.microsoft.com/fwlink/?linkid=320837).</span></span>

<span data-ttu-id="44705-146">Una volta completati questi passaggi, l'applicazione è configurata toouse hello redis-Provider della Cache di Output.</span><span class="sxs-lookup"><span data-stu-id="44705-146">Once these steps are performed, your application is configured toouse hello Redis Output Cache Provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44705-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="44705-147">Next steps</span></span>
<span data-ttu-id="44705-148">Estrarre hello [Provider di stato sessione ASP.NET per Cache Redis di Azure](cache-aspnet-session-state-provider.md).</span><span class="sxs-lookup"><span data-stu-id="44705-148">Check out hello [ASP.NET Session State Provider for Azure Redis Cache](cache-aspnet-session-state-provider.md).</span></span>

