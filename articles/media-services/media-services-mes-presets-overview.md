---
title: set di impostazioni di aaaTask per MES (Media Encoder Standard) | Documenti Microsoft
description: "Panoramica dei set di impostazioni di attività per MES (Media Encoder Standard) e offre argomento Hello."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: f243ed1c-ac9c-4300-a5f7-f092cf9853b9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 56e098d6d8c8f84031421ec59f087f20370ba111
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="task-presets-for-mes-media-encoder-standard"></a>Set di impostazioni delle attività MES (Media Encoder Standard)

**Media Encoder Standard** definisce un set di impostazioni di codifica che è possibile usare per la creazione di processi di codifica. È consigliabile hello toouse "Il flusso adattivo" predefinito se si desidera tooencode un video per streaming con servizi multimediali. Quando si specifica il set di impostazioni Media Encoder Standard [genera automaticamente un bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md). 

Tuttavia, se è necessario toocustomize un set di impostazioni di codifica, è necessario effettuare una delle hello predefiniti definiti in questa sezione come modello per la configurazione personalizzata di codifica. Per una spiegazione di ogni elemento in tali mezzi predefiniti e i valori validi di hello per ogni elemento, vedere hello [schema Media Encoder Standard](media-services-mes-schema.md) argomento.  
  
> [!NOTE]
>  Quando si utilizza un set di impostazioni di codifica 4 KB, è necessario ottenere hello `S3` tipo di unità riservate. Per ulteriori informazioni, vedere [come tooScale codifica](https://azure.microsoft.com/en-us/documentation/articles/media-services-portal-encoding-units).  
  
Quando si usa Media Encoder Standard, la rotazione è abilitata per impostazione predefinita. Se il video è stato registrato su uno smartphone o altro dispositivo mobile in modalità verticale, quindi tali predefiniti, per impostazione predefinita, ruoterà li tooencoding precedente di modalità tooLandscape (a differenza di, quando si lavora con Azure Media Encoder, rotazione del video in cui è un'operazione manuale, come descritto in [questo](http://azure.microsoft.com/blog/2014/08/21/advanced-encoding-features-in-azure-media-encoder/) blog, in "Video rotazione").  
  
Set di impostazioni disponibili:  
  
 [H264 bitrate multiplo con risoluzione 1080p e Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-1080p-Audio-5.1.md) produce un set di 8 file MP4 allineati GOP, comprese tra 6000 kbps too400 kbps e audio 5.1 AAC.  
  
 [H264 bitrate multiplo con risoluzione 1080p](media-services-mes-preset-H264-Multiple-Bitrate-1080p.md) produce un set di 8 file MP4 allineati GOP, comprese tra 6000 kbps too400 kbps e audio AAC stereo.  
  
 [H264 bitrate multiplo con risoluzione 16x9 per iOS](media-services-mes-preset-H264-Multiple-Bitrate-16x9-for-iOS.md) produce un set di 8 file MP4 allineati GOP, compreso fra 8500 kbps too200 kbps e audio AAC stereo.  
  
 [H264 bitrate multiplo con risoluzione 16x9 SD e Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-16x9-SD-Audio-5.1.md) produce un set di 5 file MP4 allineati GOP, compreso tra 1900 kbps too400 kbps e audio 5.1 AAC.  
  
 [H264 bitrate multiplo con risoluzione 16x9 SD](media-services-mes-preset-H264-Multiple-Bitrate-16x9-SD.md) produce un set di 5 file MP4 allineati GOP, compreso tra 1900 kbps too400 kbps e audio AAC stereo.  
  
 [H264 bitrate multiplo con risoluzione 4K e Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-4K-Audio-5.1.md) produce un set di file MP4 allineati GOP a 12, compreso fra 20000 kbps too1000 kbps e audio 5.1 AAC.  
  
 [H264 bitrate multiplo con risoluzione 4K](media-services-mes-preset-H264-Multiple-Bitrate-4K.md) produce un set di file MP4 allineati GOP a 12, compreso fra 20000 kbps too1000 kbps e audio AAC stereo.  
  
 [H264 bitrate multiplo con risoluzione 4x3 per iOS](media-services-mes-preset-H264-Multiple-Bitrate-4x3-for-iOS.md) produce un set di 8 file MP4 allineati GOP, compreso fra 8500 kbps too200 kbps e audio AAC stereo.  
  
 [H264 bitrate multiplo con risoluzione 4x3 SD e Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-4x3-SD-Audio-5.1.md) produce un set di 5 file MP4 allineati GOP, compreso tra 1600 kbps too400 kbps e audio 5.1 AAC.  
  
 [H264 bitrate multiplo con risoluzione 4x3 SD](media-services-mes-preset-H264-Multiple-Bitrate-4x3-SD.md) produce un set di 5 file MP4 allineati GOP, compreso tra 1600 kbps too400 kbps e audio AAC stereo.  
  
 [H264 bitrate multiplo con risoluzione 720p e Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-720p-Audio-5.1.md) produce un set di file MP4 allineati GOP a 6, comprese tra 3400 kbps too400 kbps e audio 5.1 AAC.  
  
 [H264 bitrate multiplo con risoluzione 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) produce un set di file MP4 allineati GOP a 6, comprese tra 3400 kbps too400 kbps e audio AAC stereo.  
  
 [Codec video H.264 a bitrate singolo con risoluzione 1080p e audio 5.1](media-services-mes-preset-H264-Single-Bitrate-1080p-Audio-5.1.md) genera un file MP4 con audio AAC 5.1 e una velocità in bit di 6.750 kbps.  
  
 [Codec video H.264 a bitrate singolo con risoluzione 1080p](media-services-mes-preset-H264-Single-Bitrate-1080p.md) genera un file MP4 con audio AAC stereo e una velocità in bit di 6.750 kbps.  
  
 [Codec video H.264 a bitrate singolo con risoluzione 4K e audio 5.1](media-services-mes-preset-H264-Single-Bitrate-4K-Audio-5.1.md) genera un file MP4 con audio AAC 5.1 e una velocità in bit di 18.000 kbps.  
  
 [Codec video H.264 a bitrate singolo con risoluzione 4K](media-services-mes-preset-H264-Single-Bitrate-4K.md) genera un file MP4 con audio AAC stereo e una velocità in bit di 18.000 kbps.  
  
 [Codec video H.264 a bitrate singolo con risoluzione 4x3 SD e audio 5.1](media-services-mes-preset-H264-Single-Bitrate-4x3-SD-Audio-5.1.md) genera un file MP4 con audio AAC 5.1 e una velocità in bit di 1800 kbps.  
  
 [Codec video H.264 a bitrate singolo con risoluzione 4x3 SD](media-services-mes-preset-H264-Single-Bitrate-4x3-SD.md) genera un file MP4 con audio AAC stereo e una velocità in bit di 1800 kbps.  
  
 [Codec video H.264 a bitrate singolo con risoluzione 16x9 SD e audio 5.1](media-services-mes-preset-H264-Single-Bitrate-16x9-SD-Audio-5.1.md) genera un file MP4 con audio AAC 5.1 e una velocità in bit di 2.200 kbps.  
  
 [Codec video H.264 a bitrate singolo con risoluzione 16x9 SD](media-services-mes-preset-H264-Single-Bitrate-16x9-SD.md) genera un file MP4 con audio AAC stereo e una velocità in bit di 2.200 kbps.  
  
 [Codec video H.264 a bitrate singolo con risoluzione 720p e audio 5.1](media-services-mes-preset-H264-Single-Bitrate-720p-Audio-5.1.md) genera un file MP4 con audio AAC 5.1 e una velocità in bit di 4.500 kbps.  
  
 [Codec video H.264 a bitrate singolo con risoluzione 720p per Android](media-services-mes-preset-H264-Single-Bitrate-720p-for-Android.md) genera un file MP4 con audio AAC 5.1 stereo e una velocità in bit di 2.000 kbps.  
  
 [Codec video H.264 a bitrate singolo con risoluzione 720p](media-services-mes-preset-H264-Single-Bitrate-720p.md) genera un file MP4 con audio AAC stereo e una velocità in bit di 4.500 kbps.  
  
 [Codec video H.264 a bitrate singolo con risoluzione SD di alta qualità per Android](media-services-mes-preset-H264-Single-Bitrate-High-Quality-SD-for-Android.md) genera un file MP4 con audio AAC stereo e una velocità in bit di 500 kbps.  
  
 [Codec video H.264 a bitrate singolo con risoluzione SD di bassa qualità per Android](media-services-mes-preset-H264-Single-Bitrate-Low-Quality-SD-for-Android.md) genera un file MP4 con audio AAC stereo e una velocità in bit di 56 kbps.  
  
 Per ulteriori informazioni vedere codificatori servizi correlati tooMedia, [codifica su richiesta con servizi multimediali di Azure](https://azure.microsoft.com/en-us/documentation/articles/media-services-encode-asset/).
