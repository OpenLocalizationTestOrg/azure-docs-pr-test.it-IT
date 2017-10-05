---
title: Panoramica della creazione dinamica dei pacchetti di Servizi multimediali di Azure | Documentazione Microsoft
description: Questo argomento fornisce una panoramica della creazione dinamica dei pacchetti.
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
ms.openlocfilehash: 2d212599302fced3f60085ab30cdeaefc1ee2e6a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="dynamic-packaging"></a><span data-ttu-id="d9414-103">Creazione dinamica dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="d9414-103">Dynamic packaging</span></span>
## <a name="overview"></a><span data-ttu-id="d9414-104">Overview</span><span class="sxs-lookup"><span data-stu-id="d9414-104">Overview</span></span>
<span data-ttu-id="d9414-105">Servizi multimediali di Microsoft Azure può essere usato per distribuire molti formati di file di origine multimediali, formati di streaming multimediali e formati di protezione del contenuto in un'ampia gamma di tecnologie client, ad esempio iOS, Xbox, Silverlight e Windows 8.</span><span class="sxs-lookup"><span data-stu-id="d9414-105">Microsoft Azure Media Services can be used to deliver many media source file formats, media streaming formats, and content protection formats to a variety of client technologies (for example, iOS, XBOX, Silverlight, Windows 8).</span></span> <span data-ttu-id="d9414-106">Questi client supportano tuttavia protocolli diversi. iOS, ad esempio, richiede un formato HTTP Live Streaming (HLS) V4, mentre Silverlight e Xbox richiedono Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="d9414-106">These clients understand different protocols, for example iOS requires an HTTP Live Streaming (HLS) V4 format and Silverlight and Xbox require Smooth Streaming.</span></span> <span data-ttu-id="d9414-107">Se è presente un set di file MP4 a velocità in bit adattiva, ovvero più velocità in bit, (ISO Base Media 14496-12) o di un set di file Smooth Streaming a velocità in bit adattiva e si vuole renderli disponibili per i client che supportano contenuto MPEG DASH, HLS o Smooth Streaming, è possibile usare la funzionalità di creazione dinamica dei pacchetti di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="d9414-107">If you have a set of adaptive bitrate (multi-bitrate) MP4 (ISO Base Media 14496-12) files or a set of adaptive bitrate Smooth Streaming files that you want to serve to clients that understand MPEG DASH, HLS or Smooth Streaming, you should take advantage of Media Services dynamic packaging.</span></span>

<span data-ttu-id="d9414-108">Con la funzionalità di creazione dinamica dei pacchetti, è sufficiente creare un asset che contenga un set di file MP4 o Smooth Streaming a velocità in bit adattiva.</span><span class="sxs-lookup"><span data-stu-id="d9414-108">With dynamic packaging all you need is to create an asset that contains a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="d9414-109">In base al formato specificato nella richiesta del manifesto o del frammento, il server di streaming on demand garantirà che il flusso sia ricevuto nel protocollo scelto.</span><span class="sxs-lookup"><span data-stu-id="d9414-109">Then, based on the specified format in the manifest or fragment request, the On-Demand Streaming server will ensure that you receive the stream in the protocol you have chosen.</span></span> <span data-ttu-id="d9414-110">Di conseguenza, si archiviano e si pagano solo i file in un singolo formato di archiviazione e il servizio Servizi multimediali crea e fornisce la risposta appropriata in base alle richieste di un client.</span><span class="sxs-lookup"><span data-stu-id="d9414-110">As a result, you only need to store and pay for the files in single storage format and Media Services service will build and serve the appropriate response based on requests from a client.</span></span>

<span data-ttu-id="d9414-111">Il diagramma seguente mostra il flusso di lavoro tradizionale di codifica e creazione statica dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="d9414-111">The following diagram shows the traditional encoding and static packaging workflow.</span></span>

![Codifica statica](./media/media-services-dynamic-packaging-overview/media-services-static-packaging.png)

<span data-ttu-id="d9414-113">Il diagramma seguente mostra il flusso di lavoro di creazione dinamica dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="d9414-113">The following diagram shows the dynamic packaging workflow.</span></span>

![Codifica dinamica](./media/media-services-dynamic-packaging-overview/media-services-dynamic-packaging.png)


## <a name="common-scenario"></a><span data-ttu-id="d9414-115">Scenario comune</span><span class="sxs-lookup"><span data-stu-id="d9414-115">Common scenario</span></span>
1. <span data-ttu-id="d9414-116">Caricare un file di input (detto file in formato intermedio).</span><span class="sxs-lookup"><span data-stu-id="d9414-116">Upload an input file (called a mezzanine file).</span></span> <span data-ttu-id="d9414-117">Ad esempio, H.264, MP4 o WMV (per l'elenco dei formati supportati, vedere [Formati e codec Media Encoder Standard](media-services-media-encoder-standard-formats.md)).</span><span class="sxs-lookup"><span data-stu-id="d9414-117">For example, H.264, MP4, or WMV (for the list of supported formats see [Formats Supported by the Media Encoder Standard](media-services-media-encoder-standard-formats.md).</span></span>
2. <span data-ttu-id="d9414-118">Codificare il file in formato intermedio in set MP4 a velocità in bit adattiva H.264.</span><span class="sxs-lookup"><span data-stu-id="d9414-118">Encode your mezzanine file to H.264 MP4 adaptive bitrate sets.</span></span>
3. <span data-ttu-id="d9414-119">Pubblicare l'asset contenente il set MP4 a velocità in bit adattiva creando il localizzatore su richiesta.</span><span class="sxs-lookup"><span data-stu-id="d9414-119">Publish the asset that contains the adaptive bitrate MP4 set by creating the On-Demand Locator.</span></span>
4. <span data-ttu-id="d9414-120">Creare gli URL di streaming per accedere e al contenuto e trasmetterlo in streaming.</span><span class="sxs-lookup"><span data-stu-id="d9414-120">Build the streaming URLs to access and stream your content.</span></span>

## <a name="preparing-assets-for-dynamic-streaming"></a><span data-ttu-id="d9414-121">Preparazione di asset per lo streaming dinamico</span><span class="sxs-lookup"><span data-stu-id="d9414-121">Preparing assets for dynamic streaming</span></span>
<span data-ttu-id="d9414-122">Per preparare l'asset per lo streaming dinamico sono disponibili due opzioni:</span><span class="sxs-lookup"><span data-stu-id="d9414-122">To prepare your asset for dynamic streaming you have two options:</span></span>

1. <span data-ttu-id="d9414-123">[Caricare un file master](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="d9414-123">[Upload a master file](media-services-dotnet-upload-files.md).</span></span>
2. <span data-ttu-id="d9414-124">[Usare il codificatore Media Encoder Standard per generare set MP4 velocità in bit adattiva H.264](media-services-dotnet-encode-with-media-encoder-standard.md).</span><span class="sxs-lookup"><span data-stu-id="d9414-124">[Use the Media Encoder Standard encoder to produce H.264 MP4 adaptive bitrate sets](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>
3. <span data-ttu-id="d9414-125">[Trasmettere i contenuti in streaming](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d9414-125">[Stream your content](media-services-deliver-content-overview.md).</span></span>

## <span data-ttu-id="d9414-126"><a id="unsupported_formats"></a>Formati non supportati dalla creazione dinamica dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="d9414-126"><a id="unsupported_formats"></a>Formats that are not supported by dynamic packaging</span></span>
<span data-ttu-id="d9414-127">I formati di file di origine seguenti non sono supportati dalla creazione dinamica dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="d9414-127">The following source file formats are not supported by dynamic packaging.</span></span>

* <span data-ttu-id="d9414-128">File Dolby Digital MP4.</span><span class="sxs-lookup"><span data-stu-id="d9414-128">Dolby digital mp4 files.</span></span>
* <span data-ttu-id="d9414-129">File Dolby Digital Smooth.</span><span class="sxs-lookup"><span data-stu-id="d9414-129">Dolby digital smooth files.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="d9414-130">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="d9414-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d9414-131">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="d9414-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

