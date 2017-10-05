---
title: Gestire la scadenza di contenuti Web nella rete CDN di Azure | Microsoft Docs
description: Informazioni su come gestire la scadenza del contenuto di app Web o servizi cloud di Azure, ASP.NET o IIS nella rete CDN di Azure.
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
ms.openlocfilehash: c207d780857a61d4b1fc0f39e6185cae67abc955
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-expiration-of-azure-web-appscloud-services-aspnet-or-iis-content-in-azure-cdn"></a><span data-ttu-id="9dbd5-103">Gestire la scadenza del contenuto di app Web o servizi cloud di Azure, ASP.NET o IIS nella rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="9dbd5-103">Manage expiration of Azure Web Apps/Cloud Services, ASP.NET, or IIS content in Azure CDN</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9dbd5-104">App Web/Servizi cloud di Azure, ASP.NET o IIS</span><span class="sxs-lookup"><span data-stu-id="9dbd5-104">Azure Web Apps/Cloud Services, ASP.NET, or IIS</span></span>](cdn-manage-expiration-of-cloud-service-content.md)
> * [<span data-ttu-id="9dbd5-105">Servizio BLOB del servizio di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="9dbd5-105">Azure Storage blob service</span></span>](cdn-manage-expiration-of-blob-content.md)
> 
> 

<span data-ttu-id="9dbd5-106">I file provenienti da un server Web di origine accessibile pubblicamente possono essere memorizzati nella cache della rete CDN di Azure fino allo scadere della relativa durata (TTL).</span><span class="sxs-lookup"><span data-stu-id="9dbd5-106">Files from any publicly accessible origin web server can be cached in Azure CDN until its time-to-live (TTL) elapses.</span></span>  <span data-ttu-id="9dbd5-107">La durata (TTL) è determinata dall'[intestazione *Cache-Control*](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) nella risposta HTTP del server di origine.</span><span class="sxs-lookup"><span data-stu-id="9dbd5-107">The TTL is determined by the [*Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in the HTTP response from the origin server.</span></span>  <span data-ttu-id="9dbd5-108">Questo articolo descrive come impostare le intestazioni `Cache-Control` per App Web di Azure, Servizi cloud di Azure, applicazioni ASP.NET e siti Internet Information Services, che hanno tutti una configurazione simile.</span><span class="sxs-lookup"><span data-stu-id="9dbd5-108">This article describes how to set `Cache-Control` headers for Azure Web Apps, Azure Cloud Services, ASP.NET applications, and Internet Information Services sites, all of which are configured similarly.</span></span>

> [!TIP]
> <span data-ttu-id="9dbd5-109">È possibile scegliere di non impostare alcuna durata (TTL) per un file.</span><span class="sxs-lookup"><span data-stu-id="9dbd5-109">You may choose to set no TTL on a file.</span></span>  <span data-ttu-id="9dbd5-110">In tal caso, la rete CDN di Azure applica automaticamente una durata (TTL) predefinita di sette giorni.</span><span class="sxs-lookup"><span data-stu-id="9dbd5-110">In this case, Azure CDN automatically applies a default TTL of seven days.</span></span>
> 
> <span data-ttu-id="9dbd5-111">Per altre informazioni sull'uso della rete CDN di Azure per velocizzare l'accesso a file e altre risorse, vedere la [panoramica della rete CDN di Azure](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9dbd5-111">For more information about how Azure CDN works to speed up access to files and other resources, see the [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

## <a name="setting-cache-control-headers-in-configuration"></a><span data-ttu-id="9dbd5-112">Impostazione delle intestazioni Cache-Control nella configurazione</span><span class="sxs-lookup"><span data-stu-id="9dbd5-112">Setting Cache-Control Headers in configuration</span></span>
<span data-ttu-id="9dbd5-113">Per il contenuto statico, come immagini e fogli di stile, è possibile controllare la frequenza di aggiornamento modificando i file **applicationHost.config** o **web.config** per l'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="9dbd5-113">For static content, such as images and style sheets, you can control the update frequency by modifying the **applicationHost.config** or **web.config** files for your web application.</span></span>  <span data-ttu-id="9dbd5-114">L'elemento **system.webServer\staticContent\clientCache** nel file di configurazione imposterà l'intestazione `Cache-Control` per il contenuto.</span><span class="sxs-lookup"><span data-stu-id="9dbd5-114">The **system.webServer\staticContent\clientCache** element in the configuration file will set the `Cache-Control` header for your content.</span></span> <span data-ttu-id="9dbd5-115">Per **web.config**, le impostazioni di configurazione influiranno su qualsiasi elemento presente nella cartella e in tutte le sottocartelle, a meno di non eseguirne l'override a livello di sottocartella.</span><span class="sxs-lookup"><span data-stu-id="9dbd5-115">For **web.config**, the configuration settings will affect everything in the folder and all subfolders, unless overridden at the subfolder level.</span></span>  <span data-ttu-id="9dbd5-116">Ad esempio, è possibile impostare una durata (TTL) predefinita nella radice per memorizzare nella cache tutto il contenuto statico per tre giorni, ma impostare un valore di sei ore per una sottocartella che include contenuto più variabile.</span><span class="sxs-lookup"><span data-stu-id="9dbd5-116">For example, you can set a default time-to-live at the root to have all static content cached for 3 days, but have a subfolder that has more variable content with a cache setting of 6 hours.</span></span>  <span data-ttu-id="9dbd5-117">Per **applicationHost.config**, tutte le applicazioni nel sito saranno interessate, ma è possibile eseguirne l'override nei file **web.config** nelle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="9dbd5-117">For **applicationHost.config**, all applications on the site will be affected, but can be overridden in **web.config** files in the applications.</span></span>

<span data-ttu-id="9dbd5-118">L'esempio di codice XML seguente mostra l'impostazione di **clientCache** in modo da specificare una durata massima di tre giorni:</span><span class="sxs-lookup"><span data-stu-id="9dbd5-118">The following XML shows an example of setting **clientCache** to specify a maximum age of 3 days:</span></span>  

```xml
<configuration>
    <system.webServer>
        <staticContent>
            <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00" />
        </staticContent>
    </system.webServer>
</configuration>
```

<span data-ttu-id="9dbd5-119">Specificando **UseMaxAge**, si aggiunge un'intestazione `Cache-Control: max-age=<nnn>` alla risposta in base al valore specificato nell'attributo **CacheControlMaxAge**.</span><span class="sxs-lookup"><span data-stu-id="9dbd5-119">Specifying **UseMaxAge** adds a `Cache-Control: max-age=<nnn>` header to the response based on the value specified in the **CacheControlMaxAge** attribute.</span></span> <span data-ttu-id="9dbd5-120">Il formato dell'intervallo di tempo per l'attributo **cacheControlMaxAge** è <days>.<hours>:<min>:<sec>.</span><span class="sxs-lookup"><span data-stu-id="9dbd5-120">The format of the timespan is for the **cacheControlMaxAge** attribute is <days>.<hours>:<min>:<sec>.</span></span> <span data-ttu-id="9dbd5-121">Per altre informazioni sul nodo **clientCache**, vedere l'argomento relativo alla [cache client <clientCache>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).</span><span class="sxs-lookup"><span data-stu-id="9dbd5-121">For more information on the **clientCache** node, see [Client Cache <clientCache>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).</span></span>  

## <a name="setting-cache-control-headers-in-code"></a><span data-ttu-id="9dbd5-122">Impostazione delle intestazioni Cache-Control nel codice</span><span class="sxs-lookup"><span data-stu-id="9dbd5-122">Setting Cache-Control Headers in Code</span></span>
<span data-ttu-id="9dbd5-123">Per le applicazioni ASP.NET, è possibile impostare a livello di codice il comportamento di memorizzazione nella cache della rete CDN impostando la proprietà **HttpResponse.Cache** .</span><span class="sxs-lookup"><span data-stu-id="9dbd5-123">For ASP.NET applications, you can set the CDN caching behavior programmatically by setting the **HttpResponse.Cache** property.</span></span> <span data-ttu-id="9dbd5-124">Per altre informazioni sulla proprietà **HttpResponse.Cache**, vedere [Proprietà HttpResponse.Cache](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) e [Classe HttpCachePolicy](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span><span class="sxs-lookup"><span data-stu-id="9dbd5-124">For more information on the **HttpResponse.Cache** property, see [HttpResponse.Cache Property](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) and [HttpCachePolicy Class](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span></span>  

<span data-ttu-id="9dbd5-125">Se si vuole memorizzare nella cache il contenuto dell'applicazione a livello di codice in ASP.NET, assicurarsi che tale contenuto sia contrassegnato come inseribile nella cache impostando HttpCacheability su *Public*.</span><span class="sxs-lookup"><span data-stu-id="9dbd5-125">If you want to programmatically cache application content in ASP.NET, make sure that the content is marked as cacheable by setting HttpCacheability to *Public*.</span></span> <span data-ttu-id="9dbd5-126">Assicurarsi anche che sia impostato un validator della cache.</span><span class="sxs-lookup"><span data-stu-id="9dbd5-126">Also, ensure that a cache validator is set.</span></span> <span data-ttu-id="9dbd5-127">Il validator della cache può essere un timestamp dell'ultima modifica impostato chiamando SetLastModified oppure un valore etag impostato chiamando SetETag.</span><span class="sxs-lookup"><span data-stu-id="9dbd5-127">The cache validator can be a Last Modified timestamp set by calling SetLastModified, or an etag value set by calling SetETag.</span></span> <span data-ttu-id="9dbd5-128">Facoltativamente, è anche possibile specificare una scadenza della cache chiamando SetExpires oppure affidarsi all'euristica predefinita della cache descritta prima in questo documento.</span><span class="sxs-lookup"><span data-stu-id="9dbd5-128">Optionally, you can also specify a cache expiration time by calling SetExpires, or you can rely on the default cache heuristics described earlier in this document.</span></span>  

<span data-ttu-id="9dbd5-129">Ad esempio, per memorizzare nella cache il contenuto per un'ora, aggiungere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="9dbd5-129">For example, to cache content for one hour, add the following:</span></span>  

```csharp
// Set the caching parameters.
Response.Cache.SetExpires(DateTime.Now.AddHours(1));
Response.Cache.SetCacheability(HttpCacheability.Public);
Response.Cache.SetLastModified(DateTime.Now);
```

## <a name="next-steps"></a><span data-ttu-id="9dbd5-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9dbd5-130">Next Steps</span></span>
* [<span data-ttu-id="9dbd5-131">Vedere informazioni dettagliate sull'elemento **clientCache**</span><span class="sxs-lookup"><span data-stu-id="9dbd5-131">Read details about the **clientCache** element</span></span>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache)
* [<span data-ttu-id="9dbd5-132">Vedere la documentazione sulla proprietà **HttpResponse.Cache**</span><span class="sxs-lookup"><span data-stu-id="9dbd5-132">Read the documentation for the **HttpResponse.Cache** Property</span></span>](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) 
* <span data-ttu-id="9dbd5-133">[Vedere la documentazione sulla classe **HttpCachePolicy**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx)</span><span class="sxs-lookup"><span data-stu-id="9dbd5-133">[Read the documentation for the **HttpCachePolicy Class**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span></span>  

