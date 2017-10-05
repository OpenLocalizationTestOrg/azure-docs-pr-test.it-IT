---
title: Codificare un asset mediante Media Encoder Standard con il portale di Azure | Microsoft Docs
description: Questa esercitazione descrive le operazioni di codifica di un asset mediante Media Encoder Standard con il portale di Azure.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 107d9e9a-71e9-43e5-b17c-6e00983aceab
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: a299245e285c4caa68988b184799cd6f4d13e080
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="encode-an-asset-using-media-encoder-standard-with-the-azure-portal"></a><span data-ttu-id="5b9e9-103">Codificare un asset mediante Media Encoder Standard con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="5b9e9-103">Encode an asset using Media Encoder Standard with the Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="5b9e9-104">Per completare l'esercitazione, è necessario un account Azure.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-104">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="5b9e9-105">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5b9e9-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="5b9e9-106">Quando si usa Servizi multimediali di Azure, uno degli scenari più frequenti consiste nella distribuzione di contenuti in streaming a velocità in bit adattiva ai client.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-106">When working with Azure Media Services one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span></span> <span data-ttu-id="5b9e9-107">Servizi multimediali supporta le tecnologie di streaming a bitrate adattivo seguenti: HTTP Live Streaming (HLS), Smooth Streaming e MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-107">Media Services supports the following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span> <span data-ttu-id="5b9e9-108">Per preparare i video per lo streaming a bitrate adattivo, è necessario codificare il video di origine in file a più bitrate.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-108">To prepare your videos for adaptive bitrate streaming, you need to encode your source video into multi-bitrate files.</span></span> <span data-ttu-id="5b9e9-109">Per codificare i video, è consigliabile usare il codificatore **Media Encoder Standard** .</span><span class="sxs-lookup"><span data-stu-id="5b9e9-109">You should use the **Media Encoder Standard** encoder to encode your videos.</span></span>  

<span data-ttu-id="5b9e9-110">Servizi multimediali include la funzionalità per la creazione dinamica dei pacchetti, che consente di distribuire file MP4 a bitrate multipli nei formati MPEG-DASH, HLS e Smooth Streaming, senza dover ricreare i pacchetti in questi formati di streaming.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-110">Media Services also provides dynamic packaging which allows you to deliver your multi-bitrate MP4s in the following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having to re-package into these streaming formats.</span></span> <span data-ttu-id="5b9e9-111">Con la creazione dinamica dei pacchetti si archiviano e si pagano solo i file in un unico formato di archiviazione e Servizi multimediali crea e fornisce la risposta appropriata in base alle richieste di un client.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-111">With dynamic packaging you only need to store and pay for the files in single storage format and Media Services will build and serve the appropriate response based on requests from a client.</span></span>

<span data-ttu-id="5b9e9-112">Per sfruttare i vantaggi della creazione dinamica dei pacchetti, è necessario codificare il file di origine in un set di file MP4 a bitrate multipli. La procedura per la codifica è descritta più avanti in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-112">To take advantage of dynamic packaging, you need to encode your source file into a set of multi-bitrate MP4 files (the encoding steps are demonstrated later in this section).</span></span>

<span data-ttu-id="5b9e9-113">Per ridimensionare l'elaborazione multimediale, vedere [questo](media-services-portal-scale-media-processing.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-113">To scale media processing, see [this](media-services-portal-scale-media-processing.md) topic.</span></span>

## <a name="encode-with-the-azure-portal"></a><span data-ttu-id="5b9e9-114">Eseguire la codifica con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="5b9e9-114">Encode with the Azure portal</span></span>
<span data-ttu-id="5b9e9-115">Questa sezione descrive la procedura per la codifica di contenuti con Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-115">This section describes the steps you can take to encode your content with Media Encoder Standard.</span></span>

1. <span data-ttu-id="5b9e9-116">Nel [portale di Azure ](https://portal.azure.com/) selezionare l'account Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-116">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="5b9e9-117">Nella finestra **Impostazioni** selezionare **Asset**.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-117">In the **Settings** window, select **Assets**.</span></span>  
3. <span data-ttu-id="5b9e9-118">Nella finestra **Asset** selezionare la risorsa che si vuole codificare.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-118">In the **Assets** window, select the asset that you would like to encode.</span></span>
4. <span data-ttu-id="5b9e9-119">Fare clic sul pulsante **Codifica** .</span><span class="sxs-lookup"><span data-stu-id="5b9e9-119">Press the **Encode** button.</span></span>
5. <span data-ttu-id="5b9e9-120">Nella finestra **Codifica un asset** selezionare il processore "Media Encoder Standard" e un set di impostazioni.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-120">In the **Encode an asset** window, select the "Media Encoder Standard" processor and a preset.</span></span> <span data-ttu-id="5b9e9-121">Per informazioni sui set di impostazioni, vedere [Generare automaticamente un bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) e [Set di impostazioni delle attività MES](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5b9e9-121">For information about presets, see [auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task Presets for MES](media-services-mes-presets-overview.md).</span></span> <span data-ttu-id="5b9e9-122">Se si prevede di controllare il set di impostazioni di codifica usato, tenere presente che è importante selezionare il set di impostazioni più appropriato per il video di input.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-122">If you plan to control which encoding preset is used, keep this in mind: it is important to select the preset that is most appropriate for your input video.</span></span> <span data-ttu-id="5b9e9-123">Ad esempio, se è noto che il video di input ha una risoluzione di 1920x1080 pixel, è possibile usare il set di impostazioni "Codec video H.264 a bitrate multiplo con risoluzione 1080p".</span><span class="sxs-lookup"><span data-stu-id="5b9e9-123">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use the "H264 Multiple Bitrate 1080p" preset.</span></span> <span data-ttu-id="5b9e9-124">Se il video disponibile è a bassa risoluzione (640x360), non usare il set di impostazioni "Codec video H.264 a bitrate multiplo con risoluzione 1080p".</span><span class="sxs-lookup"><span data-stu-id="5b9e9-124">If you have a low resolution (640x360) video, then you should not be using "H264 Multiple Bitrate 1080p" preset.</span></span>
   
   <span data-ttu-id="5b9e9-125">Per una gestione più semplice, è possibile modificare il nome dell'asset di output e il nome del processo.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-125">For easier management, you have an option of editing the name of the output asset, and the name of the job.</span></span>
   
   ![Codificare gli asset](./media/media-services-portal-vod-get-started/media-services-encode1.png)
6. <span data-ttu-id="5b9e9-127">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-127">Press **Create**.</span></span>

## <a name="next-step"></a><span data-ttu-id="5b9e9-128">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="5b9e9-128">Next step</span></span>
<span data-ttu-id="5b9e9-129">È possibile monitorare lo stato del processo di codifica con il portale di Azure, come descritto in [questo](media-services-portal-check-job-progress.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-129">You can monitor encoding job progress with the Azure portal, as described in [this](media-services-portal-check-job-progress.md) article.</span></span>  

## <a name="media-services-learning-paths"></a><span data-ttu-id="5b9e9-130">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="5b9e9-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5b9e9-131">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="5b9e9-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

