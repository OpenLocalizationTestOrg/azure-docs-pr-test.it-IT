---
title: aaaEncode un asset con Media Encoder Standard hello portale di Azure | Documenti Microsoft
description: In questa esercitazione vengono illustrati i passaggi hello di codifica un asset con Media Encoder Standard hello portale di Azure.
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
ms.openlocfilehash: 0d118bbbe1fa9f4ba0bfa3ea3b10fb541d1d6379
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="encode-an-asset-using-media-encoder-standard-with-hello-azure-portal"></a><span data-ttu-id="f90a8-103">Codificare un asset con Media Encoder Standard hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f90a8-103">Encode an asset using Media Encoder Standard with hello Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="f90a8-104">toocomplete questa esercitazione, è necessario un account di Azure.</span><span class="sxs-lookup"><span data-stu-id="f90a8-104">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="f90a8-105">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f90a8-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="f90a8-106">Quando si lavora con servizi multimediali di Azure offre uno degli scenari più comuni di hello client tooyour streaming velocità in bit adattiva.</span><span class="sxs-lookup"><span data-stu-id="f90a8-106">When working with Azure Media Services one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="f90a8-107">Servizi multimediali supporta hello velocità in bit adattive tecnologie seguente: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="f90a8-107">Media Services supports hello following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span> <span data-ttu-id="f90a8-108">tooprepare i video per lo streaming a velocità in bit adattiva, è necessario tooencode l'origine video in file più velocità in bit.</span><span class="sxs-lookup"><span data-stu-id="f90a8-108">tooprepare your videos for adaptive bitrate streaming, you need tooencode your source video into multi-bitrate files.</span></span> <span data-ttu-id="f90a8-109">È consigliabile utilizzare hello **Media Encoder Standard** tooencode codificatore video.</span><span class="sxs-lookup"><span data-stu-id="f90a8-109">You should use hello **Media Encoder Standard** encoder tooencode your videos.</span></span>  

<span data-ttu-id="f90a8-110">Servizi multimediali offre anche creazione dinamica dei pacchetti che consente di toodeliver MP4s l'asset MP4 in hello seguenti formati di streaming: MPEG DASH, HLS, Smooth Streaming, senza che sia necessario toore-package in questi formati di streaming.</span><span class="sxs-lookup"><span data-stu-id="f90a8-110">Media Services also provides dynamic packaging which allows you toodeliver your multi-bitrate MP4s in hello following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having toore-package into these streaming formats.</span></span> <span data-ttu-id="f90a8-111">Con creazione dinamica dei pacchetti è necessario solo toostore e pagare per i file hello in unico formato di archiviazione e servizi multimediali creerà e fornirà hello risposta appropriata in base alle richieste da un client.</span><span class="sxs-lookup"><span data-stu-id="f90a8-111">With dynamic packaging you only need toostore and pay for hello files in single storage format and Media Services will build and serve hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="f90a8-112">Il vantaggio di tootake creazione dinamica dei pacchetti, è necessario tooencode il file di origine in un set di file MP4 a più velocità in bit (hello codifica passaggi sono illustrati più avanti in questa sezione).</span><span class="sxs-lookup"><span data-stu-id="f90a8-112">tootake advantage of dynamic packaging, you need tooencode your source file into a set of multi-bitrate MP4 files (hello encoding steps are demonstrated later in this section).</span></span>

<span data-ttu-id="f90a8-113">supporto tooscale l'elaborazione, vedere [questo](media-services-portal-scale-media-processing.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="f90a8-113">tooscale media processing, see [this](media-services-portal-scale-media-processing.md) topic.</span></span>

## <a name="encode-with-hello-azure-portal"></a><span data-ttu-id="f90a8-114">Codifica con hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f90a8-114">Encode with hello Azure portal</span></span>
<span data-ttu-id="f90a8-115">In questa sezione descrive i passaggi di hello è possibile eseguire tooencode il contenuto con Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="f90a8-115">This section describes hello steps you can take tooencode your content with Media Encoder Standard.</span></span>

1. <span data-ttu-id="f90a8-116">In hello [portale di Azure](https://portal.azure.com/), selezionare l'account di servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="f90a8-116">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="f90a8-117">In hello **impostazioni** selezionare **asset**.</span><span class="sxs-lookup"><span data-stu-id="f90a8-117">In hello **Settings** window, select **Assets**.</span></span>  
3. <span data-ttu-id="f90a8-118">In hello **asset** finestra, che si desidera tooencode asset di hello selezionare.</span><span class="sxs-lookup"><span data-stu-id="f90a8-118">In hello **Assets** window, select hello asset that you would like tooencode.</span></span>
4. <span data-ttu-id="f90a8-119">Hello premere **Encode** pulsante.</span><span class="sxs-lookup"><span data-stu-id="f90a8-119">Press hello **Encode** button.</span></span>
5. <span data-ttu-id="f90a8-120">In hello **codificare un asset** finestra e processore "Media Encoder Standard" hello selezionare un set di impostazioni.</span><span class="sxs-lookup"><span data-stu-id="f90a8-120">In hello **Encode an asset** window, select hello "Media Encoder Standard" processor and a preset.</span></span> <span data-ttu-id="f90a8-121">Per informazioni sui set di impostazioni, vedere [Generare automaticamente un bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) e [Set di impostazioni delle attività MES](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f90a8-121">For information about presets, see [auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task Presets for MES](media-services-mes-presets-overview.md).</span></span> <span data-ttu-id="f90a8-122">Se si prevede di toocontrol viene utilizzato il set di impostazioni di codifica, questo tenere presenti: è importante hello tooselect set di impostazioni che è più appropriato per il video di input.</span><span class="sxs-lookup"><span data-stu-id="f90a8-122">If you plan toocontrol which encoding preset is used, keep this in mind: it is important tooselect hello preset that is most appropriate for your input video.</span></span> <span data-ttu-id="f90a8-123">Ad esempio, se si conosce il video di input dispone di una risoluzione di 1920x1080 pixel, è possibile utilizzare hello "H264 bitrate multiplo con risoluzione 1080p" predefinito.</span><span class="sxs-lookup"><span data-stu-id="f90a8-123">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use hello "H264 Multiple Bitrate 1080p" preset.</span></span> <span data-ttu-id="f90a8-124">Se il video disponibile è a bassa risoluzione (640x360), non usare il set di impostazioni "Codec video H.264 a bitrate multiplo con risoluzione 1080p".</span><span class="sxs-lookup"><span data-stu-id="f90a8-124">If you have a low resolution (640x360) video, then you should not be using "H264 Multiple Bitrate 1080p" preset.</span></span>
   
   <span data-ttu-id="f90a8-125">Per facilitare la gestione, è un'opzione di modifica nome hello dell'asset di output di hello e nome hello del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="f90a8-125">For easier management, you have an option of editing hello name of hello output asset, and hello name of hello job.</span></span>
   
   ![Codificare gli asset](./media/media-services-portal-vod-get-started/media-services-encode1.png)
6. <span data-ttu-id="f90a8-127">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="f90a8-127">Press **Create**.</span></span>

## <a name="next-step"></a><span data-ttu-id="f90a8-128">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="f90a8-128">Next step</span></span>
<span data-ttu-id="f90a8-129">È possibile monitorare lo stato del processo codifica con hello portale di Azure, come descritto in [questo](media-services-portal-check-job-progress.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="f90a8-129">You can monitor encoding job progress with hello Azure portal, as described in [this](media-services-portal-check-job-progress.md) article.</span></span>  

## <a name="media-services-learning-paths"></a><span data-ttu-id="f90a8-130">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="f90a8-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f90a8-131">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="f90a8-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

