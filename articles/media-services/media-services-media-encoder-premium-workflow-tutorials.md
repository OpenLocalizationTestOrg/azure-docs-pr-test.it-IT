---
title: esercitazioni di flusso di lavoro Premium del codificatore multimediale aaaAvanced
description: "Questo documento contiene procedure dettagliate che illustrano come tooperform avanzate attività con flusso di lavoro Premium del codificatore multimediale e anche come toocreate flussi di lavoro complessi con Progettazione flussi di lavoro."
services: media-services
documentationcenter: 
author: xstof
manager: cfowler
editor: 
ms.assetid: 1ba52865-b4a8-4ca0-ac96-920d55b9d15b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: christoc;xpouyat;juliako
ms.openlocfilehash: 641bd1be3bd795b5e138fa7ffdf299ff6710904e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-media-encoder-premium-workflow-tutorials"></a><span data-ttu-id="ff041-103">Esercitazioni avanzate del flusso di lavoro Premium del codificatore multimediale</span><span class="sxs-lookup"><span data-stu-id="ff041-103">Advanced Media Encoder Premium Workflow tutorials</span></span>
## <a name="overview"></a><span data-ttu-id="ff041-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="ff041-104">Overview</span></span>
<span data-ttu-id="ff041-105">Questo documento contiene procedure dettagliate che illustrano come flussi di lavoro toocustomize con **Progettazione flussi di lavoro**.</span><span class="sxs-lookup"><span data-stu-id="ff041-105">This document contains walkthroughs that show how toocustomize workflows with  **Workflow Designer**.</span></span> <span data-ttu-id="ff041-106">È possibile trovare i file del flusso di lavoro effettivo hello [qui](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples).</span><span class="sxs-lookup"><span data-stu-id="ff041-106">You can find hello actual workflow files [here](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples).</span></span>  

## <a name="toc"></a><span data-ttu-id="ff041-107">Sommario</span><span class="sxs-lookup"><span data-stu-id="ff041-107">TOC</span></span>
<span data-ttu-id="ff041-108">viene trattato i seguenti argomenti Hello:</span><span class="sxs-lookup"><span data-stu-id="ff041-108">hello following topics are covered:</span></span>

* [<span data-ttu-id="ff041-109">Codifica di un file MXF in un MP4 a velocità in bit singola</span><span class="sxs-lookup"><span data-stu-id="ff041-109">Encoding MXF into a single bitrate MP4</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)
  * [<span data-ttu-id="ff041-110">Avvio di un nuovo flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="ff041-110">Starting a new workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_start_new)
  * [<span data-ttu-id="ff041-111">Utilizzo di hello Input del File di supporto</span><span class="sxs-lookup"><span data-stu-id="ff041-111">Using hello Media File Input</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_file_input)
  * [<span data-ttu-id="ff041-112">Analisi di flussi multimediali</span><span class="sxs-lookup"><span data-stu-id="ff041-112">Inspecting media streams</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_streams)
  * [<span data-ttu-id="ff041-113">Aggiunta di un codificatore video per la generazione di file MP4</span><span class="sxs-lookup"><span data-stu-id="ff041-113">Adding a video encoder for .MP4 file generation</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_file_generation)
  * [<span data-ttu-id="ff041-114">Flusso audio di codifica hello</span><span class="sxs-lookup"><span data-stu-id="ff041-114">Encoding hello audio stream</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio)
  * [<span data-ttu-id="ff041-115">Multiplexing di flussi audio e video in un contenitore MP4</span><span class="sxs-lookup"><span data-stu-id="ff041-115">Multiplexing Audio and Video streams into an MP4 container</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio_and_fideo)
  * [<span data-ttu-id="ff041-116">Scrittura di file MP4 hello</span><span class="sxs-lookup"><span data-stu-id="ff041-116">Writing hello MP4 file</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_writing_mp4)
  * [<span data-ttu-id="ff041-117">Creazione di un Asset di servizi multimediali dal file di output di hello</span><span class="sxs-lookup"><span data-stu-id="ff041-117">Creating a Media Services Asset from hello output file</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_asset_from_output)
  * [<span data-ttu-id="ff041-118">Hello test completato del flusso di lavoro locale</span><span class="sxs-lookup"><span data-stu-id="ff041-118">Test hello finished workflow locally</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_test)
* [<span data-ttu-id="ff041-119">Codifica di un file MXF in MP4 a velocità in bit multipla - Creazione dinamica dei pacchetti abilitata</span><span class="sxs-lookup"><span data-stu-id="ff041-119">Encoding MXF into multibitrate MP4s - dynamic packaging enabled</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)
  * [<span data-ttu-id="ff041-120">Aggiunta di uno o più output MP4</span><span class="sxs-lookup"><span data-stu-id="ff041-120">Adding one or more additional MP4 outputs</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_more_outputs)
  * [<span data-ttu-id="ff041-121">Output nomi file di configurazione hello</span><span class="sxs-lookup"><span data-stu-id="ff041-121">Configuring hello file output names</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_conf_output_names)
  * [<span data-ttu-id="ff041-122">Aggiunta di una traccia audio separata</span><span class="sxs-lookup"><span data-stu-id="ff041-122">Adding a separate Audio Track</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_audio_tracks)
  * [<span data-ttu-id="ff041-123">Aggiunta di hello. File SMIL ISM</span><span class="sxs-lookup"><span data-stu-id="ff041-123">Adding hello .ISM SMIL File</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_ism_file)
* [<span data-ttu-id="ff041-124">Codifica di un file MXF in un MP4 a velocità in bit multipla - Progetto avanzato</span><span class="sxs-lookup"><span data-stu-id="ff041-124">Encoding MXF into multibitrate MP4 - enhanced blueprint</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4)
  * [<span data-ttu-id="ff041-125">Flusso di lavoro Panoramica tooenhance</span><span class="sxs-lookup"><span data-stu-id="ff041-125">Workflow overview tooenhance</span></span>](#workflow-overview-to-enhance)
  * [<span data-ttu-id="ff041-126">Convenzioni di denominazione dei file</span><span class="sxs-lookup"><span data-stu-id="ff041-126">File Naming Conventions</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_file_naming)
  * [<span data-ttu-id="ff041-127">La pubblicazione delle proprietà del componente nella radice del flusso di lavoro hello</span><span class="sxs-lookup"><span data-stu-id="ff041-127">Publishing component properties onto hello workflow root</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_publishing)
  * [<span data-ttu-id="ff041-128">Fare in modo che i nomi file di output generati si basino sui valori delle proprietà pubblicati</span><span class="sxs-lookup"><span data-stu-id="ff041-128">Have generated output file names rely on published property values</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_output_files)
* [<span data-ttu-id="ff041-129">Aggiunta dell'output di anteprime toomultibitrate MP4</span><span class="sxs-lookup"><span data-stu-id="ff041-129">Adding thumbnails toomultibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4)
  * [<span data-ttu-id="ff041-130">Flusso di lavoro Panoramica tooadd anteprime</span><span class="sxs-lookup"><span data-stu-id="ff041-130">Workflow overview tooadd thumbnails to</span></span>](#workflow-overview-to-add-thumbnails-to)
  * [<span data-ttu-id="ff041-131">Aggiunta della codifica JPG</span><span class="sxs-lookup"><span data-stu-id="ff041-131">Adding JPG Encoding</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4__with_jpg)
  * [<span data-ttu-id="ff041-132">Gestione della conversione dello spazio colore</span><span class="sxs-lookup"><span data-stu-id="ff041-132">Dealing with Color Space conversion</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_color_space)
  * [<span data-ttu-id="ff041-133">Anteprime di hello scrittura</span><span class="sxs-lookup"><span data-stu-id="ff041-133">Writing hello thumbnails</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_writing_thumbnails)
  * [<span data-ttu-id="ff041-134">Rilevamento di errori in un flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="ff041-134">Detecting errors in a workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_errors)
  * [<span data-ttu-id="ff041-135">Flusso di lavoro completato</span><span class="sxs-lookup"><span data-stu-id="ff041-135">Finished Workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_finish)
* [<span data-ttu-id="ff041-136">Taglio basato sull'ora dell'output MP4 a velocità in bit multipla</span><span class="sxs-lookup"><span data-stu-id="ff041-136">Time-based trimming of multibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim)
  * [<span data-ttu-id="ff041-137">Flusso di lavoro Panoramica toostart aggiunta di taglio per</span><span class="sxs-lookup"><span data-stu-id="ff041-137">Workflow overview toostart adding trimming to</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_start)
  * [<span data-ttu-id="ff041-138">Utilizzo di hello compensatore di flusso</span><span class="sxs-lookup"><span data-stu-id="ff041-138">Using hello Stream Trimmer</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_use_stream_trimmer)
  * [<span data-ttu-id="ff041-139">Flusso di lavoro completato</span><span class="sxs-lookup"><span data-stu-id="ff041-139">Finished Workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_finish)
* [<span data-ttu-id="ff041-140">Introduzione a hello componente script</span><span class="sxs-lookup"><span data-stu-id="ff041-140">Introducing hello Scripted Component</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#scripting)
  * [<span data-ttu-id="ff041-141">Scripting in un flusso di lavoro: hello world</span><span class="sxs-lookup"><span data-stu-id="ff041-141">Scripting within a workflow: hello world</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#scripting_hello_world)
* [<span data-ttu-id="ff041-142">Taglio basato sul fotogramma dell'output MP4 a velocità in bit multipla</span><span class="sxs-lookup"><span data-stu-id="ff041-142">Frame-based trimming of multibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim)
  * [<span data-ttu-id="ff041-143">Cianografia toostart Panoramica aggiunta la rimozione di</span><span class="sxs-lookup"><span data-stu-id="ff041-143">Blueprint overview toostart adding trimming to</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_start)
  * [<span data-ttu-id="ff041-144">Utilizzo di hello Clip elenco XML</span><span class="sxs-lookup"><span data-stu-id="ff041-144">Using hello Clip List XML</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clip_list)
  * [<span data-ttu-id="ff041-145">Modifica elenco di clip hello da un componente script</span><span class="sxs-lookup"><span data-stu-id="ff041-145">Modifying hello clip list from a Scripted Component</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_modify_clip_list)
  * [<span data-ttu-id="ff041-146">Aggiunta di una pratica proprietà ClippingEnabled</span><span class="sxs-lookup"><span data-stu-id="ff041-146">Adding a ClippingEnabled convenience property</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clippingenabled_prop)

## <span data-ttu-id="ff041-147"><a id="MXF_to_MP4"></a>Codifica di un file MXF in un MP4 a velocità in bit singola</span><span class="sxs-lookup"><span data-stu-id="ff041-147"><a id="MXF_to_MP4"></a>Encoding MXF into a single bitrate MP4</span></span>
<span data-ttu-id="ff041-148">In questa procedura dettagliata verrà creato un file MP4 a velocità in bit singola con audio con codifica AAC-HE da un file di input MXF.</span><span class="sxs-lookup"><span data-stu-id="ff041-148">In this walkthrough we'll create a single bitrate .MP4 file with AAC-HE encoded audio from an .MXF input file.</span></span>

### <span data-ttu-id="ff041-149"><a id="MXF_to_MP4_start_new"></a>Avvio di un nuovo flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="ff041-149"><a id="MXF_to_MP4_start_new"></a>Starting a new workflow</span></span>
<span data-ttu-id="ff041-150">Aprire Progettazione flussi di lavoro e selezionare "File" - "New Workspace" - "Transcode Blueprint"</span><span class="sxs-lookup"><span data-stu-id="ff041-150">Open Workflow Designer and select "File"-"New Workspace"-"Transcode Blueprint"</span></span>

<span data-ttu-id="ff041-151">nuovo flusso di lavoro Hello visualizzerà 3 elementi:</span><span class="sxs-lookup"><span data-stu-id="ff041-151">hello new workflow will show 3 elements:</span></span>

* <span data-ttu-id="ff041-152">Primary Source File</span><span class="sxs-lookup"><span data-stu-id="ff041-152">Primary Source File</span></span>
* <span data-ttu-id="ff041-153">Clip List XML</span><span class="sxs-lookup"><span data-stu-id="ff041-153">Clip List XML</span></span>
* <span data-ttu-id="ff041-154">Output File/Asset</span><span class="sxs-lookup"><span data-stu-id="ff041-154">Output File/Asset</span></span>  

![Nuovo flusso di lavoro della codifica](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-transcode-blueprint.png)

<span data-ttu-id="ff041-156">*Nuovo flusso di lavoro della codifica*</span><span class="sxs-lookup"><span data-stu-id="ff041-156">*New Encoding Workflow*</span></span>

### <span data-ttu-id="ff041-157"><a id="MXF_to_MP4_with_file_input"></a>Utilizzo di hello Input del File di supporto</span><span class="sxs-lookup"><span data-stu-id="ff041-157"><a id="MXF_to_MP4_with_file_input"></a>Using hello Media File Input</span></span>
<span data-ttu-id="ff041-158">In ordine tooaccept il file multimediale di input, uno inizia con l'aggiunta di un componente di Input di File multimediali.</span><span class="sxs-lookup"><span data-stu-id="ff041-158">In order tooaccept our input media file, one starts with adding a Media File Input component.</span></span> <span data-ttu-id="ff041-159">tooadd un componente toohello del flusso di lavoro, cercare nella casella di ricerca Repository hello e trascinare la voce hello desiderato nel riquadro della finestra di progettazione di hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-159">tooadd a component toohello workflow, look for it in hello Repository search box and drag hello desired entry onto hello designer pane.</span></span> <span data-ttu-id="ff041-160">Eseguire questa operazione per l'Input di File multimediali hello e connettersi hello File di origine primario componente toohello Filename pin di input da hello supporti File di Input.</span><span class="sxs-lookup"><span data-stu-id="ff041-160">Do this for hello Media File Input and connect hello Primary Source File component toohello Filename input pin from hello Media File Input.</span></span>

![Media File Input connesso](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-input.png)

<span data-ttu-id="ff041-162">*Media File Input connesso*</span><span class="sxs-lookup"><span data-stu-id="ff041-162">*Connected Media File Input*</span></span>

<span data-ttu-id="ff041-163">Prima di effettuare molte altre operazioni, è prima necessario Progettazione flussi di lavoro di tooindicate toohello il file di esempio desideriamo toouse toodesign con il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="ff041-163">Before we can do much else, we'll first need tooindicate toohello workflow designer what sample file we'd like toouse toodesign our workflow with.</span></span> <span data-ttu-id="ff041-164">toodo in tal caso, fare clic sullo sfondo della finestra di progettazione riquadro hello e cercare proprietà File di origine primario hello nel riquadro di destra proprietà hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-164">toodo so, click hello designer pane background and look for hello Primary Source File property on hello right-hand property pane.</span></span> <span data-ttu-id="ff041-165">Fare clic sull'icona di cartella hello e selezionare hello desiderato file tootest hello flusso di lavoro con.</span><span class="sxs-lookup"><span data-stu-id="ff041-165">Click hello folder icon and select hello desired file tootest hello workflow with.</span></span> <span data-ttu-id="ff041-166">Non appena questa operazione viene eseguita, hello Input File multimediali componente esaminare il file hello e popolare il file di hello tooreflect pin di output che controllato.</span><span class="sxs-lookup"><span data-stu-id="ff041-166">As soon as this is done, hello Media File Input component will inspect hello file and populate its output pins tooreflect hello file it inspected.</span></span>

![Media File Input popolato](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-populated-media-file-input.png)

<span data-ttu-id="ff041-168">*Media File Input popolato*</span><span class="sxs-lookup"><span data-stu-id="ff041-168">*Populated Media File Input*</span></span>

<span data-ttu-id="ff041-169">Mentre con il tipo di input che desideriamo toowork con specifica, non ti dirà ancora in output di hello con codificata da utilizzare.</span><span class="sxs-lookup"><span data-stu-id="ff041-169">While this specifies with what input we'd like toowork with, it doesn't tell yet where hello encoded output should go to.</span></span> <span data-ttu-id="ff041-170">Simile hello toohow File di origine primario è stato configurato, configurare proprietà della variabile di cartella di Output, solo di sotto di hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-170">Similar toohow hello Primary Source File was configured, now configure hello Output Folder Variable property, just below it.</span></span>

![Proprietà di input e output configurate](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configured-io-properties.png)

<span data-ttu-id="ff041-172">*Proprietà di input e output configurate*</span><span class="sxs-lookup"><span data-stu-id="ff041-172">*Configured Input and Output properties*</span></span>

### <span data-ttu-id="ff041-173"><a id="MXF_to_MP4_streams"></a>Analisi di flussi multimediali</span><span class="sxs-lookup"><span data-stu-id="ff041-173"><a id="MXF_to_MP4_streams"></a>Inspecting media streams</span></span>
<span data-ttu-id="ff041-174">Spesso è preferibile tooknow aspetto di questo flusso hello sono illustrate le fasi del flusso di lavoro di hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-174">Often it's desired tooknow how hello stream looks like that flows through hello workflow.</span></span> <span data-ttu-id="ff041-175">solo tooinspect un flusso in qualsiasi punto del flusso di lavoro di hello, fare clic su un output o il pin di input in uno qualsiasi dei componenti di hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-175">tooinspect a stream at any point in hello workflow, just click an output or input pin on any of hello components.</span></span> <span data-ttu-id="ff041-176">In questo caso, provare a fare clic sul pin di output di hello Video non compressi dall'Input del File di supporto.</span><span class="sxs-lookup"><span data-stu-id="ff041-176">In this case, try clicking on hello Uncompressed Video output pin from our Media File Input.</span></span> <span data-ttu-id="ff041-177">Verrà aperta una finestra di dialogo che consente tooinspect hello in uscita video.</span><span class="sxs-lookup"><span data-stu-id="ff041-177">A dialog will open up that allows tooinspect hello outbound video.</span></span>

![Esame pin di output di hello Video non compresso](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-inspecting-uncompressed-video-output.png)

<span data-ttu-id="ff041-179">*Esame pin di output di hello Video non compresso*</span><span class="sxs-lookup"><span data-stu-id="ff041-179">*Inspecting hello Uncompressed Video output pin*</span></span>

<span data-ttu-id="ff041-180">In questo caso, ad esempio, indica che si ha a che fare con un input 1920x1080 a 24 fotogrammi al secondo nel campionamento 4:2:2 per un video di almeno 2 minuti.</span><span class="sxs-lookup"><span data-stu-id="ff041-180">In our case, it tells us for example that we're dealing with a 1920x1080 input at 24 frames per second in 4:2:2 sampling for a video of almost 2 minutes.</span></span>

### <span data-ttu-id="ff041-181"><a id="MXF_to_MP4_file_generation"></a>Aggiunta di un codificatore video per la generazione di file MP4</span><span class="sxs-lookup"><span data-stu-id="ff041-181"><a id="MXF_to_MP4_file_generation"></a>Adding a video encoder for .MP4 file generation</span></span>
<span data-ttu-id="ff041-182">Si noti che ora in Media File Input sono disponibili per l'uso un pin Uncompressed Video e più pin di output Uncompressed Audio.</span><span class="sxs-lookup"><span data-stu-id="ff041-182">Note that now, an Uncompressed Video and multiple Uncompressed Audio output pins are available for use on our Media File Input.</span></span> <span data-ttu-id="ff041-183">In ordine tooencode hello video in ingresso, è necessario un componente di codifica, in questo caso per la generazione. File MP4.</span><span class="sxs-lookup"><span data-stu-id="ff041-183">In order tooencode hello inbound video, we need an encoding component - in this case for generating .MP4 files.</span></span>

<span data-ttu-id="ff041-184">tooencode hello tooH.264 flusso video, aggiungere l'area della finestra di progettazione toohello hello codificatore Video AVC dei componenti.</span><span class="sxs-lookup"><span data-stu-id="ff041-184">tooencode hello video stream tooH.264, add hello AVC Video Encoder component toohello designer surface.</span></span> <span data-ttu-id="ff041-185">Questo componente accetta un flusso video non compresso e genera un flusso video compresso AVC nel pin di output.</span><span class="sxs-lookup"><span data-stu-id="ff041-185">This component takes an uncompress video stream as input and delivers an AVC compressed video stream on its output pin.</span></span>

![Codificatore AVC non connesso](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-avc-encoder.png)

<span data-ttu-id="ff041-187">*Codificatore AVC non connesso*</span><span class="sxs-lookup"><span data-stu-id="ff041-187">*Unconnected AVC Encoder*</span></span>

<span data-ttu-id="ff041-188">Le proprietà determinano come codifica hello esattamente avviene.</span><span class="sxs-lookup"><span data-stu-id="ff041-188">Its properties determine how hello encoding exactly happens.</span></span> <span data-ttu-id="ff041-189">Di seguito sono descritte alcune di hello impostazioni più importanti:</span><span class="sxs-lookup"><span data-stu-id="ff041-189">Let's have a look at some of hello more important settings:</span></span>

* <span data-ttu-id="ff041-190">Larghezza di output e l'altezza di Output: consentono di determinare la risoluzione di hello del video codificato hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-190">Output width and Output height: these determine hello resolution of hello encoded video.</span></span> <span data-ttu-id="ff041-191">In questo caso, si usa 640x360.</span><span class="sxs-lookup"><span data-stu-id="ff041-191">In our case let's go with 640x360</span></span>
* <span data-ttu-id="ff041-192">Frequenza dei fotogrammi: quando toopassthrough set verranno semplicemente adottano frequenza dei fotogrammi hello origine, è possibile toooverride questo tuttavia.</span><span class="sxs-lookup"><span data-stu-id="ff041-192">Frame Rate: when set toopassthrough it will just adopt hello source frame rate, it's possible toooverride this though.</span></span> <span data-ttu-id="ff041-193">Si noti che tale conversione della frequenza dei fotogrammi non è compensata dal movimento.</span><span class="sxs-lookup"><span data-stu-id="ff041-193">Note that such framerate conversion is not motion-compensated.</span></span>
* <span data-ttu-id="ff041-194">Profilo e il livello: consentono di determinare il profilo di hello AVC e il livello.</span><span class="sxs-lookup"><span data-stu-id="ff041-194">Profile and Level: these determine hello AVC profile and level.</span></span> <span data-ttu-id="ff041-195">tooconveniently ottenere ulteriori informazioni su livelli diversi di hello e profili, fare clic sull'icona di punto interrogativo hello sul componente codificatore Video AVC hello e pagina della Guida hello verrà visualizzati ulteriori informazioni su ciascuno dei livelli di hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-195">tooconveniently get more information about hello different levels and profiles, click hello question mark icon on hello AVC Video Encoder component and hello help page will show more detail about each of hello levels.</span></span> <span data-ttu-id="ff041-196">Per l'esempio Proviamo il profilo principale a livello 3.2 (impostazione predefinita hello).</span><span class="sxs-lookup"><span data-stu-id="ff041-196">For our sample, let's go with Main Profile at level 3.2 (hello default).</span></span>
* <span data-ttu-id="ff041-197">Rate Control Mode e Bitrate (kbps): in questo scenario viene usato un output con velocità in bit costante (CBR) a 1200 kbps</span><span class="sxs-lookup"><span data-stu-id="ff041-197">Rate Control Mode and Bitrate (kbps): in our scenario we opt for a constant bitrate (CBR) output at 1200 kbps</span></span>
* <span data-ttu-id="ff041-198">Formato video: questo argomento vengono descritti hello VUI (Video di usabilità Information) che vengono scritte nel flusso di hello h. 264 (le informazioni sul lato che potrebbero essere utilizzate da un decodificatore tooenhance hello visualizzazione, ma non è essenziale toocorrectly decodificare):</span><span class="sxs-lookup"><span data-stu-id="ff041-198">Video Format: this is about hello VUI (Video Usability Information) that gets written into hello H.264 stream (side information that might be used by a decoder tooenhance hello display but not essential toocorrectly decode):</span></span>
* <span data-ttu-id="ff041-199">NTSC (tipico per Stati Uniti o Giappone, usa 30 fps)</span><span class="sxs-lookup"><span data-stu-id="ff041-199">NTSC (typical for US or Japan, using 30 fps)</span></span>
* <span data-ttu-id="ff041-200">PAL (tipico per l'Europa, usa 25 fps)</span><span class="sxs-lookup"><span data-stu-id="ff041-200">PAL (typical for Europe, using 25 fps)</span></span>
* <span data-ttu-id="ff041-201">GOP Size Mode: in questo caso, verrà configurata una dimensione GOP fissa con un intervallo chiave di 2 secondi con GOP chiusi.</span><span class="sxs-lookup"><span data-stu-id="ff041-201">GOP Size Mode: we'll configure Fixed GOP Size for our purposes with a Key Interval of 2 seconds with Closed GOPs.</span></span> <span data-ttu-id="ff041-202">Ciò garantisce la compatibilità con hello che fornisce servizi multimediali di Azure di creazione dinamica dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="ff041-202">This ensures compatibility with hello dynamic packaging Azure Media Services provides.</span></span>

<span data-ttu-id="ff041-203">toofeed il codificatore AVC, connettersi pin di output di hello Video non compressi da hello supporti File componente toohello Video non compressi input pin di Input dal codificatore hello AVC.</span><span class="sxs-lookup"><span data-stu-id="ff041-203">toofeed our AVC encoder, connect hello Uncompressed Video output pin from hello Media File Input component toohello Uncompressed Video input pin from hello AVC encoder.</span></span>

![Codificatore AVC connesso](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-avc-encoder.png)

<span data-ttu-id="ff041-205">*Codificatore principale AVC connesso*</span><span class="sxs-lookup"><span data-stu-id="ff041-205">*Connected AVC Main encoder*</span></span>

### <span data-ttu-id="ff041-206"><a id="MXF_to_MP4_audio"></a>Flusso audio di codifica hello</span><span class="sxs-lookup"><span data-stu-id="ff041-206"><a id="MXF_to_MP4_audio"></a>Encoding hello audio stream</span></span>
<span data-ttu-id="ff041-207">A questo punto, è stato codificato video ma hello flusso di audio non compresso originale deve comunque toobe compressi.</span><span class="sxs-lookup"><span data-stu-id="ff041-207">At this point, we have encoded video but hello original uncompressed audio stream still needs toobe compressed.</span></span> <span data-ttu-id="ff041-208">Per questo verranno prese con AAC codifica hello componente codificatore AAC (Dolby).</span><span class="sxs-lookup"><span data-stu-id="ff041-208">For this we'll go with AAC encoding by hello AAC Encoder (Dolby) component.</span></span> <span data-ttu-id="ff041-209">Aggiungerlo toohello del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="ff041-209">Add it toohello workflow.</span></span>

![Codificatore AVC non connesso](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-aac-encoder.png)

<span data-ttu-id="ff041-211">*Codificatore AAC non connesso*</span><span class="sxs-lookup"><span data-stu-id="ff041-211">*Unconnected AAC encoder*</span></span>

<span data-ttu-id="ff041-212">Ora è presente un problema di incompatibilità: è presente solo un singolo non compresso audio pin di input dal codificatore AAC hello mentre più probabile hello supporti File di Input avranno due diversi non compressi flusso audio disponibile: uno per hello canale audio e uno per hello a sinistra Ok.</span><span class="sxs-lookup"><span data-stu-id="ff041-212">Now there's an incompatibility: there's only a single uncompressed audio input pin from hello AAC Encoder while more than likely hello Media File Input will have two different uncompressed audio stream available: one for hello left audio channel and one for hello right.</span></span> <span data-ttu-id="ff041-213">Se si usa un sistema audio di tipo surround, i canali saranno addirittura 6. Pertanto non è possibile toodirectly collegare audio hello dall'origine di Input di File multimediali hello codifica audio AAC di hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-213">(If you're dealing with surround sound, that's 6 channels.) So it's not possible toodirectly connect hello audio from hello Media File Input source into hello AAC audio encoder.</span></span> <span data-ttu-id="ff041-214">componente AAC Hello prevede un flusso audio "interleaved" cosiddetto: un singolo flusso che contiene sia hello canali destra a sinistra e hello interlacciati tra loro.</span><span class="sxs-lookup"><span data-stu-id="ff041-214">hello AAC component expects a so-called "interleaved" audio stream: a single stream that has both hello left and hello right channels interleaved with each other.</span></span> <span data-ttu-id="ff041-215">Una volta acquisite da questo file di origine le tracce audio la posizione nell'origine hello, è possibile generare tali interleaved flusso audio con hello correttamente assegnati posizioni degli altoparlanti per left e right.</span><span class="sxs-lookup"><span data-stu-id="ff041-215">Once we know from our source media file which audio tracks are on what position in hello source, we can generate such interleaved audio stream with hello correctly assigned speaker positions for left and right.</span></span>

<span data-ttu-id="ff041-216">Prima di tutto uno desidererà toogenerated un flusso di interfoliazione da canali audio sorgente hello necessario.</span><span class="sxs-lookup"><span data-stu-id="ff041-216">First one will want toogenerated an interleaved stream from hello required source audio channels.</span></span> <span data-ttu-id="ff041-217">componente Interleaver flusso Audio Hello questo gestirà automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ff041-217">hello Audio Stream Interleaver component will handle this for us.</span></span> <span data-ttu-id="ff041-218">Aggiungerlo toohello del flusso di lavoro e la connessione di output audio hello da hello Input del File di supporto al suo interno.</span><span class="sxs-lookup"><span data-stu-id="ff041-218">Add it toohello workflow and connect hello audio outputs from hello Media File Input into it.</span></span>

![Audio Stream Interleaver connesso](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-audio-stream-interleaver.png)

<span data-ttu-id="ff041-220">*Audio Stream Interleaver connesso*</span><span class="sxs-lookup"><span data-stu-id="ff041-220">*Connected Audio Stream Interleaver*</span></span>

<span data-ttu-id="ff041-221">Ora che è disponibile un flusso audio interleaved, è ancora non sono state specificate in altoparlante sinistro o destro di hello tooassign posiziona per.</span><span class="sxs-lookup"><span data-stu-id="ff041-221">Now that we have an interleaved audio stream, we still didn't specify where tooassign hello left or right speaker positions to.</span></span> <span data-ttu-id="ff041-222">In ordine toospecify questo, è possibile sfruttare tutte hello chi assegna posizione degli altoparlanti.</span><span class="sxs-lookup"><span data-stu-id="ff041-222">In order toospecify this, we can leverage hello Speaker Position Assigner.</span></span>

![Aggiunta di Speaker Position Assigner](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-speaker-position-assigner.png)

<span data-ttu-id="ff041-224">*Aggiunta di Speaker Position Assigner*</span><span class="sxs-lookup"><span data-stu-id="ff041-224">*Adding a Speaker Position Assigner*</span></span>

<span data-ttu-id="ff041-225">Configurare hello chi assegna posizione altoparlante per l'utilizzo con un flusso di input stereo tramite un filtro di set di impostazioni del codificatore "Custom" e hello canale predefinito denominato "2.0 (L, R)".</span><span class="sxs-lookup"><span data-stu-id="ff041-225">Configure hello Speaker Position Assigner for use with a stereo input stream through an Encoder Preset Filter of "Custom" and hello Channel Preset called "2.0 (L,R)".</span></span> <span data-ttu-id="ff041-226">(Questo assegnerà hello altoparlante sinistro posizione toochannel 1 e hello altoparlante destro posizione toochannel 2.)</span><span class="sxs-lookup"><span data-stu-id="ff041-226">(This will assign hello left speaker position toochannel 1 and hello right speaker position toochannel 2.)</span></span>

<span data-ttu-id="ff041-227">Connettere l'output di hello dell'input di toohello chi assegna posizione altoparlante hello di hello AAC codificatore.</span><span class="sxs-lookup"><span data-stu-id="ff041-227">Connect hello output of hello Speaker Position Assigner toohello input of hello AAC Encoder.</span></span> <span data-ttu-id="ff041-228">Specificare quindi la hello AAC codificatore toowork con una "2.0 (L, R)" canale predefinito, indicargli toodeal con audio stereo come input.</span><span class="sxs-lookup"><span data-stu-id="ff041-228">Then, tell hello AAC Encoder toowork with a "2.0 (L,R)" Channel Preset, so it knows toodeal with stereo audio as input.</span></span>

### <span data-ttu-id="ff041-229"><a id="MXF_to_MP4_audio_and_fideo"></a>Multiplexing di flussi audio e video in un contenitore MP4</span><span class="sxs-lookup"><span data-stu-id="ff041-229"><a id="MXF_to_MP4_audio_and_fideo"></a>Multiplexing Audio and Video streams into an MP4 container</span></span>
<span data-ttu-id="ff041-230">È possibile acquisire sia il flusso video con codifica AVC che il flusso audio con codifica AAC in un contenitore MP4.</span><span class="sxs-lookup"><span data-stu-id="ff041-230">Given our AVC encoded video stream and our AAC encoded audio stream, we can capture both into an .MP4 container.</span></span> <span data-ttu-id="ff041-231">il processo di Hello di combinazione di flussi diversi in un unico viene chiamato "multiplexing" (o "muxing").</span><span class="sxs-lookup"><span data-stu-id="ff041-231">hello process of mixing different streams into a single one is called "multiplexing" (or "muxing").</span></span> <span data-ttu-id="ff041-232">In questo caso ci stiamo interfoliazione hello flussi audio e hello video in una singola coerente. Pacchetto di file MP4.</span><span class="sxs-lookup"><span data-stu-id="ff041-232">In this case we're interleaving hello audio and hello video streams in a single coherent .MP4 package.</span></span> <span data-ttu-id="ff041-233">componente Hello che coordina per un. Contenitore MP4 viene chiamato hello Multiplexer ISO MPEG-4.</span><span class="sxs-lookup"><span data-stu-id="ff041-233">hello component that coordinates this for an .MP4 container is called hello ISO MPEG-4 Multiplexer.</span></span> <span data-ttu-id="ff041-234">Aggiungere un'area di progettazione toohello e connettere hello codificatore Video AVC sia gli input di tooits AAC codificatore hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-234">Add one toohello designer surface and connect both hello AVC Video Encoder and hello AAC Encoder tooits inputs.</span></span>

![MPEG4 Multiplexer connesso](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-mpeg4-multiplexer.png)

<span data-ttu-id="ff041-236">*MPEG4 Multiplexer connesso*</span><span class="sxs-lookup"><span data-stu-id="ff041-236">*Connected MPEG4 Multiplexer*</span></span>

### <span data-ttu-id="ff041-237"><a id="MXF_to_MP4_writing_mp4"></a>Scrittura di file MP4 hello</span><span class="sxs-lookup"><span data-stu-id="ff041-237"><a id="MXF_to_MP4_writing_mp4"></a>Writing hello MP4 file</span></span>
<span data-ttu-id="ff041-238">Quando si scrive un file di output, viene utilizzato il componente di Output del File hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-238">When writing an output file, hello File Output component is used.</span></span> <span data-ttu-id="ff041-239">È possibile connettersi a questo output toohello di hello multiplexer ISO MPEG-4, in modo che l'output viene scritto toodisk.</span><span class="sxs-lookup"><span data-stu-id="ff041-239">We can connect this toohello output of hello ISO MPEG-4 Multiplexer so that its output gets written toodisk.</span></span> <span data-ttu-id="ff041-240">toodo, connettersi hello contenitore (MPEG-4) pin toohello scrittura input pin di output di hello File di Output.</span><span class="sxs-lookup"><span data-stu-id="ff041-240">toodo this, connect hello Container (MPEG-4) output pin toohello Write input pin of hello File Output.</span></span>

![File Output connesso](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-file-output.png)

<span data-ttu-id="ff041-242">*File Output connesso*</span><span class="sxs-lookup"><span data-stu-id="ff041-242">*Connected File Output*</span></span>

<span data-ttu-id="ff041-243">filename Hello che verrà utilizzato è determinato dalla proprietà del File hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-243">hello filename that will be used is determined by hello File property.</span></span> <span data-ttu-id="ff041-244">Tale proprietà può essere hardcoded tooa dato valore, più probabilmente una desidererà tooset tramite un'espressione invece.</span><span class="sxs-lookup"><span data-stu-id="ff041-244">While that property can be hardcoded tooa given value, most likely one will want tooset it through an expression instead.</span></span>

<span data-ttu-id="ff041-245">flusso di lavoro hello toohave determinare automaticamente l'output di hello da un'espressione di proprietà del nome di File, scegliere il nome del File hello pulsante successivo toohello (icona di cartella toohello Avanti).</span><span class="sxs-lookup"><span data-stu-id="ff041-245">toohave hello workflow automatically determine hello output File name property from an expression, click hello buton next toohello File name (next toohello folder icon).</span></span> <span data-ttu-id="ff041-246">Da hello menu a discesa, quindi selezionare "Espressione".</span><span class="sxs-lookup"><span data-stu-id="ff041-246">From hello drop down menu then select "Expression".</span></span> <span data-ttu-id="ff041-247">Verrà visualizzata editor espressioni hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-247">This will bring up hello expression editor.</span></span> <span data-ttu-id="ff041-248">Cancella contenuto hello dell'editor di hello prima.</span><span class="sxs-lookup"><span data-stu-id="ff041-248">Clear hello contents of hello editor first.</span></span>

![Expression Editor vuoto](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-empty-expression-editor.png)

<span data-ttu-id="ff041-250">*Expression Editor vuoto*</span><span class="sxs-lookup"><span data-stu-id="ff041-250">*Empty Expression Editor*</span></span>

<span data-ttu-id="ff041-251">editor di espressioni Hello consente tooenter qualsiasi valore letterale, combinato con una o più variabili.</span><span class="sxs-lookup"><span data-stu-id="ff041-251">hello expression editor allows tooenter any literal value, mixed with one or more variables.</span></span> <span data-ttu-id="ff041-252">Le variabili iniziano con un simbolo di dollaro.</span><span class="sxs-lookup"><span data-stu-id="ff041-252">Variables start with a dollar sign.</span></span> <span data-ttu-id="ff041-253">Quando si premere il tasto di $ hello, dell'editor di hello verrà visualizzata una casella a discesa con una scelta delle variabili disponibili.</span><span class="sxs-lookup"><span data-stu-id="ff041-253">As you hit hello $ key, hello editor will show a dropdown box with a choice of available variables.</span></span> <span data-ttu-id="ff041-254">In questo caso si userà una combinazione di variabile di directory di output di hello e variabile di nome file di input base hello:</span><span class="sxs-lookup"><span data-stu-id="ff041-254">In our case we'll use a combination of hello output directory variable and hello base input file name variable:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}.MP4

![Expression Editor compilato](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-expression-editor.png)

<span data-ttu-id="ff041-256">*Expression Editor compilato*</span><span class="sxs-lookup"><span data-stu-id="ff041-256">*Filled out Expression Editor*</span></span>

> [!NOTE]
> <span data-ttu-id="ff041-257">In ordine toosee visualizzare un file di output del processo di codifica in Azure, è necessario fornire un valore nell'editor di espressioni hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-257">In order toosee see an output file of your encoding job in Azure, you must provide a value in hello expression editor.</span></span>
>
>

<span data-ttu-id="ff041-258">Quando si conferma espressione hello facendo clic su ok, finestra Proprietà hello verrà visualizzate in anteprima toowhat valore hello File proprietà risolve in questo momento.</span><span class="sxs-lookup"><span data-stu-id="ff041-258">When you confirm hello expression by hitting ok, hello property window will preview toowhat value hello File property resolves at this point in time.</span></span>

![L'espressione File risolve la directory di output](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-expression-resolves-output-dir.png)

<span data-ttu-id="ff041-260">*L'espressione File risolve la directory di output*</span><span class="sxs-lookup"><span data-stu-id="ff041-260">*File Expression resolves output dir*</span></span>

### <span data-ttu-id="ff041-261"><a id="MXF_to_MP4_asset_from_output"></a>Creazione di un Asset di servizi multimediali dal file di output di hello</span><span class="sxs-lookup"><span data-stu-id="ff041-261"><a id="MXF_to_MP4_asset_from_output"></a>Creating a Media Services Asset from hello output file</span></span>
<span data-ttu-id="ff041-262">Anche se è stato scritto un file di output MP4, è comunque necessario tooindicate che il file appartiene toohello output asset di servizi multimediali di cui verranno generato in seguito all'esecuzione del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="ff041-262">While we have written an MP4 output file, we still need tooindicate that this file belongs toohello output asset which media services will generate as a result of executing this workflow.</span></span> <span data-ttu-id="ff041-263">fine toothis, nodo di File/Asset di Output di hello nell'area di disegno del flusso di lavoro hello viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="ff041-263">toothis end, hello Output File/Asset node on hello workflow canvas is used.</span></span> <span data-ttu-id="ff041-264">Tutti i file in arrivo in questo nodo renderà parte dell'asset di servizi multimediali di Azure risultante hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-264">All incoming files into this node will make part of hello resulting Azure Media Services asset.</span></span>

<span data-ttu-id="ff041-265">Connettersi hello Output File componente toohello Asset di Output File/componente toofinish hello del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="ff041-265">Connect hello File Output component toohello Output File/Asset component toofinish hello workflow.</span></span>

![Flusso di lavoro completato](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow.png)

<span data-ttu-id="ff041-267">*Flusso di lavoro completato*</span><span class="sxs-lookup"><span data-stu-id="ff041-267">*Finished Workflow*</span></span>

### <span data-ttu-id="ff041-268"><a id="MXF_to_MP4_test"></a>Hello test completato del flusso di lavoro locale</span><span class="sxs-lookup"><span data-stu-id="ff041-268"><a id="MXF_to_MP4_test"></a>Test hello finished workflow locally</span></span>
<span data-ttu-id="ff041-269">tootest hello flusso di lavoro in locale, ha raggiunto il pulsante play hello nella barra degli strumenti hello nella parte superiore di hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-269">tootest hello workflow locally, hit hello play button in hello toolbar at hello top.</span></span> <span data-ttu-id="ff041-270">Quando il flusso di lavoro hello terminato l'esecuzione, esaminare l'output di hello generato nella cartella di output di hello configurato.</span><span class="sxs-lookup"><span data-stu-id="ff041-270">When hello workflow finished executing, inspect hello output generated in hello configured output folder.</span></span> <span data-ttu-id="ff041-271">Si noterà hello completato MP4 i file di output che è stato codificato dal file di origine di input MXF hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-271">You'll see hello finished MP4 output file that was encoded from hello MXF input source file.</span></span>

## <span data-ttu-id="ff041-272"><a id="MXF_to_MP4_with_dyn_packaging"></a>Codifica di un file MXF in MP4 - Creazione dinamica dei pacchetti a velocità in bit multipla abilitata</span><span class="sxs-lookup"><span data-stu-id="ff041-272"><a id="MXF_to_MP4_with_dyn_packaging"></a>Encoding MXF into MP4 - multibitrate dynamic packaging enabled</span></span>
<span data-ttu-id="ff041-273">In questa procedura dettagliata verrà creato un set di file MP4 a velocità in bit multipla con audio con codifica AAC da un solo file di input MXF.</span><span class="sxs-lookup"><span data-stu-id="ff041-273">In this walkthrough we'll create a set of multiple bitrate MP4 files with AAC encoded audio from a single .MXF input file.</span></span>

<span data-ttu-id="ff041-274">Quando un output di asset con più velocità in bit desiderato per l'utilizzo in combinazione con le funzionalità di creazione dinamica dei pacchetti hello offerte da servizi multimediali di Azure, più file MP4 allineati GOP di ogni una velocità in bit diverse e una risoluzione sarà necessario toobe generato.</span><span class="sxs-lookup"><span data-stu-id="ff041-274">When a multi-bitrate asset output is desired for use in combination with hello Dynamic Packaging features offered by Azure Media Services, multiple GOP-aligned MP4 files of each a different bitrate and resolution will need toobe generated.</span></span> <span data-ttu-id="ff041-275">hello in tal caso, toodo [MXF codifica in un file MP4 velocità in bit singola](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) procedura dettagliata ci offre un buon punto di partenza.</span><span class="sxs-lookup"><span data-stu-id="ff041-275">toodo so, hello [Encoding MXF into a single bitrate MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) walkthrough provides us with a good starting point.</span></span>

![Flusso di lavoro iniziale](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow.png)

<span data-ttu-id="ff041-277">*Flusso di lavoro iniziale*</span><span class="sxs-lookup"><span data-stu-id="ff041-277">*Starting Workflow*</span></span>

### <span data-ttu-id="ff041-278"><a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>Aggiunta di uno o più output MP4</span><span class="sxs-lookup"><span data-stu-id="ff041-278"><a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>Adding one or more additional MP4 outputs</span></span>
<span data-ttu-id="ff041-279">Ogni file MP4 nell'asset di Servizi multimediali di Azure risultante supporterà una velocità in bit e una risoluzione diversa.</span><span class="sxs-lookup"><span data-stu-id="ff041-279">Every MP4 file in our resulting Azure Media Services asset will support a different bitrate and resolution.</span></span> <span data-ttu-id="ff041-280">Aggiungere uno o più file MP4 output file toohello del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="ff041-280">Let's add one or more MP4 output files toohello workflow.</span></span>

<span data-ttu-id="ff041-281">toomake che hanno tutti i codificatori video creati con le stesse impostazioni di hello, è più pratico tooduplicate hello codificatore di Video AVC già esistente e configurare un'altra combinazione di risoluzione e velocità in bit (aggiungere uno dei 960x540 25 fotogrammi al secondo 2,5 Mbps).</span><span class="sxs-lookup"><span data-stu-id="ff041-281">toomake sure we have all our video encoders created with hello same settings, it's most convenient tooduplicate hello already existing AVC Video Encoder and configure another combination of resolution and bitrate (let's add one of 960 x 540 at 25 frames per second at 2,5 Mbps).</span></span> <span data-ttu-id="ff041-282">codificatore esistente hello tooduplicate, copia incollarlo nell'area di progettazione hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-282">tooduplicate hello existing encoder, copy paste it on hello designer surface.</span></span>

<span data-ttu-id="ff041-283">Connettersi hello del pin di output di hello Input File multimediali in questo nuovo componente AVC Video non compressi.</span><span class="sxs-lookup"><span data-stu-id="ff041-283">Connect hello Uncompressed Video output pin of hello Media File Input into our new AVC component.</span></span>

![Secondo codificatore AVC connesso](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-avc-encoder-connected.png)

<span data-ttu-id="ff041-285">*Secondo codificatore AVC connesso*</span><span class="sxs-lookup"><span data-stu-id="ff041-285">*Second AVC encoder connected*</span></span>

<span data-ttu-id="ff041-286">Ora adattare configurazione hello per il nostro toooutput di codificatore AVC di nuovo 960x540 2,5 Mbps.</span><span class="sxs-lookup"><span data-stu-id="ff041-286">Now adapt hello configuration for our new AVC encoder toooutput 960x540 at 2,5 Mbps.</span></span> <span data-ttu-id="ff041-287">usando le proprietà "Output width", "Output height" e "Bitrate (kbps)".</span><span class="sxs-lookup"><span data-stu-id="ff041-287">(Use its properties "Output width", "Output height", and "Bitrate (kbps)" for this.)</span></span>

<span data-ttu-id="ff041-288">Dato vogliamo asset risultante di hello toouse con creazione dinamica dei pacchetti servizi multimediali di Azure, hello endpoint di streaming deve toobe in grado di generare da tali file MP4 frammenti MP4/DASH HLS/frammentato esattamente allineato tooeach altri in modo che i client che passa diverse velocità in bit ottengano un singolo smooth continua audio e video.</span><span class="sxs-lookup"><span data-stu-id="ff041-288">Given we want toouse hello resulting asset together with Azure Media Services' dynamic packaging, hello streaming endpoint needs toobe capable of generating from these MP4 files HLS/Fragmented MP4/DASH fragments that are exactly aligned tooeach other in a way that clients that are switching between different bitrates get a single smooth continuous video and audio experience.</span></span> <span data-ttu-id="ff041-289">toomake che si verificano, dobbiamo tooensure nelle proprietà hello di entrambi i codificatori AVC hello dimensioni GOP ("group of pictures") per entrambi i file MP4 è impostato too2 secondi, che possono essere eseguite da:</span><span class="sxs-lookup"><span data-stu-id="ff041-289">toomake that happen, we need tooensure that, in hello properties of both AVC encoders hello GOP ("group of pictures") size for both MP4 files is set too2 seconds, which can be done by:</span></span>

* <span data-ttu-id="ff041-290">impostazione delle dimensioni di GOP tooFixed modalità di ridimensionamento GOP hello e</span><span class="sxs-lookup"><span data-stu-id="ff041-290">setting hello GOP Size Mode tooFixed GOP size and</span></span>
* <span data-ttu-id="ff041-291">secondi di tootwo Hello intervallo dei fotogrammi chiave.</span><span class="sxs-lookup"><span data-stu-id="ff041-291">hello Key Frame Interval tootwo seconds.</span></span>
* <span data-ttu-id="ff041-292">inoltre impostare hello GOP IDR controllo tooClosed GOP tooensure tutti GOP sono permanente per i propri senza dipendenze</span><span class="sxs-lookup"><span data-stu-id="ff041-292">also set hello GOP IDR Control tooClosed GOP tooensure all GOP's are standing on their own without dependencies</span></span>

<span data-ttu-id="ff041-293">toomake nostri toounderstand pratico del flusso di lavoro, rinominare troppo codificatore AVC prima hello "codificatore Video AVC 640x360 kbps 1200" e hello secondo codificatore AVC "codificatore Video AVC 960x540 kbps 2500".</span><span class="sxs-lookup"><span data-stu-id="ff041-293">toomake our workflow convenient toounderstand, rename hello first AVC encoder too"AVC Video Encoder 640x360 1200kbps" and hello second AVC encoder "AVC Video Encoder 960x540 2500 kbps".</span></span>

<span data-ttu-id="ff041-294">Ora aggiungere un secondo componente ISO MPEG-4 Multiplexer e un secondo componente File Output.</span><span class="sxs-lookup"><span data-stu-id="ff041-294">Now add a second ISO MPEG-4 Multiplexer and a second File Output.</span></span> <span data-ttu-id="ff041-295">Connettersi hello multiplexer toohello nuovo AVC codificatore e verificare che il relativo output viene indirizzato in File di Output di hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-295">Connect hello multiplexer toohello new AVC encoder and make sure its output is directed into hello File Output.</span></span> <span data-ttu-id="ff041-296">Connettiti a nuovo toohello output codifica audio AAC hello input di multiplexer.</span><span class="sxs-lookup"><span data-stu-id="ff041-296">Then also connect hello AAC audio encoder output toohello new multiplexer's input.</span></span> <span data-ttu-id="ff041-297">File di Output di Hello, a sua volta, può quindi essere connesso toohello Asset di Output File/nodo tooadd è toohello Asset di servizi multimediali che verrà creato.</span><span class="sxs-lookup"><span data-stu-id="ff041-297">hello File Output in turn can then be connected toohello Output File/Asset node tooadd it toohello Media Services Asset that will be created.</span></span>

![Secondo muxer e File Output connessi](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-muxer-file-output-connected.png)

<span data-ttu-id="ff041-299">*Secondo muxer e File Output connessi*</span><span class="sxs-lookup"><span data-stu-id="ff041-299">*Second Muxer and File Output connected*</span></span>

<span data-ttu-id="ff041-300">Per compatibilità con creazione dinamica dei pacchetti servizi multimediali di Azure, configurare conteggio tooGOP di hello della multiplexer, modalità di blocco o la durata e impostare hello GOP per ogni blocco too1.</span><span class="sxs-lookup"><span data-stu-id="ff041-300">For compatibility with Azure Media Services dynamic packaging, configure hello multiplexer's Chunk Mode tooGOP count or duration and set hello GOPs per chunk too1.</span></span> <span data-ttu-id="ff041-301">(Deve essere predefinito hello).</span><span class="sxs-lookup"><span data-stu-id="ff041-301">(This should be hello default.)</span></span>

![Modalità blocco del muxer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-muxer-chunk-modes.png)

<span data-ttu-id="ff041-303">*Modalità blocco del muxer*</span><span class="sxs-lookup"><span data-stu-id="ff041-303">*Muxer Chunk Modes*</span></span>

<span data-ttu-id="ff041-304">Nota: è consigliabile toorepeat questo processo per qualsiasi altro velocità in bit e la risoluzione combinazioni desiderato toohave aggiunto output asset toohello.</span><span class="sxs-lookup"><span data-stu-id="ff041-304">Note: you may want toorepeat this process for any other bitrate and resolution combinations you want toohave added toohello asset output.</span></span>

### <span data-ttu-id="ff041-305"><a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>Output nomi file di configurazione hello</span><span class="sxs-lookup"><span data-stu-id="ff041-305"><a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>Configuring hello file output names</span></span>
<span data-ttu-id="ff041-306">Sono presenti più di un asset di output toohello singolo file aggiunto.</span><span class="sxs-lookup"><span data-stu-id="ff041-306">We have more than one single file added toohello output asset.</span></span> <span data-ttu-id="ff041-307">In questo modo un necessità toomake che hello nomi di file per ogni hello output file sono diversi tra loro e forse anche applicano una convenzione di denominazione dei file in modo che diventi non crittografato hello nome del file si vuole eseguire.</span><span class="sxs-lookup"><span data-stu-id="ff041-307">This provides a need toomake sure hello filenames for each of hello output files are different from each other and maybe even apply a file-naming convention so it becomes clear from hello file name what you're dealing with.</span></span>

<span data-ttu-id="ff041-308">È possibile controllare la denominazione di file di output tramite espressioni nella finestra di progettazione hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-308">File output naming can be controlled through expressions in hello designer.</span></span> <span data-ttu-id="ff041-309">Aprire il riquadro Proprietà hello per uno dei componenti di File di Output di hello e aprire l'editor di espressioni hello per proprietà File hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-309">Open hello property pane for one of hello File Output components and open hello expression editor for hello File property.</span></span> <span data-ttu-id="ff041-310">Il primo file di output è stato configurato tramite l'espressione seguente hello (vedere l'esercitazione hello per spostarsi da [MXF tooa velocità in bit singola output MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):</span><span class="sxs-lookup"><span data-stu-id="ff041-310">Our first output file was configured through hello following expression (see hello tutorial for going from [MXF tooa single bitrate MP4 output](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}.MP4

<span data-ttu-id="ff041-311">Ciò significa che il nome del file è determinato da due variabili: hello di output directory toowrite hello e nel nome di base del file di origine.</span><span class="sxs-lookup"><span data-stu-id="ff041-311">This means that our filename is determined by two variables: hello output directory toowrite in and hello source file base name.</span></span> <span data-ttu-id="ff041-312">ex Hello viene esposto come una proprietà a livello radice del flusso di lavoro hello e hello quest'ultimo è determinato dal file di hello in arrivo.</span><span class="sxs-lookup"><span data-stu-id="ff041-312">hello former is exposed as a property on hello workflow root and hello latter is determined by hello incoming file.</span></span> <span data-ttu-id="ff041-313">Si noti che directory di output di hello è ciò che si usa per test locale; per questa proprietà verrà sottoposto a override dal motore del flusso di lavoro hello quando il flusso di lavoro hello viene eseguito dal processore di contenuti multimediali basata su cloud hello in servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="ff041-313">Note that hello output directory is what you use for local testing; this property will be overridden by hello workflow engine when hello workflow is executed by hello cloud-based media processor in Azure Media Services.</span></span>
<span data-ttu-id="ff041-314">toogive sia l'output file una denominazione coerente output, hello modifica file prima denominazione espressione per:</span><span class="sxs-lookup"><span data-stu-id="ff041-314">toogive both our output files a consistent output naming, change hello first file naming expression to:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

<span data-ttu-id="ff041-315">e hello in secondo luogo per:</span><span class="sxs-lookup"><span data-stu-id="ff041-315">and hello second to:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_960x540_2.MP4

<span data-ttu-id="ff041-316">Eseguire un test intermedio eseguire toomake che entrambi i file di output MP4 generati correttamente.</span><span class="sxs-lookup"><span data-stu-id="ff041-316">Execute an intermediate test run toomake sure both MP4 output files are properly generated.</span></span>

### <span data-ttu-id="ff041-317"><a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>Aggiunta di una traccia audio separata</span><span class="sxs-lookup"><span data-stu-id="ff041-317"><a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>Adding a separate Audio Track</span></span>
<span data-ttu-id="ff041-318">Come si vedrà in un secondo momento quando si genera un toogo di file con estensione ISM con i file di output MP4, si richiede inoltre un file MP4 solo audio come traccia audio hello per il flusso adattivo.</span><span class="sxs-lookup"><span data-stu-id="ff041-318">As we'll see later when we generate an .ism file toogo with our MP4 output files, we will also require a audio-only MP4 file as hello audio track for our adaptive streaming.</span></span> <span data-ttu-id="ff041-319">toocreate questo file, aggiungere ulteriori muxer toohello flusso di lavoro (Multiplexer ISO-MPEG-4) e connettersi pin di output del codificatore AAC hello con il proprio pin di input per la traccia 1.</span><span class="sxs-lookup"><span data-stu-id="ff041-319">toocreate this file, add an additional muxer toohello workflow (ISO-MPEG-4 Multiplexer) and connect hello AAC encoder's output pin with its input pin for Track 1.</span></span>

![Muxer audio aggiunto](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-added.png)

<span data-ttu-id="ff041-321">*Muxer audio aggiunto*</span><span class="sxs-lookup"><span data-stu-id="ff041-321">*Audio Muxer Added*</span></span>

<span data-ttu-id="ff041-322">Il nome di un terzo File componente toooutput hello in uscita flusso di Output di hello muxer e configurare l'espressione di denominazione file hello come:</span><span class="sxs-lookup"><span data-stu-id="ff041-322">Create a third File Output component toooutput hello outbound stream from hello muxer and configure hello file naming expression as:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_128kbps_audio.MP4

![Creazione di File Output con il muxer audio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-creating-file-output.png)

<span data-ttu-id="ff041-324">*Creazione di File Output con il muxer audio*</span><span class="sxs-lookup"><span data-stu-id="ff041-324">*Audio Muxer creating File Output*</span></span>

### <span data-ttu-id="ff041-325"><a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>Aggiunta di hello. File SMIL ISM</span><span class="sxs-lookup"><span data-stu-id="ff041-325"><a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>Adding hello .ISM SMIL File</span></span>
<span data-ttu-id="ff041-326">Per toowork creazione dinamica dei pacchetti hello in combinazione con entrambi MP4 i file (e hello MP4 solo audio) nell'asset di servizi multimediali, è necessario anche un file manifesto (denominato anche "SMIL" file: Synchronized Multimedia Integration Language).</span><span class="sxs-lookup"><span data-stu-id="ff041-326">For hello dynamic packaging toowork in combination with both MP4 files (and hello audio-only MP4) in our Media Services asset, we also need a manifest file (also called a "SMIL" file: Synchronized Multimedia Integration Language).</span></span> <span data-ttu-id="ff041-327">Questo file indica a servizi multimediali tooAzure quali file MP4 sono disponibili per la creazione dinamica dei pacchetti e quali di questi tooconsider per i flussi audio hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-327">This file indicates tooAzure Media Services what MP4 files are available for dynamic packaging and which of those tooconsider for hello audio streaming.</span></span> <span data-ttu-id="ff041-328">Un file manifesto tipico per un set di MP4 con un solo flusso audio sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="ff041-328">A typical manifest file for a set of MP4's with a single audio stream looks like this:</span></span>

    <?xml version="1.0" encoding="utf-8" standalone="yes"?>
    <smil xmlns="http://www.w3.org/2001/SMIL20/Language">
      <head>
        <meta name="formats" content="mp4" />
      </head>
      <body>
        <switch>
          <video src="H264_1900kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_1300kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_900kbps_AAC_und_ch2_96kbps.mp4" />
          <audio src="AAC_ch2_96kbps.mp4" title="AAC_und_ch2_96kbps" />
        </switch>
      </body>
    </smil>

<span data-ttu-id="ff041-329">file con estensione ISM Hello contiene all'interno di un'istruzione switch, tooeach un riferimento di file video MP4 singoli hello e inoltre tooan MP4 contenente solo audio hello fa riferimento a file audio toothose anche uno (o più).</span><span class="sxs-lookup"><span data-stu-id="ff041-329">hello .ism file contains within a switch statement, a reference tooeach of hello individual MP4 video files and in addition toothose also one (or more) audio file references tooan MP4 that only contains hello audio.</span></span>

<span data-ttu-id="ff041-330">Generazione del file manifesto hello per il set di MP4 possono essere eseguita tramite un componente denominato "AMS manifesto Writer" hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-330">Generating hello manifest file for our set of MP4's can be done through a component called hello "AMS Manifest Writer".</span></span> <span data-ttu-id="ff041-331">toouse, trascinarlo sull'area hello e connettersi pin di output "Scrittura completa" hello da hello tre File di Output componenti toohello Writer AMS manifesto di input.</span><span class="sxs-lookup"><span data-stu-id="ff041-331">toouse it, drag it onto hello surface and connect hello "Write Complete" output pins from hello three File Output components toohello AMS Manifest Writer input.</span></span> <span data-ttu-id="ff041-332">Verificare quindi che output di hello tooconnect di hello AMS manifesto Writer toohello/Asset di File di Output.</span><span class="sxs-lookup"><span data-stu-id="ff041-332">Then make sure tooconnect hello output of hello AMS Manifest Writer toohello Output File/Asset.</span></span>

<span data-ttu-id="ff041-333">Come con il nostro altri componenti output file, configurare il nome output del file con estensione ISM hello con un'espressione:</span><span class="sxs-lookup"><span data-stu-id="ff041-333">As with our other file output components, configure hello .ism file output name with an expression:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_manifest.ism

<span data-ttu-id="ff041-334">Il flusso di lavoro terminato l'aspetto hello riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="ff041-334">Our finished workflow looks like hello below:</span></span>

![Flusso di file MP4 toomultibitrate MXF completata](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-mxf-to-multibitrate-mp4-workflow.png)

<span data-ttu-id="ff041-336">*Flusso di file MP4 toomultibitrate MXF completata*</span><span class="sxs-lookup"><span data-stu-id="ff041-336">*Finished MXF toomultibitrate MP4 workflow*</span></span>

## <span data-ttu-id="ff041-337"><a id="MXF_to__multibitrate_MP4"></a>Codifica di un file MXF in un MP4 a velocità in bit multipla - Progetto avanzato</span><span class="sxs-lookup"><span data-stu-id="ff041-337"><a id="MXF_to__multibitrate_MP4"></a>Encoding MXF into multibitrate MP4 - enhanced blueprint</span></span>
<span data-ttu-id="ff041-338">In hello [procedura dettagliata precedente del flusso di lavoro](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) abbiamo visto come un singolo asset di input MXF può essere convertito in un asset di output con file MP4 a più velocità in bit, un file MP4 solo audio e un file manifesto da utilizzare in combinazione con il supporto di Azure I servizi di creazione dinamica dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="ff041-338">In hello [previous workflow walkthrough](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) we've seen how a single MXF input asset can be converted into an output asset with multi-bitrate MP4 files, an audio-only MP4 file and a manifest file for use in conjunction with Azure Media Services dynamic packaging.</span></span>

<span data-ttu-id="ff041-339">Questa procedura dettagliata verrà illustrano come alcuni degli aspetti hello possibile avanzato e apportate più semplice.</span><span class="sxs-lookup"><span data-stu-id="ff041-339">This walkthrough will show how some of hello aspects can be enhanced and made more convenient.</span></span>

### <span data-ttu-id="ff041-340"><a id="MXF_to_multibitrate_MP4_overview"></a>Flusso di lavoro Panoramica tooenhance</span><span class="sxs-lookup"><span data-stu-id="ff041-340"><a id="MXF_to_multibitrate_MP4_overview"></a>Workflow overview tooenhance</span></span>
![Multibitrate MP4 tooenhance di flusso di lavoro](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-enhance.png)

<span data-ttu-id="ff041-342">*Multibitrate MP4 tooenhance di flusso di lavoro*</span><span class="sxs-lookup"><span data-stu-id="ff041-342">*Multibitrate MP4 workflow tooenhance*</span></span>

### <span data-ttu-id="ff041-343"><a id="MXF_to__multibitrate_MP4_file_naming"></a>Convenzioni di denominazione dei file</span><span class="sxs-lookup"><span data-stu-id="ff041-343"><a id="MXF_to__multibitrate_MP4_file_naming"></a>File Naming Conventions</span></span>
<span data-ttu-id="ff041-344">Nel flusso di lavoro precedente hello è specificata un'espressione semplice come base di hello per la generazione di nomi file di output.</span><span class="sxs-lookup"><span data-stu-id="ff041-344">In hello previous workflow we specified a simple expression as hello basis for generating output file names.</span></span> <span data-ttu-id="ff041-345">Abbiamo anche se alcuni duplicazione: tutti i componenti di file singolo output di hello hello specificata espressione di questo tipo.</span><span class="sxs-lookup"><span data-stu-id="ff041-345">We have some duplication though: all of hello hello individual output file components specified such expression.</span></span>

<span data-ttu-id="ff041-346">Ad esempio, il componente di output file per file video prima hello è configurato con questa espressione:</span><span class="sxs-lookup"><span data-stu-id="ff041-346">For example, our file output component for hello first video file is configured with this expression:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

<span data-ttu-id="ff041-347">Mentre hello secondo output video, può essere un'espressione simile:</span><span class="sxs-lookup"><span data-stu-id="ff041-347">While for hello second output video, we have an expression like:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_960x540_2.MP4

<span data-ttu-id="ff041-348">Non sarebbe più lineare, meno soggetto a errori e più pratico, se fosse possibile rimuovere alcune duplicazioni e rendere il tutto più facilmente configurabile?</span><span class="sxs-lookup"><span data-stu-id="ff041-348">Wouldn't it be cleaner, less error prone and more convenient if we could remove some of this duplication and make things more configurable instead?</span></span> <span data-ttu-id="ff041-349">Fortunatamente, è possibile: le funzioni di espressioni della finestra di progettazione di hello in combinazione con le proprietà personalizzate di hello possibilità toocreate per la radice del flusso di lavoro ci consentirà di ottenere un ulteriore livello di praticità.</span><span class="sxs-lookup"><span data-stu-id="ff041-349">Luckily we can: hello designer's expression capabilities in combination with hello ability toocreate custom properties on our workflow root will give us an added layer of convenience.</span></span>

<span data-ttu-id="ff041-350">Si supponga che si sarà unità configurazione filename da hello di singoli file hello. MP4 velocità in bit.</span><span class="sxs-lookup"><span data-stu-id="ff041-350">Let's assume we'll drive filename configuration from hello bitrates of hello individual MP4 files.</span></span> <span data-ttu-id="ff041-351">Le velocità in bit verrà siamo tooconfigure in un centro posizionare (su hello radice il grafico), da dove saranno usati tooconfigure e unità di generazione del nome file.</span><span class="sxs-lookup"><span data-stu-id="ff041-351">These bitrates we'll aim tooconfigure in one central place (on hello root of our graph), from where they'll be accessed tooconfigure and drive file name generation.</span></span> <span data-ttu-id="ff041-352">toodo, iniziamo pubblicando proprietà velocità in bit hello entrambi radice AVC codificatori toohello il flusso di lavoro, in modo che diventi accessibile da entrambi radice hello anche da codificatori hello AVC.</span><span class="sxs-lookup"><span data-stu-id="ff041-352">toodo this, we start by publishing hello bitrate property from both AVC encoders toohello root of our workflow, so that it becomes accessible from both hello root as well as from hello AVC encoders.</span></span> <span data-ttu-id="ff041-353">Anche se visualizzata in due punti diversi, esiste un solo valore sottostante.</span><span class="sxs-lookup"><span data-stu-id="ff041-353">(Even if displayed in two different spots, there's only one underlying value.)</span></span>

### <span data-ttu-id="ff041-354"><a id="MXF_to__multibitrate_MP4_publishing"></a>La pubblicazione delle proprietà del componente nella radice del flusso di lavoro hello</span><span class="sxs-lookup"><span data-stu-id="ff041-354"><a id="MXF_to__multibitrate_MP4_publishing"></a>Publishing component properties onto hello workflow root</span></span>
<span data-ttu-id="ff041-355">Aprire codificatore AVC prima hello, passare a proprietà velocità in bit (kbps) toohello e dall'elenco a discesa hello scegliere pubblica.</span><span class="sxs-lookup"><span data-stu-id="ff041-355">Open hello first AVC encoder, go toohello Bitrate (kbps) property and from hello dropdown choose Publish.</span></span>

![Proprietà della pubblicazione hello velocità in bit](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-bitrate-property.png)

<span data-ttu-id="ff041-357">*Proprietà della pubblicazione hello velocità in bit*</span><span class="sxs-lookup"><span data-stu-id="ff041-357">*Publishing hello bitrate property*</span></span>

<span data-ttu-id="ff041-358">Configurare hello pubblicare finestra di dialogo toopublish toohello radice il grafico del flusso di lavoro, con un nome pubblicato di "video1bitrate" e un nome leggibile di "Velocità in bit Video 1".</span><span class="sxs-lookup"><span data-stu-id="ff041-358">Configure hello publish dialog toopublish toohello root of our workflow graph, with a published name of "video1bitrate" and a readable display name of "Video 1 Bitrate".</span></span> <span data-ttu-id="ff041-359">Configurare un nome gruppo denominato "Streaming Bitrates" e fare clic su Publish.</span><span class="sxs-lookup"><span data-stu-id="ff041-359">Configure a custom group name called "Streaming Bitrates" and hit Publish.</span></span>

![Proprietà della pubblicazione hello velocità in bit](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-bitrate-property.png)

<span data-ttu-id="ff041-361">*Finestra di dialogo di pubblicazione per la proprietà della velocità in bit*</span><span class="sxs-lookup"><span data-stu-id="ff041-361">*Publishing dialog for bitrate property*</span></span>

<span data-ttu-id="ff041-362">Ripetizione hello stesso per la proprietà di velocità in bit hello di hello secondo codificatore AVC e denominarla "video2bitrate" con un nome visualizzato di "Velocità in bit Video 2", in hello stessa personalizzato di raggruppamento "Streaming velocità in bit".</span><span class="sxs-lookup"><span data-stu-id="ff041-362">Repeat hello same for hello bitrate property of hello second AVC encoder and name it "video2bitrate" with a display name of "Video 2 Bitrate", in hello same custom group "Streaming Bitrates".</span></span>

<span data-ttu-id="ff041-363">È ora possibile controllare le proprietà di radice di hello del flusso di lavoro, vedremo il gruppo personalizzato con hello visualizzati due proprietà pubblicata.</span><span class="sxs-lookup"><span data-stu-id="ff041-363">If we now inspect hello workflow root properties, we'll see our custom group with hello two published properties show up.</span></span> <span data-ttu-id="ff041-364">Entrambi sono che riflette il valore di hello del loro rispettivi AVC codificatore a velocità in bit.</span><span class="sxs-lookup"><span data-stu-id="ff041-364">Both are reflecting hello value of their respective AVC encoder bitrate.</span></span>

![Proprietà della velocità in bit pubblicate nella radice del flusso di lavoro](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-bitrate-props-on-workflow-root.png)

<span data-ttu-id="ff041-366">Ogni volta che si desidera tooaccess queste proprietà dal codice o da un'espressione, è possibile farlo simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="ff041-366">Whenever we want tooaccess these properties from code or from an expression, we can do so like this:</span></span>

* <span data-ttu-id="ff041-367">dal codice inline da un componente sotto la radice hello: node.getPropertyAsString('.. / video1bitrate', null)</span><span class="sxs-lookup"><span data-stu-id="ff041-367">from inline code from a component right below hello root: node.getPropertyAsString('../video1bitrate',null)</span></span>
* <span data-ttu-id="ff041-368">in un'espressione: ${ROOT_video1bitrate}</span><span class="sxs-lookup"><span data-stu-id="ff041-368">within an expression: ${ROOT_video1bitrate}</span></span>

<span data-ttu-id="ff041-369">Ora è necessario completare gruppo "Streaming velocità in bit" hello pubblicando nonché la velocità di traccia audio su di esso.</span><span class="sxs-lookup"><span data-stu-id="ff041-369">Let's complete hello "Streaming Bitrates" group by publishing our audio track bitrate on it as well.</span></span> <span data-ttu-id="ff041-370">All'interno delle proprietà di hello di hello codificatore AAC, cercare l'impostazione di velocità in bit hello e selezionare pubblica tooit avanti di hello elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="ff041-370">Within hello properties of hello AAC Encoder, search for hello Bitrate setting and select Publish from hello dropdown next tooit.</span></span> <span data-ttu-id="ff041-371">Pubblicare toohello radice del grafico hello con nome "audio1bitrate" e il nome "Velocità in bit Audio 1" all'interno di questo gruppo personalizzato "Streaming velocità in bit" visualizzato.</span><span class="sxs-lookup"><span data-stu-id="ff041-371">Publish toohello root of hello graph with name "audio1bitrate" and display name "Audio 1 Bitrate" within our custom group "Streaming Bitrates".</span></span>

![Finestra di dialogo di pubblicazione per la velocità in bit audio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-audio-bitrate.png)

<span data-ttu-id="ff041-373">*Finestra di dialogo di pubblicazione per la velocità in bit audio*</span><span class="sxs-lookup"><span data-stu-id="ff041-373">*Publishing dialog for audio bitrate*</span></span>

![Proprietà video e audio risultanti nella radice](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-resulting-video-and-audio-props-on-root.png)

<span data-ttu-id="ff041-375">*Proprietà video e audio risultanti nella radice*</span><span class="sxs-lookup"><span data-stu-id="ff041-375">*Resulting video and audio props on root*</span></span>

<span data-ttu-id="ff041-376">Si noti che la modifica di una di queste tre valori anche riconfigura e modifiche hello valori su cui sono collegate con in base ai rispettivi componenti hello (e in cui è pubblicato da).</span><span class="sxs-lookup"><span data-stu-id="ff041-376">Note that changing any of those three values also re-configures and changes hello values on hello respective components they are linked with (and where published from).</span></span>

### <span data-ttu-id="ff041-377"><a id="MXF_to__multibitrate_MP4_output_files"></a>Fare in modo che i nomi file di output generati si basino sui valori delle proprietà pubblicati</span><span class="sxs-lookup"><span data-stu-id="ff041-377"><a id="MXF_to__multibitrate_MP4_output_files"></a>Have generated output file names rely on published property values</span></span>
<span data-ttu-id="ff041-378">Anziché a livello di codice ai nomi file generato, è possibile ora modificare l'espressione di nome file in ogni toorely componenti File di Output di hello sulle proprietà di velocità in bit hello che è appena pubblicati a livello di radice grafico hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-378">Instead of hardcoding our generated file names, we can now change our filename expression on each of hello File Output components toorely on hello bitrate properties we just published on hello graph root.</span></span> <span data-ttu-id="ff041-379">A partire da questo primo output del file, trovare la proprietà di File hello e modificare l'espressione hello simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="ff041-379">Starting with our first file output, find hello File property and edit hello expression like this:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video1bitrate}kbps.MP4

<span data-ttu-id="ff041-380">siano accessibili e immessi facendo clic sul segno di dollaro hello tastiera hello nella finestra espressione di hello diversi parametri di Hello in questa espressione.</span><span class="sxs-lookup"><span data-stu-id="ff041-380">hello different parameters in this expression can be accessed and entered by hitting hello dollar sign on hello keyboard while in hello expression window.</span></span> <span data-ttu-id="ff041-381">Uno dei parametri disponibili hello è la proprietà video1bitrate è pubblicate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="ff041-381">One of hello available parameters is our video1bitrate property which we published earlier.</span></span>

![Accesso ai parametri in un'espressione](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-accessing-parameters-within-an-expression.png)

<span data-ttu-id="ff041-383">*Accesso ai parametri in un'espressione*</span><span class="sxs-lookup"><span data-stu-id="ff041-383">*Accessing parameters within an expression*</span></span>

<span data-ttu-id="ff041-384">Hello lo stesso per hello file di output per il secondo video:</span><span class="sxs-lookup"><span data-stu-id="ff041-384">Do hello same for hello file output for our second video:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video2bitrate}kbps.MP4

<span data-ttu-id="ff041-385">e per l'output di hello file solo audio:</span><span class="sxs-lookup"><span data-stu-id="ff041-385">and for hello audio-only file output:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_audio1bitrate}bps_audio.MP4

<span data-ttu-id="ff041-386">Se si modifica ora velocità in bit hello per le hello file video o audio, verrà riconfigurato codificatore rispettivi hello e convenzione di denominazione di file in base a velocità in bit hello verrà rispettata completamente automatico.</span><span class="sxs-lookup"><span data-stu-id="ff041-386">If we now change hello bitrate for any of hello video or audio files, hello respective encoder will be reconfigured and hello bitrate-based file name convention will be honored all automatic.</span></span>

## <span data-ttu-id="ff041-387"><a id="thumbnails_to__multibitrate_MP4"></a>Aggiunta dell'output di anteprime toomultibitrate MP4</span><span class="sxs-lookup"><span data-stu-id="ff041-387"><a id="thumbnails_to__multibitrate_MP4"></a>Adding thumbnails toomultibitrate MP4 output</span></span>
<span data-ttu-id="ff041-388">A partire da un flusso di lavoro che genera l'errore [un output più file MP4 da un input di MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), ora esamineremo nell'aggiunta dell'output toohello anteprime.</span><span class="sxs-lookup"><span data-stu-id="ff041-388">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into adding thumbnails toohello output.</span></span>

### <span data-ttu-id="ff041-389"><a id="thumbnails_to__multibitrate_MP4_overview"></a>Flusso di lavoro Panoramica tooadd anteprime</span><span class="sxs-lookup"><span data-stu-id="ff041-389"><a id="thumbnails_to__multibitrate_MP4_overview"></a>Workflow overview tooadd thumbnails to</span></span>
![Multibitrate MP4 toostart di flusso di lavoro da](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-start-from.png)

<span data-ttu-id="ff041-391">*Multibitrate MP4 toostart di flusso di lavoro da*</span><span class="sxs-lookup"><span data-stu-id="ff041-391">*Multibitrate MP4 workflow toostart from*</span></span>

### <span data-ttu-id="ff041-392"><a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>Aggiunta della codifica JPG</span><span class="sxs-lookup"><span data-stu-id="ff041-392"><a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>Adding JPG Encoding</span></span>
<span data-ttu-id="ff041-393">cuore Hello del nostro generazione anteprima sarà componente codificatore JPG hello, in grado di toooutput JPG (file).</span><span class="sxs-lookup"><span data-stu-id="ff041-393">hello heart of our thumbnail generation will be hello JPG Encoder component, able toooutput JPG files.</span></span>

![JPG Encoder](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-jpg-encoder.png)

<span data-ttu-id="ff041-395">*JPG Encoder*</span><span class="sxs-lookup"><span data-stu-id="ff041-395">*JPG Encoder*</span></span>

<span data-ttu-id="ff041-396">Connessione non è tuttavia direttamente il flusso Video non compressi da hello Input File multimediali in codificatore JPG hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-396">We cannot however directly connect our Uncompressed Video stream from hello Media File Input into hello JPG encoder.</span></span> <span data-ttu-id="ff041-397">In alternativa, è previsto che toobe passato singoli frame.</span><span class="sxs-lookup"><span data-stu-id="ff041-397">Instead, it expects toobe handed individual frames.</span></span> <span data-ttu-id="ff041-398">Questa operazione, è possibile eseguire questa operazione tramite il componente di controllo Frame Video hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-398">This, we can do through hello Video Frame Gate component.</span></span>

![La connessione a un codificatore di frame gate toohello JPG](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-frame-gate-to-jpg-encoder.png)

<span data-ttu-id="ff041-400">*La connessione a un codificatore di frame gate toohello JPG*</span><span class="sxs-lookup"><span data-stu-id="ff041-400">*Connecting a frame gate toohello JPG encoder*</span></span>

<span data-ttu-id="ff041-401">controllo frame Hello dopo ogni moltissimi secondi o frame consente un toopass fotogrammi video.</span><span class="sxs-lookup"><span data-stu-id="ff041-401">hello frame gate once every so many seconds or frames allows a video frame toopass.</span></span> <span data-ttu-id="ff041-402">Hello intervallo e hello differenza di orario con cui in questo caso è possibile configurare nelle proprietà hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-402">hello interval and hello time offset with which this happens is configurable in hello properties.</span></span>

![Proprietà di Video Frame Gate](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-video-frame-gate-properties.png)

<span data-ttu-id="ff041-404">*Proprietà di Video Frame Gate*</span><span class="sxs-lookup"><span data-stu-id="ff041-404">*Video Frame Gate properties*</span></span>

<span data-ttu-id="ff041-405">Si crea un'immagine di anteprima ogni minuto impostando tooTime modalità hello (secondi) e hello too60 intervallo.</span><span class="sxs-lookup"><span data-stu-id="ff041-405">Let's create a thumbnail every minute by setting hello mode tooTime (seconds) and hello Interval too60.</span></span>

### <span data-ttu-id="ff041-406"><a id="thumbnails_to__multibitrate_MP4_color_space"></a>Gestione della conversione dello spazio colore</span><span class="sxs-lookup"><span data-stu-id="ff041-406"><a id="thumbnails_to__multibitrate_MP4_color_space"></a>Dealing with Color Space conversion</span></span>
<span data-ttu-id="ff041-407">Anche se potrebbe sembrare logico sia PIN Video non compressi di controllo frame hello e hello Input del File di supporto può ora essere connesso, si otterrebbe un avviso se è necessario farlo.</span><span class="sxs-lookup"><span data-stu-id="ff041-407">While it would seem logical both Uncompressed Video pins of hello frame gate and hello Media File Input can now be connected, we would get a warning if we would do so.</span></span>

![Errore relativo allo spazio color di input](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-input-color-space-error.png)

<span data-ttu-id="ff041-409">*Errore relativo allo spazio color di input*</span><span class="sxs-lookup"><span data-stu-id="ff041-409">*Input color space error*</span></span>

<span data-ttu-id="ff041-410">In questo modo hello quali colori informazioni vengono rappresentate nel nostro originale non elaborato non compresso flusso video, provenienti dal nostro MXF, è diverso da quali hello prevede che il codificatore JPG.</span><span class="sxs-lookup"><span data-stu-id="ff041-410">This is because hello way in which colour information is represented in our original raw uncompressed video stream, coming from our MXF, is different from what hello JPG Encoder is expecting.</span></span> <span data-ttu-id="ff041-411">Più in particolare, una cosiddetta "spazio colore" di "RGB" o "Grigio" è previsto tooflow in.</span><span class="sxs-lookup"><span data-stu-id="ff041-411">More specifically, a so-called "color space" of "RGB" or "Grayscale" is expected tooflow in.</span></span> <span data-ttu-id="ff041-412">Ciò significa che flusso video in ingresso che hello Video Frame Gate necessario toohave una conversione riguardanti lo spazio colore applicata per primo.</span><span class="sxs-lookup"><span data-stu-id="ff041-412">This means that hello Video Frame Gate's inbound video stream will need toohave a conversion applied regarding its color space first.</span></span>

<span data-ttu-id="ff041-413">Trascinare hello del flusso di lavoro hello convertitore spazio colore - Intel e connetterla tooour gate di frame.</span><span class="sxs-lookup"><span data-stu-id="ff041-413">Drag onto hello workflow hello Color Space Converter - Intel and connect it tooour frame gate.</span></span>

![Connessione di un convertitore dello spazio colore](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-color-space-convertor.png)

<span data-ttu-id="ff041-415">*Connessione di un convertitore dello spazio colore*</span><span class="sxs-lookup"><span data-stu-id="ff041-415">*Connecting a Color Space Convertor*</span></span>

<span data-ttu-id="ff041-416">Nella finestra Proprietà hello, selezionare la voce hello BGR 24 dall'elenco predefinito di hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-416">In hello properties window, pick hello BGR 24 entry from hello Preset list.</span></span>

### <span data-ttu-id="ff041-417"><a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>Anteprime di hello scrittura</span><span class="sxs-lookup"><span data-stu-id="ff041-417"><a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>Writing hello thumbnails</span></span>
<span data-ttu-id="ff041-418">Diverso da nel video di MP4, hello codificatore JPG componente l'output contiene più di un file.</span><span class="sxs-lookup"><span data-stu-id="ff041-418">Different from our MP4 video's, hello JPG Encoder component will output more than one file.</span></span> <span data-ttu-id="ff041-419">In ordine toodeal con questo oggetto, è possibile utilizzare un componente Writer di File JPG Ricerca scena: verrà richiedere anteprime di hello in arrivo JPG e scriverli out, ogni nome di file viene preceduto da un numero diverso.</span><span class="sxs-lookup"><span data-stu-id="ff041-419">In order toodeal with this, a Scene Search JPG File Writer component can be used: it will take hello incoming JPG thumbnails and write them out, each filename being suffixed by a different number.</span></span> <span data-ttu-id="ff041-420">(hello numero in genere hello del secondi/unità nel flusso di hello hello anteprima è stato creato da).</span><span class="sxs-lookup"><span data-stu-id="ff041-420">(hello number typically indicating hello number of seconds/units in hello stream which hello thumbnail was drawn from.)</span></span>

![Introduzione a hello Writer di File JPG Ricerca scena](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer.png)

<span data-ttu-id="ff041-422">*Introduzione a hello Writer di File JPG Ricerca scena*</span><span class="sxs-lookup"><span data-stu-id="ff041-422">*Introducing hello Scene Search JPG File Writer*</span></span>

<span data-ttu-id="ff041-423">Configurare proprietà percorso di cartella di Output di hello con espressione hello: ${ROOT_outputWriteDirectory}</span><span class="sxs-lookup"><span data-stu-id="ff041-423">Configure hello Output Folder Path property with hello expression: ${ROOT_outputWriteDirectory}</span></span>

<span data-ttu-id="ff041-424">e la proprietà con il prefisso del nome file hello:</span><span class="sxs-lookup"><span data-stu-id="ff041-424">and hello Filename Prefix property with:</span></span>

    ${ROOT_sourceFileBaseName}_thumb_

<span data-ttu-id="ff041-425">prefisso Hello determinerà come file di anteprima hello sono denominati.</span><span class="sxs-lookup"><span data-stu-id="ff041-425">hello prefix will determine how hello thumbnail files are being named.</span></span> <span data-ttu-id="ff041-426">Essi verrà aggiunto un suffisso con la posizione di un numero che indica hello della casella di scorrimento nel flusso hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-426">They will be suffixed with a number indicating hello thumb's position in hello stream.</span></span>

![Proprietà di Scene Search JPG File Writer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer-properties.png)

<span data-ttu-id="ff041-428">*Proprietà di Scene Search JPG File Writer*</span><span class="sxs-lookup"><span data-stu-id="ff041-428">*Scene Search JPG File Writer properties*</span></span>

<span data-ttu-id="ff041-429">Connettere hello Writer di File JPG Ricerca scena toohello Asset di Output File/nodo.</span><span class="sxs-lookup"><span data-stu-id="ff041-429">Connect hello Scene Search JPG File Writer toohello Output File/Asset node.</span></span>

### <span data-ttu-id="ff041-430"><a id="thumbnails_to__multibitrate_MP4_errors"></a>Rilevamento di errori in un flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="ff041-430"><a id="thumbnails_to__multibitrate_MP4_errors"></a>Detecting errors in a workflow</span></span>
<span data-ttu-id="ff041-431">Connettere l'input hello di hello colore spazio convertitore toohello non elaborato non compresso output video.</span><span class="sxs-lookup"><span data-stu-id="ff041-431">Connect hello input of hello color space converter toohello raw uncompressed video output.</span></span> <span data-ttu-id="ff041-432">A questo punto, eseguire un test locale per flusso di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-432">Now perform a local test run for hello workflow.</span></span> <span data-ttu-id="ff041-433">È presente un flusso di lavoro hello buone probabilità verrà improvvisamente arrestare l'esecuzione e indicare con un contorno rosso sul componente hello che si è verificato un errore:</span><span class="sxs-lookup"><span data-stu-id="ff041-433">There's a good chance hello workflow will suddenly stop executing and indicate with a red outline on hello component that encountered an error:</span></span>

![Errore di Color Space Converter](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error.png)

<span data-ttu-id="ff041-435">*Errore di Color Space Converter*</span><span class="sxs-lookup"><span data-stu-id="ff041-435">*Color Space Converter error*</span></span>

<span data-ttu-id="ff041-436">Fare clic sull'icona "E" hello leggermente rosso hello angolo superiore destro di hello convertitore spazio colore componente toosee qual è il motivo di hello hello codifica non è riuscito.</span><span class="sxs-lookup"><span data-stu-id="ff041-436">Click hello little red "E" icon in hello top right corner of hello Color Space Converter component toosee what's hello reason hello encoding attempt failed.</span></span>

![Finestra di dialogo dell'errore di Color Space Converter](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error-dialog.png)

<span data-ttu-id="ff041-438">*Finestra di dialogo dell'errore di Color Space Converter*</span><span class="sxs-lookup"><span data-stu-id="ff041-438">*Color Space Converter error dialog*</span></span>

<span data-ttu-id="ff041-439">Si scopre, come si può notare che hello in arrivo spazio colore standard per convertitore di spazio colori hello è rec601 toobe per la conversione di tooRGB YUV richiesta.</span><span class="sxs-lookup"><span data-stu-id="ff041-439">It turns out, as you can see, that hello incoming color space standard for hello color space converter has toobe rec601 for our requested conversion of YUV tooRGB.</span></span> <span data-ttu-id="ff041-440">Sembra che il flusso non indichi rec601.</span><span class="sxs-lookup"><span data-stu-id="ff041-440">Apparently our stream doesn't indicate it's rec601.</span></span> <span data-ttu-id="ff041-441">Rec 601 è uno standard per la codifica dei segnali video analogici interlacciati nel formato video digitale.</span><span class="sxs-lookup"><span data-stu-id="ff041-441">(Rec 601 is a standard for encoding interlaced analog video signals in digital video form.</span></span> <span data-ttu-id="ff041-442">Specifica un'area attiva che copre 720 campioni di luminanza e 360 campioni di crominanza per linea.</span><span class="sxs-lookup"><span data-stu-id="ff041-442">It specifies an active region covering 720 luminance samples and 360 chrominance samples per line.</span></span> <span data-ttu-id="ff041-443">sistema di codifica dei colori di Hello sono noto come allineamento 4:2:2.)</span><span class="sxs-lookup"><span data-stu-id="ff041-443">hello color encoding system is known as YCbCr 4:2:2.)</span></span>

<span data-ttu-id="ff041-444">toofix, si verrà indicano i metadati di hello del nostro flusso ci stiamo occupa rec601 contenuto.</span><span class="sxs-lookup"><span data-stu-id="ff041-444">toofix this, we'll indicate on hello metadata of our stream that we're dealing with rec601 content.</span></span> <span data-ttu-id="ff041-445">toodo utilizzeremo un componente di aggiornamento di tipo di dati Video, che è stato verrà inserito tra il nostro raw origine e hello colore spazio componente per la conversione.</span><span class="sxs-lookup"><span data-stu-id="ff041-445">toodo so we'll use a Video Data Type Updater component, which we'll put in between our raw source and hello color space conversion component.</span></span> <span data-ttu-id="ff041-446">L'aggiornamento di tipo di dati consente l'aggiornamento manuale di hello di determinati dati video le proprietà del tipo.</span><span class="sxs-lookup"><span data-stu-id="ff041-446">This data type updater allows for hello manual update of certain video data type properties.</span></span> <span data-ttu-id="ff041-447">Configurarlo tooindicate uno spazio colore Standard di "Rec 601".</span><span class="sxs-lookup"><span data-stu-id="ff041-447">Configure it tooindicate a Color Space Standard of "Rec 601".</span></span> <span data-ttu-id="ff041-448">In questo modo flusso hello tootag Updater tipo di dati Video di hello con spazio di colore "Rec 601" hello, se si è verificato alcun spazio colore ancora definito.</span><span class="sxs-lookup"><span data-stu-id="ff041-448">This will cause hello Video Data Type Updater tootag hello stream with hello "Rec 601" color space if there was no color space defined yet.</span></span> <span data-ttu-id="ff041-449">(Non sostituisce eventuali metadati esistenti, a meno che non è stata selezionata la casella di controllo Override hello.)</span><span class="sxs-lookup"><span data-stu-id="ff041-449">(It will not override any existing metadata, unless hello Override checkbox was checked.)</span></span>

![Aggiornamento Standard di spazio colore in hello Updater tipo di dati](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-update-color-space-standard-on-data-type.png)

<span data-ttu-id="ff041-451">*Aggiornamento Standard di spazio colore in hello Updater tipo di dati*</span><span class="sxs-lookup"><span data-stu-id="ff041-451">*Updating Color Space Standard on hello Data Type Updater*</span></span>

### <span data-ttu-id="ff041-452"><a id="thumbnails_to__multibitrate_MP4_finish"></a>Flusso di lavoro completato</span><span class="sxs-lookup"><span data-stu-id="ff041-452"><a id="thumbnails_to__multibitrate_MP4_finish"></a>Finished Workflow</span></span>
<span data-ttu-id="ff041-453">Ora che il nostro il flusso di lavoro viene terminato, eseguire un altro toosee esecuzione dei test vengano superati.</span><span class="sxs-lookup"><span data-stu-id="ff041-453">Now that our our workflow is finished, do another test run toosee it pass.</span></span>

![Flusso di lavoro completato per l'output di più MP4 con anteprime](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-for-multi-mp4-thumbnails.png)

<span data-ttu-id="ff041-455">*Flusso di lavoro completato per l'output di più MP4 con anteprime*</span><span class="sxs-lookup"><span data-stu-id="ff041-455">*Finished workflow for multi-mp4 output with thumbnails*</span></span>

## <span data-ttu-id="ff041-456"><a id="time_based_trim"></a>Taglio basato sull'ora dell'output MP4 a velocità in bit multipla</span><span class="sxs-lookup"><span data-stu-id="ff041-456"><a id="time_based_trim"></a>Time-based trimming of multibitrate MP4 output</span></span>
<span data-ttu-id="ff041-457">A partire da un flusso di lavoro che genera l'errore [un output più file MP4 da un input di MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), ora esamineremo in trimming video di origine hello in base a un timestamp.</span><span class="sxs-lookup"><span data-stu-id="ff041-457">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into trimming hello source video based on time-stamps.</span></span>

### <span data-ttu-id="ff041-458"><a id="time_based_trim_start"></a>Flusso di lavoro Panoramica toostart aggiunta di taglio per</span><span class="sxs-lookup"><span data-stu-id="ff041-458"><a id="time_based_trim_start"></a>Workflow overview toostart adding trimming to</span></span>
![Avvio rimozione tooadd del flusso di lavoro a](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow-to-add-trimming.png)

<span data-ttu-id="ff041-460">*Avvio rimozione tooadd del flusso di lavoro a*</span><span class="sxs-lookup"><span data-stu-id="ff041-460">*Starting workflow tooadd trimming to*</span></span>

### <span data-ttu-id="ff041-461"><a id="time_based_trim_use_stream_trimmer"></a>Utilizzo di hello compensatore di flusso</span><span class="sxs-lookup"><span data-stu-id="ff041-461"><a id="time_based_trim_use_stream_trimmer"></a>Using hello Stream Trimmer</span></span>
<span data-ttu-id="ff041-462">componente flusso compensatore Hello consente tootrim hello inizio e alla fine di un flusso di input basata sulle informazioni di intervallo (secondi, minuti,...). compensatore Hello non supporta la rimozione di basati su frame.</span><span class="sxs-lookup"><span data-stu-id="ff041-462">hello Stream Trimmer component allows tootrim hello beginning and ending of an input stream base on timing information (seconds, minutes, ...). hello trimmer does not support frame-based trimming.</span></span>

![Stream Trimmer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-stream-trimmer.png)

<span data-ttu-id="ff041-464">*Stream Trimmer*</span><span class="sxs-lookup"><span data-stu-id="ff041-464">*Stream Trimmer*</span></span>

<span data-ttu-id="ff041-465">Anziché direttamente il collegamento codificatori hello AVC e degli altoparlanti posizione chi assegna toohello Input del File di supporto, si verrà inserita tra tali compensatore flusso hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-465">Instead of linking hello AVC encoders and speaker position assigner toohello Media File Input directly, we'll put in between those hello stream trimmer.</span></span> <span data-ttu-id="ff041-466">(Uno per il segnale video hello e uno per hello interleaved segnali audio).</span><span class="sxs-lookup"><span data-stu-id="ff041-466">(One for hello video signal and one for hello interleaved audio signal.)</span></span>

![Inserire Stream Trimmer in mezzo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-put-stream-trimmer-in-between.png)

<span data-ttu-id="ff041-468">*Inserire Stream Trimmer in mezzo*</span><span class="sxs-lookup"><span data-stu-id="ff041-468">*Put Stream Trimmer in between*</span></span>

<span data-ttu-id="ff041-469">Configurazione compensatore hello in modo che verranno elaborati solo video e audio compreso tra 15 e 60 secondi in video hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-469">Let's configure hello trimmer so that we will only process video and audio between 15 seconds and 60 seconds in hello video.</span></span>

<span data-ttu-id="ff041-470">Passare la proprietà toohello di hello compensatore flusso Video e configurare l'ora di inizio (15s) sia le proprietà dell'ora di fine (60 s).</span><span class="sxs-lookup"><span data-stu-id="ff041-470">Go toohello properties of hello Video Stream Trimmer and configure both Start Time (15s) and End Time (60s) properties.</span></span> <span data-ttu-id="ff041-471">toomake che sia il compensatore audio e video siano sempre configurata toohello stesso iniziare e terminare i valori, verranno pubblicate tali radice toohello del flusso di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-471">toomake sure both our audio and video trimmer are always configured toohello same start and end values, we will publish those toohello root of hello workflow.</span></span>

![Pubblicare la proprietà Start Time da Stream Trimmer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-start-time-from-stream-trimmer.png)

<span data-ttu-id="ff041-473">*Pubblicare la proprietà Start Time da Stream Trimmer*</span><span class="sxs-lookup"><span data-stu-id="ff041-473">*Publish start time property from Stream Trimmer*</span></span>

![Finestra di dialogo Publish Property per Start Time](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-start-time.png)

<span data-ttu-id="ff041-475">*Finestra di dialogo Publish Property per Start Time*</span><span class="sxs-lookup"><span data-stu-id="ff041-475">*Publish property dialog for start time*</span></span>

![Finestra di dialogo Publish Property per End Time](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-end-time.png)

<span data-ttu-id="ff041-477">*Finestra di dialogo Publish Property per End Time*</span><span class="sxs-lookup"><span data-stu-id="ff041-477">*Publish property dialog for end time*</span></span>

<span data-ttu-id="ff041-478">Se è ora possibile esaminare radice hello il flusso di lavoro, entrambe le proprietà sarà perfettamente configurabile e visualizzati da qui.</span><span class="sxs-lookup"><span data-stu-id="ff041-478">If we now inspect hello root of our workflow, both properties will be neatly displayed and configurable from there.</span></span>

![Proprietà pubblicate disponibili nella radice](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-properties-available-on-root.png)

<span data-ttu-id="ff041-480">*Proprietà pubblicate disponibili nella radice*</span><span class="sxs-lookup"><span data-stu-id="ff041-480">*Published properties available on root*</span></span>

<span data-ttu-id="ff041-481">Ora aprire le proprietà di taglio hello da compensatore audio hello e configurare i tempi di inizio e di fine con un'espressione che fa riferimento toohello pubblicato le proprietà nella directory principale di hello di questo flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="ff041-481">Now open hello trimming properties from hello audio trimmer and configure both start and end times with an expression that refers toohello published properties on hello root of our workflow.</span></span>

<span data-ttu-id="ff041-482">Ora di inizio rimozione audio per hello:</span><span class="sxs-lookup"><span data-stu-id="ff041-482">For hello audio trimming start time:</span></span>

    ${ROOT_TrimmingStartTime}

<span data-ttu-id="ff041-483">e per l'ora di fine:</span><span class="sxs-lookup"><span data-stu-id="ff041-483">and for its end time:</span></span>

    ${ROOT_TrimmingEndTime}

### <span data-ttu-id="ff041-484"><a id="time_based_trim_finish"></a>Flusso di lavoro completato</span><span class="sxs-lookup"><span data-stu-id="ff041-484"><a id="time_based_trim_finish"></a>Finished Workflow</span></span>
![Flusso di lavoro completato](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-time-base-trimming.png)

<span data-ttu-id="ff041-486">*Flusso di lavoro completato*</span><span class="sxs-lookup"><span data-stu-id="ff041-486">*Finished Workflow*</span></span>

## <span data-ttu-id="ff041-487"><a id="scripting"></a>Introduzione a hello componente script</span><span class="sxs-lookup"><span data-stu-id="ff041-487"><a id="scripting"></a>Introducing hello Scripted Component</span></span>
<span data-ttu-id="ff041-488">Componenti di script possono essere eseguiti gli script arbitrari durante le fasi di esecuzione hello del nostro del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="ff041-488">Scripted Components can execute arbitrary scripts during hello execution phases of our workflow.</span></span> <span data-ttu-id="ff041-489">Sono disponibili quattro diversi script che può essere eseguito, ognuna con caratteristiche specifiche e luogo nel ciclo di vita di hello del flusso di lavoro:</span><span class="sxs-lookup"><span data-stu-id="ff041-489">There are four different scripts that can be executed, each with specific characteristics and their own place in hello workflow life-cycle:</span></span>

* <span data-ttu-id="ff041-490">**commandScript**</span><span class="sxs-lookup"><span data-stu-id="ff041-490">**commandScript**</span></span>
* <span data-ttu-id="ff041-491">**realizeScript**</span><span class="sxs-lookup"><span data-stu-id="ff041-491">**realizeScript**</span></span>
* <span data-ttu-id="ff041-492">**processInputScript**</span><span class="sxs-lookup"><span data-stu-id="ff041-492">**processInputScript**</span></span>
* <span data-ttu-id="ff041-493">**lifeCycleScript**</span><span class="sxs-lookup"><span data-stu-id="ff041-493">**lifeCycleScript**</span></span>

<span data-ttu-id="ff041-494">Hello inserire la documentazione di hello componente script in modo più dettagliato per ogni hello precedente.</span><span class="sxs-lookup"><span data-stu-id="ff041-494">hello documentation of hello Scripted Component goes in more detail for each of hello above.</span></span> <span data-ttu-id="ff041-495">In [hello seguente sezione](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), hello **realizeScript** componente script è tooconstruct utilizzato un file xml di cliplist volo hello all'avvio di flusso di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-495">In [hello following section](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), hello **realizeScript** scripting component is used tooconstruct a cliplist xml on hello fly when hello workflow starts.</span></span> <span data-ttu-id="ff041-496">Questo script viene chiamato durante l'installazione di componenti hello, che si verifica una sola volta nel relativo ciclo di vita.</span><span class="sxs-lookup"><span data-stu-id="ff041-496">This script is called during hello component setup, which happens only once in it's lifecycle.</span></span>

### <span data-ttu-id="ff041-497"><a id="scripting_hello_world"></a>Scripting in un flusso di lavoro: hello world</span><span class="sxs-lookup"><span data-stu-id="ff041-497"><a id="scripting_hello_world"></a>Scripting within a workflow: hello world</span></span>
<span data-ttu-id="ff041-498">Trascinare un componente script nell'area di progettazione hello e rinominarlo (ad esempio, "SetClipListXML").</span><span class="sxs-lookup"><span data-stu-id="ff041-498">Drag a Scripted Component onto hello designer surface and rename it (for example, "SetClipListXML").</span></span>

![Aggiunta di un componente con script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

<span data-ttu-id="ff041-500">*Aggiunta di un componente con script*</span><span class="sxs-lookup"><span data-stu-id="ff041-500">*Adding a Scripted Component*</span></span>

<span data-ttu-id="ff041-501">Quando si esaminano le proprietà di hello di hello componente script, hello verranno visualizzati quattro tipi di script diverso, ogni script diverso tooa configurabile.</span><span class="sxs-lookup"><span data-stu-id="ff041-501">When you inspect hello properties of hello Scripted Component, hello four different script types will be shown, each configurable tooa different script.</span></span>

![Proprietà del componente con script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

<span data-ttu-id="ff041-503">*Proprietà del componente con script*</span><span class="sxs-lookup"><span data-stu-id="ff041-503">*Scripted Component properties*</span></span>

<span data-ttu-id="ff041-504">Deselezionare hello processInputScript e aprire l'editor di hello per realizeScript hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-504">Clear hello processInputScript and open hello editor for hello realizeScript.</span></span> <span data-ttu-id="ff041-505">È ora completato la configurazione e pronto toostart scripting.</span><span class="sxs-lookup"><span data-stu-id="ff041-505">Now we're set up and ready toostart scripting.</span></span>

<span data-ttu-id="ff041-506">Gli script vengono scritti in Groovy, un linguaggio di scripting compilato in modo dinamico per la piattaforma Java hello che mantiene la compatibilità con Java.</span><span class="sxs-lookup"><span data-stu-id="ff041-506">Scripts are written in Groovy, a dynamically compiled scripting language for hello Java platform that retains compatibility with Java.</span></span> <span data-ttu-id="ff041-507">La maggior parte del codice Java è effettivamente codice Groovy valido.</span><span class="sxs-lookup"><span data-stu-id="ff041-507">Actually, most Java code is valid Groovy code.</span></span>

<span data-ttu-id="ff041-508">Di seguito scrivere uno script di semplice hello world groovy nel contesto di hello del nostro realizeScript.</span><span class="sxs-lookup"><span data-stu-id="ff041-508">Let's write a simple hello world groovy script in hello context of our realizeScript.</span></span> <span data-ttu-id="ff041-509">Immettere il seguente hello nell'editor di hello:</span><span class="sxs-lookup"><span data-stu-id="ff041-509">Enter hello following in hello editor:</span></span>

    node.log("hello world");

<span data-ttu-id="ff041-510">Ora effettuare un'esecuzione di test locale.</span><span class="sxs-lookup"><span data-stu-id="ff041-510">Now execute a local test run.</span></span> <span data-ttu-id="ff041-511">Dopo l'esecuzione, controllare (tramite scheda sistema hello nel componente script hello) hello proprietà log.</span><span class="sxs-lookup"><span data-stu-id="ff041-511">After this run, inspect (through hello System tab on hello Scripted Component) hello Logs property.</span></span>

![Output di log hello world](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output.png)

<span data-ttu-id="ff041-513">*Output di log hello world*</span><span class="sxs-lookup"><span data-stu-id="ff041-513">*Hello world log output*</span></span>

<span data-ttu-id="ff041-514">oggetto del nodo Hello viene chiamato il metodo di log hello, fa riferimento tooour corrente "nodo" o un componente di hello ci stiamo l'esecuzione degli script.</span><span class="sxs-lookup"><span data-stu-id="ff041-514">hello node object we call hello log method on, refers tooour current "node" or hello component we're scripting within.</span></span> <span data-ttu-id="ff041-515">Di conseguenza, ogni componente ha hello possibilità toooutput la registrazione dati, disponibili tramite la scheda di sistema hello. In questo caso, è output hello stringa letterale "hello world".</span><span class="sxs-lookup"><span data-stu-id="ff041-515">Every component as such has hello ability toooutput logging data, available through hello system tab. In this case, we output hello string literal "hello world".</span></span> <span data-ttu-id="ff041-516">Qui toounderstand importante è che ciò può rivelarsi toobe uno strumento estremamente utile di debug, visualizzando le informazioni dettagliate su quali script hello è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="ff041-516">Important toounderstand here is that this can prove toobe an invaluable debugging tool, providing you with insight on what hello script is actually doing.</span></span>

<span data-ttu-id="ff041-517">Da in ambiente di scripting, è necessario anche accesso tooproperties su altri componenti.</span><span class="sxs-lookup"><span data-stu-id="ff041-517">From within our scripting environment, we also have access tooproperties on other components.</span></span> <span data-ttu-id="ff041-518">Provare a eseguire quanto segue:</span><span class="sxs-lookup"><span data-stu-id="ff041-518">Try this:</span></span>

    //inspect current node:
    def nodepath = node.getNodePath();
    node.log("this node path: " + nodepath);

    //walking up tooother nodes:
    def parentnode = node.getParentNode();
    def parentnodepath = parentnode.getNodePath();
    node.log("parent node path: " + parentnodepath);

    //read properties from a node:
    def sourceFileExt = parentnode.getPropertyAsString( "sourceFileExtension", null );
    def sourceFileName = parentnode.getPropertyAsString("sourceFileBaseName", null);
    node.log("source file name with extension " + sourceFileExt + " is: " + sourceFileName);

<span data-ttu-id="ff041-519">La finestra del log mostrerà hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="ff041-519">Our log window will show us hello following:</span></span>

![Output dei log per l'accesso ai percorsi dei nodi](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output2.png)

<span data-ttu-id="ff041-521">*Output dei log per l'accesso ai percorsi dei nodi*</span><span class="sxs-lookup"><span data-stu-id="ff041-521">*Log output for accessing node paths*</span></span>

## <span data-ttu-id="ff041-522"><a id="frame_based_trim"></a>Taglio basato sul fotogramma dell'output MP4 a velocità in bit multipla</span><span class="sxs-lookup"><span data-stu-id="ff041-522"><a id="frame_based_trim"></a>Frame-based trimming of multibitrate MP4 output</span></span>
<span data-ttu-id="ff041-523">A partire da un flusso di lavoro che genera l'errore [un output più file MP4 da un input di MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), ora esamineremo in trimming video di origine hello in base al conteggio dei frame.</span><span class="sxs-lookup"><span data-stu-id="ff041-523">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into trimming hello source video based on frame counts.</span></span>

### <span data-ttu-id="ff041-524"><a id="frame_based_trim_start"></a>Cianografia toostart Panoramica aggiunta la rimozione di</span><span class="sxs-lookup"><span data-stu-id="ff041-524"><a id="frame_based_trim_start"></a>Blueprint overview toostart adding trimming to</span></span>
![Aggiunta di taglio per toostart di flusso di lavoro](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-workflow-start-adding-trimming-to.png)

<span data-ttu-id="ff041-526">*Aggiunta di taglio per toostart di flusso di lavoro*</span><span class="sxs-lookup"><span data-stu-id="ff041-526">*Workflow toostart adding trimming to*</span></span>

### <span data-ttu-id="ff041-527"><a id="frame_based_trim_clip_list"></a>Utilizzo di hello Clip elenco XML</span><span class="sxs-lookup"><span data-stu-id="ff041-527"><a id="frame_based_trim_clip_list"></a>Using hello Clip List XML</span></span>
<span data-ttu-id="ff041-528">In tutte le esercitazioni del flusso di lavoro precedente, abbiamo utilizzato componente di Input di File di supporto hello come l'origine video di input.</span><span class="sxs-lookup"><span data-stu-id="ff041-528">In all previous workflow tutorials, we used hello Media File Input component as our video input source.</span></span> <span data-ttu-id="ff041-529">Per questo scenario specifico, tuttavia, verrà usato il componente di origine dell'elenco Clip hello invece.</span><span class="sxs-lookup"><span data-stu-id="ff041-529">For this specific scenario though, we'll be using hello Clip List Source component instead.</span></span> <span data-ttu-id="ff041-530">Si noti che questo non deve essere hello preferito modo di lavorare; utilizzare solo hello Clip elenco origine quando esiste un toodo motivo effettivo così (come in hello sotto i casi in cui rendiamo utilizzo delle funzionalità di taglio hello clip elenco).</span><span class="sxs-lookup"><span data-stu-id="ff041-530">Note that this should not be hello preferred way of working; only use hello Clip List Source when there's a real reason toodo so (like in hello below case, where we're making use of hello clip list trimming capabilities).</span></span>

<span data-ttu-id="ff041-531">tooswitch dal nostro toohello di Input di File multimediali Clip elenco origine, trascinare il componente di origine dell'elenco Clip hello nell'area di progettazione hello e connettersi hello Clip elenco XML pin toohello Clip elenco il nodo XML di progettazione del flusso di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-531">tooswitch from our Media File Input toohello Clip List Source, drag hello Clip List Source component onto hello design surface and connect hello Clip List XML pin toohello Clip List XML node of hello workflow designer.</span></span> <span data-ttu-id="ff041-532">Questo deve popolare hello Clip elenco origine con il PIN di output, in base tooour video di input.</span><span class="sxs-lookup"><span data-stu-id="ff041-532">This should populate hello Clip List Source with output pins, according tooour input video.</span></span> <span data-ttu-id="ff041-533">Connettersi a questo punto i pin non compresso Audio e Video non compresso hello da hello hello Clip elenco origine toohello rispettivi AVC codificatori e Interleaver flusso Audio.</span><span class="sxs-lookup"><span data-stu-id="ff041-533">Now connect hello Uncompressed Video and Uncompressed Audio pins from hello hello Clip List Source toohello respective AVC Encoders and Audio Stream Interleaver.</span></span> <span data-ttu-id="ff041-534">Rimuovere hello Input del File di supporto.</span><span class="sxs-lookup"><span data-stu-id="ff041-534">Now remove hello Media File Input.</span></span>

![Sostituito hello Input File multimediali con hello Clip elenco origine](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-replaced-media-file-with-clip-source.png)

<span data-ttu-id="ff041-536">*Sostituito hello Input File multimediali con hello Clip elenco origine*</span><span class="sxs-lookup"><span data-stu-id="ff041-536">*Replaced hello Media File Input with hello Clip List Source*</span></span>

<span data-ttu-id="ff041-537">componente di origine dell'elenco Clip Hello accetta come input un "Clip elenco XML".</span><span class="sxs-lookup"><span data-stu-id="ff041-537">hello Clip List Source component takes as its input a "Clip List XML".</span></span> <span data-ttu-id="ff041-538">Selezionando tootest di file di origine hello con localmente, questo elenco di ritaglio codice xml viene popolato automaticamente per l'utente.</span><span class="sxs-lookup"><span data-stu-id="ff041-538">When selecting hello source file tootest with locally, this clip list xml is auto-populated for you.</span></span>

![Proprietà Clip List XML popolata automaticamente](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-auto-populated-clip-list-xml-property.png)

<span data-ttu-id="ff041-540">*Proprietà Clip List XML popolata automaticamente*</span><span class="sxs-lookup"><span data-stu-id="ff041-540">*Auto-populated Clip List XML property*</span></span>

<span data-ttu-id="ff041-541">Esaminando un bit più vicino toohello xml, ecco come appare come:</span><span class="sxs-lookup"><span data-stu-id="ff041-541">Looking a bit closer toohello xml, this is how it looks like:</span></span>

![Finestra di dialogo di modifica dell'elenco di clip](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-edit-clip-list-dialog.png)

<span data-ttu-id="ff041-543">*Finestra di dialogo di modifica dell'elenco di clip*</span><span class="sxs-lookup"><span data-stu-id="ff041-543">*Edit clip list dialog*</span></span>

<span data-ttu-id="ff041-544">Questo tuttavia non riflette le funzionalità di hello di hello clip elenco xml.</span><span class="sxs-lookup"><span data-stu-id="ff041-544">This however does not reflect hello capabilities of hello clip list xml.</span></span> <span data-ttu-id="ff041-545">Abbiamo è tooadd un elemento "Trim" hello audio e video origine audio, simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="ff041-545">One option we have is tooadd a "Trim" element under both hello video and audio source, like this:</span></span>

![Aggiunta di un elenco di ritaglio di elemento trim toohello](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-trim-element-to-clip-list.png)

<span data-ttu-id="ff041-547">*Aggiunta di un elenco di ritaglio di elemento trim toohello*</span><span class="sxs-lookup"><span data-stu-id="ff041-547">*Adding a trim element toohello clip list*</span></span>

<span data-ttu-id="ff041-548">Se si modifica hello clip elenco xml simile al seguente di sopra e si esegue un'esecuzione dei test locali, si noterà video hello correttamente stato tagliati compreso tra 10 e 20 secondi in video hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-548">If you modify hello clip list xml like this above and perform a local test run, you'll see hello video correctly been trimmed between 10 and 20 seconds in hello video.</span></span>

<span data-ttu-id="ff041-549">Toowhat contrarie si verifica quando si esegue un'esecuzione locale, tuttavia, questa stessa xml cliplist non avrebbero hello lo stesso effetto di quando applicato in un flusso di lavoro in esecuzione in servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="ff041-549">Contrary toowhat happens when you do a local run though, this very same cliplist xml would not have hello same effect when applied in a workflow that runs in Azure Media Services.</span></span> <span data-ttu-id="ff041-550">Quando viene avviato codificatore Premium di Azure, hello cliplist xml viene generato ogni volta che, in base alle hello file di input hello codifica processo è stato specificato.</span><span class="sxs-lookup"><span data-stu-id="ff041-550">When Azure Premium Encoder starts, hello cliplist xml is generated every time again, based on hello input file hello encoding job was given.</span></span> <span data-ttu-id="ff041-551">Ciò significa che tutte le modifiche facciamo su xml hello verrebbero Purtroppo eseguito l'override.</span><span class="sxs-lookup"><span data-stu-id="ff041-551">This means that any changes we do on hello xml would unfortunately be overridden.</span></span>

<span data-ttu-id="ff041-552">toocounter hello cliplist xml venga cancellato quando viene avviato un processo di codifica, è possibile generare di nuovo il volo hello subito dopo l'inizio di hello il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="ff041-552">toocounter hello cliplist xml being wiped when an encoding job is started, we can re-generate it on hello fly just after hello start of our workflow.</span></span> <span data-ttu-id="ff041-553">Tali azioni personalizzate possono essere eseguite con un cosiddetto "componente con script".</span><span class="sxs-lookup"><span data-stu-id="ff041-553">Such custom actions can be taken through what is called a "Scripted Component".</span></span> <span data-ttu-id="ff041-554">Per ulteriori informazioni, vedere [Introducing hello componente script](media-services-media-encoder-premium-workflow-tutorials.md#scripting).</span><span class="sxs-lookup"><span data-stu-id="ff041-554">For more information, see [Introducing hello Scripted Component](media-services-media-encoder-premium-workflow-tutorials.md#scripting).</span></span>

<span data-ttu-id="ff041-555">Trascinare un componente script nell'area di progettazione hello e rinominarlo troppo "SetClipListXML".</span><span class="sxs-lookup"><span data-stu-id="ff041-555">Drag a Scripted Component onto hello designer surface and rename it too"SetClipListXML".</span></span>

![Aggiunta di un componente con script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

<span data-ttu-id="ff041-557">*Aggiunta di un componente con script*</span><span class="sxs-lookup"><span data-stu-id="ff041-557">*Adding a Scripted Component*</span></span>

<span data-ttu-id="ff041-558">Quando si esaminano le proprietà di hello di hello componente script, hello verranno visualizzati quattro tipi di script diverso, ogni script diverso tooa configurabile.</span><span class="sxs-lookup"><span data-stu-id="ff041-558">When you inspect hello properties of hello Scripted Component, hello four different script types will be shown, each configurable tooa different script.</span></span>

![Proprietà del componente con script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

<span data-ttu-id="ff041-560">*Proprietà del componente con script*</span><span class="sxs-lookup"><span data-stu-id="ff041-560">*Scripted Component properties*</span></span>

### <span data-ttu-id="ff041-561"><a id="frame_based_trim_modify_clip_list"></a>Modifica elenco di clip hello da un componente script</span><span class="sxs-lookup"><span data-stu-id="ff041-561"><a id="frame_based_trim_modify_clip_list"></a>Modifying hello clip list from a Scripted Component</span></span>
<span data-ttu-id="ff041-562">È possibile scrivere nuovamente hello cliplist xml che viene generato durante l'avvio del flusso di lavoro, è necessario contenuto e la proprietà xml toohave accesso toohello cliplist.</span><span class="sxs-lookup"><span data-stu-id="ff041-562">Before we can re-write hello cliplist xml that is generated during workflow startup, we'll need toohave access toohello cliplist xml property and contents.</span></span> <span data-ttu-id="ff041-563">A questo scopo, è possibile usare il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="ff041-563">We can do so like this:</span></span>

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: " + clipListXML);

![Elenco di clip in entrata da registrare](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-incoming-clip-list-logged.png)

<span data-ttu-id="ff041-565">*Elenco di clip in entrata da registrare*</span><span class="sxs-lookup"><span data-stu-id="ff041-565">*Incoming clip list being logged*</span></span>

<span data-ttu-id="ff041-566">È necessario un modo toodetermine da che punto fino a quel punto si desidera tootrim hello video.</span><span class="sxs-lookup"><span data-stu-id="ff041-566">First we need a way toodetermine from which point till which point we want tootrim hello video.</span></span> <span data-ttu-id="ff041-567">pubblicare questo utente meno tecniche toohello pratico di flusso di lavoro hello toomake radice toohello due proprietà del grafico hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-567">toomake this convenient toohello less-technical user of hello workflow, publish two properties toohello root of hello graph.</span></span> <span data-ttu-id="ff041-568">toodo, fare clic con il pulsante destro progettazione hello e selezionare "Aggiungi proprietà":</span><span class="sxs-lookup"><span data-stu-id="ff041-568">toodo this, right click hello designer surface and select "Add Property":</span></span>

* <span data-ttu-id="ff041-569">Prima proprietà: "ClippingTimeStart" di tipo: "TIMECODE"</span><span class="sxs-lookup"><span data-stu-id="ff041-569">First property: "ClippingTimeStart" of type: "TIMECODE"</span></span>
* <span data-ttu-id="ff041-570">Seconda proprietà: "ClippingTimeEnd" di tipo: "TIMECODE"</span><span class="sxs-lookup"><span data-stu-id="ff041-570">Second property: "ClippingTimeEnd" of type: "TIMECODE"</span></span>

![Finestra di dialogo Add Property per l'ora di inizio del ritaglio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-start-time.png)

<span data-ttu-id="ff041-572">*Finestra di dialogo Add Property per l'ora di inizio del ritaglio*</span><span class="sxs-lookup"><span data-stu-id="ff041-572">*Add Property dialog for clipping start time*</span></span>

![Proprietà degli orari di ritaglio pubblicate nella radice del flusso di lavoro](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-time-props.png)

<span data-ttu-id="ff041-574">*Proprietà degli orari di ritaglio pubblicate nella radice del flusso di lavoro*</span><span class="sxs-lookup"><span data-stu-id="ff041-574">*Published clipping time props on workflow root*</span></span>

<span data-ttu-id="ff041-575">Configurare entrambi valore di proprietà tooa appropriato:</span><span class="sxs-lookup"><span data-stu-id="ff041-575">Configure both properties tooa suitable value:</span></span>

![Configurare hello ritaglio proprietà start ed end](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configure-clip-start-end-prop.png)

<span data-ttu-id="ff041-577">*Configurare hello ritaglio proprietà start ed end*</span><span class="sxs-lookup"><span data-stu-id="ff041-577">*Configure hello clipping start and end properties*</span></span>

<span data-ttu-id="ff041-578">Ora dallo script è possibile accedere a entrambe le proprietà, in questo modo:</span><span class="sxs-lookup"><span data-stu-id="ff041-578">Now, from within our script, we can access both properties, like this:</span></span>

    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    node.log("clipping start: " + clipstart);
    node.log("clipping end: " + clipend);

![Finestra dei log che mostra l'inizio e la fine del ritaglio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-show-start-end-clip.png)

<span data-ttu-id="ff041-580">*Finestra dei log che mostra l'inizio e la fine del ritaglio*</span><span class="sxs-lookup"><span data-stu-id="ff041-580">*Log window showing start and end of clipping*</span></span>

<span data-ttu-id="ff041-581">Di seguito è possibile analizzare le stringhe di timecode hello in un form toouse più semplice, usando un'espressione regolare semplice:</span><span class="sxs-lookup"><span data-stu-id="ff041-581">Let's parse hello timecode strings into a more convenient toouse form, using a simple regular expression:</span></span>

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);
    node.log("framerate end is: " + endframerate);

![Finestra dei log con l'output del time code analizzato](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-output-parsed-timecode.png)

<span data-ttu-id="ff041-583">*Finestra dei log con l'output del time code analizzato*</span><span class="sxs-lookup"><span data-stu-id="ff041-583">*Log window with output of parsed timecode*</span></span>

<span data-ttu-id="ff041-584">Con queste informazioni in questione, è possibile ora modificare hello cliplist xml tooreflect hello e l'ora di fine per hello desiderato ritaglio ad alta precisione del filmato hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-584">With this information at hand, we can now modify hello cliplist xml tooreflect hello start and end times for hello desired frame-accurate clipping of hello movie.</span></span>

![Elementi di taglio tooadd codice di script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-trim-elements.png)

<span data-ttu-id="ff041-586">*Elementi di taglio tooadd codice di script*</span><span class="sxs-lookup"><span data-stu-id="ff041-586">*Script code tooadd trim elements*</span></span>

<span data-ttu-id="ff041-587">Queste modifiche sono state apportate con normali operazioni di manipolazione delle stringhe.</span><span class="sxs-lookup"><span data-stu-id="ff041-587">This was done through normal string manipulation operations.</span></span> <span data-ttu-id="ff041-588">codice xml risultante ClipArt modificata elenco Hello vengono riscritti toohello clipListXML proprietà a livello radice del flusso di lavoro hello tramite il metodo "setProperty" hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-588">hello resulting modified clip list xml is written back toohello clipListXML property on hello workflow root through hello "setProperty" method.</span></span> <span data-ttu-id="ff041-589">finestra log Hello dopo l'esecuzione di un altro test sarebbe mostrano hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="ff041-589">hello log window after another test run would show us hello following:</span></span>

![Registrazione elenco clip risultante hello](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-result-clip-list.png)

<span data-ttu-id="ff041-591">*Registrazione elenco clip risultante hello*</span><span class="sxs-lookup"><span data-stu-id="ff041-591">*Logging hello resulting clip list*</span></span>

<span data-ttu-id="ff041-592">Eseguire un toosee di esecuzione dei test come sono stati ritagliati flussi audio e video hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-592">Do a test-run toosee how hello video and audio streams have been clipped.</span></span> <span data-ttu-id="ff041-593">Come verranno eseguite più di una esecuzione dei test con valori diversi per i punti di taglio hello, si noterà che quelli non accederà conto tuttavia!</span><span class="sxs-lookup"><span data-stu-id="ff041-593">As you'll do more than one test-run with different values for hello trimming points, you'll notice that those will not be taken into account however!</span></span> <span data-ttu-id="ff041-594">motivo Hello è tale finestra di progettazione di hello, a differenza di hello runtime di Azure, non non override hello cliplist xml ogni esecuzione.</span><span class="sxs-lookup"><span data-stu-id="ff041-594">hello reason for this is that hello designer, unlike hello Azure runtime, does NOT override hello cliplist xml every run.</span></span> <span data-ttu-id="ff041-595">Ciò significa che solo hello attutire impostate hello i punti, causerà hello xml tootransform, tutti hello altre volte, la clausola guard (se (clipListXML.indexOf ("<trim>") = = -1)), non potrà del flusso di lavoro hello aggiungerne un altro trim elemento quando è già presente.</span><span class="sxs-lookup"><span data-stu-id="ff041-595">This means that only hello very first time you have set hello in and out points, will cause hello xml tootransform, all hello other times, our guard clause (if(clipListXML.indexOf("<trim>") == -1)) will prevent hello workflow from adding another trim element when there's already one present.</span></span>

<span data-ttu-id="ff041-596">toomake il flusso di lavoro pratico tootest in locale, è migliore aggiungere il codice di parti di riferimento che controlla se un elemento trim è già presente.</span><span class="sxs-lookup"><span data-stu-id="ff041-596">toomake our workflow convenient tootest locally, we best add some house-keeping code that inspects if a trim element was already present.</span></span> <span data-ttu-id="ff041-597">In questo caso, è possibile rimuoverlo prima di continuare modificando hello xml con i nuovi valori hello.</span><span class="sxs-lookup"><span data-stu-id="ff041-597">If so, we can remove it before continuing by modifying hello xml with hello new values.</span></span> <span data-ttu-id="ff041-598">Anziché utilizzare stringhe normale, è probabilmente sicura toodo tramite l'oggetto xml reale durante l'analisi del modello.</span><span class="sxs-lookup"><span data-stu-id="ff041-598">Rather than using plain string manipulations, it's probably safer toodo this through real xml object model parsing.</span></span>

<span data-ttu-id="ff041-599">Tuttavia, è possibile aggiungere tale codice, è necessario tooadd che un numero di istruzioni import in hello iniziare prima dello script:</span><span class="sxs-lookup"><span data-stu-id="ff041-599">Before we can add such code though, we'll need tooadd a number of import statements at hello start of our script first:</span></span>

    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

<span data-ttu-id="ff041-600">Successivamente, è possibile aggiungere hello necessaria la pulizia di codice:</span><span class="sxs-lookup"><span data-stu-id="ff041-600">After this, we can add hello required cleaning code:</span></span>

    //for local testing: delete any pre-existing trim elements from hello clip list xml by parsing hello xml into a DOM:
    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements,dom,XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
     //delete hello trim nodes:
    elementsToDelete.each{
        e -> e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

<span data-ttu-id="ff041-601">Questo codice viene inserito sopra il punto di hello in corrispondenza del quale è aggiungere hello elementi trim toohello cliplist xml.</span><span class="sxs-lookup"><span data-stu-id="ff041-601">This code goes just above hello point at which we add hello trim elements toohello cliplist xml.</span></span>

<span data-ttu-id="ff041-602">A questo punto, è possibile eseguire e modificare il flusso di lavoro come determinante dal momento che durante le modifiche apportate hello applicato mai ora.</span><span class="sxs-lookup"><span data-stu-id="ff041-602">At this point, we can run and modify our workflow as much as we want while having hello changes applied ever time.</span></span>    

### <span data-ttu-id="ff041-603"><a id="frame_based_trim_clippingenabled_prop"></a>Aggiunta di una pratica proprietà ClippingEnabled</span><span class="sxs-lookup"><span data-stu-id="ff041-603"><a id="frame_based_trim_clippingenabled_prop"></a>Adding a ClippingEnabled convenience property</span></span>
<span data-ttu-id="ff041-604">Poiché non è sempre consigliabile toohappen taglio, completare disattivare il flusso di lavoro tramite l'aggiunta di un semplice flag booleano che indica se si vuole tooenable trimming / ritaglio.</span><span class="sxs-lookup"><span data-stu-id="ff041-604">As you might not always want trimming toohappen, let's finish off our workflow by adding a convenient boolean flag that indicates whether or not we want tooenable trimming / clipping.</span></span>

<span data-ttu-id="ff041-605">Proprio come prima, pubblicare una nuova proprietà toohello directory principale di questo flusso di lavoro denominato "ClippingEnabled" di tipo "BOOLEAN".</span><span class="sxs-lookup"><span data-stu-id="ff041-605">Just as before, publish a new property toohello root of our workflow called "ClippingEnabled" of type "BOOLEAN".</span></span>

![Pubblicare una proprietà per l'abilitazione del ritaglio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-enable-clip.png)

<span data-ttu-id="ff041-607">*Pubblicare una proprietà per l'abilitazione del ritaglio*</span><span class="sxs-lookup"><span data-stu-id="ff041-607">*Published a property for enabling clipping*</span></span>

<span data-ttu-id="ff041-608">Con hello seguito clausola guard semplice, è possibile controllare se è necessaria la rimozione e decidere se l'elenco di ritaglio deve pertanto toobe modificato o meno.</span><span class="sxs-lookup"><span data-stu-id="ff041-608">With hello below simple guard clause, we can check if trimming is required and decide if our clip list as such needs toobe modified or not.</span></span>

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }


### <span data-ttu-id="ff041-609"><a id="code"></a>Codice completo</span><span class="sxs-lookup"><span data-stu-id="ff041-609"><a id="code"></a>Complete code</span></span>
    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: \n" + clipListXML);
    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);

    node.log("framerate end is: " + endframerate);

    //for local testing: delete any pre-existing trim elements
    //from hello clip list xml by parsing hello xml into a DOM:

    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements, dom, XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
    //delete hello trim nodes:
    elementsToDelete.each{ e ->
        e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }

    //add trim elements toocliplist xml
    if ( clipListXML.indexOf("<trim>") == -1 )
    {
        //trim video
        clipListXML = clipListXML.replace("<videoSource>","<videoSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\"" + endframerate +"\"> " + endtimecode +
            " </outPoint>\n </trim> \n");
        //trim audio
        clipListXML = clipListXML.replace("<audioSource>","<audioSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\""+ endframerate +"\">" +
            endtimecode + "</outPoint>\n </trim>\n");
        node.log( "clip list going out: \n" +clipListXML );
        node.setProperty("../clipListXml",clipListXML);
    }


## <a name="also-see"></a><span data-ttu-id="ff041-610">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="ff041-610">Also see</span></span>
[<span data-ttu-id="ff041-611">Introduzione alla codifica Premium in Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="ff041-611">Introducing Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)

[<span data-ttu-id="ff041-612">Come tooUse codifica Premium in servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="ff041-612">How tooUse Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)

[<span data-ttu-id="ff041-613">Codifica di contenuti su richiesta con Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="ff041-613">Encoding On-Demand Content with Azure Media Service</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)

[<span data-ttu-id="ff041-614">Codec e formati del flusso di lavoro Premium del codificatore multimediale</span><span class="sxs-lookup"><span data-stu-id="ff041-614">Media Encoder Premium Workflow Formats and Codecs</span></span>](media-services-premium-workflow-encoder-formats.md)

[<span data-ttu-id="ff041-615">File del flusso di lavoro di esempio</span><span class="sxs-lookup"><span data-stu-id="ff041-615">Sample workflow files</span></span>](http://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows)

[<span data-ttu-id="ff041-616">Strumento di esplorazione di Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="ff041-616">Azure Media Services Explorer tool</span></span>](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a><span data-ttu-id="ff041-617">Percorsi di apprendimento di Media Services</span><span class="sxs-lookup"><span data-stu-id="ff041-617">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ff041-618">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="ff041-618">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
