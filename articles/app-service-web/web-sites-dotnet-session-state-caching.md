---
title: Stato della sessione con Cache Redis di Azure in Servizio app di Azure
description: Informazioni su come usare Servizio cache di Azure per supportare la memorizzazione nella cache dello stato della sessione ASP.NET.
services: app-service\web
documentationcenter: .net
author: Rick-Anderson
manager: erikre
editor: none
ms.assetid: 4f98d289-2698-464d-85cd-99ec40fad1f2
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 06/27/2016
ms.author: riande
ms.openlocfilehash: 64fa909daf92b2b1f0cf4c7b334edba807fe7228
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="session-state-with-azure-redis-cache-in-azure-app-service"></a><span data-ttu-id="a4db1-103">Stato della sessione con Cache Redis di Azure in Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="a4db1-103">Session state with Azure Redis cache in Azure App Service</span></span>
<span data-ttu-id="a4db1-104">questo argomento illustra come usare il servizio Cache Redis di Azure per lo stato sessione.</span><span class="sxs-lookup"><span data-stu-id="a4db1-104">This topic explains how to use the Azure Redis Cache Service for session state.</span></span>

<span data-ttu-id="a4db1-105">Se l'app Web ASP.NET usa lo stato della sessione, sarà necessario usare un provider di stato della sessione esterno (il provider del servizio Cache Redis o un provider di stato della sessione SQL Server).</span><span class="sxs-lookup"><span data-stu-id="a4db1-105">If your ASP.NET web app uses session state, you will need to configure an external session state provider (either the Redis Cache Service or a SQL Server session state provider).</span></span> <span data-ttu-id="a4db1-106">Se si usa lo stato della sessione, e non un provider esterno, verrà applicato il limite di una sola istanza dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="a4db1-106">If you use session state, and don't use an external provider, you will be limited to one instance of your web app.</span></span> <span data-ttu-id="a4db1-107">Il servizio Cache Redis può essere abilitato con la massima rapidità e semplicità.</span><span class="sxs-lookup"><span data-stu-id="a4db1-107">The Redis Cache Service is the fastest and simplest to enable.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="a4db1-108"><a id="createcache"></a>Creare la Cache</span><span class="sxs-lookup"><span data-stu-id="a4db1-108"><a id="createcache"></a>Create the Cache</span></span>
<span data-ttu-id="a4db1-109">Per creare la cache, attenersi a [queste istruzioni](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache).</span><span class="sxs-lookup"><span data-stu-id="a4db1-109">Follow [these directions](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) to create the cache.</span></span>

## <span data-ttu-id="a4db1-110"><a id="configureproject"></a>Aggiungere il pacchetto NuGet RedisSessionStateProvider all'app Web</span><span class="sxs-lookup"><span data-stu-id="a4db1-110"><a id="configureproject"></a>Add the RedisSessionStateProvider NuGet package to your web app</span></span>
<span data-ttu-id="a4db1-111">Installare il pacchetto NuGet `RedisSessionStateProvider` .</span><span class="sxs-lookup"><span data-stu-id="a4db1-111">Install the NuGet `RedisSessionStateProvider` package.</span></span>  <span data-ttu-id="a4db1-112">Usare il comando seguente per effettuare l'installazione dalla Console di Gestione pacchetti (**Strumenti** > **Gestione pacchetti NuGet** > **Console di Gestione pacchetti**):</span><span class="sxs-lookup"><span data-stu-id="a4db1-112">Use the following command to install from the package manager console (**Tools** > **NuGet Package Manager** > **Package Manager Console**):</span></span>

  `PM> Install-Package Microsoft.Web.RedisSessionStateProvider`

<span data-ttu-id="a4db1-113">Per effettuare l'installazione da **Strumenti** > **Gestione pacchetti NuGet** > **Manage NugGet Packages for Solution** (Gestisci pacchetti NuGet per la soluzione), cercare `RedisSessionStateProvider`.</span><span class="sxs-lookup"><span data-stu-id="a4db1-113">To install from **Tools** > **NuGet Package Manager** > **Manage NugGet Packages for Solution**, search for `RedisSessionStateProvider`.</span></span>

<span data-ttu-id="a4db1-114">Per altre informazioni, vedere la [pagina relativa a RedisSessionStateProvider di NuGet](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) e la pagina [Configurare i client della cache](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).</span><span class="sxs-lookup"><span data-stu-id="a4db1-114">For more information see the [NuGet RedisSessionStateProvider page](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) and [Configure the cache client](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).</span></span>

## <span data-ttu-id="a4db1-115"><a id="configurewebconfig"></a>Modificare il file Web.Config</span><span class="sxs-lookup"><span data-stu-id="a4db1-115"><a id="configurewebconfig"></a>Modify the Web.Config File</span></span>
<span data-ttu-id="a4db1-116">Oltre a creare riferimenti ad assembly per la cache, il pacchetto NuGet aggiunge voci stub nel file *web.config* .</span><span class="sxs-lookup"><span data-stu-id="a4db1-116">In addition to making assembly references for Cache, the NuGet package adds stub entries in the *web.config* file.</span></span> 

1. <span data-ttu-id="a4db1-117">Aprire *web.config* e trovare l'elemento **sessionState** .</span><span class="sxs-lookup"><span data-stu-id="a4db1-117">Open the *web.config* and find the the **sessionState** element.</span></span>
2. <span data-ttu-id="a4db1-118">Immettere i valori relativi a `host`, `accessKey`, `port` (la porta SSL deve essere 6380) e impostare `SSL` su `true`</span><span class="sxs-lookup"><span data-stu-id="a4db1-118">Enter the values for `host`, `accessKey`, `port` (the SSL port should be 6380), and set `SSL` to `true`.</span></span> <span data-ttu-id="a4db1-119">Questi valori possono essere ottenuti dal pannello del [portale di Azure](http://go.microsoft.com/fwlink/?LinkId=529715) per l'istanza della cache.</span><span class="sxs-lookup"><span data-stu-id="a4db1-119">These values can be obtained from the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) blade for your cache instance.</span></span> <span data-ttu-id="a4db1-120">Per altre informazioni, vedere [Connettersi alla cache](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache).</span><span class="sxs-lookup"><span data-stu-id="a4db1-120">For more information, see [Connect to the cache](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache).</span></span> <span data-ttu-id="a4db1-121">Si tenga presente che per le nuove cache la porta senza SSL è disabilitata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="a4db1-121">Note that the non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="a4db1-122">Per altre informazioni sull'abilitazione della porta senza SSL, vedere la sezione relativa alle [porte di accesso](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) nell'argomento [Configurare una cache in Cache Redis di Azure](https://msdn.microsoft.com/library/azure/dn793612.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4db1-122">For more information about enabling the non-SSL port, see the [Access Ports](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) section in the [Configure a cache in Azure Redis Cache](https://msdn.microsoft.com/library/azure/dn793612.aspx) topic.</span></span> <span data-ttu-id="a4db1-123">Il markup seguente mostra le modifiche per il *Web. config* in modo specifico le modifiche apportate al file *porta*, *host*, accessKey * e *ssl* .</span><span class="sxs-lookup"><span data-stu-id="a4db1-123">The following markup shows the changes to the *web.config* file, specifically the changes to *port*, *host*, accessKey*, and *ssl*.</span></span>
   
          <system.web>;
            <customErrors mode="Off" />;
            <authentication mode="None" />;
            <compilation debug="true" targetFramework="4.5" />;
            <httpRuntime targetFramework="4.5" />;
            <sessionState mode="Custom" customProvider="RedisSessionProvider">;
              <providers>;  
                  <!--<add name="RedisSessionProvider" 
                    host = "127.0.0.1" [String]
                    port = "" [number]
                    accessKey = "" [String]
                    ssl = "false" [true|false]
                    throwOnError = "true" [true|false]
                    retryTimeoutInMilliseconds = "0" [number]
                    databaseId = "0" [number]
                    applicationName = "" [String]
                  />;-->;
                 <add name="RedisSessionProvider" 
                      type="Microsoft.Web.Redis.RedisSessionStateProvider" 
                      port="6380"
                      host="movie2.redis.cache.windows.net" 
                      accessKey="m7PNV60CrvKpLqMUxosC3dSe6kx9nQ6jP5del8TmADk=" 
                      ssl="true" />;
              <!--<add name="MySessionStateStore" type="Microsoft.Web.Redis.RedisSessionStateProvider" host="127.0.0.1" accessKey="" ssl="false" />;-->;
              </providers>;
            </sessionState>;
          </system.web>;

## <span data-ttu-id="a4db1-124"><a id="usesessionobject"></a> Utilizzo dell'oggetto Session nel codice</span><span class="sxs-lookup"><span data-stu-id="a4db1-124"><a id="usesessionobject"></a> Use the Session Object in Code</span></span>
<span data-ttu-id="a4db1-125">Il passaggio finale consiste nell'iniziare a utilizzare l'oggetto Session nel proprio codice ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="a4db1-125">The final step is to begin using the Session object in your ASP.NET code.</span></span> <span data-ttu-id="a4db1-126">Aggiungere oggetti allo stato sessione usando il metodo **Session.Add**.</span><span class="sxs-lookup"><span data-stu-id="a4db1-126">You add objects to session state by using the **Session.Add** method.</span></span> <span data-ttu-id="a4db1-127">che utilizza coppie chiave-valore per memorizzare elementi nella cache di stato sessione.</span><span class="sxs-lookup"><span data-stu-id="a4db1-127">This method uses key-value pairs to store items in the session state cache.</span></span>

    string strValue = "yourvalue";
    Session.Add("yourkey", strValue);

<span data-ttu-id="a4db1-128">Il codice seguente recupera questo valore dallo stato sessione.</span><span class="sxs-lookup"><span data-stu-id="a4db1-128">The following code retrieves this value from session state.</span></span>

    object objValue = Session["yourkey"];
    if (objValue != null)
       strValue = (string)objValue;    

<span data-ttu-id="a4db1-129">È inoltre possibile usare Cache Redis per nascondere gli oggetti nell'app Web.</span><span class="sxs-lookup"><span data-stu-id="a4db1-129">You can also use the Redis Cache to cache objects in your web app.</span></span> <span data-ttu-id="a4db1-130">Per altre informazioni, vedere il blog relativo all' applicazione per filmati [MVC con Cache Redis di Azure in 15 minuti](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).</span><span class="sxs-lookup"><span data-stu-id="a4db1-130">For more info, see [MVC movie app with Azure Redis Cache in 15 minutes](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).</span></span>
<span data-ttu-id="a4db1-131">Per altre informazioni su come usare lo stato sessione ASP.NET, vedere [Cenni preliminari sullo stato della sessione ASP.NET][ASP.NET Session State Overview].</span><span class="sxs-lookup"><span data-stu-id="a4db1-131">For more details about how to use ASP.NET session state, see [ASP.NET Session State Overview][ASP.NET Session State Overview].</span></span>

> [!NOTE]
> <span data-ttu-id="a4db1-132">Per iniziare a usare il servizio app di Azure prima di registrarsi per ottenere un account Azure, andare a [Prova il servizio app](https://azure.microsoft.com/try/app-service/), dove è possibile creare un'app Web iniziale temporanea nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="a4db1-132">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="a4db1-133">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="a4db1-133">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="a4db1-134">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="a4db1-134">What's changed</span></span>
* <span data-ttu-id="a4db1-135">Per una guida relativa al passaggio da Siti Web al servizio app, vedere [Servizio app di Azure e impatto sui servizi di Azure esistenti](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="a4db1-135">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>
  
  <span data-ttu-id="a4db1-136">*Autore: [Rick Anderson](https://twitter.com/RickAndMSFT)*</span><span class="sxs-lookup"><span data-stu-id="a4db1-136">*By [Rick Anderson](https://twitter.com/RickAndMSFT)*</span></span>

[installed the latest]: http://www.windowsazure.com/downloads/?sdk=net  
[ASP.NET Session State Overview]: http://msdn.microsoft.com/library/ms178581.aspx

[NewIcon]: ./media/web-sites-dotnet-session-state-caching/CacheScreenshot_NewButton.png
[NewCacheDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CreateOptions.png
[CacheIcon]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheIcon.png
[NuGetDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_NuGet.png
[OutputConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_OC_WebConfig.png
[CacheConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheConfig.png
[EndpointURL]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_EndpointURL.png
[ManageKeys]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_ManageAccessKeys.png

