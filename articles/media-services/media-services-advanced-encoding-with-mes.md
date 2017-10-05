---
title: "Eseguire attività di codifica avanzata personalizzando i set di impostazioni di Media Encoder Standard | Documentazione Microsoft"
description: "Questo argomento illustra come eseguire la codifica avanzata personalizzando i set di impostazioni delle attività di Media Encoder Standard."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 2a4ade25-e600-4bce-a66e-e29cf4a38369
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: juliako
ms.openlocfilehash: 8de3bdd45261c84a0e1bb90f1c58863ad740dd5a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="perform-advanced-encoding-by-customizing-mes-presets"></a><span data-ttu-id="a418b-103">Eseguire attività di codifica avanzata personalizzando i set di impostazioni di Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="a418b-103">Perform advanced encoding by customizing MES presets</span></span> 

## <a name="overview"></a><span data-ttu-id="a418b-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="a418b-104">Overview</span></span>

<span data-ttu-id="a418b-105">Questo argomento descrive come personalizzare i set d impostazioni di Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="a418b-105">This topic shows how to customize Media Encoder Standard presets.</span></span> <span data-ttu-id="a418b-106">L'argomento [Codifica avanzata con Media Encoder Standard](media-services-custom-mes-presets-with-dotnet.md) mostra come usare .NET per creare un'attività di codifica e un processo per l'esecuzione di tale attività.</span><span class="sxs-lookup"><span data-stu-id="a418b-106">The [Encoding with Media Encoder Standard using custom presets](media-services-custom-mes-presets-with-dotnet.md) topic shows how to use .NET to create an encoding task and a job that executes this task.</span></span> <span data-ttu-id="a418b-107">Dopo aver personalizzato un set di impostazioni, fornire tali impostazioni all'attività di codifica.</span><span class="sxs-lookup"><span data-stu-id="a418b-107">Once you customize a preset, supply the custom presets to the encoding task.</span></span> 

>[!NOTE]
><span data-ttu-id="a418b-108">Se si usa un set di impostazioni XML, assicurarsi di mantenere l'ordine degli elementi, come illustrato negli esempi XML seguenti (KeyFrameInterval, ad esempio, deve precedere SceneChangeDetection).</span><span class="sxs-lookup"><span data-stu-id="a418b-108">If using an XML preset, make sure to preserve the order of elements, as shown in XML samples below (for example, KeyFrameInterval should precede SceneChangeDetection).</span></span>
>

<span data-ttu-id="a418b-109">In questo argomento vengono illustrati i set di impostazioni personalizzati che eseguono le attività di codifica seguenti.</span><span class="sxs-lookup"><span data-stu-id="a418b-109">In this topic, the custom presets that perform the following encoding tasks are demonstrated.</span></span>

## <a name="support-for-relative-sizes"></a><span data-ttu-id="a418b-110">Supporto per le dimensioni relative</span><span class="sxs-lookup"><span data-stu-id="a418b-110">Support for relative sizes</span></span>

<span data-ttu-id="a418b-111">Quando si generano anteprime, non è sempre necessario specificare la larghezza e l'altezza dell'output in pixel.</span><span class="sxs-lookup"><span data-stu-id="a418b-111">When generating thumbnails, you do not need to always specify output width and height in pixels.</span></span> <span data-ttu-id="a418b-112">È possibile specificare questi valori sotto forma di percentuali nell'intervallo [1%, …, 100%].</span><span class="sxs-lookup"><span data-stu-id="a418b-112">You can specify them in percentages, in the range [1%, …, 100%].</span></span>

### <a name="json-preset"></a><span data-ttu-id="a418b-113">Set di impostazioni JSON</span><span class="sxs-lookup"><span data-stu-id="a418b-113">JSON preset</span></span>
    "Width": "100%",
    "Height": "100%"

### <a name="xml-preset"></a><span data-ttu-id="a418b-114">Set di impostazioni XML</span><span class="sxs-lookup"><span data-stu-id="a418b-114">XML preset</span></span>
    <Width>100%</Width>
    <Height>100%</Height>

## <span data-ttu-id="a418b-115"><a id="thumbnails"></a>Generare anteprime</span><span class="sxs-lookup"><span data-stu-id="a418b-115"><a id="thumbnails"></a>Generate thumbnails</span></span>

<span data-ttu-id="a418b-116">Questa sezione illustra come personalizzare un set di impostazioni che genera anteprime.</span><span class="sxs-lookup"><span data-stu-id="a418b-116">This section shows how to customize a preset that generates thumbnails.</span></span> <span data-ttu-id="a418b-117">Il set di impostazioni definito di seguito contiene informazioni su come codificare il file, nonché le informazioni necessarie per generare le anteprime.</span><span class="sxs-lookup"><span data-stu-id="a418b-117">The preset defined below contains information on how you want to encode your file as well as information needed to generate thumbnails.</span></span> <span data-ttu-id="a418b-118">È possibile usare uno dei set di impostazioni per Media Encoder Standard documentati in [questa](media-services-mes-presets-overview.md) sezione e aggiungere il codice che genera le anteprime.</span><span class="sxs-lookup"><span data-stu-id="a418b-118">You can take any of the MES presets documented [this](media-services-mes-presets-overview.md) section and add code that generates thumbnails.</span></span>  

> [!NOTE]
> <span data-ttu-id="a418b-119">L'impostazione **SceneChangeDetection** nell'impostazione predefinita seguente può essere impostata a true solo in caso di codifica in un video a velocità in bit singola.</span><span class="sxs-lookup"><span data-stu-id="a418b-119">The **SceneChangeDetection** setting in the following preset can only be set to true if you are encoding to a single  bitrate video.</span></span> <span data-ttu-id="a418b-120">In caso di codifica in video a bitrate multipli e impostazione di **SceneChangeDetection** su true, il codificatore restituisce un errore.</span><span class="sxs-lookup"><span data-stu-id="a418b-120">If you are encoding to a multi-bitrate video and set **SceneChangeDetection** to true, the encoder returns an error.</span></span>  
>
>

<span data-ttu-id="a418b-121">Per informazioni sullo schema, vedere [questo](media-services-mes-schema.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="a418b-121">For information about schema, see [this](media-services-mes-schema.md) topic.</span></span>

<span data-ttu-id="a418b-122">Assicurarsi di esaminare la sezione [Considerazioni](#considerations) .</span><span class="sxs-lookup"><span data-stu-id="a418b-122">Make sure to review the [Considerations](#considerations) section.</span></span>

### <span data-ttu-id="a418b-123"><a id="json"></a>Set di impostazioni JSON</span><span class="sxs-lookup"><span data-stu-id="a418b-123"><a id="json"></a>JSON preset</span></span>
    {
      "Version": 1.0,
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": "true",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 4500,
              "MaxBitrate": 4500,
              "BufferWindow": "00:00:05",
              "Width": 1280,
              "Height": 720,
              "ReferenceFrames": 3,
              "EntropyMode": "Cabac",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"

            }
          ],
          "Type": "H264Video"
        },
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "{Best}",
          "Type": "JpgImage"
        },
        {
          "PngLayers": [
            {
              "Type": "PngLayer",
              "Width": 640,
              "Height": 360,
            }
          ],
          "Start": "00:00:01",
          "Step": "00:00:10",
          "Range": "00:00:58",
          "Type": "PngImage"
        },
        {
          "BmpLayers": [
            {
              "Type": "BmpLayer",
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "10%",
          "Step": "10%",
          "Range": "90%",
          "Type": "BmpImage"
        },
        {
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        },
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "PngFormat"
          }
        },
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "BmpFormat"
          }
        },
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <span data-ttu-id="a418b-124"><a id="xml"></a>Set di impostazioni XML</span><span class="sxs-lookup"><span data-stu-id="a418b-124"><a id="xml"></a>XML preset</span></span>
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <SceneChangeDetection>true</SceneChangeDetection>
          <H264Layers>
            <H264Layer>
              <Bitrate>4500</Bitrate>
              <Width>1280</Width>
              <Height>720</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>4500</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
        <JpgImage Start="{Best}">
          <JpgLayers>
            <JpgLayer>
              <Width>640</Width>
              <Height>360</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
        <BmpImage Start="10%" Step="10%" Range="90%">
          <BmpLayers>
            <BmpLayer>
              <Width>640</Width>
              <Height>360</Height>
            </BmpLayer>
          </BmpLayers>
        </BmpImage>
        <PngImage Start="00:00:01" Step="00:00:10" Range="00:00:58">
          <PngLayers>
            <PngLayer>
              <Width>640</Width>
              <Height>360</Height>
            </PngLayer>
          </PngLayers>
        </PngImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <BmpFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <PngFormat />
        </Output>
      </Outputs>
    </Preset>

### <a name="considerations"></a><span data-ttu-id="a418b-125">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="a418b-125">Considerations</span></span>

<span data-ttu-id="a418b-126">Si applicano le considerazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a418b-126">The following considerations apply:</span></span>

* <span data-ttu-id="a418b-127">L'utilizzo di timestamp espliciti per Inizio/Passaggio/Intervallo presuppone che l'origine dell'input duri almeno 1 minuto.</span><span class="sxs-lookup"><span data-stu-id="a418b-127">The use of explicit timestamps for Start/Step/Range assumes that the input source is at least 1 minute long.</span></span>
* <span data-ttu-id="a418b-128">Gli elementi Jpg/Png/BmpImage hanno gli attributi inizio, passaggio e intervallo della stringa, che possono essere interpretati come:</span><span class="sxs-lookup"><span data-stu-id="a418b-128">Jpg/Png/BmpImage elements have Start, Step, and Range string attributes – these can be interpreted as:</span></span>

  * <span data-ttu-id="a418b-129">Se sono numeri interi non negativi, numero di frame, ad esempio "Start": "120",</span><span class="sxs-lookup"><span data-stu-id="a418b-129">Frame Number if they are non-negative integers, for example "Start": "120",</span></span>
  * <span data-ttu-id="a418b-130">Relativi alla durata di origine se espressi con il suffisso %, ad esempio "Start": "15%", OR</span><span class="sxs-lookup"><span data-stu-id="a418b-130">Relative to source duration if expressed as %-suffixed, for example "Start": "15%", OR</span></span>
  * <span data-ttu-id="a418b-131">Timestamp se espresso come HH:MM:SS</span><span class="sxs-lookup"><span data-stu-id="a418b-131">Timestamp if expressed as HH:MM:SS…</span></span> <span data-ttu-id="a418b-132">come formato, ad esempio "Start": "00:01:00"</span><span class="sxs-lookup"><span data-stu-id="a418b-132">format, for example "Start" : "00:01:00"</span></span>

    <span data-ttu-id="a418b-133">È possibile combinare e associare le notazioni a piacimento.</span><span class="sxs-lookup"><span data-stu-id="a418b-133">You can mix and match notations as you please.</span></span>

    <span data-ttu-id="a418b-134">Inoltre, Inizio supporta anche una Macro speciale: {Best}, che tenta di determinare il primo fotogramma "interessante" della NOTA contenuto: (Passaggio e Intervallo vengono ignorati quando Inizio è impostato su {Best})</span><span class="sxs-lookup"><span data-stu-id="a418b-134">Additionally, Start also supports a special Macro:{Best}, which attempts to determine the first “interesting” frame of the content NOTE: (Step and Range are ignored when Start is set to {Best})</span></span>
  * <span data-ttu-id="a418b-135">Impostazioni predefinite: Start: {Best}</span><span class="sxs-lookup"><span data-stu-id="a418b-135">Defaults: Start:{Best}</span></span>
* <span data-ttu-id="a418b-136">Il formato di output deve essere specificato in modo esplicito per ogni formato immagine: Jpg/Png/BmpFormat.</span><span class="sxs-lookup"><span data-stu-id="a418b-136">Output format needs to be explicitly provided for each Image format: Jpg/Png/BmpFormat.</span></span> <span data-ttu-id="a418b-137">Quando è presente, MES collega JpgVideo a JpgFormat e così via.</span><span class="sxs-lookup"><span data-stu-id="a418b-137">When present, MES matches JpgVideo to JpgFormat and so on.</span></span> <span data-ttu-id="a418b-138">OutputFormat presenta una nuova Macro specifica di codec di immagine : {Index}, che deve essere presente (una volta e una sola volta) per i formati immagine.</span><span class="sxs-lookup"><span data-stu-id="a418b-138">OutputFormat introduces a new image-codec specific Macro: {Index}, which needs to be present (once and only once) for image output formats.</span></span>

## <span data-ttu-id="a418b-139"><a id="trim_video"></a>Tagliare un video (ritaglio)</span><span class="sxs-lookup"><span data-stu-id="a418b-139"><a id="trim_video"></a>Trim a video (clipping)</span></span>
<span data-ttu-id="a418b-140">Questa sezione descrive la modifica di set di impostazioni del codificatore per tagliare o ritagliare il video di input quando l'input è un file in formato intermedio o su richiesta.</span><span class="sxs-lookup"><span data-stu-id="a418b-140">This section talks about modifying the encoder presets to clip or trim the input video where the input is a so-called mezzanine file or on-demand file.</span></span> <span data-ttu-id="a418b-141">Il codificatore può anche essere usato per tagliare o ritagliare un asset acquisito o archiviato da un flusso in tempo reale. Per i relativi dettagli, vedere [questo blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="a418b-141">The encoder can also be used to clip or trim an asset, which is captured or archived from a live stream – the details for this are available in [this blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).</span></span>

<span data-ttu-id="a418b-142">Per tagliare i video, è possibile eseguire uno dei set di impostazioni di Media Encoder Standard documentati in [questa](media-services-mes-presets-overview.md) sezione e modificare l'elemento **Sources** (come illustrato di seguito).</span><span class="sxs-lookup"><span data-stu-id="a418b-142">To trim your videos, you can take any of the MES presets documented [this](media-services-mes-presets-overview.md) section and modify the **Sources** element (as shown below).</span></span> <span data-ttu-id="a418b-143">Il valore di StartTime deve corrispondere ai timestamp assoluti del video di input.</span><span class="sxs-lookup"><span data-stu-id="a418b-143">The value of StartTime needs to match the absolute timestamps of the input video.</span></span> <span data-ttu-id="a418b-144">Ad esempio, se il primo fotogramma del video di input ha un timestamp di 12:00:10.000, il valore di StartTime deve essere di almeno 12:00:10.000 o superiore.</span><span class="sxs-lookup"><span data-stu-id="a418b-144">For example, if the first frame of the input video has a timestamp of 12:00:10.000, then StartTime should be at least 12:00:10.000 and greater.</span></span> <span data-ttu-id="a418b-145">Nell'esempio seguente, si presuppone che il video di input abbia un timestamp iniziale pari a zero.</span><span class="sxs-lookup"><span data-stu-id="a418b-145">In the example below, we assume that the input video has a starting timestamp of zero.</span></span> <span data-ttu-id="a418b-146">**Sources** deve essere posizionato all'inizio del set di impostazioni.</span><span class="sxs-lookup"><span data-stu-id="a418b-146">**Sources** should be placed at the beginning of the preset.</span></span>

### <span data-ttu-id="a418b-147"><a id="json"></a>Set di impostazioni JSON</span><span class="sxs-lookup"><span data-stu-id="a418b-147"><a id="json"></a>JSON preset</span></span>
    {
      "Version": 1.0,
      "Sources": [
        {
          "StartTime": "00:00:04",
          "Duration": "00:00:16"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 3400,
              "MaxBitrate": 3400,
              "BufferWindow": "00:00:05",
              "Width": 1280,
              "Height": 720,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 2250,
              "MaxBitrate": 2250,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1500,
              "MaxBitrate": 1500,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1000,
              "MaxBitrate": 1000,
              "BufferWindow": "00:00:05",
              "Width": 640,
              "Height": 360,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 650,
              "MaxBitrate": 650,
              "BufferWindow": "00:00:05",
              "Width": 640,
              "Height": 360,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 400,
              "MaxBitrate": 400,
              "BufferWindow": "00:00:05",
              "Width": 320,
              "Height": 180,
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

### <a name="xml-preset"></a><span data-ttu-id="a418b-148">Set di impostazioni XML</span><span class="sxs-lookup"><span data-stu-id="a418b-148">XML preset</span></span>
<span data-ttu-id="a418b-149">Per tagliare i video, è possibile eseguire un’impostazione predefinita MES documentata [qui](media-services-mes-presets-overview.md) e modificare l'elemento **Sources** (come illustrato di seguito).</span><span class="sxs-lookup"><span data-stu-id="a418b-149">To trim your videos, you can take any of the MES presets documented [here](media-services-mes-presets-overview.md) and modify the **Sources** element (as shown below).</span></span>

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source StartTime="PT4S" Duration="PT14S"/>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>3400</Bitrate>
              <Width>1280</Width>
              <Height>720</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>3400</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>2250</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>2250</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1500</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1500</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1000</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1000</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>650</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>650</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>400</Bitrate>
              <Width>320</Width>
              <Height>180</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>400</MaxBitrate>
            </H264Layer>
          </H264Layers>
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

## <span data-ttu-id="a418b-150"><a id="overlay"></a>Creare una sovrimpressione</span><span class="sxs-lookup"><span data-stu-id="a418b-150"><a id="overlay"></a>Create an overlay</span></span>

<span data-ttu-id="a418b-151">Il Media Encoder Standard consente di sovrapporre un'immagine a un video esistente.</span><span class="sxs-lookup"><span data-stu-id="a418b-151">The Media Encoder Standard allows you to overlay an image onto an existing video.</span></span> <span data-ttu-id="a418b-152">Attualmente, sono supportati i seguenti formati: png, jpg, gif e bmp.</span><span class="sxs-lookup"><span data-stu-id="a418b-152">Currently, the following formats are supported: png, jpg, gif, and bmp.</span></span> <span data-ttu-id="a418b-153">Il set di impostazioni definito di seguito è un esempio di base di una sovrimpressione video.</span><span class="sxs-lookup"><span data-stu-id="a418b-153">The preset defined below is a basic example  of a video overlay.</span></span>

<span data-ttu-id="a418b-154">Oltre a definire un file del set di impostazioni, è anche necessario indicare a Servizi multimediali quale file dell'asset corrisponde all'immagine da sovrapporre e quale file contiene il video di origine sul quale sovrapporre l'immagine.</span><span class="sxs-lookup"><span data-stu-id="a418b-154">In addition to defining a preset file, you also have to let Media Services know which file in the asset is the overlay image and which file is the source video onto which you want to overlay the image.</span></span> <span data-ttu-id="a418b-155">Il file video deve essere il file **primario** .</span><span class="sxs-lookup"><span data-stu-id="a418b-155">The video file has to be the **primary** file.</span></span>

<span data-ttu-id="a418b-156">Se si usa .NET, aggiungere le due funzioni seguenti all'esempio .NET definito in [questo](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) argomento.</span><span class="sxs-lookup"><span data-stu-id="a418b-156">If you are using .NET, add the following two functions to the .NET example defined in [this](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) topic.</span></span> <span data-ttu-id="a418b-157">La funzione **UploadMediaFilesFromFolder** carica i file, ad esempio BigBuckBunny.mp4 e Image001.png, da una cartella e imposta il file con estensione mp4 come file primario dell'asset.</span><span class="sxs-lookup"><span data-stu-id="a418b-157">The **UploadMediaFilesFromFolder** function uploads files from a folder (for example, BigBuckBunny.mp4 and Image001.png) and sets the mp4 file to be the primary file in the asset.</span></span> <span data-ttu-id="a418b-158">La funzione **EncodeWithOverlay** usa il file di set di impostazioni personalizzato passato alla funzione stessa, ad esempio il set di impostazioni seguente, per creare l'attività di codifica.</span><span class="sxs-lookup"><span data-stu-id="a418b-158">The **EncodeWithOverlay** function uses the custom preset file that was passed to it (for example, the preset that follows) to create the encoding task.</span></span>


    static public IAsset UploadMediaFilesFromFolder(string folderPath)
    {
        IAsset asset = _context.Assets.CreateFromFolder(folderPath, AssetCreationOptions.None);
    
        foreach (var af in asset.AssetFiles)
        {
            // The following code assumes 
            // you have an input folder with one MP4 and one overlay image file.
            if (af.Name.Contains(".mp4"))
                af.IsPrimary = true;
            else
                af.IsPrimary = false;
    
            af.Update();
        }
    
        return asset;
    }

    static public IAsset EncodeWithOverlay(IAsset assetSource, string customPresetFileName)
    {
        // Declare a new job.
        IJob job = _context.Jobs.Create("Media Encoder Standard Job");
        // Get a media processor reference, and pass to it the name of the 
        // processor to use for the specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Load the XML (or JSON) from the local file.
        string configuration = File.ReadAllText(customPresetFileName);

        // Create a task
        ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            configuration,
            TaskOptions.None);

        // Specify the input assets to be encoded.
        // This asset contains a source file and an overlay file.
        task.InputAssets.Add(assetSource);

        // Add an output asset to contain the results of the job. 
        task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.None);

        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
        job.Submit();
        job.GetExecutionProgressTask(CancellationToken.None).Wait();

        return job.OutputMediaAssets[0];
    }


> [!NOTE]
> <span data-ttu-id="a418b-159">Limitazioni correnti:</span><span class="sxs-lookup"><span data-stu-id="a418b-159">Current limitations:</span></span>
>
> <span data-ttu-id="a418b-160">L'impostazione di opacità della sovrimpressione non è supportata.</span><span class="sxs-lookup"><span data-stu-id="a418b-160">The overlay opacity setting is not supported.</span></span>
>
> <span data-ttu-id="a418b-161">Il file video di origine e il file dell'immagine sovrapposta devono essere nello stesso asset e il file video deve essere impostato come file primario nell'asset.</span><span class="sxs-lookup"><span data-stu-id="a418b-161">Your source video file and the overlay image file have to be in the same asset, and the video file needs to be set as the primary file in this asset.</span></span>
>
>

### <a name="json-preset"></a><span data-ttu-id="a418b-162">Set di impostazioni JSON</span><span class="sxs-lookup"><span data-stu-id="a418b-162">JSON preset</span></span>
    {
      "Version": 1.0,
      "Sources": [
        {
          "Streams": [],
          "Filters": {
            "VideoOverlay": {
              "Position": {
                "X": 100,
                "Y": 100,
                "Width": 100,
                "Height": 50
              },
              "AudioGainLevel": 0.0,
              "MediaParams": [
                {
                  "OverlayLoopCount": 1
                },
                {
                  "IsOverlay": true,
                  "OverlayLoopCount": 1,
                  "InputLoop": true
                }
              ],
              "Source": "Image001.png",
              "Clip": {
                "Duration": "00:00:05"
              },
              "FadeInDuration": {
                "Duration": "00:00:01"
              },
              "FadeOutDuration": {
                "StartTime": "00:00:03",
                "Duration": "00:00:04"
              }
            }
          },
          "Pad": true
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1045,
              "MaxBitrate": 1045,
              "BufferWindow": "00:00:05",
              "ReferenceFrames": 3,
              "EntropyMode": "Cavlc",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Type": "CopyAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}{Extension}",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <a name="xml-preset"></a><span data-ttu-id="a418b-163">Set di impostazioni XML</span><span class="sxs-lookup"><span data-stu-id="a418b-163">XML preset</span></span>
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source>
          <Streams />
          <Filters>
            <VideoOverlay>
              <Source>Image001.png</Source>
              <Clip Duration="PT5S" />
              <FadeInDuration Duration="PT1S" />
              <FadeOutDuration StartTime="PT3S" Duration="PT4S" />
              <Position X="100" Y="100" Width="100" Height="50" />
              <Opacity>0</Opacity>
              <AudioGainLevel>0</AudioGainLevel>
              <MediaParams>
                <MediaParam>
                  <IsOverlay>false</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>false</InputLoop>
                </MediaParam>
                <MediaParam>
                  <IsOverlay>true</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>true</InputLoop>
                </MediaParam>
              </MediaParams>
            </VideoOverlay>
          </Filters>
          <Pad>true</Pad>
        </Source>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>1045</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>0</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cavlc</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1045</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <CopyAudio />
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}{Extension}">
          <MP4Format />
        </Output>
      </Outputs>
    </Preset>


## <span data-ttu-id="a418b-164"><a id="silent_audio"></a>Inserire una traccia audio silenziosa quando l'input è privo di audio</span><span class="sxs-lookup"><span data-stu-id="a418b-164"><a id="silent_audio"></a>Insert a silent audio track when input has no audio</span></span>
<span data-ttu-id="a418b-165">Per impostazione predefinita, se si invia al codificatore un input che contiene solo video e nessun audio, l'asset di output contiene file di soli dati video.</span><span class="sxs-lookup"><span data-stu-id="a418b-165">By default, if you send an input to the encoder that contains only video, and no audio, then the output asset contains files that contain only video data.</span></span> <span data-ttu-id="a418b-166">Alcuni lettori non possono gestire flussi di output di questo tipo.</span><span class="sxs-lookup"><span data-stu-id="a418b-166">Some players may not be able to handle such output streams.</span></span> <span data-ttu-id="a418b-167">In tal caso, è possibile usare questa impostazione per forzare l'aggiunta di una traccia audio silenziosa all'output da parte del codificatore.</span><span class="sxs-lookup"><span data-stu-id="a418b-167">You can use this setting to force the encoder to add a silent audio track to the output in that scenario.</span></span>

<span data-ttu-id="a418b-168">Per forzare la generazione di un asset contenente una traccia audio silenziosa da parte del codificatore quando l'input è privo di audio, specificare il valore "InsertSilenceIfNoAudio".</span><span class="sxs-lookup"><span data-stu-id="a418b-168">To force the encoder to produce an asset that contains a silent audio track when input has no audio, specify the "InsertSilenceIfNoAudio" value.</span></span>

<span data-ttu-id="a418b-169">È possibile usare uno dei set di impostazioni di Media Encoder Standard documentati in [questa](media-services-mes-presets-overview.md) sezione e apportare la modifica seguente:</span><span class="sxs-lookup"><span data-stu-id="a418b-169">You can take any of the MES presets documented in [this](media-services-mes-presets-overview.md) section, and make the following modification:</span></span>

### <a name="json-preset"></a><span data-ttu-id="a418b-170">Set di impostazioni JSON</span><span class="sxs-lookup"><span data-stu-id="a418b-170">JSON preset</span></span>
    {
      "Channels": 2,
      "SamplingRate": 44100,
      "Bitrate": 96,
      "Type": "AACAudio",
      "Condition": "InsertSilenceIfNoAudio"
    }

### <a name="xml-preset"></a><span data-ttu-id="a418b-171">Set di impostazioni XML</span><span class="sxs-lookup"><span data-stu-id="a418b-171">XML preset</span></span>
    <AACAudio Condition="InsertSilenceIfNoAudio">
      <Channels>2</Channels>
      <SamplingRate>44100</SamplingRate>
      <Bitrate>96</Bitrate>
    </AACAudio>

## <span data-ttu-id="a418b-172"><a id="deinterlacing"></a>Disabilitare il deinterlacciamento automatico</span><span class="sxs-lookup"><span data-stu-id="a418b-172"><a id="deinterlacing"></a>Disable auto de-interlacing</span></span>
<span data-ttu-id="a418b-173">I clienti non devono eseguire alcuna operazione se desiderano che il contenuto interlacciato sia automaticamente deinterlacciato.</span><span class="sxs-lookup"><span data-stu-id="a418b-173">Customers don’t need to do anything if they like the interlace contents to be automatically de-interlaced.</span></span> <span data-ttu-id="a418b-174">Quando il deinterlacciamento automatico è attivato (impostazione predefinita) il MES rileva automaticamente i fotogrammi interlacciati e deinterlaccia solo i fotogrammi contrassegnati come interlacciati.</span><span class="sxs-lookup"><span data-stu-id="a418b-174">When the auto de-interlacing is on (default) the MES does the auto detection of interlaced frames and only de-interlaces frames marked as interlaced.</span></span>

<span data-ttu-id="a418b-175">È possibile disattivare il deinterlacciamento automatico.</span><span class="sxs-lookup"><span data-stu-id="a418b-175">You can turn the auto de-interlacing off.</span></span> <span data-ttu-id="a418b-176">Questa opzione non è consigliata.</span><span class="sxs-lookup"><span data-stu-id="a418b-176">This option is not recommended.</span></span>

### <a name="json-preset"></a><span data-ttu-id="a418b-177">Set di impostazioni JSON</span><span class="sxs-lookup"><span data-stu-id="a418b-177">JSON preset</span></span>
    "Sources": [
    {
     "Filters": {
        "Deinterlace": {
          "Mode": "Off"
        }
      },
    }
    ]

### <a name="xml-preset"></a><span data-ttu-id="a418b-178">Set di impostazioni XML</span><span class="sxs-lookup"><span data-stu-id="a418b-178">XML preset</span></span>
    <Sources>
    <Source>
      <Filters>
        <Deinterlace>
          <Mode>Off</Mode>
        </Deinterlace>
      </Filters>
    </Source>
    </Sources>


## <span data-ttu-id="a418b-179"><a id="audio_only"></a>Impostazioni predefinite solo audio</span><span class="sxs-lookup"><span data-stu-id="a418b-179"><a id="audio_only"></a>Audio-only presets</span></span>
<span data-ttu-id="a418b-180">In questa sezione vengono illustrate due impostazioni predefinite MES solo audio: Audio AAC e Audio AAC di buona qualità.</span><span class="sxs-lookup"><span data-stu-id="a418b-180">This section demonstrates two audio-only MES presets: AAC Audio and AAC Good Quality Audio.</span></span>

### <a name="aac-audio"></a><span data-ttu-id="a418b-181">Audio ACC</span><span class="sxs-lookup"><span data-stu-id="a418b-181">AAC Audio</span></span>
    {
      "Version": 1.0,
      "Codecs": [
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
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

### <a name="aac-good-quality-audio"></a><span data-ttu-id="a418b-182">Audio AAC di buona qualità</span><span class="sxs-lookup"><span data-stu-id="a418b-182">AAC Good Quality Audio</span></span>
    {
      "Version": 1.0,
      "Codecs": [
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 192,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <span data-ttu-id="a418b-183"><a id="concatenate"></a>Concatenare due o più file video</span><span class="sxs-lookup"><span data-stu-id="a418b-183"><a id="concatenate"></a>Concatenate two or more video files</span></span>

<span data-ttu-id="a418b-184">Nell'esempio seguente viene illustrato come generare un set di impostazioni per concatenare due o più file video.</span><span class="sxs-lookup"><span data-stu-id="a418b-184">The following example illustrates how you can generate a preset to concatenate two or more video files.</span></span> <span data-ttu-id="a418b-185">Lo scenario più comune è l'aggiunta di un'intestazione o una sequenza finale al video principale.</span><span class="sxs-lookup"><span data-stu-id="a418b-185">The most common scenario is when you want to add a header or a trailer to the main video.</span></span> <span data-ttu-id="a418b-186">L'uso previsto sono i file video modificati insieme che condividono proprietà: risoluzione video, frequenza dei fotogrammi, conteggio tracce audio e così via.</span><span class="sxs-lookup"><span data-stu-id="a418b-186">The intended use is when the video files being edited together share  properties (video resolution, frame rate, audio track count, etc.).</span></span> <span data-ttu-id="a418b-187">Prestare attenzione a non combinare video con frequenze dei fotogrammi diverse o con un numero diverso di tracce audio.</span><span class="sxs-lookup"><span data-stu-id="a418b-187">You should take care not to mix videos of different frame rates, or with different number of audio tracks.</span></span>

>[!NOTE]
><span data-ttu-id="a418b-188">La struttura corrente della funzionalità di concatenazione prevede che i clip video siano coerenti in termini di risoluzione, frequenza dei fotogrammi e così via.</span><span class="sxs-lookup"><span data-stu-id="a418b-188">The current design of the concatenation feature expects that the input video clips are consistent in terms of resolution, frame rate etc.</span></span> 

### <a name="requirements-and-considerations"></a><span data-ttu-id="a418b-189">Problemi e considerazioni</span><span class="sxs-lookup"><span data-stu-id="a418b-189">Requirements and considerations</span></span>

* <span data-ttu-id="a418b-190">I video di input devono contenere solo una traccia audio.</span><span class="sxs-lookup"><span data-stu-id="a418b-190">Input videos should only have one audio track.</span></span>
* <span data-ttu-id="a418b-191">Tutti i video di input devono avere la stessa frequenza dei fotogrammi.</span><span class="sxs-lookup"><span data-stu-id="a418b-191">Input videos should all have the same frame rate.</span></span>
* <span data-ttu-id="a418b-192">È necessario caricare i video in asset separati e impostare i video come file primario in ogni asset.</span><span class="sxs-lookup"><span data-stu-id="a418b-192">You must upload your videos into separate assets and set the videos as the primary file in each asset.</span></span>
* <span data-ttu-id="a418b-193">È necessario conoscere la durata dei video.</span><span class="sxs-lookup"><span data-stu-id="a418b-193">You need to know the duration of your videos.</span></span>
* <span data-ttu-id="a418b-194">Il seguente esempio di set di impostazioni presuppone che tutti i video di input inizino con un timestamp pari a zero.</span><span class="sxs-lookup"><span data-stu-id="a418b-194">The preset examples below assumes that all the input videos start with a timestamp of zero.</span></span> <span data-ttu-id="a418b-195">È necessario modificare i valori StartTime se i video hanno un timestamp iniziale diverso, come avviene in genere con gli archivi in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="a418b-195">You need to modify the StartTime values if the videos have different starting timestamp, as is typically the case with live archives.</span></span>
* <span data-ttu-id="a418b-196">Il set di impostazioni JSON fa riferimenti espliciti ai valori AssetID degli asset di input.</span><span class="sxs-lookup"><span data-stu-id="a418b-196">The JSON preset makes explicit references to the AssetID values of the input assets.</span></span>
* <span data-ttu-id="a418b-197">Il codice di esempio presuppone che il set di impostazioni JSON sia stato salvato in un file locale, ad esempio "C:\supportFiles\preset.json".</span><span class="sxs-lookup"><span data-stu-id="a418b-197">The sample code assumes that the JSON preset has been saved to a local file, such as "C:\supportFiles\preset.json".</span></span> <span data-ttu-id="a418b-198">Presuppone anche che siano stati creati due asset caricando due file video e che si conoscano i valori AssetID risultanti.</span><span class="sxs-lookup"><span data-stu-id="a418b-198">It also assumes that two assets have been created by uploading two video files, and that you know the resultant AssetID values.</span></span>
* <span data-ttu-id="a418b-199">Il frammento di codice e il set di impostazioni JSON mostrano un esempio di concatenazione di due file video.</span><span class="sxs-lookup"><span data-stu-id="a418b-199">The code snippet and JSON preset shows an example of concatenating two video files.</span></span> <span data-ttu-id="a418b-200">È possibile estendere la concatenazione a più di due video nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="a418b-200">You can extend it to more than two videos by:</span></span>

  1. <span data-ttu-id="a418b-201">Chiamando ripetutamente task.InputAssets.Add() per aggiungere più video in ordine.</span><span class="sxs-lookup"><span data-stu-id="a418b-201">Calling task.InputAssets.Add() repeatedly to add more videos, in order.</span></span>
  2. <span data-ttu-id="a418b-202">Effettuando le modifiche corrispondenti all'elemento "Sources" nel file JSON, aggiungendo altre voci nello stesso ordine.</span><span class="sxs-lookup"><span data-stu-id="a418b-202">Making corresponding edits to the "Sources" element in the JSON, by adding more entries, in the same order.</span></span>

### <a name="net-code"></a><span data-ttu-id="a418b-203">Codice .NET</span><span class="sxs-lookup"><span data-stu-id="a418b-203">.NET code</span></span>

    IAsset asset1 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:606db602-efd7-4436-97b4-c0b867ba195b").FirstOrDefault();
    IAsset asset2 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e").FirstOrDefault();

    // Declare a new job.
    IJob job = _context.Jobs.Create("Media Encoder Standard Job for Concatenating Videos");
    // Get a media processor reference, and pass to it the name of the
    // processor to use for the specific task.
    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

    // Load the XML (or JSON) from the local file.
    string configuration = File.ReadAllText(@"c:\supportFiles\preset.json");

    // Create a task
    ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
        processor,
        configuration,
        TaskOptions.None);

    // Specify the input videos to be concatenated (in order).
    task.InputAssets.Add(asset1);
    task.InputAssets.Add(asset2);
    // Add an output asset to contain the results of the job.
    // This output is specified as AssetCreationOptions.None, which
    // means the output asset is not encrypted.
    task.OutputAssets.AddNew("Output asset",
        AssetCreationOptions.None);

    job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
    job.Submit();
    job.GetExecutionProgressTask(CancellationToken.None).Wait();

### <a name="json-preset"></a><span data-ttu-id="a418b-204">Set di impostazioni JSON</span><span class="sxs-lookup"><span data-stu-id="a418b-204">JSON preset</span></span>

<span data-ttu-id="a418b-205">Aggiornare il set di impostazioni personalizzate con gli ID degli asset che si vuole concatenare e l'intervallo di tempo appropriato per ogni video.</span><span class="sxs-lookup"><span data-stu-id="a418b-205">Update your custom preset with ids of the assets that you want to concatenate, and with the appropriate time segment for each video.</span></span>

    {
      "Version": 1.0,
      "Sources": [
        {
          "AssetID": "606db602-efd7-4436-97b4-c0b867ba195b",
          "StartTime": "00:00:01",
          "Duration": "00:00:15"
        },
        {
          "AssetID": "a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e",
          "StartTime": "00:00:02",
          "Duration": "00:00:05"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": true,
          "H264Layers": [
            {
              "Level": "auto",
              "Bitrate": 1800,
              "MaxBitrate": 1800,
              "BufferWindow": "00:00:05",
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
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

## <span data-ttu-id="a418b-206"><a id="crop"></a>Ritagliare video con Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="a418b-206"><a id="crop"></a>Crop videos with Media Encoder Standard</span></span>
<span data-ttu-id="a418b-207">Vedere l'argomento [Ritagliare video con Media Encoder Standard](media-services-crop-video.md) .</span><span class="sxs-lookup"><span data-stu-id="a418b-207">See the [Crop videos with Media Encoder Standard](media-services-crop-video.md) topic.</span></span>

## <span data-ttu-id="a418b-208"><a id="no_video"></a>Inserire una traccia video quando l'input non ha video</span><span class="sxs-lookup"><span data-stu-id="a418b-208"><a id="no_video"></a>Insert a video track when input has no video</span></span>

<span data-ttu-id="a418b-209">Per impostazione predefinita, se si invia al codificatore un input che contiene solo audio e nessun video, l'asset di output contiene file di soli dati audio.</span><span class="sxs-lookup"><span data-stu-id="a418b-209">By default, if you send an input to the encoder that contains only audio, and no video, then the output asset contains files that contain only audio data.</span></span> <span data-ttu-id="a418b-210">Alcuni lettori, tra cui Azure Media Player (vedere [qui](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) potrebbero non essere in grado di gestire tali flussi.</span><span class="sxs-lookup"><span data-stu-id="a418b-210">Some players, including Azure Media Player (see [this](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) may not be able to handle such streams.</span></span> <span data-ttu-id="a418b-211">In tal caso, è possibile usare questa impostazione per forzare l'aggiunta di una traccia video monocromatica all'output da parte del codificatore.</span><span class="sxs-lookup"><span data-stu-id="a418b-211">You can use this setting to force the encoder to add a monochrome video track to the output in that scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="a418b-212">Forzando il codificatore a inserire una traccia video di output si accresce la dimensione dell'asset di output e perciò il costo sostenuto per l'attività di codifica.</span><span class="sxs-lookup"><span data-stu-id="a418b-212">Forcing the encoder to insert an output video track increases the size of the output Asset, and thereby the cost incurred for the encoding Task.</span></span> <span data-ttu-id="a418b-213">È necessario eseguire test per verificare che questo incremento abbia un impatto modesto sugli addebiti mensili.</span><span class="sxs-lookup"><span data-stu-id="a418b-213">You should run tests to verify that this resultant increase has only a modest impact on your monthly charges.</span></span>
>

### <a name="inserting-video-at-only-the-lowest-bitrate"></a><span data-ttu-id="a418b-214">Inserimento di video alla sola velocità in bit più bassa</span><span class="sxs-lookup"><span data-stu-id="a418b-214">Inserting video at only the lowest bitrate</span></span>

<span data-ttu-id="a418b-215">Si supponga di usare un'impostazione di codifica a bitrate multipli, ad esempio ["H264 bitrate multipli 720p"](media-services-mes-preset-h264-multiple-bitrate-720p.md) per codificare l'intero catalogo di input per lo streaming, che contiene una combinazione di file video e file di solo audio.</span><span class="sxs-lookup"><span data-stu-id="a418b-215">Suppose you are using a multiple bitrate encoding preset such as ["H264 Multiple Bitrate 720p"](media-services-mes-preset-h264-multiple-bitrate-720p.md) to encode your entire input catalog for streaming, which contains a mix of video files and audio-only files.</span></span> <span data-ttu-id="a418b-216">In questo scenario, quando l'input non ha video, è opportuno forzare il codificatore a inserire una traccia video monocromatica solo alla velocità in bit più bassa, anziché inserire il video a tutte le velocità in bit.</span><span class="sxs-lookup"><span data-stu-id="a418b-216">In this scenario, when the input has no video, you may want to force the encoder to insert a monochrome video track at just the lowest bitrate, as opposed to inserting video at every output bitrate.</span></span> <span data-ttu-id="a418b-217">A tale scopo è necessario usare il flag **InsertBlackIfNoVideoBottomLayerOnly**.</span><span class="sxs-lookup"><span data-stu-id="a418b-217">To achieve this, you need to use the **InsertBlackIfNoVideoBottomLayerOnly** flag.</span></span>

<span data-ttu-id="a418b-218">È possibile usare uno dei set di impostazioni di Media Encoder Standard documentati in [questa](media-services-mes-presets-overview.md) sezione e apportare la modifica seguente:</span><span class="sxs-lookup"><span data-stu-id="a418b-218">You can take any of the MES presets documented in [this](media-services-mes-presets-overview.md) section, and make the following modification:</span></span>

#### <a name="json-preset"></a><span data-ttu-id="a418b-219">Set di impostazioni JSON</span><span class="sxs-lookup"><span data-stu-id="a418b-219">JSON preset</span></span>
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideoBottomLayerOnly",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a><span data-ttu-id="a418b-220">Set di impostazioni XML</span><span class="sxs-lookup"><span data-stu-id="a418b-220">XML preset</span></span>

<span data-ttu-id="a418b-221">Se si usa XML, applicare Condition="InsertBlackIfNoVideoBottomLayerOnly" come attributo per l'elemento **H264Video** e Condition="InsertSilenceIfNoAudio" come attributo per l'elemento **AACAudio**.</span><span class="sxs-lookup"><span data-stu-id="a418b-221">When using XML, use Condition="InsertBlackIfNoVideoBottomLayerOnly" as an attribute to the **H264Video** element and  Condition="InsertSilenceIfNoAudio" as an attribute to **AACAudio**.</span></span>

```
. . .
<Encoding>
  <H264Video Condition="InsertBlackIfNoVideoBottomLayerOnly">
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <SceneChangeDetection>true</SceneChangeDetection>
    <StretchMode>AutoSize</StretchMode>
    <H264Layers>
      <H264Layer>
        . . .
      </H264Layer>
    </H264Layers>
    <Chapters />
  </H264Video>
  <AACAudio Condition="InsertSilenceIfNoAudio">
    <Profile>AACLC</Profile>
    <Channels>2</Channels>
    <SamplingRate>48000</SamplingRate>
    <Bitrate>128</Bitrate>
  </AACAudio>
</Encoding>
. . .
```

### <a name="inserting-video-at-all-output-bitrates"></a><span data-ttu-id="a418b-222">Inserimento di video a tutte le velocità in bit di output</span><span class="sxs-lookup"><span data-stu-id="a418b-222">Inserting video at all output bitrates</span></span>
<span data-ttu-id="a418b-223">Si supponga di usare un'impostazione di codifica a bitrate multipli, ad esempio ["H264 bitrate multipli 720p"](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) per codificare l'intero catalogo di input per lo streaming, che contiene una combinazione di file video e file di solo audio.</span><span class="sxs-lookup"><span data-stu-id="a418b-223">Suppose you are using a multiple bitrate encoding preset such as ["H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) to encode your entire input catalog for streaming, which contains a mix of video files and audio-only files.</span></span> <span data-ttu-id="a418b-224">In questo scenario, quando l'input non ha video, è opportuno forzare il codificatore a inserire una traccia video monocromatica a tutte le velocità in bit di output.</span><span class="sxs-lookup"><span data-stu-id="a418b-224">In this scenario, when the input has no video, you may want to force the encoder to insert a monochrome video track at all the output bitrates.</span></span> <span data-ttu-id="a418b-225">In questo modo gli asset di output saranno tutti omogenei rispetto al numero di tracce video e tracce audio.</span><span class="sxs-lookup"><span data-stu-id="a418b-225">This ensures that your output Assets are all homogenous with respect to number of video tracks and audio tracks.</span></span> <span data-ttu-id="a418b-226">A tale scopo è necessario specificare il flag "InsertBlackIfNoVideo".</span><span class="sxs-lookup"><span data-stu-id="a418b-226">To achieve this, you need to specify the "InsertBlackIfNoVideo" flag.</span></span>

<span data-ttu-id="a418b-227">È possibile usare uno dei set di impostazioni di Media Encoder Standard documentati in [questa](media-services-mes-presets-overview.md) sezione e apportare la modifica seguente:</span><span class="sxs-lookup"><span data-stu-id="a418b-227">You can take any of the MES presets documented in [this](media-services-mes-presets-overview.md) section, and make the following modification:</span></span>

#### <a name="json-preset"></a><span data-ttu-id="a418b-228">Set di impostazioni JSON</span><span class="sxs-lookup"><span data-stu-id="a418b-228">JSON preset</span></span>
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideo",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a><span data-ttu-id="a418b-229">Set di impostazioni XML</span><span class="sxs-lookup"><span data-stu-id="a418b-229">XML preset</span></span>

<span data-ttu-id="a418b-230">Se si usa XML, applicare Condition="InsertBlackIfNoVideo" come attributo per l'elemento **H264Video** e Condition="InsertSilenceIfNoAudio" come attributo per l'elemento **AACAudio**.</span><span class="sxs-lookup"><span data-stu-id="a418b-230">When using XML, use Condition="InsertBlackIfNoVideo" as an attribute to the **H264Video** element and  Condition="InsertSilenceIfNoAudio" as an attribute to **AACAudio**.</span></span>

```
. . .
<Encoding>
  <H264Video Condition="InsertBlackIfNoVideo">
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <SceneChangeDetection>true</SceneChangeDetection>
    <StretchMode>AutoSize</StretchMode>
    <H264Layers>
      <H264Layer>
        . . .
      </H264Layer>
    </H264Layers>
    <Chapters />
  </H264Video>
  <AACAudio Condition="InsertSilenceIfNoAudio">
    <Profile>AACLC</Profile>
    <Channels>2</Channels>
    <SamplingRate>48000</SamplingRate>
    <Bitrate>128</Bitrate>
  </AACAudio>
</Encoding>
. . .  
```

## <span data-ttu-id="a418b-231"><a id="rotate_video"></a>Ruotare un video</span><span class="sxs-lookup"><span data-stu-id="a418b-231"><a id="rotate_video"></a>Rotate a video</span></span>
<span data-ttu-id="a418b-232">Il [codificatore multimediale standard](media-services-dotnet-encode-with-media-encoder-standard.md) supporta la rotazione in base ad angoli di 0/90/180/270.</span><span class="sxs-lookup"><span data-stu-id="a418b-232">The [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supports rotation by angles of 0/90/180/270.</span></span> <span data-ttu-id="a418b-233">Il comportamento predefinito è "Auto", che tenta di rilevare i metadati di rotazione nel file video in arrivo per la compensazione.</span><span class="sxs-lookup"><span data-stu-id="a418b-233">The default behavior is "Auto", where it tries to detect the rotation metadata in the incoming video file and compensate for it.</span></span> <span data-ttu-id="a418b-234">Includere l'elemento **Sources** seguente in uno dei set di impostazioni definiti in [questa](media-services-mes-presets-overview.md) sezione:</span><span class="sxs-lookup"><span data-stu-id="a418b-234">Include the following **Sources** element to one of the presets defined in [this](media-services-mes-presets-overview.md) section:</span></span>

### <a name="json-preset"></a><span data-ttu-id="a418b-235">Set di impostazioni JSON</span><span class="sxs-lookup"><span data-stu-id="a418b-235">JSON preset</span></span>
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...
### <a name="xml-preset"></a><span data-ttu-id="a418b-236">Set di impostazioni XML</span><span class="sxs-lookup"><span data-stu-id="a418b-236">XML preset</span></span>
    <Sources>
           <Source>
          <Streams />
          <Filters>
            <Rotation>90</Rotation>
          </Filters>
        </Source>
    </Sources>

<span data-ttu-id="a418b-237">Per altre informazioni sul modo in cui il codificatore interpreta le impostazioni di larghezza e altezza nei set di impostazioni quando è attivata la compensazione di rotazione, vedere [questo](media-services-mes-schema.md#PreserveResolutionAfterRotation) argomento.</span><span class="sxs-lookup"><span data-stu-id="a418b-237">Also, see [this](media-services-mes-schema.md#PreserveResolutionAfterRotation) topic for more information on how the encoder interprets the Width and Height settings in the preset, when rotation compensation is triggered.</span></span>

<span data-ttu-id="a418b-238">È possibile usare il valore "0" per indicare al codificatore di ignorare i metadati di rotazione, se presenti, nel video di input.</span><span class="sxs-lookup"><span data-stu-id="a418b-238">You can use the value "0" to indicate to the encoder to ignore rotation metadata, if present, in the input video.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="a418b-239">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="a418b-239">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a418b-240">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="a418b-240">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="a418b-241">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="a418b-241">See Also</span></span>
[<span data-ttu-id="a418b-242">Panoramica sulla codifica dei servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="a418b-242">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)
