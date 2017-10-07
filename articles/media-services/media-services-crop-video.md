---
title: aaaHow toocrop video con Media Encoder Standard - Azure | Documenti Microsoft
description: Questo articolo viene illustrato come video toocrop con Media Encoder Standard.
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
ms.openlocfilehash: 2b4ac3d96228b93c890a38c57c4913988de1e8bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="crop-videos-with-media-encoder-standard"></a><span data-ttu-id="bd2fc-103">Ritagliare video con Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="bd2fc-103">Crop videos with Media Encoder Standard</span></span>
<span data-ttu-id="bd2fc-104">È possibile utilizzare supporti codificatore Standard (MES) toocrop il video di input.</span><span class="sxs-lookup"><span data-stu-id="bd2fc-104">You can use Media Encoder Standard (MES) toocrop your input video.</span></span> <span data-ttu-id="bd2fc-105">Il ritaglio è il processo di hello di selezione di una finestra rettangolare all'interno di fotogrammi video hello e codifica solo i pixel hello all'interno di tale finestra.</span><span class="sxs-lookup"><span data-stu-id="bd2fc-105">Cropping is hello process of selecting a rectangular window within hello video frame, and encoding just hello pixels within that window.</span></span> <span data-ttu-id="bd2fc-106">Consente di illustrare il processo di hello Hello seguente diagramma.</span><span class="sxs-lookup"><span data-stu-id="bd2fc-106">hello following diagram helps illustrate hello process.</span></span>

![Ritagliare un video](./media/media-services-crop-video/media-services-crop-video01.png)

<span data-ttu-id="bd2fc-108">Si supponga di che avere come input un video con risoluzione di 1920x1080 pixel (proporzioni 16:9), ma ha nere (pillar caselle) hello sinistro e destro, in modo che solo una finestra di 4:3 o 1440 x 1080 pixel contiene video attivo.</span><span class="sxs-lookup"><span data-stu-id="bd2fc-108">Suppose you have as input a video that has a resolution of 1920x1080 pixels (16:9 aspect ratio), but has black bars (pillar boxes) at hello left and right, so that only a 4:3 window or 1440x1080 pixels contains active video.</span></span> <span data-ttu-id="bd2fc-109">È possibile utilizzare MES toocrop o modificare le barre di hello nero e codificare area 1440 x 1080 hello.</span><span class="sxs-lookup"><span data-stu-id="bd2fc-109">You can use MES toocrop or edit out hello black bars, and encode hello 1440x1080 region.</span></span>

<span data-ttu-id="bd2fc-110">Ritaglio in MES è una fase di pre-elaborazione, pertanto i parametri di ritaglio hello in set di impostazioni di codifica hello applicano toohello video di input originale.</span><span class="sxs-lookup"><span data-stu-id="bd2fc-110">Cropping in MES is a pre-processing stage, so hello cropping parameters in hello encoding preset apply toohello original input video.</span></span> <span data-ttu-id="bd2fc-111">La codifica è una fase successiva, e le impostazioni di larghezza/altezza hello applicano toohello *pre-elaborato* video e non i video originale toohello.</span><span class="sxs-lookup"><span data-stu-id="bd2fc-111">Encoding is a subsequent stage, and hello width/height settings apply toohello *pre-processed* video, and not toohello original video.</span></span> <span data-ttu-id="bd2fc-112">Quando si progetta il set di impostazioni è necessario seguente hello toodo: (a) selezionare i parametri di ritaglio hello in base a video di input originale hello e (b) il codificare le impostazioni in base hello ritagliata video.</span><span class="sxs-lookup"><span data-stu-id="bd2fc-112">When designing your preset you need toodo hello following: (a) select hello crop parameters based on hello original input video, and (b) select your encode settings based on hello cropped video.</span></span> <span data-ttu-id="bd2fc-113">Se non corrispondono il codificare toohello impostazioni ritagliata video, l'output di hello non sarà come previsto.</span><span class="sxs-lookup"><span data-stu-id="bd2fc-113">If you do not match your encode settings toohello cropped video, hello output will not be as you expect.</span></span>

<span data-ttu-id="bd2fc-114">Hello [seguente](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) argomento viene illustrato come un processo di codifica con MES toocreate e come toospecify personalizzato preimpostato per hello attività di codifica.</span><span class="sxs-lookup"><span data-stu-id="bd2fc-114">hello [following](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) topic shows how toocreate an encoding job with MES and how toospecify a custom preset for hello encoding task.</span></span> 

## <a name="creating-a-custom-preset"></a><span data-ttu-id="bd2fc-115">Creazione di un set di impostazioni personalizzato</span><span class="sxs-lookup"><span data-stu-id="bd2fc-115">Creating a custom preset</span></span>
<span data-ttu-id="bd2fc-116">Nell'esempio hello illustrato nel diagramma hello:</span><span class="sxs-lookup"><span data-stu-id="bd2fc-116">In hello example shown in hello diagram:</span></span>

1. <span data-ttu-id="bd2fc-117">L'input originale è 1920x1080</span><span class="sxs-lookup"><span data-stu-id="bd2fc-117">Original input is 1920x1080</span></span>
2. <span data-ttu-id="bd2fc-118">È necessario toobe ritagliata output tooan di 1440 x 1080, viene centrata nel frame input hello</span><span class="sxs-lookup"><span data-stu-id="bd2fc-118">It needs toobe cropped tooan output of 1440x1080, which is centered in hello input frame</span></span>
3. <span data-ttu-id="bd2fc-119">Ciò equivale a un offset X (1920 - 1440)/2 = 240 e un offset Y pari a zero</span><span class="sxs-lookup"><span data-stu-id="bd2fc-119">This means an X offset of (1920 – 1440)/2 = 240, and a Y offset of zero</span></span>
4. <span data-ttu-id="bd2fc-120">Hello larghezza e altezza del rettangolo di ritaglio hello sono rispettivamente 1440 e 1080,</span><span class="sxs-lookup"><span data-stu-id="bd2fc-120">hello Width and Height of hello Crop rectangle are 1440 and 1080, respectively</span></span>
5. <span data-ttu-id="bd2fc-121">In hello fase codifica, hello chiedere tooproduce tre livelli, sono rispettivamente risoluzioni 1440 x 1080, 960 x 720 e 480 x 360</span><span class="sxs-lookup"><span data-stu-id="bd2fc-121">In hello encode stage, hello ask is tooproduce three layers, are resolutions 1440x1080, 960x720 and 480x360, respectively</span></span>

### <a name="json-preset"></a><span data-ttu-id="bd2fc-122">Set di impostazioni JSON</span><span class="sxs-lookup"><span data-stu-id="bd2fc-122">JSON preset</span></span>
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


## <a name="restrictions-on-cropping"></a><span data-ttu-id="bd2fc-123">Restrizioni relative al ritaglio</span><span class="sxs-lookup"><span data-stu-id="bd2fc-123">Restrictions on cropping</span></span>
<span data-ttu-id="bd2fc-124">Hello ritaglio funzionalità deve essere toobe manuale.</span><span class="sxs-lookup"><span data-stu-id="bd2fc-124">hello cropping feature is meant toobe manual.</span></span> <span data-ttu-id="bd2fc-125">È necessario tooload l'input video in uno strumento di modificando appropriato che consente di selezionare i frame di interesse, posizionare hello cursore toodetermine offset per il rettangolo di ritaglio hello, toodetermine hello set di impostazioni di codifica che è ottimizzato per quel particolare video, e così via. Questa funzionalità non è stata progettata tooenable ad esempio: rilevamento automatico e la rimozione dei bordi neri letterbox/formato pillarbox nell'input video.</span><span class="sxs-lookup"><span data-stu-id="bd2fc-125">You would need tooload your input video into a suitable editing tool that lets you select frames of interest, position hello cursor toodetermine offsets for hello cropping rectangle, toodetermine hello encoding preset that is tuned for that particular video, etc. This feature is not meant tooenable things like: automatic detection and removal of black letterbox/pillarbox borders in your input video.</span></span>

<span data-ttu-id="bd2fc-126">I vincoli seguenti si applicano toohello ritaglio funzionalità.</span><span class="sxs-lookup"><span data-stu-id="bd2fc-126">Following constraints apply toohello cropping feature.</span></span> <span data-ttu-id="bd2fc-127">Se questi non vengono soddisfatte, hello codificare attività può non riuscire o produrre un output imprevisto.</span><span class="sxs-lookup"><span data-stu-id="bd2fc-127">If these are not met, hello encode Task can fail, or produce an unexpected output.</span></span>

1. <span data-ttu-id="bd2fc-128">salve le coordinate e le dimensioni del rettangolo di ritaglio hello hanno toofit all'interno di video di input hello</span><span class="sxs-lookup"><span data-stu-id="bd2fc-128">hello co-ordinates and size of hello Crop rectangle have toofit within hello input video</span></span>
2. <span data-ttu-id="bd2fc-129">Come indicato in precedenza, hello larghezza e altezza in hello alle impostazioni di codifica sono toohello toocorrespond ritagliata video</span><span class="sxs-lookup"><span data-stu-id="bd2fc-129">As mentioned above, hello Width & Height in hello encode settings have toocorrespond toohello cropped video</span></span>
3. <span data-ttu-id="bd2fc-130">Ritaglio applica toovideos acquisiti in modalità orizzontale (ovvero non applicabile toovideos registrate con uno smartphone contenute in verticale o in modalità verticale)</span><span class="sxs-lookup"><span data-stu-id="bd2fc-130">Cropping applies toovideos captured in landscape mode (i.e. not applicable toovideos recorded with a smartphone held vertically or in portrait mode)</span></span>
4. <span data-ttu-id="bd2fc-131">Il ritaglio funziona in modo ottimale con video progressivo acquisito con pixel quadrati</span><span class="sxs-lookup"><span data-stu-id="bd2fc-131">Works best with progressive video captured with square pixels</span></span>

## <a name="provide-feedback"></a><span data-ttu-id="bd2fc-132">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="bd2fc-132">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="bd2fc-133">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="bd2fc-133">Next step</span></span>
<span data-ttu-id="bd2fc-134">Apprendimento toohelp percorsi di che conoscere funzionalità eccellenti offerta dal sistema AMS servizi multimediali di Azure, vedere.</span><span class="sxs-lookup"><span data-stu-id="bd2fc-134">See Azure Media Services learning paths toohelp you learn about great features offered by AMS.</span></span>  

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]
