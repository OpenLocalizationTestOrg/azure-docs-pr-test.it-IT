---
title: aaaManage scadenza del contenuto web nella rete CDN di Azure | Documenti Microsoft
description: Informazioni su come toomanage scadenza del contenuto di Azure Web App o servizi basati su Cloud, ASP.NET o IIS nella rete CDN di Azure.
services: cdn
documentationcenter: .NET
author: zhangmanling
manager: erikre
editor: 
ms.assetid: bef53fcc-bb13-4002-9324-9edee9da8288
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: a0154236c3893b627f4480e0688f555964862556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-expiration-of-azure-web-appscloud-services-aspnet-or-iis-content-in-azure-cdn"></a><span data-ttu-id="dc0bc-103">Gestire la scadenza del contenuto di app Web o servizi cloud di Azure, ASP.NET o IIS nella rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="dc0bc-103">Manage expiration of Azure Web Apps/Cloud Services, ASP.NET, or IIS content in Azure CDN</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dc0bc-104">App Web/Servizi cloud di Azure, ASP.NET o IIS</span><span class="sxs-lookup"><span data-stu-id="dc0bc-104">Azure Web Apps/Cloud Services, ASP.NET, or IIS</span></span>](cdn-manage-expiration-of-cloud-service-content.md)
> * [<span data-ttu-id="dc0bc-105">Servizio BLOB del servizio di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="dc0bc-105">Azure Storage blob service</span></span>](cdn-manage-expiration-of-blob-content.md)
> 
> 

<span data-ttu-id="dc0bc-106">I file provenienti da un server Web di origine accessibile pubblicamente possono essere memorizzati nella cache della rete CDN di Azure fino allo scadere della relativa durata (TTL).</span><span class="sxs-lookup"><span data-stu-id="dc0bc-106">Files from any publicly accessible origin web server can be cached in Azure CDN until its time-to-live (TTL) elapses.</span></span>  <span data-ttu-id="dc0bc-107">Hello durata (TTL) è determinato dal hello [ *Cache-Control* intestazione](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in risposta hello HTTP dal server di origine hello.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-107">hello TTL is determined by hello [*Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in hello HTTP response from hello origin server.</span></span>  <span data-ttu-id="dc0bc-108">Questo articolo viene descritto come tooset `Cache-Control` intestazioni per le app Web di Azure, servizi Cloud di Azure, le applicazioni e siti di Internet Information Services, che sono configurati in modo analogo.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-108">This article describes how tooset `Cache-Control` headers for Azure Web Apps, Azure Cloud Services, ASP.NET applications, and Internet Information Services sites, all of which are configured similarly.</span></span>

> [!TIP]
> <span data-ttu-id="dc0bc-109">È non possibile scegliere tooset alcuna durata (TTL) su un file.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-109">You may choose tooset no TTL on a file.</span></span>  <span data-ttu-id="dc0bc-110">In tal caso, la rete CDN di Azure applica automaticamente una durata (TTL) predefinita di sette giorni.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-110">In this case, Azure CDN automatically applies a default TTL of seven days.</span></span>
> 
> <span data-ttu-id="dc0bc-111">Per ulteriori informazioni sul funzionamento toospeed toofiles di accesso e altre risorse di rete CDN di Azure, vedere hello [Panoramica della rete CDN di Azure](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dc0bc-111">For more information about how Azure CDN works toospeed up access toofiles and other resources, see hello [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

## <a name="setting-cache-control-headers-in-configuration"></a><span data-ttu-id="dc0bc-112">Impostazione delle intestazioni Cache-Control nella configurazione</span><span class="sxs-lookup"><span data-stu-id="dc0bc-112">Setting Cache-Control Headers in configuration</span></span>
<span data-ttu-id="dc0bc-113">Per il contenuto statico, ad esempio immagini e fogli di stile, è possibile controllare la frequenza di aggiornamento hello modificando hello **applicationHost. config** o **Web. config** file per l'applicazione web.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-113">For static content, such as images and style sheets, you can control hello update frequency by modifying hello **applicationHost.config** or **web.config** files for your web application.</span></span>  <span data-ttu-id="dc0bc-114">Hello **system.webServer\staticContent\clientCache** elemento nel file di configurazione hello imposterà hello `Cache-Control` intestazione per il contenuto.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-114">hello **system.webServer\staticContent\clientCache** element in hello configuration file will set hello `Cache-Control` header for your content.</span></span> <span data-ttu-id="dc0bc-115">Per **Web. config**, hello configurazione impostazioni avranno effetto su tutti gli elementi nella cartella di hello e tutte le sottocartelle, a meno che non viene sottoposto a override a livello di hello sottocartella.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-115">For **web.config**, hello configuration settings will affect everything in hello folder and all subfolders, unless overridden at hello subfolder level.</span></span>  <span data-ttu-id="dc0bc-116">Ad esempio, è possibile impostare un valore predefinito time-to-live in hello radice toohave tutto il contenuto statico memorizzato nella cache per 3 giorni, ma è presente una sottocartella con più variabile contenuto con le impostazioni della cache di 6 ore.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-116">For example, you can set a default time-to-live at hello root toohave all static content cached for 3 days, but have a subfolder that has more variable content with a cache setting of 6 hours.</span></span>  <span data-ttu-id="dc0bc-117">Per **applicationHost. config**, tutte le applicazioni hello sito verranno modificate, ma può essere sottoposto a override in **Web. config** file hello applicazioni.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-117">For **applicationHost.config**, all applications on hello site will be affected, but can be overridden in **web.config** files in hello applications.</span></span>

<span data-ttu-id="dc0bc-118">Hello codice XML seguente viene illustrato un esempio dell'impostazione **clientCache** toospecify una durata massima di 3 giorni:</span><span class="sxs-lookup"><span data-stu-id="dc0bc-118">hello following XML shows an example of setting **clientCache** toospecify a maximum age of 3 days:</span></span>  

```xml
<configuration>
    <system.webServer>
        <staticContent>
            <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00" />
        </staticContent>
    </system.webServer>
</configuration>
```

<span data-ttu-id="dc0bc-119">Specifica di **UseMaxAge** aggiunge un `Cache-Control: max-age=<nnn>` risposta toohello intestazione in base al valore di hello specificato in hello **CacheControlMaxAge** attributo.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-119">Specifying **UseMaxAge** adds a `Cache-Control: max-age=<nnn>` header toohello response based on hello value specified in hello **CacheControlMaxAge** attribute.</span></span> <span data-ttu-id="dc0bc-120">formato Hello di timespan hello è per hello **cacheControlMaxAge** attributo <days>.<hours>:<min>:<sec>.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-120">hello format of hello timespan is for hello **cacheControlMaxAge** attribute is <days>.<hours>:<min>:<sec>.</span></span> <span data-ttu-id="dc0bc-121">Per ulteriori informazioni su hello **clientCache** nodo, vedere [nella Cache del Client <clientCache> ](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).</span><span class="sxs-lookup"><span data-stu-id="dc0bc-121">For more information on hello **clientCache** node, see [Client Cache <clientCache>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).</span></span>  

## <a name="setting-cache-control-headers-in-code"></a><span data-ttu-id="dc0bc-122">Impostazione delle intestazioni Cache-Control nel codice</span><span class="sxs-lookup"><span data-stu-id="dc0bc-122">Setting Cache-Control Headers in Code</span></span>
<span data-ttu-id="dc0bc-123">Per le applicazioni ASP.NET, è possibile impostare il comportamento della cache di hello CDN a livello di programmazione dall'impostazione hello **HttpResponse** proprietà.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-123">For ASP.NET applications, you can set hello CDN caching behavior programmatically by setting hello **HttpResponse.Cache** property.</span></span> <span data-ttu-id="dc0bc-124">Per ulteriori informazioni su hello **HttpResponse** proprietà, vedere [proprietà HttpResponse cache](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) e [classe HttpCachePolicy](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span><span class="sxs-lookup"><span data-stu-id="dc0bc-124">For more information on hello **HttpResponse.Cache** property, see [HttpResponse.Cache Property](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) and [HttpCachePolicy Class](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span></span>  

<span data-ttu-id="dc0bc-125">Se si desidera il contenuto dell'applicazione di cache tooprogrammatically in ASP.NET, assicurarsi che il contenuto di hello viene contrassegnato come inseribile nella cache impostando HttpCacheability troppo*pubblica*.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-125">If you want tooprogrammatically cache application content in ASP.NET, make sure that hello content is marked as cacheable by setting HttpCacheability too*Public*.</span></span> <span data-ttu-id="dc0bc-126">Assicurarsi anche che sia impostato un validator della cache.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-126">Also, ensure that a cache validator is set.</span></span> <span data-ttu-id="dc0bc-127">validator della cache di Hello può essere una data ultima modifica timestamp impostato chiamando SetLastModified o un valore etag impostato chiamando SetETag.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-127">hello cache validator can be a Last Modified timestamp set by calling SetLastModified, or an etag value set by calling SetETag.</span></span> <span data-ttu-id="dc0bc-128">Facoltativamente, è anche possibile specificare una data di scadenza della cache chiamando SetExpires oppure affidarsi euristica hello predefinita della cache descritta in precedenza in questo documento.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-128">Optionally, you can also specify a cache expiration time by calling SetExpires, or you can rely on hello default cache heuristics described earlier in this document.</span></span>  

<span data-ttu-id="dc0bc-129">Ad esempio, toocache contenuto per un'ora, aggiungere il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="dc0bc-129">For example, toocache content for one hour, add hello following:</span></span>  

```csharp
// Set hello caching parameters.
Response.Cache.SetExpires(DateTime.Now.AddHours(1));
Response.Cache.SetCacheability(HttpCacheability.Public);
Response.Cache.SetLastModified(DateTime.Now);
```

## <a name="next-steps"></a><span data-ttu-id="dc0bc-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dc0bc-130">Next Steps</span></span>
* [<span data-ttu-id="dc0bc-131">Dettagli sugli hello **clientCache** elemento</span><span class="sxs-lookup"><span data-stu-id="dc0bc-131">Read details about hello **clientCache** element</span></span>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache)
* [<span data-ttu-id="dc0bc-132">Leggere la documentazione di hello per hello **HttpResponse** proprietà</span><span class="sxs-lookup"><span data-stu-id="dc0bc-132">Read hello documentation for hello **HttpResponse.Cache** Property</span></span>](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) 
* <span data-ttu-id="dc0bc-133">[Leggere la documentazione di hello per hello **classe HttpCachePolicy**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span><span class="sxs-lookup"><span data-stu-id="dc0bc-133">[Read hello documentation for hello **HttpCachePolicy Class**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span></span>  

