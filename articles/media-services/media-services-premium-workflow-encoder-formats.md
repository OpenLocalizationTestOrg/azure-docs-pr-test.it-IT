---
title: flusso di lavoro Premium del codificatore aaaMedia codec e formati | Documenti Microsoft
description: Questo argomento offre una panoramica dei codec e dei formati del flusso di lavoro Premium del codificatore multimediale
services: media-services
documentationcenter: 
author: juliako
manager: erik43
editor: 
ms.assetid: b197fce8-3b9b-4189-8d08-486810c0426f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;anilmur
ms.openlocfilehash: e781384ca8f08926f00c83b6710fd413ce2a3e1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="media-encoder-premium-workflow-formats-and-codecs"></a><span data-ttu-id="f26e6-103">Codec e formati del flusso di lavoro Premium del codificatore multimediale</span><span class="sxs-lookup"><span data-stu-id="f26e6-103">Media Encoder Premium Workflow formats and codecs</span></span>
> [!NOTE]
> <span data-ttu-id="f26e6-104">Per domande relative al codificatore Premium, inviare mepd tramite un messaggio di posta elettronica a Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="f26e6-104">For premium encoder questions, email mepd at Microsoft.com.</span></span>
> 
> <span data-ttu-id="f26e6-105">Il processore di contenuti multimediali del flusso di lavoro Premium del codificatore multimediale descritto in questo argomento non è disponibile in Cina.</span><span class="sxs-lookup"><span data-stu-id="f26e6-105">Media Encoder Premium Workflow media processor discussed in this topic is not available in China.</span></span> 
> 
> 

<span data-ttu-id="f26e6-106">Questo documento contiene un elenco di formati di file di input e output e i codec che sono supportati dalla versione di anteprima pubblica di hello di hello **flusso di lavoro Premium del codificatore multimediale** codificatore.</span><span class="sxs-lookup"><span data-stu-id="f26e6-106">This document contains a list of input and output file formats and codecs that are supported by hello public preview version of hello **Media Encoder Premium Workflow** encoder.</span></span>

[<span data-ttu-id="f26e6-107">Codec e formati di input del flusso di lavoro Premium del codificatore multimediale</span><span class="sxs-lookup"><span data-stu-id="f26e6-107">Media Encoder Premium Worflow Input Formats and Codecs</span></span>](#input_formats)

[<span data-ttu-id="f26e6-108">Codec e formati di output del flusso di lavoro Premium del codificatore multimediale</span><span class="sxs-lookup"><span data-stu-id="f26e6-108">Media Encoder Premium Worflow Output Formats and Codecs</span></span>](#output_formats)

<span data-ttu-id="f26e6-109">**flusso di lavoro Premium del codificatore multimediale** supporta i sottotitoli codificati descritti in [questa](#closed_captioning) sezione.</span><span class="sxs-lookup"><span data-stu-id="f26e6-109">**Media Encoder Premium Workflow** supports closed captioning described in [this](#closed_captioning) section.</span></span> 

## <span data-ttu-id="f26e6-110"><a id="input_formats"></a>Codec e formati di input del flusso di lavoro Premium del codificatore multimediale</span><span class="sxs-lookup"><span data-stu-id="f26e6-110"><a id="input_formats"></a>Media Encoder Premium Workflow Input Formats and Codecs</span></span>
<span data-ttu-id="f26e6-111">Hello seguente sezione vengono elencate hello codec e formati di file che supporta il processore di contenuti multimediali come input.</span><span class="sxs-lookup"><span data-stu-id="f26e6-111">hello following section lists hello codecs and file formats that this media processor supports as input.</span></span>

### <a name="input-containerfile-formats"></a><span data-ttu-id="f26e6-112">Contenitore di input/formati di file</span><span class="sxs-lookup"><span data-stu-id="f26e6-112">Input Container/File Formats</span></span>
* <span data-ttu-id="f26e6-113">Adobe® Flash® F4V</span><span class="sxs-lookup"><span data-stu-id="f26e6-113">Adobe® Flash® F4V</span></span>
* <span data-ttu-id="f26e6-114">MXF/SMPTE 377M</span><span class="sxs-lookup"><span data-stu-id="f26e6-114">MXF/SMPTE 377M</span></span>
* <span data-ttu-id="f26e6-115">GXF</span><span class="sxs-lookup"><span data-stu-id="f26e6-115">GXF</span></span>
* <span data-ttu-id="f26e6-116">MPEG-2 Transport Stream</span><span class="sxs-lookup"><span data-stu-id="f26e6-116">MPEG-2 Transport Streams</span></span>
* <span data-ttu-id="f26e6-117">MPEG-2 Program Stream</span><span class="sxs-lookup"><span data-stu-id="f26e6-117">MPEG-2 Program Streams</span></span>
* <span data-ttu-id="f26e6-118">MPEG-4/MP4</span><span class="sxs-lookup"><span data-stu-id="f26e6-118">MPEG-4/MP4</span></span>
* <span data-ttu-id="f26e6-119">Windows Media/ASF</span><span class="sxs-lookup"><span data-stu-id="f26e6-119">Windows Media/ASF</span></span>
* <span data-ttu-id="f26e6-120">AVI (non compresso 8 bit/10 bit)</span><span class="sxs-lookup"><span data-stu-id="f26e6-120">AVI (Uncompressed 8bit/10bit)</span></span>

### <a name="input-video-codecs"></a><span data-ttu-id="f26e6-121">Codec video di input</span><span class="sxs-lookup"><span data-stu-id="f26e6-121">Input Video Codecs</span></span>
* <span data-ttu-id="f26e6-122">AVC 8 bit/10 bit, di too4:2:2, tra cui AVCIntra</span><span class="sxs-lookup"><span data-stu-id="f26e6-122">AVC 8-bit/10-bit, up too4:2:2, including AVCIntra</span></span>
* <span data-ttu-id="f26e6-123">Avid DNxHD (in MXF)</span><span class="sxs-lookup"><span data-stu-id="f26e6-123">Avid DNxHD (in MXF)</span></span>
* <span data-ttu-id="f26e6-124">DVCPro/DVCProHD (in MXF)</span><span class="sxs-lookup"><span data-stu-id="f26e6-124">DVCPro/DVCProHD (in MXF)</span></span>
* <span data-ttu-id="f26e6-125">JPEG2000</span><span class="sxs-lookup"><span data-stu-id="f26e6-125">JPEG2000</span></span>
* <span data-ttu-id="f26e6-126">MPEG-2 (backup too422 profilo e di livello elevato, ad esempio varianti XDCAM, XDCAM HD, XDCAM IMX, CableLabs® e D10)</span><span class="sxs-lookup"><span data-stu-id="f26e6-126">MPEG-2 (up too422 Profile and High Level; including variants such as XDCAM, XDCAM HD, XDCAM IMX, CableLabs® and D10)</span></span>
* <span data-ttu-id="f26e6-127">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="f26e6-127">MPEG-1</span></span>
* <span data-ttu-id="f26e6-128">Windows Media Video/VC-1</span><span class="sxs-lookup"><span data-stu-id="f26e6-128">Windows Media Video/VC-1</span></span>

### <a name="input-audio-codecs"></a><span data-ttu-id="f26e6-129">Codec audio di input</span><span class="sxs-lookup"><span data-stu-id="f26e6-129">Input Audio Codecs</span></span>
* <span data-ttu-id="f26e6-130">AES (SMPTE 331M e 302M, AES3-2003)</span><span class="sxs-lookup"><span data-stu-id="f26e6-130">AES (SMPTE 331M and 302M, AES3-2003)</span></span>
* <span data-ttu-id="f26e6-131">Dolby® E</span><span class="sxs-lookup"><span data-stu-id="f26e6-131">Dolby® E</span></span>
* <span data-ttu-id="f26e6-132">Dolby® Digital (AC3)</span><span class="sxs-lookup"><span data-stu-id="f26e6-132">Dolby® Digital (AC3)</span></span>
* <span data-ttu-id="f26e6-133">AAC (AAC-LC, HE-AAC e AAC-HEv2; backup too5.1)</span><span class="sxs-lookup"><span data-stu-id="f26e6-133">AAC (AAC-LC, AAC-HE, and AAC-HEv2; up too5.1)</span></span>
* <span data-ttu-id="f26e6-134">MPEG Layer 2</span><span class="sxs-lookup"><span data-stu-id="f26e6-134">MPEG Layer 2</span></span>
* <span data-ttu-id="f26e6-135">MP3 (MPEG-1 Audio Layer 3)</span><span class="sxs-lookup"><span data-stu-id="f26e6-135">MP3 (MPEG-1 Audio Layer 3)</span></span>
* <span data-ttu-id="f26e6-136">Windows Media Audio</span><span class="sxs-lookup"><span data-stu-id="f26e6-136">Windows Media Audio</span></span>
* <span data-ttu-id="f26e6-137">WAV/PCM</span><span class="sxs-lookup"><span data-stu-id="f26e6-137">WAV/PCM</span></span>

## <span data-ttu-id="f26e6-138"><a id="output_format"></a>Codec e formati di output del flusso di lavoro Premium del codificatore multimediale</span><span class="sxs-lookup"><span data-stu-id="f26e6-138"><a id="output_format"></a>Media Encoder Premium Workflow Output Formats and Codecs</span></span>
<span data-ttu-id="f26e6-139">Hello nella sezione seguente sono elencati hello codec e formati di file che sono supportati come output di questo processore di contenuti multimediali.</span><span class="sxs-lookup"><span data-stu-id="f26e6-139">hello following section lists hello codecs and file formats that are supported as output from this media processor.</span></span>

### <a name="output-containerfile-formats"></a><span data-ttu-id="f26e6-140">Contenitore di output/formati di file</span><span class="sxs-lookup"><span data-stu-id="f26e6-140">Output Container/File Formats</span></span>
* <span data-ttu-id="f26e6-141">Adobe® Flash® F4V</span><span class="sxs-lookup"><span data-stu-id="f26e6-141">Adobe® Flash® F4V</span></span>
* <span data-ttu-id="f26e6-142">MXF (OP1a, XDCAM e AS02)</span><span class="sxs-lookup"><span data-stu-id="f26e6-142">MXF (OP1a, XDCAM and AS02)</span></span>
* <span data-ttu-id="f26e6-143">DPP (incluso AS11)</span><span class="sxs-lookup"><span data-stu-id="f26e6-143">DPP (including AS11)</span></span>
* <span data-ttu-id="f26e6-144">GXF</span><span class="sxs-lookup"><span data-stu-id="f26e6-144">GXF</span></span>
* <span data-ttu-id="f26e6-145">MPEG-4/MP4</span><span class="sxs-lookup"><span data-stu-id="f26e6-145">MPEG-4/MP4</span></span>
* <span data-ttu-id="f26e6-146">Windows Media/ASF</span><span class="sxs-lookup"><span data-stu-id="f26e6-146">Windows Media/ASF</span></span>
* <span data-ttu-id="f26e6-147">AVI (non compresso 8 bit/10 bit)</span><span class="sxs-lookup"><span data-stu-id="f26e6-147">AVI (Uncompressed 8bit/10bit)</span></span>
* <span data-ttu-id="f26e6-148">Formato di file Smooth Streaming (PIFF 1.3)</span><span class="sxs-lookup"><span data-stu-id="f26e6-148">Smooth Streaming File Format (PIFF 1.3)</span></span>
* <span data-ttu-id="f26e6-149">MPEG-TS</span><span class="sxs-lookup"><span data-stu-id="f26e6-149">MPEG-TS</span></span> 

### <a name="output-video-codecs"></a><span data-ttu-id="f26e6-150">Codec video di output</span><span class="sxs-lookup"><span data-stu-id="f26e6-150">Output Video Codecs</span></span>
* <span data-ttu-id="f26e6-151">AVC (h. 264; 8 bit; backup tooHigh profilo, livello 5.2; HD Ultra 4K. All'interno di AVC)</span><span class="sxs-lookup"><span data-stu-id="f26e6-151">AVC (H.264; 8-bit; up tooHigh Profile, Level 5.2; 4K Ultra HD; AVC Intra)</span></span>
* <span data-ttu-id="f26e6-152">Avid DNxHD (in MXF)</span><span class="sxs-lookup"><span data-stu-id="f26e6-152">Avid DNxHD (in MXF)</span></span>
* <span data-ttu-id="f26e6-153">DVCPro/DVCProHD (in MXF)</span><span class="sxs-lookup"><span data-stu-id="f26e6-153">DVCPro/DVCProHD (in MXF)</span></span>
* <span data-ttu-id="f26e6-154">MPEG-2 (backup too422 profilo e di livello elevato, ad esempio varianti XDCAM, XDCAM HD, XDCAM IMX, CableLabs® e D10)</span><span class="sxs-lookup"><span data-stu-id="f26e6-154">MPEG-2 (up too422 Profile and High Level; including variants such as XDCAM, XDCAM HD, XDCAM IMX, CableLabs® and D10)</span></span>
* <span data-ttu-id="f26e6-155">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="f26e6-155">MPEG-1</span></span>
* <span data-ttu-id="f26e6-156">Windows Media Video/VC-1</span><span class="sxs-lookup"><span data-stu-id="f26e6-156">Windows Media Video/VC-1</span></span>
* <span data-ttu-id="f26e6-157">Creazione anteprime JPEG</span><span class="sxs-lookup"><span data-stu-id="f26e6-157">JPEG thumbnail creation</span></span>

### <a name="output-audio-codecs"></a><span data-ttu-id="f26e6-158">Codec audio di output</span><span class="sxs-lookup"><span data-stu-id="f26e6-158">Output Audio Codecs</span></span>
* <span data-ttu-id="f26e6-159">AES (SMPTE 331M e 302M, AES3-2003)</span><span class="sxs-lookup"><span data-stu-id="f26e6-159">AES (SMPTE 331M and 302M, AES3-2003)</span></span>
* <span data-ttu-id="f26e6-160">Dolby® Digital (AC3)</span><span class="sxs-lookup"><span data-stu-id="f26e6-160">Dolby® Digital (AC3)</span></span>
* <span data-ttu-id="f26e6-161">Dolby® Digital Plus (AC3 E) di too7.1</span><span class="sxs-lookup"><span data-stu-id="f26e6-161">Dolby® Digital Plus (E-AC3) up too7.1</span></span>
* <span data-ttu-id="f26e6-162">AAC (AAC-LC, HE-AAC e AAC-HEv2; backup too5.1)</span><span class="sxs-lookup"><span data-stu-id="f26e6-162">AAC (AAC-LC, AAC-HE, and AAC-HEv2; up too5.1)</span></span>
* <span data-ttu-id="f26e6-163">MPEG Layer 2</span><span class="sxs-lookup"><span data-stu-id="f26e6-163">MPEG Layer 2</span></span>
* <span data-ttu-id="f26e6-164">MP3 (MPEG-1 Audio Layer 3)</span><span class="sxs-lookup"><span data-stu-id="f26e6-164">MP3 (MPEG-1 Audio Layer 3)</span></span>
* <span data-ttu-id="f26e6-165">Windows Media Audio</span><span class="sxs-lookup"><span data-stu-id="f26e6-165">Windows Media Audio</span></span>

>[!NOTE]
><span data-ttu-id="f26e6-166">Se si codifica tooDolby® Digital (AC3), è possibile scrivere l'output di hello solo in un file ISO MP4.</span><span class="sxs-lookup"><span data-stu-id="f26e6-166">If you encode tooDolby® Digital (AC3), hello output can only be written into an ISO MP4 file.</span></span>

## <span data-ttu-id="f26e6-167"><a id="closed_captioning"></a>Supporto per sottotitoli codificati</span><span class="sxs-lookup"><span data-stu-id="f26e6-167"><a id="closed_captioning"></a>Support for Closed Captioning</span></span>
<span data-ttu-id="f26e6-168">In ingresso, il **flusso di lavoro Premium del codificatore multimediale** supporta:</span><span class="sxs-lookup"><span data-stu-id="f26e6-168">On ingest, **Media Encoder Premium Workflow** supports:</span></span>

1. <span data-ttu-id="f26e6-169">File SCC</span><span class="sxs-lookup"><span data-stu-id="f26e6-169">SCC files</span></span>
2. <span data-ttu-id="f26e6-170">File SMPTE-TT</span><span class="sxs-lookup"><span data-stu-id="f26e6-170">SMPTE-TT files</span></span>
3. <span data-ttu-id="f26e6-171">CEA-608/CEA-708 – Trasportato come dati (messaggi SEI di flussi elementari H.264, ATSC/53, SCTE20) o trasportato come dati ausiliari in file MXF/GXF</span><span class="sxs-lookup"><span data-stu-id="f26e6-171">CEA-608/CEA-708 – carried as user data (SEI messages of H.264 elementary streams, ATSC/53, SCTE20) or carried as ancillary data in MXF/GXF files</span></span>
4. <span data-ttu-id="f26e6-172">File con sottotitoli STL</span><span class="sxs-lookup"><span data-stu-id="f26e6-172">STL subtitle files</span></span>

<span data-ttu-id="f26e6-173">Nell'output, sono disponibile hello le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f26e6-173">On output, hello following options are available:</span></span>

1. <span data-ttu-id="f26e6-174">CEA-608 tooCEA 708 traduzione</span><span class="sxs-lookup"><span data-stu-id="f26e6-174">CEA-608 tooCEA-708 translation</span></span>
2. <span data-ttu-id="f26e6-175">Pass-through di CEA-608/CEA-708 (incorporato in messaggi SEI di flussi elementari H.264 o trasportato come dati ausiliari in file MXF)</span><span class="sxs-lookup"><span data-stu-id="f26e6-175">CEA-608/CEA-708 pass through (embedded in SEI messages of H.264 elementary streams, or carried as ancillary data in MXF files)</span></span>
3. <span data-ttu-id="f26e6-176">SCC</span><span class="sxs-lookup"><span data-stu-id="f26e6-176">SCC</span></span>
4. <span data-ttu-id="f26e6-177">SMPTE Timed Text (da origine CEA-608 per SMPTE RP2052; inclusa la creazione di file DFXP)</span><span class="sxs-lookup"><span data-stu-id="f26e6-177">SMPTE Timed Text (from source CEA-608 per SMPTE RP2052; including DFXP file creation)</span></span>
5. <span data-ttu-id="f26e6-178">File di sottotitoli SRT</span><span class="sxs-lookup"><span data-stu-id="f26e6-178">SRT Subtitle file</span></span>
6. <span data-ttu-id="f26e6-179">Flussi di sottotitoli DVB</span><span class="sxs-lookup"><span data-stu-id="f26e6-179">DVB subtitle streams</span></span>

<span data-ttu-id="f26e6-180">Nota: non tutti hello sopra i formati di output sono supportati per il recapito tramite streaming in servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="f26e6-180">Note: not all of hello above output formats are supported for delivery via streaming in Azure Media Services.</span></span>

## <a name="known-issues"></a><span data-ttu-id="f26e6-181">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="f26e6-181">Known issues</span></span>
<span data-ttu-id="f26e6-182">Se il video di input non contiene sottotitoli, hello output che asset conterrà comunque un file TTML vuoto.</span><span class="sxs-lookup"><span data-stu-id="f26e6-182">If your input video does not contain closed captioning, hello output Asset will still contain an empty TTML file.</span></span> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="f26e6-183">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="f26e6-183">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f26e6-184">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="f26e6-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

