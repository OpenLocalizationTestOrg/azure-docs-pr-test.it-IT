---
title: Creazione di filtri con l'API REST di Servizi multimediali di Azure | Microsoft Docs
description: "Questo argomento descrive come creare filtri che il client può usare per trasmettere in streaming sezioni specifiche di un flusso. Servizi multimediali crea manifesti dinamici per consentire questo streaming selettivo."
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
ms.openlocfilehash: 76d2721138668d9f0a908af3fa42840309b068ef
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="creating-filters-with-azure-media-services-rest-api"></a><span data-ttu-id="f8a8e-104">Creazione di filtri con l'API REST di Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="f8a8e-104">Creating Filters with Azure Media Services REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f8a8e-105">.NET</span><span class="sxs-lookup"><span data-stu-id="f8a8e-105">.NET</span></span>](media-services-dotnet-dynamic-manifest.md)
> * [<span data-ttu-id="f8a8e-106">REST</span><span class="sxs-lookup"><span data-stu-id="f8a8e-106">REST</span></span>](media-services-rest-dynamic-manifest.md)
> 
> 

<span data-ttu-id="f8a8e-107">A partire dalla versione 2.11, Servizi multimediali consente di definire filtri per i propri asset.</span><span class="sxs-lookup"><span data-stu-id="f8a8e-107">Starting with 2.11 release, Media Services enables you to define filters for your assets.</span></span> <span data-ttu-id="f8a8e-108">I filtri sono costituiti da regole lato server che consentono ai clienti di eseguire operazioni particolari, come riprodurre solo una sezione di un video (anziché il video intero) oppure specificare solo un sottoinsieme di rendering audio e video, in modo che possa essere gestito dal dispositivo del cliente (anziché tutti i rendering associati all'asset).</span><span class="sxs-lookup"><span data-stu-id="f8a8e-108">These filters are server side rules that will allow your customers to choose to do things like: playback only a section of a video (instead of playing the whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all the renditions that are associated with the asset).</span></span> <span data-ttu-id="f8a8e-109">Il filtro degli asset viene archiviato attraverso **manifesti dinamici**creati su richiesta del cliente per trasmettere un video in streaming in base ai filtri specificati.</span><span class="sxs-lookup"><span data-stu-id="f8a8e-109">This filtering of your assets is archived through **Dynamic Manifest**s that are created upon your customer's request to stream a video based on specified filter(s).</span></span>

<span data-ttu-id="f8a8e-110">Per altre informazioni sui filtri e sul manifesto dinamico, vedere [Filtri e manifesti dinamici](media-services-dynamic-manifest-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f8a8e-110">For more detailed information related to filters and Dynamic Manifest, see [Dynamic manifests overview](media-services-dynamic-manifest-overview.md).</span></span>

<span data-ttu-id="f8a8e-111">Questo argomento illustra come usare le API REST per creare, aggiornare ed eliminare filtri.</span><span class="sxs-lookup"><span data-stu-id="f8a8e-111">This topic shows how to use REST APIs to create, update, and delete filters.</span></span> 

## <a name="types-used-to-create-filters"></a><span data-ttu-id="f8a8e-112">Tipi usati per la creazione dei filtri</span><span class="sxs-lookup"><span data-stu-id="f8a8e-112">Types used to create filters</span></span>
<span data-ttu-id="f8a8e-113">Durante la creazione dei filtri vengono usati i tipi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f8a8e-113">The following types are used when creating filters:</span></span>  

* [<span data-ttu-id="f8a8e-114">Filter</span><span class="sxs-lookup"><span data-stu-id="f8a8e-114">Filter</span></span>](https://docs.microsoft.com/rest/api/media/operations/filter)
* [<span data-ttu-id="f8a8e-115">AssetFilter</span><span class="sxs-lookup"><span data-stu-id="f8a8e-115">AssetFilter</span></span>](https://docs.microsoft.com/rest/api/media/operations/assetfilter)
* [<span data-ttu-id="f8a8e-116">PresentationTimeRange</span><span class="sxs-lookup"><span data-stu-id="f8a8e-116">PresentationTimeRange</span></span>](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)
* [<span data-ttu-id="f8a8e-117">FilterTrackSelect e FilterTrackPropertyCondition</span><span class="sxs-lookup"><span data-stu-id="f8a8e-117">FilterTrackSelect and FilterTrackPropertyCondition</span></span>](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)

>[!NOTE]

><span data-ttu-id="f8a8e-118">Quando si accede alle entità in Servizi multimediali, è necessario impostare valori e campi di intestazione specifici nelle richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="f8a8e-118">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="f8a8e-119">Per altre informazioni, vedere [Panoramica dell'API REST di Servizi multimediali](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="f8a8e-119">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="f8a8e-120">Connettersi a Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="f8a8e-120">Connect to Media Services</span></span>

<span data-ttu-id="f8a8e-121">Per informazioni su come connettersi all'API AMS, vedere [Accedere all'API di Servizi multimediali di Azure con l'autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="f8a8e-121">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="f8a8e-122">Dopo avere stabilito la connessione a https://media.windows.net, si riceverà un reindirizzamento 301 che indica un altro URI di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="f8a8e-122">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="f8a8e-123">Le chiamate successive dovranno essere effettuate al nuovo URI.</span><span class="sxs-lookup"><span data-stu-id="f8a8e-123">You must make subsequent calls to the new URI.</span></span>

## <a name="create-filters"></a><span data-ttu-id="f8a8e-124">Creare filtri</span><span class="sxs-lookup"><span data-stu-id="f8a8e-124">Create filters</span></span>
### <a name="create-global-filters"></a><span data-ttu-id="f8a8e-125">Creare filtri globali</span><span class="sxs-lookup"><span data-stu-id="f8a8e-125">Create global Filters</span></span>
<span data-ttu-id="f8a8e-126">Per creare un filtro globale, usare le richieste HTTP seguenti:</span><span class="sxs-lookup"><span data-stu-id="f8a8e-126">To create a global Filter, use the following HTTP requests:</span></span>  

#### <a name="http-request"></a><span data-ttu-id="f8a8e-127">Richiesta HTTP</span><span class="sxs-lookup"><span data-stu-id="f8a8e-127">HTTP Request</span></span>
<span data-ttu-id="f8a8e-128">Intestazioni richiesta</span><span class="sxs-lookup"><span data-stu-id="f8a8e-128">Request Headers</span></span>

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

<span data-ttu-id="f8a8e-129">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="f8a8e-129">Request body</span></span> 

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




#### <a name="http-response"></a><span data-ttu-id="f8a8e-130">Risposta HTTP</span><span class="sxs-lookup"><span data-stu-id="f8a8e-130">HTTP Response</span></span>
    HTTP/1.1 201 Created 

### <a name="create-local-assetfilters"></a><span data-ttu-id="f8a8e-131">Creare AssetFilters locali</span><span class="sxs-lookup"><span data-stu-id="f8a8e-131">Create local AssetFilters</span></span>
<span data-ttu-id="f8a8e-132">Per creare un AssetFilter locale, usare le richieste HTTP seguenti:</span><span class="sxs-lookup"><span data-stu-id="f8a8e-132">To create a local AssetFilter, use the following HTTP requests:</span></span>  

#### <a name="http-request"></a><span data-ttu-id="f8a8e-133">Richiesta HTTP</span><span class="sxs-lookup"><span data-stu-id="f8a8e-133">HTTP Request</span></span>
<span data-ttu-id="f8a8e-134">Intestazioni richiesta</span><span class="sxs-lookup"><span data-stu-id="f8a8e-134">Request Headers</span></span>

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

<span data-ttu-id="f8a8e-135">Corpo della richiesta</span><span class="sxs-lookup"><span data-stu-id="f8a8e-135">Request body</span></span> 

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

#### <a name="http-response"></a><span data-ttu-id="f8a8e-136">Risposta HTTP</span><span class="sxs-lookup"><span data-stu-id="f8a8e-136">HTTP Response</span></span>
    HTTP/1.1 201 Created 
    . . . 

## <a name="list-filters"></a><span data-ttu-id="f8a8e-137">Elencare i filtri</span><span class="sxs-lookup"><span data-stu-id="f8a8e-137">List filters</span></span>
### <a name="get-all-global-filters-in-the-ams-account"></a><span data-ttu-id="f8a8e-138">Ottenere tutti i **Filter**globali nell'account di Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="f8a8e-138">Get all global **Filter**s in the AMS account</span></span>
<span data-ttu-id="f8a8e-139">Per elencare i filtri, usare le richieste HTTP seguenti:</span><span class="sxs-lookup"><span data-stu-id="f8a8e-139">To list filters, use the following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="f8a8e-140">Richiesta HTTP</span><span class="sxs-lookup"><span data-stu-id="f8a8e-140">HTTP Request</span></span>
    GET https://media.windows.net/API/Filters HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

### <a name="get-assetfilters-associated-with-an-asset"></a><span data-ttu-id="f8a8e-141">Ottenere gli **AssetFilter**associati a un asset</span><span class="sxs-lookup"><span data-stu-id="f8a8e-141">Get **AssetFilter**s associated with an asset</span></span>
#### <a name="http-request"></a><span data-ttu-id="f8a8e-142">Richiesta HTTP</span><span class="sxs-lookup"><span data-stu-id="f8a8e-142">HTTP Request</span></span>
    GET https://media.windows.net/API/Assets('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592')/AssetFilters HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 

### <a name="get-an-assetfilter-based-on-its-id"></a><span data-ttu-id="f8a8e-143">Ottenere un **AssetFilter** in base all'ID</span><span class="sxs-lookup"><span data-stu-id="f8a8e-143">Get an **AssetFilter** based on its Id</span></span>
#### <a name="http-request"></a><span data-ttu-id="f8a8e-144">Richiesta HTTP</span><span class="sxs-lookup"><span data-stu-id="f8a8e-144">HTTP Request</span></span>
    GET https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__TestFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000


## <a name="update-filters"></a><span data-ttu-id="f8a8e-145">Aggiornare i filtri</span><span class="sxs-lookup"><span data-stu-id="f8a8e-145">Update filters</span></span>
<span data-ttu-id="f8a8e-146">Usare PATCH, PUT o MERGE per aggiornare un filtro con i nuovi valori di proprietà.</span><span class="sxs-lookup"><span data-stu-id="f8a8e-146">Use PATCH, PUT or MERGE to update a filter with new property values.</span></span>  <span data-ttu-id="f8a8e-147">Per altre informazioni su queste operazioni, vedere [PATCH, PUT, MERGE](http://msdn.microsoft.com/library/dd541276.aspx).</span><span class="sxs-lookup"><span data-stu-id="f8a8e-147">For more information about these operations, see [PATCH, PUT, MERGE](http://msdn.microsoft.com/library/dd541276.aspx).</span></span>

<span data-ttu-id="f8a8e-148">Se si aggiorna un filtro, l'endpoint di streaming può impiegare fino a due minuti per aggiornare le regole.</span><span class="sxs-lookup"><span data-stu-id="f8a8e-148">If you update a filter, it can take up to 2 minutes for streaming endpoint to refresh the rules.</span></span> <span data-ttu-id="f8a8e-149">Se il contenuto è stato trasmesso usando dei filtri (e memorizzato nelle cache dei proxy e delle reti CDN), l'aggiornamento del filtro può determinare un errore del lettore.</span><span class="sxs-lookup"><span data-stu-id="f8a8e-149">If the content was served using this filter (and cached in proxies and CDN caches), updating this filter can result in player failures.</span></span> <span data-ttu-id="f8a8e-150">È consigliabile quindi cancellare la cache dopo aver aggiornato il filtro.</span><span class="sxs-lookup"><span data-stu-id="f8a8e-150">It is recommend to clear the cache after updating the filter.</span></span> <span data-ttu-id="f8a8e-151">Se questa operazione non è consentita, prendere in considerazione la possibilità di usare un filtro diverso.</span><span class="sxs-lookup"><span data-stu-id="f8a8e-151">If this option is not possible, consider using a different filter.</span></span>  

### <a name="update-global-filters"></a><span data-ttu-id="f8a8e-152">Aggiornare filtri globali</span><span class="sxs-lookup"><span data-stu-id="f8a8e-152">Update global Filters</span></span>
<span data-ttu-id="f8a8e-153">Per aggiornare un filtro globale, usare le richieste HTTP seguenti:</span><span class="sxs-lookup"><span data-stu-id="f8a8e-153">To update a global filter, use the following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="f8a8e-154">Richiesta HTTP</span><span class="sxs-lookup"><span data-stu-id="f8a8e-154">HTTP Request</span></span>
<span data-ttu-id="f8a8e-155">Intestazioni della richiesta:</span><span class="sxs-lookup"><span data-stu-id="f8a8e-155">Request headers:</span></span> 

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

<span data-ttu-id="f8a8e-156">Corpo della richiesta:</span><span class="sxs-lookup"><span data-stu-id="f8a8e-156">Request body:</span></span> 

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

### <a name="update-local-assetfilters"></a><span data-ttu-id="f8a8e-157">Aggiornare AssetFilters locali</span><span class="sxs-lookup"><span data-stu-id="f8a8e-157">Update local AssetFilters</span></span>
<span data-ttu-id="f8a8e-158">Per aggiornare un filtro locale, usare le richieste HTTP seguenti:</span><span class="sxs-lookup"><span data-stu-id="f8a8e-158">To update a local filter, use the following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="f8a8e-159">Richiesta HTTP</span><span class="sxs-lookup"><span data-stu-id="f8a8e-159">HTTP Request</span></span>
<span data-ttu-id="f8a8e-160">Intestazioni della richiesta:</span><span class="sxs-lookup"><span data-stu-id="f8a8e-160">Request headers:</span></span> 

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

<span data-ttu-id="f8a8e-161">Corpo della richiesta:</span><span class="sxs-lookup"><span data-stu-id="f8a8e-161">Request body:</span></span> 

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


## <a name="delete-filters"></a><span data-ttu-id="f8a8e-162">Eliminare filtri</span><span class="sxs-lookup"><span data-stu-id="f8a8e-162">Delete filters</span></span>
### <a name="delete-global-filters"></a><span data-ttu-id="f8a8e-163">Eliminare filtri globali</span><span class="sxs-lookup"><span data-stu-id="f8a8e-163">Delete global Filters</span></span>
<span data-ttu-id="f8a8e-164">Per eliminare un filtro globale, usare le richieste HTTP seguenti:</span><span class="sxs-lookup"><span data-stu-id="f8a8e-164">To delete a global Filter, use the following HTTP requests:</span></span>

#### <a name="http-request"></a><span data-ttu-id="f8a8e-165">Richiesta HTTP</span><span class="sxs-lookup"><span data-stu-id="f8a8e-165">HTTP Request</span></span>
    DELETE https://media.windows.net/api/Filters('GlobalFilter') HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 


### <a name="delete-local-assetfilters"></a><span data-ttu-id="f8a8e-166">Eliminare AssetFilter locali</span><span class="sxs-lookup"><span data-stu-id="f8a8e-166">Delete local AssetFilters</span></span>
<span data-ttu-id="f8a8e-167">Per eliminare un AssetFilter locale, usare le richieste HTTP seguenti:</span><span class="sxs-lookup"><span data-stu-id="f8a8e-167">To delete a local AssetFilter, use the following HTTP requests:</span></span>

#### <a name="http-request"></a><span data-ttu-id="f8a8e-168">Richiesta HTTP</span><span class="sxs-lookup"><span data-stu-id="f8a8e-168">HTTP Request</span></span>
    DELETE https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__LocalFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

## <a name="build-streaming-urls-that-use-filters"></a><span data-ttu-id="f8a8e-169">Creare URL di streaming basati su filtri</span><span class="sxs-lookup"><span data-stu-id="f8a8e-169">Build streaming URLs that use filters</span></span>
<span data-ttu-id="f8a8e-170">Per informazioni su come pubblicare e distribuire asset, vedere [Informazioni generali sulla distribuzione di contenuti ai clienti](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f8a8e-170">For information on how to publish and deliver your assets, see [Delivering Content to Customers Overview](media-services-deliver-content-overview.md).</span></span>

<span data-ttu-id="f8a8e-171">Gli esempi seguenti illustrano come aggiungere filtri agli URL di streaming.</span><span class="sxs-lookup"><span data-stu-id="f8a8e-171">The following examples show how to add filters to your streaming URLs.</span></span>

<span data-ttu-id="f8a8e-172">**MPEG DASH**</span><span class="sxs-lookup"><span data-stu-id="f8a8e-172">**MPEG DASH**</span></span> 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

<span data-ttu-id="f8a8e-173">**Apple HTTP Live Streaming (HLS) V4**</span><span class="sxs-lookup"><span data-stu-id="f8a8e-173">**Apple HTTP Live Streaming (HLS) V4**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

<span data-ttu-id="f8a8e-174">**Apple HTTP Live Streaming (HLS) V3**</span><span class="sxs-lookup"><span data-stu-id="f8a8e-174">**Apple HTTP Live Streaming (HLS) V3**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

<span data-ttu-id="f8a8e-175">**Smooth Streaming**</span><span class="sxs-lookup"><span data-stu-id="f8a8e-175">**Smooth Streaming**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)

    
## <a name="media-services-learning-paths"></a><span data-ttu-id="f8a8e-176">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="f8a8e-176">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f8a8e-177">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="f8a8e-177">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="f8a8e-178">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f8a8e-178">See Also</span></span>
[<span data-ttu-id="f8a8e-179">Filtri e manifesti dinamici</span><span class="sxs-lookup"><span data-stu-id="f8a8e-179">Dynamic manifests overview</span></span>](media-services-dynamic-manifest-overview.md)

