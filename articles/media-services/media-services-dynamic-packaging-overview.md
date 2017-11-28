---
title: Cenni preliminari sulla creazione dinamica dei pacchetti di servizi multimediali aaaAzure | Documenti Microsoft
description: Consente di argomento Hello e Cenni preliminari sulla creazione dinamica dei pacchetti.
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 0d9e4f54-5daa-45c1-bfaa-cf09ca89b812
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 970e24eba800e098774172c87f56629430b227a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-packaging"></a><span data-ttu-id="9acb4-103">creazione dinamica dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="9acb4-103">Dynamic packaging</span></span>
## <a name="overview"></a><span data-ttu-id="9acb4-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="9acb4-104">Overview</span></span>
<span data-ttu-id="9acb4-105">Servizi multimediali di Microsoft Azure può essere utilizzato toodeliver un'origine multimediale molti formati di file, formati di streaming multimediali e la protezione del contenuto formati tooa varie tecnologie client (ad esempio, iOS, XBOX, Silverlight, Windows 8).</span><span class="sxs-lookup"><span data-stu-id="9acb4-105">Microsoft Azure Media Services can be used toodeliver many media source file formats, media streaming formats, and content protection formats tooa variety of client technologies (for example, iOS, XBOX, Silverlight, Windows 8).</span></span> <span data-ttu-id="9acb4-106">Questi client supportano tuttavia protocolli diversi. iOS, ad esempio, richiede un formato HTTP Live Streaming (HLS) V4, mentre Silverlight e Xbox richiedono Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="9acb4-106">These clients understand different protocols, for example iOS requires an HTTP Live Streaming (HLS) V4 format and Silverlight and Xbox require Smooth Streaming.</span></span> <span data-ttu-id="9acb4-107">Se si dispone di un set di velocità in bit adattiva (più velocità in bit) MP4 file (ISO Base Media 14496-12) o un set di file Smooth Streaming a velocità in bit adattiva che si desidera tooclients tooserve che supportano contenuto MPEG DASH, HLS o Smooth Streaming, è opportuno avvalersi del supporto I servizi di creazione dinamica dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="9acb4-107">If you have a set of adaptive bitrate (multi-bitrate) MP4 (ISO Base Media 14496-12) files or a set of adaptive bitrate Smooth Streaming files that you want tooserve tooclients that understand MPEG DASH, HLS or Smooth Streaming, you should take advantage of Media Services dynamic packaging.</span></span>

<span data-ttu-id="9acb4-108">Creazione di pacchetti dinamiche tutto che il necessario è toocreate un asset che contiene un set di file MP4 o file Smooth Streaming a velocità in bit adattiva.</span><span class="sxs-lookup"><span data-stu-id="9acb4-108">With dynamic packaging all you need is toocreate an asset that contains a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="9acb4-109">Quindi, base hello formato specificato nel manifesto hello o frammentare la richiesta, hello server ti garantisce che il flusso di hello nel protocollo hello che si è scelto di Streaming On Demand.</span><span class="sxs-lookup"><span data-stu-id="9acb4-109">Then, based on hello specified format in hello manifest or fragment request, hello On-Demand Streaming server will ensure that you receive hello stream in hello protocol you have chosen.</span></span> <span data-ttu-id="9acb4-110">Di conseguenza, è necessario solo toostore e pagare per i file hello in unico formato di archiviazione e servizi multimediali creerà e fornirà hello risposta appropriata in base alle richieste da un client.</span><span class="sxs-lookup"><span data-stu-id="9acb4-110">As a result, you only need toostore and pay for hello files in single storage format and Media Services service will build and serve hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="9acb4-111">Hello diagramma seguente mostra la codifica tradizionale hello e flusso di lavoro di creazione statica dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="9acb4-111">hello following diagram shows hello traditional encoding and static packaging workflow.</span></span>

![Codifica statica](./media/media-services-dynamic-packaging-overview/media-services-static-packaging.png)

<span data-ttu-id="9acb4-113">Hello diagramma seguente mostra del flusso di lavoro di hello creazione dinamica dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="9acb4-113">hello following diagram shows hello dynamic packaging workflow.</span></span>

![Codifica dinamica](./media/media-services-dynamic-packaging-overview/media-services-dynamic-packaging.png)


## <a name="common-scenario"></a><span data-ttu-id="9acb4-115">Scenario comune</span><span class="sxs-lookup"><span data-stu-id="9acb4-115">Common scenario</span></span>
1. <span data-ttu-id="9acb4-116">Caricare un file di input (detto file in formato intermedio).</span><span class="sxs-lookup"><span data-stu-id="9acb4-116">Upload an input file (called a mezzanine file).</span></span> <span data-ttu-id="9acb4-117">Ad esempio, h. 264, MP4 o WMV (per l'elenco di hello dei formati supportati, vedere [formati supportati da Media Encoder Standard hello](media-services-media-encoder-standard-formats.md).</span><span class="sxs-lookup"><span data-stu-id="9acb4-117">For example, H.264, MP4, or WMV (for hello list of supported formats see [Formats Supported by hello Media Encoder Standard](media-services-media-encoder-standard-formats.md).</span></span>
2. <span data-ttu-id="9acb4-118">Codificare i set di velocità in bit adattiva in formato intermedio in file MP4 tooH.264.</span><span class="sxs-lookup"><span data-stu-id="9acb4-118">Encode your mezzanine file tooH.264 MP4 adaptive bitrate sets.</span></span>
3. <span data-ttu-id="9acb4-119">Pubblicare l'asset di hello contenente hello velocità in bit adattiva set MP4 creando hello localizzatore su richiesta.</span><span class="sxs-lookup"><span data-stu-id="9acb4-119">Publish hello asset that contains hello adaptive bitrate MP4 set by creating hello On-Demand Locator.</span></span>
4. <span data-ttu-id="9acb4-120">Compilare hello tooaccess gli URL di streaming e lo streaming del contenuto.</span><span class="sxs-lookup"><span data-stu-id="9acb4-120">Build hello streaming URLs tooaccess and stream your content.</span></span>

## <a name="preparing-assets-for-dynamic-streaming"></a><span data-ttu-id="9acb4-121">Preparazione di asset per lo streaming dinamico</span><span class="sxs-lookup"><span data-stu-id="9acb4-121">Preparing assets for dynamic streaming</span></span>
<span data-ttu-id="9acb4-122">tooprepare l'asset per streaming è dinamico sono disponibili due opzioni:</span><span class="sxs-lookup"><span data-stu-id="9acb4-122">tooprepare your asset for dynamic streaming you have two options:</span></span>

1. <span data-ttu-id="9acb4-123">[Caricare un file master](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="9acb4-123">[Upload a master file](media-services-dotnet-upload-files.md).</span></span>
2. <span data-ttu-id="9acb4-124">[Utilizzare set di hello Media Encoder Standard codificatore tooproduce MP4 h. 264 velocità in bit adattiva](media-services-dotnet-encode-with-media-encoder-standard.md).</span><span class="sxs-lookup"><span data-stu-id="9acb4-124">[Use hello Media Encoder Standard encoder tooproduce H.264 MP4 adaptive bitrate sets](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>
3. <span data-ttu-id="9acb4-125">[Trasmettere i contenuti in streaming](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9acb4-125">[Stream your content](media-services-deliver-content-overview.md).</span></span>

## <span data-ttu-id="9acb4-126"><a id="unsupported_formats"></a>Formati non supportati dalla creazione dinamica dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="9acb4-126"><a id="unsupported_formats"></a>Formats that are not supported by dynamic packaging</span></span>
<span data-ttu-id="9acb4-127">Hello seguenti formati di file di origine non sono supportati dalla creazione dinamica dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="9acb4-127">hello following source file formats are not supported by dynamic packaging.</span></span>

* <span data-ttu-id="9acb4-128">File Dolby Digital MP4.</span><span class="sxs-lookup"><span data-stu-id="9acb4-128">Dolby digital mp4 files.</span></span>
* <span data-ttu-id="9acb4-129">File Dolby Digital Smooth.</span><span class="sxs-lookup"><span data-stu-id="9acb4-129">Dolby digital smooth files.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="9acb4-130">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="9acb4-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9acb4-131">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="9acb4-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

