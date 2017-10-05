---
title: Codec e formati del flusso di lavoro Premium del codificatore multimediale | Microsoft Docs
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
ms.openlocfilehash: e18de2adc9aac585d6890dd7b43a54f1a0ca177e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="media-encoder-premium-workflow-formats-and-codecs"></a><span data-ttu-id="2e39c-103">Codec e formati del flusso di lavoro Premium del codificatore multimediale</span><span class="sxs-lookup"><span data-stu-id="2e39c-103">Media Encoder Premium Workflow formats and codecs</span></span>
> [!NOTE]
> <span data-ttu-id="2e39c-104">Per domande relative al codificatore Premium, inviare mepd tramite un messaggio di posta elettronica a Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="2e39c-104">For premium encoder questions, email mepd at Microsoft.com.</span></span>
> 
> <span data-ttu-id="2e39c-105">Il processore di contenuti multimediali del flusso di lavoro Premium del codificatore multimediale descritto in questo argomento non è disponibile in Cina.</span><span class="sxs-lookup"><span data-stu-id="2e39c-105">Media Encoder Premium Workflow media processor discussed in this topic is not available in China.</span></span> 
> 
> 

<span data-ttu-id="2e39c-106">Questo documento include un elenco dei codec e dei formati di file di input e output supportati nella versione di anteprima pubblica del codificatore per il **flusso di lavoro Premium del codificatore multimediale** .</span><span class="sxs-lookup"><span data-stu-id="2e39c-106">This document contains a list of input and output file formats and codecs that are supported by the public preview version of the **Media Encoder Premium Workflow** encoder.</span></span>

[<span data-ttu-id="2e39c-107">Codec e formati di input del flusso di lavoro Premium del codificatore multimediale</span><span class="sxs-lookup"><span data-stu-id="2e39c-107">Media Encoder Premium Worflow Input Formats and Codecs</span></span>](#input_formats)

[<span data-ttu-id="2e39c-108">Codec e formati di output del flusso di lavoro Premium del codificatore multimediale</span><span class="sxs-lookup"><span data-stu-id="2e39c-108">Media Encoder Premium Worflow Output Formats and Codecs</span></span>](#output_formats)

<span data-ttu-id="2e39c-109">**flusso di lavoro Premium del codificatore multimediale** supporta i sottotitoli codificati descritti in [questa](#closed_captioning) sezione.</span><span class="sxs-lookup"><span data-stu-id="2e39c-109">**Media Encoder Premium Workflow** supports closed captioning described in [this](#closed_captioning) section.</span></span> 

## <span data-ttu-id="2e39c-110"><a id="input_formats"></a>Codec e formati di input del flusso di lavoro Premium del codificatore multimediale</span><span class="sxs-lookup"><span data-stu-id="2e39c-110"><a id="input_formats"></a>Media Encoder Premium Workflow Input Formats and Codecs</span></span>
<span data-ttu-id="2e39c-111">La seguente sezione include l'elenco dei codec e dei formati di file supportati come input da questo processore di contenuti multimediali.</span><span class="sxs-lookup"><span data-stu-id="2e39c-111">The following section lists the codecs and file formats that this media processor supports as input.</span></span>

### <a name="input-containerfile-formats"></a><span data-ttu-id="2e39c-112">Contenitore di input/formati di file</span><span class="sxs-lookup"><span data-stu-id="2e39c-112">Input Container/File Formats</span></span>
* <span data-ttu-id="2e39c-113">Adobe® Flash® F4V</span><span class="sxs-lookup"><span data-stu-id="2e39c-113">Adobe® Flash® F4V</span></span>
* <span data-ttu-id="2e39c-114">MXF/SMPTE 377M</span><span class="sxs-lookup"><span data-stu-id="2e39c-114">MXF/SMPTE 377M</span></span>
* <span data-ttu-id="2e39c-115">GXF</span><span class="sxs-lookup"><span data-stu-id="2e39c-115">GXF</span></span>
* <span data-ttu-id="2e39c-116">MPEG-2 Transport Stream</span><span class="sxs-lookup"><span data-stu-id="2e39c-116">MPEG-2 Transport Streams</span></span>
* <span data-ttu-id="2e39c-117">MPEG-2 Program Stream</span><span class="sxs-lookup"><span data-stu-id="2e39c-117">MPEG-2 Program Streams</span></span>
* <span data-ttu-id="2e39c-118">MPEG-4/MP4</span><span class="sxs-lookup"><span data-stu-id="2e39c-118">MPEG-4/MP4</span></span>
* <span data-ttu-id="2e39c-119">Windows Media/ASF</span><span class="sxs-lookup"><span data-stu-id="2e39c-119">Windows Media/ASF</span></span>
* <span data-ttu-id="2e39c-120">AVI (non compresso 8 bit/10 bit)</span><span class="sxs-lookup"><span data-stu-id="2e39c-120">AVI (Uncompressed 8bit/10bit)</span></span>

### <a name="input-video-codecs"></a><span data-ttu-id="2e39c-121">Codec video di input</span><span class="sxs-lookup"><span data-stu-id="2e39c-121">Input Video Codecs</span></span>
* <span data-ttu-id="2e39c-122">AVC 8 bit/10 bit, fino a 4:2:2, incluso AVCIntra</span><span class="sxs-lookup"><span data-stu-id="2e39c-122">AVC 8-bit/10-bit, up to 4:2:2, including AVCIntra</span></span>
* <span data-ttu-id="2e39c-123">Avid DNxHD (in MXF)</span><span class="sxs-lookup"><span data-stu-id="2e39c-123">Avid DNxHD (in MXF)</span></span>
* <span data-ttu-id="2e39c-124">DVCPro/DVCProHD (in MXF)</span><span class="sxs-lookup"><span data-stu-id="2e39c-124">DVCPro/DVCProHD (in MXF)</span></span>
* <span data-ttu-id="2e39c-125">JPEG2000</span><span class="sxs-lookup"><span data-stu-id="2e39c-125">JPEG2000</span></span>
* <span data-ttu-id="2e39c-126">MPEG-2 (fino a 4:2:2 Profile e High Level; incluse varianti quali XDCAM, XDCAM HD, XDCAM IMX, CableLabs® e D10)</span><span class="sxs-lookup"><span data-stu-id="2e39c-126">MPEG-2 (up to 422 Profile and High Level; including variants such as XDCAM, XDCAM HD, XDCAM IMX, CableLabs® and D10)</span></span>
* <span data-ttu-id="2e39c-127">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="2e39c-127">MPEG-1</span></span>
* <span data-ttu-id="2e39c-128">Windows Media Video/VC-1</span><span class="sxs-lookup"><span data-stu-id="2e39c-128">Windows Media Video/VC-1</span></span>

### <a name="input-audio-codecs"></a><span data-ttu-id="2e39c-129">Codec audio di input</span><span class="sxs-lookup"><span data-stu-id="2e39c-129">Input Audio Codecs</span></span>
* <span data-ttu-id="2e39c-130">AES (SMPTE 331M e 302M, AES3-2003)</span><span class="sxs-lookup"><span data-stu-id="2e39c-130">AES (SMPTE 331M and 302M, AES3-2003)</span></span>
* <span data-ttu-id="2e39c-131">Dolby® E</span><span class="sxs-lookup"><span data-stu-id="2e39c-131">Dolby® E</span></span>
* <span data-ttu-id="2e39c-132">Dolby® Digital (AC3)</span><span class="sxs-lookup"><span data-stu-id="2e39c-132">Dolby® Digital (AC3)</span></span>
* <span data-ttu-id="2e39c-133">AAC (AAC-LC, AAC-HE e AAC-HEv2; fino a 5.1)</span><span class="sxs-lookup"><span data-stu-id="2e39c-133">AAC (AAC-LC, AAC-HE, and AAC-HEv2; up to 5.1)</span></span>
* <span data-ttu-id="2e39c-134">MPEG Layer 2</span><span class="sxs-lookup"><span data-stu-id="2e39c-134">MPEG Layer 2</span></span>
* <span data-ttu-id="2e39c-135">MP3 (MPEG-1 Audio Layer 3)</span><span class="sxs-lookup"><span data-stu-id="2e39c-135">MP3 (MPEG-1 Audio Layer 3)</span></span>
* <span data-ttu-id="2e39c-136">Windows Media Audio</span><span class="sxs-lookup"><span data-stu-id="2e39c-136">Windows Media Audio</span></span>
* <span data-ttu-id="2e39c-137">WAV/PCM</span><span class="sxs-lookup"><span data-stu-id="2e39c-137">WAV/PCM</span></span>

## <span data-ttu-id="2e39c-138"><a id="output_format"></a>Codec e formati di output del flusso di lavoro Premium del codificatore multimediale</span><span class="sxs-lookup"><span data-stu-id="2e39c-138"><a id="output_format"></a>Media Encoder Premium Workflow Output Formats and Codecs</span></span>
<span data-ttu-id="2e39c-139">La seguente sezione include l'elenco dei codec e dei formati di file supportati come output da questo processore di contenuti multimediali.</span><span class="sxs-lookup"><span data-stu-id="2e39c-139">The following section lists the codecs and file formats that are supported as output from this media processor.</span></span>

### <a name="output-containerfile-formats"></a><span data-ttu-id="2e39c-140">Contenitore di output/formati di file</span><span class="sxs-lookup"><span data-stu-id="2e39c-140">Output Container/File Formats</span></span>
* <span data-ttu-id="2e39c-141">Adobe® Flash® F4V</span><span class="sxs-lookup"><span data-stu-id="2e39c-141">Adobe® Flash® F4V</span></span>
* <span data-ttu-id="2e39c-142">MXF (OP1a, XDCAM e AS02)</span><span class="sxs-lookup"><span data-stu-id="2e39c-142">MXF (OP1a, XDCAM and AS02)</span></span>
* <span data-ttu-id="2e39c-143">DPP (incluso AS11)</span><span class="sxs-lookup"><span data-stu-id="2e39c-143">DPP (including AS11)</span></span>
* <span data-ttu-id="2e39c-144">GXF</span><span class="sxs-lookup"><span data-stu-id="2e39c-144">GXF</span></span>
* <span data-ttu-id="2e39c-145">MPEG-4/MP4</span><span class="sxs-lookup"><span data-stu-id="2e39c-145">MPEG-4/MP4</span></span>
* <span data-ttu-id="2e39c-146">Windows Media/ASF</span><span class="sxs-lookup"><span data-stu-id="2e39c-146">Windows Media/ASF</span></span>
* <span data-ttu-id="2e39c-147">AVI (non compresso 8 bit/10 bit)</span><span class="sxs-lookup"><span data-stu-id="2e39c-147">AVI (Uncompressed 8bit/10bit)</span></span>
* <span data-ttu-id="2e39c-148">Formato di file Smooth Streaming (PIFF 1.3)</span><span class="sxs-lookup"><span data-stu-id="2e39c-148">Smooth Streaming File Format (PIFF 1.3)</span></span>
* <span data-ttu-id="2e39c-149">MPEG-TS</span><span class="sxs-lookup"><span data-stu-id="2e39c-149">MPEG-TS</span></span> 

### <a name="output-video-codecs"></a><span data-ttu-id="2e39c-150">Codec video di output</span><span class="sxs-lookup"><span data-stu-id="2e39c-150">Output Video Codecs</span></span>
* <span data-ttu-id="2e39c-151">AVC (H.264; 8 bit; fino a High Profile, Level 5.2; 4K Ultra HD; AVC Intra)</span><span class="sxs-lookup"><span data-stu-id="2e39c-151">AVC (H.264; 8-bit; up to High Profile, Level 5.2; 4K Ultra HD; AVC Intra)</span></span>
* <span data-ttu-id="2e39c-152">Avid DNxHD (in MXF)</span><span class="sxs-lookup"><span data-stu-id="2e39c-152">Avid DNxHD (in MXF)</span></span>
* <span data-ttu-id="2e39c-153">DVCPro/DVCProHD (in MXF)</span><span class="sxs-lookup"><span data-stu-id="2e39c-153">DVCPro/DVCProHD (in MXF)</span></span>
* <span data-ttu-id="2e39c-154">MPEG-2 (fino a 4:2:2 Profile e High Level; incluse varianti quali XDCAM, XDCAM HD, XDCAM IMX, CableLabs® e D10)</span><span class="sxs-lookup"><span data-stu-id="2e39c-154">MPEG-2 (up to 422 Profile and High Level; including variants such as XDCAM, XDCAM HD, XDCAM IMX, CableLabs® and D10)</span></span>
* <span data-ttu-id="2e39c-155">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="2e39c-155">MPEG-1</span></span>
* <span data-ttu-id="2e39c-156">Windows Media Video/VC-1</span><span class="sxs-lookup"><span data-stu-id="2e39c-156">Windows Media Video/VC-1</span></span>
* <span data-ttu-id="2e39c-157">Creazione anteprime JPEG</span><span class="sxs-lookup"><span data-stu-id="2e39c-157">JPEG thumbnail creation</span></span>

### <a name="output-audio-codecs"></a><span data-ttu-id="2e39c-158">Codec audio di output</span><span class="sxs-lookup"><span data-stu-id="2e39c-158">Output Audio Codecs</span></span>
* <span data-ttu-id="2e39c-159">AES (SMPTE 331M e 302M, AES3-2003)</span><span class="sxs-lookup"><span data-stu-id="2e39c-159">AES (SMPTE 331M and 302M, AES3-2003)</span></span>
* <span data-ttu-id="2e39c-160">Dolby® Digital (AC3)</span><span class="sxs-lookup"><span data-stu-id="2e39c-160">Dolby® Digital (AC3)</span></span>
* <span data-ttu-id="2e39c-161">Dolby® Digital Plus (E-AC3) fino a 7.1</span><span class="sxs-lookup"><span data-stu-id="2e39c-161">Dolby® Digital Plus (E-AC3) up to 7.1</span></span>
* <span data-ttu-id="2e39c-162">AAC (AAC-LC, AAC-HE e AAC-HEv2; fino a 5.1)</span><span class="sxs-lookup"><span data-stu-id="2e39c-162">AAC (AAC-LC, AAC-HE, and AAC-HEv2; up to 5.1)</span></span>
* <span data-ttu-id="2e39c-163">MPEG Layer 2</span><span class="sxs-lookup"><span data-stu-id="2e39c-163">MPEG Layer 2</span></span>
* <span data-ttu-id="2e39c-164">MP3 (MPEG-1 Audio Layer 3)</span><span class="sxs-lookup"><span data-stu-id="2e39c-164">MP3 (MPEG-1 Audio Layer 3)</span></span>
* <span data-ttu-id="2e39c-165">Windows Media Audio</span><span class="sxs-lookup"><span data-stu-id="2e39c-165">Windows Media Audio</span></span>

>[!NOTE]
><span data-ttu-id="2e39c-166">Se si codifica per Dolby® Digital (AC3), l'output può essere scritto solo in un file ISO MP4.</span><span class="sxs-lookup"><span data-stu-id="2e39c-166">If you encode to Dolby® Digital (AC3), the output can only be written into an ISO MP4 file.</span></span>

## <span data-ttu-id="2e39c-167"><a id="closed_captioning"></a>Supporto per sottotitoli codificati</span><span class="sxs-lookup"><span data-stu-id="2e39c-167"><a id="closed_captioning"></a>Support for Closed Captioning</span></span>
<span data-ttu-id="2e39c-168">In ingresso, il **flusso di lavoro Premium del codificatore multimediale** supporta:</span><span class="sxs-lookup"><span data-stu-id="2e39c-168">On ingest, **Media Encoder Premium Workflow** supports:</span></span>

1. <span data-ttu-id="2e39c-169">File SCC</span><span class="sxs-lookup"><span data-stu-id="2e39c-169">SCC files</span></span>
2. <span data-ttu-id="2e39c-170">File SMPTE-TT</span><span class="sxs-lookup"><span data-stu-id="2e39c-170">SMPTE-TT files</span></span>
3. <span data-ttu-id="2e39c-171">CEA-608/CEA-708 – Trasportato come dati (messaggi SEI di flussi elementari H.264, ATSC/53, SCTE20) o trasportato come dati ausiliari in file MXF/GXF</span><span class="sxs-lookup"><span data-stu-id="2e39c-171">CEA-608/CEA-708 – carried as user data (SEI messages of H.264 elementary streams, ATSC/53, SCTE20) or carried as ancillary data in MXF/GXF files</span></span>
4. <span data-ttu-id="2e39c-172">File con sottotitoli STL</span><span class="sxs-lookup"><span data-stu-id="2e39c-172">STL subtitle files</span></span>

<span data-ttu-id="2e39c-173">In uscita, sono disponibili le seguenti opzioni:</span><span class="sxs-lookup"><span data-stu-id="2e39c-173">On output, the following options are available:</span></span>

1. <span data-ttu-id="2e39c-174">Conversione da CEA-608 a CEA-708</span><span class="sxs-lookup"><span data-stu-id="2e39c-174">CEA-608 to CEA-708 translation</span></span>
2. <span data-ttu-id="2e39c-175">Pass-through di CEA-608/CEA-708 (incorporato in messaggi SEI di flussi elementari H.264 o trasportato come dati ausiliari in file MXF)</span><span class="sxs-lookup"><span data-stu-id="2e39c-175">CEA-608/CEA-708 pass through (embedded in SEI messages of H.264 elementary streams, or carried as ancillary data in MXF files)</span></span>
3. <span data-ttu-id="2e39c-176">SCC</span><span class="sxs-lookup"><span data-stu-id="2e39c-176">SCC</span></span>
4. <span data-ttu-id="2e39c-177">SMPTE Timed Text (da origine CEA-608 per SMPTE RP2052; inclusa la creazione di file DFXP)</span><span class="sxs-lookup"><span data-stu-id="2e39c-177">SMPTE Timed Text (from source CEA-608 per SMPTE RP2052; including DFXP file creation)</span></span>
5. <span data-ttu-id="2e39c-178">File di sottotitoli SRT</span><span class="sxs-lookup"><span data-stu-id="2e39c-178">SRT Subtitle file</span></span>
6. <span data-ttu-id="2e39c-179">Flussi di sottotitoli DVB</span><span class="sxs-lookup"><span data-stu-id="2e39c-179">DVB subtitle streams</span></span>

<span data-ttu-id="2e39c-180">Nota: non tutti i formati di output precedenti sono supportati per il recapito tramite streaming in Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="2e39c-180">Note: not all of the above output formats are supported for delivery via streaming in Azure Media Services.</span></span>

## <a name="known-issues"></a><span data-ttu-id="2e39c-181">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="2e39c-181">Known issues</span></span>
<span data-ttu-id="2e39c-182">Se il video di input non contiene i sottotitoli codificati, l'asset di output conterrà comunque un file TTML vuoto.</span><span class="sxs-lookup"><span data-stu-id="2e39c-182">If your input video does not contain closed captioning, the output Asset will still contain an empty TTML file.</span></span> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="2e39c-183">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="2e39c-183">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2e39c-184">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="2e39c-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

