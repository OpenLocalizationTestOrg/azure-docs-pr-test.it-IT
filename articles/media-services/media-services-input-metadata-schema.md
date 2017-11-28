---
title: schema dei metadati di input di servizi multimediali aaaAzure | Documenti Microsoft
description: Hello argomento viene fornita una panoramica dello schema dei metadati di input di servizi multimediali di Azure.
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
ms.openlocfilehash: 9b72c6ff317aa98451ea75548465dc6023b44a55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="input-metadata"></a><span data-ttu-id="4a930-103">Metadati di input</span><span class="sxs-lookup"><span data-stu-id="4a930-103">Input Metadata</span></span>
<span data-ttu-id="4a930-104">Un processo di codifica è associato a un asset di input (o attività) in cui si desidera tooperform alcune attività di codifica.</span><span class="sxs-lookup"><span data-stu-id="4a930-104">An encoding job is associated with an input asset (or assets) on which you want tooperform some encoding tasks.</span></span>  <span data-ttu-id="4a930-105">Al termine di un'attività, viene generato un asset di output.</span><span class="sxs-lookup"><span data-stu-id="4a930-105">Upon completion of a task, an output asset is produced.</span></span>  <span data-ttu-id="4a930-106">asset di output di hello e così via. contiene inoltre un file con i metadati sull'asset di input hello Hello output contenente video, audio, le anteprime, il manifesto.</span><span class="sxs-lookup"><span data-stu-id="4a930-106">hello output asset contains video, audio, thumbnails, manifest, etc. hello output asset also contains a file with metadata about hello input asset.</span></span> <span data-ttu-id="4a930-107">nome del file XML dei metadati di hello Hello ha hello seguente formato: &lt;asset_id&gt;<id_asset>_metadata.XML (ad esempio, d 57-8 41114ad3 eb5e - 4c 92-5354e2b7d4a4_metadata.xml), in cui &lt;asset_id&gt; è hello AssetId valore dell'asset di input hello.</span><span class="sxs-lookup"><span data-stu-id="4a930-107">hello name of hello metadata XML file has hello following format: &lt;asset_id&gt;_metadata.xml (for example, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), where &lt;asset_id&gt; is hello AssetId value of hello input asset.</span></span>  

<span data-ttu-id="4a930-108">Se si desidera tooexamine hello metadati file, è possibile creare un **SAS** download e l'indicatore di posizione hello computer locale tooyour di file.</span><span class="sxs-lookup"><span data-stu-id="4a930-108">If you want tooexamine hello metadata file, you can create a **SAS** locator and download hello file tooyour local computer.</span></span> <span data-ttu-id="4a930-109">È possibile trovare un esempio su come toocreate un localizzatore SAS e scaricare un file [utilizzando hello Media Services .NET SDK Extensions](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4a930-109">You can find an example on how toocreate a SAS locator and download a file  [Using hello Media Services .NET SDK Extensions](media-services-dotnet-get-started.md).</span></span>  

<span data-ttu-id="4a930-110">Questo argomento vengono elementi hello e tipi di schema XML hello per metadati di input quali hello (&lt;asset_id&gt;<asset_id>_metadata.XML) è basato.</span><span class="sxs-lookup"><span data-stu-id="4a930-110">This topic discusses hello elements and types of hello XML schema on which hello input metada (&lt;asset_id&gt;_metadata.xml) is based.</span></span>  <span data-ttu-id="4a930-111">Per informazioni sul file hello che contiene i metadati sull'asset di output di hello, vedere [Output metadati](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="4a930-111">For information about hello file that contains metadata about hello output asset, see [Output Metadata](media-services-output-metadata-schema.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="4a930-112">È possibile trovare hello [codice Schema](media-services-input-metadata-schema.md#code) un [file XML di esempio](media-services-input-metadata-schema.md#xml) alla fine di hello di questo argomento.</span><span class="sxs-lookup"><span data-stu-id="4a930-112">You can find hello [Schema Code](media-services-input-metadata-schema.md#code) an [XML example](media-services-input-metadata-schema.md#xml) at hello end of this topic.</span></span>  
> 
> 

## <span data-ttu-id="4a930-113"><a name="AssetFiles"></a> Elemento radice AssetFile</span><span class="sxs-lookup"><span data-stu-id="4a930-113"><a name="AssetFiles"></a> AssetFiles element (root element)</span></span>
<span data-ttu-id="4a930-114">Contiene una raccolta di [elemento AssetFile](media-services-input-metadata-schema.md#AssetFile)s per il processo di codifica hello.</span><span class="sxs-lookup"><span data-stu-id="4a930-114">Contains a collection of [AssetFile element](media-services-input-metadata-schema.md#AssetFile)s for hello encoding job.</span></span>  

<span data-ttu-id="4a930-115">Vedere un esempio XML alla fine di hello di questo argomento: [file XML di esempio](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="4a930-115">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

| <span data-ttu-id="4a930-116">Nome</span><span class="sxs-lookup"><span data-stu-id="4a930-116">Name</span></span> | <span data-ttu-id="4a930-117">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4a930-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4a930-118">**AssetFile**</span><span class="sxs-lookup"><span data-stu-id="4a930-118">**AssetFile**</span></span><br /><br /> <span data-ttu-id="4a930-119">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="4a930-119">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="4a930-120">Un singolo elemento figlio.</span><span class="sxs-lookup"><span data-stu-id="4a930-120">A single child element.</span></span> <span data-ttu-id="4a930-121">Per altre informazioni, vedere [Elemento AssetFile](media-services-input-metadata-schema.md#AssetFile).</span><span class="sxs-lookup"><span data-stu-id="4a930-121">For more information, see [AssetFile element](media-services-input-metadata-schema.md#AssetFile).</span></span> |

## <span data-ttu-id="4a930-122"><a name="AssetFile"></a> Elemento AssetFile</span><span class="sxs-lookup"><span data-stu-id="4a930-122"><a name="AssetFile"></a> AssetFile element</span></span>
 <span data-ttu-id="4a930-123">Contiene gli attributi e gli elementi che descrivono un file di asset.</span><span class="sxs-lookup"><span data-stu-id="4a930-123">Contains attributes and elements that describe an asset file.</span></span>  

 <span data-ttu-id="4a930-124">Vedere un esempio XML alla fine di hello di questo argomento: [file XML di esempio](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="4a930-124">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="4a930-125">Attributi</span><span class="sxs-lookup"><span data-stu-id="4a930-125">Attributes</span></span>
| <span data-ttu-id="4a930-126">Nome</span><span class="sxs-lookup"><span data-stu-id="4a930-126">Name</span></span> | <span data-ttu-id="4a930-127">Tipo</span><span class="sxs-lookup"><span data-stu-id="4a930-127">Type</span></span> | <span data-ttu-id="4a930-128">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4a930-128">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4a930-129">**Nome**</span><span class="sxs-lookup"><span data-stu-id="4a930-129">**Name**</span></span><br /><br /> <span data-ttu-id="4a930-130">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a930-130">Required</span></span> |<span data-ttu-id="4a930-131">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="4a930-131">**xs:string**</span></span> |<span data-ttu-id="4a930-132">Nome del file di asset</span><span class="sxs-lookup"><span data-stu-id="4a930-132">Asset file name.</span></span> |
| <span data-ttu-id="4a930-133">**Dimensione**</span><span class="sxs-lookup"><span data-stu-id="4a930-133">**Size**</span></span><br /><br /> <span data-ttu-id="4a930-134">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a930-134">Required</span></span> |<span data-ttu-id="4a930-135">**xs:long**</span><span class="sxs-lookup"><span data-stu-id="4a930-135">**xs:long**</span></span> |<span data-ttu-id="4a930-136">Dimensioni del file di asset hello in byte.</span><span class="sxs-lookup"><span data-stu-id="4a930-136">Size of hello asset file in bytes.</span></span> |
| <span data-ttu-id="4a930-137">**Duration**</span><span class="sxs-lookup"><span data-stu-id="4a930-137">**Duration**</span></span><br /><br /> <span data-ttu-id="4a930-138">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a930-138">Required</span></span> |<span data-ttu-id="4a930-139">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="4a930-139">**xs:duration**</span></span> |<span data-ttu-id="4a930-140">Durata della riproduzione del contenuto.</span><span class="sxs-lookup"><span data-stu-id="4a930-140">Content play back duration.</span></span> <span data-ttu-id="4a930-141">Esempio: Duration="PT25M37.757S".</span><span class="sxs-lookup"><span data-stu-id="4a930-141">Example: Duration="PT25M37.757S".</span></span> |
| <span data-ttu-id="4a930-142">**NumberOfStreams**</span><span class="sxs-lookup"><span data-stu-id="4a930-142">**NumberOfStreams**</span></span><br /><br /> <span data-ttu-id="4a930-143">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a930-143">Required</span></span> |<span data-ttu-id="4a930-144">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="4a930-144">**xs:int**</span></span> |<span data-ttu-id="4a930-145">Numero di flussi nel file di asset hello.</span><span class="sxs-lookup"><span data-stu-id="4a930-145">Number of streams in hello asset file.</span></span> |
| <span data-ttu-id="4a930-146">**FormatNames**</span><span class="sxs-lookup"><span data-stu-id="4a930-146">**FormatNames**</span></span><br /><br /> <span data-ttu-id="4a930-147">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a930-147">Required</span></span> |<span data-ttu-id="4a930-148">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="4a930-148">**xs:string**</span></span> |<span data-ttu-id="4a930-149">Nomi del formato.</span><span class="sxs-lookup"><span data-stu-id="4a930-149">Format names.</span></span> |
| <span data-ttu-id="4a930-150">**FormatVerboseNames**</span><span class="sxs-lookup"><span data-stu-id="4a930-150">**FormatVerboseNames**</span></span><br /><br /> <span data-ttu-id="4a930-151">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a930-151">Required</span></span> |<span data-ttu-id="4a930-152">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="4a930-152">**xs:string**</span></span> |<span data-ttu-id="4a930-153">Nomi dettagliati del formato.</span><span class="sxs-lookup"><span data-stu-id="4a930-153">Format verbose names.</span></span> |
| <span data-ttu-id="4a930-154">**StartTime**</span><span class="sxs-lookup"><span data-stu-id="4a930-154">**StartTime**</span></span> |<span data-ttu-id="4a930-155">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="4a930-155">**xs:duration**</span></span> |<span data-ttu-id="4a930-156">Ora di inizio del contenuto.</span><span class="sxs-lookup"><span data-stu-id="4a930-156">Content start time.</span></span> <span data-ttu-id="4a930-157">Esempio: StartTime="PT2.669S".</span><span class="sxs-lookup"><span data-stu-id="4a930-157">Example: StartTime="PT2.669S".</span></span> |
| <span data-ttu-id="4a930-158">**OverallBitRate**</span><span class="sxs-lookup"><span data-stu-id="4a930-158">**OverallBitRate**</span></span> |<span data-ttu-id="4a930-159">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="4a930-159">**xs:int**</span></span> |<span data-ttu-id="4a930-160">Velocità in bit media del file di asset hello in kbps.</span><span class="sxs-lookup"><span data-stu-id="4a930-160">Average bitrate of hello asset file in kbps.</span></span> |

> [!NOTE]
> <span data-ttu-id="4a930-161">Hello 4 elementi figlio seguenti deve apparire in una sequenza.</span><span class="sxs-lookup"><span data-stu-id="4a930-161">hello following 4 child elements must appear in a sequence.</span></span>  
> 
> 

### <a name="child-elements"></a><span data-ttu-id="4a930-162">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="4a930-162">Child elements</span></span>
| <span data-ttu-id="4a930-163">Nome</span><span class="sxs-lookup"><span data-stu-id="4a930-163">Name</span></span> | <span data-ttu-id="4a930-164">Tipo</span><span class="sxs-lookup"><span data-stu-id="4a930-164">Type</span></span> | <span data-ttu-id="4a930-165">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4a930-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4a930-166">**Programs**</span><span class="sxs-lookup"><span data-stu-id="4a930-166">**Programs**</span></span><br /><br /> <span data-ttu-id="4a930-167">minOccurs="0"</span><span class="sxs-lookup"><span data-stu-id="4a930-167">minOccurs="0"</span></span> | |<span data-ttu-id="4a930-168">Raccolta di tutti [elemento Programs](media-services-input-metadata-schema.md#Programs) quando il file di asset hello è in formato MPEG-TS.</span><span class="sxs-lookup"><span data-stu-id="4a930-168">Collection of all [Programs element](media-services-input-metadata-schema.md#Programs) when hello asset file is in MPEG-TS format.</span></span> |
| <span data-ttu-id="4a930-169">**VideoTracks**</span><span class="sxs-lookup"><span data-stu-id="4a930-169">**VideoTracks**</span></span><br /><br /> <span data-ttu-id="4a930-170">minOccurs="0"</span><span class="sxs-lookup"><span data-stu-id="4a930-170">minOccurs="0"</span></span> | |<span data-ttu-id="4a930-171">Ogni file di asset fisico può contenere da zero a più tracce video con interfoliazione in un formato contenitore appropriato.</span><span class="sxs-lookup"><span data-stu-id="4a930-171">Each physical asset file can contain zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="4a930-172">Questo elemento contiene una raccolta di tutti [elemento VideoTracks](media-services-input-metadata-schema.md#VideoTracks) che fanno parte del file di asset hello.</span><span class="sxs-lookup"><span data-stu-id="4a930-172">This element contains a collection of all [VideoTracks element](media-services-input-metadata-schema.md#VideoTracks) that are part of hello asset file.</span></span> |
| <span data-ttu-id="4a930-173">**AudioTrack**</span><span class="sxs-lookup"><span data-stu-id="4a930-173">**AudioTracks**</span></span><br /><br /> <span data-ttu-id="4a930-174">minOccurs="0"</span><span class="sxs-lookup"><span data-stu-id="4a930-174">minOccurs="0"</span></span> | |<span data-ttu-id="4a930-175">Ogni file di asset fisico può contenere da zero a più tracce audio con interfoliazione in un formato contenitore appropriato.</span><span class="sxs-lookup"><span data-stu-id="4a930-175">Each physical asset file can contain zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="4a930-176">Questo elemento contiene una raccolta di tutti [elemento AudioTracks](media-services-input-metadata-schema.md#AudioTracks) che fanno parte del file di asset hello.</span><span class="sxs-lookup"><span data-stu-id="4a930-176">This element contains a collection of all [AudioTracks element](media-services-input-metadata-schema.md#AudioTracks) that are part of hello asset file.</span></span> |
| <span data-ttu-id="4a930-177">**Metadata**</span><span class="sxs-lookup"><span data-stu-id="4a930-177">**Metadata**</span></span><br /><br /> <span data-ttu-id="4a930-178">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="4a930-178">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="4a930-179">MetadataType</span><span class="sxs-lookup"><span data-stu-id="4a930-179">MetadataType</span></span>](media-services-input-metadata-schema.md#MetadataType) |<span data-ttu-id="4a930-180">Metadati del file di asset rappresentati come stringhe chiave-valore.</span><span class="sxs-lookup"><span data-stu-id="4a930-180">Asset file’s metadata represented as key\value strings.</span></span> <span data-ttu-id="4a930-181">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="4a930-181">For example:</span></span><br /><br /> <span data-ttu-id="4a930-182">**&lt;Metadata key="language" value="eng" /&gt;**</span><span class="sxs-lookup"><span data-stu-id="4a930-182">**&lt;Metadata key="language" value="eng" /&gt;**</span></span> |

## <span data-ttu-id="4a930-183"><a name="TrackType"></a> TrackType</span><span class="sxs-lookup"><span data-stu-id="4a930-183"><a name="TrackType"></a> TrackType</span></span>
<span data-ttu-id="4a930-184">Vedere un esempio XML alla fine di hello di questo argomento: [file XML di esempio](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="4a930-184">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="4a930-185">Attributi</span><span class="sxs-lookup"><span data-stu-id="4a930-185">Attributes</span></span>
| <span data-ttu-id="4a930-186">Nome</span><span class="sxs-lookup"><span data-stu-id="4a930-186">Name</span></span> | <span data-ttu-id="4a930-187">Tipo</span><span class="sxs-lookup"><span data-stu-id="4a930-187">Type</span></span> | <span data-ttu-id="4a930-188">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4a930-188">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4a930-189">**Id**</span><span class="sxs-lookup"><span data-stu-id="4a930-189">**Id**</span></span><br /><br /> <span data-ttu-id="4a930-190">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a930-190">Required</span></span> |<span data-ttu-id="4a930-191">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="4a930-191">**xs:int**</span></span> |<span data-ttu-id="4a930-192">Indice in base zero della traccia audio o video.</span><span class="sxs-lookup"><span data-stu-id="4a930-192">Zero-based index of this audio or video track.</span></span><br /><br /> <span data-ttu-id="4a930-193">Non è necessariamente tale hello TrackID usato in un file MP4.</span><span class="sxs-lookup"><span data-stu-id="4a930-193">This is not necessarily that hello TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="4a930-194">**Codec**</span><span class="sxs-lookup"><span data-stu-id="4a930-194">**Codec**</span></span> |<span data-ttu-id="4a930-195">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="4a930-195">**xs:string**</span></span> |<span data-ttu-id="4a930-196">Stringa del codec della traccia video.</span><span class="sxs-lookup"><span data-stu-id="4a930-196">Video track codec string.</span></span> |
| <span data-ttu-id="4a930-197">**CodecLongName**</span><span class="sxs-lookup"><span data-stu-id="4a930-197">**CodecLongName**</span></span> |<span data-ttu-id="4a930-198">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="4a930-198">**xs:string**</span></span> |<span data-ttu-id="4a930-199">Nome lungo del codec della traccia audio o video.</span><span class="sxs-lookup"><span data-stu-id="4a930-199">Audio or video track codec long name.</span></span> |
| <span data-ttu-id="4a930-200">**TimeBase**</span><span class="sxs-lookup"><span data-stu-id="4a930-200">**TimeBase**</span></span><br /><br /> <span data-ttu-id="4a930-201">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a930-201">Required</span></span> |<span data-ttu-id="4a930-202">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="4a930-202">**xs:string**</span></span> |<span data-ttu-id="4a930-203">Tempo base.</span><span class="sxs-lookup"><span data-stu-id="4a930-203">Time base.</span></span> <span data-ttu-id="4a930-204">Esempio: TimeBase="1/48000"</span><span class="sxs-lookup"><span data-stu-id="4a930-204">Example: TimeBase="1/48000"</span></span> |
| <span data-ttu-id="4a930-205">**NumberOfFrames**</span><span class="sxs-lookup"><span data-stu-id="4a930-205">**NumberOfFrames**</span></span> |<span data-ttu-id="4a930-206">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="4a930-206">**xs:int**</span></span> |<span data-ttu-id="4a930-207">Numero di frame (presenti per le tracce video).</span><span class="sxs-lookup"><span data-stu-id="4a930-207">Number of frames (present for video tracks).</span></span> |
| <span data-ttu-id="4a930-208">**StartTime**</span><span class="sxs-lookup"><span data-stu-id="4a930-208">**StartTime**</span></span> |<span data-ttu-id="4a930-209">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="4a930-209">**xs:duration**</span></span> |<span data-ttu-id="4a930-210">Ora di inizio della traccia.</span><span class="sxs-lookup"><span data-stu-id="4a930-210">Track start time.</span></span> <span data-ttu-id="4a930-211">Esempio: StartTime="PT2.669S"</span><span class="sxs-lookup"><span data-stu-id="4a930-211">Example: StartTime="PT2.669S"</span></span> |
| <span data-ttu-id="4a930-212">**Duration**</span><span class="sxs-lookup"><span data-stu-id="4a930-212">**Duration**</span></span> |<span data-ttu-id="4a930-213">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="4a930-213">**xs:duration**</span></span> |<span data-ttu-id="4a930-214">Durata della traccia.</span><span class="sxs-lookup"><span data-stu-id="4a930-214">Track duration.</span></span> <span data-ttu-id="4a930-215">Esempio: Duration="PTSampleFormat M37.757S".</span><span class="sxs-lookup"><span data-stu-id="4a930-215">Example: Duration="PTSampleFormat M37.757S".</span></span> |

> [!NOTE]
> <span data-ttu-id="4a930-216">Hello 2 elementi figlio seguenti deve apparire in una sequenza.</span><span class="sxs-lookup"><span data-stu-id="4a930-216">hello following 2 child elements must appear in a sequence.</span></span>  
> 
> 

### <a name="child-elements"></a><span data-ttu-id="4a930-217">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="4a930-217">Child elements</span></span>
| <span data-ttu-id="4a930-218">Nome</span><span class="sxs-lookup"><span data-stu-id="4a930-218">Name</span></span> | <span data-ttu-id="4a930-219">Tipo</span><span class="sxs-lookup"><span data-stu-id="4a930-219">Type</span></span> | <span data-ttu-id="4a930-220">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4a930-220">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4a930-221">**Disposition**</span><span class="sxs-lookup"><span data-stu-id="4a930-221">**Disposition**</span></span><br /><br /> <span data-ttu-id="4a930-222">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="4a930-222">minOccurs="0" maxOccurs="1"</span></span> |[<span data-ttu-id="4a930-223">StreamDispositionType</span><span class="sxs-lookup"><span data-stu-id="4a930-223">StreamDispositionType</span></span>](media-services-input-metadata-schema.md#StreamDispositionType) |<span data-ttu-id="4a930-224">Contiene informazioni di presentazione (ad esempio, se una determinata traccia audio è per utenti con problemi di vista).</span><span class="sxs-lookup"><span data-stu-id="4a930-224">Contains presentation information (for example, whether a particular audio track is for visually impaired viewers).</span></span> |
| <span data-ttu-id="4a930-225">**Metadata**</span><span class="sxs-lookup"><span data-stu-id="4a930-225">**Metadata**</span></span><br /><br /> <span data-ttu-id="4a930-226">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="4a930-226">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="4a930-227">MetadataType</span><span class="sxs-lookup"><span data-stu-id="4a930-227">MetadataType</span></span>](media-services-input-metadata-schema.md#MetadataType) |<span data-ttu-id="4a930-228">Stringhe chiave/valore generiche che possono essere utilizzati toohold un'ampia gamma di informazioni.</span><span class="sxs-lookup"><span data-stu-id="4a930-228">Generic key/value strings that can be used toohold a variety of information.</span></span> <span data-ttu-id="4a930-229">Esempio, key="language" e value="eng".</span><span class="sxs-lookup"><span data-stu-id="4a930-229">For example, key=”language”, and value=”eng”.</span></span> |

## <span data-ttu-id="4a930-230"><a name="AudioTrackType"></a> AudioTrackType (eredita da TrackType)</span><span class="sxs-lookup"><span data-stu-id="4a930-230"><a name="AudioTrackType"></a> AudioTrackType (inherits from TrackType)</span></span>
 <span data-ttu-id="4a930-231">**AudioTrackType** è un tipo globale complesso che eredita da [TrackType](media-services-input-metadata-schema.md#TrackType).</span><span class="sxs-lookup"><span data-stu-id="4a930-231">**AudioTrackType** is a global complex type that inherits from [TrackType](media-services-input-metadata-schema.md#TrackType).</span></span>  

 <span data-ttu-id="4a930-232">tipo di Hello rappresenta una specifica traccia audio nel file di asset hello.</span><span class="sxs-lookup"><span data-stu-id="4a930-232">hello type represents a specific audio track in hello asset file.</span></span>  

 <span data-ttu-id="4a930-233">Vedere un esempio XML alla fine di hello di questo argomento: [file XML di esempio](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="4a930-233">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="4a930-234">Attributi</span><span class="sxs-lookup"><span data-stu-id="4a930-234">Attributes</span></span>
| <span data-ttu-id="4a930-235">Nome</span><span class="sxs-lookup"><span data-stu-id="4a930-235">Name</span></span> | <span data-ttu-id="4a930-236">Tipo</span><span class="sxs-lookup"><span data-stu-id="4a930-236">Type</span></span> | <span data-ttu-id="4a930-237">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4a930-237">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4a930-238">**SampleFormat**</span><span class="sxs-lookup"><span data-stu-id="4a930-238">**SampleFormat**</span></span> |<span data-ttu-id="4a930-239">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="4a930-239">**xs:string**</span></span> |<span data-ttu-id="4a930-240">Formato del campione.</span><span class="sxs-lookup"><span data-stu-id="4a930-240">Sample format.</span></span> |
| <span data-ttu-id="4a930-241">**ChannelLayout**</span><span class="sxs-lookup"><span data-stu-id="4a930-241">**ChannelLayout**</span></span> |<span data-ttu-id="4a930-242">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="4a930-242">**xs:string**</span></span> |<span data-ttu-id="4a930-243">Layout del canale.</span><span class="sxs-lookup"><span data-stu-id="4a930-243">Channel layout.</span></span> |
| <span data-ttu-id="4a930-244">**Channels**</span><span class="sxs-lookup"><span data-stu-id="4a930-244">**Channels**</span></span><br /><br /> <span data-ttu-id="4a930-245">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a930-245">Required</span></span> |<span data-ttu-id="4a930-246">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="4a930-246">**xs:int**</span></span> |<span data-ttu-id="4a930-247">Numero di canali audio (da 0 in su).</span><span class="sxs-lookup"><span data-stu-id="4a930-247">Number (0 or more) of audio channels.</span></span> |
| <span data-ttu-id="4a930-248">**SamplingRate**</span><span class="sxs-lookup"><span data-stu-id="4a930-248">**SamplingRate**</span></span><br /><br /> <span data-ttu-id="4a930-249">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a930-249">Required</span></span> |<span data-ttu-id="4a930-250">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="4a930-250">**xs:int**</span></span> |<span data-ttu-id="4a930-251">Frequenza di campionamento dell'audio in campioni/sec o Hz.</span><span class="sxs-lookup"><span data-stu-id="4a930-251">Audio sampling rate in samples/sec or Hz.</span></span> |
| <span data-ttu-id="4a930-252">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="4a930-252">**Bitrate**</span></span> |<span data-ttu-id="4a930-253">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="4a930-253">**xs:int**</span></span> |<span data-ttu-id="4a930-254">Velocità in bit audio Media in bit al secondo, calcolata dal file di asset hello.</span><span class="sxs-lookup"><span data-stu-id="4a930-254">Average audio bit rate in bits per second, as calculated from hello asset file.</span></span> <span data-ttu-id="4a930-255">Viene contato solo payload del flusso elementare hello e overhead di creazione di pacchetti hello non è incluso in questo conteggio.</span><span class="sxs-lookup"><span data-stu-id="4a930-255">Only hello elementary stream payload is counted, and hello packaging overhead is not included in this count.</span></span> |
| <span data-ttu-id="4a930-256">**BitsPerSample**</span><span class="sxs-lookup"><span data-stu-id="4a930-256">**BitsPerSample**</span></span> |<span data-ttu-id="4a930-257">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="4a930-257">**xs:int**</span></span> |<span data-ttu-id="4a930-258">Bit per campione per formato wFormatTag hello digitare.</span><span class="sxs-lookup"><span data-stu-id="4a930-258">Bits per sample for hello wFormatTag format type.</span></span> |

## <span data-ttu-id="4a930-259"><a name="VideoTrackType"></a> VideoTrackType (eredita da TrackType)</span><span class="sxs-lookup"><span data-stu-id="4a930-259"><a name="VideoTrackType"></a> VideoTrackType (inherits from TrackType)</span></span>
<span data-ttu-id="4a930-260">**AudioTrackType** è un tipo globale complesso che eredita da [TrackType](media-services-input-metadata-schema.md#TrackType).</span><span class="sxs-lookup"><span data-stu-id="4a930-260">**VideoTrackType** is a global complex type that inherits from [TrackType](media-services-input-metadata-schema.md#TrackType).</span></span>  

<span data-ttu-id="4a930-261">tipo di Hello rappresenta una specifica traccia video nel file di asset hello.</span><span class="sxs-lookup"><span data-stu-id="4a930-261">hello type represents a specific video track in hello asset file.</span></span>  

<span data-ttu-id="4a930-262">Vedere un esempio XML alla fine di hello di questo argomento: [file XML di esempio](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="4a930-262">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="4a930-263">Attributi</span><span class="sxs-lookup"><span data-stu-id="4a930-263">Attributes</span></span>
| <span data-ttu-id="4a930-264">Nome</span><span class="sxs-lookup"><span data-stu-id="4a930-264">Name</span></span> | <span data-ttu-id="4a930-265">Tipo</span><span class="sxs-lookup"><span data-stu-id="4a930-265">Type</span></span> | <span data-ttu-id="4a930-266">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4a930-266">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4a930-267">**FourCC**</span><span class="sxs-lookup"><span data-stu-id="4a930-267">**FourCC**</span></span><br /><br /> <span data-ttu-id="4a930-268">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a930-268">Required</span></span> |<span data-ttu-id="4a930-269">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="4a930-269">**xs:string**</span></span> |<span data-ttu-id="4a930-270">Codice FourCC del codec video.</span><span class="sxs-lookup"><span data-stu-id="4a930-270">Video codec FourCC code.</span></span> |
| <span data-ttu-id="4a930-271">**Profilo**</span><span class="sxs-lookup"><span data-stu-id="4a930-271">**Profile**</span></span> |<span data-ttu-id="4a930-272">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="4a930-272">**xs:string**</span></span> |<span data-ttu-id="4a930-273">Profilo della traccia video.</span><span class="sxs-lookup"><span data-stu-id="4a930-273">Video track's profile.</span></span> |
| <span data-ttu-id="4a930-274">**Level**</span><span class="sxs-lookup"><span data-stu-id="4a930-274">**Level**</span></span> |<span data-ttu-id="4a930-275">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="4a930-275">**xs:string**</span></span> |<span data-ttu-id="4a930-276">Livello della traccia video.</span><span class="sxs-lookup"><span data-stu-id="4a930-276">Video track's level.</span></span> |
| <span data-ttu-id="4a930-277">**PixelFormat**</span><span class="sxs-lookup"><span data-stu-id="4a930-277">**PixelFormat**</span></span> |<span data-ttu-id="4a930-278">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="4a930-278">**xs:string**</span></span> |<span data-ttu-id="4a930-279">Formato pixel della traccia video.</span><span class="sxs-lookup"><span data-stu-id="4a930-279">Video track's pixel format.</span></span> |
| <span data-ttu-id="4a930-280">**Width**</span><span class="sxs-lookup"><span data-stu-id="4a930-280">**Width**</span></span><br /><br /> <span data-ttu-id="4a930-281">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a930-281">Required</span></span> |<span data-ttu-id="4a930-282">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="4a930-282">**xs:int**</span></span> |<span data-ttu-id="4a930-283">Larghezza del video codificata in pixel.</span><span class="sxs-lookup"><span data-stu-id="4a930-283">Encoded video width in pixels.</span></span> |
| <span data-ttu-id="4a930-284">**Height**</span><span class="sxs-lookup"><span data-stu-id="4a930-284">**Height**</span></span><br /><br /> <span data-ttu-id="4a930-285">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a930-285">Required</span></span> |<span data-ttu-id="4a930-286">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="4a930-286">**xs:int**</span></span> |<span data-ttu-id="4a930-287">Altezza del video codificata in pixel.</span><span class="sxs-lookup"><span data-stu-id="4a930-287">Encoded video height in pixels.</span></span> |
| <span data-ttu-id="4a930-288">**DisplayAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="4a930-288">**DisplayAspectRatioNumerator**</span></span><br /><br /> <span data-ttu-id="4a930-289">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a930-289">Required</span></span> |<span data-ttu-id="4a930-290">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="4a930-290">**xs:double**</span></span> |<span data-ttu-id="4a930-291">Numeratore delle proporzioni della visualizzazione video.</span><span class="sxs-lookup"><span data-stu-id="4a930-291">Video display aspect ratio numerator.</span></span> |
| <span data-ttu-id="4a930-292">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="4a930-292">**DisplayAspectRatioDenominator**</span></span><br /><br /> <span data-ttu-id="4a930-293">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a930-293">Required</span></span> |<span data-ttu-id="4a930-294">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="4a930-294">**xs:double**</span></span> |<span data-ttu-id="4a930-295">Denominatore delle proporzioni della visualizzazione video.</span><span class="sxs-lookup"><span data-stu-id="4a930-295">Video display aspect ratio denominator.</span></span> |
| <span data-ttu-id="4a930-296">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="4a930-296">**DisplayAspectRatioDenominator**</span></span><br /><br /> <span data-ttu-id="4a930-297">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a930-297">Required</span></span> |<span data-ttu-id="4a930-298">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="4a930-298">**xs:double**</span></span> |<span data-ttu-id="4a930-299">Numeratore delle proporzioni del campione video.</span><span class="sxs-lookup"><span data-stu-id="4a930-299">Video sample aspect ratio numerator.</span></span> |
| <span data-ttu-id="4a930-300">**SampleAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="4a930-300">**SampleAspectRatioNumerator**</span></span> |<span data-ttu-id="4a930-301">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="4a930-301">**xs:double**</span></span> |<span data-ttu-id="4a930-302">Numeratore delle proporzioni del campione video.</span><span class="sxs-lookup"><span data-stu-id="4a930-302">Video sample aspect ratio numerator.</span></span> |
| <span data-ttu-id="4a930-303">**SampleAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="4a930-303">**SampleAspectRatioNumerator**</span></span> |<span data-ttu-id="4a930-304">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="4a930-304">**xs:double**</span></span> |<span data-ttu-id="4a930-305">Denominatore delle proporzioni del campione video.</span><span class="sxs-lookup"><span data-stu-id="4a930-305">Video sample aspect ratio denominator.</span></span> |
| <span data-ttu-id="4a930-306">**FrameRate**</span><span class="sxs-lookup"><span data-stu-id="4a930-306">**FrameRate**</span></span><br /><br /> <span data-ttu-id="4a930-307">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a930-307">Required</span></span> |<span data-ttu-id="4a930-308">**xs: decimal**</span><span class="sxs-lookup"><span data-stu-id="4a930-308">**xs:decimal**</span></span> |<span data-ttu-id="4a930-309">Frequenza dei frame misurata in formato .3F.</span><span class="sxs-lookup"><span data-stu-id="4a930-309">Measured video frame rate in .3f format.</span></span> |
| <span data-ttu-id="4a930-310">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="4a930-310">**Bitrate**</span></span> |<span data-ttu-id="4a930-311">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="4a930-311">**xs:int**</span></span> |<span data-ttu-id="4a930-312">Velocità in bit video Media in kilobit al secondo, calcolata dal file di asset hello.</span><span class="sxs-lookup"><span data-stu-id="4a930-312">Average video bit rate in kilobits per second, as calculated from hello asset file.</span></span> <span data-ttu-id="4a930-313">Viene contato solo payload del flusso elementare hello e overhead di creazione di pacchetti hello non è incluso.</span><span class="sxs-lookup"><span data-stu-id="4a930-313">Only hello elementary stream payload is counted, and hello packaging overhead is not included.</span></span> |
| <span data-ttu-id="4a930-314">**MaxGOPBitrate**</span><span class="sxs-lookup"><span data-stu-id="4a930-314">**MaxGOPBitrate**</span></span> |<span data-ttu-id="4a930-315">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="4a930-315">**xs:int**</span></span> |<span data-ttu-id="4a930-316">Velocità media in bit Max GOP per la traccia video, in kilobit al secondo.</span><span class="sxs-lookup"><span data-stu-id="4a930-316">Max GOP average bitrate for this video track, in kilobits per second.</span></span> |
| <span data-ttu-id="4a930-317">**HasBFrames**</span><span class="sxs-lookup"><span data-stu-id="4a930-317">**HasBFrames**</span></span> |<span data-ttu-id="4a930-318">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="4a930-318">**xs:int**</span></span> |<span data-ttu-id="4a930-319">Numero di traccia video dei fotogrammi B.</span><span class="sxs-lookup"><span data-stu-id="4a930-319">Video track number of B frames.</span></span> |

## <span data-ttu-id="4a930-320"><a name="MetadataType"></a> MetadataType</span><span class="sxs-lookup"><span data-stu-id="4a930-320"><a name="MetadataType"></a> MetadataType</span></span>
<span data-ttu-id="4a930-321">**MetadataType** è un tipo globale complesso che descrive i metadati di un file di asset come stringhe chiave-valore.</span><span class="sxs-lookup"><span data-stu-id="4a930-321">**MetadataType** is a global complex type that describes metadata of an asset file as key/value strings.</span></span> <span data-ttu-id="4a930-322">Esempio, key="language" e value="eng".</span><span class="sxs-lookup"><span data-stu-id="4a930-322">For example, key=”language”, and value=”eng”.</span></span>  

<span data-ttu-id="4a930-323">Vedere un esempio XML alla fine di hello di questo argomento: [file XML di esempio](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="4a930-323">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="4a930-324">Attributi</span><span class="sxs-lookup"><span data-stu-id="4a930-324">Attributes</span></span>
| <span data-ttu-id="4a930-325">Nome</span><span class="sxs-lookup"><span data-stu-id="4a930-325">Name</span></span> | <span data-ttu-id="4a930-326">Tipo</span><span class="sxs-lookup"><span data-stu-id="4a930-326">Type</span></span> | <span data-ttu-id="4a930-327">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4a930-327">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4a930-328">**key**</span><span class="sxs-lookup"><span data-stu-id="4a930-328">**key**</span></span><br /><br /> <span data-ttu-id="4a930-329">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a930-329">Required</span></span> |<span data-ttu-id="4a930-330">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="4a930-330">**xs:string**</span></span> |<span data-ttu-id="4a930-331">chiave di Hello nella coppia chiave/valore hello.</span><span class="sxs-lookup"><span data-stu-id="4a930-331">hello key in hello key/value pair.</span></span> |
| <span data-ttu-id="4a930-332">**value**</span><span class="sxs-lookup"><span data-stu-id="4a930-332">**value**</span></span><br /><br /> <span data-ttu-id="4a930-333">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a930-333">Required</span></span> |<span data-ttu-id="4a930-334">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="4a930-334">**xs:string**</span></span> |<span data-ttu-id="4a930-335">valore di Hello nella coppia chiave/valore hello.</span><span class="sxs-lookup"><span data-stu-id="4a930-335">hello value in hello key/value pair.</span></span> |

## <span data-ttu-id="4a930-336"><a name="ProgramType"></a> ProgramType</span><span class="sxs-lookup"><span data-stu-id="4a930-336"><a name="ProgramType"></a> ProgramType</span></span>
<span data-ttu-id="4a930-337">**ProgramType** è un tipo globale complesso che descrive un programma.</span><span class="sxs-lookup"><span data-stu-id="4a930-337">**ProgramType** is a global complex type that describes a program.</span></span>  

### <a name="attributes"></a><span data-ttu-id="4a930-338">Attributi</span><span class="sxs-lookup"><span data-stu-id="4a930-338">Attributes</span></span>
| <span data-ttu-id="4a930-339">Nome</span><span class="sxs-lookup"><span data-stu-id="4a930-339">Name</span></span> | <span data-ttu-id="4a930-340">Tipo</span><span class="sxs-lookup"><span data-stu-id="4a930-340">Type</span></span> | <span data-ttu-id="4a930-341">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4a930-341">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4a930-342">**ProgramId**</span><span class="sxs-lookup"><span data-stu-id="4a930-342">**ProgramId**</span></span><br /><br /> <span data-ttu-id="4a930-343">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a930-343">Required</span></span> |<span data-ttu-id="4a930-344">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="4a930-344">**xs:int**</span></span> |<span data-ttu-id="4a930-345">ID programma</span><span class="sxs-lookup"><span data-stu-id="4a930-345">Program Id</span></span> |
| <span data-ttu-id="4a930-346">**NumberOfPrograms**</span><span class="sxs-lookup"><span data-stu-id="4a930-346">**NumberOfPrograms**</span></span><br /><br /> <span data-ttu-id="4a930-347">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a930-347">Required</span></span> |<span data-ttu-id="4a930-348">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="4a930-348">**xs:int**</span></span> |<span data-ttu-id="4a930-349">Numero di programmi.</span><span class="sxs-lookup"><span data-stu-id="4a930-349">Number of programs.</span></span> |
| <span data-ttu-id="4a930-350">**PmtPid**</span><span class="sxs-lookup"><span data-stu-id="4a930-350">**PmtPid**</span></span><br /><br /> <span data-ttu-id="4a930-351">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a930-351">Required</span></span> |<span data-ttu-id="4a930-352">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="4a930-352">**xs:int**</span></span> |<span data-ttu-id="4a930-353">Tabelle di mappa dei programmi (PMT) che contengono informazioni sui programmi.</span><span class="sxs-lookup"><span data-stu-id="4a930-353">Program Map Tables (PMTs) contain information about programs.</span></span>  <span data-ttu-id="4a930-354">Per altre informazioni, vedere [PMT](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT).</span><span class="sxs-lookup"><span data-stu-id="4a930-354">For more information, see [PMt](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT).</span></span> |
| <span data-ttu-id="4a930-355">**PcrPid**</span><span class="sxs-lookup"><span data-stu-id="4a930-355">**PcrPid**</span></span><br /><br /> <span data-ttu-id="4a930-356">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a930-356">Required</span></span> |<span data-ttu-id="4a930-357">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="4a930-357">**xs:int**</span></span> |<span data-ttu-id="4a930-358">Usato dal decodificatore.</span><span class="sxs-lookup"><span data-stu-id="4a930-358">Used by decoder.</span></span> <span data-ttu-id="4a930-359">Per altre informazioni, vedere [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR).</span><span class="sxs-lookup"><span data-stu-id="4a930-359">For more information, see [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR)</span></span> |
| <span data-ttu-id="4a930-360">**StartPTS**</span><span class="sxs-lookup"><span data-stu-id="4a930-360">**StartPTS**</span></span> |<span data-ttu-id="4a930-361">**xs: long**</span><span class="sxs-lookup"><span data-stu-id="4a930-361">**xs: long**</span></span> |<span data-ttu-id="4a930-362">Timestamp di avvio della presentazione.</span><span class="sxs-lookup"><span data-stu-id="4a930-362">Starting presentation time stamp.</span></span> |
| <span data-ttu-id="4a930-363">**EndPTS**</span><span class="sxs-lookup"><span data-stu-id="4a930-363">**EndPTS**</span></span> |<span data-ttu-id="4a930-364">**xs: long**</span><span class="sxs-lookup"><span data-stu-id="4a930-364">**xs: long**</span></span> |<span data-ttu-id="4a930-365">Timestamp di fine della presentazione.</span><span class="sxs-lookup"><span data-stu-id="4a930-365">Ending presentation time stamp.</span></span> |

## <span data-ttu-id="4a930-366"><a name="StreamDispositionType"></a> StreamDispositionType</span><span class="sxs-lookup"><span data-stu-id="4a930-366"><a name="StreamDispositionType"></a> StreamDispositionType</span></span>
<span data-ttu-id="4a930-367">**StreamDispositionType** è un tipo globale complesso che descrive il flusso di hello.</span><span class="sxs-lookup"><span data-stu-id="4a930-367">**StreamDispositionType** is a global complex type that describes hello stream.</span></span>  

<span data-ttu-id="4a930-368">Vedere un esempio XML alla fine di hello di questo argomento: [file XML di esempio](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="4a930-368">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="4a930-369">Attributi</span><span class="sxs-lookup"><span data-stu-id="4a930-369">Attributes</span></span>
| <span data-ttu-id="4a930-370">Nome</span><span class="sxs-lookup"><span data-stu-id="4a930-370">Name</span></span> | <span data-ttu-id="4a930-371">Tipo</span><span class="sxs-lookup"><span data-stu-id="4a930-371">Type</span></span> | <span data-ttu-id="4a930-372">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4a930-372">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4a930-373">**Default**</span><span class="sxs-lookup"><span data-stu-id="4a930-373">**Default**</span></span><br /><br /> <span data-ttu-id="4a930-374">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a930-374">Required</span></span> |<span data-ttu-id="4a930-375">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="4a930-375">**xs:int**</span></span> |<span data-ttu-id="4a930-376">Impostare questo tooindicate too1 attributo di che si tratta presentazione predefinita hello.</span><span class="sxs-lookup"><span data-stu-id="4a930-376">Set this attribute too1 tooindicate this is hello default presentation.</span></span> |
| <span data-ttu-id="4a930-377">**Dub**</span><span class="sxs-lookup"><span data-stu-id="4a930-377">**Dub**</span></span><br /><br /> <span data-ttu-id="4a930-378">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a930-378">Required</span></span> |<span data-ttu-id="4a930-379">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="4a930-379">**xs:int**</span></span> |<span data-ttu-id="4a930-380">Impostare questa proprietà tooindicate di too1 questo attributo è hello riregistrare presentazione.</span><span class="sxs-lookup"><span data-stu-id="4a930-380">Set this attribute too1 tooindicate this is hello dubbed presentation.</span></span> |
| <span data-ttu-id="4a930-381">**Original**</span><span class="sxs-lookup"><span data-stu-id="4a930-381">**Original**</span></span><br /><br /> <span data-ttu-id="4a930-382">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a930-382">Required</span></span> |<span data-ttu-id="4a930-383">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="4a930-383">**xs:int**</span></span> |<span data-ttu-id="4a930-384">Impostare questo tooindicate too1 attributo di che si tratta presentazione originale hello.</span><span class="sxs-lookup"><span data-stu-id="4a930-384">Set this attribute too1 tooindicate this is hello original presentation.</span></span> |
| <span data-ttu-id="4a930-385">**Comment**</span><span class="sxs-lookup"><span data-stu-id="4a930-385">**Comment**</span></span><br /><br /> <span data-ttu-id="4a930-386">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a930-386">Required</span></span> |<span data-ttu-id="4a930-387">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="4a930-387">**xs:int**</span></span> |<span data-ttu-id="4a930-388">Impostare questo tooindicate too1 attributo questa traccia contiene dei commenti.</span><span class="sxs-lookup"><span data-stu-id="4a930-388">Set this attribute too1 tooindicate this track contains commentary.</span></span> |
| <span data-ttu-id="4a930-389">**Lyrics**</span><span class="sxs-lookup"><span data-stu-id="4a930-389">**Lyrics**</span></span><br /><br /> <span data-ttu-id="4a930-390">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a930-390">Required</span></span> |<span data-ttu-id="4a930-391">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="4a930-391">**xs:int**</span></span> |<span data-ttu-id="4a930-392">Impostare questo tooindicate too1 attributo questa traccia contiene del testo.</span><span class="sxs-lookup"><span data-stu-id="4a930-392">Set this attribute too1 tooindicate this track contains lyrics.</span></span> |
| <span data-ttu-id="4a930-393">**Karaoke**</span><span class="sxs-lookup"><span data-stu-id="4a930-393">**Karaoke**</span></span><br /><br /> <span data-ttu-id="4a930-394">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a930-394">Required</span></span> |<span data-ttu-id="4a930-395">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="4a930-395">**xs:int**</span></span> |<span data-ttu-id="4a930-396">Impostare questo tooindicate too1 attributo rappresenta hello traccia karaoke (musica di sottofondo, senza canto).</span><span class="sxs-lookup"><span data-stu-id="4a930-396">Set this attribute too1 tooindicate this represents hello karaoke track (background music, no vocals).</span></span> |
| <span data-ttu-id="4a930-397">**Forced**</span><span class="sxs-lookup"><span data-stu-id="4a930-397">**Forced**</span></span><br /><br /> <span data-ttu-id="4a930-398">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a930-398">Required</span></span> |<span data-ttu-id="4a930-399">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="4a930-399">**xs:int**</span></span> |<span data-ttu-id="4a930-400">Impostare questo tooindicate too1 attributo di che si tratta presentazione di hello forzato.</span><span class="sxs-lookup"><span data-stu-id="4a930-400">Set this attribute too1 tooindicate this is hello forced presentation.</span></span> |
| <span data-ttu-id="4a930-401">**HearingImpaired**</span><span class="sxs-lookup"><span data-stu-id="4a930-401">**HearingImpaired**</span></span><br /><br /> <span data-ttu-id="4a930-402">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a930-402">Required</span></span> |<span data-ttu-id="4a930-403">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="4a930-403">**xs:int**</span></span> |<span data-ttu-id="4a930-404">Impostare questo tooindicate too1 attributo che questa traccia è per udenti hello.</span><span class="sxs-lookup"><span data-stu-id="4a930-404">Set this attribute too1 tooindicate this track is for hello hearing impaired.</span></span> |
| <span data-ttu-id="4a930-405">**VisualImpaired**</span><span class="sxs-lookup"><span data-stu-id="4a930-405">**VisualImpaired**</span></span><br /><br /> <span data-ttu-id="4a930-406">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a930-406">Required</span></span> |<span data-ttu-id="4a930-407">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="4a930-407">**xs:int**</span></span> |<span data-ttu-id="4a930-408">Impostare questo tooindicate too1 attributo che questa traccia è per hello vedenti.</span><span class="sxs-lookup"><span data-stu-id="4a930-408">Set this attribute too1 tooindicate this track is for hello visually impaired.</span></span> |
| <span data-ttu-id="4a930-409">**CleanEffects**</span><span class="sxs-lookup"><span data-stu-id="4a930-409">**CleanEffects**</span></span><br /><br /> <span data-ttu-id="4a930-410">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a930-410">Required</span></span> |<span data-ttu-id="4a930-411">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="4a930-411">**xs:int**</span></span> |<span data-ttu-id="4a930-412">Impostare questo tooindicate too1 attributo che questa traccia contiene effetti di trasparenza.</span><span class="sxs-lookup"><span data-stu-id="4a930-412">Set this attribute too1 tooindicate this track has clean effects.</span></span> |
| <span data-ttu-id="4a930-413">**AttachedPic**</span><span class="sxs-lookup"><span data-stu-id="4a930-413">**AttachedPic**</span></span><br /><br /> <span data-ttu-id="4a930-414">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4a930-414">Required</span></span> |<span data-ttu-id="4a930-415">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="4a930-415">**xs:int**</span></span> |<span data-ttu-id="4a930-416">Impostare questo tooindicate too1 attributo che questa traccia contiene immagini.</span><span class="sxs-lookup"><span data-stu-id="4a930-416">Set this attribute too1 tooindicate this track has pictures.</span></span> |

## <span data-ttu-id="4a930-417"><a name="Programs"></a> Elemento Programs</span><span class="sxs-lookup"><span data-stu-id="4a930-417"><a name="Programs"></a> Programs element</span></span>
<span data-ttu-id="4a930-418">Elemento wrapper contenente più elementi **Program**.</span><span class="sxs-lookup"><span data-stu-id="4a930-418">Wrapper element holding multiple **Program** elements.</span></span>  

### <a name="child-elements"></a><span data-ttu-id="4a930-419">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="4a930-419">Child elements</span></span>
| <span data-ttu-id="4a930-420">Nome</span><span class="sxs-lookup"><span data-stu-id="4a930-420">Name</span></span> | <span data-ttu-id="4a930-421">Tipo</span><span class="sxs-lookup"><span data-stu-id="4a930-421">Type</span></span> | <span data-ttu-id="4a930-422">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4a930-422">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4a930-423">**Program**</span><span class="sxs-lookup"><span data-stu-id="4a930-423">**Program**</span></span><br /><br /> <span data-ttu-id="4a930-424">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="4a930-424">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="4a930-425">ProgramType</span><span class="sxs-lookup"><span data-stu-id="4a930-425">ProgramType</span></span>](media-services-input-metadata-schema.md#ProgramType) |<span data-ttu-id="4a930-426">Per i file di asset in formato MPEG-TS, contiene informazioni sui programmi nel file di asset hello.</span><span class="sxs-lookup"><span data-stu-id="4a930-426">For asset files that are in MPEG-TS format, contains information about programs in hello asset file.</span></span> |

## <span data-ttu-id="4a930-427"><a name="VideoTracks"></a> Elemento VideoTracks</span><span class="sxs-lookup"><span data-stu-id="4a930-427"><a name="VideoTracks"></a> VideoTracks element</span></span>
 <span data-ttu-id="4a930-428">Elemento wrapper contenente più elementi **VideoTrack**.</span><span class="sxs-lookup"><span data-stu-id="4a930-428">Wrapper element holding multiple **VideoTrack** elements.</span></span>  

 <span data-ttu-id="4a930-429">Vedere un esempio XML alla fine di hello di questo argomento: [file XML di esempio](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="4a930-429">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="4a930-430">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="4a930-430">Child elements</span></span>
| <span data-ttu-id="4a930-431">Nome</span><span class="sxs-lookup"><span data-stu-id="4a930-431">Name</span></span> | <span data-ttu-id="4a930-432">Tipo</span><span class="sxs-lookup"><span data-stu-id="4a930-432">Type</span></span> | <span data-ttu-id="4a930-433">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4a930-433">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4a930-434">**VideoTrack**</span><span class="sxs-lookup"><span data-stu-id="4a930-434">**VideoTrack**</span></span><br /><br /> <span data-ttu-id="4a930-435">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="4a930-435">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="4a930-436">VideoTrackType (eredita da TrackType)</span><span class="sxs-lookup"><span data-stu-id="4a930-436">VideoTrackType (inherits from TrackType)</span></span>](media-services-input-metadata-schema.md#VideoTrackType) |<span data-ttu-id="4a930-437">Contiene informazioni su tracce video presenti nel file di asset hello.</span><span class="sxs-lookup"><span data-stu-id="4a930-437">Contains information about video tracks in hello asset file.</span></span> |

## <span data-ttu-id="4a930-438"><a name="AudioTracks"></a> Elemento AudioTrack</span><span class="sxs-lookup"><span data-stu-id="4a930-438"><a name="AudioTracks"></a> AudioTracks element</span></span>
 <span data-ttu-id="4a930-439">Elemento wrapper contenente più elementi **AudioTrack**.</span><span class="sxs-lookup"><span data-stu-id="4a930-439">Wrapper element holding multiple **AudioTrack** elements.</span></span>  

 <span data-ttu-id="4a930-440">Vedere un esempio XML alla fine di hello di questo argomento: [file XML di esempio](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="4a930-440">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="elements"></a><span data-ttu-id="4a930-441">Elementi figlio</span><span class="sxs-lookup"><span data-stu-id="4a930-441">elements</span></span>
| <span data-ttu-id="4a930-442">Nome</span><span class="sxs-lookup"><span data-stu-id="4a930-442">Name</span></span> | <span data-ttu-id="4a930-443">Tipo</span><span class="sxs-lookup"><span data-stu-id="4a930-443">Type</span></span> | <span data-ttu-id="4a930-444">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4a930-444">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4a930-445">**AudioTrack**</span><span class="sxs-lookup"><span data-stu-id="4a930-445">**AudioTrack**</span></span><br /><br /> <span data-ttu-id="4a930-446">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="4a930-446">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="4a930-447">AudioTrackType (eredita da TrackType)</span><span class="sxs-lookup"><span data-stu-id="4a930-447">AudioTrackType (inherits from TrackType)</span></span>](media-services-input-metadata-schema.md#AudioTrackType) |<span data-ttu-id="4a930-448">Contiene informazioni su tracce audio presenti nel file di asset hello.</span><span class="sxs-lookup"><span data-stu-id="4a930-448">Contains information about audio tracks in hello asset file.</span></span> |

## <span data-ttu-id="4a930-449"><a name="code"></a> Codice schema</span><span class="sxs-lookup"><span data-stu-id="4a930-449"><a name="code"></a> Schema Code</span></span>
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
            <xs:documentation>zero-based index of this video track. Note: this is not necessarily hello TrackID as used in an MP4 file</xs:documentation>  
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
          <xs:documentation>A specific video track in hello parent AssetFile</xs:documentation>  
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
                <xs:documentation>average video bit rate in kilobits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
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
          <xs:documentation>a specific audio track in hello parent AssetFile</xs:documentation>  
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
                <xs:documentation>average audio bit rate in bits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="BitsPerSample">  
              <xs:annotation>  
                <xs:documentation>Bits per sample for hello wFormatTag format type</xs:documentation>  
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
          <xs:documentation>Collection of AssetFile entries for hello encoding job</xs:documentation>  
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
                      <xs:documentation>This is hello collection of all programs when file is MPEG-TS</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="Program" type="ProgramType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="VideoTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is hello collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" type="VideoTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="AudioTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is hello collection of all those audio tracks</xs:documentation>  
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
                    <xs:documentation>hello media asset file name</xs:documentation>  
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
                    <xs:documentation>average bitrate of hello asset file in kbps</xs:documentation>  
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


## <span data-ttu-id="4a930-450"><a name="xml"></a> Esempio XML</span><span class="sxs-lookup"><span data-stu-id="4a930-450"><a name="xml"></a> XML example</span></span>
<span data-ttu-id="4a930-451">Hello Ecco un esempio di file di metadati di Input hello.</span><span class="sxs-lookup"><span data-stu-id="4a930-451">hello following is an example of hello Input metadata file.</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="4a930-452">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4a930-452">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4a930-453">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="4a930-453">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

