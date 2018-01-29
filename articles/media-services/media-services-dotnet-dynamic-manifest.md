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
ms.date: 12/07/2017
ms.author: juliako;cenkdin
ms.openlocfilehash: 8ffd310573d0800593bd9d93d74da4bcece61fa4
ms.sourcegitcommit: 821b6306aab244d2feacbd722f60d99881e9d2a4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/18/2017
---
# <a name="creating-filters-with-azure-media-services-net-sdk"></a>Creazione di filtri con il .NET SDK di Servizi multimediali di Azure
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-dynamic-manifest.md)
> * [REST](media-services-rest-dynamic-manifest.md)
> 
> 

A partire dalla versione 2.17, servizi multimediali consente di definire i filtri per le risorse. Questi filtri sono regole lato server che consentono ai clienti di scegliere di eseguire operazioni come: la riproduzione solo una sezione di un video (anziché la riproduzione del video intero), oppure specificare solo un subset di audio e video trasformate in grado di gestire i dispositivi del cliente (invece di tutte le copie trasformate associati all'asset). Il filtro degli asset viene eseguito attraverso **manifesti dinamici**creati su richiesta del cliente per trasmettere un video in streaming in base ai filtri specificati.

Per altre informazioni sui filtri e sul manifesto dinamico, vedere [Filtri e manifesti dinamici](media-services-dynamic-manifest-overview.md).

In questo articolo viene illustrato come utilizzare Media Services .NET SDK per creare, aggiornare ed eliminare filtri. 

Nota che se si aggiorna un filtro, potrebbe richiedere fino a due minuti per l'endpoint per aggiornare le regole di streaming. Se il contenuto è stato trasmesso usando dei filtri (e memorizzato nelle cache dei proxy e delle reti CDN), l'aggiornamento del filtro può determinare un errore del lettore. Cancellare la cache dopo l'aggiornamento del filtro. Se questa operazione non è consentita, prendere in considerazione la possibilità di usare un filtro diverso. 

## <a name="types-used-to-create-filters"></a>Tipi usati per la creazione dei filtri
Durante la creazione dei filtri vengono usati i tipi seguenti: 

* **IStreamingFilter**.  Questo tipo è basato sulla seguente API REST [Filter](https://docs.microsoft.com/rest/api/media/operations/filter)
* **IStreamingAssetFilter**. Questo tipo è basato sulla seguente API REST [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)
* **PresentationTimeRange**. Questo tipo è basato sulla seguente API REST [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)
* **FilterTrackSelectStatement** e **IFilterTrackPropertyCondition**. Questi tipi sono basati sulle seguenti API REST [FilterTrackSelect e FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)

## <a name="createupdatereaddelete-global-filters"></a>Creare/aggiornare/leggere/eliminare filtri globali
Il codice seguente viene illustrato come utilizzare .NET per creare, aggiornare, leggere ed eliminare filtri di asset.

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
Il codice seguente viene illustrato come utilizzare .NET per creare, aggiornare, leggere ed eliminare filtri di asset.

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
Per informazioni su come pubblicare e distribuire asset, vedere [Informazioni generali sulla distribuzione di contenuti ai clienti](media-services-deliver-content-overview.md).

Gli esempi seguenti illustrano come aggiungere filtri agli URL di streaming.

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

