---
title: i filtri di aaaCreating con l'API REST di servizi multimediali di Azure | Documenti Microsoft
description: "In questo argomento viene descritto come toocreate filtra il client può utilizzarli toostream sezioni specifiche di un flusso. Servizi multimediali crea manifesti dinamica tooachieve questo flusso selettiva."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: f7d23daf-7cd2-49c7-a195-ab902912ab3c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako;cenkdin
ms.openlocfilehash: d0b5af3b193b35f22ac70887963c2f0a06b60bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-filters-with-azure-media-services-rest-api"></a><span data-ttu-id="8806d-104">Creazione di filtri con l'API REST di Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="8806d-104">Creating Filters with Azure Media Services REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8806d-105">.NET</span><span class="sxs-lookup"><span data-stu-id="8806d-105">.NET</span></span>](media-services-dotnet-dynamic-manifest.md)
> * [<span data-ttu-id="8806d-106">REST</span><span class="sxs-lookup"><span data-stu-id="8806d-106">REST</span></span>](media-services-rest-dynamic-manifest.md)
> 
> 

<span data-ttu-id="8806d-107">A partire dalla versione 2.11, servizi multimediali consente toodefine filtri per le risorse.</span><span class="sxs-lookup"><span data-stu-id="8806d-107">Starting with 2.11 release, Media Services enables you toodefine filters for your assets.</span></span> <span data-ttu-id="8806d-108">Questi filtri sono regole lato server che consentono ai clienti toochoose toodo elementi quali: la riproduzione solo una sezione di un video (anziché la riproduzione di hello video interi), oppure specificare solo un subset di rendering audio e video che (è possono gestire i dispositivi del cliente invece di tutte le copie trasformate hello associati asset hello).</span><span class="sxs-lookup"><span data-stu-id="8806d-108">These filters are server side rules that will allow your customers toochoose toodo things like: playback only a section of a video (instead of playing hello whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all hello renditions that are associated with hello asset).</span></span> <span data-ttu-id="8806d-109">Questo filtro delle risorse di archiviazione tramite **manifesto dinamica**che vengono creati al momento di toostream di richiesta del cliente, un video in base a filtri specificati.</span><span class="sxs-lookup"><span data-stu-id="8806d-109">This filtering of your assets is archived through **Dynamic Manifest**s that are created upon your customer's request toostream a video based on specified filter(s).</span></span>

<span data-ttu-id="8806d-110">Per informazioni più dettagliate toofilters correlati e il manifesto dinamica, vedere [dinamico manifesti Panoramica](media-services-dynamic-manifest-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8806d-110">For more detailed information related toofilters and Dynamic Manifest, see [Dynamic manifests overview](media-services-dynamic-manifest-overview.md).</span></span>

<span data-ttu-id="8806d-111">Questo argomento viene illustrato come toouse toocreate di API REST, aggiornare ed eliminare filtri.</span><span class="sxs-lookup"><span data-stu-id="8806d-111">This topic shows how toouse REST APIs toocreate, update, and delete filters.</span></span> 

## <a name="types-used-toocreate-filters"></a><span data-ttu-id="8806d-112">I tipi utilizzati filtri toocreate</span><span class="sxs-lookup"><span data-stu-id="8806d-112">Types used toocreate filters</span></span>
<span data-ttu-id="8806d-113">Hello vengono utilizzati i seguenti tipi quando si creano filtri:</span><span class="sxs-lookup"><span data-stu-id="8806d-113">hello following types are used when creating filters:</span></span>  

* [<span data-ttu-id="8806d-114">Filter</span><span class="sxs-lookup"><span data-stu-id="8806d-114">Filter</span></span>](https://docs.microsoft.com/rest/api/media/operations/filter)
* [<span data-ttu-id="8806d-115">AssetFilter</span><span class="sxs-lookup"><span data-stu-id="8806d-115">AssetFilter</span></span>](https://docs.microsoft.com/rest/api/media/operations/assetfilter)
* [<span data-ttu-id="8806d-116">PresentationTimeRange</span><span class="sxs-lookup"><span data-stu-id="8806d-116">PresentationTimeRange</span></span>](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)
* [<span data-ttu-id="8806d-117">FilterTrackSelect e FilterTrackPropertyCondition</span><span class="sxs-lookup"><span data-stu-id="8806d-117">FilterTrackSelect and FilterTrackPropertyCondition</span></span>](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)

>[!NOTE]

><span data-ttu-id="8806d-118">Quando si accede alle entità in Servizi multimediali, è necessario impostare valori e campi di intestazione specifici nelle richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="8806d-118">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="8806d-119">Per altre informazioni, vedere [Panoramica dell'API REST di Servizi multimediali](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="8806d-119">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="8806d-120">Connessione dei servizi tooMedia</span><span class="sxs-lookup"><span data-stu-id="8806d-120">Connect tooMedia Services</span></span>

<span data-ttu-id="8806d-121">Per informazioni su come tooconnect toohello AMS API, vedere [hello accesso API di servizi multimediali di Azure con autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="8806d-121">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="8806d-122">Dopo avere stabilito la connessione toohttps://media.windows.net, si riceverà un reindirizzamento 301 specificando un altro URI di servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="8806d-122">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="8806d-123">È necessario effettuare le chiamate successive toohello nuovo URI.</span><span class="sxs-lookup"><span data-stu-id="8806d-123">You must make subsequent calls toohello new URI.</span></span>

## <a name="create-filters"></a><span data-ttu-id="8806d-124">Creare filtri</span><span class="sxs-lookup"><span data-stu-id="8806d-124">Create filters</span></span>
### <a name="create-global-filters"></a><span data-ttu-id="8806d-125">Creare filtri globali</span><span class="sxs-lookup"><span data-stu-id="8806d-125">Create global Filters</span></span>
<span data-ttu-id="8806d-126">toocreate filtro globale, utilizzare hello richieste HTTP seguenti:</span><span class="sxs-lookup"><span data-stu-id="8806d-126">toocreate a global Filter, use hello following HTTP requests:</span></span>  

#### <a name="http-request"></a><span data-ttu-id="8806d-127">Richiesta HTTP</span><span class="sxs-lookup"><span data-stu-id="8806d-127">HTTP Request</span></span>
<span data-ttu-id="8806d-128">Intestazioni richiesta</span><span class="sxs-lookup"><span data-stu-id="8806d-128">Request Headers</span></span>

    POST https://media.windows.net/API/Filters HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host:media.windows.net 

<span data-ttu-id="8806d-129">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="8806d-129">Request body</span></span> 

    {  
       "Name":"GlobalFilter",
       "PresentationTimeRange":{  
          "StartTimestamp":"0",
          "EndTimestamp":"9223372036854775807",
          "PresentationWindowDuration":"12000000000",
          "LiveBackoffDuration":"0",
          "Timescale":"10000000"
       },
       "Tracks":[  
          {  
             "PropertyConditions":
                  [  
                {  
                   "Property":"Type",
                   "Value":"audio",
                   "Operator":"Equal"
                },
                {  
                   "Property":"Bitrate",
                   "Value":"0-2147483647",
                   "Operator":"Equal"
                }
             ]
          }
       ]
    }




#### <a name="http-response"></a><span data-ttu-id="8806d-130">Risposta HTTP</span><span class="sxs-lookup"><span data-stu-id="8806d-130">HTTP Response</span></span>
    HTTP/1.1 201 Created 

### <a name="create-local-assetfilters"></a><span data-ttu-id="8806d-131">Creare AssetFilters locali</span><span class="sxs-lookup"><span data-stu-id="8806d-131">Create local AssetFilters</span></span>
<span data-ttu-id="8806d-132">toocreate un AssetFilter locale, utilizzare hello richieste HTTP seguenti:</span><span class="sxs-lookup"><span data-stu-id="8806d-132">toocreate a local AssetFilter, use hello following HTTP requests:</span></span>  

#### <a name="http-request"></a><span data-ttu-id="8806d-133">Richiesta HTTP</span><span class="sxs-lookup"><span data-stu-id="8806d-133">HTTP Request</span></span>
<span data-ttu-id="8806d-134">Intestazioni richiesta</span><span class="sxs-lookup"><span data-stu-id="8806d-134">Request Headers</span></span>

    POST https://media.windows.net/API/AssetFilters HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net  

<span data-ttu-id="8806d-135">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="8806d-135">Request body</span></span> 

    {   
       "Name":"AssetFilter", 
       "ParentAssetId":"nb:cid:UUID:536e555d-1500-80c3-92dc-f1e4fdc6c592", 
       "PresentationTimeRange":{   
          "StartTimestamp":"0", 
          "EndTimestamp":"9223372036854775807", 
          "PresentationWindowDuration":"12000000000", 
          "LiveBackoffDuration":"0", 
          "Timescale":"10000000" 
       }, 
       "Tracks":[   
          {   
             "PropertyConditions": 
                  [   
                {   
                   "Property":"Type", 
                   "Value":"audio", 
                   "Operator":"Equal" 
                }, 
                {   
                   "Property":"Bitrate", 
                   "Value":"0-2147483647", 
                   "Operator":"Equal" 
                } 
             ] 
          } 
       ] 
    } 

#### <a name="http-response"></a><span data-ttu-id="8806d-136">Risposta HTTP</span><span class="sxs-lookup"><span data-stu-id="8806d-136">HTTP Response</span></span>
    HTTP/1.1 201 Created 
    . . . 

## <a name="list-filters"></a><span data-ttu-id="8806d-137">Elencare i filtri</span><span class="sxs-lookup"><span data-stu-id="8806d-137">List filters</span></span>
### <a name="get-all-global-filters-in-hello-ams-account"></a><span data-ttu-id="8806d-138">Ottenere tutti globali **filtro**s nell'account di sistema AMS hello</span><span class="sxs-lookup"><span data-stu-id="8806d-138">Get all global **Filter**s in hello AMS account</span></span>
<span data-ttu-id="8806d-139">filtri toolist, utilizzare hello richieste HTTP seguenti:</span><span class="sxs-lookup"><span data-stu-id="8806d-139">toolist filters, use hello following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="8806d-140">Richiesta HTTP</span><span class="sxs-lookup"><span data-stu-id="8806d-140">HTTP Request</span></span>
    GET https://media.windows.net/API/Filters HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

### <a name="get-assetfilters-associated-with-an-asset"></a><span data-ttu-id="8806d-141">Ottenere gli **AssetFilter**associati a un asset</span><span class="sxs-lookup"><span data-stu-id="8806d-141">Get **AssetFilter**s associated with an asset</span></span>
#### <a name="http-request"></a><span data-ttu-id="8806d-142">Richiesta HTTP</span><span class="sxs-lookup"><span data-stu-id="8806d-142">HTTP Request</span></span>
    GET https://media.windows.net/API/Assets('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592')/AssetFilters HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 

### <a name="get-an-assetfilter-based-on-its-id"></a><span data-ttu-id="8806d-143">Ottenere un **AssetFilter** in base all'ID</span><span class="sxs-lookup"><span data-stu-id="8806d-143">Get an **AssetFilter** based on its Id</span></span>
#### <a name="http-request"></a><span data-ttu-id="8806d-144">Richiesta HTTP</span><span class="sxs-lookup"><span data-stu-id="8806d-144">HTTP Request</span></span>
    GET https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__TestFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000


## <a name="update-filters"></a><span data-ttu-id="8806d-145">Aggiornare i filtri</span><span class="sxs-lookup"><span data-stu-id="8806d-145">Update filters</span></span>
<span data-ttu-id="8806d-146">Utilizzo di PATCH, PUT o tipo MERGE tooupdate un filtro con nuovi valori della proprietà.</span><span class="sxs-lookup"><span data-stu-id="8806d-146">Use PATCH, PUT or MERGE tooupdate a filter with new property values.</span></span>  <span data-ttu-id="8806d-147">Per altre informazioni su queste operazioni, vedere [PATCH, PUT, MERGE](http://msdn.microsoft.com/library/dd541276.aspx).</span><span class="sxs-lookup"><span data-stu-id="8806d-147">For more information about these operations, see [PATCH, PUT, MERGE](http://msdn.microsoft.com/library/dd541276.aspx).</span></span>

<span data-ttu-id="8806d-148">Se si aggiorna un filtro, può richiedere too2 minuti per le regole di hello toorefresh endpoint di streaming.</span><span class="sxs-lookup"><span data-stu-id="8806d-148">If you update a filter, it can take up too2 minutes for streaming endpoint toorefresh hello rules.</span></span> <span data-ttu-id="8806d-149">Se contenuto hello è disponibile quando si utilizza il filtro e memorizzati nella cache in proxy e della rete CDN memorizza nella cache, l'aggiornamento di questo filtro può causare errori di Windows Media player.</span><span class="sxs-lookup"><span data-stu-id="8806d-149">If hello content was served using this filter (and cached in proxies and CDN caches), updating this filter can result in player failures.</span></span> <span data-ttu-id="8806d-150">È consigliabile cache di hello tooclear dopo l'aggiornamento del filtro hello.</span><span class="sxs-lookup"><span data-stu-id="8806d-150">It is recommend tooclear hello cache after updating hello filter.</span></span> <span data-ttu-id="8806d-151">Se questa operazione non è consentita, prendere in considerazione la possibilità di usare un filtro diverso.</span><span class="sxs-lookup"><span data-stu-id="8806d-151">If this option is not possible, consider using a different filter.</span></span>  

### <a name="update-global-filters"></a><span data-ttu-id="8806d-152">Aggiornare filtri globali</span><span class="sxs-lookup"><span data-stu-id="8806d-152">Update global Filters</span></span>
<span data-ttu-id="8806d-153">tooupdate filtro globale, utilizzare hello richieste HTTP seguenti:</span><span class="sxs-lookup"><span data-stu-id="8806d-153">tooupdate a global filter, use hello following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="8806d-154">Richiesta HTTP</span><span class="sxs-lookup"><span data-stu-id="8806d-154">HTTP Request</span></span>
<span data-ttu-id="8806d-155">Intestazioni della richiesta:</span><span class="sxs-lookup"><span data-stu-id="8806d-155">Request headers:</span></span> 

    MERGE https://media.windows.net/API/Filters('filterName') HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 
    Content-Length: 384

<span data-ttu-id="8806d-156">Corpo della richiesta:</span><span class="sxs-lookup"><span data-stu-id="8806d-156">Request body:</span></span> 

    { 
       "Tracks":[   
          {   
             "PropertyConditions": 
             [   
                {   
                   "Property":"Type", 
                   "Value":"audio", 
                   "Operator":"Equal" 
                }, 
                {   
                   "Property":"Bitrate", 
                   "Value":"0-2147483647", 
                   "Operator":"Equal" 
                } 
             ] 
          } 
       ] 
    } 

### <a name="update-local-assetfilters"></a><span data-ttu-id="8806d-157">Aggiornare AssetFilters locali</span><span class="sxs-lookup"><span data-stu-id="8806d-157">Update local AssetFilters</span></span>
<span data-ttu-id="8806d-158">tooupdate un filtro locale, utilizzare hello richieste HTTP seguenti:</span><span class="sxs-lookup"><span data-stu-id="8806d-158">tooupdate a local filter, use hello following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="8806d-159">Richiesta HTTP</span><span class="sxs-lookup"><span data-stu-id="8806d-159">HTTP Request</span></span>
<span data-ttu-id="8806d-160">Intestazioni della richiesta:</span><span class="sxs-lookup"><span data-stu-id="8806d-160">Request headers:</span></span> 

    MERGE https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__TestFilter')  HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 

<span data-ttu-id="8806d-161">Corpo della richiesta:</span><span class="sxs-lookup"><span data-stu-id="8806d-161">Request body:</span></span> 

    { 
       "Tracks":[   
          {   
             "PropertyConditions": 
             [   
                {   
                   "Property":"Type", 
                   "Value":"audio", 
                   "Operator":"Equal" 
                }, 
                {   
                   "Property":"Bitrate", 
                   "Value":"0-2147483647", 
                   "Operator":"Equal" 
                } 
             ] 
          } 
       ] 
    } 


## <a name="delete-filters"></a><span data-ttu-id="8806d-162">Eliminare filtri</span><span class="sxs-lookup"><span data-stu-id="8806d-162">Delete filters</span></span>
### <a name="delete-global-filters"></a><span data-ttu-id="8806d-163">Eliminare filtri globali</span><span class="sxs-lookup"><span data-stu-id="8806d-163">Delete global Filters</span></span>
<span data-ttu-id="8806d-164">toodelete filtro globale, utilizzare hello richieste HTTP seguenti:</span><span class="sxs-lookup"><span data-stu-id="8806d-164">toodelete a global Filter, use hello following HTTP requests:</span></span>

#### <a name="http-request"></a><span data-ttu-id="8806d-165">Richiesta HTTP</span><span class="sxs-lookup"><span data-stu-id="8806d-165">HTTP Request</span></span>
    DELETE https://media.windows.net/api/Filters('GlobalFilter') HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 


### <a name="delete-local-assetfilters"></a><span data-ttu-id="8806d-166">Eliminare AssetFilter locali</span><span class="sxs-lookup"><span data-stu-id="8806d-166">Delete local AssetFilters</span></span>
<span data-ttu-id="8806d-167">toodelete un AssetFilter locale, utilizzare hello richieste HTTP seguenti:</span><span class="sxs-lookup"><span data-stu-id="8806d-167">toodelete a local AssetFilter, use hello following HTTP requests:</span></span>

#### <a name="http-request"></a><span data-ttu-id="8806d-168">Richiesta HTTP</span><span class="sxs-lookup"><span data-stu-id="8806d-168">HTTP Request</span></span>
    DELETE https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__LocalFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

## <a name="build-streaming-urls-that-use-filters"></a><span data-ttu-id="8806d-169">Creare URL di streaming basati su filtri</span><span class="sxs-lookup"><span data-stu-id="8806d-169">Build streaming URLs that use filters</span></span>
<span data-ttu-id="8806d-170">Per informazioni su come toopublish e offrire le risorse, vedere [tooCustomers recapito contenuto Panoramica](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8806d-170">For information on how toopublish and deliver your assets, see [Delivering Content tooCustomers Overview](media-services-deliver-content-overview.md).</span></span>

<span data-ttu-id="8806d-171">Hello esempi seguenti mostrano come tooadd filtri tooyour gli URL di streaming.</span><span class="sxs-lookup"><span data-stu-id="8806d-171">hello following examples show how tooadd filters tooyour streaming URLs.</span></span>

<span data-ttu-id="8806d-172">**MPEG DASH**</span><span class="sxs-lookup"><span data-stu-id="8806d-172">**MPEG DASH**</span></span> 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

<span data-ttu-id="8806d-173">**Apple HTTP Live Streaming (HLS) V4**</span><span class="sxs-lookup"><span data-stu-id="8806d-173">**Apple HTTP Live Streaming (HLS) V4**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

<span data-ttu-id="8806d-174">**Apple HTTP Live Streaming (HLS) V3**</span><span class="sxs-lookup"><span data-stu-id="8806d-174">**Apple HTTP Live Streaming (HLS) V3**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

<span data-ttu-id="8806d-175">**Smooth Streaming**</span><span class="sxs-lookup"><span data-stu-id="8806d-175">**Smooth Streaming**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)

    
## <a name="media-services-learning-paths"></a><span data-ttu-id="8806d-176">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="8806d-176">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8806d-177">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="8806d-177">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="8806d-178">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="8806d-178">See Also</span></span>
[<span data-ttu-id="8806d-179">Filtri e manifesti dinamici</span><span class="sxs-lookup"><span data-stu-id="8806d-179">Dynamic manifests overview</span></span>](media-services-dynamic-manifest-overview.md)

