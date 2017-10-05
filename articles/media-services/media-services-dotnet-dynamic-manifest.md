---
title: Creazione di filtri con il .NET SDK di Servizi multimediali di Azure
description: "Questo argomento descrive come creare filtri che il client può usare per trasmettere in streaming sezioni specifiche di un flusso. Servizi multimediali crea manifesti dinamici per consentire questo streaming selettivo."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 2f6894ca-fb43-43c0-9151-ddbb2833cafd
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 07/21/2017
ms.author: juliako;cenkdin
ms.openlocfilehash: 6c43473b86c14679ace558de478bd95f41d476da
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="creating-filters-with-azure-media-services-net-sdk"></a><span data-ttu-id="9a077-104">Creazione di filtri con il .NET SDK di Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="9a077-104">Creating Filters with Azure Media Services .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9a077-105">.NET</span><span class="sxs-lookup"><span data-stu-id="9a077-105">.NET</span></span>](media-services-dotnet-dynamic-manifest.md)
> * [<span data-ttu-id="9a077-106">REST</span><span class="sxs-lookup"><span data-stu-id="9a077-106">REST</span></span>](media-services-rest-dynamic-manifest.md)
> 
> 

<span data-ttu-id="9a077-107">A partire dalla versione 2.11, Servizi multimediali consente di definire filtri per i propri asset.</span><span class="sxs-lookup"><span data-stu-id="9a077-107">Starting with 2.11 release, Media Services enables you to define filters for your assets.</span></span> <span data-ttu-id="9a077-108">I filtri sono costituiti da regole lato server che consentono ai clienti di eseguire operazioni particolari, come riprodurre solo una sezione di un video (anziché il video intero) oppure specificare solo un sottoinsieme di rendering audio e video, in modo che possa essere gestito dal dispositivo del cliente (anziché tutti i rendering associati all'asset).</span><span class="sxs-lookup"><span data-stu-id="9a077-108">These filters are server side rules that will allow your customers to choose to do things like: playback only a section of a video (instead of playing the whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all the renditions that are associated with the asset).</span></span> <span data-ttu-id="9a077-109">Il filtro degli asset viene eseguito attraverso **manifesti dinamici**creati su richiesta del cliente per trasmettere un video in streaming in base ai filtri specificati.</span><span class="sxs-lookup"><span data-stu-id="9a077-109">This filtering of your assets is achieved through **Dynamic Manifest**s that are created upon your customer's request to stream a video based on specified filter(s).</span></span>

<span data-ttu-id="9a077-110">Per altre informazioni sui filtri e sul manifesto dinamico, vedere [Filtri e manifesti dinamici](media-services-dynamic-manifest-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9a077-110">For more detailed information related to filters and Dynamic Manifest, see [Dynamic manifests overview](media-services-dynamic-manifest-overview.md).</span></span>

<span data-ttu-id="9a077-111">Questo argomento illustra come usare l’SDK .NET Servizi multimediali per creare, aggiornare ed eliminare filtri.</span><span class="sxs-lookup"><span data-stu-id="9a077-111">This topic shows how to use Media Services .NET SDK to create, update, and delete filters.</span></span> 

<span data-ttu-id="9a077-112">Si noti che si aggiorna un filtro, l'endpoint di streaming può impiegare fino a due minuti per aggiornare le regole.</span><span class="sxs-lookup"><span data-stu-id="9a077-112">Note if you update a filter, it can take up to 2 minutes for streaming endpoint to refresh the rules.</span></span> <span data-ttu-id="9a077-113">Se il contenuto è stato trasmesso usando dei filtri (e memorizzato nelle cache dei proxy e delle reti CDN), l'aggiornamento del filtro può determinare un errore del lettore.</span><span class="sxs-lookup"><span data-stu-id="9a077-113">If the content was served using this filter (and cached in proxies and CDN caches), updating this filter can result in player failures.</span></span> <span data-ttu-id="9a077-114">È consigliabile quindi cancellare la cache dopo aver aggiornato il filtro.</span><span class="sxs-lookup"><span data-stu-id="9a077-114">It is recommend to clear the cache after updating the filter.</span></span> <span data-ttu-id="9a077-115">Se questa operazione non è consentita, prendere in considerazione la possibilità di usare un filtro diverso.</span><span class="sxs-lookup"><span data-stu-id="9a077-115">If this option is not possible, consider using a different filter.</span></span> 

## <a name="types-used-to-create-filters"></a><span data-ttu-id="9a077-116">Tipi usati per la creazione dei filtri</span><span class="sxs-lookup"><span data-stu-id="9a077-116">Types used to create filters</span></span>
<span data-ttu-id="9a077-117">Durante la creazione dei filtri vengono usati i tipi seguenti:</span><span class="sxs-lookup"><span data-stu-id="9a077-117">The following types are used when creating filters:</span></span> 

* <span data-ttu-id="9a077-118">**IStreamingFilter**.</span><span class="sxs-lookup"><span data-stu-id="9a077-118">**IStreamingFilter**.</span></span>  <span data-ttu-id="9a077-119">Questo tipo è basato sulla seguente API REST [Filter](https://docs.microsoft.com/rest/api/media/operations/filter)</span><span class="sxs-lookup"><span data-stu-id="9a077-119">This type is based on the following REST API [Filter](https://docs.microsoft.com/rest/api/media/operations/filter)</span></span>
* <span data-ttu-id="9a077-120">**IStreamingAssetFilter**.</span><span class="sxs-lookup"><span data-stu-id="9a077-120">**IStreamingAssetFilter**.</span></span> <span data-ttu-id="9a077-121">Questo tipo è basato sulla seguente API REST [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)</span><span class="sxs-lookup"><span data-stu-id="9a077-121">This type is based on the following REST API [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)</span></span>
* <span data-ttu-id="9a077-122">**PresentationTimeRange**.</span><span class="sxs-lookup"><span data-stu-id="9a077-122">**PresentationTimeRange**.</span></span> <span data-ttu-id="9a077-123">Questo tipo è basato sulla seguente API REST [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)</span><span class="sxs-lookup"><span data-stu-id="9a077-123">This type is based on the following REST API [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)</span></span>
* <span data-ttu-id="9a077-124">**FilterTrackSelectStatement** e **IFilterTrackPropertyCondition**.</span><span class="sxs-lookup"><span data-stu-id="9a077-124">**FilterTrackSelectStatement** and **IFilterTrackPropertyCondition**.</span></span> <span data-ttu-id="9a077-125">Questi tipi sono basati sulle seguenti API REST [FilterTrackSelect e FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)</span><span class="sxs-lookup"><span data-stu-id="9a077-125">These types are based on the following REST APIs [FilterTrackSelect and FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)</span></span>

## <a name="createupdatereaddelete-global-filters"></a><span data-ttu-id="9a077-126">Creare/aggiornare/leggere/eliminare filtri globali</span><span class="sxs-lookup"><span data-stu-id="9a077-126">Create/Update/Read/Delete global filters</span></span>
<span data-ttu-id="9a077-127">Il seguente codice illustra come utilizzare .NET per creare, aggiornare, leggere ed eliminare filtri di asset.</span><span class="sxs-lookup"><span data-stu-id="9a077-127">The following code shows how to use .NET to create, update,read, and delete asset filters.</span></span>

    string filterName = "GlobalFilter_" + Guid.NewGuid().ToString();

    List<FilterTrackSelectStatement> filterTrackSelectStatements = new List<FilterTrackSelectStatement>();

    FilterTrackSelectStatement filterTrackSelectStatement = new FilterTrackSelectStatement();
    filterTrackSelectStatement.PropertyConditions = new List<IFilterTrackPropertyCondition>();
    filterTrackSelectStatement.PropertyConditions.Add(new FilterTrackNameCondition("Track Name", FilterTrackCompareOperator.NotEqual));
    filterTrackSelectStatement.PropertyConditions.Add(new FilterTrackBitrateRangeCondition(new FilterTrackBitrateRange(0, 1), FilterTrackCompareOperator.NotEqual));
    filterTrackSelectStatement.PropertyConditions.Add(new FilterTrackTypeCondition(FilterTrackType.Audio, FilterTrackCompareOperator.NotEqual));
    filterTrackSelectStatements.Add(filterTrackSelectStatement);

    // Create
    IStreamingFilter filter = _context.Filters.Create(filterName, new PresentationTimeRange(), filterTrackSelectStatements);

    // Update
    filter.PresentationTimeRange = new PresentationTimeRange(timescale: 500);
    filter.Update();

    // Read
    var filterUpdated = _context.Filters.FirstOrDefault();
    Console.WriteLine(filterUpdated.Name);

    // Delete
    filter.Delete();


## <a name="createupdatereaddelete-asset-filters"></a><span data-ttu-id="9a077-128">Creare/aggiornare/leggere/eliminare filtri di asset</span><span class="sxs-lookup"><span data-stu-id="9a077-128">Create/Update/Read/Delete asset filters</span></span>
<span data-ttu-id="9a077-129">Il seguente codice illustra come utilizzare .NET per creare, aggiornare, leggere ed eliminare filtri di asset.</span><span class="sxs-lookup"><span data-stu-id="9a077-129">The following code shows how to use .NET to create, update,read, and delete asset filters.</span></span>

    string assetName = "AssetFilter_" + Guid.NewGuid().ToString();
    var asset = _context.Assets.Create(assetName, AssetCreationOptions.None);

    string filterName = "AssetFilter_" + Guid.NewGuid().ToString();


    // Create
    IStreamingAssetFilter filter = asset.AssetFilters.Create(filterName,
                                        new PresentationTimeRange(), 
                                        new List<FilterTrackSelectStatement>());

    // Update
    filter.PresentationTimeRange = 
            new PresentationTimeRange(start: 6000000000, end: 72000000000);

    filter.Update();

    // Read
    asset = _context.Assets.Where(c => c.Id == asset.Id).FirstOrDefault();
    var filterUpdated = asset.AssetFilters.FirstOrDefault();
    Console.WriteLine(filterUpdated.Name);

    // Delete
    filterUpdated.Delete();




## <a name="build-streaming-urls-that-use-filters"></a><span data-ttu-id="9a077-130">Creare URL di streaming basati su filtri</span><span class="sxs-lookup"><span data-stu-id="9a077-130">Build streaming URLs that use filters</span></span>
<span data-ttu-id="9a077-131">Per informazioni su come pubblicare e distribuire asset, vedere [Informazioni generali sulla distribuzione di contenuti ai clienti](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9a077-131">For information on how to publish and deliver your assets, see [Delivering Content to Customers Overview](media-services-deliver-content-overview.md).</span></span>

<span data-ttu-id="9a077-132">Gli esempi seguenti illustrano come aggiungere filtri agli URL di streaming.</span><span class="sxs-lookup"><span data-stu-id="9a077-132">The following examples show how to add filters to your streaming URLs.</span></span>

<span data-ttu-id="9a077-133">**MPEG DASH**</span><span class="sxs-lookup"><span data-stu-id="9a077-133">**MPEG DASH**</span></span> 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

<span data-ttu-id="9a077-134">**Apple HTTP Live Streaming (HLS) V4**</span><span class="sxs-lookup"><span data-stu-id="9a077-134">**Apple HTTP Live Streaming (HLS) V4**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

<span data-ttu-id="9a077-135">**Apple HTTP Live Streaming (HLS) V3**</span><span class="sxs-lookup"><span data-stu-id="9a077-135">**Apple HTTP Live Streaming (HLS) V3**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

<span data-ttu-id="9a077-136">**Smooth Streaming**</span><span class="sxs-lookup"><span data-stu-id="9a077-136">**Smooth Streaming**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)


## <a name="media-services-learning-paths"></a><span data-ttu-id="9a077-137">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="9a077-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9a077-138">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="9a077-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="9a077-139">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9a077-139">See Also</span></span>
[<span data-ttu-id="9a077-140">Filtri e manifesti dinamici</span><span class="sxs-lookup"><span data-stu-id="9a077-140">Dynamic manifests overview</span></span>](media-services-dynamic-manifest-overview.md)

