---
title: aaa"caricamento di file in un account di servizi multimediali tramite hello portale di Azure | Documenti di Microsoft"
description: In questa esercitazione vengono illustrati i passaggi hello di caricamento dei file in un account di servizi multimediali tramite hello portale di Azure
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3ad3dcea-95be-4711-9aae-a455a32434f6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 4ce1e133c72854532735ba7c72a43c92a75bc240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-azure-portal"></a><span data-ttu-id="5c40e-103">Caricare file in un account di servizi multimediali tramite hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="5c40e-103">Upload files into a Media Services account using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5c40e-104">Portale</span><span class="sxs-lookup"><span data-stu-id="5c40e-104">Portal</span></span>](media-services-portal-upload-files.md)
> * [<span data-ttu-id="5c40e-105">.NET</span><span class="sxs-lookup"><span data-stu-id="5c40e-105">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="5c40e-106">REST</span><span class="sxs-lookup"><span data-stu-id="5c40e-106">REST</span></span>](media-services-rest-upload-files.md)
> 
> [!NOTE]
> <span data-ttu-id="5c40e-107">toocomplete questa esercitazione, è necessario un account di Azure.</span><span class="sxs-lookup"><span data-stu-id="5c40e-107">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="5c40e-108">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5c40e-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 


<span data-ttu-id="5c40e-109">In Servizi multimediali è possibile caricare i file digitali in un asset.</span><span class="sxs-lookup"><span data-stu-id="5c40e-109">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="5c40e-110">Hello Asset può contenere video, audio, immagini, raccolte di anteprime, testo tracce e sottotitoli file (e relativi metadati hello.) Una volta caricati i file hello, il contenuto è archiviato in modo sicuro nel cloud hello per continuare l'elaborazione e il flusso.</span><span class="sxs-lookup"><span data-stu-id="5c40e-110">hello Asset  can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.) Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>


## <a name="upload-files"></a><span data-ttu-id="5c40e-111">Caricare file</span><span class="sxs-lookup"><span data-stu-id="5c40e-111">Upload files</span></span>

>[!NOTE]
><span data-ttu-id="5c40e-112">È una limite toohello dimensione massima supportata per l'elaborazione in servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="5c40e-112">There is a limit toohello maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="5c40e-113">Vedere [questo](media-services-quotas-and-limitations.md) per informazioni sulla limitazione delle dimensioni del file hello.</span><span class="sxs-lookup"><span data-stu-id="5c40e-113">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
>

1. <span data-ttu-id="5c40e-114">In hello [portale di Azure](https://portal.azure.com/), selezionare l'account di servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="5c40e-114">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="5c40e-115">In hello **impostazioni** pannello, fare clic su **asset**.</span><span class="sxs-lookup"><span data-stu-id="5c40e-115">On hello **Settings** blade, click **Assets**.</span></span>
   
    ![Caricare file](./media/media-services-portal-vod-get-started/media-services-upload.png)
3. <span data-ttu-id="5c40e-117">Fare clic su hello **caricare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="5c40e-117">Click hello **Upload** button.</span></span>
   
    <span data-ttu-id="5c40e-118">Hello **caricare una risorsa video** verrà visualizzata la finestra.</span><span class="sxs-lookup"><span data-stu-id="5c40e-118">hello **Upload a video asset** window appears.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5c40e-119">Non esistono limiti alle dimensioni dei file.</span><span class="sxs-lookup"><span data-stu-id="5c40e-119">There is no file size limitation.</span></span>
   > 
   > 
4. <span data-ttu-id="5c40e-120">Sfoglia video toohello desiderato nel computer in uso, selezionarlo e fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="5c40e-120">Browse toohello desired video on your computer, select it, and hit OK.</span></span>  
   
    <span data-ttu-id="5c40e-121">Avvia il caricamento di Hello ed è possibile visualizzare lo stato di avanzamento hello in nome file hello.</span><span class="sxs-lookup"><span data-stu-id="5c40e-121">hello upload starts and you can see hello progress under hello file name.</span></span>  

<span data-ttu-id="5c40e-122">Una volta completato il caricamento di hello, si noterà nuovo asset hello elencati in hello **asset** finestra.</span><span class="sxs-lookup"><span data-stu-id="5c40e-122">Once hello upload completes, you will see hello new asset listed in hello **Assets** window.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5c40e-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5c40e-123">Next steps</span></span>
<span data-ttu-id="5c40e-124">Ora è possibile codificare gli asset caricati.</span><span class="sxs-lookup"><span data-stu-id="5c40e-124">You can now encode your uploaded assets.</span></span> <span data-ttu-id="5c40e-125">Per altre informazioni, vedere [Encode assets](media-services-portal-encode.md)(Codificare gli asset).</span><span class="sxs-lookup"><span data-stu-id="5c40e-125">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="5c40e-126">È possibile utilizzare anche funzioni Azure tootrigger un processo di codifica in base a un file in arrivo nel contenitore hello configurato.</span><span class="sxs-lookup"><span data-stu-id="5c40e-126">You can also use Azure Functions tootrigger an encoding job based on a file arriving in hello configured container.</span></span> <span data-ttu-id="5c40e-127">Per altre informazioni, vedere [questo esempio](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span><span class="sxs-lookup"><span data-stu-id="5c40e-127">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="5c40e-128">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="5c40e-128">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5c40e-129">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="5c40e-129">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

