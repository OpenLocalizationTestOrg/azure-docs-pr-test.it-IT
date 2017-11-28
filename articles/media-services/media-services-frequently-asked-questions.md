---
title: Servizi multimediali di domande frequenti aaaAzure | Documenti Microsoft
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
ms.openlocfilehash: 6d48a5c1291f3c2559d8445921d571718d0a0a6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions"></a><span data-ttu-id="85bc4-103">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="85bc4-103">Frequently asked questions</span></span>

<span data-ttu-id="85bc4-104">Questo articolo illustra domande più frequenti generati da una comunità di utenti di servizi multimediali di Azure (AMS) hello.</span><span class="sxs-lookup"><span data-stu-id="85bc4-104">This article addresses frequently asked questions raised by hello Azure Media Services (AMS) user community.</span></span>

## <a name="general-ams-faqs"></a><span data-ttu-id="85bc4-105">Domande frequenti generali su AMS</span><span class="sxs-lookup"><span data-stu-id="85bc4-105">General AMS FAQs</span></span>
<span data-ttu-id="85bc4-106">D: Come scalare l'indicizzazione?</span><span class="sxs-lookup"><span data-stu-id="85bc4-106">Q: How do you scale indexing?</span></span>

<span data-ttu-id="85bc4-107">R: unità hello riservato sono hello stesso per la codifica e l'indicizzazione delle attività.</span><span class="sxs-lookup"><span data-stu-id="85bc4-107">A: hello reserved units are hello same for Encoding and Indexing tasks.</span></span> <span data-ttu-id="85bc4-108">Seguire le istruzioni [come unità riservate di codifica tooScale](media-services-scale-media-processing-overview.md).</span><span class="sxs-lookup"><span data-stu-id="85bc4-108">Follow instructions on [How tooScale Encoding Reserved Units](media-services-scale-media-processing-overview.md).</span></span> <span data-ttu-id="85bc4-109">**Tenere presente** che le prestazioni dell'indicizzatore non vengono influenzate dal tipo di unità riservata.</span><span class="sxs-lookup"><span data-stu-id="85bc4-109">**Note** that Indexer performance is not affected by Reserved Unit Type.</span></span>

<span data-ttu-id="85bc4-110">D: Ho caricato, codificato e pubblicato un video.</span><span class="sxs-lookup"><span data-stu-id="85bc4-110">Q: I uploaded, encoded, and published a video.</span></span> <span data-ttu-id="85bc4-111">Che verrebbero video di hello hello motivo non viene riprodotto quando si tenta di toostream è?</span><span class="sxs-lookup"><span data-stu-id="85bc4-111">What would be hello reason hello video does not play when I try toostream it?</span></span>

<span data-ttu-id="85bc4-112">R: una delle più comuni motivi è hello da cui si sta tentando di tooplayback in hello endpoint di streaming non si dispone di hello **esecuzione** stato.</span><span class="sxs-lookup"><span data-stu-id="85bc4-112">A: One of hello most common reasons is you do not have hello streaming endpoint from which you are trying tooplayback in hello **Running** state.</span></span>  

<span data-ttu-id="85bc4-113">D: È possibile eseguire la composizione in un flusso live?</span><span class="sxs-lookup"><span data-stu-id="85bc4-113">Q: Can I do compositing on a live stream?</span></span>

<span data-ttu-id="85bc4-114">R: composizione dei flussi in tempo reale attualmente non è disponibile in servizi multimediali di Azure, pertanto sarà necessario toopre-comporre nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="85bc4-114">A: Compositing on live streams is currently not offered in Azure Media Services, so you would need toopre-compose on your computer.</span></span>

<span data-ttu-id="85bc4-115">D: È possibile usare la rete CDN di Azure con Live Streaming?</span><span class="sxs-lookup"><span data-stu-id="85bc4-115">Q: Can I use Azure CDN with Live Streaming?</span></span>

<span data-ttu-id="85bc4-116">R: Media Services supporta l'integrazione con rete CDN di Azure (per ulteriori informazioni, vedere [come endpoint di Streaming tooManage in un Account di servizi multimediali](media-services-portal-manage-streaming-endpoints.md)).</span><span class="sxs-lookup"><span data-stu-id="85bc4-116">A: Media Services supports integration with Azure CDN (for more information, see [How tooManage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)).</span></span>  <span data-ttu-id="85bc4-117">È quindi possibile usare Live streaming con la rete CDN.</span><span class="sxs-lookup"><span data-stu-id="85bc4-117">You can use Live streaming with CDN.</span></span> <span data-ttu-id="85bc4-118">Servizi multimediali di Azure fornisce output in formato Smooth Streaming, HLS e MPEG-DASH.</span><span class="sxs-lookup"><span data-stu-id="85bc4-118">Azure Media Services provides Smooth Streaming, HLS and MPEG-DASH outputs.</span></span> <span data-ttu-id="85bc4-119">Tutti questi formati usano il protocollo HTTP per trasferire dati e ottenere i vantaggi derivanti dalla cache HTTP.</span><span class="sxs-lookup"><span data-stu-id="85bc4-119">All these formats use HTTP for transferring data and get benefits of HTTP caching.</span></span> <span data-ttu-id="85bc4-120">In dati video o audio effettivi in streaming in tempo reale è diviso toofragments e memorizzazione nella cache di questo singoli frammenti nella rete CDN.</span><span class="sxs-lookup"><span data-stu-id="85bc4-120">In live streaming actual video/audio data is divided toofragments and this individual fragments get cached in CDN.</span></span> <span data-ttu-id="85bc4-121">Solo i toobe di esigenze dati aggiornati è dati hello del manifesto.</span><span class="sxs-lookup"><span data-stu-id="85bc4-121">Only data needs toobe refreshed is hello manifest data.</span></span> <span data-ttu-id="85bc4-122">e viene effettuato periodicamente dalla rete CDN.</span><span class="sxs-lookup"><span data-stu-id="85bc4-122">CDN periodically refreshes manifest data.</span></span>

<span data-ttu-id="85bc4-123">D: Servizi multimediali di Azure supporta anche l'archiviazione di immagini?</span><span class="sxs-lookup"><span data-stu-id="85bc4-123">Q: Does Azure Media services support storing images?</span></span>

<span data-ttu-id="85bc4-124">R: se si vuole semplicemente toostore JPEG o immagini PNG, è consigliabile mantenere quelle nell'archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="85bc4-124">A: If you are just looking toostore JPEG or PNG images, you should keep those in Azure Blob Storage.</span></span> <span data-ttu-id="85bc4-125">Non è tooputting alcun vantaggio in servizi multimediali account a meno che non si desidera tookeep che li associate a un Video o Audio asset.</span><span class="sxs-lookup"><span data-stu-id="85bc4-125">There is no benefit tooputting them in your Media Services account unless you want tookeep them associated with your Video or Audio Assets.</span></span> <span data-ttu-id="85bc4-126">O se è necessario un toouse necessità hello immagini come sovrapposizioni di codificatore video hello. Media Encoder Standard supporta la sovrapposizione delle immagini su video, e che vengono elencati JPEG e PNG come supportati i formati di input.</span><span class="sxs-lookup"><span data-stu-id="85bc4-126">Or if you might have a need toouse hello images as overlays in hello video encoder.Media Encoder Standard supports overlaying images on top of videos, and that is what it lists JPEG and PNG as supported input formats.</span></span> <span data-ttu-id="85bc4-127">Per altre informazioni, vedere [Creazione di sovrimpressioni](media-services-advanced-encoding-with-mes.md#overlay).</span><span class="sxs-lookup"><span data-stu-id="85bc4-127">For more information, see [Creating Overlays](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

<span data-ttu-id="85bc4-128">D: come è possibile copiare le risorse da un tooanother di account di servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="85bc4-128">Q: How can I copy assets from one Media Services account tooanother.</span></span>

<span data-ttu-id="85bc4-129">R: toocopy asset da uno tooanother di account di servizi multimediali usando .NET, usare [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) metodo di estensione disponibile in hello [Azure Media Services .NET SDK Extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions/) repository.</span><span class="sxs-lookup"><span data-stu-id="85bc4-129">A: toocopy assets from one Media Services account tooanother using .NET, use [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) extension method available in hello [Azure Media Services .NET SDK Extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions/) repository.</span></span> <span data-ttu-id="85bc4-130">Per altre informazioni, vedere [questo](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) thread del forum.</span><span class="sxs-lookup"><span data-stu-id="85bc4-130">For more information, see [this](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) forum thread.</span></span>

<span data-ttu-id="85bc4-131">D: quali sono hello caratteri supportati per la denominazione dei file quando si lavora con AMS?</span><span class="sxs-lookup"><span data-stu-id="85bc4-131">Q: What are hello supported characters for naming files when working with AMS?</span></span>

<span data-ttu-id="85bc4-132">R: Media Services utilizza il valore di hello di hello IAssetFile.Name proprietà durante la creazione di URL per hello streaming del contenuto (ad esempio, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Per questo motivo, la codifica percentuale non è consentita.</span><span class="sxs-lookup"><span data-stu-id="85bc4-132">A: Media Services uses hello value of hello IAssetFile.Name property when building URLs for hello streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="85bc4-133">valore di hello Hello **nome** proprietà non può avere uno dei seguenti hello [% riservati per la codifica caratteri](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] ".</span><span class="sxs-lookup"><span data-stu-id="85bc4-133">hello value of hello **Name** property cannot have any of hello following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="85bc4-134">Può essere presente solo un carattere '.'</span><span class="sxs-lookup"><span data-stu-id="85bc4-134">Also, there can only be one ‘.’</span></span> <span data-ttu-id="85bc4-135">per l'estensione di file hello.</span><span class="sxs-lookup"><span data-stu-id="85bc4-135">for hello file name extension.</span></span>

<span data-ttu-id="85bc4-136">D: come tooconnect usando REST?</span><span class="sxs-lookup"><span data-stu-id="85bc4-136">Q: How tooconnect using REST?</span></span>

<span data-ttu-id="85bc4-137">R: per informazioni su come tooconnect toohello AMS API, vedere [hello accesso API di servizi multimediali di Azure con autenticazione di Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="85bc4-137">A: For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> <span data-ttu-id="85bc4-138">Dopo avere stabilito la connessione toohttps://media.windows.net, si riceverà un reindirizzamento 301 specificando un altro URI di servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="85bc4-138">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="85bc4-139">È necessario effettuare le chiamate successive toohello nuovo URI.</span><span class="sxs-lookup"><span data-stu-id="85bc4-139">You must make subsequent calls toohello new URI.</span></span> 

<span data-ttu-id="85bc4-140">D: come è possibile ruotare un video durante il processo di codifica hello.</span><span class="sxs-lookup"><span data-stu-id="85bc4-140">Q: How can I rotate a video during hello encoding process.</span></span>

<span data-ttu-id="85bc4-141">R: hello [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supporta rotazione dagli angoli di 90/180 o 270.</span><span class="sxs-lookup"><span data-stu-id="85bc4-141">A: hello [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supports rotation by angles of 90/180/270.</span></span> <span data-ttu-id="85bc4-142">comportamento predefinito di Hello è "Auto", in cui tenta di metadati di rotazione toodetect hello in file MP4/MOV di hello in arrivo e compensare relativo.</span><span class="sxs-lookup"><span data-stu-id="85bc4-142">hello default behavior is "Auto", where it tries toodetect hello rotation metadata in hello incoming MP4/MOV file and compensate for it.</span></span> <span data-ttu-id="85bc4-143">Sono inclusi i seguenti hello **origini** tooone elemento delle impostazioni predefinite di json hello definito [qui](media-services-mes-presets-overview.md):</span><span class="sxs-lookup"><span data-stu-id="85bc4-143">Include hello following **Sources** element tooone of hello json presets defined [here](media-services-mes-presets-overview.md):</span></span>

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


## <a name="media-services-learning-paths"></a><span data-ttu-id="85bc4-144">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="85bc4-144">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="85bc4-145">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="85bc4-145">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
