---
title: set di impostazioni bitrate singolo con risoluzione 16x9 SD Media Encoder Standard aaaH264 - Azure | Documenti Microsoft
description: Hello argomento viene fornita una panoramica di hello * * H264 bitrate singolo con risoluzione 16x9 SD * * set di impostazioni.
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: ce0efc07-3461-44f6-a7bc-c4877bc09529
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: e5fbf6b8accaf779014bee67ee4f5fd6910b2d25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="h264-single-bitrate-16x9-sd"></a><span data-ttu-id="2fea4-103">Codec video H.264 a bitrate singolo con risoluzione 16x9 SD</span><span class="sxs-lookup"><span data-stu-id="2fea4-103">H264 Single Bitrate 16x9 SD</span></span>
<span data-ttu-id="2fea4-104">`Media Encoder Standard` definisce un set di impostazioni di codifica che è possibile usare per la creazione di processi di codifica.</span><span class="sxs-lookup"><span data-stu-id="2fea4-104">`Media Encoder Standard` defines a set of encoding presets you can use when creating encoding jobs.</span></span> <span data-ttu-id="2fea4-105">È possibile utilizzare un `preset name` toospecify in formato di cui si desidera tooencode nel file multimediale.</span><span class="sxs-lookup"><span data-stu-id="2fea4-105">You can either use a `preset name` toospecify into which format you would like tooencode your media file.</span></span> <span data-ttu-id="2fea4-106">oppure creare set di impostazioni basati su JSON o XML personalizzati, con codifica UTF-8 o UTF-16.</span><span class="sxs-lookup"><span data-stu-id="2fea4-106">Or, you can create your own JSON or XML-based presets (using UTF-8 or UTF-16 encoding.</span></span> <span data-ttu-id="2fea4-107">È quindi necessario passare codificatore personalizzato toohello preimpostato hello.</span><span class="sxs-lookup"><span data-stu-id="2fea4-107">You would then pass hello custom preset toohello encoder.</span></span> <span data-ttu-id="2fea4-108">Per elenco hello di hello tutti nomi supportati da questo set di impostazioni `Media Encoder Standard` codificatore, vedere [set di impostazioni di attività per supporti codificatore Standard](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2fea4-108">For hello list of all hello preset names supported by this `Media Encoder Standard` encoder, see [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span></span>  
  
 <span data-ttu-id="2fea4-109">In questo argomento viene hello `H264 Single Bitrate 16x9 SD` predefinito in formato XML e JSON.</span><span class="sxs-lookup"><span data-stu-id="2fea4-109">This topic shows hello `H264 Single Bitrate 16x9 SD` preset in XML and JSON format.</span></span>  
  
 <span data-ttu-id="2fea4-110">Il set di impostazioni genera un unico file MP4 con una velocità in bit di 2200 kbps e audio AAC stereo.</span><span class="sxs-lookup"><span data-stu-id="2fea4-110">This preset produces a single MP4 file with a bitrate of 2200 kbps, and stereo AAC audio.</span></span> <span data-ttu-id="2fea4-111">Per informazioni dettagliate sul profilo, velocità in bit, il campionamento di velocità e così via di questo set di impostazioni, esaminare hello XML o JSON definita di seguito.</span><span class="sxs-lookup"><span data-stu-id="2fea4-111">For detailed information about profile, bitrate, sampling rate, etc. of this preset, examine hello XML or JSON defined below.</span></span> <span data-ttu-id="2fea4-112">Per una spiegazione di ogni elemento in tali mezzi predefiniti e i valori validi di hello per ogni elemento, vedere hello [schema Media Encoder Standard](media-services-mes-schema.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="2fea4-112">For explanations of what each element in these presets means, and hello valid values for each element, see hello [Media Encoder Standard schema](media-services-mes-schema.md) topic.</span></span>  
  
 <span data-ttu-id="2fea4-113">XML</span><span class="sxs-lookup"><span data-stu-id="2fea4-113">XML</span></span>  
  
```  
<?xml version="1.0" encoding="utf-16"?>  
<Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">  
  <Encoding>  
    <H264Video>  
      <KeyFrameInterval>00:00:02</KeyFrameInterval>  
      <SceneChangeDetection>true</SceneChangeDetection>  
      <H264Layers>  
        <H264Layer>  
          <Bitrate>2200</Bitrate>  
          <Width>848</Width>  
          <Height>480</Height>  
          <FrameRate>0/1</FrameRate>  
          <Profile>Auto</Profile>  
          <Level>auto</Level>  
          <BFrames>3</BFrames>  
          <ReferenceFrames>3</ReferenceFrames>  
          <Slices>0</Slices>  
          <AdaptiveBFrame>true</AdaptiveBFrame>  
          <EntropyMode>Cabac</EntropyMode>  
          <BufferWindow>00:00:05</BufferWindow>  
          <MaxBitrate>2200</MaxBitrate>  
        </H264Layer>  
      </H264Layers>  
      <Chapters />  
    </H264Video>  
    <AACAudio>  
      <Profile>AACLC</Profile>  
      <Channels>2</Channels>  
      <SamplingRate>48000</SamplingRate>  
      <Bitrate>128</Bitrate>  
    </AACAudio>  
  </Encoding>  
  <Outputs>  
    <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">  
      <MP4Format />  
    </Output>  
  </Outputs>  
</Preset>  
```  
  
 <span data-ttu-id="2fea4-114">JSON</span><span class="sxs-lookup"><span data-stu-id="2fea4-114">JSON</span></span>  
  
```  
{  
  "Version": 1.0,  
  "Codecs": [  
    {  
      "KeyFrameInterval": "00:00:02",  
      "SceneChangeDetection": true,  
      "H264Layers": [  
        {  
          "Profile": "Auto",  
          "Level": "auto",  
          "Bitrate": 2200,  
          "MaxBitrate": 2200,  
          "BufferWindow": "00:00:05",  
          "Width": 848,  
          "Height": 480,  
          "BFrames": 3,  
          "ReferenceFrames": 3,  
          "AdaptiveBFrame": true,  
          "Type": "H264Layer",  
          "FrameRate": "0/1"  
        }  
      ],  
      "Type": "H264Video"  
    },  
    {  
      "Profile": "AACLC",  
      "Channels": 2,  
      "SamplingRate": 48000,  
      "Bitrate": 128,  
      "Type": "AACAudio"  
    }  
  ],  
  "Outputs": [  
    {  
      "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",  
      "Format": {  
        "Type": "MP4Format"  
      }  
    }  
  ]  
}  
```
