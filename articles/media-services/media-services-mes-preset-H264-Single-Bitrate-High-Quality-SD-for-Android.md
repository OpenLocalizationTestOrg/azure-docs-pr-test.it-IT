---
title: "Codec video H.264 a bitrate singolo con risoluzione SD di alta qualità per Android | Microsoft Docs"
description: "Questo argomento fornisce una panoramica del set di impostazioni delle attività **Codec video H.264 a bitrate singolo con risoluzione SD di alta qualità per Android**."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 4a190f24-ec6a-47e7-8bca-6294e064b15b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 325078dd188556daaf4092909a174d97a2e01e1a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="h264-single-bitrate-high-quality-sd-for-android"></a><span data-ttu-id="06e1a-103">Codec video H.264 a bitrate singolo con risoluzione SD di alta qualità per Android</span><span class="sxs-lookup"><span data-stu-id="06e1a-103">H264 Single Bitrate High Quality SD for Android</span></span>
<span data-ttu-id="06e1a-104">`Media Encoder Standard` definisce un set di impostazioni di codifica che è possibile usare per la creazione di processi di codifica.</span><span class="sxs-lookup"><span data-stu-id="06e1a-104">`Media Encoder Standard` defines a set of encoding presets you can use when creating encoding jobs.</span></span> <span data-ttu-id="06e1a-105">È possibile usare un `preset name` per specificare il formato in cui codificare il file multimediale</span><span class="sxs-lookup"><span data-stu-id="06e1a-105">You can either use a `preset name` to specify into which format you would like to encode your media file.</span></span> <span data-ttu-id="06e1a-106">oppure creare set di impostazioni basati su JSON o XML personalizzati, con codifica UTF-8 o UTF-16.</span><span class="sxs-lookup"><span data-stu-id="06e1a-106">Or, you can create your own JSON or XML-based presets (using UTF-8 or UTF-16 encoding.</span></span> <span data-ttu-id="06e1a-107">Dopodiché, occorre trasmettere il set di impostazioni personalizzato al codificatore.</span><span class="sxs-lookup"><span data-stu-id="06e1a-107">You would then pass the custom preset to the encoder.</span></span> <span data-ttu-id="06e1a-108">Per un elenco di tutti i nomi dei set di impostazioni supportati dal codificatore `Media Encoder Standard`, vedere [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md) (Set di impostazioni di attività per Media Encoder Standard).</span><span class="sxs-lookup"><span data-stu-id="06e1a-108">For the list of all the preset names supported by this `Media Encoder Standard` encoder, see [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span></span>  
  
 <span data-ttu-id="06e1a-109">Questo argomento illustra il set di impostazioni `H264 Single Bitrate High Quality SD for Android` nei formati XML e JSON.</span><span class="sxs-lookup"><span data-stu-id="06e1a-109">This topic shows the `H264 Single Bitrate High Quality SD for Android` preset in XML and JSON format.</span></span>  
  
 <span data-ttu-id="06e1a-110">Questo set di impostazioni genera un file MP4 con una velocità in bit di 500 kbps e audio AAC stereo.</span><span class="sxs-lookup"><span data-stu-id="06e1a-110">This preset produces a single MP4 file with a bitrate of 500 kbps, and stereo AAC audio.</span></span> <span data-ttu-id="06e1a-111">Per informazioni dettagliate su profilo, velocità in bit, frequenza di campionamento e così via di questo set di impostazioni, esaminare il codice XML o JSON definito di seguito.</span><span class="sxs-lookup"><span data-stu-id="06e1a-111">For detailed information about profile, bitrate, sampling rate, etc. of this preset, examine the XML or JSON defined below.</span></span> <span data-ttu-id="06e1a-112">Per informazioni sul significato di ogni elemento in questi set di impostazioni e sui valori possibili per ciascuno, vedere lo [schema di Media Encoder Standard](media-services-mes-schema.md).</span><span class="sxs-lookup"><span data-stu-id="06e1a-112">For explanations of what each element in these presets means, and the valid values for each element, see the [Media Encoder Standard schema](media-services-mes-schema.md) topic.</span></span>  
  
 <span data-ttu-id="06e1a-113">XML</span><span class="sxs-lookup"><span data-stu-id="06e1a-113">XML</span></span>  
  
```  
<?xml version="1.0" encoding="utf-16"?>  
<Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">  
  <Encoding>  
    <H264Video>  
      <KeyFrameInterval>00:00:05</KeyFrameInterval>  
      <SceneChangeDetection>true</SceneChangeDetection>  
      <H264Layers>  
        <H264Layer>  
          <Bitrate>500</Bitrate>  
          <Width>480</Width>  
          <Height>360</Height>  
          <FrameRate>0/1</FrameRate>  
          <Profile>Baseline</Profile>  
          <Level>3</Level>  
          <BFrames>0</BFrames>  
          <ReferenceFrames>3</ReferenceFrames>  
          <Slices>0</Slices>  
          <AdaptiveBFrame>false</AdaptiveBFrame>  
          <EntropyMode>Cavlc</EntropyMode>  
          <BufferWindow>00:00:05</BufferWindow>  
          <MaxBitrate>500</MaxBitrate>  
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
  
 <span data-ttu-id="06e1a-114">JSON</span><span class="sxs-lookup"><span data-stu-id="06e1a-114">JSON</span></span>  
  
```  
{  
  "Version": 1.0,  
  "Codecs": [  
    {  
      "KeyFrameInterval": "00:00:05",  
      "SceneChangeDetection": true,  
      "H264Layers": [  
        {  
          "Profile": "Baseline",  
          "Level": "3",  
          "Bitrate": 500,  
          "MaxBitrate": 500,  
          "BufferWindow": "00:00:05",  
          "Width": 480,  
          "Height": 360,  
          "ReferenceFrames": 3,  
          "EntropyMode": "Cavlc",  
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
