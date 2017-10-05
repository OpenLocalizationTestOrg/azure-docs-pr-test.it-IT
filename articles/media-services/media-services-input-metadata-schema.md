---
title: Schema dei metadati di input dei Servizi multimediali di Azure | Microsoft Docs
description: Questo argomento fornisce una panoramica dello schema di input dei Servizi multimediali di Azure.
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: d72848e2-4b65-4c84-94bc-e2a90a6e7f47
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 4787e4033e1afda6339b0b917263ecc165e400ad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="input-metadata"></a><span data-ttu-id="d6ece-103">Metadati di input</span><span class="sxs-lookup"><span data-stu-id="d6ece-103">Input Metadata</span></span>
<span data-ttu-id="d6ece-104">Un processo di codifica è associato uno (o più) asset di input in cui si desidera eseguire alcune attività di codifica.</span><span class="sxs-lookup"><span data-stu-id="d6ece-104">An encoding job is associated with an input asset (or assets) on which you want to perform some encoding tasks.</span></span>  <span data-ttu-id="d6ece-105">Al termine di un'attività, viene generato un asset di output.</span><span class="sxs-lookup"><span data-stu-id="d6ece-105">Upon completion of a task, an output asset is produced.</span></span>  <span data-ttu-id="d6ece-106">L'asset di output contiene video, audio, anteprime, manifest e così via. L'asset di output include anche un file contenente i metadati dell'asset di input.</span><span class="sxs-lookup"><span data-stu-id="d6ece-106">The output asset contains video, audio, thumbnails, manifest, etc. The output asset also contains a file with metadata about the input asset.</span></span> <span data-ttu-id="d6ece-107">Il nome del file XML dei metadati ha il seguente formato: &lt;asset_id&gt;_metadata.xml (ad esempio, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), dove &lt;asset_id&gt; è il valore AssetId dell'asset di input.</span><span class="sxs-lookup"><span data-stu-id="d6ece-107">The name of the metadata XML file has the following format: &lt;asset_id&gt;_metadata.xml (for example, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), where &lt;asset_id&gt; is the AssetId value of the input asset.</span></span>  

<span data-ttu-id="d6ece-108">Se si desidera esaminare il file di metadati, è possibile creare un localizzatore **SAS** e scaricare il file nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="d6ece-108">If you want to examine the metadata file, you can create a **SAS** locator and download the file to your local computer.</span></span> <span data-ttu-id="d6ece-109">È possibile trovare un esempio su come creare un localizzatore SAS e scaricare un file tramite le [estensioni dell'SDK .NET di Servizi multimediali](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d6ece-109">You can find an example on how to create a SAS locator and download a file  [Using the Media Services .NET SDK Extensions](media-services-dotnet-get-started.md).</span></span>  

<span data-ttu-id="d6ece-110">In questo argomento vengono descritti gli elementi e i tipi di schema XML su cui si basato i metadati di input (&lt;asset_id&gt;_metadata.xml).</span><span class="sxs-lookup"><span data-stu-id="d6ece-110">This topic discusses the elements and types of the XML schema on which the input metada (&lt;asset_id&gt;_metadata.xml) is based.</span></span>  <span data-ttu-id="d6ece-111">Per informazioni sul file contenente i metadati sull'asset di output, vedere [Output Metadata](media-services-output-metadata-schema.md) (Metadati di output).</span><span class="sxs-lookup"><span data-stu-id="d6ece-111">For information about the file that contains metadata about the output asset, see [Output Metadata](media-services-output-metadata-schema.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="d6ece-112">Il [codice schema](media-services-input-metadata-schema.md#code) completo e un [esempio di codice XML](media-services-input-metadata-schema.md#xml) sono disponibili alla fine di questo argomento.</span><span class="sxs-lookup"><span data-stu-id="d6ece-112">You can find the [Schema Code](media-services-input-metadata-schema.md#code) an [XML example](media-services-input-metadata-schema.md#xml) at the end of this topic.</span></span>  
> 
> 

## <span data-ttu-id="d6ece-113"><a name="AssetFiles"></a> Elemento radice AssetFile</span><span class="sxs-lookup"><span data-stu-id="d6ece-113"><a name="AssetFiles"></a> AssetFiles element (root element)</span></span>
<span data-ttu-id="d6ece-114">Contiene una raccolta di [elementi AssetFile](media-services-input-metadata-schema.md#AssetFile) per il processo di codifica.</span><span class="sxs-lookup"><span data-stu-id="d6ece-114">Contains a collection of [AssetFile element](media-services-input-metadata-schema.md#AssetFile)s for the encoding job.</span></span>  

<span data-ttu-id="d6ece-115">Vedere un esempio di codice XML alla fine di questo argomento: [esempio XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="d6ece-115">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

| <span data-ttu-id="d6ece-116">Nome</span><span class="sxs-lookup"><span data-stu-id="d6ece-116">Name</span></span> | <span data-ttu-id="d6ece-117">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d6ece-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d6ece-118">**AssetFile**</span><span class="sxs-lookup"><span data-stu-id="d6ece-118">**AssetFile**</span></span><br /><br /> <span data-ttu-id="d6ece-119">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="d6ece-119">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="d6ece-120">Un singolo elemento figlio.</span><span class="sxs-lookup"><span data-stu-id="d6ece-120">A single child element.</span></span> <span data-ttu-id="d6ece-121">Per altre informazioni, vedere [Elemento AssetFile](media-services-input-metadata-schema.md#AssetFile).</span><span class="sxs-lookup"><span data-stu-id="d6ece-121">For more information, see [AssetFile element](media-services-input-metadata-schema.md#AssetFile).</span></span> |

## <span data-ttu-id="d6ece-122"><a name="AssetFile"></a> Elemento AssetFile</span><span class="sxs-lookup"><span data-stu-id="d6ece-122"><a name="AssetFile"></a> AssetFile element</span></span>
 <span data-ttu-id="d6ece-123">Contiene gli attributi e gli elementi che descrivono un file di asset.</span><span class="sxs-lookup"><span data-stu-id="d6ece-123">Contains attributes and elements that describe an asset file.</span></span>  

 <span data-ttu-id="d6ece-124">Vedere un esempio di codice XML alla fine di questo argomento: [esempio XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="d6ece-124">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="d6ece-125">Attributi</span><span class="sxs-lookup"><span data-stu-id="d6ece-125">Attributes</span></span>
| <span data-ttu-id="d6ece-126">Nome</span><span class="sxs-lookup"><span data-stu-id="d6ece-126">Name</span></span> | <span data-ttu-id="d6ece-127">Tipo</span><span class="sxs-lookup"><span data-stu-id="d6ece-127">Type</span></span> | <span data-ttu-id="d6ece-128">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d6ece-128">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6ece-129">**Nome**</span><span class="sxs-lookup"><span data-stu-id="d6ece-129">**Name**</span></span><br /><br /> <span data-ttu-id="d6ece-130">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d6ece-130">Required</span></span> |<span data-ttu-id="d6ece-131">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="d6ece-131">**xs:string**</span></span> |<span data-ttu-id="d6ece-132">Nome del file di asset</span><span class="sxs-lookup"><span data-stu-id="d6ece-132">Asset file name.</span></span> |
| <span data-ttu-id="d6ece-133">**Dimensione**</span><span class="sxs-lookup"><span data-stu-id="d6ece-133">**Size**</span></span><br /><br /> <span data-ttu-id="d6ece-134">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d6ece-134">Required</span></span> |<span data-ttu-id="d6ece-135">**xs:long**</span><span class="sxs-lookup"><span data-stu-id="d6ece-135">**xs:long**</span></span> |<span data-ttu-id="d6ece-136">Dimensioni del file di asset in byte.</span><span class="sxs-lookup"><span data-stu-id="d6ece-136">Size of the asset file in bytes.</span></span> |
| <span data-ttu-id="d6ece-137">**Duration**</span><span class="sxs-lookup"><span data-stu-id="d6ece-137">**Duration**</span></span><br /><br /> <span data-ttu-id="d6ece-138">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d6ece-138">Required</span></span> |<span data-ttu-id="d6ece-139">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="d6ece-139">**xs:duration**</span></span> |<span data-ttu-id="d6ece-140">Durata della riproduzione del contenuto.</span><span class="sxs-lookup"><span data-stu-id="d6ece-140">Content play back duration.</span></span> <span data-ttu-id="d6ece-141">Esempio: Duration="PT25M37.757S".</span><span class="sxs-lookup"><span data-stu-id="d6ece-141">Example: Duration="PT25M37.757S".</span></span> |
| <span data-ttu-id="d6ece-142">**NumberOfStreams**</span><span class="sxs-lookup"><span data-stu-id="d6ece-142">**NumberOfStreams**</span></span><br /><br /> <span data-ttu-id="d6ece-143">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d6ece-143">Required</span></span> |<span data-ttu-id="d6ece-144">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d6ece-144">**xs:int**</span></span> |<span data-ttu-id="d6ece-145">Numero di flussi nel file di asset.</span><span class="sxs-lookup"><span data-stu-id="d6ece-145">Number of streams in the asset file.</span></span> |
| <span data-ttu-id="d6ece-146">**FormatNames**</span><span class="sxs-lookup"><span data-stu-id="d6ece-146">**FormatNames**</span></span><br /><br /> <span data-ttu-id="d6ece-147">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d6ece-147">Required</span></span> |<span data-ttu-id="d6ece-148">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="d6ece-148">**xs:string**</span></span> |<span data-ttu-id="d6ece-149">Nomi del formato.</span><span class="sxs-lookup"><span data-stu-id="d6ece-149">Format names.</span></span> |
| <span data-ttu-id="d6ece-150">**FormatVerboseNames**</span><span class="sxs-lookup"><span data-stu-id="d6ece-150">**FormatVerboseNames**</span></span><br /><br /> <span data-ttu-id="d6ece-151">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d6ece-151">Required</span></span> |<span data-ttu-id="d6ece-152">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="d6ece-152">**xs:string**</span></span> |<span data-ttu-id="d6ece-153">Nomi dettagliati del formato.</span><span class="sxs-lookup"><span data-stu-id="d6ece-153">Format verbose names.</span></span> |
| <span data-ttu-id="d6ece-154">**StartTime**</span><span class="sxs-lookup"><span data-stu-id="d6ece-154">**StartTime**</span></span> |<span data-ttu-id="d6ece-155">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="d6ece-155">**xs:duration**</span></span> |<span data-ttu-id="d6ece-156">Ora di inizio del contenuto.</span><span class="sxs-lookup"><span data-stu-id="d6ece-156">Content start time.</span></span> <span data-ttu-id="d6ece-157">Esempio: StartTime="PT2.669S".</span><span class="sxs-lookup"><span data-stu-id="d6ece-157">Example: StartTime="PT2.669S".</span></span> |
| <span data-ttu-id="d6ece-158">**OverallBitRate**</span><span class="sxs-lookup"><span data-stu-id="d6ece-158">**OverallBitRate**</span></span> |<span data-ttu-id="d6ece-159">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d6ece-159">**xs:int**</span></span> |<span data-ttu-id="d6ece-160">Media della velocità in bit del file di asset, espressa in kbps.</span><span class="sxs-lookup"><span data-stu-id="d6ece-160">Average bitrate of the asset file in kbps.</span></span> |

> [!NOTE]
> <span data-ttu-id="d6ece-161">I seguenti 4 elementi figlio devono comparire in una sequenza.</span><span class="sxs-lookup"><span data-stu-id="d6ece-161">The following 4 child elements must appear in a sequence.</span></span>  
> 
> 

### <a name="child-elements"></a><span data-ttu-id="d6ece-162">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="d6ece-162">Child elements</span></span>
| <span data-ttu-id="d6ece-163">Nome</span><span class="sxs-lookup"><span data-stu-id="d6ece-163">Name</span></span> | <span data-ttu-id="d6ece-164">Tipo</span><span class="sxs-lookup"><span data-stu-id="d6ece-164">Type</span></span> | <span data-ttu-id="d6ece-165">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d6ece-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6ece-166">**Programs**</span><span class="sxs-lookup"><span data-stu-id="d6ece-166">**Programs**</span></span><br /><br /> <span data-ttu-id="d6ece-167">minOccurs="0"</span><span class="sxs-lookup"><span data-stu-id="d6ece-167">minOccurs="0"</span></span> | |<span data-ttu-id="d6ece-168">Raccolta di tutti gli [Elementi Programs](media-services-input-metadata-schema.md#Programs) quando il file di asset è in formato MPEG-TS.</span><span class="sxs-lookup"><span data-stu-id="d6ece-168">Collection of all [Programs element](media-services-input-metadata-schema.md#Programs) when the asset file is in MPEG-TS format.</span></span> |
| <span data-ttu-id="d6ece-169">**VideoTracks**</span><span class="sxs-lookup"><span data-stu-id="d6ece-169">**VideoTracks**</span></span><br /><br /> <span data-ttu-id="d6ece-170">minOccurs="0"</span><span class="sxs-lookup"><span data-stu-id="d6ece-170">minOccurs="0"</span></span> | |<span data-ttu-id="d6ece-171">Ogni file di asset fisico può contenere da zero a più tracce video con interfoliazione in un formato contenitore appropriato.</span><span class="sxs-lookup"><span data-stu-id="d6ece-171">Each physical asset file can contain zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="d6ece-172">Questo elemento contiene una raccolta di tutti gli [elementi VideoTrack](media-services-input-metadata-schema.md#VideoTracks) che fanno parte del file di asset.</span><span class="sxs-lookup"><span data-stu-id="d6ece-172">This element contains a collection of all [VideoTracks element](media-services-input-metadata-schema.md#VideoTracks) that are part of the asset file.</span></span> |
| <span data-ttu-id="d6ece-173">**AudioTrack**</span><span class="sxs-lookup"><span data-stu-id="d6ece-173">**AudioTracks**</span></span><br /><br /> <span data-ttu-id="d6ece-174">minOccurs="0"</span><span class="sxs-lookup"><span data-stu-id="d6ece-174">minOccurs="0"</span></span> | |<span data-ttu-id="d6ece-175">Ogni file di asset fisico può contenere da zero a più tracce audio con interfoliazione in un formato contenitore appropriato.</span><span class="sxs-lookup"><span data-stu-id="d6ece-175">Each physical asset file can contain zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="d6ece-176">Questo elemento contiene una raccolta di tutti gli [elementi AudioTrack](media-services-input-metadata-schema.md#AudioTracks) che fanno parte del file di asset.</span><span class="sxs-lookup"><span data-stu-id="d6ece-176">This element contains a collection of all [AudioTracks element](media-services-input-metadata-schema.md#AudioTracks) that are part of the asset file.</span></span> |
| <span data-ttu-id="d6ece-177">**Metadata**</span><span class="sxs-lookup"><span data-stu-id="d6ece-177">**Metadata**</span></span><br /><br /> <span data-ttu-id="d6ece-178">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="d6ece-178">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="d6ece-179">MetadataType</span><span class="sxs-lookup"><span data-stu-id="d6ece-179">MetadataType</span></span>](media-services-input-metadata-schema.md#MetadataType) |<span data-ttu-id="d6ece-180">Metadati del file di asset rappresentati come stringhe chiave-valore.</span><span class="sxs-lookup"><span data-stu-id="d6ece-180">Asset file’s metadata represented as key\value strings.</span></span> <span data-ttu-id="d6ece-181">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="d6ece-181">For example:</span></span><br /><br /> <span data-ttu-id="d6ece-182">**&lt;Metadata key="language" value="eng" /&gt;**</span><span class="sxs-lookup"><span data-stu-id="d6ece-182">**&lt;Metadata key="language" value="eng" /&gt;**</span></span> |

## <span data-ttu-id="d6ece-183"><a name="TrackType"></a> TrackType</span><span class="sxs-lookup"><span data-stu-id="d6ece-183"><a name="TrackType"></a> TrackType</span></span>
<span data-ttu-id="d6ece-184">Vedere un esempio di codice XML alla fine di questo argomento: [esempio XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="d6ece-184">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="d6ece-185">Attributi</span><span class="sxs-lookup"><span data-stu-id="d6ece-185">Attributes</span></span>
| <span data-ttu-id="d6ece-186">Nome</span><span class="sxs-lookup"><span data-stu-id="d6ece-186">Name</span></span> | <span data-ttu-id="d6ece-187">Tipo</span><span class="sxs-lookup"><span data-stu-id="d6ece-187">Type</span></span> | <span data-ttu-id="d6ece-188">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d6ece-188">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6ece-189">**Id**</span><span class="sxs-lookup"><span data-stu-id="d6ece-189">**Id**</span></span><br /><br /> <span data-ttu-id="d6ece-190">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d6ece-190">Required</span></span> |<span data-ttu-id="d6ece-191">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d6ece-191">**xs:int**</span></span> |<span data-ttu-id="d6ece-192">Indice in base zero della traccia audio o video.</span><span class="sxs-lookup"><span data-stu-id="d6ece-192">Zero-based index of this audio or video track.</span></span><br /><br /> <span data-ttu-id="d6ece-193">Non corrisponde necessariamente al TrackID usato in un file MP4.</span><span class="sxs-lookup"><span data-stu-id="d6ece-193">This is not necessarily that the TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="d6ece-194">**Codec**</span><span class="sxs-lookup"><span data-stu-id="d6ece-194">**Codec**</span></span> |<span data-ttu-id="d6ece-195">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="d6ece-195">**xs:string**</span></span> |<span data-ttu-id="d6ece-196">Stringa del codec della traccia video.</span><span class="sxs-lookup"><span data-stu-id="d6ece-196">Video track codec string.</span></span> |
| <span data-ttu-id="d6ece-197">**CodecLongName**</span><span class="sxs-lookup"><span data-stu-id="d6ece-197">**CodecLongName**</span></span> |<span data-ttu-id="d6ece-198">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="d6ece-198">**xs:string**</span></span> |<span data-ttu-id="d6ece-199">Nome lungo del codec della traccia audio o video.</span><span class="sxs-lookup"><span data-stu-id="d6ece-199">Audio or video track codec long name.</span></span> |
| <span data-ttu-id="d6ece-200">**TimeBase**</span><span class="sxs-lookup"><span data-stu-id="d6ece-200">**TimeBase**</span></span><br /><br /> <span data-ttu-id="d6ece-201">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d6ece-201">Required</span></span> |<span data-ttu-id="d6ece-202">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="d6ece-202">**xs:string**</span></span> |<span data-ttu-id="d6ece-203">Tempo base.</span><span class="sxs-lookup"><span data-stu-id="d6ece-203">Time base.</span></span> <span data-ttu-id="d6ece-204">Esempio: TimeBase="1/48000"</span><span class="sxs-lookup"><span data-stu-id="d6ece-204">Example: TimeBase="1/48000"</span></span> |
| <span data-ttu-id="d6ece-205">**NumberOfFrames**</span><span class="sxs-lookup"><span data-stu-id="d6ece-205">**NumberOfFrames**</span></span> |<span data-ttu-id="d6ece-206">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d6ece-206">**xs:int**</span></span> |<span data-ttu-id="d6ece-207">Numero di frame (presenti per le tracce video).</span><span class="sxs-lookup"><span data-stu-id="d6ece-207">Number of frames (present for video tracks).</span></span> |
| <span data-ttu-id="d6ece-208">**StartTime**</span><span class="sxs-lookup"><span data-stu-id="d6ece-208">**StartTime**</span></span> |<span data-ttu-id="d6ece-209">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="d6ece-209">**xs:duration**</span></span> |<span data-ttu-id="d6ece-210">Ora di inizio della traccia.</span><span class="sxs-lookup"><span data-stu-id="d6ece-210">Track start time.</span></span> <span data-ttu-id="d6ece-211">Esempio: StartTime="PT2.669S"</span><span class="sxs-lookup"><span data-stu-id="d6ece-211">Example: StartTime="PT2.669S"</span></span> |
| <span data-ttu-id="d6ece-212">**Duration**</span><span class="sxs-lookup"><span data-stu-id="d6ece-212">**Duration**</span></span> |<span data-ttu-id="d6ece-213">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="d6ece-213">**xs:duration**</span></span> |<span data-ttu-id="d6ece-214">Durata della traccia.</span><span class="sxs-lookup"><span data-stu-id="d6ece-214">Track duration.</span></span> <span data-ttu-id="d6ece-215">Esempio: Duration="PTSampleFormat M37.757S".</span><span class="sxs-lookup"><span data-stu-id="d6ece-215">Example: Duration="PTSampleFormat M37.757S".</span></span> |

> [!NOTE]
> <span data-ttu-id="d6ece-216">I seguenti 2 elementi figlio devono comparire in una sequenza.</span><span class="sxs-lookup"><span data-stu-id="d6ece-216">The following 2 child elements must appear in a sequence.</span></span>  
> 
> 

### <a name="child-elements"></a><span data-ttu-id="d6ece-217">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="d6ece-217">Child elements</span></span>
| <span data-ttu-id="d6ece-218">Nome</span><span class="sxs-lookup"><span data-stu-id="d6ece-218">Name</span></span> | <span data-ttu-id="d6ece-219">Tipo</span><span class="sxs-lookup"><span data-stu-id="d6ece-219">Type</span></span> | <span data-ttu-id="d6ece-220">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d6ece-220">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6ece-221">**Disposition**</span><span class="sxs-lookup"><span data-stu-id="d6ece-221">**Disposition**</span></span><br /><br /> <span data-ttu-id="d6ece-222">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="d6ece-222">minOccurs="0" maxOccurs="1"</span></span> |[<span data-ttu-id="d6ece-223">StreamDispositionType</span><span class="sxs-lookup"><span data-stu-id="d6ece-223">StreamDispositionType</span></span>](media-services-input-metadata-schema.md#StreamDispositionType) |<span data-ttu-id="d6ece-224">Contiene informazioni di presentazione (ad esempio, se una determinata traccia audio è per utenti con problemi di vista).</span><span class="sxs-lookup"><span data-stu-id="d6ece-224">Contains presentation information (for example, whether a particular audio track is for visually impaired viewers).</span></span> |
| <span data-ttu-id="d6ece-225">**Metadata**</span><span class="sxs-lookup"><span data-stu-id="d6ece-225">**Metadata**</span></span><br /><br /> <span data-ttu-id="d6ece-226">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="d6ece-226">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="d6ece-227">MetadataType</span><span class="sxs-lookup"><span data-stu-id="d6ece-227">MetadataType</span></span>](media-services-input-metadata-schema.md#MetadataType) |<span data-ttu-id="d6ece-228">Stringhe chiave-valore generiche che possono essere usate per contenere una varietà di informazioni.</span><span class="sxs-lookup"><span data-stu-id="d6ece-228">Generic key/value strings that can be used to hold a variety of information.</span></span> <span data-ttu-id="d6ece-229">Esempio, key="language" e value="eng".</span><span class="sxs-lookup"><span data-stu-id="d6ece-229">For example, key=”language”, and value=”eng”.</span></span> |

## <span data-ttu-id="d6ece-230"><a name="AudioTrackType"></a> AudioTrackType (eredita da TrackType)</span><span class="sxs-lookup"><span data-stu-id="d6ece-230"><a name="AudioTrackType"></a> AudioTrackType (inherits from TrackType)</span></span>
 <span data-ttu-id="d6ece-231">**AudioTrackType** è un tipo globale complesso che eredita da [TrackType](media-services-input-metadata-schema.md#TrackType).</span><span class="sxs-lookup"><span data-stu-id="d6ece-231">**AudioTrackType** is a global complex type that inherits from [TrackType](media-services-input-metadata-schema.md#TrackType).</span></span>  

 <span data-ttu-id="d6ece-232">Il tipo rappresenta una specifica traccia audio nel file di asset.</span><span class="sxs-lookup"><span data-stu-id="d6ece-232">The type represents a specific audio track in the asset file.</span></span>  

 <span data-ttu-id="d6ece-233">Vedere un esempio di codice XML alla fine di questo argomento: [esempio XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="d6ece-233">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="d6ece-234">Attributi</span><span class="sxs-lookup"><span data-stu-id="d6ece-234">Attributes</span></span>
| <span data-ttu-id="d6ece-235">Nome</span><span class="sxs-lookup"><span data-stu-id="d6ece-235">Name</span></span> | <span data-ttu-id="d6ece-236">Tipo</span><span class="sxs-lookup"><span data-stu-id="d6ece-236">Type</span></span> | <span data-ttu-id="d6ece-237">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d6ece-237">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6ece-238">**SampleFormat**</span><span class="sxs-lookup"><span data-stu-id="d6ece-238">**SampleFormat**</span></span> |<span data-ttu-id="d6ece-239">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="d6ece-239">**xs:string**</span></span> |<span data-ttu-id="d6ece-240">Formato del campione.</span><span class="sxs-lookup"><span data-stu-id="d6ece-240">Sample format.</span></span> |
| <span data-ttu-id="d6ece-241">**ChannelLayout**</span><span class="sxs-lookup"><span data-stu-id="d6ece-241">**ChannelLayout**</span></span> |<span data-ttu-id="d6ece-242">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="d6ece-242">**xs:string**</span></span> |<span data-ttu-id="d6ece-243">Layout del canale.</span><span class="sxs-lookup"><span data-stu-id="d6ece-243">Channel layout.</span></span> |
| <span data-ttu-id="d6ece-244">**Channels**</span><span class="sxs-lookup"><span data-stu-id="d6ece-244">**Channels**</span></span><br /><br /> <span data-ttu-id="d6ece-245">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d6ece-245">Required</span></span> |<span data-ttu-id="d6ece-246">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d6ece-246">**xs:int**</span></span> |<span data-ttu-id="d6ece-247">Numero di canali audio (da 0 in su).</span><span class="sxs-lookup"><span data-stu-id="d6ece-247">Number (0 or more) of audio channels.</span></span> |
| <span data-ttu-id="d6ece-248">**SamplingRate**</span><span class="sxs-lookup"><span data-stu-id="d6ece-248">**SamplingRate**</span></span><br /><br /> <span data-ttu-id="d6ece-249">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d6ece-249">Required</span></span> |<span data-ttu-id="d6ece-250">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d6ece-250">**xs:int**</span></span> |<span data-ttu-id="d6ece-251">Frequenza di campionamento dell'audio in campioni/sec o Hz.</span><span class="sxs-lookup"><span data-stu-id="d6ece-251">Audio sampling rate in samples/sec or Hz.</span></span> |
| <span data-ttu-id="d6ece-252">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="d6ece-252">**Bitrate**</span></span> |<span data-ttu-id="d6ece-253">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d6ece-253">**xs:int**</span></span> |<span data-ttu-id="d6ece-254">Velocità media in bit audio in bit al secondo, calcolata in base al file di asset.</span><span class="sxs-lookup"><span data-stu-id="d6ece-254">Average audio bit rate in bits per second, as calculated from the asset file.</span></span> <span data-ttu-id="d6ece-255">Viene contato solo il payload del flusso elementare, mentre l'overhead di creazione dei pacchetti è escluso dal conteggio.</span><span class="sxs-lookup"><span data-stu-id="d6ece-255">Only the elementary stream payload is counted, and the packaging overhead is not included in this count.</span></span> |
| <span data-ttu-id="d6ece-256">**BitsPerSample**</span><span class="sxs-lookup"><span data-stu-id="d6ece-256">**BitsPerSample**</span></span> |<span data-ttu-id="d6ece-257">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d6ece-257">**xs:int**</span></span> |<span data-ttu-id="d6ece-258">Tipo di bit per campione per il formato wFormatTag.</span><span class="sxs-lookup"><span data-stu-id="d6ece-258">Bits per sample for the wFormatTag format type.</span></span> |

## <span data-ttu-id="d6ece-259"><a name="VideoTrackType"></a> VideoTrackType (eredita da TrackType)</span><span class="sxs-lookup"><span data-stu-id="d6ece-259"><a name="VideoTrackType"></a> VideoTrackType (inherits from TrackType)</span></span>
<span data-ttu-id="d6ece-260">**AudioTrackType** è un tipo globale complesso che eredita da [TrackType](media-services-input-metadata-schema.md#TrackType).</span><span class="sxs-lookup"><span data-stu-id="d6ece-260">**VideoTrackType** is a global complex type that inherits from [TrackType](media-services-input-metadata-schema.md#TrackType).</span></span>  

<span data-ttu-id="d6ece-261">Il tipo rappresenta una specifica traccia video nel file di asset.</span><span class="sxs-lookup"><span data-stu-id="d6ece-261">The type represents a specific video track in the asset file.</span></span>  

<span data-ttu-id="d6ece-262">Vedere un esempio di codice XML alla fine di questo argomento: [esempio XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="d6ece-262">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="d6ece-263">Attributi</span><span class="sxs-lookup"><span data-stu-id="d6ece-263">Attributes</span></span>
| <span data-ttu-id="d6ece-264">Nome</span><span class="sxs-lookup"><span data-stu-id="d6ece-264">Name</span></span> | <span data-ttu-id="d6ece-265">Tipo</span><span class="sxs-lookup"><span data-stu-id="d6ece-265">Type</span></span> | <span data-ttu-id="d6ece-266">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d6ece-266">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6ece-267">**FourCC**</span><span class="sxs-lookup"><span data-stu-id="d6ece-267">**FourCC**</span></span><br /><br /> <span data-ttu-id="d6ece-268">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d6ece-268">Required</span></span> |<span data-ttu-id="d6ece-269">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="d6ece-269">**xs:string**</span></span> |<span data-ttu-id="d6ece-270">Codice FourCC del codec video.</span><span class="sxs-lookup"><span data-stu-id="d6ece-270">Video codec FourCC code.</span></span> |
| <span data-ttu-id="d6ece-271">**Profilo**</span><span class="sxs-lookup"><span data-stu-id="d6ece-271">**Profile**</span></span> |<span data-ttu-id="d6ece-272">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="d6ece-272">**xs:string**</span></span> |<span data-ttu-id="d6ece-273">Profilo della traccia video.</span><span class="sxs-lookup"><span data-stu-id="d6ece-273">Video track's profile.</span></span> |
| <span data-ttu-id="d6ece-274">**Level**</span><span class="sxs-lookup"><span data-stu-id="d6ece-274">**Level**</span></span> |<span data-ttu-id="d6ece-275">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="d6ece-275">**xs:string**</span></span> |<span data-ttu-id="d6ece-276">Livello della traccia video.</span><span class="sxs-lookup"><span data-stu-id="d6ece-276">Video track's level.</span></span> |
| <span data-ttu-id="d6ece-277">**PixelFormat**</span><span class="sxs-lookup"><span data-stu-id="d6ece-277">**PixelFormat**</span></span> |<span data-ttu-id="d6ece-278">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="d6ece-278">**xs:string**</span></span> |<span data-ttu-id="d6ece-279">Formato pixel della traccia video.</span><span class="sxs-lookup"><span data-stu-id="d6ece-279">Video track's pixel format.</span></span> |
| <span data-ttu-id="d6ece-280">**Width**</span><span class="sxs-lookup"><span data-stu-id="d6ece-280">**Width**</span></span><br /><br /> <span data-ttu-id="d6ece-281">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d6ece-281">Required</span></span> |<span data-ttu-id="d6ece-282">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d6ece-282">**xs:int**</span></span> |<span data-ttu-id="d6ece-283">Larghezza del video codificata in pixel.</span><span class="sxs-lookup"><span data-stu-id="d6ece-283">Encoded video width in pixels.</span></span> |
| <span data-ttu-id="d6ece-284">**Height**</span><span class="sxs-lookup"><span data-stu-id="d6ece-284">**Height**</span></span><br /><br /> <span data-ttu-id="d6ece-285">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d6ece-285">Required</span></span> |<span data-ttu-id="d6ece-286">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d6ece-286">**xs:int**</span></span> |<span data-ttu-id="d6ece-287">Altezza del video codificata in pixel.</span><span class="sxs-lookup"><span data-stu-id="d6ece-287">Encoded video height in pixels.</span></span> |
| <span data-ttu-id="d6ece-288">**DisplayAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="d6ece-288">**DisplayAspectRatioNumerator**</span></span><br /><br /> <span data-ttu-id="d6ece-289">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d6ece-289">Required</span></span> |<span data-ttu-id="d6ece-290">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="d6ece-290">**xs:double**</span></span> |<span data-ttu-id="d6ece-291">Numeratore delle proporzioni della visualizzazione video.</span><span class="sxs-lookup"><span data-stu-id="d6ece-291">Video display aspect ratio numerator.</span></span> |
| <span data-ttu-id="d6ece-292">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="d6ece-292">**DisplayAspectRatioDenominator**</span></span><br /><br /> <span data-ttu-id="d6ece-293">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d6ece-293">Required</span></span> |<span data-ttu-id="d6ece-294">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="d6ece-294">**xs:double**</span></span> |<span data-ttu-id="d6ece-295">Denominatore delle proporzioni della visualizzazione video.</span><span class="sxs-lookup"><span data-stu-id="d6ece-295">Video display aspect ratio denominator.</span></span> |
| <span data-ttu-id="d6ece-296">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="d6ece-296">**DisplayAspectRatioDenominator**</span></span><br /><br /> <span data-ttu-id="d6ece-297">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d6ece-297">Required</span></span> |<span data-ttu-id="d6ece-298">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="d6ece-298">**xs:double**</span></span> |<span data-ttu-id="d6ece-299">Numeratore delle proporzioni del campione video.</span><span class="sxs-lookup"><span data-stu-id="d6ece-299">Video sample aspect ratio numerator.</span></span> |
| <span data-ttu-id="d6ece-300">**SampleAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="d6ece-300">**SampleAspectRatioNumerator**</span></span> |<span data-ttu-id="d6ece-301">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="d6ece-301">**xs:double**</span></span> |<span data-ttu-id="d6ece-302">Numeratore delle proporzioni del campione video.</span><span class="sxs-lookup"><span data-stu-id="d6ece-302">Video sample aspect ratio numerator.</span></span> |
| <span data-ttu-id="d6ece-303">**SampleAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="d6ece-303">**SampleAspectRatioNumerator**</span></span> |<span data-ttu-id="d6ece-304">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="d6ece-304">**xs:double**</span></span> |<span data-ttu-id="d6ece-305">Denominatore delle proporzioni del campione video.</span><span class="sxs-lookup"><span data-stu-id="d6ece-305">Video sample aspect ratio denominator.</span></span> |
| <span data-ttu-id="d6ece-306">**FrameRate**</span><span class="sxs-lookup"><span data-stu-id="d6ece-306">**FrameRate**</span></span><br /><br /> <span data-ttu-id="d6ece-307">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d6ece-307">Required</span></span> |<span data-ttu-id="d6ece-308">**xs: decimal**</span><span class="sxs-lookup"><span data-stu-id="d6ece-308">**xs:decimal**</span></span> |<span data-ttu-id="d6ece-309">Frequenza dei frame misurata in formato .3F.</span><span class="sxs-lookup"><span data-stu-id="d6ece-309">Measured video frame rate in .3f format.</span></span> |
| <span data-ttu-id="d6ece-310">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="d6ece-310">**Bitrate**</span></span> |<span data-ttu-id="d6ece-311">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d6ece-311">**xs:int**</span></span> |<span data-ttu-id="d6ece-312">Velocità media in bit video in kilobit al secondo, calcolata in base al file di asset.</span><span class="sxs-lookup"><span data-stu-id="d6ece-312">Average video bit rate in kilobits per second, as calculated from the asset file.</span></span> <span data-ttu-id="d6ece-313">Viene contato solo il payload del flusso elementare, mentre l'overhead di creazione dei pacchetti è escluso.</span><span class="sxs-lookup"><span data-stu-id="d6ece-313">Only the elementary stream payload is counted, and the packaging overhead is not included.</span></span> |
| <span data-ttu-id="d6ece-314">**MaxGOPBitrate**</span><span class="sxs-lookup"><span data-stu-id="d6ece-314">**MaxGOPBitrate**</span></span> |<span data-ttu-id="d6ece-315">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d6ece-315">**xs:int**</span></span> |<span data-ttu-id="d6ece-316">Velocità media in bit Max GOP per la traccia video, in kilobit al secondo.</span><span class="sxs-lookup"><span data-stu-id="d6ece-316">Max GOP average bitrate for this video track, in kilobits per second.</span></span> |
| <span data-ttu-id="d6ece-317">**HasBFrames**</span><span class="sxs-lookup"><span data-stu-id="d6ece-317">**HasBFrames**</span></span> |<span data-ttu-id="d6ece-318">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d6ece-318">**xs:int**</span></span> |<span data-ttu-id="d6ece-319">Numero di traccia video dei fotogrammi B.</span><span class="sxs-lookup"><span data-stu-id="d6ece-319">Video track number of B frames.</span></span> |

## <span data-ttu-id="d6ece-320"><a name="MetadataType"></a> MetadataType</span><span class="sxs-lookup"><span data-stu-id="d6ece-320"><a name="MetadataType"></a> MetadataType</span></span>
<span data-ttu-id="d6ece-321">**MetadataType** è un tipo globale complesso che descrive i metadati di un file di asset come stringhe chiave-valore.</span><span class="sxs-lookup"><span data-stu-id="d6ece-321">**MetadataType** is a global complex type that describes metadata of an asset file as key/value strings.</span></span> <span data-ttu-id="d6ece-322">Esempio, key="language" e value="eng".</span><span class="sxs-lookup"><span data-stu-id="d6ece-322">For example, key=”language”, and value=”eng”.</span></span>  

<span data-ttu-id="d6ece-323">Vedere un esempio di codice XML alla fine di questo argomento: [esempio XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="d6ece-323">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="d6ece-324">Attributi</span><span class="sxs-lookup"><span data-stu-id="d6ece-324">Attributes</span></span>
| <span data-ttu-id="d6ece-325">Nome</span><span class="sxs-lookup"><span data-stu-id="d6ece-325">Name</span></span> | <span data-ttu-id="d6ece-326">Tipo</span><span class="sxs-lookup"><span data-stu-id="d6ece-326">Type</span></span> | <span data-ttu-id="d6ece-327">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d6ece-327">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6ece-328">**key**</span><span class="sxs-lookup"><span data-stu-id="d6ece-328">**key**</span></span><br /><br /> <span data-ttu-id="d6ece-329">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d6ece-329">Required</span></span> |<span data-ttu-id="d6ece-330">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="d6ece-330">**xs:string**</span></span> |<span data-ttu-id="d6ece-331">La chiave nella coppia chiave-valore.</span><span class="sxs-lookup"><span data-stu-id="d6ece-331">The key in the key/value pair.</span></span> |
| <span data-ttu-id="d6ece-332">**value**</span><span class="sxs-lookup"><span data-stu-id="d6ece-332">**value**</span></span><br /><br /> <span data-ttu-id="d6ece-333">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d6ece-333">Required</span></span> |<span data-ttu-id="d6ece-334">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="d6ece-334">**xs:string**</span></span> |<span data-ttu-id="d6ece-335">Il valore nella coppia chiave-valore.</span><span class="sxs-lookup"><span data-stu-id="d6ece-335">The value in the key/value pair.</span></span> |

## <span data-ttu-id="d6ece-336"><a name="ProgramType"></a> ProgramType</span><span class="sxs-lookup"><span data-stu-id="d6ece-336"><a name="ProgramType"></a> ProgramType</span></span>
<span data-ttu-id="d6ece-337">**ProgramType** è un tipo globale complesso che descrive un programma.</span><span class="sxs-lookup"><span data-stu-id="d6ece-337">**ProgramType** is a global complex type that describes a program.</span></span>  

### <a name="attributes"></a><span data-ttu-id="d6ece-338">Attributi</span><span class="sxs-lookup"><span data-stu-id="d6ece-338">Attributes</span></span>
| <span data-ttu-id="d6ece-339">Nome</span><span class="sxs-lookup"><span data-stu-id="d6ece-339">Name</span></span> | <span data-ttu-id="d6ece-340">Tipo</span><span class="sxs-lookup"><span data-stu-id="d6ece-340">Type</span></span> | <span data-ttu-id="d6ece-341">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d6ece-341">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6ece-342">**ProgramId**</span><span class="sxs-lookup"><span data-stu-id="d6ece-342">**ProgramId**</span></span><br /><br /> <span data-ttu-id="d6ece-343">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d6ece-343">Required</span></span> |<span data-ttu-id="d6ece-344">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d6ece-344">**xs:int**</span></span> |<span data-ttu-id="d6ece-345">ID programma</span><span class="sxs-lookup"><span data-stu-id="d6ece-345">Program Id</span></span> |
| <span data-ttu-id="d6ece-346">**NumberOfPrograms**</span><span class="sxs-lookup"><span data-stu-id="d6ece-346">**NumberOfPrograms**</span></span><br /><br /> <span data-ttu-id="d6ece-347">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d6ece-347">Required</span></span> |<span data-ttu-id="d6ece-348">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d6ece-348">**xs:int**</span></span> |<span data-ttu-id="d6ece-349">Numero di programmi.</span><span class="sxs-lookup"><span data-stu-id="d6ece-349">Number of programs.</span></span> |
| <span data-ttu-id="d6ece-350">**PmtPid**</span><span class="sxs-lookup"><span data-stu-id="d6ece-350">**PmtPid**</span></span><br /><br /> <span data-ttu-id="d6ece-351">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d6ece-351">Required</span></span> |<span data-ttu-id="d6ece-352">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d6ece-352">**xs:int**</span></span> |<span data-ttu-id="d6ece-353">Tabelle di mappa dei programmi (PMT) che contengono informazioni sui programmi.</span><span class="sxs-lookup"><span data-stu-id="d6ece-353">Program Map Tables (PMTs) contain information about programs.</span></span>  <span data-ttu-id="d6ece-354">Per altre informazioni, vedere [PMT](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT).</span><span class="sxs-lookup"><span data-stu-id="d6ece-354">For more information, see [PMt](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT).</span></span> |
| <span data-ttu-id="d6ece-355">**PcrPid**</span><span class="sxs-lookup"><span data-stu-id="d6ece-355">**PcrPid**</span></span><br /><br /> <span data-ttu-id="d6ece-356">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d6ece-356">Required</span></span> |<span data-ttu-id="d6ece-357">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d6ece-357">**xs:int**</span></span> |<span data-ttu-id="d6ece-358">Usato dal decodificatore.</span><span class="sxs-lookup"><span data-stu-id="d6ece-358">Used by decoder.</span></span> <span data-ttu-id="d6ece-359">Per altre informazioni, vedere [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR).</span><span class="sxs-lookup"><span data-stu-id="d6ece-359">For more information, see [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR)</span></span> |
| <span data-ttu-id="d6ece-360">**StartPTS**</span><span class="sxs-lookup"><span data-stu-id="d6ece-360">**StartPTS**</span></span> |<span data-ttu-id="d6ece-361">**xs: long**</span><span class="sxs-lookup"><span data-stu-id="d6ece-361">**xs: long**</span></span> |<span data-ttu-id="d6ece-362">Timestamp di avvio della presentazione.</span><span class="sxs-lookup"><span data-stu-id="d6ece-362">Starting presentation time stamp.</span></span> |
| <span data-ttu-id="d6ece-363">**EndPTS**</span><span class="sxs-lookup"><span data-stu-id="d6ece-363">**EndPTS**</span></span> |<span data-ttu-id="d6ece-364">**xs: long**</span><span class="sxs-lookup"><span data-stu-id="d6ece-364">**xs: long**</span></span> |<span data-ttu-id="d6ece-365">Timestamp di fine della presentazione.</span><span class="sxs-lookup"><span data-stu-id="d6ece-365">Ending presentation time stamp.</span></span> |

## <span data-ttu-id="d6ece-366"><a name="StreamDispositionType"></a> StreamDispositionType</span><span class="sxs-lookup"><span data-stu-id="d6ece-366"><a name="StreamDispositionType"></a> StreamDispositionType</span></span>
<span data-ttu-id="d6ece-367">**StreamDispositionType** è un tipo globale complesso che descrive il flusso.</span><span class="sxs-lookup"><span data-stu-id="d6ece-367">**StreamDispositionType** is a global complex type that describes the stream.</span></span>  

<span data-ttu-id="d6ece-368">Vedere un esempio di codice XML alla fine di questo argomento: [esempio XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="d6ece-368">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="d6ece-369">Attributi</span><span class="sxs-lookup"><span data-stu-id="d6ece-369">Attributes</span></span>
| <span data-ttu-id="d6ece-370">Nome</span><span class="sxs-lookup"><span data-stu-id="d6ece-370">Name</span></span> | <span data-ttu-id="d6ece-371">Tipo</span><span class="sxs-lookup"><span data-stu-id="d6ece-371">Type</span></span> | <span data-ttu-id="d6ece-372">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d6ece-372">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6ece-373">**Default**</span><span class="sxs-lookup"><span data-stu-id="d6ece-373">**Default**</span></span><br /><br /> <span data-ttu-id="d6ece-374">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d6ece-374">Required</span></span> |<span data-ttu-id="d6ece-375">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d6ece-375">**xs:int**</span></span> |<span data-ttu-id="d6ece-376">Impostare questo attributo su 1 per indicare che si tratta della presentazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="d6ece-376">Set this attribute to 1 to indicate this is the default presentation.</span></span> |
| <span data-ttu-id="d6ece-377">**Dub**</span><span class="sxs-lookup"><span data-stu-id="d6ece-377">**Dub**</span></span><br /><br /> <span data-ttu-id="d6ece-378">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d6ece-378">Required</span></span> |<span data-ttu-id="d6ece-379">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d6ece-379">**xs:int**</span></span> |<span data-ttu-id="d6ece-380">Impostare questo attributo su 1 per indicare che si tratta della presentazione doppiata.</span><span class="sxs-lookup"><span data-stu-id="d6ece-380">Set this attribute to 1 to indicate this is the dubbed presentation.</span></span> |
| <span data-ttu-id="d6ece-381">**Original**</span><span class="sxs-lookup"><span data-stu-id="d6ece-381">**Original**</span></span><br /><br /> <span data-ttu-id="d6ece-382">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d6ece-382">Required</span></span> |<span data-ttu-id="d6ece-383">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d6ece-383">**xs:int**</span></span> |<span data-ttu-id="d6ece-384">Impostare questo attributo su 1 per indicare che si tratta della presentazione originale.</span><span class="sxs-lookup"><span data-stu-id="d6ece-384">Set this attribute to 1 to indicate this is the original presentation.</span></span> |
| <span data-ttu-id="d6ece-385">**Comment**</span><span class="sxs-lookup"><span data-stu-id="d6ece-385">**Comment**</span></span><br /><br /> <span data-ttu-id="d6ece-386">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d6ece-386">Required</span></span> |<span data-ttu-id="d6ece-387">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d6ece-387">**xs:int**</span></span> |<span data-ttu-id="d6ece-388">Impostare questo attributo su 1 per indicare che questa traccia contiene commenti.</span><span class="sxs-lookup"><span data-stu-id="d6ece-388">Set this attribute to 1 to indicate this track contains commentary.</span></span> |
| <span data-ttu-id="d6ece-389">**Lyrics**</span><span class="sxs-lookup"><span data-stu-id="d6ece-389">**Lyrics**</span></span><br /><br /> <span data-ttu-id="d6ece-390">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d6ece-390">Required</span></span> |<span data-ttu-id="d6ece-391">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d6ece-391">**xs:int**</span></span> |<span data-ttu-id="d6ece-392">Impostare questo attributo su 1 per indicare che questa traccia contiene testi.</span><span class="sxs-lookup"><span data-stu-id="d6ece-392">Set this attribute to 1 to indicate this track contains lyrics.</span></span> |
| <span data-ttu-id="d6ece-393">**Karaoke**</span><span class="sxs-lookup"><span data-stu-id="d6ece-393">**Karaoke**</span></span><br /><br /> <span data-ttu-id="d6ece-394">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d6ece-394">Required</span></span> |<span data-ttu-id="d6ece-395">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d6ece-395">**xs:int**</span></span> |<span data-ttu-id="d6ece-396">Impostare questo attributo su 1 per indicare che si tratta della traccia karaoke (musica di sottofondo, senza cantato).</span><span class="sxs-lookup"><span data-stu-id="d6ece-396">Set this attribute to 1 to indicate this represents the karaoke track (background music, no vocals).</span></span> |
| <span data-ttu-id="d6ece-397">**Forced**</span><span class="sxs-lookup"><span data-stu-id="d6ece-397">**Forced**</span></span><br /><br /> <span data-ttu-id="d6ece-398">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d6ece-398">Required</span></span> |<span data-ttu-id="d6ece-399">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d6ece-399">**xs:int**</span></span> |<span data-ttu-id="d6ece-400">Impostare questo attributo su 1 per indicare che si tratta della presentazione forzata.</span><span class="sxs-lookup"><span data-stu-id="d6ece-400">Set this attribute to 1 to indicate this is the forced presentation.</span></span> |
| <span data-ttu-id="d6ece-401">**HearingImpaired**</span><span class="sxs-lookup"><span data-stu-id="d6ece-401">**HearingImpaired**</span></span><br /><br /> <span data-ttu-id="d6ece-402">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d6ece-402">Required</span></span> |<span data-ttu-id="d6ece-403">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d6ece-403">**xs:int**</span></span> |<span data-ttu-id="d6ece-404">Impostare questo attributo su 1 per indicare che questa traccia è destinata agli utenti con problemi di udito.</span><span class="sxs-lookup"><span data-stu-id="d6ece-404">Set this attribute to 1 to indicate this track is for the hearing impaired.</span></span> |
| <span data-ttu-id="d6ece-405">**VisualImpaired**</span><span class="sxs-lookup"><span data-stu-id="d6ece-405">**VisualImpaired**</span></span><br /><br /> <span data-ttu-id="d6ece-406">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d6ece-406">Required</span></span> |<span data-ttu-id="d6ece-407">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d6ece-407">**xs:int**</span></span> |<span data-ttu-id="d6ece-408">Impostare questo attributo su 1 per indicare che questa traccia è destinata agli utenti con problemi di vista.</span><span class="sxs-lookup"><span data-stu-id="d6ece-408">Set this attribute to 1 to indicate this track is for the visually impaired.</span></span> |
| <span data-ttu-id="d6ece-409">**CleanEffects**</span><span class="sxs-lookup"><span data-stu-id="d6ece-409">**CleanEffects**</span></span><br /><br /> <span data-ttu-id="d6ece-410">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d6ece-410">Required</span></span> |<span data-ttu-id="d6ece-411">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d6ece-411">**xs:int**</span></span> |<span data-ttu-id="d6ece-412">Impostare questo attributo su 1 per indicare che questa traccia contiene effetti clean.</span><span class="sxs-lookup"><span data-stu-id="d6ece-412">Set this attribute to 1 to indicate this track has clean effects.</span></span> |
| <span data-ttu-id="d6ece-413">**AttachedPic**</span><span class="sxs-lookup"><span data-stu-id="d6ece-413">**AttachedPic**</span></span><br /><br /> <span data-ttu-id="d6ece-414">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="d6ece-414">Required</span></span> |<span data-ttu-id="d6ece-415">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="d6ece-415">**xs:int**</span></span> |<span data-ttu-id="d6ece-416">Impostare questo attributo su 1 per indicare che questa traccia contiene foto.</span><span class="sxs-lookup"><span data-stu-id="d6ece-416">Set this attribute to 1 to indicate this track has pictures.</span></span> |

## <span data-ttu-id="d6ece-417"><a name="Programs"></a> Elemento Programs</span><span class="sxs-lookup"><span data-stu-id="d6ece-417"><a name="Programs"></a> Programs element</span></span>
<span data-ttu-id="d6ece-418">Elemento wrapper contenente più elementi **Program**.</span><span class="sxs-lookup"><span data-stu-id="d6ece-418">Wrapper element holding multiple **Program** elements.</span></span>  

### <a name="child-elements"></a><span data-ttu-id="d6ece-419">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="d6ece-419">Child elements</span></span>
| <span data-ttu-id="d6ece-420">Nome</span><span class="sxs-lookup"><span data-stu-id="d6ece-420">Name</span></span> | <span data-ttu-id="d6ece-421">Tipo</span><span class="sxs-lookup"><span data-stu-id="d6ece-421">Type</span></span> | <span data-ttu-id="d6ece-422">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d6ece-422">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6ece-423">**Program**</span><span class="sxs-lookup"><span data-stu-id="d6ece-423">**Program**</span></span><br /><br /> <span data-ttu-id="d6ece-424">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="d6ece-424">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="d6ece-425">ProgramType</span><span class="sxs-lookup"><span data-stu-id="d6ece-425">ProgramType</span></span>](media-services-input-metadata-schema.md#ProgramType) |<span data-ttu-id="d6ece-426">Per i file di asset in formato MPEG-TS, contiene informazioni sui programmi nel file di asset.</span><span class="sxs-lookup"><span data-stu-id="d6ece-426">For asset files that are in MPEG-TS format, contains information about programs in the asset file.</span></span> |

## <span data-ttu-id="d6ece-427"><a name="VideoTracks"></a> Elemento VideoTracks</span><span class="sxs-lookup"><span data-stu-id="d6ece-427"><a name="VideoTracks"></a> VideoTracks element</span></span>
 <span data-ttu-id="d6ece-428">Elemento wrapper contenente più elementi **VideoTrack**.</span><span class="sxs-lookup"><span data-stu-id="d6ece-428">Wrapper element holding multiple **VideoTrack** elements.</span></span>  

 <span data-ttu-id="d6ece-429">Vedere un esempio di codice XML alla fine di questo argomento: [esempio XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="d6ece-429">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="d6ece-430">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="d6ece-430">Child elements</span></span>
| <span data-ttu-id="d6ece-431">Nome</span><span class="sxs-lookup"><span data-stu-id="d6ece-431">Name</span></span> | <span data-ttu-id="d6ece-432">Tipo</span><span class="sxs-lookup"><span data-stu-id="d6ece-432">Type</span></span> | <span data-ttu-id="d6ece-433">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d6ece-433">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6ece-434">**VideoTrack**</span><span class="sxs-lookup"><span data-stu-id="d6ece-434">**VideoTrack**</span></span><br /><br /> <span data-ttu-id="d6ece-435">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="d6ece-435">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="d6ece-436">VideoTrackType (eredita da TrackType)</span><span class="sxs-lookup"><span data-stu-id="d6ece-436">VideoTrackType (inherits from TrackType)</span></span>](media-services-input-metadata-schema.md#VideoTrackType) |<span data-ttu-id="d6ece-437">Contiene informazioni sulle tracce video presenti nel file di asset.</span><span class="sxs-lookup"><span data-stu-id="d6ece-437">Contains information about video tracks in the asset file.</span></span> |

## <span data-ttu-id="d6ece-438"><a name="AudioTracks"></a> Elemento AudioTracks</span><span class="sxs-lookup"><span data-stu-id="d6ece-438"><a name="AudioTracks"></a> AudioTracks element</span></span>
 <span data-ttu-id="d6ece-439">Elemento wrapper contenente più elementi **AudioTrack**.</span><span class="sxs-lookup"><span data-stu-id="d6ece-439">Wrapper element holding multiple **AudioTrack** elements.</span></span>  

 <span data-ttu-id="d6ece-440">Vedere un esempio di codice XML alla fine di questo argomento: [Esempio XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="d6ece-440">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="elements"></a><span data-ttu-id="d6ece-441">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="d6ece-441">elements</span></span>
| <span data-ttu-id="d6ece-442">Nome</span><span class="sxs-lookup"><span data-stu-id="d6ece-442">Name</span></span> | <span data-ttu-id="d6ece-443">Tipo</span><span class="sxs-lookup"><span data-stu-id="d6ece-443">Type</span></span> | <span data-ttu-id="d6ece-444">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d6ece-444">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6ece-445">**AudioTrack**</span><span class="sxs-lookup"><span data-stu-id="d6ece-445">**AudioTrack**</span></span><br /><br /> <span data-ttu-id="d6ece-446">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="d6ece-446">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="d6ece-447">AudioTrackType (eredita da TrackType)</span><span class="sxs-lookup"><span data-stu-id="d6ece-447">AudioTrackType (inherits from TrackType)</span></span>](media-services-input-metadata-schema.md#AudioTrackType) |<span data-ttu-id="d6ece-448">Contiene informazioni sulle tracce audio presenti nel file di asset.</span><span class="sxs-lookup"><span data-stu-id="d6ece-448">Contains information about audio tracks in the asset file.</span></span> |

## <span data-ttu-id="d6ece-449"><a name="code"></a> Codice schema</span><span class="sxs-lookup"><span data-stu-id="d6ece-449"><a name="code"></a> Schema Code</span></span>
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" version="1.0"  
               xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata"  
               targetNamespace="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata"  
               elementFormDefault="qualified">  

      <xs:complexType name="MetadataType">  
        <xs:attribute name="key"   type="xs:string" use="required"/>  
        <xs:attribute name="value" type="xs:string" use="required"/>  
      </xs:complexType>  

      <xs:complexType name="ProgramType">  
        <xs:attribute name="ProgramId" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>Program Id</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="NumberOfPrograms" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>Number of programs</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="PmtPid" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>pmt pid</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="PcrPid" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>pcr pid</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="StartPTS" type="xs:long">  
          <xs:annotation>  
            <xs:documentation>start pts</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="EndPTS" type="xs:long">  
          <xs:annotation>  
            <xs:documentation>end pts</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
      </xs:complexType>  

      <xs:complexType name="StreamDispositionType">  
        <xs:attribute name="Default"          type="xs:int" use="required" />  
        <xs:attribute name="Dub"              type="xs:int" use="required" />  
        <xs:attribute name="Original"         type="xs:int" use="required" />  
        <xs:attribute name="Comment"          type="xs:int" use="required" />  
        <xs:attribute name="Lyrics"           type="xs:int" use="required" />  
        <xs:attribute name="Karaoke"          type="xs:int" use="required" />  
        <xs:attribute name="Forced"           type="xs:int" use="required" />  
        <xs:attribute name="HearingImpaired"  type="xs:int" use="required" />  
        <xs:attribute name="VisualImpaired"   type="xs:int" use="required" />  
        <xs:attribute name="CleanEffects"     type="xs:int" use="required" />  
        <xs:attribute name="AttachedPic"      type="xs:int" use="required" />  
      </xs:complexType>  

      <xs:complexType name="TrackType" abstract="true">  
        <xs:sequence>  
          <xs:element name="Disposition" type="StreamDispositionType" minOccurs="0" maxOccurs="1"/>  
          <xs:element name="Metadata" type="MetadataType" minOccurs="0" maxOccurs="unbounded"/>  
        </xs:sequence>  
        <xs:attribute name="Id" use="required">  
          <xs:annotation>  
            <xs:documentation>zero-based index of this video track. Note: this is not necessarily the TrackID as used in an MP4 file</xs:documentation>  
          </xs:annotation>  
          <xs:simpleType>  
            <xs:restriction base="xs:int">  
              <xs:minInclusive value="0"/>  
            </xs:restriction>  
          </xs:simpleType>  
        </xs:attribute>  
        <xs:attribute name="Codec" type="xs:string">  
          <xs:annotation>  
            <xs:documentation>video track codec string</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="CodecLongName" type="xs:string">  
          <xs:annotation>  
            <xs:documentation>video track codec long name</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="TimeBase"  type="xs:string" use="required">  
          <xs:annotation>  
            <xs:documentation>Time base. Example: TimeBase="1/48000"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="NumberOfFrames">  
          <xs:annotation>  
            <xs:documentation>number of frames</xs:documentation>  
          </xs:annotation>  
          <xs:simpleType>  
            <xs:restriction base="xs:int">  
              <xs:minInclusive value="0"/>  
            </xs:restriction>  
          </xs:simpleType>  
        </xs:attribute>  
        <xs:attribute name="StartTime" type="xs:duration">  
          <xs:annotation>  
            <xs:documentation>Track start time. Example: StartTime="PT2.669S"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="Duration" type="xs:duration">  
          <xs:annotation>  
            <xs:documentation>Track duration. Example: Duration="PT25M37.757S"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
      </xs:complexType>  

      <xs:complexType name="VideoTrackType">  
        <xs:annotation>  
          <xs:documentation>A specific video track in the parent AssetFile</xs:documentation>  
        </xs:annotation>  
        <xs:complexContent>  
          <xs:extension base="TrackType">  
            <xs:attribute name="FourCC" type="xs:string" use="required">  
              <xs:annotation>  
                <xs:documentation>video codec FourCC code</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Profile" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>profile</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Level" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>level</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="PixelFormat" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>Video track's pixel format</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Width" use="required">  
              <xs:annotation>  
                <xs:documentation>encoded video width in pixels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Height" use="required">  
              <xs:annotation>  
                <xs:documentation>encoded video height in pixels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="DisplayAspectRatioNumerator" use="required">  
              <xs:annotation>  
                <xs:documentation>video display aspect ratio numerator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="DisplayAspectRatioDenominator" use="required">  
              <xs:annotation>  
                <xs:documentation>video display aspect ratio denominator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SampleAspectRatioNumerator">  
              <xs:annotation>  
                <xs:documentation>video sample aspect ratio numerator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SampleAspectRatioDenominator">  
              <xs:annotation>  
                <xs:documentation>video sample aspect ratio denominator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="FrameRate" use="required">  
              <xs:annotation>  
                <xs:documentation>measured video frame rate in .3f format</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:decimal">  
                  <xs:minInclusive value="0"/>  
                  <xs:fractionDigits value="3"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Bitrate">  
              <xs:annotation>  
                <xs:documentation>average video bit rate in kilobits per second, as calculated from the AssetFile. Counts only the elementary stream payload, and does not include the packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="MaxGOPBitrate">  
              <xs:annotation>  
                <xs:documentation>Max GOP average bitrate for this video track, in kilobits per second</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="HasBFrames" type="xs:int">  
              <xs:annotation>  
                <xs:documentation>video track number of B frames</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
          </xs:extension>  
        </xs:complexContent>  
      </xs:complexType>  

      <xs:complexType name="AudioTrackType">  
        <xs:annotation>  
          <xs:documentation>a specific audio track in the parent AssetFile</xs:documentation>  
        </xs:annotation>  
        <xs:complexContent>  
          <xs:extension base="TrackType">  
            <xs:attribute name="SampleFormat"  type="xs:string">  
              <xs:annotation>  
                <xs:documentation>sample format</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="ChannelLayout"  type="xs:string">  
              <xs:annotation>  
                <xs:documentation>channel layout</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Channels" use="required">  
              <xs:annotation>  
                <xs:documentation>number of audio channels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SamplingRate" use="required">  
              <xs:annotation>  
                <xs:documentation>audio sampling rate in samples/sec or Hz</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Bitrate">  
              <xs:annotation>  
                <xs:documentation>average audio bit rate in bits per second, as calculated from the AssetFile. Counts only the elementary stream payload, and does not include the packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="BitsPerSample">  
              <xs:annotation>  
                <xs:documentation>Bits per sample for the wFormatTag format type</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
          </xs:extension>  
        </xs:complexContent>  
      </xs:complexType>  

      <xs:element name="AssetFiles">  
        <xs:annotation>  
          <xs:documentation>Collection of AssetFile entries for the encoding job</xs:documentation>  
        </xs:annotation>  
        <xs:complexType>  
          <xs:sequence>  
            <xs:element name="AssetFile" minOccurs="1" maxOccurs="unbounded">  
              <xs:annotation>  
                <xs:documentation>asset file</xs:documentation>  
              </xs:annotation>  
              <xs:complexType>  
                <xs:sequence>  
                  <xs:element name="Programs" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>This is the collection of all programs when file is MPEG-TS</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="Program" type="ProgramType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="VideoTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is the collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" type="VideoTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="AudioTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is the collection of all those audio tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="AudioTrack" type="AudioTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="Metadata" type="MetadataType" minOccurs="0" maxOccurs="unbounded" />  
                </xs:sequence>  
                <xs:attribute name="Name" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>the media asset file name</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="Size" use="required">  
                  <xs:annotation>  
                    <xs:documentation>size of file in bytes</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:long">  
                      <xs:minInclusive value="0"/>  
                    </xs:restriction>  
                  </xs:simpleType>  
                </xs:attribute>  
                <xs:attribute name="Duration" type="xs:duration" use="required">  
                  <xs:annotation>  
                    <xs:documentation>content play back duration. Example: Duration="PT25M37.757S"</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="NumberOfStreams" type="xs:int" use="required">  
                  <xs:annotation>  
                    <xs:documentation>number of streams in asset file</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="FormatNames" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>format names</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="FormatVerboseName" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>format verbose names</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="StartTime" type="xs:duration">  
                  <xs:annotation>  
                    <xs:documentation>content start time. Example: StartTime="PT2.669S"</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="OverallBitRate">  
                  <xs:annotation>  
                    <xs:documentation>average bitrate of the asset file in kbps</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:int">  
                      <xs:minInclusive value="0"/>  
                    </xs:restriction>  
                  </xs:simpleType>  
                </xs:attribute>  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:schema>  


## <span data-ttu-id="d6ece-450"><a name="xml"></a> Esempio XML</span><span class="sxs-lookup"><span data-stu-id="d6ece-450"><a name="xml"></a> XML example</span></span>
<span data-ttu-id="d6ece-451">Di seguito è riportato un esempio di file di metadati di input.</span><span class="sxs-lookup"><span data-stu-id="d6ece-451">The following is an example of the Input metadata file.</span></span>  

    <?xml version="1.0" encoding="utf-8"?>  
    <AssetFiles xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata">  
      <AssetFile Name="bear.mp4" Size="1973733" Duration="PT12.678S" NumberOfStreams="2" FormatNames="mov,mp4,m4a,3gp,3g2,mj2" FormatVerboseName="QuickTime / MOV" StartTime="PT0S" OverallBitRate="1245">  
        <VideoTracks>  
          <VideoTrack Id="1" Codec="h264" CodecLongName="H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10" TimeBase="1/29970" NumberOfFrames="375" StartTime="PT0.034S" Duration="PT12.645S" FourCC="avc1" Profile="High" Level="4.1" PixelFormat="yuv420p" Width="512" Height="384" DisplayAspectRatioNumerator="4" DisplayAspectRatioDenominator="3" SampleAspectRatioNumerator="1" SampleAspectRatioDenominator="1" FrameRate="29.656" Bitrate="1043" HasBFrames="1">  
            <Disposition Default="1" Dub="0" Original="0" Comment="0" Lyrics="0" Karaoke="0" Forced="0" HearingImpaired="0" VisualImpaired="0" CleanEffects="0" AttachedPic="0" />  
            <Metadata key="creation_time" value="2010-03-10 16:11:56" />  
            <Metadata key="language" value="eng" />  
            <Metadata key="handler_name" value="Mainconcept MP4 Video Media Handler" />  
          </VideoTrack>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="aac" CodecLongName="AAC (Advanced Audio Coding)" TimeBase="1/44100" NumberOfFrames="546" StartTime="PT0S" Duration="PT12.678S" SampleFormat="fltp" ChannelLayout="stereo" Channels="2" SamplingRate="44100" Bitrate="156" BitsPerSample="0">  
            <Disposition Default="1" Dub="0" Original="0" Comment="0" Lyrics="0" Karaoke="0" Forced="0" HearingImpaired="0" VisualImpaired="0" CleanEffects="0" AttachedPic="0" />  
            <Metadata key="creation_time" value="2010-03-10 16:11:56" />  
            <Metadata key="language" value="eng" />  
            <Metadata key="handler_name" value="Mainconcept MP4 Sound Media Handler" />  
          </AudioTrack>  
        </AudioTracks>  
        <Metadata key="major_brand" value="mp42" />  
        <Metadata key="minor_version" value="0" />  
        <Metadata key="compatible_brands" value="mp42mp41" />  
        <Metadata key="creation_time" value="2010-03-10 16:11:53" />  
        <Metadata key="comment" value="Courtesy of National Geographic.  Used by Permission." />  
      </AssetFile>  
    </AssetFiles>  

## <a name="next-steps"></a><span data-ttu-id="d6ece-452">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d6ece-452">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d6ece-453">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="d6ece-453">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

