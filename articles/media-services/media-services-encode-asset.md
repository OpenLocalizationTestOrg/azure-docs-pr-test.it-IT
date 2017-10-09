---
title: aaaOverview e confronto di Azure su richiesta codificatori supporti | Documenti Microsoft
description: Questo argomento offre una panoramica e un confronto tra i codificatori multimediali su richiesta di Azure.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: e6bfc068-fa46-4d68-b1ce-9092c8f3a3c9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: 24a3e0a16162b1bebfcde290b6baf2dd8dbfff17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-and-comparison-of-azure-on-demand-media-encoders"></a>Panoramica e confronto dei codificatori multimediali su richiesta di Azure
## <a name="encoding-overview"></a>Panoramica della codifica
Servizi multimediali di Azure fornisce più opzioni per la codifica dei file multimediali in cloud hello hello.

Quando si avvia con servizi multimediali, è importante toounderstand differenza di hello tra codec e formati di file.
Codec sono costituiti da software hello che implementa gli algoritmi di compressione/decompressione hello, mentre i formati di file sono contenitori che includono il video compresso hello.

Servizi multimediali fornisce creazione dinamica dei pacchetti che consente la velocità in bit adattiva MP4 o Smooth Streaming con codifica contenuto in streaming formati supportati da servizi multimediali (MPEG DASH, HLS, Smooth Streaming) toodeliver senza che sia necessario toore-package in questi formati di streaming.

>[!NOTE]
>Quando viene creato l'account di sistema AMS un **predefinito** endpoint di streaming viene aggiunto l'account tooyour in hello **arrestato** stato. lo streaming del contenuto e intraprendere sfruttare creazione dinamica dei pacchetti e la crittografia dinamica, toostart hello endpoint di streaming da cui si desidera in hello del contenuto toostream è toobe **esecuzione** stato. sfruttare tootake [creazione dinamica dei pacchetti](media-services-dynamic-packaging-overview.md), è necessario toodo hello segue:
>
>Inoltre, è possibile codificare il file di origine in un set di file MP4 o file Smooth Streaming a velocità in bit adattiva (passaggi codifica hello sono illustrati più avanti in questa esercitazione).

Servizi multimediali supporta i seguenti hello in codificatori di richiesta che sono descritte in questo articolo:

* [Codificatore multimediale standard](media-services-encode-asset.md#media-encoder-standard)
* [Flusso di lavoro Premium del codificatore multimediale](media-services-encode-asset.md#media-encoder-premium-workflow)

In questo articolo offre una breve panoramica su richiesta codificatori media e fornisce collegamenti tooarticles che offrono informazioni più dettagliate. argomento Hello fornisce inoltre il confronto dei codificatori hello.

>[!NOTE]
>Per impostazione predefinita, in ciascun account di Servizi multimediali può essere attiva una sola attività di codifica alla volta. È possibile riservare unità di codifica che consentono di toohave più attività di codifica contemporaneamente, uno per ciascuna unità acquistata. Per informazioni, vedere [Scalabilità dell’unità di codifica](media-services-scale-media-processing-overview.md).

## <a name="media-encoder-standard"></a>Codificatore multimediale standard
### <a name="how-toouse"></a>Come toouse
[Come tooencode con Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md)

### <a name="formats"></a>Formati
[Codec e formati](media-services-media-encoder-standard-formats.md)

### <a name="presets"></a>Impostazioni predefinite
Media Encoder Standard viene configurato usando uno dei set di impostazioni di codificatore hello descritto [qui](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).

### <a name="input-and-output-metadata"></a>Metadati di input e output
Hello codificatori dei metadati di input sono descritto [qui](media-services-input-metadata-schema.md).

Hello codificatori output metadati descritto [qui](media-services-output-metadata-schema.md).

### <a name="generate-thumbnails"></a>Generare anteprime
Per informazioni, vedere [come anteprime toogenerate usando Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).

### <a name="trim-videos-clipping"></a>Tagliare video (ritaglio)
Per informazioni, vedere [come video tootrim Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video).

### <a name="create-overlays"></a>Creare sovrimpressioni
Per informazioni, vedere [come sovrapposizioni toocreate usando Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay).

### <a name="see-also"></a>Vedere anche
[blog di servizi multimediali Hello](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/)

## <a name="media-encoder-premium-workflow"></a>Flusso di lavoro Premium del codificatore multimediale
### <a name="overview"></a>Overview
[Introduzione alla codifica Premium in Servizi multimediali di Azure](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/)

### <a name="how-toouse"></a>Come toouse
Il flusso di lavoro Premium del codificatore multimediale viene configurato usando flussi di lavoro complessi. I file del flusso di lavoro può essere creati e aggiornato utilizzando hello [Progettazione flussi di lavoro](media-services-workflow-designer.md) strumento.

[Come tooUse codifica Premium in servizi multimediali di Azure](https://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services/)

### <a name="known-issues"></a>Problemi noti
Se il video di input non contiene sottotitoli, hello output che asset conterrà comunque un file TTML vuoto.


## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a>Articoli correlati
* [Eseguire attività di codifica avanzata personalizzando i set di impostazioni di Media Encoder Standard](media-services-custom-mes-presets-with-dotnet.md)
* [Quote e limitazioni](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
