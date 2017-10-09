---
title: stato aaaSession con Azure Redis cache in Azure App Service
description: Informazioni su come toouse hello servizio Cache di Azure toosupport ASP.NET sessione dello stato di memorizzazione nella cache.
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
ms.openlocfilehash: f689b6754ea072aa195f822ab6482f4bf2748375
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="session-state-with-azure-redis-cache-in-azure-app-service"></a><span data-ttu-id="736a2-103">Stato della sessione con Cache Redis di Azure in Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="736a2-103">Session state with Azure Redis cache in Azure App Service</span></span>
<span data-ttu-id="736a2-104">In questo argomento viene illustrato come toouse hello servizio Cache Redis di Azure per lo stato della sessione.</span><span class="sxs-lookup"><span data-stu-id="736a2-104">This topic explains how toouse hello Azure Redis Cache Service for session state.</span></span>

<span data-ttu-id="736a2-105">Se l'app web ASP.NET utilizza lo stato della sessione, è necessario tooconfigure un provider di stato sessione esterno (servizio Cache Redis hello o un provider di stato sessione SQL Server).</span><span class="sxs-lookup"><span data-stu-id="736a2-105">If your ASP.NET web app uses session state, you will need tooconfigure an external session state provider (either hello Redis Cache Service or a SQL Server session state provider).</span></span> <span data-ttu-id="736a2-106">Se si utilizza lo stato della sessione e non utilizza un provider esterno, sarà limitato tooone istanza dell'app web.</span><span class="sxs-lookup"><span data-stu-id="736a2-106">If you use session state, and don't use an external provider, you will be limited tooone instance of your web app.</span></span> <span data-ttu-id="736a2-107">Servizio Cache Redis Hello è hello più semplice e rapido tooenable.</span><span class="sxs-lookup"><span data-stu-id="736a2-107">hello Redis Cache Service is hello fastest and simplest tooenable.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="736a2-108"><a id="createcache"></a>Creare una Cache di hello</span><span class="sxs-lookup"><span data-stu-id="736a2-108"><a id="createcache"></a>Create hello Cache</span></span>
<span data-ttu-id="736a2-109">Seguire [queste direzioni](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) toocreate cache di hello.</span><span class="sxs-lookup"><span data-stu-id="736a2-109">Follow [these directions](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) toocreate hello cache.</span></span>

## <span data-ttu-id="736a2-110"><a id="configureproject"></a>Aggiungere hello RedisSessionStateProvider NuGet pacchetto tooyour web app</span><span class="sxs-lookup"><span data-stu-id="736a2-110"><a id="configureproject"></a>Add hello RedisSessionStateProvider NuGet package tooyour web app</span></span>
<span data-ttu-id="736a2-111">Installare hello NuGet `RedisSessionStateProvider` pacchetto.</span><span class="sxs-lookup"><span data-stu-id="736a2-111">Install hello NuGet `RedisSessionStateProvider` package.</span></span>  <span data-ttu-id="736a2-112">Comando che segue di hello utilizzare tooinstall dalla console di gestione pacchetti hello (**strumenti** > **Gestione pacchetti NuGet** > **Package Manager Console**):</span><span class="sxs-lookup"><span data-stu-id="736a2-112">Use hello following command tooinstall from hello package manager console (**Tools** > **NuGet Package Manager** > **Package Manager Console**):</span></span>

  `PM> Install-Package Microsoft.Web.RedisSessionStateProvider`

<span data-ttu-id="736a2-113">tooinstall da **strumenti** > **Gestione pacchetti NuGet** > **gestire NugGet pacchetti per la soluzione**, cercare `RedisSessionStateProvider`.</span><span class="sxs-lookup"><span data-stu-id="736a2-113">tooinstall from **Tools** > **NuGet Package Manager** > **Manage NugGet Packages for Solution**, search for `RedisSessionStateProvider`.</span></span>

<span data-ttu-id="736a2-114">Per ulteriori informazioni, vedere hello [pagina NuGet RedisSessionStateProvider](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) e [client della cache di hello configura](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).</span><span class="sxs-lookup"><span data-stu-id="736a2-114">For more information see hello [NuGet RedisSessionStateProvider page](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) and [Configure hello cache client](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).</span></span>

## <span data-ttu-id="736a2-115"><a id="configurewebconfig"></a>Modificare il File Web. config hello</span><span class="sxs-lookup"><span data-stu-id="736a2-115"><a id="configurewebconfig"></a>Modify hello Web.Config File</span></span>
<span data-ttu-id="736a2-116">Inoltre toomaking assembly fa riferimento per la Cache, il pacchetto NuGet di hello aggiunge voci stub hello *Web. config* file.</span><span class="sxs-lookup"><span data-stu-id="736a2-116">In addition toomaking assembly references for Cache, hello NuGet package adds stub entries in hello *web.config* file.</span></span> 

1. <span data-ttu-id="736a2-117">Aprire hello *Web. config* e trovare hello hello **sessionState** elemento.</span><span class="sxs-lookup"><span data-stu-id="736a2-117">Open hello *web.config* and find hello hello **sessionState** element.</span></span>
2. <span data-ttu-id="736a2-118">Immettere i valori hello per `host`, `accessKey`, `port` (hello porta SSL deve essere 6380) e impostare `SSL` troppo`true`.</span><span class="sxs-lookup"><span data-stu-id="736a2-118">Enter hello values for `host`, `accessKey`, `port` (hello SSL port should be 6380), and set `SSL` too`true`.</span></span> <span data-ttu-id="736a2-119">Questi valori possono essere ottenuti da hello [portale Azure](http://go.microsoft.com/fwlink/?LinkId=529715) pannello per l'istanza di cache.</span><span class="sxs-lookup"><span data-stu-id="736a2-119">These values can be obtained from hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) blade for your cache instance.</span></span> <span data-ttu-id="736a2-120">Per ulteriori informazioni, vedere [connessione della cache toohello](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache).</span><span class="sxs-lookup"><span data-stu-id="736a2-120">For more information, see [Connect toohello cache](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache).</span></span> <span data-ttu-id="736a2-121">Si noti che la porta non SSL di hello è disattivata per impostazione predefinita per le nuove cache.</span><span class="sxs-lookup"><span data-stu-id="736a2-121">Note that hello non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="736a2-122">Per ulteriori informazioni sull'abilitazione della porta non SSL hello, vedere hello [porte di accesso](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) sezione hello [configurare una cache in Cache Redis di Azure](https://msdn.microsoft.com/library/azure/dn793612.aspx) argomento.</span><span class="sxs-lookup"><span data-stu-id="736a2-122">For more information about enabling hello non-SSL port, see hello [Access Ports](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) section in hello [Configure a cache in Azure Redis Cache](https://msdn.microsoft.com/library/azure/dn793612.aspx) topic.</span></span> <span data-ttu-id="736a2-123">Hello markup seguente viene illustrato hello modifiche toohello *Web. config* file, in modo specifico le modifiche di hello troppo*porta*, *host*, accessKey * e *ssl*.</span><span class="sxs-lookup"><span data-stu-id="736a2-123">hello following markup shows hello changes toohello *web.config* file, specifically hello changes too*port*, *host*, accessKey*, and *ssl*.</span></span>
   
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

## <span data-ttu-id="736a2-124"><a id="usesessionobject"></a>Utilizzare hello oggetto di sessione nel codice</span><span class="sxs-lookup"><span data-stu-id="736a2-124"><a id="usesessionobject"></a> Use hello Session Object in Code</span></span>
<span data-ttu-id="736a2-125">passaggio finale Hello è toobegin utilizzando l'oggetto sessione hello in codice ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="736a2-125">hello final step is toobegin using hello Session object in your ASP.NET code.</span></span> <span data-ttu-id="736a2-126">Si aggiunge lo stato di toosession oggetti utilizzando hello **Session.Add** metodo.</span><span class="sxs-lookup"><span data-stu-id="736a2-126">You add objects toosession state by using hello **Session.Add** method.</span></span> <span data-ttu-id="736a2-127">Questo metodo Usa gli elementi di coppie chiave-valore toostore nella cache di stato sessione hello.</span><span class="sxs-lookup"><span data-stu-id="736a2-127">This method uses key-value pairs toostore items in hello session state cache.</span></span>

    string strValue = "yourvalue";
    Session.Add("yourkey", strValue);

<span data-ttu-id="736a2-128">Hello seguente codice recupera il valore dallo stato sessione.</span><span class="sxs-lookup"><span data-stu-id="736a2-128">hello following code retrieves this value from session state.</span></span>

    object objValue = Session["yourkey"];
    if (objValue != null)
       strValue = (string)objValue;    

<span data-ttu-id="736a2-129">È inoltre possibile utilizzare oggetti di toocache Cache Redis di hello nell'app web.</span><span class="sxs-lookup"><span data-stu-id="736a2-129">You can also use hello Redis Cache toocache objects in your web app.</span></span> <span data-ttu-id="736a2-130">Per altre informazioni, vedere il blog relativo all' applicazione per filmati [MVC con Cache Redis di Azure in 15 minuti](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).</span><span class="sxs-lookup"><span data-stu-id="736a2-130">For more info, see [MVC movie app with Azure Redis Cache in 15 minutes](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).</span></span>
<span data-ttu-id="736a2-131">Per ulteriori informazioni su come toouse lo stato della sessione ASP.NET, vedere [panoramica dello stato della sessione di ASP.NET][ASP.NET Session State Overview].</span><span class="sxs-lookup"><span data-stu-id="736a2-131">For more details about how toouse ASP.NET session state, see [ASP.NET Session State Overview][ASP.NET Session State Overview].</span></span>

> [!NOTE]
> <span data-ttu-id="736a2-132">Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="736a2-132">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="736a2-133">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="736a2-133">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="736a2-134">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="736a2-134">What's changed</span></span>
* <span data-ttu-id="736a2-135">Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="736a2-135">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>
  
  <span data-ttu-id="736a2-136">*Autore: [Rick Anderson](https://twitter.com/RickAndMSFT)*</span><span class="sxs-lookup"><span data-stu-id="736a2-136">*By [Rick Anderson](https://twitter.com/RickAndMSFT)*</span></span>

[installed hello latest]: http://www.windowsazure.com/downloads/?sdk=net  
[ASP.NET Session State Overview]: http://msdn.microsoft.com/library/ms178581.aspx

[NewIcon]: ./media/web-sites-dotnet-session-state-caching/CacheScreenshot_NewButton.png
[NewCacheDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CreateOptions.png
[CacheIcon]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheIcon.png
[NuGetDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_NuGet.png
[OutputConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_OC_WebConfig.png
[CacheConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheConfig.png
[EndpointURL]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_EndpointURL.png
[ManageKeys]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_ManageAccessKeys.png

