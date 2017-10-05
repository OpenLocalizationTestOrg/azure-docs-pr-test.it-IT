---
title: " Caricare file in un account Servizi multimediali usando il portale di Azure | Documentazione Microsoft"
description: Questa esercitazione illustra la procedura di caricamento di file in un account Servizi multimediali con il portale di Azure.
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
ms.openlocfilehash: 3a1dd7470f940da839687478b636464d930d8ab7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="upload-files-into-a-media-services-account-using-the-azure-portal"></a><span data-ttu-id="4c4e8-103">Caricare file in un account Servizi multimediali usando il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="4c4e8-103">Upload files into a Media Services account using the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4c4e8-104">Portale</span><span class="sxs-lookup"><span data-stu-id="4c4e8-104">Portal</span></span>](media-services-portal-upload-files.md)
> * [<span data-ttu-id="4c4e8-105">.NET</span><span class="sxs-lookup"><span data-stu-id="4c4e8-105">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="4c4e8-106">REST</span><span class="sxs-lookup"><span data-stu-id="4c4e8-106">REST</span></span>](media-services-rest-upload-files.md)
> 
> [!NOTE]
> <span data-ttu-id="4c4e8-107">Per completare l'esercitazione, è necessario un account Azure.</span><span class="sxs-lookup"><span data-stu-id="4c4e8-107">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="4c4e8-108">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4c4e8-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 


<span data-ttu-id="4c4e8-109">In Servizi multimediali è possibile caricare i file digitali in un asset.</span><span class="sxs-lookup"><span data-stu-id="4c4e8-109">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="4c4e8-110">L'asset può contenere video, audio, immagini, raccolte di anteprime, tracce di testo e file di sottotitoli codificati, oltre ai metadati relativi a questi file. Dopo aver caricato i file, i contenuti vengono archiviati in modo sicuro nel cloud per altre operazioni di elaborazione e streaming.</span><span class="sxs-lookup"><span data-stu-id="4c4e8-110">The Asset  can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.) Once the files are uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span>


## <a name="upload-files"></a><span data-ttu-id="4c4e8-111">Caricare file</span><span class="sxs-lookup"><span data-stu-id="4c4e8-111">Upload files</span></span>

>[!NOTE]
><span data-ttu-id="4c4e8-112">È previsto un limite per le dimensioni massime dei file supportate per l'elaborazione in Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="4c4e8-112">There is a limit to the maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="4c4e8-113">Vedere [questo](media-services-quotas-and-limitations.md) argomento per informazioni dettagliate sulla limitazione per le dimensioni dei file.</span><span class="sxs-lookup"><span data-stu-id="4c4e8-113">Please see [this](media-services-quotas-and-limitations.md) topic for details about the file size limitation.</span></span>
>

1. <span data-ttu-id="4c4e8-114">Nel [portale di Azure ](https://portal.azure.com/) selezionare l'account Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="4c4e8-114">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="4c4e8-115">Nel pannello **Impostazioni** fare clic su **Asset**.</span><span class="sxs-lookup"><span data-stu-id="4c4e8-115">On the **Settings** blade, click **Assets**.</span></span>
   
    ![Caricare file](./media/media-services-portal-vod-get-started/media-services-upload.png)
3. <span data-ttu-id="4c4e8-117">Fare clic sul pulsante **Upload** .</span><span class="sxs-lookup"><span data-stu-id="4c4e8-117">Click the **Upload** button.</span></span>
   
    <span data-ttu-id="4c4e8-118">Verrà visualizzata la finestra **Carica un asset video** .</span><span class="sxs-lookup"><span data-stu-id="4c4e8-118">The **Upload a video asset** window appears.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4c4e8-119">Non esistono limiti alle dimensioni dei file.</span><span class="sxs-lookup"><span data-stu-id="4c4e8-119">There is no file size limitation.</span></span>
   > 
   > 
4. <span data-ttu-id="4c4e8-120">Passare al video desiderato nel computer locale, selezionarlo e fare clic su OK.</span><span class="sxs-lookup"><span data-stu-id="4c4e8-120">Browse to the desired video on your computer, select it, and hit OK.</span></span>  
   
    <span data-ttu-id="4c4e8-121">Il caricamento viene avviato ed è possibile visualizzare l'avanzamento sotto il nome del file.</span><span class="sxs-lookup"><span data-stu-id="4c4e8-121">The upload starts and you can see the progress under the file name.</span></span>  

<span data-ttu-id="4c4e8-122">Al termine del caricamento, il nuovo asset verrà visualizzato nella finestra **Asset** .</span><span class="sxs-lookup"><span data-stu-id="4c4e8-122">Once the upload completes, you will see the new asset listed in the **Assets** window.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4c4e8-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4c4e8-123">Next steps</span></span>
<span data-ttu-id="4c4e8-124">Ora è possibile codificare gli asset caricati.</span><span class="sxs-lookup"><span data-stu-id="4c4e8-124">You can now encode your uploaded assets.</span></span> <span data-ttu-id="4c4e8-125">Per altre informazioni, vedere [Encode assets](media-services-portal-encode.md)(Codificare gli asset).</span><span class="sxs-lookup"><span data-stu-id="4c4e8-125">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="4c4e8-126">È anche possibile usare Funzioni di Azure per attivare un processo di codifica basato su un file che arriva nel contenitore configurato.</span><span class="sxs-lookup"><span data-stu-id="4c4e8-126">You can also use Azure Functions to trigger an encoding job based on a file arriving in the configured container.</span></span> <span data-ttu-id="4c4e8-127">Per altre informazioni, vedere [questo esempio](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span><span class="sxs-lookup"><span data-stu-id="4c4e8-127">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="4c4e8-128">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="4c4e8-128">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4c4e8-129">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="4c4e8-129">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

