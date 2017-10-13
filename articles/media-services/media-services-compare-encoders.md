---
title: Confronto tra i codificatori multimediali su richiesta di Azure | Documentazione Microsoft
description: "Questo argomento mette a confronto le funzionalità di codifica di **Media Encoder Standard** e di **Flusso di lavoro Premium del codificatore multimediale**."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: a79437c0-4832-423a-bca8-82632b2c47cc
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: 3bba48d5425ae47c72aca893af7c11fe270c2929
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="comparison-of-azure-on-demand-media-encoders"></a>Confronto tra i codificatori multimediali su richiesta di Azure

Questo argomento mette a confronto le funzionalità di codifica di **Media Encoder Standard** e di **Flusso di lavoro Premium del codificatore multimediale**.

## <a name="video-and-audio-processing-capabilities"></a>Funzionalità di elaborazione audio e video

La tabella seguente mette a confronto le funzionalità di Media Encoder Standard (MES) e Media Encoder Premium Workflow (MEPW). 

|Funzionalità|Codificatore multimediale standard|Flusso di lavoro Premium del codificatore multimediale|
|---|---|---|
|Applicazione della logica condizionale durante la codifica<br/>(ad esempio, se l'input è HD viene usata la codifica audio 5.1)|No|Sì|
|Sottotitoli|No|[Sì](media-services-premium-workflow-encoder-formats.md#closed_captioning)|
|[Dolby® Professional Loudness Correction](http://www.dolby.com/us/en/technologies/dolby-professional-loudness-solutions.pdf)<br/> con Dialogue Intelligence™|No|Sì|
|Deinterlacciamento, telecine inverso|Basic|Qualità broadcast|
|Rilevamento e rimozione dei bordi neri <br/>(formati 4:3, formati 16:9)|No|Sì|
|Generazione di anteprime|[Sì](media-services-dotnet-generate-thumbnail-with-mes.md)|[Sì](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4)|
|Ritaglio/rifilatura e pinzatura di video|[Sì](media-services-advanced-encoding-with-mes.md#trim_video)|Sì|
|Sovrapposizioni di audio o video|[Sì](media-services-advanced-encoding-with-mes.md#overlay)|[Sì](media-services-media-encoder-premium-workflow-multiplefilesinput.md#example-1--overlay-an-image-on-top-of-the-video)|
|Sovrapposizioni di elementi grafici|Da origini di immagini|Da origini di immagini e testo|
|Tracce audio in più lingue|Limitato|[Sì](media-services-media-encoder-premium-workflow-multiplefilesinput.md#example-2--multiple-audio-language-encoding)|

## <a id="billing"></a>Metro di fatturazione usato da ogni codificatore
| Nome del processore multimediale | Prezzi applicabili | Note |
| --- | --- | --- |
| **Codificatore multimediale standard** |CODIFICATORE |Le attività di codifica verranno addebitate le attività in base alla durata totale, espressa in minuti, di tutti i file multimediali generati come output, alla tariffa specificata [qui][1], nella colonna CODIFICATORE. |
| **Flusso di lavoro Premium del codificatore multimediale** |CODIFICATORE PREMIUM |Le attività di codifica verranno addebitate le attività in base alla durata totale, espressa in minuti, di tutti i file multimediali generati come output, alla tariffa specificata [qui][1], nella colonna CODIFICATORE PREMIUM. |

## <a name="input-containerfile-formats"></a>Contenitore di input/formati di file
| Contenitore di input/formati di file | Codificatore multimediale standard | Flusso di lavoro Premium del codificatore multimediale |
| --- | --- | --- |
| Adobe® Flash® F4V |Sì |Sì |
| MXF/SMPTE 377M |Sì |Sì |
| GXF |Sì |Sì |
| MPEG-2 Transport Stream |Sì |Sì |
| MPEG-2 Program Stream |Sì |Sì |
| MPEG-4/MP4 |Sì |Sì |
| Windows Media/ASF |Sì |Sì |
| AVI (non compresso 8 bit/10 bit) |Sì |Sì |
| 3GPP/3GPP2 |Sì |No |
| Formato di file Smooth Streaming (PIFF 1.3) |Sì |No |
| [Microsoft Digital Video Recording (DVR-MS)](https://msdn.microsoft.com/library/windows/desktop/dd692984) |Sì |No |
| Matroska/WebM |Sì |No |
| QuickTime (.mov) |Sì |No |

## <a name="input-video-codecs"></a>Codec video di input
| Codec video di input | Codificatore multimediale standard | Flusso di lavoro Premium del codificatore multimediale |
| --- | --- | --- |
| AVC 8 bit/10 bit, fino a 4:2:2, incluso AVCIntra |4:2:0 e 4:2:2 a 8 bit |Sì |
| Avid DNxHD (in MXF) |Sì |Sì |
| DVCPro/DVCProHD (in MXF) |Sì |Sì |
| JPEG2000 |Sì |Sì |
| MPEG-2 (fino a 4:2:2 Profile e High Level; incluse varianti quali XDCAM, XDCAM HD, XDCAM IMX, CableLabs® e D10) |Fino a 422 Profile |Sì |
| MPEG-1 |Sì |Sì |
| Windows Media Video/VC-1 |Sì |Sì |
| Canopus HQ/HQX |No |No |
| MPEG-4 parte 2 |Sì |No |
| [Theora](https://en.wikipedia.org/wiki/Theora) |Sì |No |
| Apple ProRes 422 |Sì |No |
| Apple ProRes 422 LT |Sì |No |
| Apple ProRes 422 HQ |Sì |No |
| Apple ProRes Proxy |Sì |No |
| Apple ProRes 4444 |Sì |No |
| Apple ProRes 4444 XQ |Sì |No |

## <a name="input-audio-codecs"></a>Codec audio di input
| Codec audio di input | Codificatore multimediale standard | Flusso di lavoro Premium del codificatore multimediale |
| --- | --- | --- |
| AES (SMPTE 331M e 302M, AES3-2003) |No |Sì |
| Dolby® E |No |Sì |
| Dolby® Digital (AC3) |No |Sì |
| Dolby® Digital Plus (E-AC3) |No |Sì |
| AAC (AAC-LC, AAC-HE e AAC-HEv2; fino a 5.1) |Sì |Sì |
| MPEG Layer 2 |Sì |Sì |
| MP3 (MPEG-1 Audio Layer 3) |Sì |Sì |
| Windows Media Audio |Sì |Sì |
| WAV/PCM |Sì |Sì |
| [FLAC](https://en.wikipedia.org/wiki/FLAC)</a> |Sì |No |
| [Opus](https://en.wikipedia.org/wiki/Opus_\(audio_format\)) |Sì |No |
| [Vorbis](https://en.wikipedia.org/wiki/Vorbis)</a> |Sì |No |

## <a name="output-containerfile-formats"></a>Contenitore di output/formati di file
| Contenitore di output/formati di file | Codificatore multimediale standard | Flusso di lavoro Premium del codificatore multimediale |
| --- | --- | --- |
| Adobe® Flash® F4V |No |Sì |
| MXF (OP1a, XDCAM e AS02) |No |Sì |
| DPP (incluso AS11) |No |Sì |
| GXF |No |Sì |
| MPEG-4/MP4 |Sì |Sì |
| MPEG-TS |Sì |Sì |
| Windows Media/ASF |No |Sì |
| AVI (non compresso 8 bit/10 bit) |No |Sì |
| Formato di file Smooth Streaming (PIFF 1.3) |No |Sì |

## <a name="output-video-codecs"></a>Codec video di output
| Codec video di output | Codificatore multimediale standard | Flusso di lavoro Premium del codificatore multimediale |
| --- | --- | --- |
| AVC (H.264; 8 bit; fino a High Profile, Level 5.2; 4K Ultra HD; AVC Intra) |Solo 4:2:0 a 8 bit |Sì |
| Avid DNxHD (in MXF) |No |Sì |
| MPEG-2 (fino a 4:2:2 Profile e High Level; incluse varianti quali XDCAM, XDCAM HD, XDCAM IMX, CableLabs® e D10) |No |Sì |
| MPEG-1 |No |Sì |
| Windows Media Video/VC-1 |No |Sì |
| Creazione anteprime JPEG |Sì |Sì |
| Creazione di anteprime PNG |Sì |Sì |
| Creazione di anteprime BMP |Sì |No |

## <a name="output-audio-codecs"></a>Codec audio di output
| Codec audio di output | Codificatore multimediale standard | Flusso di lavoro Premium del codificatore multimediale |
| --- | --- | --- |
| AES (SMPTE 331M e 302M, AES3-2003) |No |Sì |
| Dolby® Digital (AC3) |No |Sì |
| Dolby® Digital Plus (E-AC3) fino a 7.1 |No |Sì |
| AAC (AAC-LC, AAC-HE e AAC-HEv2; fino a 5.1) |Sì |Sì |
| MPEG Layer 2 |No |Sì |
| MP3 (MPEG-1 Audio Layer 3) |No |Sì |
| Windows Media Audio |No |Sì |

>[!NOTE]
>Se si codifica per Dolby® Digital (AC3), l'output può essere scritto solo in un file ISO MP4.

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a>Articoli correlati
* [Eseguire attività di codifica avanzata personalizzando i set di impostazioni di Media Encoder Standard](media-services-custom-mes-presets-with-dotnet.md)
* [Quote e limitazioni](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
