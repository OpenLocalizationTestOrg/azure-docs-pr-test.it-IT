---
title: aaaPerform avanzate codifica personalizzando MES predefiniti | Documenti Microsoft
description: "Questo argomento viene illustrato come tooperform avanzate codifica personalizzando Media Encoder Standard attività predefiniti."
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
ms.openlocfilehash: 9caa68fafacaf51f91f0554c5bafe491928d8c77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="perform-advanced-encoding-by-customizing-mes-presets"></a><span data-ttu-id="757ac-103">Eseguire attività di codifica avanzata personalizzando i set di impostazioni di Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="757ac-103">Perform advanced encoding by customizing MES presets</span></span> 

## <a name="overview"></a><span data-ttu-id="757ac-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="757ac-104">Overview</span></span>

<span data-ttu-id="757ac-105">Questo argomento viene illustrato come toocustomize Media Encoder Standard predefiniti.</span><span class="sxs-lookup"><span data-stu-id="757ac-105">This topic shows how toocustomize Media Encoder Standard presets.</span></span> <span data-ttu-id="757ac-106">Hello [codifica con Media Encoder Standard utilizzando predefiniti personalizzati](media-services-custom-mes-presets-with-dotnet.md) argomento viene illustrato come toouse .NET toocreate una codifica attività e un processo che esegue questa attività.</span><span class="sxs-lookup"><span data-stu-id="757ac-106">hello [Encoding with Media Encoder Standard using custom presets](media-services-custom-mes-presets-with-dotnet.md) topic shows how toouse .NET toocreate an encoding task and a job that executes this task.</span></span> <span data-ttu-id="757ac-107">Dopo aver personalizzato di un set di impostazioni attività codifica toohello alimentatore hello predefiniti personalizzati.</span><span class="sxs-lookup"><span data-stu-id="757ac-107">Once you customize a preset, supply hello custom presets toohello encoding task.</span></span> 

>[!NOTE]
><span data-ttu-id="757ac-108">Se si utilizza un set di impostazioni XML, creare che toopreserve hello ordine degli elementi, come illustrato negli esempi XML seguenti (durata di KeyFrameInterval, ad esempio, deve precedere SceneChangeDetection).</span><span class="sxs-lookup"><span data-stu-id="757ac-108">If using an XML preset, make sure toopreserve hello order of elements, as shown in XML samples below (for example, KeyFrameInterval should precede SceneChangeDetection).</span></span>
>

<span data-ttu-id="757ac-109">In questo argomento vengono illustrati predefiniti personalizzati hello che eseguono hello seguente attività di codifica.</span><span class="sxs-lookup"><span data-stu-id="757ac-109">In this topic, hello custom presets that perform hello following encoding tasks are demonstrated.</span></span>

## <a name="support-for-relative-sizes"></a><span data-ttu-id="757ac-110">Supporto per le dimensioni relative</span><span class="sxs-lookup"><span data-stu-id="757ac-110">Support for relative sizes</span></span>

<span data-ttu-id="757ac-111">Durante la generazione di anteprime, non è necessario specificare di tooalways output larghezza e altezza in pixel.</span><span class="sxs-lookup"><span data-stu-id="757ac-111">When generating thumbnails, you do not need tooalways specify output width and height in pixels.</span></span> <span data-ttu-id="757ac-112">È possibile specificarle in percentuali nell'intervallo di hello [% 1, …, 100%].</span><span class="sxs-lookup"><span data-stu-id="757ac-112">You can specify them in percentages, in hello range [1%, …, 100%].</span></span>

### <a name="json-preset"></a><span data-ttu-id="757ac-113">Set di impostazioni JSON</span><span class="sxs-lookup"><span data-stu-id="757ac-113">JSON preset</span></span>
    "Width": "100%",
    "Height": "100%"

### <a name="xml-preset"></a><span data-ttu-id="757ac-114">Set di impostazioni XML</span><span class="sxs-lookup"><span data-stu-id="757ac-114">XML preset</span></span>
    <Width>100%</Width>
    <Height>100%</Height>

## <span data-ttu-id="757ac-115"><a id="thumbnails"></a>Generare anteprime</span><span class="sxs-lookup"><span data-stu-id="757ac-115"><a id="thumbnails"></a>Generate thumbnails</span></span>

<span data-ttu-id="757ac-116">Questa sezione viene illustrato come toocustomize un set di impostazioni che genera le anteprime.</span><span class="sxs-lookup"><span data-stu-id="757ac-116">This section shows how toocustomize a preset that generates thumbnails.</span></span> <span data-ttu-id="757ac-117">Hello predefinito definito di seguito contiene informazioni su come si desidera tooencode il file, nonché le informazioni necessarie toogenerate anteprime.</span><span class="sxs-lookup"><span data-stu-id="757ac-117">hello preset defined below contains information on how you want tooencode your file as well as information needed toogenerate thumbnails.</span></span> <span data-ttu-id="757ac-118">È possibile eseguire uno dei set di impostazioni MES hello documentato [questo](media-services-mes-presets-overview.md) sezione e aggiungere codice che genera le anteprime.</span><span class="sxs-lookup"><span data-stu-id="757ac-118">You can take any of hello MES presets documented [this](media-services-mes-presets-overview.md) section and add code that generates thumbnails.</span></span>  

> [!NOTE]
> <span data-ttu-id="757ac-119">Hello **SceneChangeDetection** impostazione hello seguente set di impostazioni può essere impostato solo tootrue se si esegue la codifica video con velocità in bit singola tooa.</span><span class="sxs-lookup"><span data-stu-id="757ac-119">hello **SceneChangeDetection** setting in hello following preset can only be set tootrue if you are encoding tooa single  bitrate video.</span></span> <span data-ttu-id="757ac-120">Se si esegue la codifica tooa più velocità in bit video e impostare **SceneChangeDetection** tootrue, il codificatore hello restituisce un errore.</span><span class="sxs-lookup"><span data-stu-id="757ac-120">If you are encoding tooa multi-bitrate video and set **SceneChangeDetection** tootrue, hello encoder returns an error.</span></span>  
>
>

<span data-ttu-id="757ac-121">Per informazioni sullo schema, vedere [questo](media-services-mes-schema.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="757ac-121">For information about schema, see [this](media-services-mes-schema.md) topic.</span></span>

<span data-ttu-id="757ac-122">Verificare che hello tooreview [considerazioni](#considerations) sezione.</span><span class="sxs-lookup"><span data-stu-id="757ac-122">Make sure tooreview hello [Considerations](#considerations) section.</span></span>

### <span data-ttu-id="757ac-123"><a id="json"></a>Set di impostazioni JSON</span><span class="sxs-lookup"><span data-stu-id="757ac-123"><a id="json"></a>JSON preset</span></span>
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


### <span data-ttu-id="757ac-124"><a id="xml"></a>Set di impostazioni XML</span><span class="sxs-lookup"><span data-stu-id="757ac-124"><a id="xml"></a>XML preset</span></span>
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

### <a name="considerations"></a><span data-ttu-id="757ac-125">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="757ac-125">Considerations</span></span>

<span data-ttu-id="757ac-126">si applica Hello seguenti considerazioni:</span><span class="sxs-lookup"><span data-stu-id="757ac-126">hello following considerations apply:</span></span>

* <span data-ttu-id="757ac-127">utilizzo di Hello del timestamp esplicito per Inizio passaggio/intervallo presuppone che tale origine di input hello è lungo almeno 1 minuto.</span><span class="sxs-lookup"><span data-stu-id="757ac-127">hello use of explicit timestamps for Start/Step/Range assumes that hello input source is at least 1 minute long.</span></span>
* <span data-ttu-id="757ac-128">Gli elementi Jpg/Png/BmpImage hanno gli attributi inizio, passaggio e intervallo della stringa, che possono essere interpretati come:</span><span class="sxs-lookup"><span data-stu-id="757ac-128">Jpg/Png/BmpImage elements have Start, Step, and Range string attributes – these can be interpreted as:</span></span>

  * <span data-ttu-id="757ac-129">Se sono numeri interi non negativi, numero di frame, ad esempio "Start": "120",</span><span class="sxs-lookup"><span data-stu-id="757ac-129">Frame Number if they are non-negative integers, for example "Start": "120",</span></span>
  * <span data-ttu-id="757ac-130">Durata toosource relativo se espresso come presenta il suffisso %, ad esempio "Start": "% 15", o</span><span class="sxs-lookup"><span data-stu-id="757ac-130">Relative toosource duration if expressed as %-suffixed, for example "Start": "15%", OR</span></span>
  * <span data-ttu-id="757ac-131">Timestamp se espresso come HH:MM:SS</span><span class="sxs-lookup"><span data-stu-id="757ac-131">Timestamp if expressed as HH:MM:SS…</span></span> <span data-ttu-id="757ac-132">come formato, ad esempio "Start": "00:01:00"</span><span class="sxs-lookup"><span data-stu-id="757ac-132">format, for example "Start" : "00:01:00"</span></span>

    <span data-ttu-id="757ac-133">È possibile combinare e associare le notazioni a piacimento.</span><span class="sxs-lookup"><span data-stu-id="757ac-133">You can mix and match notations as you please.</span></span>

    <span data-ttu-id="757ac-134">Inizio supporta inoltre anche una Macro speciale: {ottimale}, che tenta di toodetermine hello primo "interessante" frame di contenuto hello Nota: (passaggio e intervallo vengono ignorati quando l'avvio viene impostato troppo {migliore})</span><span class="sxs-lookup"><span data-stu-id="757ac-134">Additionally, Start also supports a special Macro:{Best}, which attempts toodetermine hello first “interesting” frame of hello content NOTE: (Step and Range are ignored when Start is set too{Best})</span></span>
  * <span data-ttu-id="757ac-135">Impostazioni predefinite: Start: {Best}</span><span class="sxs-lookup"><span data-stu-id="757ac-135">Defaults: Start:{Best}</span></span>
* <span data-ttu-id="757ac-136">Formato di output deve toobe forniti in modo esplicito per ogni formato di immagine: Jpg o Png/BmpFormat.</span><span class="sxs-lookup"><span data-stu-id="757ac-136">Output format needs toobe explicitly provided for each Image format: Jpg/Png/BmpFormat.</span></span> <span data-ttu-id="757ac-137">Se presente, MES corrisponde JpgVideo tooJpgFormat e così via.</span><span class="sxs-lookup"><span data-stu-id="757ac-137">When present, MES matches JpgVideo tooJpgFormat and so on.</span></span> <span data-ttu-id="757ac-138">OutputFormat introduce una nuova immagine codec specifico (macro): {indice}, che richiede toobe presente (una volta e una sola volta) per formati di output di immagine.</span><span class="sxs-lookup"><span data-stu-id="757ac-138">OutputFormat introduces a new image-codec specific Macro: {Index}, which needs toobe present (once and only once) for image output formats.</span></span>

## <span data-ttu-id="757ac-139"><a id="trim_video"></a>Tagliare un video (ritaglio)</span><span class="sxs-lookup"><span data-stu-id="757ac-139"><a id="trim_video"></a>Trim a video (clipping)</span></span>
<span data-ttu-id="757ac-140">Discussioni questa sezione sulla modifica del codificatore hello predefiniti tooclip o tagliare i video di input hello dove hello input è un file mezzanine cosiddetti o su richiesta.</span><span class="sxs-lookup"><span data-stu-id="757ac-140">This section talks about modifying hello encoder presets tooclip or trim hello input video where hello input is a so-called mezzanine file or on-demand file.</span></span> <span data-ttu-id="757ac-141">Hello codificatore può anche essere utilizzati tooclip o tagliare un asset, che viene acquisito o archiviato da un flusso in tempo reale: hello dettagli per questo sono disponibili nel [questo blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="757ac-141">hello encoder can also be used tooclip or trim an asset, which is captured or archived from a live stream – hello details for this are available in [this blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).</span></span>

<span data-ttu-id="757ac-142">tootrim i video, può accettare qualsiasi hello MES predefiniti documentati [questo](media-services-mes-presets-overview.md) sezione e modificare hello **origini** elemento (come illustrato di seguito).</span><span class="sxs-lookup"><span data-stu-id="757ac-142">tootrim your videos, you can take any of hello MES presets documented [this](media-services-mes-presets-overview.md) section and modify hello **Sources** element (as shown below).</span></span> <span data-ttu-id="757ac-143">il valore di Hello di StartTime deve toomatch hello i timestamp assoluto del video di input hello.</span><span class="sxs-lookup"><span data-stu-id="757ac-143">hello value of StartTime needs toomatch hello absolute timestamps of hello input video.</span></span> <span data-ttu-id="757ac-144">Ad esempio, se hello primo frame del video di input hello ha un timestamp di 12:00:10.000 quindi StartTime deve essere almeno 12:00:10.000 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="757ac-144">For example, if hello first frame of hello input video has a timestamp of 12:00:10.000, then StartTime should be at least 12:00:10.000 and greater.</span></span> <span data-ttu-id="757ac-145">Nell'esempio hello seguente, si presuppone che l'input di hello video presenta un timestamp inizio pari a zero.</span><span class="sxs-lookup"><span data-stu-id="757ac-145">In hello example below, we assume that hello input video has a starting timestamp of zero.</span></span> <span data-ttu-id="757ac-146">**Origini** deve essere inserito all'inizio di hello di hello predefinito.</span><span class="sxs-lookup"><span data-stu-id="757ac-146">**Sources** should be placed at hello beginning of hello preset.</span></span>

### <span data-ttu-id="757ac-147"><a id="json"></a>Set di impostazioni JSON</span><span class="sxs-lookup"><span data-stu-id="757ac-147"><a id="json"></a>JSON preset</span></span>
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

### <a name="xml-preset"></a><span data-ttu-id="757ac-148">Set di impostazioni XML</span><span class="sxs-lookup"><span data-stu-id="757ac-148">XML preset</span></span>
<span data-ttu-id="757ac-149">tootrim i video, può accettare qualsiasi hello MES predefiniti documentati [qui](media-services-mes-presets-overview.md) e modificare hello **origini** elemento (come illustrato di seguito).</span><span class="sxs-lookup"><span data-stu-id="757ac-149">tootrim your videos, you can take any of hello MES presets documented [here](media-services-mes-presets-overview.md) and modify hello **Sources** element (as shown below).</span></span>

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

## <span data-ttu-id="757ac-150"><a id="overlay"></a>Creare una sovrimpressione</span><span class="sxs-lookup"><span data-stu-id="757ac-150"><a id="overlay"></a>Create an overlay</span></span>

<span data-ttu-id="757ac-151">Hello Media Encoder Standard consente toooverlay un'immagine in un video esistente.</span><span class="sxs-lookup"><span data-stu-id="757ac-151">hello Media Encoder Standard allows you toooverlay an image onto an existing video.</span></span> <span data-ttu-id="757ac-152">Attualmente, è supportato i seguenti formati hello: png, jpg, gif, bmp e.</span><span class="sxs-lookup"><span data-stu-id="757ac-152">Currently, hello following formats are supported: png, jpg, gif, and bmp.</span></span> <span data-ttu-id="757ac-153">Hello predefinito definito di seguito è un esempio di base di un sovrimpressione video.</span><span class="sxs-lookup"><span data-stu-id="757ac-153">hello preset defined below is a basic example  of a video overlay.</span></span>

<span data-ttu-id="757ac-154">Inoltre toodefining un file predefinito, è inoltre servizi multimediali toolet sapere quali file di asset hello è l'immagine sovrapposta hello e il file di cui è in cui si desidera che toooverlay hello immagine video di origine di hello.</span><span class="sxs-lookup"><span data-stu-id="757ac-154">In addition toodefining a preset file, you also have toolet Media Services know which file in hello asset is hello overlay image and which file is hello source video onto which you want toooverlay hello image.</span></span> <span data-ttu-id="757ac-155">file video Hello è hello toobe **primario** file.</span><span class="sxs-lookup"><span data-stu-id="757ac-155">hello video file has toobe hello **primary** file.</span></span>

<span data-ttu-id="757ac-156">Se si utilizza .NET, aggiungere hello seguenti due funzioni di esempio .NET toohello definito in [questo](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) argomento.</span><span class="sxs-lookup"><span data-stu-id="757ac-156">If you are using .NET, add hello following two functions toohello .NET example defined in [this](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) topic.</span></span> <span data-ttu-id="757ac-157">Hello **UploadMediaFilesFromFolder** funzione carica i file da una cartella (ad esempio, BigBuckBunny.mp4 e Image001.png) e set hello mp4 file toobe hello file primario nel asset hello.</span><span class="sxs-lookup"><span data-stu-id="757ac-157">hello **UploadMediaFilesFromFolder** function uploads files from a folder (for example, BigBuckBunny.mp4 and Image001.png) and sets hello mp4 file toobe hello primary file in hello asset.</span></span> <span data-ttu-id="757ac-158">Hello **EncodeWithOverlay** funzione utilizza hello personalizzato preimpostate che è stato passato tooit (ad esempio, hello preset che segue) toocreate hello attività di codifica.</span><span class="sxs-lookup"><span data-stu-id="757ac-158">hello **EncodeWithOverlay** function uses hello custom preset file that was passed tooit (for example, hello preset that follows) toocreate hello encoding task.</span></span>


    static public IAsset UploadMediaFilesFromFolder(string folderPath)
    {
        IAsset asset = _context.Assets.CreateFromFolder(folderPath, AssetCreationOptions.None);
    
        foreach (var af in asset.AssetFiles)
        {
            // hello following code assumes 
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
        // Get a media processor reference, and pass tooit hello name of hello 
        // processor toouse for hello specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Load hello XML (or JSON) from hello local file.
        string configuration = File.ReadAllText(customPresetFileName);

        // Create a task
        ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            configuration,
            TaskOptions.None);

        // Specify hello input assets toobe encoded.
        // This asset contains a source file and an overlay file.
        task.InputAssets.Add(assetSource);

        // Add an output asset toocontain hello results of hello job. 
        task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.None);

        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
        job.Submit();
        job.GetExecutionProgressTask(CancellationToken.None).Wait();

        return job.OutputMediaAssets[0];
    }


> [!NOTE]
> <span data-ttu-id="757ac-159">Limitazioni correnti:</span><span class="sxs-lookup"><span data-stu-id="757ac-159">Current limitations:</span></span>
>
> <span data-ttu-id="757ac-160">impostazione di opacità Hello sovrapposizione non è supportata.</span><span class="sxs-lookup"><span data-stu-id="757ac-160">hello overlay opacity setting is not supported.</span></span>
>
> <span data-ttu-id="757ac-161">Il file video di origine e di un file di immagine sovrapposta hello hanno toobe in hello stesso asset e hello file video esigenze toobe set come file primario hello questo asset.</span><span class="sxs-lookup"><span data-stu-id="757ac-161">Your source video file and hello overlay image file have toobe in hello same asset, and hello video file needs toobe set as hello primary file in this asset.</span></span>
>
>

### <a name="json-preset"></a><span data-ttu-id="757ac-162">Set di impostazioni JSON</span><span class="sxs-lookup"><span data-stu-id="757ac-162">JSON preset</span></span>
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


### <a name="xml-preset"></a><span data-ttu-id="757ac-163">Set di impostazioni XML</span><span class="sxs-lookup"><span data-stu-id="757ac-163">XML preset</span></span>
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


## <span data-ttu-id="757ac-164"><a id="silent_audio"></a>Inserire una traccia audio silenziosa quando l'input è privo di audio</span><span class="sxs-lookup"><span data-stu-id="757ac-164"><a id="silent_audio"></a>Insert a silent audio track when input has no audio</span></span>
<span data-ttu-id="757ac-165">Per impostazione predefinita, se si invia un codificatore toohello input che contiene solo i video e audio non hello asset di output contiene file che contengono dati solo video.</span><span class="sxs-lookup"><span data-stu-id="757ac-165">By default, if you send an input toohello encoder that contains only video, and no audio, then hello output asset contains files that contain only video data.</span></span> <span data-ttu-id="757ac-166">Alcuni lettori potrebbero non essere possibile toohandle tali flussi di output.</span><span class="sxs-lookup"><span data-stu-id="757ac-166">Some players may not be able toohandle such output streams.</span></span> <span data-ttu-id="757ac-167">È possibile utilizzare questo tooadd di codificatore hello tooforce impostazione un output di traccia audio invisibile all'utente toohello in tale scenario.</span><span class="sxs-lookup"><span data-stu-id="757ac-167">You can use this setting tooforce hello encoder tooadd a silent audio track toohello output in that scenario.</span></span>

<span data-ttu-id="757ac-168">tooforce hello codificatore tooproduce un asset che contenga una traccia audio invisibile all'utente quando l'input non dispone di alcun audio, specificare il valore di "InsertSilenceIfNoAudio" hello.</span><span class="sxs-lookup"><span data-stu-id="757ac-168">tooforce hello encoder tooproduce an asset that contains a silent audio track when input has no audio, specify hello "InsertSilenceIfNoAudio" value.</span></span>

<span data-ttu-id="757ac-169">È possibile eseguire qualsiasi hello MES predefiniti documentati in [questo](media-services-mes-presets-overview.md) sezione e rendere hello seguente modifica:</span><span class="sxs-lookup"><span data-stu-id="757ac-169">You can take any of hello MES presets documented in [this](media-services-mes-presets-overview.md) section, and make hello following modification:</span></span>

### <a name="json-preset"></a><span data-ttu-id="757ac-170">Set di impostazioni JSON</span><span class="sxs-lookup"><span data-stu-id="757ac-170">JSON preset</span></span>
    {
      "Channels": 2,
      "SamplingRate": 44100,
      "Bitrate": 96,
      "Type": "AACAudio",
      "Condition": "InsertSilenceIfNoAudio"
    }

### <a name="xml-preset"></a><span data-ttu-id="757ac-171">Set di impostazioni XML</span><span class="sxs-lookup"><span data-stu-id="757ac-171">XML preset</span></span>
    <AACAudio Condition="InsertSilenceIfNoAudio">
      <Channels>2</Channels>
      <SamplingRate>44100</SamplingRate>
      <Bitrate>96</Bitrate>
    </AACAudio>

## <span data-ttu-id="757ac-172"><a id="deinterlacing"></a>Disabilitare il deinterlacciamento automatico</span><span class="sxs-lookup"><span data-stu-id="757ac-172"><a id="deinterlacing"></a>Disable auto de-interlacing</span></span>
<span data-ttu-id="757ac-173">I clienti non devono toodo alcuna operazione se sono ad esempio hello interlacciata toobe contenuto automaticamente deallocare interlacciata.</span><span class="sxs-lookup"><span data-stu-id="757ac-173">Customers don’t need toodo anything if they like hello interlace contents toobe automatically de-interlaced.</span></span> <span data-ttu-id="757ac-174">Una volta deinterlacciamento dei automatica hello in hello (impostazione predefinita) MES hello automaticamente il rilevamento di fotogrammi interlacciati e solo interlaces deallocare frame contrassegnati come interlacciata.</span><span class="sxs-lookup"><span data-stu-id="757ac-174">When hello auto de-interlacing is on (default) hello MES does hello auto detection of interlaced frames and only de-interlaces frames marked as interlaced.</span></span>

<span data-ttu-id="757ac-175">È possibile disattivare deinterlacciamento dei automatica hello.</span><span class="sxs-lookup"><span data-stu-id="757ac-175">You can turn hello auto de-interlacing off.</span></span> <span data-ttu-id="757ac-176">Questa opzione non è consigliata.</span><span class="sxs-lookup"><span data-stu-id="757ac-176">This option is not recommended.</span></span>

### <a name="json-preset"></a><span data-ttu-id="757ac-177">Set di impostazioni JSON</span><span class="sxs-lookup"><span data-stu-id="757ac-177">JSON preset</span></span>
    "Sources": [
    {
     "Filters": {
        "Deinterlace": {
          "Mode": "Off"
        }
      },
    }
    ]

### <a name="xml-preset"></a><span data-ttu-id="757ac-178">Set di impostazioni XML</span><span class="sxs-lookup"><span data-stu-id="757ac-178">XML preset</span></span>
    <Sources>
    <Source>
      <Filters>
        <Deinterlace>
          <Mode>Off</Mode>
        </Deinterlace>
      </Filters>
    </Source>
    </Sources>


## <span data-ttu-id="757ac-179"><a id="audio_only"></a>Impostazioni predefinite solo audio</span><span class="sxs-lookup"><span data-stu-id="757ac-179"><a id="audio_only"></a>Audio-only presets</span></span>
<span data-ttu-id="757ac-180">In questa sezione vengono illustrate due impostazioni predefinite MES solo audio: Audio AAC e Audio AAC di buona qualità.</span><span class="sxs-lookup"><span data-stu-id="757ac-180">This section demonstrates two audio-only MES presets: AAC Audio and AAC Good Quality Audio.</span></span>

### <a name="aac-audio"></a><span data-ttu-id="757ac-181">Audio ACC</span><span class="sxs-lookup"><span data-stu-id="757ac-181">AAC Audio</span></span>
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

### <a name="aac-good-quality-audio"></a><span data-ttu-id="757ac-182">Audio AAC di buona qualità</span><span class="sxs-lookup"><span data-stu-id="757ac-182">AAC Good Quality Audio</span></span>
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

## <span data-ttu-id="757ac-183"><a id="concatenate"></a>Concatenare due o più file video</span><span class="sxs-lookup"><span data-stu-id="757ac-183"><a id="concatenate"></a>Concatenate two or more video files</span></span>

<span data-ttu-id="757ac-184">Hello seguente viene illustrato come è possibile generare un set di impostazioni tooconcatenate due o più file video.</span><span class="sxs-lookup"><span data-stu-id="757ac-184">hello following example illustrates how you can generate a preset tooconcatenate two or more video files.</span></span> <span data-ttu-id="757ac-185">nello scenario più comune di Hello è quando si desidera tooadd un'intestazione o un video principale di toohello finale.</span><span class="sxs-lookup"><span data-stu-id="757ac-185">hello most common scenario is when you want tooadd a header or a trailer toohello main video.</span></span> <span data-ttu-id="757ac-186">Hello scopo viene utilizzato quando i file video hello in fase di modifica insieme condividono proprietà (risoluzione video, frequenza dei fotogrammi, conteggio traccia audio e così via).</span><span class="sxs-lookup"><span data-stu-id="757ac-186">hello intended use is when hello video files being edited together share  properties (video resolution, frame rate, audio track count, etc.).</span></span> <span data-ttu-id="757ac-187">È necessario prestare attenzione non toomix video di frequenze diverse o con un numero diverso di tracce audio.</span><span class="sxs-lookup"><span data-stu-id="757ac-187">You should take care not toomix videos of different frame rates, or with different number of audio tracks.</span></span>

>[!NOTE]
><span data-ttu-id="757ac-188">Hello struttura corrente della funzionalità di concatenazione hello prevede che hello input clip video sono coerenti in termini di risoluzione, frequenza dei fotogrammi e così via.</span><span class="sxs-lookup"><span data-stu-id="757ac-188">hello current design of hello concatenation feature expects that hello input video clips are consistent in terms of resolution, frame rate etc.</span></span> 

### <a name="requirements-and-considerations"></a><span data-ttu-id="757ac-189">Problemi e considerazioni</span><span class="sxs-lookup"><span data-stu-id="757ac-189">Requirements and considerations</span></span>

* <span data-ttu-id="757ac-190">I video di input devono contenere solo una traccia audio.</span><span class="sxs-lookup"><span data-stu-id="757ac-190">Input videos should only have one audio track.</span></span>
* <span data-ttu-id="757ac-191">Video di input devono tutti avere hello stessa frequenza dei fotogrammi.</span><span class="sxs-lookup"><span data-stu-id="757ac-191">Input videos should all have hello same frame rate.</span></span>
* <span data-ttu-id="757ac-192">È necessario caricare i video in asset separati e impostare video hello come file primario hello ogni asset.</span><span class="sxs-lookup"><span data-stu-id="757ac-192">You must upload your videos into separate assets and set hello videos as hello primary file in each asset.</span></span>
* <span data-ttu-id="757ac-193">È necessario durata hello tooknow dei video.</span><span class="sxs-lookup"><span data-stu-id="757ac-193">You need tooknow hello duration of your videos.</span></span>
* <span data-ttu-id="757ac-194">Hello predefiniti negli esempi seguenti si presuppone che tutti i video di input hello inizino con un timestamp pari a zero.</span><span class="sxs-lookup"><span data-stu-id="757ac-194">hello preset examples below assumes that all hello input videos start with a timestamp of zero.</span></span> <span data-ttu-id="757ac-195">Sono necessari valori di StartTime hello toomodify se video hello con un timestamp di inizio diversi, come avviene in genere hello con gli archivi in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="757ac-195">You need toomodify hello StartTime values if hello videos have different starting timestamp, as is typically hello case with live archives.</span></span>
* <span data-ttu-id="757ac-196">Hello JSON predefinito rende i riferimenti espliciti toohello AssetID valori hello di asset di input.</span><span class="sxs-lookup"><span data-stu-id="757ac-196">hello JSON preset makes explicit references toohello AssetID values of hello input assets.</span></span>
* <span data-ttu-id="757ac-197">codice di esempio Hello si presuppone che hello che JSON predefinito è stato salvato come file locale tooa, ad esempio "C:\supportFiles\preset.json".</span><span class="sxs-lookup"><span data-stu-id="757ac-197">hello sample code assumes that hello JSON preset has been saved tooa local file, such as "C:\supportFiles\preset.json".</span></span> <span data-ttu-id="757ac-198">Si presuppone inoltre che siano state create due asset caricando due file video, di cui si conosce hello valori AssetID risultanti.</span><span class="sxs-lookup"><span data-stu-id="757ac-198">It also assumes that two assets have been created by uploading two video files, and that you know hello resultant AssetID values.</span></span>
* <span data-ttu-id="757ac-199">Hello frammento di codice e JSON predefinito viene illustrato un esempio della concatenazione di due file video.</span><span class="sxs-lookup"><span data-stu-id="757ac-199">hello code snippet and JSON preset shows an example of concatenating two video files.</span></span> <span data-ttu-id="757ac-200">È possibile estenderlo toomore rispetto a due video da:</span><span class="sxs-lookup"><span data-stu-id="757ac-200">You can extend it toomore than two videos by:</span></span>

  1. <span data-ttu-id="757ac-201">Attività chiamata. InputAssets.Add() ripetutamente tooadd altri video, in ordine.</span><span class="sxs-lookup"><span data-stu-id="757ac-201">Calling task.InputAssets.Add() repeatedly tooadd more videos, in order.</span></span>
  2. <span data-ttu-id="757ac-202">Rendendo corrispondente Modifica elemento toohello "origini" hello JSON, dall'aggiunta di più voci, hello stesso ordine.</span><span class="sxs-lookup"><span data-stu-id="757ac-202">Making corresponding edits toohello "Sources" element in hello JSON, by adding more entries, in hello same order.</span></span>

### <a name="net-code"></a><span data-ttu-id="757ac-203">Codice .NET</span><span class="sxs-lookup"><span data-stu-id="757ac-203">.NET code</span></span>

    IAsset asset1 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:606db602-efd7-4436-97b4-c0b867ba195b").FirstOrDefault();
    IAsset asset2 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e").FirstOrDefault();

    // Declare a new job.
    IJob job = _context.Jobs.Create("Media Encoder Standard Job for Concatenating Videos");
    // Get a media processor reference, and pass tooit hello name of the
    // processor toouse for hello specific task.
    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

    // Load hello XML (or JSON) from hello local file.
    string configuration = File.ReadAllText(@"c:\supportFiles\preset.json");

    // Create a task
    ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
        processor,
        configuration,
        TaskOptions.None);

    // Specify hello input videos toobe concatenated (in order).
    task.InputAssets.Add(asset1);
    task.InputAssets.Add(asset2);
    // Add an output asset toocontain hello results of hello job.
    // This output is specified as AssetCreationOptions.None, which
    // means hello output asset is not encrypted.
    task.OutputAssets.AddNew("Output asset",
        AssetCreationOptions.None);

    job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
    job.Submit();
    job.GetExecutionProgressTask(CancellationToken.None).Wait();

### <a name="json-preset"></a><span data-ttu-id="757ac-204">Set di impostazioni JSON</span><span class="sxs-lookup"><span data-stu-id="757ac-204">JSON preset</span></span>

<span data-ttu-id="757ac-205">Aggiornare personalizzati predefiniti con gli ID degli asset hello che si desidera tooconcatenate e con intervallo di tempo appropriato hello per ogni video.</span><span class="sxs-lookup"><span data-stu-id="757ac-205">Update your custom preset with ids of hello assets that you want tooconcatenate, and with hello appropriate time segment for each video.</span></span>

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

## <span data-ttu-id="757ac-206"><a id="crop"></a>Ritagliare video con Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="757ac-206"><a id="crop"></a>Crop videos with Media Encoder Standard</span></span>
<span data-ttu-id="757ac-207">Vedere hello [ritagliare video con Media Encoder Standard](media-services-crop-video.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="757ac-207">See hello [Crop videos with Media Encoder Standard](media-services-crop-video.md) topic.</span></span>

## <span data-ttu-id="757ac-208"><a id="no_video"></a>Inserire una traccia video quando l'input non ha video</span><span class="sxs-lookup"><span data-stu-id="757ac-208"><a id="no_video"></a>Insert a video track when input has no video</span></span>

<span data-ttu-id="757ac-209">Per impostazione predefinita, se si invia un codificatore toohello input che contiene solo audio e video non hello asset di output contiene file che contengono dati solo audio.</span><span class="sxs-lookup"><span data-stu-id="757ac-209">By default, if you send an input toohello encoder that contains only audio, and no video, then hello output asset contains files that contain only audio data.</span></span> <span data-ttu-id="757ac-210">Alcuni lettori, tra cui Azure Media Player (vedere [questo](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) potrebbe non essere in grado di toohandle questi flussi.</span><span class="sxs-lookup"><span data-stu-id="757ac-210">Some players, including Azure Media Player (see [this](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) may not be able toohandle such streams.</span></span> <span data-ttu-id="757ac-211">È possibile utilizzare un output di traccia video monocromatica toohello tooadd di codificatore questa impostazione tooforce hello in tale scenario.</span><span class="sxs-lookup"><span data-stu-id="757ac-211">You can use this setting tooforce hello encoder tooadd a monochrome video track toohello output in that scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="757ac-212">Una dimensione di hello aumenta traccia video output di hello forzando hello codificatore tooinsert Asset di output e hello in tal modo i costi sostenuti per attività di codifica hello.</span><span class="sxs-lookup"><span data-stu-id="757ac-212">Forcing hello encoder tooinsert an output video track increases hello size of hello output Asset, and thereby hello cost incurred for hello encoding Task.</span></span> <span data-ttu-id="757ac-213">È consigliabile eseguire test tooverify questo aumento incide solo modesta sugli addebiti mensili.</span><span class="sxs-lookup"><span data-stu-id="757ac-213">You should run tests tooverify that this resultant increase has only a modest impact on your monthly charges.</span></span>
>

### <a name="inserting-video-at-only-hello-lowest-bitrate"></a><span data-ttu-id="757ac-214">Inserimento di video a solo hello più bassa velocità in bit</span><span class="sxs-lookup"><span data-stu-id="757ac-214">Inserting video at only hello lowest bitrate</span></span>

<span data-ttu-id="757ac-215">Si supponga che si utilizza una velocità in bit più codifica predefinito, ad esempio ["H264 bitrate multiplo con risoluzione 720p"](media-services-mes-preset-h264-multiple-bitrate-720p.md) tooencode all'intero catalogo per lo streaming, che contiene una combinazione di file solo audio e video di input.</span><span class="sxs-lookup"><span data-stu-id="757ac-215">Suppose you are using a multiple bitrate encoding preset such as ["H264 Multiple Bitrate 720p"](media-services-mes-preset-h264-multiple-bitrate-720p.md) tooencode your entire input catalog for streaming, which contains a mix of video files and audio-only files.</span></span> <span data-ttu-id="757ac-216">In questo scenario, quando l'input hello dispone di alcun monitor, è opportuno tooforce hello codificatore tooinsert un video monocromatico rilevare al solo hello più bassa velocità in bit, come tooinserting anziché video a velocità in bit ogni output.</span><span class="sxs-lookup"><span data-stu-id="757ac-216">In this scenario, when hello input has no video, you may want tooforce hello encoder tooinsert a monochrome video track at just hello lowest bitrate, as opposed tooinserting video at every output bitrate.</span></span> <span data-ttu-id="757ac-217">tooachieve, è necessario hello toouse **InsertBlackIfNoVideoBottomLayerOnly** flag.</span><span class="sxs-lookup"><span data-stu-id="757ac-217">tooachieve this, you need toouse hello **InsertBlackIfNoVideoBottomLayerOnly** flag.</span></span>

<span data-ttu-id="757ac-218">È possibile eseguire qualsiasi hello MES predefiniti documentati in [questo](media-services-mes-presets-overview.md) sezione e rendere hello seguente modifica:</span><span class="sxs-lookup"><span data-stu-id="757ac-218">You can take any of hello MES presets documented in [this](media-services-mes-presets-overview.md) section, and make hello following modification:</span></span>

#### <a name="json-preset"></a><span data-ttu-id="757ac-219">Set di impostazioni JSON</span><span class="sxs-lookup"><span data-stu-id="757ac-219">JSON preset</span></span>
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideoBottomLayerOnly",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a><span data-ttu-id="757ac-220">Set di impostazioni XML</span><span class="sxs-lookup"><span data-stu-id="757ac-220">XML preset</span></span>

<span data-ttu-id="757ac-221">Quando si utilizza XML, utilizzare una condizione = "InsertBlackIfNoVideoBottomLayerOnly" come un attributo di toohello **H264Video** elemento e condizione = "InsertSilenceIfNoAudio" come attributo troppo**AACAudio**.</span><span class="sxs-lookup"><span data-stu-id="757ac-221">When using XML, use Condition="InsertBlackIfNoVideoBottomLayerOnly" as an attribute toohello **H264Video** element and  Condition="InsertSilenceIfNoAudio" as an attribute too**AACAudio**.</span></span>

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

### <a name="inserting-video-at-all-output-bitrates"></a><span data-ttu-id="757ac-222">Inserimento di video a tutte le velocità in bit di output</span><span class="sxs-lookup"><span data-stu-id="757ac-222">Inserting video at all output bitrates</span></span>
<span data-ttu-id="757ac-223">Si supponga che si utilizza una velocità in bit più codifica predefinito, ad esempio ["H264 bitrate multiplo con risoluzione 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) tooencode all'intero catalogo per lo streaming, che contiene una combinazione di file solo audio e video di input.</span><span class="sxs-lookup"><span data-stu-id="757ac-223">Suppose you are using a multiple bitrate encoding preset such as ["H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) tooencode your entire input catalog for streaming, which contains a mix of video files and audio-only files.</span></span> <span data-ttu-id="757ac-224">In questo scenario, quando l'input hello dispone di alcun monitor, è opportuno tooforce hello codificatore tooinsert tenere traccia di un video monocromatico a tutte le velocità di output di hello in.</span><span class="sxs-lookup"><span data-stu-id="757ac-224">In this scenario, when hello input has no video, you may want tooforce hello encoder tooinsert a monochrome video track at all hello output bitrates.</span></span> <span data-ttu-id="757ac-225">Ciò garantisce che l'output di attività sono tutte omogeneo con riguardo toonumber di tracce video e le tracce audio.</span><span class="sxs-lookup"><span data-stu-id="757ac-225">This ensures that your output Assets are all homogenous with respect toonumber of video tracks and audio tracks.</span></span> <span data-ttu-id="757ac-226">tooachieve, è necessario toospecify hello flag "InsertBlackIfNoVideo".</span><span class="sxs-lookup"><span data-stu-id="757ac-226">tooachieve this, you need toospecify hello "InsertBlackIfNoVideo" flag.</span></span>

<span data-ttu-id="757ac-227">È possibile eseguire qualsiasi hello MES predefiniti documentati in [questo](media-services-mes-presets-overview.md) sezione e rendere hello seguente modifica:</span><span class="sxs-lookup"><span data-stu-id="757ac-227">You can take any of hello MES presets documented in [this](media-services-mes-presets-overview.md) section, and make hello following modification:</span></span>

#### <a name="json-preset"></a><span data-ttu-id="757ac-228">Set di impostazioni JSON</span><span class="sxs-lookup"><span data-stu-id="757ac-228">JSON preset</span></span>
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideo",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a><span data-ttu-id="757ac-229">Set di impostazioni XML</span><span class="sxs-lookup"><span data-stu-id="757ac-229">XML preset</span></span>

<span data-ttu-id="757ac-230">Quando si utilizza XML, utilizzare una condizione = "InsertBlackIfNoVideo" come un attributo di toohello **H264Video** elemento e condizione = "InsertSilenceIfNoAudio" come attributo troppo**AACAudio**.</span><span class="sxs-lookup"><span data-stu-id="757ac-230">When using XML, use Condition="InsertBlackIfNoVideo" as an attribute toohello **H264Video** element and  Condition="InsertSilenceIfNoAudio" as an attribute too**AACAudio**.</span></span>

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

## <span data-ttu-id="757ac-231"><a id="rotate_video"></a>Ruotare un video</span><span class="sxs-lookup"><span data-stu-id="757ac-231"><a id="rotate_video"></a>Rotate a video</span></span>
<span data-ttu-id="757ac-232">Hello [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supporta rotazione dagli angoli di utilizzabile come 0, 90, 180 o 270.</span><span class="sxs-lookup"><span data-stu-id="757ac-232">hello [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supports rotation by angles of 0/90/180/270.</span></span> <span data-ttu-id="757ac-233">comportamento predefinito di Hello è "Auto", in cui tenta toodetect hello rotazione metadati nel file video in ingresso hello e compensare relativo.</span><span class="sxs-lookup"><span data-stu-id="757ac-233">hello default behavior is "Auto", where it tries toodetect hello rotation metadata in hello incoming video file and compensate for it.</span></span> <span data-ttu-id="757ac-234">Sono inclusi i seguenti hello **origini** tooone elemento hello predefiniti definiti in [questo](media-services-mes-presets-overview.md) sezione:</span><span class="sxs-lookup"><span data-stu-id="757ac-234">Include hello following **Sources** element tooone of hello presets defined in [this](media-services-mes-presets-overview.md) section:</span></span>

### <a name="json-preset"></a><span data-ttu-id="757ac-235">Set di impostazioni JSON</span><span class="sxs-lookup"><span data-stu-id="757ac-235">JSON preset</span></span>
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
### <a name="xml-preset"></a><span data-ttu-id="757ac-236">Set di impostazioni XML</span><span class="sxs-lookup"><span data-stu-id="757ac-236">XML preset</span></span>
    <Sources>
           <Source>
          <Streams />
          <Filters>
            <Rotation>90</Rotation>
          </Filters>
        </Source>
    </Sources>

<span data-ttu-id="757ac-237">Vedere anche [questo](media-services-mes-schema.md#PreserveResolutionAfterRotation) argomento per ulteriori informazioni sulla modalità di interpretazione delle impostazioni di larghezza e altezza hello in hello codificatore hello predefinito, quando viene attivato compensazione di rotazione.</span><span class="sxs-lookup"><span data-stu-id="757ac-237">Also, see [this](media-services-mes-schema.md#PreserveResolutionAfterRotation) topic for more information on how hello encoder interprets hello Width and Height settings in hello preset, when rotation compensation is triggered.</span></span>

<span data-ttu-id="757ac-238">È possibile utilizzare hello valore "0" tooindicate toohello codificatore tooignore rotazione dei metadati, se presente, nel video di input hello.</span><span class="sxs-lookup"><span data-stu-id="757ac-238">You can use hello value "0" tooindicate toohello encoder tooignore rotation metadata, if present, in hello input video.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="757ac-239">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="757ac-239">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="757ac-240">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="757ac-240">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="757ac-241">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="757ac-241">See Also</span></span>
[<span data-ttu-id="757ac-242">Panoramica sulla codifica dei servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="757ac-242">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)
