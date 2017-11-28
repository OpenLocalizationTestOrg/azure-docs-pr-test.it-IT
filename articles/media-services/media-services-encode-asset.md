---
title: Panoramica e confronto dei codificatori multimediali su richiesta di Azure | Microsoft Docs
description: Questo argomento offre una panoramica e un confronto tra i codificatori multimediali su richiesta di Azure.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: e6bfc068-fa46-4d68-b1ce-9092c8f3a3c9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: 538a6ab60168735c2626a93cdeedd8d4999a6efc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="overview-and-comparison-of-azure-on-demand-media-encoders"></a><span data-ttu-id="e7d6a-103">Panoramica e confronto dei codificatori multimediali su richiesta di Azure</span><span class="sxs-lookup"><span data-stu-id="e7d6a-103">Overview and comparison of Azure on demand media encoders</span></span>
## <a name="encoding-overview"></a><span data-ttu-id="e7d6a-104">Panoramica della codifica</span><span class="sxs-lookup"><span data-stu-id="e7d6a-104">Encoding overview</span></span>
<span data-ttu-id="e7d6a-105">Servizi multimediali di Azure offre diverse opzioni per la codifica di servizi multimediali nel cloud.</span><span class="sxs-lookup"><span data-stu-id="e7d6a-105">Azure Media Services provides multiple options for the encoding of media in the cloud.</span></span>

<span data-ttu-id="e7d6a-106">Quando si iniziano ad utilizzare i servizi multimediali, è importante comprendere la differenza tra codec e formati di file.</span><span class="sxs-lookup"><span data-stu-id="e7d6a-106">When starting out with Media Services, it is important to understand the difference between codecs and file formats.</span></span>
<span data-ttu-id="e7d6a-107">I codec sono costituiti da software che implementa gli algoritmi di compressione/decompressione, mentre i formati di file sono contenitori che includono il video compresso.</span><span class="sxs-lookup"><span data-stu-id="e7d6a-107">Codecs are the software that implements the compression/decompression algorithms whereas file formats are containers that hold the compressed video.</span></span>

<span data-ttu-id="e7d6a-108">Servizi multimediali include la funzionalità per la creazione dinamica dei pacchetti, che consente di distribuire contenuto con codifica Smooth Streaming o MP4 a bitrate adattivo nei formati supportati da Servizi multimediali, ovvero MPEG-DASH, HLS, Smooth Streaming, senza dover ricreare i pacchetti in questi formati di streaming.</span><span class="sxs-lookup"><span data-stu-id="e7d6a-108">Media Services provides dynamic packaging which allows you to deliver your adaptive bitrate MP4 or Smooth Streaming encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) without you having to re-package into these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="e7d6a-109">Quando l'account AMS viene creato, un endpoint di streaming **predefinito** viene aggiunto all'account con stato **Arrestato**.</span><span class="sxs-lookup"><span data-stu-id="e7d6a-109">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="e7d6a-110">Per avviare lo streaming del contenuto e sfruttare i vantaggi della creazione dinamica dei pacchetti e della crittografia dinamica, l'endpoint di streaming da cui si vuole trasmettere il contenuto deve essere nello stato **In esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="e7d6a-110">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> <span data-ttu-id="e7d6a-111">Per sfruttare i vantaggi del servizio di [creazione dinamica dei pacchetti](media-services-dynamic-packaging-overview.md), è necessario seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="e7d6a-111">To take advantage of [dynamic packaging](media-services-dynamic-packaging-overview.md), you need to do the following:</span></span>
>
><span data-ttu-id="e7d6a-112">Codificare anche il file di origine in un set di file MP4 o Smooth Streaming a velocità in bit adattiva (i passaggi per la codifica sono descritti più avanti in questa esercitazione).</span><span class="sxs-lookup"><span data-stu-id="e7d6a-112">Also, encode your source file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files (the encoding steps are demonstrated later in this tutorial).</span></span>

<span data-ttu-id="e7d6a-113">Servizi multimediali supporta i seguenti codificatori su richiesta descritti in questo articolo:</span><span class="sxs-lookup"><span data-stu-id="e7d6a-113">Media Services supports the following on demand encoders that are described in this article:</span></span>

* [<span data-ttu-id="e7d6a-114">Codificatore multimediale standard</span><span class="sxs-lookup"><span data-stu-id="e7d6a-114">Media Encoder Standard</span></span>](media-services-encode-asset.md#media-encoder-standard)
* [<span data-ttu-id="e7d6a-115">Flusso di lavoro Premium del codificatore multimediale</span><span class="sxs-lookup"><span data-stu-id="e7d6a-115">Media Encoder Premium Workflow</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)

<span data-ttu-id="e7d6a-116">In questo articolo è fornita una breve panoramica dei codificatori multimediali su richiesta e sono presenti collegamenti ad articoli che contengono informazioni più dettagliate.</span><span class="sxs-lookup"><span data-stu-id="e7d6a-116">This article gives a brief overview of on demand media encoders and provides links to articles that give more detailed information.</span></span> <span data-ttu-id="e7d6a-117">L'argomento fornisce inoltre il confronto dei codificatori.</span><span class="sxs-lookup"><span data-stu-id="e7d6a-117">The topic also provides comparison of the encoders.</span></span>

>[!NOTE]
><span data-ttu-id="e7d6a-118">Per impostazione predefinita, in ciascun account di Servizi multimediali può essere attiva una sola attività di codifica alla volta.</span><span class="sxs-lookup"><span data-stu-id="e7d6a-118">By default each Media Services account can have one active encoding task at a time.</span></span> <span data-ttu-id="e7d6a-119">È tuttavia possibile riservare unità di codifica che consentano di eseguire più attività di codifica contemporaneamente, una per ciascuna unità acquistata.</span><span class="sxs-lookup"><span data-stu-id="e7d6a-119">You can reserve encoding units that allow you to have multiple encoding tasks running concurrently, one for each encoding reserved unit you purchase.</span></span> <span data-ttu-id="e7d6a-120">Per informazioni, vedere [Scalabilità dell’unità di codifica](media-services-scale-media-processing-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e7d6a-120">For information, see [Scaling encoding units](media-services-scale-media-processing-overview.md).</span></span>

## <a name="media-encoder-standard"></a><span data-ttu-id="e7d6a-121">Codificatore multimediale standard</span><span class="sxs-lookup"><span data-stu-id="e7d6a-121">Media Encoder Standard</span></span>
### <a name="how-to-use"></a><span data-ttu-id="e7d6a-122">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="e7d6a-122">How to use</span></span>
[<span data-ttu-id="e7d6a-123">Come codificare con Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="e7d6a-123">How to encode with Media Encoder Standard</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)

### <a name="formats"></a><span data-ttu-id="e7d6a-124">Formati</span><span class="sxs-lookup"><span data-stu-id="e7d6a-124">Formats</span></span>
[<span data-ttu-id="e7d6a-125">Codec e formati</span><span class="sxs-lookup"><span data-stu-id="e7d6a-125">Formats and codecs</span></span>](media-services-media-encoder-standard-formats.md)

### <a name="presets"></a><span data-ttu-id="e7d6a-126">Impostazioni predefinite</span><span class="sxs-lookup"><span data-stu-id="e7d6a-126">Presets</span></span>
<span data-ttu-id="e7d6a-127">Media Encoder Standard viene configurato mediante un set di impostazioni descritto [qui](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="e7d6a-127">Media Encoder Standard is configured using one of the encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

### <a name="input-and-output-metadata"></a><span data-ttu-id="e7d6a-128">Metadati di input e output</span><span class="sxs-lookup"><span data-stu-id="e7d6a-128">Input and output metadata</span></span>
<span data-ttu-id="e7d6a-129">I metadati di input dei codificatori sono descritti [qui](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="e7d6a-129">The encoders input metadata is described [here](media-services-input-metadata-schema.md).</span></span>

<span data-ttu-id="e7d6a-130">I metadati di output dei codificatori sono descritti [qui](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="e7d6a-130">The encoders output metadata is described [here](media-services-output-metadata-schema.md).</span></span>

### <a name="generate-thumbnails"></a><span data-ttu-id="e7d6a-131">Generare anteprime</span><span class="sxs-lookup"><span data-stu-id="e7d6a-131">Generate thumbnails</span></span>
<span data-ttu-id="e7d6a-132">Per informazioni, vedere l'argomento [Come generare anteprime utilizzando Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).</span><span class="sxs-lookup"><span data-stu-id="e7d6a-132">For information, see [How to generate thumbnails using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).</span></span>

### <a name="trim-videos-clipping"></a><span data-ttu-id="e7d6a-133">Tagliare video (ritaglio)</span><span class="sxs-lookup"><span data-stu-id="e7d6a-133">Trim videos (clipping)</span></span>
<span data-ttu-id="e7d6a-134">Per informazioni, vedere [Come tagliare video usando Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video).</span><span class="sxs-lookup"><span data-stu-id="e7d6a-134">For information, see [How to trim videos using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video).</span></span>

### <a name="create-overlays"></a><span data-ttu-id="e7d6a-135">Creare sovrimpressioni</span><span class="sxs-lookup"><span data-stu-id="e7d6a-135">Create overlays</span></span>
<span data-ttu-id="e7d6a-136">Per informazioni, vedere [Come creare sovrimpressioni usando Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay).</span><span class="sxs-lookup"><span data-stu-id="e7d6a-136">For information, see [How to create overlays using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

### <a name="see-also"></a><span data-ttu-id="e7d6a-137">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="e7d6a-137">See also</span></span>
[<span data-ttu-id="e7d6a-138">Blog di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="e7d6a-138">The Media Services blog</span></span>](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/)

## <a name="media-encoder-premium-workflow"></a><span data-ttu-id="e7d6a-139">Flusso di lavoro Premium del codificatore multimediale</span><span class="sxs-lookup"><span data-stu-id="e7d6a-139">Media Encoder Premium Workflow</span></span>
### <a name="overview"></a><span data-ttu-id="e7d6a-140">Overview</span><span class="sxs-lookup"><span data-stu-id="e7d6a-140">Overview</span></span>
[<span data-ttu-id="e7d6a-141">Introduzione alla codifica Premium in Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="e7d6a-141">Introducing Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/)

### <a name="how-to-use"></a><span data-ttu-id="e7d6a-142">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="e7d6a-142">How to use</span></span>
<span data-ttu-id="e7d6a-143">Il flusso di lavoro Premium del codificatore multimediale viene configurato usando flussi di lavoro complessi.</span><span class="sxs-lookup"><span data-stu-id="e7d6a-143">Media Encoder Premium Workflow is configured using complex workflows.</span></span> <span data-ttu-id="e7d6a-144">Per creare e aggiornare i file di un flusso di lavoro, è possibile usare lo strumento [Progettazione flussi di lavoro](media-services-workflow-designer.md) .</span><span class="sxs-lookup"><span data-stu-id="e7d6a-144">Workflow files could be created and updated using the [Workflow Designer](media-services-workflow-designer.md) tool.</span></span>

[<span data-ttu-id="e7d6a-145">Come usare la codifica Premium in Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="e7d6a-145">How to Use Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services/)

### <a name="known-issues"></a><span data-ttu-id="e7d6a-146">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="e7d6a-146">Known issues</span></span>
<span data-ttu-id="e7d6a-147">Se il video di input non contiene i sottotitoli codificati, l'asset di output conterrà comunque un file TTML vuoto.</span><span class="sxs-lookup"><span data-stu-id="e7d6a-147">If your input video does not contain closed captioning, the output Asset will still contain an empty TTML file.</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="e7d6a-148">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="e7d6a-148">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e7d6a-149">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="e7d6a-149">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="e7d6a-150">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="e7d6a-150">Related articles</span></span>
* [<span data-ttu-id="e7d6a-151">Eseguire attività di codifica avanzata personalizzando i set di impostazioni di Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="e7d6a-151">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="e7d6a-152">Quote e limitazioni</span><span class="sxs-lookup"><span data-stu-id="e7d6a-152">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
