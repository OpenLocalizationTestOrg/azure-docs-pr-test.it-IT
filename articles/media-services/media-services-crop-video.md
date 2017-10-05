---
title: Questo articolo illustra come ritagliare video con Media Encoder Standard - Azure | Documentazione Microsoft
description: Questo articolo illustra come ritagliare video con Media Encoder Standard.
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 7628f674-2005-4531-8b61-d7a4f53e46ba
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/09/2017
ms.author: anilmur;juliako;
ms.openlocfilehash: 60d0ce14a271fcbe698559da95ca011cb888b221
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="crop-videos-with-media-encoder-standard"></a><span data-ttu-id="836f4-103">Ritagliare video con Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="836f4-103">Crop videos with Media Encoder Standard</span></span>
<span data-ttu-id="836f4-104">È possibile usare Media Encoder Standard (MES) per ritagliare l'input video.</span><span class="sxs-lookup"><span data-stu-id="836f4-104">You can use Media Encoder Standard (MES) to crop your input video.</span></span> <span data-ttu-id="836f4-105">Il ritaglio è il processo di selezione di una finestra rettangolare all'interno del fotogramma video per codificare solo i pixel all'interno di quella finestra.</span><span class="sxs-lookup"><span data-stu-id="836f4-105">Cropping is the process of selecting a rectangular window within the video frame, and encoding just the pixels within that window.</span></span> <span data-ttu-id="836f4-106">Il diagramma seguente illustra il processo.</span><span class="sxs-lookup"><span data-stu-id="836f4-106">The following diagram helps illustrate the process.</span></span>

![Ritagliare un video](./media/media-services-crop-video/media-services-crop-video01.png)

<span data-ttu-id="836f4-108">Si supponga di avere come input un video che ha una risoluzione di 1920x1080 pixel (proporzioni 16:9), ma presenta barre nere (formato 4:3) a sinistra e a destra, quindi solo una finestra in formato 4:3 o di 1440x1080 pixel contiene il video attivo.</span><span class="sxs-lookup"><span data-stu-id="836f4-108">Suppose you have as input a video that has a resolution of 1920x1080 pixels (16:9 aspect ratio), but has black bars (pillar boxes) at the left and right, so that only a 4:3 window or 1440x1080 pixels contains active video.</span></span> <span data-ttu-id="836f4-109">È possibile usare MES per ritagliare o modificare le barre nere e codificare l'area di 1440x1080 pixel.</span><span class="sxs-lookup"><span data-stu-id="836f4-109">You can use MES to crop or edit out the black bars, and encode the 1440x1080 region.</span></span>

<span data-ttu-id="836f4-110">Il ritaglio in MES è una fase di pre-elaborazione, quindi i parametri di ritaglio nel set di impostazioni di codifica si applicano al video di input originale.</span><span class="sxs-lookup"><span data-stu-id="836f4-110">Cropping in MES is a pre-processing stage, so the cropping parameters in the encoding preset apply to the original input video.</span></span> <span data-ttu-id="836f4-111">La codifica è una fase successiva e le impostazioni di larghezza/altezza si applicano al video *pre-elaborato* e non al video originale.</span><span class="sxs-lookup"><span data-stu-id="836f4-111">Encoding is a subsequent stage, and the width/height settings apply to the *pre-processed* video, and not to the original video.</span></span> <span data-ttu-id="836f4-112">Quando si progetta il set di impostazioni è necessario eseguire queste operazioni: (a) selezionare i parametri di ritaglio in base al video di input originale e (b) selezionare le impostazioni di codifica in base al video ritagliato.</span><span class="sxs-lookup"><span data-stu-id="836f4-112">When designing your preset you need to do the following: (a) select the crop parameters based on the original input video, and (b) select your encode settings based on the cropped video.</span></span> <span data-ttu-id="836f4-113">Se le impostazioni di codifica non corrispondono al video ritagliato, l'output non sarà quello previsto.</span><span class="sxs-lookup"><span data-stu-id="836f4-113">If you do not match your encode settings to the cropped video, the output will not be as you expect.</span></span>

<span data-ttu-id="836f4-114">L'argomento [seguente](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) illustra come creare un processo di codifica con MES e come specificare un set di impostazioni personalizzato per l'attività di codifica.</span><span class="sxs-lookup"><span data-stu-id="836f4-114">The [following](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) topic shows how to create an encoding job with MES and how to specify a custom preset for the encoding task.</span></span> 

## <a name="creating-a-custom-preset"></a><span data-ttu-id="836f4-115">Creazione di un set di impostazioni personalizzato</span><span class="sxs-lookup"><span data-stu-id="836f4-115">Creating a custom preset</span></span>
<span data-ttu-id="836f4-116">Nell'esempio illustrato nel diagramma:</span><span class="sxs-lookup"><span data-stu-id="836f4-116">In the example shown in the diagram:</span></span>

1. <span data-ttu-id="836f4-117">L'input originale è 1920x1080</span><span class="sxs-lookup"><span data-stu-id="836f4-117">Original input is 1920x1080</span></span>
2. <span data-ttu-id="836f4-118">Deve essere ritagliato in un output di 1440x1080, centrato nel frame di input</span><span class="sxs-lookup"><span data-stu-id="836f4-118">It needs to be cropped to an output of 1440x1080, which is centered in the input frame</span></span>
3. <span data-ttu-id="836f4-119">Ciò equivale a un offset X (1920 - 1440)/2 = 240 e un offset Y pari a zero</span><span class="sxs-lookup"><span data-stu-id="836f4-119">This means an X offset of (1920 – 1440)/2 = 240, and a Y offset of zero</span></span>
4. <span data-ttu-id="836f4-120">La larghezza e l'altezza del rettangolo di ritaglio sono rispettivamente di 1440 e 1080</span><span class="sxs-lookup"><span data-stu-id="836f4-120">The Width and Height of the Crop rectangle are 1440 and 1080, respectively</span></span>
5. <span data-ttu-id="836f4-121">Nella fase di codifica, l'attività consiste nel produrre tre livelli con risoluzioni di 1440x1080, 960x720 e 480x360</span><span class="sxs-lookup"><span data-stu-id="836f4-121">In the encode stage, the ask is to produce three layers, are resolutions 1440x1080, 960x720 and 480x360, respectively</span></span>

### <a name="json-preset"></a><span data-ttu-id="836f4-122">Set di impostazioni JSON</span><span class="sxs-lookup"><span data-stu-id="836f4-122">JSON preset</span></span>
    {
      "Version": 1.0,
      "Sources": [
        {
          "Streams": [],
          "Filters": {
            "Crop": {
                "X": 240,
                "Y": 0,
                "Width": 1440,
                "Height": 1080
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
              "Bitrate": 3400,
              "MaxBitrate": 3400,
              "BufferWindow": "00:00:05",
              "Width": 1440,
              "Height": 1080,
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
              "Bitrate": 1250,
              "MaxBitrate": 1250,
              "BufferWindow": "00:00:05",
              "Width": 480,
              "Height": 360,
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


## <a name="restrictions-on-cropping"></a><span data-ttu-id="836f4-123">Restrizioni relative al ritaglio</span><span class="sxs-lookup"><span data-stu-id="836f4-123">Restrictions on cropping</span></span>
<span data-ttu-id="836f4-124">La funzionalità di ritaglio è concepita per essere manuale.</span><span class="sxs-lookup"><span data-stu-id="836f4-124">The cropping feature is meant to be manual.</span></span> <span data-ttu-id="836f4-125">Sarà necessario caricare il video di input in uno strumento di editing valido che consenta di selezionare i frame di interesse, posizionare il cursore per determinare gli offset del rettangolo di ritaglio, per determinare il set di impostazioni di codifica ottimale per quel particolare video e così via. Questa funzionalità non è progettata per consentire ad esempio il rilevamento e la rimozione automatici dei bordi neri formato 16:9 e formato 4:3 nel video di input.</span><span class="sxs-lookup"><span data-stu-id="836f4-125">You would need to load your input video into a suitable editing tool that lets you select frames of interest, position the cursor to determine offsets for the cropping rectangle, to determine the encoding preset that is tuned for that particular video, etc. This feature is not meant to enable things like: automatic detection and removal of black letterbox/pillarbox borders in your input video.</span></span>

<span data-ttu-id="836f4-126">Alla funzionalità di ritaglio si applicano le limitazioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="836f4-126">Following constraints apply to the cropping feature.</span></span> <span data-ttu-id="836f4-127">Se queste limitazioni non vengono osservate, l'attività di codifica produrrà errori o un output imprevisto.</span><span class="sxs-lookup"><span data-stu-id="836f4-127">If these are not met, the encode Task can fail, or produce an unexpected output.</span></span>

1. <span data-ttu-id="836f4-128">Le coordinate e le dimensioni del rettangolo di ritaglio devono rientrare nel video di input</span><span class="sxs-lookup"><span data-stu-id="836f4-128">The co-ordinates and size of the Crop rectangle have to fit within the input video</span></span>
2. <span data-ttu-id="836f4-129">Come indicato in precedenza, la larghezza e l'altezza nelle impostazioni di codifica devono corrispondere al video ritagliato</span><span class="sxs-lookup"><span data-stu-id="836f4-129">As mentioned above, the Width & Height in the encode settings have to correspond to the cropped video</span></span>
3. <span data-ttu-id="836f4-130">Il ritaglio si applica a video acquisiti in modalità orizzontale, ovvero non è applicabile a video registrati con uno smartphone con orientamento verticale</span><span class="sxs-lookup"><span data-stu-id="836f4-130">Cropping applies to videos captured in landscape mode (i.e. not applicable to videos recorded with a smartphone held vertically or in portrait mode)</span></span>
4. <span data-ttu-id="836f4-131">Il ritaglio funziona in modo ottimale con video progressivo acquisito con pixel quadrati</span><span class="sxs-lookup"><span data-stu-id="836f4-131">Works best with progressive video captured with square pixels</span></span>

## <a name="provide-feedback"></a><span data-ttu-id="836f4-132">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="836f4-132">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="836f4-133">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="836f4-133">Next step</span></span>
<span data-ttu-id="836f4-134">Vedere i percorsi di apprendimento di Servizi multimediali di Azure per informazioni sulle potenti funzionalità offerte da Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="836f4-134">See Azure Media Services learning paths to help you learn about great features offered by AMS.</span></span>  

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]
