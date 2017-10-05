---
title: Provider di cache di output ASP.NET della Cache
description: Informazioni su come memorizzare nella cache l'output della pagina ASP.NET mediante Cache Redis di Azure
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
ms.openlocfilehash: 845f25637a0e48460fc76c1ee36060274b3cec38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="aspnet-output-cache-provider-for-azure-redis-cache"></a><span data-ttu-id="f145d-103">Provider di cache di output ASP.NET per la Cache Redis di Azure</span><span class="sxs-lookup"><span data-stu-id="f145d-103">ASP.NET Output Cache Provider for Azure Redis Cache</span></span>
<span data-ttu-id="f145d-104">Il provider di cache Redis di output è un meccanismo di memorizzazione out-of-process per i dati della cache di output.</span><span class="sxs-lookup"><span data-stu-id="f145d-104">The Redis Output Cache Provider is an out-of-process storage mechanism for output cache data.</span></span> <span data-ttu-id="f145d-105">Tali dati sono specificamente utilizzati per le risposte HTTP complete (memorizzazione nella cache di output delle pagine).</span><span class="sxs-lookup"><span data-stu-id="f145d-105">This data is specifically for full HTTP responses (page output caching).</span></span> <span data-ttu-id="f145d-106">Il provider viene inserito nel nuovo punto di estendibilità del provider di cache di output che è stato introdotto in ASP.NET 4.</span><span class="sxs-lookup"><span data-stu-id="f145d-106">The provider plugs into the new output cache provider extensibility point that was introduced in ASP.NET 4.</span></span>

<span data-ttu-id="f145d-107">Per usare il provider di cache Redis di output, configurare prima di tutto la cache, quindi configurare l'applicazione ASP.NET usando il pacchetto NuGet del provider di cache Redis di output.</span><span class="sxs-lookup"><span data-stu-id="f145d-107">To use the Redis Output Cache Provider, first configure your cache, and then configure your ASP.NET application using the Redis Output Cache Provider NuGet package.</span></span> <span data-ttu-id="f145d-108">Questo argomento offre indicazioni sulla configurazione dell'applicazione per l'uso del provider di cache Redis di output.</span><span class="sxs-lookup"><span data-stu-id="f145d-108">This topic provides guidance on configuring your application to use the Redis Output Cache Provider.</span></span> <span data-ttu-id="f145d-109">Per altre informazioni sulla creazione e sulla configurazione di un'istanza della Cache Redis di Azure, vedere [Creare una cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span><span class="sxs-lookup"><span data-stu-id="f145d-109">For more information about creating and configuring an Azure Redis Cache instance, see [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span></span>

## <a name="store-aspnet-page-output-in-the-cache"></a><span data-ttu-id="f145d-110">Archiviare l'output della pagina ASP.NET nella cache</span><span class="sxs-lookup"><span data-stu-id="f145d-110">Store ASP.NET page output in the cache</span></span>
<span data-ttu-id="f145d-111">Per configurare un'applicazione client in Visual Studio con il pacchetto NuGet Redis Cache Session State, fare clic su **Gestione pacchetti NuGet** e quindi su **Console di Gestione pacchetti** dal menu **Strumenti**.</span><span class="sxs-lookup"><span data-stu-id="f145d-111">To configure a client application in Visual Studio using the Redis Cache Session State NuGet package, click **NuGet Package Manager**, **Package Manager Console** from the **Tools** menu.</span></span>

<span data-ttu-id="f145d-112">Eseguire questo comando nella finestra `Package Manager Console`.</span><span class="sxs-lookup"><span data-stu-id="f145d-112">Run the following command from the `Package Manager Console` window.</span></span>
    
```
Install-Package Microsoft.Web.RedisOutputCacheProvider
```

<span data-ttu-id="f145d-113">Il pacchetto NuGet del provider di cache Redis di output ha una dipendenza dal pacchetto StackExchange.Redis.StrongName.</span><span class="sxs-lookup"><span data-stu-id="f145d-113">The Redis Output Cache Provider NuGet package has a dependency on the StackExchange.Redis.StrongName package.</span></span> <span data-ttu-id="f145d-114">Se il pacchetto StackExchange.Redis.StrongName non è presente nel progetto, viene installato.</span><span class="sxs-lookup"><span data-stu-id="f145d-114">If the StackExchange.Redis.StrongName package is not present in your project, it is installed.</span></span> <span data-ttu-id="f145d-115">Per altre informazioni sul pacchetto NuGet provider di cache Redis di output, vedere la pagina di NuGet su [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/).</span><span class="sxs-lookup"><span data-stu-id="f145d-115">For more information about the Redis Output Cache Provider NuGet package, see the [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) NuGet page.</span></span>

>[!NOTE]
><span data-ttu-id="f145d-116">Oltre al pacchetto StackExchange.Redis.StrongName con nome sicuro, è disponibile anche la versione StackExchange.Redis priva di nome sicuro.</span><span class="sxs-lookup"><span data-stu-id="f145d-116">In addition to the strong-named StackExchange.Redis.StrongName package, there is also the StackExchange.Redis non-strong-named version.</span></span> <span data-ttu-id="f145d-117">Se il progetto usa la versione di StackExchange.Redis con nome non sicuro, è necessario disinstallarla per evitare conflitti di denominazione nel progetto.</span><span class="sxs-lookup"><span data-stu-id="f145d-117">If your project is using the non-strong-named StackExchange.Redis version you must uninstall it, otherwise you get naming conflicts in your project.</span></span> <span data-ttu-id="f145d-118">Per altre informazioni su questi pacchetti, vedere [Configurare i client della cache .NET](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span><span class="sxs-lookup"><span data-stu-id="f145d-118">For more information about these packages, see [Configure .NET cache clients](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span></span>
>
>

<span data-ttu-id="f145d-119">Il pacchetto NuGet scarica e aggiunge i riferimenti all'assembly richiesto e aggiunge la sezione seguente al file web.config.</span><span class="sxs-lookup"><span data-stu-id="f145d-119">The NuGet package downloads and adds the required assembly references and adds the following section into your web.config file.</span></span> <span data-ttu-id="f145d-120">Questa sezione contiene la configurazione richiesta dall'applicazione ASP.NET per usare il provider di cache di output Redis.</span><span class="sxs-lookup"><span data-stu-id="f145d-120">This section contains the required configuration for your ASP.NET application to use the Redis Output Cache Provider.</span></span>

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

<span data-ttu-id="f145d-121">La sezione commentata fornisce un esempio degli attributi e delle impostazioni di esempio per ogni attributo.</span><span class="sxs-lookup"><span data-stu-id="f145d-121">The commented section provides an example of the attributes and sample settings for each attribute.</span></span>

<span data-ttu-id="f145d-122">Configurare gli attributi con i valori del pannello Cache nel portale di Microsoft Azure e configurare gli altri valori come desiderato.</span><span class="sxs-lookup"><span data-stu-id="f145d-122">Configure the attributes with the values from your cache blade in the Microsoft Azure portal, and configure the other values as desired.</span></span> <span data-ttu-id="f145d-123">Per istruzioni sull'accesso alle proprietà della cache, vedere [Configurare le impostazioni di Cache Redis di Azure](cache-configure.md#configure-redis-cache-settings).</span><span class="sxs-lookup"><span data-stu-id="f145d-123">For instructions on accessing your cache properties, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

* <span data-ttu-id="f145d-124">**host** : specificare l'endpoint della cache.</span><span class="sxs-lookup"><span data-stu-id="f145d-124">**host** – specify your cache endpoint.</span></span>
* <span data-ttu-id="f145d-125">**port** : usare la porta non SSL o la porta SSL, in base alle impostazioni SSL.</span><span class="sxs-lookup"><span data-stu-id="f145d-125">**port** – use either your non-SSL port or your SSL port, depending on the ssl settings.</span></span>
* <span data-ttu-id="f145d-126">**accessKey** : usare la chiave primaria o secondaria per la cache.</span><span class="sxs-lookup"><span data-stu-id="f145d-126">**accessKey** – use either the primary or secondary key for your cache.</span></span>
* <span data-ttu-id="f145d-127">**ssl** :  true per proteggere le comunicazioni cache/client con SSL; in caso contrario, false.</span><span class="sxs-lookup"><span data-stu-id="f145d-127">**ssl** – true if you want to secure cache/client communications with ssl; otherwise false.</span></span> <span data-ttu-id="f145d-128">Assicurarsi di specificare la porta corretta.</span><span class="sxs-lookup"><span data-stu-id="f145d-128">Be sure to specify the correct port.</span></span>
  * <span data-ttu-id="f145d-129">Per le nuove cache la porta senza SSL è disabilitata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="f145d-129">The non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="f145d-130">Specificare true per questa impostazione per usare la porta SSL.</span><span class="sxs-lookup"><span data-stu-id="f145d-130">Specify true for this setting to use the SSL port.</span></span> <span data-ttu-id="f145d-131">Per altre informazioni sull'abilitazione della porta senza SSL, vedere la sezione [Porte di accesso](cache-configure.md#access-ports) nell'argomento [Configurare una cache](cache-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f145d-131">For more information about enabling the non-SSL port, see the [Access Ports](cache-configure.md#access-ports) section in the [Configure a cache](cache-configure.md) topic.</span></span>
* <span data-ttu-id="f145d-132">**databaseId** : specifica il database da usare per i dati di output della cache.</span><span class="sxs-lookup"><span data-stu-id="f145d-132">**databaseId** – Specified which database to use for cache output data.</span></span> <span data-ttu-id="f145d-133">Se non è specificato alcun valore, verrà usato il valore predefinito 0.</span><span class="sxs-lookup"><span data-stu-id="f145d-133">If not specified, the default value of 0 is used.</span></span>
* <span data-ttu-id="f145d-134">**applicationName**: le chiavi vengono archiviate in Redis come `<AppName>_<SessionId>_Data`.</span><span class="sxs-lookup"><span data-stu-id="f145d-134">**applicationName** – Keys are stored in redis as `<AppName>_<SessionId>_Data`.</span></span> <span data-ttu-id="f145d-135">Questo schema di denominazione consente a più applicazioni di condividere la stessa chiave.</span><span class="sxs-lookup"><span data-stu-id="f145d-135">This naming scheme enables multiple applications to share the same key.</span></span> <span data-ttu-id="f145d-136">Questo parametro è facoltativo e se non lo si specifica, verrà usato un valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="f145d-136">This parameter is optional and if you do not provide it a default value is used.</span></span>
* <span data-ttu-id="f145d-137">**connectionTimeoutInMilliseconds** : questa impostazione consente di eseguire l'override dell'impostazione connectTimeout nel client StackExchange.Redis.</span><span class="sxs-lookup"><span data-stu-id="f145d-137">**connectionTimeoutInMilliseconds** – This setting allows you to override the connectTimeout setting in the StackExchange.Redis client.</span></span> <span data-ttu-id="f145d-138">Se non viene specificato alcun valore, verrà usata l'impostazione di connectTimeout predefinita pari a 5000.</span><span class="sxs-lookup"><span data-stu-id="f145d-138">If not specified, the default connectTimeout setting of 5000 is used.</span></span> <span data-ttu-id="f145d-139">Per altre informazioni, vedere [Modello di configurazione StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).</span><span class="sxs-lookup"><span data-stu-id="f145d-139">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>
* <span data-ttu-id="f145d-140">**operationTimeoutInMilliseconds** : questa impostazione consente di eseguire l'override dell'impostazione syncTimeout nel client StackExchange.Redis.</span><span class="sxs-lookup"><span data-stu-id="f145d-140">**operationTimeoutInMilliseconds** – This setting allows you to override the syncTimeout setting in the StackExchange.Redis client.</span></span> <span data-ttu-id="f145d-141">Se non viene specificato alcun valore, verrà usata l'impostazione di syncTimeout predefinita pari a 1000.</span><span class="sxs-lookup"><span data-stu-id="f145d-141">If not specified, the default syncTimeout setting of 1000 is used.</span></span> <span data-ttu-id="f145d-142">Per altre informazioni, vedere [Modello di configurazione StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).</span><span class="sxs-lookup"><span data-stu-id="f145d-142">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>

<span data-ttu-id="f145d-143">Aggiungere una direttiva OutputCache a ogni pagina per cui si desidera memorizzare l'output nella cache.</span><span class="sxs-lookup"><span data-stu-id="f145d-143">Add an OutputCache directive to each page for which you wish to cache the output.</span></span>

```
<%@ OutputCache Duration="60" VaryByParam="*" %>
```

<span data-ttu-id="f145d-144">Nell'esempio precedente, i dati delle pagine rimangono memorizzati nella cache per 60 secondi e per ogni combinazione di parametri viene memorizzata nella cache una versione diversa della pagina.</span><span class="sxs-lookup"><span data-stu-id="f145d-144">In the previous example, the cached page data remains in the cache for 60 seconds, and a different version of the page is cached for each parameter combination.</span></span> <span data-ttu-id="f145d-145">Per altre informazioni sulla direttiva OutputCache, vedere [@OutputCache](http://go.microsoft.com/fwlink/?linkid=320837).</span><span class="sxs-lookup"><span data-stu-id="f145d-145">For more information about the OutputCache directive, see [@OutputCache](http://go.microsoft.com/fwlink/?linkid=320837).</span></span>

<span data-ttu-id="f145d-146">Dopo l'esecuzione di questi passaggi, l'applicazione è configurata per l'uso del provider di cache di output Redis.</span><span class="sxs-lookup"><span data-stu-id="f145d-146">Once these steps are performed, your application is configured to use the Redis Output Cache Provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f145d-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f145d-147">Next steps</span></span>
<span data-ttu-id="f145d-148">Vedere [Provider di stato della sessione ASP.NET per Cache Redis di Azure](cache-aspnet-session-state-provider.md).</span><span class="sxs-lookup"><span data-stu-id="f145d-148">Check out the [ASP.NET Session State Provider for Azure Redis Cache](cache-aspnet-session-state-provider.md).</span></span>

