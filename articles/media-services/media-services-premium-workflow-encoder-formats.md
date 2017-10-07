---
title: flusso di lavoro Premium del codificatore aaaMedia codec e formati | Documenti Microsoft
description: Questo argomento offre una panoramica dei codec e dei formati del flusso di lavoro Premium del codificatore multimediale
services: media-services
documentationcenter: 
author: juliako
manager: erik43
editor: 
ms.assetid: b197fce8-3b9b-4189-8d08-486810c0426f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;anilmur
ms.openlocfilehash: e781384ca8f08926f00c83b6710fd413ce2a3e1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="media-encoder-premium-workflow-formats-and-codecs"></a>Codec e formati del flusso di lavoro Premium del codificatore multimediale
> [!NOTE]
> Per domande relative al codificatore Premium, inviare mepd tramite un messaggio di posta elettronica a Microsoft.com.
> 
> Il processore di contenuti multimediali del flusso di lavoro Premium del codificatore multimediale descritto in questo argomento non è disponibile in Cina. 
> 
> 

Questo documento contiene un elenco di formati di file di input e output e i codec che sono supportati dalla versione di anteprima pubblica di hello di hello **flusso di lavoro Premium del codificatore multimediale** codificatore.

[Codec e formati di input del flusso di lavoro Premium del codificatore multimediale](#input_formats)

[Codec e formati di output del flusso di lavoro Premium del codificatore multimediale](#output_formats)

**flusso di lavoro Premium del codificatore multimediale** supporta i sottotitoli codificati descritti in [questa](#closed_captioning) sezione. 

## <a id="input_formats"></a>Codec e formati di input del flusso di lavoro Premium del codificatore multimediale
Hello seguente sezione vengono elencate hello codec e formati di file che supporta il processore di contenuti multimediali come input.

### <a name="input-containerfile-formats"></a>Contenitore di input/formati di file
* Adobe® Flash® F4V
* MXF/SMPTE 377M
* GXF
* MPEG-2 Transport Stream
* MPEG-2 Program Stream
* MPEG-4/MP4
* Windows Media/ASF
* AVI (non compresso 8 bit/10 bit)

### <a name="input-video-codecs"></a>Codec video di input
* AVC 8 bit/10 bit, di too4:2:2, tra cui AVCIntra
* Avid DNxHD (in MXF)
* DVCPro/DVCProHD (in MXF)
* JPEG2000
* MPEG-2 (backup too422 profilo e di livello elevato, ad esempio varianti XDCAM, XDCAM HD, XDCAM IMX, CableLabs® e D10)
* MPEG-1
* Windows Media Video/VC-1

### <a name="input-audio-codecs"></a>Codec audio di input
* AES (SMPTE 331M e 302M, AES3-2003)
* Dolby® E
* Dolby® Digital (AC3)
* AAC (AAC-LC, HE-AAC e AAC-HEv2; backup too5.1)
* MPEG Layer 2
* MP3 (MPEG-1 Audio Layer 3)
* Windows Media Audio
* WAV/PCM

## <a id="output_format"></a>Codec e formati di output del flusso di lavoro Premium del codificatore multimediale
Hello nella sezione seguente sono elencati hello codec e formati di file che sono supportati come output di questo processore di contenuti multimediali.

### <a name="output-containerfile-formats"></a>Contenitore di output/formati di file
* Adobe® Flash® F4V
* MXF (OP1a, XDCAM e AS02)
* DPP (incluso AS11)
* GXF
* MPEG-4/MP4
* Windows Media/ASF
* AVI (non compresso 8 bit/10 bit)
* Formato di file Smooth Streaming (PIFF 1.3)
* MPEG-TS 

### <a name="output-video-codecs"></a>Codec video di output
* AVC (h. 264; 8 bit; backup tooHigh profilo, livello 5.2; HD Ultra 4K. All'interno di AVC)
* Avid DNxHD (in MXF)
* DVCPro/DVCProHD (in MXF)
* MPEG-2 (backup too422 profilo e di livello elevato, ad esempio varianti XDCAM, XDCAM HD, XDCAM IMX, CableLabs® e D10)
* MPEG-1
* Windows Media Video/VC-1
* Creazione anteprime JPEG

### <a name="output-audio-codecs"></a>Codec audio di output
* AES (SMPTE 331M e 302M, AES3-2003)
* Dolby® Digital (AC3)
* Dolby® Digital Plus (AC3 E) di too7.1
* AAC (AAC-LC, HE-AAC e AAC-HEv2; backup too5.1)
* MPEG Layer 2
* MP3 (MPEG-1 Audio Layer 3)
* Windows Media Audio

>[!NOTE]
>Se si codifica tooDolby® Digital (AC3), è possibile scrivere l'output di hello solo in un file ISO MP4.

## <a id="closed_captioning"></a>Supporto per sottotitoli codificati
In ingresso, il **flusso di lavoro Premium del codificatore multimediale** supporta:

1. File SCC
2. File SMPTE-TT
3. CEA-608/CEA-708 – Trasportato come dati (messaggi SEI di flussi elementari H.264, ATSC/53, SCTE20) o trasportato come dati ausiliari in file MXF/GXF
4. File con sottotitoli STL

Nell'output, sono disponibile hello le opzioni seguenti:

1. CEA-608 tooCEA 708 traduzione
2. Pass-through di CEA-608/CEA-708 (incorporato in messaggi SEI di flussi elementari H.264 o trasportato come dati ausiliari in file MXF)
3. SCC
4. SMPTE Timed Text (da origine CEA-608 per SMPTE RP2052; inclusa la creazione di file DFXP)
5. File di sottotitoli SRT
6. Flussi di sottotitoli DVB

Nota: non tutti hello sopra i formati di output sono supportati per il recapito tramite streaming in servizi multimediali di Azure.

## <a name="known-issues"></a>Problemi noti
Se il video di input non contiene sottotitoli, hello output che asset conterrà comunque un file TTML vuoto. 

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

