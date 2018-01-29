---
title: Usare Azure Media Clipper nel portale | Microsoft Docs
description: Creare clip con Azure Media Clipper dal portale di Azure
services: media-services
keywords: clip;clip secondarie;codifica;file multimediali
author: dbgeorge
manager: jasonsue
ms.author: dwgeo
ms.date: 11/10/2017
ms.topic: article
ms.service: media-services
ms.openlocfilehash: 1deca68cd6a61ede7536c4d5544036a10c54209b
ms.sourcegitcommit: cc03e42cffdec775515f489fa8e02edd35fd83dc
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/07/2017
---
# <a name="create-clips-with-azure-media-clipper-in-the-portal"></a>Creare clip con Azure Media Clipper nel portale
È possibile usare Azure Media Clipper nel portale per creare clip da asset negli account Servizi multimediali. Per iniziare, passare all'account Servizi multimediali nel portale. Selezionare quindi la scheda **Subclip** (Clip secondaria).

Nella scheda **Subclip** (Clip secondaria) si può iniziare a comporre clip. Nel portale, Clipper carica file MP4 a bitrate singolo, file MP4 a bitrate multipli e archivi live pubblicati con un localizzatore di streaming valido. Gli asset non pubblicati non vengono caricati.

Clipper è attualmente in anteprima pubblica. Per accedere a Clipper nel portale di Azure, visitare questa [pagina di anteprima pubblica](https://portal.azure.com/?feature.subclipper=true).

L'immagine seguente illustra la pagina di destinazione Clipper nell'account di servizi multimediali: ![Azure Media Clipper nel portale di Azure](media/media-services-azure-media-clipper-portal/media-services-azure-media-clipper-portal.png)

## <a name="producing-clips"></a>Creazione di clip
Per creare una clip, trascinare un asset sull'interfaccia delle clip. Se si conoscono gli indicatori temporali, è possibile immetterli manualmente nell'interfaccia. In caso contrario, riprodurre l'asset o trascinare l'indicatore di riproduzione per trovare l'orario dell'indicatore di inizio e l'orario dell'indicatore di fine desiderati. Se non viene specificato un orario dell'indicatore di inizio o di fine, la clip, rispettivamente, parte dall'inizio o continua fino alla fine dell'asset di input.

Per spostarsi con precisione al fotogramma o al GOP, usare i pulsanti fotogramma/GOP successivo o fotogramma/GOP precedente. Per eseguire il ritaglio su più asset, trascinare più asset dal pannello di selezione degli asset all'interfaccia delle clip. È possibile selezionare gli asset nell'interfaccia e riorganizzarli nell'ordine desiderato. Il pannello di selezione degli asset include durata, tipo e metadati relativi alla risoluzione di ogni asset. Quando si concatenano più asset, considerare la risoluzione di origine di ogni file di input. Se le risoluzioni di origine sono diverse, l'input con risoluzione inferiore passa alla risoluzione dell'asset con la risoluzione più elevata. Per visualizzare in anteprima l'output del processo di ritaglio, selezionare il pulsante di anteprima. La clip verrà riprodotta dagli indicatori temporali selezionati.

## <a name="producing-dynamic-manifest-filters"></a>Creazione di filtri manifesto dinamico
I [filtri manifesto dinamico](https://azure.microsoft.com/blog/dynamic-manifest/) descrivono un set di regole in base agli attributi del manifesto e alla sequenza temporale dell'asset. Queste regole determinano come verrà manipolata la playlist di output (manifesto) dall'endpoint di streaming. Il filtro può essere usato per modificare i segmenti trasmessi per la riproduzione. I filtri creati da Clipper sono filtri locali specifici dell'asset di origine. A differenza delle clip sottoposte a rendering, i filtri non sono nuovi asset e non richiedono un processo di codifica per la creazione. Possono essere creati rapidamente tramite [.NET SDK](https://docs.microsoft.com/azure/media-services/media-services-dotnet-dynamic-manifest) o l'[API REST](https://docs.microsoft.com/azure/media-services/media-services-rest-dynamic-manifest), ma offrono solo precisione al GOP. Negli asset codificati per lo streaming, la dimensione dei GOP è in genere di due secondi.

Per creare un filtro manifesto dinamico, accedere alla scheda **Asset** e selezionare l'asset desiderato. Selezionare il pulsante **Clip secondaria** per il menu superiore. Selezionare il filtro manifesto dinamico come modalità di ritaglio nel menu delle impostazioni avanzate. È possibile quindi seguire lo stesso processo per generare una clip di cui è stato eseguito il rendering per la creazione del filtro. I filtri possono essere creati solo da un singolo asset.

L'immagine seguente illustra Clipper in modalità di filtro manifesto dinamico nel portale di Azure: ![Azure Media Clipper in modalità filtro manifesto dinamico nel portale di Azure](media/media-services-azure-media-clipper-portal/media-services-azure-media-clipper-filter.PNG)

## <a name="submitting-clipping-jobs"></a>Invio di processi di ritaglio
Al termine della composizione della clip, selezionare il pulsante per l'invio del processo per avviare il processo di ritaglio o la chiamata del manifesto dinamico corrispondente.

## <a name="next-steps"></a>Passaggi successivi
Per iniziare a usare Azure Media Clipper, vedere l'[articolo introduttivo](media-services-azure-media-clipper-getting-started.md) per informazioni dettagliate su come distribuire il widget.