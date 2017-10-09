---
title: aaaOverview e confronto di Azure su richiesta codificatori supporti | Documenti Microsoft
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
ms.openlocfilehash: 24a3e0a16162b1bebfcde290b6baf2dd8dbfff17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-and-comparison-of-azure-on-demand-media-encoders"></a><span data-ttu-id="a2fc4-103">Panoramica e confronto dei codificatori multimediali su richiesta di Azure</span><span class="sxs-lookup"><span data-stu-id="a2fc4-103">Overview and comparison of Azure on demand media encoders</span></span>
## <a name="encoding-overview"></a><span data-ttu-id="a2fc4-104">Panoramica della codifica</span><span class="sxs-lookup"><span data-stu-id="a2fc4-104">Encoding overview</span></span>
<span data-ttu-id="a2fc4-105">Servizi multimediali di Azure fornisce più opzioni per la codifica dei file multimediali in cloud hello hello.</span><span class="sxs-lookup"><span data-stu-id="a2fc4-105">Azure Media Services provides multiple options for hello encoding of media in hello cloud.</span></span>

<span data-ttu-id="a2fc4-106">Quando si avvia con servizi multimediali, è importante toounderstand differenza di hello tra codec e formati di file.</span><span class="sxs-lookup"><span data-stu-id="a2fc4-106">When starting out with Media Services, it is important toounderstand hello difference between codecs and file formats.</span></span>
<span data-ttu-id="a2fc4-107">Codec sono costituiti da software hello che implementa gli algoritmi di compressione/decompressione hello, mentre i formati di file sono contenitori che includono il video compresso hello.</span><span class="sxs-lookup"><span data-stu-id="a2fc4-107">Codecs are hello software that implements hello compression/decompression algorithms whereas file formats are containers that hold hello compressed video.</span></span>

<span data-ttu-id="a2fc4-108">Servizi multimediali fornisce creazione dinamica dei pacchetti che consente la velocità in bit adattiva MP4 o Smooth Streaming con codifica contenuto in streaming formati supportati da servizi multimediali (MPEG DASH, HLS, Smooth Streaming) toodeliver senza che sia necessario toore-package in questi formati di streaming.</span><span class="sxs-lookup"><span data-stu-id="a2fc4-108">Media Services provides dynamic packaging which allows you toodeliver your adaptive bitrate MP4 or Smooth Streaming encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) without you having toore-package into these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="a2fc4-109">Quando viene creato l'account di sistema AMS un **predefinito** endpoint di streaming viene aggiunto l'account tooyour in hello **arrestato** stato.</span><span class="sxs-lookup"><span data-stu-id="a2fc4-109">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="a2fc4-110">lo streaming del contenuto e intraprendere sfruttare creazione dinamica dei pacchetti e la crittografia dinamica, toostart hello endpoint di streaming da cui si desidera in hello del contenuto toostream è toobe **esecuzione** stato.</span><span class="sxs-lookup"><span data-stu-id="a2fc4-110">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> <span data-ttu-id="a2fc4-111">sfruttare tootake [creazione dinamica dei pacchetti](media-services-dynamic-packaging-overview.md), è necessario toodo hello segue:</span><span class="sxs-lookup"><span data-stu-id="a2fc4-111">tootake advantage of [dynamic packaging](media-services-dynamic-packaging-overview.md), you need toodo hello following:</span></span>
>
><span data-ttu-id="a2fc4-112">Inoltre, è possibile codificare il file di origine in un set di file MP4 o file Smooth Streaming a velocità in bit adattiva (passaggi codifica hello sono illustrati più avanti in questa esercitazione).</span><span class="sxs-lookup"><span data-stu-id="a2fc4-112">Also, encode your source file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files (hello encoding steps are demonstrated later in this tutorial).</span></span>

<span data-ttu-id="a2fc4-113">Servizi multimediali supporta i seguenti hello in codificatori di richiesta che sono descritte in questo articolo:</span><span class="sxs-lookup"><span data-stu-id="a2fc4-113">Media Services supports hello following on demand encoders that are described in this article:</span></span>

* [<span data-ttu-id="a2fc4-114">Codificatore multimediale standard</span><span class="sxs-lookup"><span data-stu-id="a2fc4-114">Media Encoder Standard</span></span>](media-services-encode-asset.md#media-encoder-standard)
* [<span data-ttu-id="a2fc4-115">Flusso di lavoro Premium del codificatore multimediale</span><span class="sxs-lookup"><span data-stu-id="a2fc4-115">Media Encoder Premium Workflow</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)

<span data-ttu-id="a2fc4-116">In questo articolo offre una breve panoramica su richiesta codificatori media e fornisce collegamenti tooarticles che offrono informazioni più dettagliate.</span><span class="sxs-lookup"><span data-stu-id="a2fc4-116">This article gives a brief overview of on demand media encoders and provides links tooarticles that give more detailed information.</span></span> <span data-ttu-id="a2fc4-117">argomento Hello fornisce inoltre il confronto dei codificatori hello.</span><span class="sxs-lookup"><span data-stu-id="a2fc4-117">hello topic also provides comparison of hello encoders.</span></span>

>[!NOTE]
><span data-ttu-id="a2fc4-118">Per impostazione predefinita, in ciascun account di Servizi multimediali può essere attiva una sola attività di codifica alla volta.</span><span class="sxs-lookup"><span data-stu-id="a2fc4-118">By default each Media Services account can have one active encoding task at a time.</span></span> <span data-ttu-id="a2fc4-119">È possibile riservare unità di codifica che consentono di toohave più attività di codifica contemporaneamente, uno per ciascuna unità acquistata.</span><span class="sxs-lookup"><span data-stu-id="a2fc4-119">You can reserve encoding units that allow you toohave multiple encoding tasks running concurrently, one for each encoding reserved unit you purchase.</span></span> <span data-ttu-id="a2fc4-120">Per informazioni, vedere [Scalabilità dell’unità di codifica](media-services-scale-media-processing-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a2fc4-120">For information, see [Scaling encoding units](media-services-scale-media-processing-overview.md).</span></span>

## <a name="media-encoder-standard"></a><span data-ttu-id="a2fc4-121">Codificatore multimediale standard</span><span class="sxs-lookup"><span data-stu-id="a2fc4-121">Media Encoder Standard</span></span>
### <a name="how-toouse"></a><span data-ttu-id="a2fc4-122">Come toouse</span><span class="sxs-lookup"><span data-stu-id="a2fc4-122">How toouse</span></span>
[<span data-ttu-id="a2fc4-123">Come tooencode con Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="a2fc4-123">How tooencode with Media Encoder Standard</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)

### <a name="formats"></a><span data-ttu-id="a2fc4-124">Formati</span><span class="sxs-lookup"><span data-stu-id="a2fc4-124">Formats</span></span>
[<span data-ttu-id="a2fc4-125">Codec e formati</span><span class="sxs-lookup"><span data-stu-id="a2fc4-125">Formats and codecs</span></span>](media-services-media-encoder-standard-formats.md)

### <a name="presets"></a><span data-ttu-id="a2fc4-126">Impostazioni predefinite</span><span class="sxs-lookup"><span data-stu-id="a2fc4-126">Presets</span></span>
<span data-ttu-id="a2fc4-127">Media Encoder Standard viene configurato usando uno dei set di impostazioni di codificatore hello descritto [qui](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="a2fc4-127">Media Encoder Standard is configured using one of hello encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

### <a name="input-and-output-metadata"></a><span data-ttu-id="a2fc4-128">Metadati di input e output</span><span class="sxs-lookup"><span data-stu-id="a2fc4-128">Input and output metadata</span></span>
<span data-ttu-id="a2fc4-129">Hello codificatori dei metadati di input sono descritto [qui](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="a2fc4-129">hello encoders input metadata is described [here](media-services-input-metadata-schema.md).</span></span>

<span data-ttu-id="a2fc4-130">Hello codificatori output metadati descritto [qui](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="a2fc4-130">hello encoders output metadata is described [here](media-services-output-metadata-schema.md).</span></span>

### <a name="generate-thumbnails"></a><span data-ttu-id="a2fc4-131">Generare anteprime</span><span class="sxs-lookup"><span data-stu-id="a2fc4-131">Generate thumbnails</span></span>
<span data-ttu-id="a2fc4-132">Per informazioni, vedere [come anteprime toogenerate usando Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).</span><span class="sxs-lookup"><span data-stu-id="a2fc4-132">For information, see [How toogenerate thumbnails using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).</span></span>

### <a name="trim-videos-clipping"></a><span data-ttu-id="a2fc4-133">Tagliare video (ritaglio)</span><span class="sxs-lookup"><span data-stu-id="a2fc4-133">Trim videos (clipping)</span></span>
<span data-ttu-id="a2fc4-134">Per informazioni, vedere [come video tootrim Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video).</span><span class="sxs-lookup"><span data-stu-id="a2fc4-134">For information, see [How tootrim videos using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video).</span></span>

### <a name="create-overlays"></a><span data-ttu-id="a2fc4-135">Creare sovrimpressioni</span><span class="sxs-lookup"><span data-stu-id="a2fc4-135">Create overlays</span></span>
<span data-ttu-id="a2fc4-136">Per informazioni, vedere [come sovrapposizioni toocreate usando Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay).</span><span class="sxs-lookup"><span data-stu-id="a2fc4-136">For information, see [How toocreate overlays using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

### <a name="see-also"></a><span data-ttu-id="a2fc4-137">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="a2fc4-137">See also</span></span>
[<span data-ttu-id="a2fc4-138">blog di servizi multimediali Hello</span><span class="sxs-lookup"><span data-stu-id="a2fc4-138">hello Media Services blog</span></span>](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/)

## <a name="media-encoder-premium-workflow"></a><span data-ttu-id="a2fc4-139">Flusso di lavoro Premium del codificatore multimediale</span><span class="sxs-lookup"><span data-stu-id="a2fc4-139">Media Encoder Premium Workflow</span></span>
### <a name="overview"></a><span data-ttu-id="a2fc4-140">Overview</span><span class="sxs-lookup"><span data-stu-id="a2fc4-140">Overview</span></span>
[<span data-ttu-id="a2fc4-141">Introduzione alla codifica Premium in Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="a2fc4-141">Introducing Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/)

### <a name="how-toouse"></a><span data-ttu-id="a2fc4-142">Come toouse</span><span class="sxs-lookup"><span data-stu-id="a2fc4-142">How toouse</span></span>
<span data-ttu-id="a2fc4-143">Il flusso di lavoro Premium del codificatore multimediale viene configurato usando flussi di lavoro complessi.</span><span class="sxs-lookup"><span data-stu-id="a2fc4-143">Media Encoder Premium Workflow is configured using complex workflows.</span></span> <span data-ttu-id="a2fc4-144">I file del flusso di lavoro può essere creati e aggiornato utilizzando hello [Progettazione flussi di lavoro](media-services-workflow-designer.md) strumento.</span><span class="sxs-lookup"><span data-stu-id="a2fc4-144">Workflow files could be created and updated using hello [Workflow Designer](media-services-workflow-designer.md) tool.</span></span>

[<span data-ttu-id="a2fc4-145">Come tooUse codifica Premium in servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="a2fc4-145">How tooUse Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services/)

### <a name="known-issues"></a><span data-ttu-id="a2fc4-146">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="a2fc4-146">Known issues</span></span>
<span data-ttu-id="a2fc4-147">Se il video di input non contiene sottotitoli, hello output che asset conterrà comunque un file TTML vuoto.</span><span class="sxs-lookup"><span data-stu-id="a2fc4-147">If your input video does not contain closed captioning, hello output Asset will still contain an empty TTML file.</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="a2fc4-148">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="a2fc4-148">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a2fc4-149">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="a2fc4-149">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="a2fc4-150">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="a2fc4-150">Related articles</span></span>
* [<span data-ttu-id="a2fc4-151">Eseguire attività di codifica avanzata personalizzando i set di impostazioni di Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="a2fc4-151">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="a2fc4-152">Quote e limitazioni</span><span class="sxs-lookup"><span data-stu-id="a2fc4-152">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
