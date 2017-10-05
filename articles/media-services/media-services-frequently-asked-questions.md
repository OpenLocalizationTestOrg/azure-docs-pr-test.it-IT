---
title: Domande frequenti su Servizi multimediali di Azure | Documentazione Microsoft
description: Domande frequenti (FAQ)
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5374f7f4-c189-43ef-8b7f-f2f4141e2748
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 48f3924d44a084d61c1d38002cd5098094001acb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="frequently-asked-questions"></a><span data-ttu-id="0f54d-103">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="0f54d-103">Frequently asked questions</span></span>

<span data-ttu-id="0f54d-104">Questo articolo contiene le domande frequenti sollevate dalla community di utenti di Servizi multimediali di Azure (AMS).</span><span class="sxs-lookup"><span data-stu-id="0f54d-104">This article addresses frequently asked questions raised by the Azure Media Services (AMS) user community.</span></span>

## <a name="general-ams-faqs"></a><span data-ttu-id="0f54d-105">Domande frequenti generali su AMS</span><span class="sxs-lookup"><span data-stu-id="0f54d-105">General AMS FAQs</span></span>
<span data-ttu-id="0f54d-106">D: Come scalare l'indicizzazione?</span><span class="sxs-lookup"><span data-stu-id="0f54d-106">Q: How do you scale indexing?</span></span>

<span data-ttu-id="0f54d-107">R: Le unità riservate sono le stesse per le attività di codifica e indicizzazione.</span><span class="sxs-lookup"><span data-stu-id="0f54d-107">A: The reserved units are the same for Encoding and Indexing tasks.</span></span> <span data-ttu-id="0f54d-108">Seguire le istruzioni in [Come scalare le unità riservate di codifica](media-services-scale-media-processing-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0f54d-108">Follow instructions on [How to Scale Encoding Reserved Units](media-services-scale-media-processing-overview.md).</span></span> <span data-ttu-id="0f54d-109">**Tenere presente** che le prestazioni dell'indicizzatore non vengono influenzate dal tipo di unità riservata.</span><span class="sxs-lookup"><span data-stu-id="0f54d-109">**Note** that Indexer performance is not affected by Reserved Unit Type.</span></span>

<span data-ttu-id="0f54d-110">D: Ho caricato, codificato e pubblicato un video.</span><span class="sxs-lookup"><span data-stu-id="0f54d-110">Q: I uploaded, encoded, and published a video.</span></span> <span data-ttu-id="0f54d-111">Quale può essere il motivo per cui il video non viene riprodotto quando provo a trasmetterlo in streaming?</span><span class="sxs-lookup"><span data-stu-id="0f54d-111">What would be the reason the video does not play when I try to stream it?</span></span>

<span data-ttu-id="0f54d-112">R: Uno dei motivi più comuni consiste nel fatto che l'endpoint di streaming da cui si sta tentando la riproduzione non si trova nello stato **In esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="0f54d-112">A: One of the most common reasons is you do not have the streaming endpoint from which you are trying to playback in the **Running** state.</span></span>  

<span data-ttu-id="0f54d-113">D: È possibile eseguire la composizione in un flusso live?</span><span class="sxs-lookup"><span data-stu-id="0f54d-113">Q: Can I do compositing on a live stream?</span></span>

<span data-ttu-id="0f54d-114">A: La composizione in flussi live non è attualmente disponibile in Servizi multimediali di Azure Media ed è quindi necessario eseguire una composizione preliminare sul proprio computer.</span><span class="sxs-lookup"><span data-stu-id="0f54d-114">A: Compositing on live streams is currently not offered in Azure Media Services, so you would need to pre-compose on your computer.</span></span>

<span data-ttu-id="0f54d-115">D: È possibile usare la rete CDN di Azure con Live Streaming?</span><span class="sxs-lookup"><span data-stu-id="0f54d-115">Q: Can I use Azure CDN with Live Streaming?</span></span>

<span data-ttu-id="0f54d-116">R: Servizi multimediali supporta l'integrazione con la rete CDN di Azure. Per altre informazioni, vedere l'articolo su [come gestire gli endpoint di streaming in un account di Servizi multimediali](media-services-portal-manage-streaming-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="0f54d-116">A: Media Services supports integration with Azure CDN (for more information, see [How to Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)).</span></span>  <span data-ttu-id="0f54d-117">È quindi possibile usare Live streaming con la rete CDN.</span><span class="sxs-lookup"><span data-stu-id="0f54d-117">You can use Live streaming with CDN.</span></span> <span data-ttu-id="0f54d-118">Servizi multimediali di Azure fornisce output in formato Smooth Streaming, HLS e MPEG-DASH.</span><span class="sxs-lookup"><span data-stu-id="0f54d-118">Azure Media Services provides Smooth Streaming, HLS and MPEG-DASH outputs.</span></span> <span data-ttu-id="0f54d-119">Tutti questi formati usano il protocollo HTTP per trasferire dati e ottenere i vantaggi derivanti dalla cache HTTP.</span><span class="sxs-lookup"><span data-stu-id="0f54d-119">All these formats use HTTP for transferring data and get benefits of HTTP caching.</span></span> <span data-ttu-id="0f54d-120">In Live Streaming i dati audio/video effettivi vengono divisi in frammenti, ciascuno dei quali viene memorizzato nella rete CDN.</span><span class="sxs-lookup"><span data-stu-id="0f54d-120">In live streaming actual video/audio data is divided to fragments and this individual fragments get cached in CDN.</span></span> <span data-ttu-id="0f54d-121">L'aggiornamento è necessario solo per i dati manifesto</span><span class="sxs-lookup"><span data-stu-id="0f54d-121">Only data needs to be refreshed is the manifest data.</span></span> <span data-ttu-id="0f54d-122">e viene effettuato periodicamente dalla rete CDN.</span><span class="sxs-lookup"><span data-stu-id="0f54d-122">CDN periodically refreshes manifest data.</span></span>

<span data-ttu-id="0f54d-123">D: Servizi multimediali di Azure supporta anche l'archiviazione di immagini?</span><span class="sxs-lookup"><span data-stu-id="0f54d-123">Q: Does Azure Media services support storing images?</span></span>

<span data-ttu-id="0f54d-124">R: Se si desidera archiviare immagini JPEG o PNG, è consigliabile memorizzarle nell'Archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="0f54d-124">A: If you are just looking to store JPEG or PNG images, you should keep those in Azure Blob Storage.</span></span> <span data-ttu-id="0f54d-125">Aggiungerle all'account di Servizi multimediali non comporta infatti alcun vantaggio, a meno che non si desideri tenerle associate ai propri asset audio o video o sia necessario usarle come sovrimpressioni nel codificatore video.</span><span class="sxs-lookup"><span data-stu-id="0f54d-125">There is no benefit to putting them in your Media Services account unless you want to keep them associated with your Video or Audio Assets.</span></span> <span data-ttu-id="0f54d-126">Media Encoder Standard supporta infatti la sovrimpressione di immagini nella parte superiore dei video ed è per questo che i formati JPEG e PNG sono elencati tra i formati di input supportati.</span><span class="sxs-lookup"><span data-stu-id="0f54d-126">Or if you might have a need to use the images as overlays in the video encoder.Media Encoder Standard supports overlaying images on top of videos, and that is what it lists JPEG and PNG as supported input formats.</span></span> <span data-ttu-id="0f54d-127">Per altre informazioni, vedere [Creazione di sovrimpressioni](media-services-advanced-encoding-with-mes.md#overlay).</span><span class="sxs-lookup"><span data-stu-id="0f54d-127">For more information, see [Creating Overlays](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

<span data-ttu-id="0f54d-128">D: Come è possibile copiare gli asset da un account di Servizi multimediali a un altro?</span><span class="sxs-lookup"><span data-stu-id="0f54d-128">Q: How can I copy assets from one Media Services account to another.</span></span>

<span data-ttu-id="0f54d-129">R: Per copiare gli asset da un account di Servizi multimediali a un altro con .NET, usare il metodo di estensione [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) disponibile nel repository [Azure Media Services .NET SDK Extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions/).</span><span class="sxs-lookup"><span data-stu-id="0f54d-129">A: To copy assets from one Media Services account to another using .NET, use [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) extension method available in the [Azure Media Services .NET SDK Extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions/) repository.</span></span> <span data-ttu-id="0f54d-130">Per altre informazioni, vedere [questo](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) thread del forum.</span><span class="sxs-lookup"><span data-stu-id="0f54d-130">For more information, see [this](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) forum thread.</span></span>

<span data-ttu-id="0f54d-131">D: Quali sono i caratteri supportati per la denominazione dei file quando si usa AMS?</span><span class="sxs-lookup"><span data-stu-id="0f54d-131">Q: What are the supported characters for naming files when working with AMS?</span></span>

<span data-ttu-id="0f54d-132">R: Servizi multimediali usa il valore della proprietà IAssetFile.Name durante la creazione di URL per i contenuti in streaming, ad esempio http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters. Per questo motivo, la codifica percentuale non è consentita.</span><span class="sxs-lookup"><span data-stu-id="0f54d-132">A: Media Services uses the value of the IAssetFile.Name property when building URLs for the streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="0f54d-133">Il valore della proprietà **Name** non può contenere i [caratteri riservati per la codifica percentuale](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters) seguenti: !*'();:@&=+$,/?%#[]".</span><span class="sxs-lookup"><span data-stu-id="0f54d-133">The value of the **Name** property cannot have any of the following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="0f54d-134">Può essere presente solo un carattere '.'</span><span class="sxs-lookup"><span data-stu-id="0f54d-134">Also, there can only be one ‘.’</span></span> <span data-ttu-id="0f54d-135">L'estensione del nome di file, inoltre, può essere preceduta da un solo punto (.).</span><span class="sxs-lookup"><span data-stu-id="0f54d-135">for the file name extension.</span></span>

<span data-ttu-id="0f54d-136">D: Come connettersi usando REST?</span><span class="sxs-lookup"><span data-stu-id="0f54d-136">Q: How to connect using REST?</span></span>

<span data-ttu-id="0f54d-137">R: Per informazioni su come connettersi all'API AMS, vedere [Accedere all'API di Servizi multimediali di Azure con l'autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="0f54d-137">A: For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> <span data-ttu-id="0f54d-138">Dopo avere stabilito la connessione a https://media.windows.net, si riceverà un reindirizzamento 301 che indica un altro URI di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="0f54d-138">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="0f54d-139">Le chiamate successive dovranno essere effettuate al nuovo URI.</span><span class="sxs-lookup"><span data-stu-id="0f54d-139">You must make subsequent calls to the new URI.</span></span> 

<span data-ttu-id="0f54d-140">D: Come è possibile ruotare un video durante il processo di codifica.</span><span class="sxs-lookup"><span data-stu-id="0f54d-140">Q: How can I rotate a video during the encoding process.</span></span>

<span data-ttu-id="0f54d-141">R: Il [codificatore multimediale standard](media-services-dotnet-encode-with-media-encoder-standard.md) supporta la rotazione in base ad angoli di 90/180/270.</span><span class="sxs-lookup"><span data-stu-id="0f54d-141">A: The [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supports rotation by angles of 90/180/270.</span></span> <span data-ttu-id="0f54d-142">Il comportamento predefinito è "Auto", che tenta di rilevare i metadati di rotazione nel file MP4/MOV in arrivo per la compensazione.</span><span class="sxs-lookup"><span data-stu-id="0f54d-142">The default behavior is "Auto", where it tries to detect the rotation metadata in the incoming MP4/MOV file and compensate for it.</span></span> <span data-ttu-id="0f54d-143">Includere l'elemento **Sources** seguente in uno dei set di impostazioni JSON definiti [qui](media-services-mes-presets-overview.md):</span><span class="sxs-lookup"><span data-stu-id="0f54d-143">Include the following **Sources** element to one of the json presets defined [here](media-services-mes-presets-overview.md):</span></span>

    "Version": 1.0,
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


## <a name="media-services-learning-paths"></a><span data-ttu-id="0f54d-144">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="0f54d-144">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0f54d-145">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="0f54d-145">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
