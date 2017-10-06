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
# <a name="creating-filters-with-azure-media-services-net-sdk"></a>Creazione di filtri con il .NET SDK di Servizi multimediali di Azure
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-dynamic-manifest.md)
> * [REST](media-services-rest-dynamic-manifest.md)
> 
> 

A partire dalla versione 2.11, servizi multimediali consente toodefine filtri per le risorse. Questi filtri sono regole lato server che consentono ai clienti toochoose toodo elementi quali: la riproduzione solo una sezione di un video (anziché la riproduzione di hello video interi), oppure specificare solo un subset di rendering audio e video che (è possono gestire i dispositivi del cliente invece di tutte le copie trasformate hello associati asset hello). Questo filtro delle risorse viene ottenuto tramite **manifesto dinamica**che vengono creati al momento di toostream di richiesta del cliente, un video in base a filtri specificati.

Per informazioni più dettagliate toofilters correlati e il manifesto dinamica, vedere [dinamico manifesti Panoramica](media-services-dynamic-manifest-overview.md).

Questo argomento viene illustrato come toouse Media Services .NET SDK toocreate, aggiornare ed eliminare filtri. 

Nota: se si aggiorna un filtro, è possibile richiedere too2 minuti per le regole di hello toorefresh endpoint di streaming. Se contenuto hello è disponibile quando si utilizza il filtro e memorizzati nella cache in proxy e della rete CDN memorizza nella cache, l'aggiornamento di questo filtro può causare errori di Windows Media player. È consigliabile cache di hello tooclear dopo l'aggiornamento del filtro hello. Se questa operazione non è consentita, prendere in considerazione la possibilità di usare un filtro diverso. 

## <a name="types-used-toocreate-filters"></a>I tipi utilizzati filtri toocreate
Hello vengono utilizzati i seguenti tipi quando si creano filtri: 

* **IStreamingFilter**.  Questo tipo è basato sull'hello seguenti API REST [filtro](https://docs.microsoft.com/rest/api/media/operations/filter)
* **IStreamingAssetFilter**. Questo tipo è basato sull'hello seguenti API REST [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)
* **PresentationTimeRange**. Questo tipo è basato sull'hello seguenti API REST [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)
* **FilterTrackSelectStatement** e **IFilterTrackPropertyCondition**. Questi tipi sono basati sulle seguenti API REST hello [FilterTrackSelect e FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)

## <a name="createupdatereaddelete-global-filters"></a>Creare/aggiornare/leggere/eliminare filtri globali
Hello codice seguente viene illustrato come toouse .NET toocreate, aggiornare, leggere ed eliminare filtri di asset.

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


## <a name="createupdatereaddelete-asset-filters"></a>Creare/aggiornare/leggere/eliminare filtri di asset
Hello codice seguente viene illustrato come toouse .NET toocreate, aggiornare, leggere ed eliminare filtri di asset.

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




## <a name="build-streaming-urls-that-use-filters"></a>Creare URL di streaming basati su filtri
Per informazioni su come toopublish e offrire le risorse, vedere [tooCustomers recapito contenuto Panoramica](media-services-deliver-content-overview.md).

Hello esempi seguenti mostrano come tooadd filtri tooyour gli URL di streaming.

**MPEG DASH** 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

**Apple HTTP Live Streaming (HLS) V4**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

**Apple HTTP Live Streaming (HLS) V3**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

**Smooth Streaming**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)


## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Vedere anche
[Filtri e manifesti dinamici](media-services-dynamic-manifest-overview.md)

