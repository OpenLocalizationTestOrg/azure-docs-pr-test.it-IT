---
title: Filtri aaaCreating con Azure Media Services .NET SDK
description: "In questo argomento viene descritto come toocreate filtra il client può utilizzarli toostream sezioni specifiche di un flusso. Servizi multimediali crea manifesti dinamica tooachieve questo flusso selettiva."
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
ms.openlocfilehash: 16d9497d48ab1d3f841dd97efb0f66016a2435c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-filters-with-azure-media-services-net-sdk"></a><span data-ttu-id="4d4a5-104">Creazione di filtri con il .NET SDK di Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="4d4a5-104">Creating Filters with Azure Media Services .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4d4a5-105">.NET</span><span class="sxs-lookup"><span data-stu-id="4d4a5-105">.NET</span></span>](media-services-dotnet-dynamic-manifest.md)
> * [<span data-ttu-id="4d4a5-106">REST</span><span class="sxs-lookup"><span data-stu-id="4d4a5-106">REST</span></span>](media-services-rest-dynamic-manifest.md)
> 
> 

<span data-ttu-id="4d4a5-107">A partire dalla versione 2.11, servizi multimediali consente toodefine filtri per le risorse.</span><span class="sxs-lookup"><span data-stu-id="4d4a5-107">Starting with 2.11 release, Media Services enables you toodefine filters for your assets.</span></span> <span data-ttu-id="4d4a5-108">Questi filtri sono regole lato server che consentono ai clienti toochoose toodo elementi quali: la riproduzione solo una sezione di un video (anziché la riproduzione di hello video interi), oppure specificare solo un subset di rendering audio e video che (è possono gestire i dispositivi del cliente invece di tutte le copie trasformate hello associati asset hello).</span><span class="sxs-lookup"><span data-stu-id="4d4a5-108">These filters are server side rules that will allow your customers toochoose toodo things like: playback only a section of a video (instead of playing hello whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all hello renditions that are associated with hello asset).</span></span> <span data-ttu-id="4d4a5-109">Questo filtro delle risorse viene ottenuto tramite **manifesto dinamica**che vengono creati al momento di toostream di richiesta del cliente, un video in base a filtri specificati.</span><span class="sxs-lookup"><span data-stu-id="4d4a5-109">This filtering of your assets is achieved through **Dynamic Manifest**s that are created upon your customer's request toostream a video based on specified filter(s).</span></span>

<span data-ttu-id="4d4a5-110">Per informazioni più dettagliate toofilters correlati e il manifesto dinamica, vedere [dinamico manifesti Panoramica](media-services-dynamic-manifest-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4d4a5-110">For more detailed information related toofilters and Dynamic Manifest, see [Dynamic manifests overview](media-services-dynamic-manifest-overview.md).</span></span>

<span data-ttu-id="4d4a5-111">Questo argomento viene illustrato come toouse Media Services .NET SDK toocreate, aggiornare ed eliminare filtri.</span><span class="sxs-lookup"><span data-stu-id="4d4a5-111">This topic shows how toouse Media Services .NET SDK toocreate, update, and delete filters.</span></span> 

<span data-ttu-id="4d4a5-112">Nota: se si aggiorna un filtro, è possibile richiedere too2 minuti per le regole di hello toorefresh endpoint di streaming.</span><span class="sxs-lookup"><span data-stu-id="4d4a5-112">Note if you update a filter, it can take up too2 minutes for streaming endpoint toorefresh hello rules.</span></span> <span data-ttu-id="4d4a5-113">Se contenuto hello è disponibile quando si utilizza il filtro e memorizzati nella cache in proxy e della rete CDN memorizza nella cache, l'aggiornamento di questo filtro può causare errori di Windows Media player.</span><span class="sxs-lookup"><span data-stu-id="4d4a5-113">If hello content was served using this filter (and cached in proxies and CDN caches), updating this filter can result in player failures.</span></span> <span data-ttu-id="4d4a5-114">È consigliabile cache di hello tooclear dopo l'aggiornamento del filtro hello.</span><span class="sxs-lookup"><span data-stu-id="4d4a5-114">It is recommend tooclear hello cache after updating hello filter.</span></span> <span data-ttu-id="4d4a5-115">Se questa operazione non è consentita, prendere in considerazione la possibilità di usare un filtro diverso.</span><span class="sxs-lookup"><span data-stu-id="4d4a5-115">If this option is not possible, consider using a different filter.</span></span> 

## <a name="types-used-toocreate-filters"></a><span data-ttu-id="4d4a5-116">I tipi utilizzati filtri toocreate</span><span class="sxs-lookup"><span data-stu-id="4d4a5-116">Types used toocreate filters</span></span>
<span data-ttu-id="4d4a5-117">Hello vengono utilizzati i seguenti tipi quando si creano filtri:</span><span class="sxs-lookup"><span data-stu-id="4d4a5-117">hello following types are used when creating filters:</span></span> 

* <span data-ttu-id="4d4a5-118">**IStreamingFilter**.</span><span class="sxs-lookup"><span data-stu-id="4d4a5-118">**IStreamingFilter**.</span></span>  <span data-ttu-id="4d4a5-119">Questo tipo è basato sull'hello seguenti API REST [filtro](https://docs.microsoft.com/rest/api/media/operations/filter)</span><span class="sxs-lookup"><span data-stu-id="4d4a5-119">This type is based on hello following REST API [Filter](https://docs.microsoft.com/rest/api/media/operations/filter)</span></span>
* <span data-ttu-id="4d4a5-120">**IStreamingAssetFilter**.</span><span class="sxs-lookup"><span data-stu-id="4d4a5-120">**IStreamingAssetFilter**.</span></span> <span data-ttu-id="4d4a5-121">Questo tipo è basato sull'hello seguenti API REST [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)</span><span class="sxs-lookup"><span data-stu-id="4d4a5-121">This type is based on hello following REST API [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)</span></span>
* <span data-ttu-id="4d4a5-122">**PresentationTimeRange**.</span><span class="sxs-lookup"><span data-stu-id="4d4a5-122">**PresentationTimeRange**.</span></span> <span data-ttu-id="4d4a5-123">Questo tipo è basato sull'hello seguenti API REST [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)</span><span class="sxs-lookup"><span data-stu-id="4d4a5-123">This type is based on hello following REST API [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)</span></span>
* <span data-ttu-id="4d4a5-124">**FilterTrackSelectStatement** e **IFilterTrackPropertyCondition**.</span><span class="sxs-lookup"><span data-stu-id="4d4a5-124">**FilterTrackSelectStatement** and **IFilterTrackPropertyCondition**.</span></span> <span data-ttu-id="4d4a5-125">Questi tipi sono basati sulle seguenti API REST hello [FilterTrackSelect e FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)</span><span class="sxs-lookup"><span data-stu-id="4d4a5-125">These types are based on hello following REST APIs [FilterTrackSelect and FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)</span></span>

## <a name="createupdatereaddelete-global-filters"></a><span data-ttu-id="4d4a5-126">Creare/aggiornare/leggere/eliminare filtri globali</span><span class="sxs-lookup"><span data-stu-id="4d4a5-126">Create/Update/Read/Delete global filters</span></span>
<span data-ttu-id="4d4a5-127">Hello codice seguente viene illustrato come toouse .NET toocreate, aggiornare, leggere ed eliminare filtri di asset.</span><span class="sxs-lookup"><span data-stu-id="4d4a5-127">hello following code shows how toouse .NET toocreate, update,read, and delete asset filters.</span></span>

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


## <a name="createupdatereaddelete-asset-filters"></a><span data-ttu-id="4d4a5-128">Creare/aggiornare/leggere/eliminare filtri di asset</span><span class="sxs-lookup"><span data-stu-id="4d4a5-128">Create/Update/Read/Delete asset filters</span></span>
<span data-ttu-id="4d4a5-129">Hello codice seguente viene illustrato come toouse .NET toocreate, aggiornare, leggere ed eliminare filtri di asset.</span><span class="sxs-lookup"><span data-stu-id="4d4a5-129">hello following code shows how toouse .NET toocreate, update,read, and delete asset filters.</span></span>

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




## <a name="build-streaming-urls-that-use-filters"></a><span data-ttu-id="4d4a5-130">Creare URL di streaming basati su filtri</span><span class="sxs-lookup"><span data-stu-id="4d4a5-130">Build streaming URLs that use filters</span></span>
<span data-ttu-id="4d4a5-131">Per informazioni su come toopublish e offrire le risorse, vedere [tooCustomers recapito contenuto Panoramica](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4d4a5-131">For information on how toopublish and deliver your assets, see [Delivering Content tooCustomers Overview](media-services-deliver-content-overview.md).</span></span>

<span data-ttu-id="4d4a5-132">Hello esempi seguenti mostrano come tooadd filtri tooyour gli URL di streaming.</span><span class="sxs-lookup"><span data-stu-id="4d4a5-132">hello following examples show how tooadd filters tooyour streaming URLs.</span></span>

<span data-ttu-id="4d4a5-133">**MPEG DASH**</span><span class="sxs-lookup"><span data-stu-id="4d4a5-133">**MPEG DASH**</span></span> 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

<span data-ttu-id="4d4a5-134">**Apple HTTP Live Streaming (HLS) V4**</span><span class="sxs-lookup"><span data-stu-id="4d4a5-134">**Apple HTTP Live Streaming (HLS) V4**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

<span data-ttu-id="4d4a5-135">**Apple HTTP Live Streaming (HLS) V3**</span><span class="sxs-lookup"><span data-stu-id="4d4a5-135">**Apple HTTP Live Streaming (HLS) V3**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

<span data-ttu-id="4d4a5-136">**Smooth Streaming**</span><span class="sxs-lookup"><span data-stu-id="4d4a5-136">**Smooth Streaming**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)


## <a name="media-services-learning-paths"></a><span data-ttu-id="4d4a5-137">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="4d4a5-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4d4a5-138">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="4d4a5-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="4d4a5-139">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="4d4a5-139">See Also</span></span>
[<span data-ttu-id="4d4a5-140">Filtri e manifesti dinamici</span><span class="sxs-lookup"><span data-stu-id="4d4a5-140">Dynamic manifests overview</span></span>](media-services-dynamic-manifest-overview.md)

