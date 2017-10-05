---
title: Esercitazioni avanzate del flusso di lavoro Premium del codificatore multimediale
description: "Questo documento contiene procedure dettagliate che illustrano come eseguire attività avanzate con il flusso di lavoro Premium del codificatore multimediale e come creare flussi di lavoro complessi con Progettazione flussi di lavoro."
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
ms.openlocfilehash: 565497bd5a35e3c4d69d29512307cf3ca2364bdd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="advanced-media-encoder-premium-workflow-tutorials"></a><span data-ttu-id="19615-103">Esercitazioni avanzate del flusso di lavoro Premium del codificatore multimediale</span><span class="sxs-lookup"><span data-stu-id="19615-103">Advanced Media Encoder Premium Workflow tutorials</span></span>
## <a name="overview"></a><span data-ttu-id="19615-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="19615-104">Overview</span></span>
<span data-ttu-id="19615-105">Questo documento contiene procedure dettagliate che illustrano come personalizzare i flussi di lavoro con **Progettazione flussi di lavoro**.</span><span class="sxs-lookup"><span data-stu-id="19615-105">This document contains walkthroughs that show how to customize workflows with  **Workflow Designer**.</span></span> <span data-ttu-id="19615-106">I file dei flussi di lavoro effettivi sono disponibili [qui](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples).</span><span class="sxs-lookup"><span data-stu-id="19615-106">You can find the actual workflow files [here](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples).</span></span>  

## <a name="toc"></a><span data-ttu-id="19615-107">Sommario</span><span class="sxs-lookup"><span data-stu-id="19615-107">TOC</span></span>
<span data-ttu-id="19615-108">Vengono trattati gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="19615-108">The following topics are covered:</span></span>

* [<span data-ttu-id="19615-109">Codifica di un file MXF in un MP4 a velocità in bit singola</span><span class="sxs-lookup"><span data-stu-id="19615-109">Encoding MXF into a single bitrate MP4</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)
  * [<span data-ttu-id="19615-110">Avvio di un nuovo flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="19615-110">Starting a new workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_start_new)
  * [<span data-ttu-id="19615-111">Uso di Media File Input</span><span class="sxs-lookup"><span data-stu-id="19615-111">Using the Media File Input</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_file_input)
  * [<span data-ttu-id="19615-112">Analisi di flussi multimediali</span><span class="sxs-lookup"><span data-stu-id="19615-112">Inspecting media streams</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_streams)
  * [<span data-ttu-id="19615-113">Aggiunta di un codificatore video per la generazione di file MP4</span><span class="sxs-lookup"><span data-stu-id="19615-113">Adding a video encoder for .MP4 file generation</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_file_generation)
  * [<span data-ttu-id="19615-114">Codifica del flusso audio</span><span class="sxs-lookup"><span data-stu-id="19615-114">Encoding the audio stream</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio)
  * [<span data-ttu-id="19615-115">Multiplexing di flussi audio e video in un contenitore MP4</span><span class="sxs-lookup"><span data-stu-id="19615-115">Multiplexing Audio and Video streams into an MP4 container</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio_and_fideo)
  * [<span data-ttu-id="19615-116">Scrittura del file MP4</span><span class="sxs-lookup"><span data-stu-id="19615-116">Writing the MP4 file</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_writing_mp4)
  * [<span data-ttu-id="19615-117">Creazione di un asset di Servizi multimediali dal file di output</span><span class="sxs-lookup"><span data-stu-id="19615-117">Creating a Media Services Asset from the output file</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_asset_from_output)
  * [<span data-ttu-id="19615-118">Testare il flusso di lavoro completato in locale</span><span class="sxs-lookup"><span data-stu-id="19615-118">Test the finished workflow locally</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_test)
* [<span data-ttu-id="19615-119">Codifica di un file MXF in MP4 a velocità in bit multipla - Creazione dinamica dei pacchetti abilitata</span><span class="sxs-lookup"><span data-stu-id="19615-119">Encoding MXF into multibitrate MP4s - dynamic packaging enabled</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)
  * [<span data-ttu-id="19615-120">Aggiunta di uno o più output MP4</span><span class="sxs-lookup"><span data-stu-id="19615-120">Adding one or more additional MP4 outputs</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_more_outputs)
  * [<span data-ttu-id="19615-121">Configurazione dei nomi di output dei file</span><span class="sxs-lookup"><span data-stu-id="19615-121">Configuring the file output names</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_conf_output_names)
  * [<span data-ttu-id="19615-122">Aggiunta di una traccia audio separata</span><span class="sxs-lookup"><span data-stu-id="19615-122">Adding a separate Audio Track</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_audio_tracks)
  * [<span data-ttu-id="19615-123">Aggiunta del file SMIL ISM</span><span class="sxs-lookup"><span data-stu-id="19615-123">Adding the .ISM SMIL File</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_ism_file)
* [<span data-ttu-id="19615-124">Codifica di un file MXF in un MP4 a velocità in bit multipla - Progetto avanzato</span><span class="sxs-lookup"><span data-stu-id="19615-124">Encoding MXF into multibitrate MP4 - enhanced blueprint</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4)
  * [<span data-ttu-id="19615-125">Panoramica del flusso di lavoro da migliorare</span><span class="sxs-lookup"><span data-stu-id="19615-125">Workflow overview to enhance</span></span>](#workflow-overview-to-enhance)
  * [<span data-ttu-id="19615-126">Convenzioni di denominazione dei file</span><span class="sxs-lookup"><span data-stu-id="19615-126">File Naming Conventions</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_file_naming)
  * [<span data-ttu-id="19615-127">Pubblicazione delle proprietà dei componenti nella radice del flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="19615-127">Publishing component properties onto the workflow root</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_publishing)
  * [<span data-ttu-id="19615-128">Fare in modo che i nomi file di output generati si basino sui valori delle proprietà pubblicati</span><span class="sxs-lookup"><span data-stu-id="19615-128">Have generated output file names rely on published property values</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_output_files)
* [<span data-ttu-id="19615-129">Aggiunta di anteprime all'output MP4 a velocità in bit multipla</span><span class="sxs-lookup"><span data-stu-id="19615-129">Adding thumbnails to multibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4)
  * [<span data-ttu-id="19615-130">Panoramica del flusso di lavoro a cui aggiungere le anteprime</span><span class="sxs-lookup"><span data-stu-id="19615-130">Workflow overview to add thumbnails to</span></span>](#workflow-overview-to-add-thumbnails-to)
  * [<span data-ttu-id="19615-131">Aggiunta della codifica JPG</span><span class="sxs-lookup"><span data-stu-id="19615-131">Adding JPG Encoding</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4__with_jpg)
  * [<span data-ttu-id="19615-132">Gestione della conversione dello spazio colore</span><span class="sxs-lookup"><span data-stu-id="19615-132">Dealing with Color Space conversion</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_color_space)
  * [<span data-ttu-id="19615-133">Scrittura delle anteprime</span><span class="sxs-lookup"><span data-stu-id="19615-133">Writing the thumbnails</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_writing_thumbnails)
  * [<span data-ttu-id="19615-134">Rilevamento di errori in un flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="19615-134">Detecting errors in a workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_errors)
  * [<span data-ttu-id="19615-135">Flusso di lavoro completato</span><span class="sxs-lookup"><span data-stu-id="19615-135">Finished Workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_finish)
* [<span data-ttu-id="19615-136">Taglio basato sull'ora dell'output MP4 a velocità in bit multipla</span><span class="sxs-lookup"><span data-stu-id="19615-136">Time-based trimming of multibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim)
  * [<span data-ttu-id="19615-137">Panoramica del flusso di lavoro a cui iniziare ad aggiungere il taglio</span><span class="sxs-lookup"><span data-stu-id="19615-137">Workflow overview to start adding trimming to</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_start)
  * [<span data-ttu-id="19615-138">Uso di Stream Trimmer</span><span class="sxs-lookup"><span data-stu-id="19615-138">Using the Stream Trimmer</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_use_stream_trimmer)
  * [<span data-ttu-id="19615-139">Flusso di lavoro completato</span><span class="sxs-lookup"><span data-stu-id="19615-139">Finished Workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_finish)
* [<span data-ttu-id="19615-140">Introduzione al componente con script</span><span class="sxs-lookup"><span data-stu-id="19615-140">Introducing the Scripted Component</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#scripting)
  * [<span data-ttu-id="19615-141">Scripting in un flusso di lavoro: hello world</span><span class="sxs-lookup"><span data-stu-id="19615-141">Scripting within a workflow: hello world</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#scripting_hello_world)
* [<span data-ttu-id="19615-142">Taglio basato sul fotogramma dell'output MP4 a velocità in bit multipla</span><span class="sxs-lookup"><span data-stu-id="19615-142">Frame-based trimming of multibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim)
  * [<span data-ttu-id="19615-143">Panoramica del progetto a cui iniziare ad aggiungere il taglio</span><span class="sxs-lookup"><span data-stu-id="19615-143">Blueprint overview to start adding trimming to</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_start)
  * [<span data-ttu-id="19615-144">Uso di Clip List XML</span><span class="sxs-lookup"><span data-stu-id="19615-144">Using the Clip List XML</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clip_list)
  * [<span data-ttu-id="19615-145">Modifica dell'elenco di clip da un componente con script</span><span class="sxs-lookup"><span data-stu-id="19615-145">Modifying the clip list from a Scripted Component</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_modify_clip_list)
  * [<span data-ttu-id="19615-146">Aggiunta di una pratica proprietà ClippingEnabled</span><span class="sxs-lookup"><span data-stu-id="19615-146">Adding a ClippingEnabled convenience property</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clippingenabled_prop)

## <span data-ttu-id="19615-147"><a id="MXF_to_MP4"></a>Codifica di un file MXF in un MP4 a velocità in bit singola</span><span class="sxs-lookup"><span data-stu-id="19615-147"><a id="MXF_to_MP4"></a>Encoding MXF into a single bitrate MP4</span></span>
<span data-ttu-id="19615-148">In questa procedura dettagliata verrà creato un file MP4 a velocità in bit singola con audio con codifica AAC-HE da un file di input MXF.</span><span class="sxs-lookup"><span data-stu-id="19615-148">In this walkthrough we'll create a single bitrate .MP4 file with AAC-HE encoded audio from an .MXF input file.</span></span>

### <span data-ttu-id="19615-149"><a id="MXF_to_MP4_start_new"></a>Avvio di un nuovo flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="19615-149"><a id="MXF_to_MP4_start_new"></a>Starting a new workflow</span></span>
<span data-ttu-id="19615-150">Aprire Progettazione flussi di lavoro e selezionare "File" - "New Workspace" - "Transcode Blueprint"</span><span class="sxs-lookup"><span data-stu-id="19615-150">Open Workflow Designer and select "File"-"New Workspace"-"Transcode Blueprint"</span></span>

<span data-ttu-id="19615-151">Il nuovo flusso di lavoro mostrerà 3 elementi:</span><span class="sxs-lookup"><span data-stu-id="19615-151">The new workflow will show 3 elements:</span></span>

* <span data-ttu-id="19615-152">Primary Source File</span><span class="sxs-lookup"><span data-stu-id="19615-152">Primary Source File</span></span>
* <span data-ttu-id="19615-153">Clip List XML</span><span class="sxs-lookup"><span data-stu-id="19615-153">Clip List XML</span></span>
* <span data-ttu-id="19615-154">Output File/Asset</span><span class="sxs-lookup"><span data-stu-id="19615-154">Output File/Asset</span></span>  

![Nuovo flusso di lavoro della codifica](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-transcode-blueprint.png)

<span data-ttu-id="19615-156">*Nuovo flusso di lavoro della codifica*</span><span class="sxs-lookup"><span data-stu-id="19615-156">*New Encoding Workflow*</span></span>

### <span data-ttu-id="19615-157"><a id="MXF_to_MP4_with_file_input"></a>Uso di Media File Input</span><span class="sxs-lookup"><span data-stu-id="19615-157"><a id="MXF_to_MP4_with_file_input"></a>Using the Media File Input</span></span>
<span data-ttu-id="19615-158">Per accettare il file multimediale di input, si inizia aggiungendo un componente Media File Input.</span><span class="sxs-lookup"><span data-stu-id="19615-158">In order to accept our input media file, one starts with adding a Media File Input component.</span></span> <span data-ttu-id="19615-159">Per aggiungere un componente al flusso di lavoro, cercarlo nella casella di ricerca del repository e trascinare la voce desiderata sul riquadro della finestra di progettazione.</span><span class="sxs-lookup"><span data-stu-id="19615-159">To add a component to the workflow, look for it in the Repository search box and drag the desired entry onto the designer pane.</span></span> <span data-ttu-id="19615-160">Eseguire questa operazione per Media File Input e connettere il componente Primary Source File al pin di input Filename da Media File Input.</span><span class="sxs-lookup"><span data-stu-id="19615-160">Do this for the Media File Input and connect the Primary Source File component to the Filename input pin from the Media File Input.</span></span>

![Media File Input connesso](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-input.png)

<span data-ttu-id="19615-162">*Media File Input connesso*</span><span class="sxs-lookup"><span data-stu-id="19615-162">*Connected Media File Input*</span></span>

<span data-ttu-id="19615-163">Prima di eseguire altre operazioni, sarà necessario indicare a Progettazione flussi di lavoro quale file di esempio usare per progettare il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="19615-163">Before we can do much else, we'll first need to indicate to the workflow designer what sample file we'd like to use to design our workflow with.</span></span> <span data-ttu-id="19615-164">A questo scopo, fare clic sullo sfondo del riquadro della finestra di progettazione e cercare la proprietà Primary Source File nel riquadro delle proprietà sulla destra.</span><span class="sxs-lookup"><span data-stu-id="19615-164">To do so, click the designer pane background and look for the Primary Source File property on the right-hand property pane.</span></span> <span data-ttu-id="19615-165">Fare clic sull'icona della cartella e selezionare il file desiderato con cui testare il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="19615-165">Click the folder icon and select the desired file to test the workflow with.</span></span> <span data-ttu-id="19615-166">Al termine dell'operazione, il componente Media File Input esaminerà il file e popolerà i pin di output per poter effettuare la reflection del file esaminato.</span><span class="sxs-lookup"><span data-stu-id="19615-166">As soon as this is done, the Media File Input component will inspect the file and populate its output pins to reflect the file it inspected.</span></span>

![Media File Input popolato](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-populated-media-file-input.png)

<span data-ttu-id="19615-168">*Media File Input popolato*</span><span class="sxs-lookup"><span data-stu-id="19615-168">*Populated Media File Input*</span></span>

<span data-ttu-id="19615-169">Questa operazione specifica l'input da usare, ma non indica ancora dove salvare l'output codificato.</span><span class="sxs-lookup"><span data-stu-id="19615-169">While this specifies with what input we'd like to work with, it doesn't tell yet where the encoded output should go to.</span></span> <span data-ttu-id="19615-170">Come è stato configurato Primary Source File, configurare ora la proprietà Output Folder Variable, appena sotto.</span><span class="sxs-lookup"><span data-stu-id="19615-170">Similar to how the Primary Source File was configured, now configure the Output Folder Variable property, just below it.</span></span>

![Proprietà di input e output configurate](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configured-io-properties.png)

<span data-ttu-id="19615-172">*Proprietà di input e output configurate*</span><span class="sxs-lookup"><span data-stu-id="19615-172">*Configured Input and Output properties*</span></span>

### <span data-ttu-id="19615-173"><a id="MXF_to_MP4_streams"></a>Analisi di flussi multimediali</span><span class="sxs-lookup"><span data-stu-id="19615-173"><a id="MXF_to_MP4_streams"></a>Inspecting media streams</span></span>
<span data-ttu-id="19615-174">Spesso si vuole sapere come appare il flusso che scorre nel flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="19615-174">Often it's desired to know how the stream looks like that flows through the workflow.</span></span> <span data-ttu-id="19615-175">Per esaminare un flusso in qualsiasi punto del flusso di lavoro, è sufficiente fare clic su un pin di output o di input in uno dei componenti.</span><span class="sxs-lookup"><span data-stu-id="19615-175">To inspect a stream at any point in the workflow, just click an output or input pin on any of the components.</span></span> <span data-ttu-id="19615-176">In questo caso, provare a fare clic sul pin di output Uncompressed Video da Media File Input.</span><span class="sxs-lookup"><span data-stu-id="19615-176">In this case, try clicking on the Uncompressed Video output pin from our Media File Input.</span></span> <span data-ttu-id="19615-177">Verrà aperta una finestra di dialogo che consente di esaminare il video in uscita.</span><span class="sxs-lookup"><span data-stu-id="19615-177">A dialog will open up that allows to inspect the outbound video.</span></span>

![Analisi del pin di output Uncompressed Video](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-inspecting-uncompressed-video-output.png)

<span data-ttu-id="19615-179">*Analisi del pin di output Uncompressed Video*</span><span class="sxs-lookup"><span data-stu-id="19615-179">*Inspecting the Uncompressed Video output pin*</span></span>

<span data-ttu-id="19615-180">In questo caso, ad esempio, indica che si ha a che fare con un input 1920x1080 a 24 fotogrammi al secondo nel campionamento 4:2:2 per un video di almeno 2 minuti.</span><span class="sxs-lookup"><span data-stu-id="19615-180">In our case, it tells us for example that we're dealing with a 1920x1080 input at 24 frames per second in 4:2:2 sampling for a video of almost 2 minutes.</span></span>

### <span data-ttu-id="19615-181"><a id="MXF_to_MP4_file_generation"></a>Aggiunta di un codificatore video per la generazione di file MP4</span><span class="sxs-lookup"><span data-stu-id="19615-181"><a id="MXF_to_MP4_file_generation"></a>Adding a video encoder for .MP4 file generation</span></span>
<span data-ttu-id="19615-182">Si noti che ora in Media File Input sono disponibili per l'uso un pin Uncompressed Video e più pin di output Uncompressed Audio.</span><span class="sxs-lookup"><span data-stu-id="19615-182">Note that now, an Uncompressed Video and multiple Uncompressed Audio output pins are available for use on our Media File Input.</span></span> <span data-ttu-id="19615-183">Per codificare il video in entrata, è necessario un componente di codifica, in questo caso per generare i file MP4.</span><span class="sxs-lookup"><span data-stu-id="19615-183">In order to encode the inbound video, we need an encoding component - in this case for generating .MP4 files.</span></span>

<span data-ttu-id="19615-184">Per codificare il flusso video in H.264, aggiungere il componente AVC Video Encoder all'area di progettazione.</span><span class="sxs-lookup"><span data-stu-id="19615-184">To encode the video stream to H.264, add the AVC Video Encoder component to the designer surface.</span></span> <span data-ttu-id="19615-185">Questo componente accetta un flusso video non compresso e genera un flusso video compresso AVC nel pin di output.</span><span class="sxs-lookup"><span data-stu-id="19615-185">This component takes an uncompress video stream as input and delivers an AVC compressed video stream on its output pin.</span></span>

![Codificatore AVC non connesso](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-avc-encoder.png)

<span data-ttu-id="19615-187">*Codificatore AVC non connesso*</span><span class="sxs-lookup"><span data-stu-id="19615-187">*Unconnected AVC Encoder*</span></span>

<span data-ttu-id="19615-188">Le proprietà determinano come avviene esattamente la codifica.</span><span class="sxs-lookup"><span data-stu-id="19615-188">Its properties determine how the encoding exactly happens.</span></span> <span data-ttu-id="19615-189">Ecco alcune delle impostazioni più importanti:</span><span class="sxs-lookup"><span data-stu-id="19615-189">Let's have a look at some of the more important settings:</span></span>

* <span data-ttu-id="19615-190">Output width e Output height: determinano la risoluzione del video codificato.</span><span class="sxs-lookup"><span data-stu-id="19615-190">Output width and Output height: these determine the resolution of the encoded video.</span></span> <span data-ttu-id="19615-191">In questo caso, si usa 640x360.</span><span class="sxs-lookup"><span data-stu-id="19615-191">In our case let's go with 640x360</span></span>
* <span data-ttu-id="19615-192">Frame Rate: se viene impostata su passthrough, adotterà la frequenza dei fotogrammi di origine, anche se è possibile eseguirne l'override.</span><span class="sxs-lookup"><span data-stu-id="19615-192">Frame Rate: when set to passthrough it will just adopt the source frame rate, it's possible to override this though.</span></span> <span data-ttu-id="19615-193">Si noti che tale conversione della frequenza dei fotogrammi non è compensata dal movimento.</span><span class="sxs-lookup"><span data-stu-id="19615-193">Note that such framerate conversion is not motion-compensated.</span></span>
* <span data-ttu-id="19615-194">Profile e Level: determinano il profilo e il livello AVC.</span><span class="sxs-lookup"><span data-stu-id="19615-194">Profile and Level: these determine the AVC profile and level.</span></span> <span data-ttu-id="19615-195">Per ottenere facilmente altre informazioni sui diversi livelli e profili, fare clic sull'icona del punto di domanda nel componente AVC Video Encoder. La pagina della Guida mostrerà altri dettagli su ogni livello.</span><span class="sxs-lookup"><span data-stu-id="19615-195">To conveniently get more information about the different levels and profiles, click the question mark icon on the AVC Video Encoder component and the help page will show more detail about each of the levels.</span></span> <span data-ttu-id="19615-196">Per questo esempio, si userà il profilo principale al livello 3.2 (impostazione predefinita).</span><span class="sxs-lookup"><span data-stu-id="19615-196">For our sample, let's go with Main Profile at level 3.2 (the default).</span></span>
* <span data-ttu-id="19615-197">Rate Control Mode e Bitrate (kbps): in questo scenario viene usato un output con velocità in bit costante (CBR) a 1200 kbps</span><span class="sxs-lookup"><span data-stu-id="19615-197">Rate Control Mode and Bitrate (kbps): in our scenario we opt for a constant bitrate (CBR) output at 1200 kbps</span></span>
* <span data-ttu-id="19615-198">Video Format: riguarda le informazioni sull'usabilità video che vengono scritte nel flusso H.264 (informazioni secondarie che possono essere usate da un decodificatore per migliorare la visualizzazione, ma non indispensabili per una corretta decodifica):</span><span class="sxs-lookup"><span data-stu-id="19615-198">Video Format: this is about the VUI (Video Usability Information) that gets written into the H.264 stream (side information that might be used by a decoder to enhance the display but not essential to correctly decode):</span></span>
* <span data-ttu-id="19615-199">NTSC (tipico per Stati Uniti o Giappone, usa 30 fps)</span><span class="sxs-lookup"><span data-stu-id="19615-199">NTSC (typical for US or Japan, using 30 fps)</span></span>
* <span data-ttu-id="19615-200">PAL (tipico per l'Europa, usa 25 fps)</span><span class="sxs-lookup"><span data-stu-id="19615-200">PAL (typical for Europe, using 25 fps)</span></span>
* <span data-ttu-id="19615-201">GOP Size Mode: in questo caso, verrà configurata una dimensione GOP fissa con un intervallo chiave di 2 secondi con GOP chiusi.</span><span class="sxs-lookup"><span data-stu-id="19615-201">GOP Size Mode: we'll configure Fixed GOP Size for our purposes with a Key Interval of 2 seconds with Closed GOPs.</span></span> <span data-ttu-id="19615-202">Questo assicura la compatibilità con la creazione dinamica di pacchetti fornita da Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="19615-202">This ensures compatibility with the dynamic packaging Azure Media Services provides.</span></span>

<span data-ttu-id="19615-203">Per alimentare il codificatore AVC, connettere il pin di output Uncompressed Video del componente Media File Input al pin di input Uncompressed Video del codificatore AVC.</span><span class="sxs-lookup"><span data-stu-id="19615-203">To feed our AVC encoder, connect the Uncompressed Video output pin from the Media File Input component to the Uncompressed Video input pin from the AVC encoder.</span></span>

![Codificatore AVC connesso](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-avc-encoder.png)

<span data-ttu-id="19615-205">*Codificatore principale AVC connesso*</span><span class="sxs-lookup"><span data-stu-id="19615-205">*Connected AVC Main encoder*</span></span>

### <span data-ttu-id="19615-206"><a id="MXF_to_MP4_audio"></a>Codifica del flusso audio</span><span class="sxs-lookup"><span data-stu-id="19615-206"><a id="MXF_to_MP4_audio"></a>Encoding the audio stream</span></span>
<span data-ttu-id="19615-207">A questo punto, il video è stato codificato, ma il flusso audio non compresso originale deve ancora essere compresso.</span><span class="sxs-lookup"><span data-stu-id="19615-207">At this point, we have encoded video but the original uncompressed audio stream still needs to be compressed.</span></span> <span data-ttu-id="19615-208">A questo scopo verrà applicata la codifica AAC usando il componente AAC Encoder (Dolby).</span><span class="sxs-lookup"><span data-stu-id="19615-208">For this we'll go with AAC encoding by the AAC Encoder (Dolby) component.</span></span> <span data-ttu-id="19615-209">Aggiungerlo al flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="19615-209">Add it to the workflow.</span></span>

![Codificatore AVC non connesso](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-aac-encoder.png)

<span data-ttu-id="19615-211">*Codificatore AAC non connesso*</span><span class="sxs-lookup"><span data-stu-id="19615-211">*Unconnected AAC encoder*</span></span>

<span data-ttu-id="19615-212">Ora esiste un'incompatibilità: è presente un solo pin di input audio non compresso dal codificatore AAC, ma molto probabilmente per Media File Input saranno disponibili due diversi flussi audio non compressi: uno per il canale audio sinistro e uno per quello destro.</span><span class="sxs-lookup"><span data-stu-id="19615-212">Now there's an incompatibility: there's only a single uncompressed audio input pin from the AAC Encoder while more than likely the Media File Input will have two different uncompressed audio stream available: one for the left audio channel and one for the right.</span></span> <span data-ttu-id="19615-213">Se si usa un sistema audio di tipo surround, i canali saranno addirittura 6. Quindi non è possibile connettere direttamente l'audio dall'origine Media File Input al codificatore audio AAC.</span><span class="sxs-lookup"><span data-stu-id="19615-213">(If you're dealing with surround sound, that's 6 channels.) So it's not possible to directly connect the audio from the Media File Input source into the AAC audio encoder.</span></span> <span data-ttu-id="19615-214">Per il componente AAC è previsto un flusso audio cosiddetto "con interleave": un solo flusso con entrambi i canali sinistro e destro con interleave reciproco.</span><span class="sxs-lookup"><span data-stu-id="19615-214">The AAC component expects a so-called "interleaved" audio stream: a single stream that has both the left and the right channels interleaved with each other.</span></span> <span data-ttu-id="19615-215">Una volta conosciuta dal file multimediale di origine la posizione nell'origine di ogni traccia audio, è possibile generare tale flusso audio con interleave con le posizioni degli altoparlanti assegnate correttamente per la sinistra e la destra.</span><span class="sxs-lookup"><span data-stu-id="19615-215">Once we know from our source media file which audio tracks are on what position in the source, we can generate such interleaved audio stream with the correctly assigned speaker positions for left and right.</span></span>

<span data-ttu-id="19615-216">Prima si genererà un flusso con interleave dai canali audio di origine necessari.</span><span class="sxs-lookup"><span data-stu-id="19615-216">First one will want to generated an interleaved stream from the required source audio channels.</span></span> <span data-ttu-id="19615-217">Il componente Audio Stream Interleaver lo gestirà automaticamente.</span><span class="sxs-lookup"><span data-stu-id="19615-217">The Audio Stream Interleaver component will handle this for us.</span></span> <span data-ttu-id="19615-218">Aggiungerlo al flusso di lavoro e connettere gli output audio da Media File Input a esso.</span><span class="sxs-lookup"><span data-stu-id="19615-218">Add it to the workflow and connect the audio outputs from the Media File Input into it.</span></span>

![Audio Stream Interleaver connesso](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-audio-stream-interleaver.png)

<span data-ttu-id="19615-220">*Audio Stream Interleaver connesso*</span><span class="sxs-lookup"><span data-stu-id="19615-220">*Connected Audio Stream Interleaver*</span></span>

<span data-ttu-id="19615-221">Ora che è disponibile un flusso audio con interleave, non si è tuttavia specificato a quali posizioni assegnare l'altoparlante sinistro o destro.</span><span class="sxs-lookup"><span data-stu-id="19615-221">Now that we have an interleaved audio stream, we still didn't specify where to assign the left or right speaker positions to.</span></span> <span data-ttu-id="19615-222">Per specificarlo, è possibile sfruttare Speaker Position Assigner.</span><span class="sxs-lookup"><span data-stu-id="19615-222">In order to specify this, we can leverage the Speaker Position Assigner.</span></span>

![Aggiunta di Speaker Position Assigner](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-speaker-position-assigner.png)

<span data-ttu-id="19615-224">*Aggiunta di Speaker Position Assigner*</span><span class="sxs-lookup"><span data-stu-id="19615-224">*Adding a Speaker Position Assigner*</span></span>

<span data-ttu-id="19615-225">Configurare Speaker Position Assigner per l'uso con un flusso di input stereo usando un filtro del set di impostazioni del codificatore "Custom" e il set di impostazioni del canale denominato "2.0 (L,R)".</span><span class="sxs-lookup"><span data-stu-id="19615-225">Configure the Speaker Position Assigner for use with a stereo input stream through an Encoder Preset Filter of "Custom" and the Channel Preset called "2.0 (L,R)".</span></span> <span data-ttu-id="19615-226">La posizione dell'altoparlante sinistro verrà assegnata al canale 1 e la posizione dell'altoparlante destro al canale 2.</span><span class="sxs-lookup"><span data-stu-id="19615-226">(This will assign the left speaker position to channel 1 and the right speaker position to channel 2.)</span></span>

<span data-ttu-id="19615-227">Connettere l'output di Speaker Position Assigner all'input del codificatore AAC.</span><span class="sxs-lookup"><span data-stu-id="19615-227">Connect the output of the Speaker Position Assigner to the input of the AAC Encoder.</span></span> <span data-ttu-id="19615-228">Indicare quindi al codificatore AAC di usare un set di impostazioni del canale "2.0 (L,R)", in modo che usi l'audio stereo come input.</span><span class="sxs-lookup"><span data-stu-id="19615-228">Then, tell the AAC Encoder to work with a "2.0 (L,R)" Channel Preset, so it knows to deal with stereo audio as input.</span></span>

### <span data-ttu-id="19615-229"><a id="MXF_to_MP4_audio_and_fideo"></a>Multiplexing di flussi audio e video in un contenitore MP4</span><span class="sxs-lookup"><span data-stu-id="19615-229"><a id="MXF_to_MP4_audio_and_fideo"></a>Multiplexing Audio and Video streams into an MP4 container</span></span>
<span data-ttu-id="19615-230">È possibile acquisire sia il flusso video con codifica AVC che il flusso audio con codifica AAC in un contenitore MP4.</span><span class="sxs-lookup"><span data-stu-id="19615-230">Given our AVC encoded video stream and our AAC encoded audio stream, we can capture both into an .MP4 container.</span></span> <span data-ttu-id="19615-231">Il processo di missaggio di flussi diversi in uno solo è chiamato "multiplexing" (o "muxing").</span><span class="sxs-lookup"><span data-stu-id="19615-231">The process of mixing different streams into a single one is called "multiplexing" (or "muxing").</span></span> <span data-ttu-id="19615-232">In questo caso verrà eseguito l'interleave dei flussi audio e video in un solo pacchetto MP4 coerente.</span><span class="sxs-lookup"><span data-stu-id="19615-232">In this case we're interleaving the audio and the video streams in a single coherent .MP4 package.</span></span> <span data-ttu-id="19615-233">Il componente che coordina questa operazione per un contenitore MP4 è chiamato ISO MPEG-4 Multiplexer.</span><span class="sxs-lookup"><span data-stu-id="19615-233">The component that coordinates this for an .MP4 container is called the ISO MPEG-4 Multiplexer.</span></span> <span data-ttu-id="19615-234">Aggiungerne uno all'area di progettazione e connettere sia AVC Video Encoder che il codificatore AAC agli input.</span><span class="sxs-lookup"><span data-stu-id="19615-234">Add one to the designer surface and connect both the AVC Video Encoder and the AAC Encoder to its inputs.</span></span>

![MPEG4 Multiplexer connesso](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-mpeg4-multiplexer.png)

<span data-ttu-id="19615-236">*MPEG4 Multiplexer connesso*</span><span class="sxs-lookup"><span data-stu-id="19615-236">*Connected MPEG4 Multiplexer*</span></span>

### <span data-ttu-id="19615-237"><a id="MXF_to_MP4_writing_mp4"></a>Scrittura del file MP4</span><span class="sxs-lookup"><span data-stu-id="19615-237"><a id="MXF_to_MP4_writing_mp4"></a>Writing the MP4 file</span></span>
<span data-ttu-id="19615-238">Quando si scrive un file di output, viene usato il componente File Output.</span><span class="sxs-lookup"><span data-stu-id="19615-238">When writing an output file, the File Output component is used.</span></span> <span data-ttu-id="19615-239">È possibile connetterlo all'output di ISO MPEG-4 Multiplexer in modo che l'output venga scritto sul disco.</span><span class="sxs-lookup"><span data-stu-id="19615-239">We can connect this to the output of the ISO MPEG-4 Multiplexer so that its output gets written to disk.</span></span> <span data-ttu-id="19615-240">A questo scopo, connettere il pin di output Container (MPEG-4) al pin di input Write di File Output.</span><span class="sxs-lookup"><span data-stu-id="19615-240">To do this, connect the Container (MPEG-4) output pin to the Write input pin of the File Output.</span></span>

![File Output connesso](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-file-output.png)

<span data-ttu-id="19615-242">*File Output connesso*</span><span class="sxs-lookup"><span data-stu-id="19615-242">*Connected File Output*</span></span>

<span data-ttu-id="19615-243">Il nome file che verrà usato viene determinato dalla proprietà File.</span><span class="sxs-lookup"><span data-stu-id="19615-243">The filename that will be used is determined by the File property.</span></span> <span data-ttu-id="19615-244">Anche se tale proprietà può essere hardcoded in un determinato valore, molto probabilmente si preferirà invece impostarla usando un'espressione.</span><span class="sxs-lookup"><span data-stu-id="19615-244">While that property can be hardcoded to a given value, most likely one will want to set it through an expression instead.</span></span>

<span data-ttu-id="19615-245">Per fare in modo che il flusso di lavoro determini automaticamente la proprietà File name di output da un'espressione, fare clic sul pulsante accanto al nome file (accanto all'icona della cartella).</span><span class="sxs-lookup"><span data-stu-id="19615-245">To have the workflow automatically determine the output File name property from an expression, click the buton next to the File name (next to the folder icon).</span></span> <span data-ttu-id="19615-246">Quindi scegliere "Expression" dal menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="19615-246">From the drop down menu then select "Expression".</span></span> <span data-ttu-id="19615-247">Verrà visualizzato l'editor espressioni.</span><span class="sxs-lookup"><span data-stu-id="19615-247">This will bring up the expression editor.</span></span> <span data-ttu-id="19615-248">Prima di tutto cancellare i contenuti dell'editor.</span><span class="sxs-lookup"><span data-stu-id="19615-248">Clear the contents of the editor first.</span></span>

![Expression Editor vuoto](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-empty-expression-editor.png)

<span data-ttu-id="19615-250">*Expression Editor vuoto*</span><span class="sxs-lookup"><span data-stu-id="19615-250">*Empty Expression Editor*</span></span>

<span data-ttu-id="19615-251">L'editor espressioni consente di immettere qualsiasi valore letterale, combinato con una o più variabili.</span><span class="sxs-lookup"><span data-stu-id="19615-251">The expression editor allows to enter any literal value, mixed with one or more variables.</span></span> <span data-ttu-id="19615-252">Le variabili iniziano con un simbolo di dollaro.</span><span class="sxs-lookup"><span data-stu-id="19615-252">Variables start with a dollar sign.</span></span> <span data-ttu-id="19615-253">Quando si preme il tasto $, l'editor visualizzerà una casella a discesa con le variabili disponibili.</span><span class="sxs-lookup"><span data-stu-id="19615-253">As you hit the $ key, the editor will show a dropdown box with a choice of available variables.</span></span> <span data-ttu-id="19615-254">In questo caso si userà una combinazione tra la variabile della directory di output e la variabile del nome file di input di base:</span><span class="sxs-lookup"><span data-stu-id="19615-254">In our case we'll use a combination of the output directory variable and the base input file name variable:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}.MP4

![Expression Editor compilato](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-expression-editor.png)

<span data-ttu-id="19615-256">*Expression Editor compilato*</span><span class="sxs-lookup"><span data-stu-id="19615-256">*Filled out Expression Editor*</span></span>

> [!NOTE]
> <span data-ttu-id="19615-257">Per visualizzare un file di output del processo di codifica in Azure, è necessario specificare un valore nell'editor espressioni.</span><span class="sxs-lookup"><span data-stu-id="19615-257">In order to see see an output file of your encoding job in Azure, you must provide a value in the expression editor.</span></span>
>
>

<span data-ttu-id="19615-258">Quando si conferma l'espressione facendo clic su OK, la finestra delle proprietà visualizzerà in anteprima il valore in cui viene attualmente risolta la proprietà File.</span><span class="sxs-lookup"><span data-stu-id="19615-258">When you confirm the expression by hitting ok, the property window will preview to what value the File property resolves at this point in time.</span></span>

![L'espressione File risolve la directory di output](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-expression-resolves-output-dir.png)

<span data-ttu-id="19615-260">*L'espressione File risolve la directory di output*</span><span class="sxs-lookup"><span data-stu-id="19615-260">*File Expression resolves output dir*</span></span>

### <span data-ttu-id="19615-261"><a id="MXF_to_MP4_asset_from_output"></a>Creazione di un asset di Servizi multimediali dal file di output</span><span class="sxs-lookup"><span data-stu-id="19615-261"><a id="MXF_to_MP4_asset_from_output"></a>Creating a Media Services Asset from the output file</span></span>
<span data-ttu-id="19615-262">Anche se è stato scritto un file di output MP4, tuttavia è necessario indicare che questo file appartiene all'asset di output che Servizi multimediali genererà come risultato dell'esecuzione del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="19615-262">While we have written an MP4 output file, we still need to indicate that this file belongs to the output asset which media services will generate as a result of executing this workflow.</span></span> <span data-ttu-id="19615-263">A questo scopo, viene usato il nodo Output File/Asset nel canvas del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="19615-263">To this end, the Output File/Asset node on the workflow canvas is used.</span></span> <span data-ttu-id="19615-264">Tutti i file in arrivo in questo nodo faranno parte dell'asset di Servizi multimediali di Azure risultante.</span><span class="sxs-lookup"><span data-stu-id="19615-264">All incoming files into this node will make part of the resulting Azure Media Services asset.</span></span>

<span data-ttu-id="19615-265">Connettere il componente File Output al componente Output File/Asset per completare il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="19615-265">Connect the File Output component to the Output File/Asset component to finish the workflow.</span></span>

![Flusso di lavoro completato](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow.png)

<span data-ttu-id="19615-267">*Flusso di lavoro completato*</span><span class="sxs-lookup"><span data-stu-id="19615-267">*Finished Workflow*</span></span>

### <span data-ttu-id="19615-268"><a id="MXF_to_MP4_test"></a>Testare il flusso di lavoro completato in locale</span><span class="sxs-lookup"><span data-stu-id="19615-268"><a id="MXF_to_MP4_test"></a>Test the finished workflow locally</span></span>
<span data-ttu-id="19615-269">Per testare il flusso di lavoro in locale, fare clic sul pulsante play nella barra degli strumenti in alto.</span><span class="sxs-lookup"><span data-stu-id="19615-269">To test the workflow locally, hit the play button in the toolbar at the top.</span></span> <span data-ttu-id="19615-270">Al termine dell'esecuzione del flusso di lavoro, esaminare l'output generato nella cartella di output configurata.</span><span class="sxs-lookup"><span data-stu-id="19615-270">When the workflow finished executing, inspect the output generated in the configured output folder.</span></span> <span data-ttu-id="19615-271">Verrà visualizzato il file di output MP4 completato codificato dal file di origine di input MXF.</span><span class="sxs-lookup"><span data-stu-id="19615-271">You'll see the finished MP4 output file that was encoded from the MXF input source file.</span></span>

## <span data-ttu-id="19615-272"><a id="MXF_to_MP4_with_dyn_packaging"></a>Codifica di un file MXF in MP4 - Creazione dinamica dei pacchetti a velocità in bit multipla abilitata</span><span class="sxs-lookup"><span data-stu-id="19615-272"><a id="MXF_to_MP4_with_dyn_packaging"></a>Encoding MXF into MP4 - multibitrate dynamic packaging enabled</span></span>
<span data-ttu-id="19615-273">In questa procedura dettagliata verrà creato un set di file MP4 a velocità in bit multipla con audio con codifica AAC da un solo file di input MXF.</span><span class="sxs-lookup"><span data-stu-id="19615-273">In this walkthrough we'll create a set of multiple bitrate MP4 files with AAC encoded audio from a single .MXF input file.</span></span>

<span data-ttu-id="19615-274">Quando si vuole usare un output di asset a velocità in bit multipla in combinazione con le funzionalità di Creazione dinamica dei pacchetti offerte da Servizi multimediali di Azure, dovranno essere generati più file MP4 allineati con GOP per ogni diversa velocità in bit e risoluzione.</span><span class="sxs-lookup"><span data-stu-id="19615-274">When a multi-bitrate asset output is desired for use in combination with the Dynamic Packaging features offered by Azure Media Services, multiple GOP-aligned MP4 files of each a different bitrate and resolution will need to be generated.</span></span> <span data-ttu-id="19615-275">A questo scopo, la procedura dettagliata [Codifica di un file MXF in un MP4 a velocità in bit singola](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) costituisce un valido punto di partenza.</span><span class="sxs-lookup"><span data-stu-id="19615-275">To do so, the [Encoding MXF into a single bitrate MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) walkthrough provides us with a good starting point.</span></span>

![Flusso di lavoro iniziale](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow.png)

<span data-ttu-id="19615-277">*Flusso di lavoro iniziale*</span><span class="sxs-lookup"><span data-stu-id="19615-277">*Starting Workflow*</span></span>

### <span data-ttu-id="19615-278"><a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>Aggiunta di uno o più output MP4</span><span class="sxs-lookup"><span data-stu-id="19615-278"><a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>Adding one or more additional MP4 outputs</span></span>
<span data-ttu-id="19615-279">Ogni file MP4 nell'asset di Servizi multimediali di Azure risultante supporterà una velocità in bit e una risoluzione diversa.</span><span class="sxs-lookup"><span data-stu-id="19615-279">Every MP4 file in our resulting Azure Media Services asset will support a different bitrate and resolution.</span></span> <span data-ttu-id="19615-280">Ora verrà aggiunto uno o più file di output MP4 al flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="19615-280">Let's add one or more MP4 output files to the workflow.</span></span>

<span data-ttu-id="19615-281">Per verificare che tutti i codificatori video creati abbiano le stesse impostazioni, la soluzione più comoda consiste nel duplicare il componente AVC Video Encoder esistente e configurare un'altra combinazione di risoluzione e velocità in bit (ne verrà aggiunta una pari a 960 x 540 a 25 fotogrammi al secondo a 2,5 Mbps).</span><span class="sxs-lookup"><span data-stu-id="19615-281">To make sure we have all our video encoders created with the same settings, it's most convenient to duplicate the already existing AVC Video Encoder and configure another combination of resolution and bitrate (let's add one of 960 x 540 at 25 frames per second at 2,5 Mbps).</span></span> <span data-ttu-id="19615-282">Per duplicare il codificatore esistente, copiarlo e incollarlo nell'area di progettazione.</span><span class="sxs-lookup"><span data-stu-id="19615-282">To duplicate the existing encoder, copy paste it on the designer surface.</span></span>

<span data-ttu-id="19615-283">Connettere il pin di output Uncompressed Video di Media File Input nel nuovo componente AVC.</span><span class="sxs-lookup"><span data-stu-id="19615-283">Connect the Uncompressed Video output pin of the Media File Input into our new AVC component.</span></span>

![Secondo codificatore AVC connesso](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-avc-encoder-connected.png)

<span data-ttu-id="19615-285">*Secondo codificatore AVC connesso*</span><span class="sxs-lookup"><span data-stu-id="19615-285">*Second AVC encoder connected*</span></span>

<span data-ttu-id="19615-286">Adattare ora la configurazione del nuovo codificatore AVC all'output 960x540 a 2,5 Mbps</span><span class="sxs-lookup"><span data-stu-id="19615-286">Now adapt the configuration for our new AVC encoder to output 960x540 at 2,5 Mbps.</span></span> <span data-ttu-id="19615-287">usando le proprietà "Output width", "Output height" e "Bitrate (kbps)".</span><span class="sxs-lookup"><span data-stu-id="19615-287">(Use its properties "Output width", "Output height", and "Bitrate (kbps)" for this.)</span></span>

<span data-ttu-id="19615-288">Poiché si vuole usare l'asset risultante con la creazione dinamica dei pacchetti di Servizi multimediali di Azure, l'endpoint di streaming deve poter generare da questi file MP4 frammenti DASH/MP4 frammentati/HLS esattamente allineati tra loro in modo che i client che passano da una velocità in bit a un'altra ottengano un'esperienza video e audio continua e uniforme.</span><span class="sxs-lookup"><span data-stu-id="19615-288">Given we want to use the resulting asset together with Azure Media Services' dynamic packaging, the streaming endpoint needs to be capable of generating from these MP4 files HLS/Fragmented MP4/DASH fragments that are exactly aligned to each other in a way that clients that are switching between different bitrates get a single smooth continuous video and audio experience.</span></span> <span data-ttu-id="19615-289">A questo scopo, è necessario assicurarsi che nelle proprietà di entrambi i codificatori AVC la dimensione GOP ("Group of Pictures") per entrambi i file MP4 sia impostata su 2 secondi, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="19615-289">To make that happen, we need to ensure that, in the properties of both AVC encoders the GOP ("group of pictures") size for both MP4 files is set to 2 seconds, which can be done by:</span></span>

* <span data-ttu-id="19615-290">impostare GOP Size Mode sulla dimensione Fixed GOP e</span><span class="sxs-lookup"><span data-stu-id="19615-290">setting the GOP Size Mode to Fixed GOP size and</span></span>
* <span data-ttu-id="19615-291">Key Frame Interval su due secondi</span><span class="sxs-lookup"><span data-stu-id="19615-291">the Key Frame Interval to two seconds.</span></span>
* <span data-ttu-id="19615-292">impostare anche GOP IDR Control su Closed GOP per assicurarsi che tutti i GOP siano autonomi senza dipendenze</span><span class="sxs-lookup"><span data-stu-id="19615-292">also set the GOP IDR Control to Closed GOP to ensure all GOP's are standing on their own without dependencies</span></span>

<span data-ttu-id="19615-293">Per rendere comprensibile il flusso di lavoro, rinominare il primo codificatore AVC "AVC Video Encoder 640x360 1200kbps" e il secondo codificatore AVC "AVC Video Encoder 960x540 2500 kbps".</span><span class="sxs-lookup"><span data-stu-id="19615-293">To make our workflow convenient to understand, rename the first AVC encoder to "AVC Video Encoder 640x360 1200kbps" and the second AVC encoder "AVC Video Encoder 960x540 2500 kbps".</span></span>

<span data-ttu-id="19615-294">Ora aggiungere un secondo componente ISO MPEG-4 Multiplexer e un secondo componente File Output.</span><span class="sxs-lookup"><span data-stu-id="19615-294">Now add a second ISO MPEG-4 Multiplexer and a second File Output.</span></span> <span data-ttu-id="19615-295">Connettere il multiplexer al nuovo codificatore AVC e verificare che l'output sia diretto a File Output.</span><span class="sxs-lookup"><span data-stu-id="19615-295">Connect the multiplexer to the new AVC encoder and make sure its output is directed into the File Output.</span></span> <span data-ttu-id="19615-296">Quindi connettere anche l'output del codificatore audio AAC all'input del nuovo multiplexer.</span><span class="sxs-lookup"><span data-stu-id="19615-296">Then also connect the AAC audio encoder output to the new multiplexer's input.</span></span> <span data-ttu-id="19615-297">File Output a sua volta può essere connesso al nodo Output File/Asset per aggiungerlo all'asset di Servizi multimediali che verrà creato.</span><span class="sxs-lookup"><span data-stu-id="19615-297">The File Output in turn can then be connected to the Output File/Asset node to add it to the Media Services Asset that will be created.</span></span>

![Secondo muxer e File Output connessi](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-muxer-file-output-connected.png)

<span data-ttu-id="19615-299">*Secondo muxer e File Output connessi*</span><span class="sxs-lookup"><span data-stu-id="19615-299">*Second Muxer and File Output connected*</span></span>

<span data-ttu-id="19615-300">Per assicurare la compatibilità con la creazione dinamica dei pacchetti di Servizi multimediali di Azure, impostare Chunk Mode del multiplexer su GOP count o su Duration e impostare i GOP per ogni blocco su 1.</span><span class="sxs-lookup"><span data-stu-id="19615-300">For compatibility with Azure Media Services dynamic packaging, configure the multiplexer's Chunk Mode to GOP count or duration and set the GOPs per chunk to 1.</span></span> <span data-ttu-id="19615-301">Questa dovrebbe essere l'impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="19615-301">(This should be the default.)</span></span>

![Modalità blocco del muxer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-muxer-chunk-modes.png)

<span data-ttu-id="19615-303">*Modalità blocco del muxer*</span><span class="sxs-lookup"><span data-stu-id="19615-303">*Muxer Chunk Modes*</span></span>

<span data-ttu-id="19615-304">Nota: è possibile ripetere questo processo per tutte le altre combinazioni di velocità in bit e risoluzione che si vuole aggiungere all'output dell'asset.</span><span class="sxs-lookup"><span data-stu-id="19615-304">Note: you may want to repeat this process for any other bitrate and resolution combinations you want to have added to the asset output.</span></span>

### <span data-ttu-id="19615-305"><a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>Configurazione dei nomi di output dei file</span><span class="sxs-lookup"><span data-stu-id="19615-305"><a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>Configuring the file output names</span></span>
<span data-ttu-id="19615-306">È stato aggiunto più di un file all'asset di output.</span><span class="sxs-lookup"><span data-stu-id="19615-306">We have more than one single file added to the output asset.</span></span> <span data-ttu-id="19615-307">Per questo è necessario verificare che i nomi di ogni file di output siano tutti diversi ed eventualmente applicare anche una convenzione di denominazione file in modo che dal nome file risulti chiaro di che cosa si tratta.</span><span class="sxs-lookup"><span data-stu-id="19615-307">This provides a need to make sure the filenames for each of the output files are different from each other and maybe even apply a file-naming convention so it becomes clear from the file name what you're dealing with.</span></span>

<span data-ttu-id="19615-308">La denominazione dell'output dei file può essere controllata con le espressioni nella finestra di progettazione.</span><span class="sxs-lookup"><span data-stu-id="19615-308">File output naming can be controlled through expressions in the designer.</span></span> <span data-ttu-id="19615-309">Aprire il riquadro delle proprietà per uno dei componenti File Output e aprire l'editor espressioni per la proprietà File.</span><span class="sxs-lookup"><span data-stu-id="19615-309">Open the property pane for one of the File Output components and open the expression editor for the File property.</span></span> <span data-ttu-id="19615-310">Il primo file di output è stato configurato con l'espressione seguente (vedere l'esercitazione per la codifica da un [file MXF in un MP4 a velocità in bit singola](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):</span><span class="sxs-lookup"><span data-stu-id="19615-310">Our first output file was configured through the following expression (see the tutorial for going from [MXF to a single bitrate MP4 output](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}.MP4

<span data-ttu-id="19615-311">Il nome file viene quindi determinato da due variabili: la directory di output in cui scrivere e il nome di base del file di origine.</span><span class="sxs-lookup"><span data-stu-id="19615-311">This means that our filename is determined by two variables: the output directory to write in and the source file base name.</span></span> <span data-ttu-id="19615-312">La prima viene esposta come proprietà nella radice del flusso di lavoro e il secondo viene determinato dal file in arrivo.</span><span class="sxs-lookup"><span data-stu-id="19615-312">The former is exposed as a property on the workflow root and the latter is determined by the incoming file.</span></span> <span data-ttu-id="19615-313">Si noti che la directory di output è quella usata per il test locale. Il motore del flusso di lavoro eseguirà l'override di questa proprietà quando il flusso di lavoro verrà eseguito dal processore multimediale basato sul cloud in Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="19615-313">Note that the output directory is what you use for local testing; this property will be overridden by the workflow engine when the workflow is executed by the cloud-based media processor in Azure Media Services.</span></span>
<span data-ttu-id="19615-314">Per assegnare a entrambi i file di output una denominazione di output coerente, modificare l'espressione di denominazione del primo file in:</span><span class="sxs-lookup"><span data-stu-id="19615-314">To give both our output files a consistent output naming, change the first file naming expression to:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

<span data-ttu-id="19615-315">e la seconda in:</span><span class="sxs-lookup"><span data-stu-id="19615-315">and the second to:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_960x540_2.MP4

<span data-ttu-id="19615-316">Effettuare un'esecuzione di test intermedia per verificare che entrambi i file di output MP4 vengano generati correttamente.</span><span class="sxs-lookup"><span data-stu-id="19615-316">Execute an intermediate test run to make sure both MP4 output files are properly generated.</span></span>

### <span data-ttu-id="19615-317"><a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>Aggiunta di una traccia audio separata</span><span class="sxs-lookup"><span data-stu-id="19615-317"><a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>Adding a separate Audio Track</span></span>
<span data-ttu-id="19615-318">Come sarà illustrato in seguito, quando si genera un file ism da usare con i file di output MP4, sarà necessario anche un file MP4 solo audio come traccia audio per il flusso adattivo.</span><span class="sxs-lookup"><span data-stu-id="19615-318">As we'll see later when we generate an .ism file to go with our MP4 output files, we will also require a audio-only MP4 file as the audio track for our adaptive streaming.</span></span> <span data-ttu-id="19615-319">Per creare questo file, aggiungere un altro muxer al flusso di lavoro (ISO-MPEG-4 Multiplexer) e connettere il pin di output del codificatore AAC al pin di input per Track 1.</span><span class="sxs-lookup"><span data-stu-id="19615-319">To create this file, add an additional muxer to the workflow (ISO-MPEG-4 Multiplexer) and connect the AAC encoder's output pin with its input pin for Track 1.</span></span>

![Muxer audio aggiunto](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-added.png)

<span data-ttu-id="19615-321">*Muxer audio aggiunto*</span><span class="sxs-lookup"><span data-stu-id="19615-321">*Audio Muxer Added*</span></span>

<span data-ttu-id="19615-322">Creare un terzo componente File Output per l'output del flusso in uscita dal muxer e configurare l'espressione di denominazione file come:</span><span class="sxs-lookup"><span data-stu-id="19615-322">Create a third File Output component to output the outbound stream from the muxer and configure the file naming expression as:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_128kbps_audio.MP4

![Creazione di File Output con il muxer audio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-creating-file-output.png)

<span data-ttu-id="19615-324">*Creazione di File Output con il muxer audio*</span><span class="sxs-lookup"><span data-stu-id="19615-324">*Audio Muxer creating File Output*</span></span>

### <span data-ttu-id="19615-325"><a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>Aggiunta del file SMIL ISM</span><span class="sxs-lookup"><span data-stu-id="19615-325"><a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>Adding the .ISM SMIL File</span></span>
<span data-ttu-id="19615-326">Per il funzionamento della creazione dinamica dei pacchetti con entrambi i file MP4 (e l'MP4 solo audio) nell'asset di Servizi multimediali, è necessario anche un file manifesto (chiamato anche file "SMIL": Synchronized Multimedia Integration Language).</span><span class="sxs-lookup"><span data-stu-id="19615-326">For the dynamic packaging to work in combination with both MP4 files (and the audio-only MP4) in our Media Services asset, we also need a manifest file (also called a "SMIL" file: Synchronized Multimedia Integration Language).</span></span> <span data-ttu-id="19615-327">Questo file indica a Servizi multimediali di Azure quali file MP4 sono disponibili per la creazione dinamica dei pacchetti e quali tenere in considerazione per il flusso audio.</span><span class="sxs-lookup"><span data-stu-id="19615-327">This file indicates to Azure Media Services what MP4 files are available for dynamic packaging and which of those to consider for the audio streaming.</span></span> <span data-ttu-id="19615-328">Un file manifesto tipico per un set di MP4 con un solo flusso audio sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="19615-328">A typical manifest file for a set of MP4's with a single audio stream looks like this:</span></span>

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

<span data-ttu-id="19615-329">Il file ism contiene in un'istruzione switch un riferimento a ogni singolo file video MP4 e, oltre a questi, anche uno o più file audio fanno riferimento a un MP4 contenente solo l'audio.</span><span class="sxs-lookup"><span data-stu-id="19615-329">The .ism file contains within a switch statement, a reference to each of the individual MP4 video files and in addition to those also one (or more) audio file references to an MP4 that only contains the audio.</span></span>

<span data-ttu-id="19615-330">La generazione del file manifesto per il set di MP4 può essere eseguita con un componente denominato "AMS Manifest Writer".</span><span class="sxs-lookup"><span data-stu-id="19615-330">Generating the manifest file for our set of MP4's can be done through a component called the "AMS Manifest Writer".</span></span> <span data-ttu-id="19615-331">Per usarlo, trascinarlo sulla superficie e connettere i pin di output "Write Complete" dai tre componenti File Output all'input di AMS Manifest Writer.</span><span class="sxs-lookup"><span data-stu-id="19615-331">To use it, drag it onto the surface and connect the "Write Complete" output pins from the three File Output components to the AMS Manifest Writer input.</span></span> <span data-ttu-id="19615-332">Verificare quindi di connettere l'output di AMS Manifest Writer ad Output File/Asset.</span><span class="sxs-lookup"><span data-stu-id="19615-332">Then make sure to connect the output of the AMS Manifest Writer to the Output File/Asset.</span></span>

<span data-ttu-id="19615-333">Come per gli altri componenti di output dei file, configurare il nome di output del file ism con un'espressione:</span><span class="sxs-lookup"><span data-stu-id="19615-333">As with our other file output components, configure the .ism file output name with an expression:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_manifest.ism

<span data-ttu-id="19615-334">Il flusso di lavoro completato è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="19615-334">Our finished workflow looks like the below:</span></span>

![File MXF completato nel flusso di lavoro MP4 a velocità in bit multipla](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-mxf-to-multibitrate-mp4-workflow.png)

<span data-ttu-id="19615-336">*File MXF completato nel flusso di lavoro MP4 a velocità in bit multipla*</span><span class="sxs-lookup"><span data-stu-id="19615-336">*Finished MXF to multibitrate MP4 workflow*</span></span>

## <span data-ttu-id="19615-337"><a id="MXF_to__multibitrate_MP4"></a>Codifica di un file MXF in un MP4 a velocità in bit multipla - Progetto avanzato</span><span class="sxs-lookup"><span data-stu-id="19615-337"><a id="MXF_to__multibitrate_MP4"></a>Encoding MXF into multibitrate MP4 - enhanced blueprint</span></span>
<span data-ttu-id="19615-338">Nella [procedura dettagliata sul flusso di lavoro precedente](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) è stato illustrato come un solo asset di input MXF possa essere convertito in un asset di output con file MP4 a velocità in bit multipla, un file MP4 solo audio e un file manifesto da usare con la creazione dinamica dei pacchetti di Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="19615-338">In the [previous workflow walkthrough](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) we've seen how a single MXF input asset can be converted into an output asset with multi-bitrate MP4 files, an audio-only MP4 file and a manifest file for use in conjunction with Azure Media Services dynamic packaging.</span></span>

<span data-ttu-id="19615-339">Questa procedura dettagliata illustra come alcuni aspetti possano essere migliorati e diventare più pratici.</span><span class="sxs-lookup"><span data-stu-id="19615-339">This walkthrough will show how some of the aspects can be enhanced and made more convenient.</span></span>

### <span data-ttu-id="19615-340"><a id="MXF_to_multibitrate_MP4_overview"></a>Panoramica del flusso di lavoro da migliorare</span><span class="sxs-lookup"><span data-stu-id="19615-340"><a id="MXF_to_multibitrate_MP4_overview"></a>Workflow overview to enhance</span></span>
![Flusso di lavoro MP4 a velocità in bit multipla da migliorare](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-enhance.png)

<span data-ttu-id="19615-342">*Flusso di lavoro MP4 a velocità in bit multipla da migliorare*</span><span class="sxs-lookup"><span data-stu-id="19615-342">*Multibitrate MP4 workflow to enhance*</span></span>

### <span data-ttu-id="19615-343"><a id="MXF_to__multibitrate_MP4_file_naming"></a>Convenzioni di denominazione dei file</span><span class="sxs-lookup"><span data-stu-id="19615-343"><a id="MXF_to__multibitrate_MP4_file_naming"></a>File Naming Conventions</span></span>
<span data-ttu-id="19615-344">Nel flusso di lavoro precedente è stata specificata una semplice espressione come base per la generazione dei nomi file di output,</span><span class="sxs-lookup"><span data-stu-id="19615-344">In the previous workflow we specified a simple expression as the basis for generating output file names.</span></span> <span data-ttu-id="19615-345">ma ci sono state alcune duplicazioni: tutti i singoli componenti dei file di output hanno specificato tale espressione.</span><span class="sxs-lookup"><span data-stu-id="19615-345">We have some duplication though: all of the the individual output file components specified such expression.</span></span>

<span data-ttu-id="19615-346">Ad esempio, il componente File Output per il primo file video è configurato con questa espressione:</span><span class="sxs-lookup"><span data-stu-id="19615-346">For example, our file output component for the first video file is configured with this expression:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

<span data-ttu-id="19615-347">Invece per il secondo video di output, l'espressione è:</span><span class="sxs-lookup"><span data-stu-id="19615-347">While for the second output video, we have an expression like:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_960x540_2.MP4

<span data-ttu-id="19615-348">Non sarebbe più lineare, meno soggetto a errori e più pratico, se fosse possibile rimuovere alcune duplicazioni e rendere il tutto più facilmente configurabile?</span><span class="sxs-lookup"><span data-stu-id="19615-348">Wouldn't it be cleaner, less error prone and more convenient if we could remove some of this duplication and make things more configurable instead?</span></span> <span data-ttu-id="19615-349">Fortunatamente è possibile: le funzionalità delle espressioni della finestra di progettazione unite alla possibilità di creare proprietà personalizzate nella radice del flusso di lavoro offrono un livello di praticità aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="19615-349">Luckily we can: the designer's expression capabilities in combination with the ability to create custom properties on our workflow root will give us an added layer of convenience.</span></span>

<span data-ttu-id="19615-350">Si supponga che la configurazione dei nomi file si basi sulle velocità in bit dei singoli file MP4.</span><span class="sxs-lookup"><span data-stu-id="19615-350">Let's assume we'll drive filename configuration from the bitrates of the individual MP4 files.</span></span> <span data-ttu-id="19615-351">Queste velocità in bit dovranno essere configurate in una posizione centrale (nella radice del grafico), da dove saranno accessibili per configurare e determinare la generazione dei nomi file.</span><span class="sxs-lookup"><span data-stu-id="19615-351">These bitrates we'll aim to configure in one central place (on the root of our graph), from where they'll be accessed to configure and drive file name generation.</span></span> <span data-ttu-id="19615-352">A questo scopo, iniziare pubblicando la proprietà della velocità in bit da entrambi i codificatori AVC nella radice del flusso di lavoro, in modo che sia accessibile da entrambe le radici oltre che dai codificatori AVC.</span><span class="sxs-lookup"><span data-stu-id="19615-352">To do this, we start by publishing the bitrate property from both AVC encoders to the root of our workflow, so that it becomes accessible from both the root as well as from the AVC encoders.</span></span> <span data-ttu-id="19615-353">Anche se visualizzata in due punti diversi, esiste un solo valore sottostante.</span><span class="sxs-lookup"><span data-stu-id="19615-353">(Even if displayed in two different spots, there's only one underlying value.)</span></span>

### <span data-ttu-id="19615-354"><a id="MXF_to__multibitrate_MP4_publishing"></a>Pubblicazione delle proprietà dei componenti nella radice del flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="19615-354"><a id="MXF_to__multibitrate_MP4_publishing"></a>Publishing component properties onto the workflow root</span></span>
<span data-ttu-id="19615-355">Aprire il primo codificatore AVC, andare alla proprietà Bitrate (kbps) e nel menu a discesa scegliere Publish.</span><span class="sxs-lookup"><span data-stu-id="19615-355">Open the first AVC encoder, go to the Bitrate (kbps) property and from the dropdown choose Publish.</span></span>

![Pubblicazione della proprietà della velocità in bit](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-bitrate-property.png)

<span data-ttu-id="19615-357">*Pubblicazione della proprietà della velocità in bit*</span><span class="sxs-lookup"><span data-stu-id="19615-357">*Publishing the bitrate property*</span></span>

<span data-ttu-id="19615-358">Configurare la finestra di dialogo di pubblicazione per la pubblicazione nella radice del grafico del flusso di lavoro, con il nome pubblicato "video1bitrate" e il nome visualizzato leggibile "Video 1 Bitrate".</span><span class="sxs-lookup"><span data-stu-id="19615-358">Configure the publish dialog to publish to the root of our workflow graph, with a published name of "video1bitrate" and a readable display name of "Video 1 Bitrate".</span></span> <span data-ttu-id="19615-359">Configurare un nome gruppo denominato "Streaming Bitrates" e fare clic su Publish.</span><span class="sxs-lookup"><span data-stu-id="19615-359">Configure a custom group name called "Streaming Bitrates" and hit Publish.</span></span>

![Pubblicazione della proprietà della velocità in bit](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-bitrate-property.png)

<span data-ttu-id="19615-361">*Finestra di dialogo di pubblicazione per la proprietà della velocità in bit*</span><span class="sxs-lookup"><span data-stu-id="19615-361">*Publishing dialog for bitrate property*</span></span>

<span data-ttu-id="19615-362">Ripetere le stesse operazioni per la proprietà della velocità in bit del secondo codificatore AVC e denominarla "video2bitrate" con il nome visualizzato "Video 2 Bitrate", nello stesso gruppo personalizzato "Streaming Bitrates".</span><span class="sxs-lookup"><span data-stu-id="19615-362">Repeat the same for the bitrate property of the second AVC encoder and name it "video2bitrate" with a display name of "Video 2 Bitrate", in the same custom group "Streaming Bitrates".</span></span>

<span data-ttu-id="19615-363">Se ora si esaminano le proprietà della radice del flusso di lavoro, si noterà il gruppo personalizzato con le due proprietà pubblicate visualizzate.</span><span class="sxs-lookup"><span data-stu-id="19615-363">If we now inspect the workflow root properties, we'll see our custom group with the two published properties show up.</span></span> <span data-ttu-id="19615-364">Entrambe mostrano il valore della velocità in bit del rispettivo codificatore AVC.</span><span class="sxs-lookup"><span data-stu-id="19615-364">Both are reflecting the value of their respective AVC encoder bitrate.</span></span>

![Proprietà della velocità in bit pubblicate nella radice del flusso di lavoro](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-bitrate-props-on-workflow-root.png)

<span data-ttu-id="19615-366">Quando si vuole accedere a queste proprietà dal codice o da un'espressione, è possibile eseguire questa operazione:</span><span class="sxs-lookup"><span data-stu-id="19615-366">Whenever we want to access these properties from code or from an expression, we can do so like this:</span></span>

* <span data-ttu-id="19615-367">dal codice inline da un componente direttamente sotto la radice: node.getPropertyAsString('../video1bitrate',null)</span><span class="sxs-lookup"><span data-stu-id="19615-367">from inline code from a component right below the root: node.getPropertyAsString('../video1bitrate',null)</span></span>
* <span data-ttu-id="19615-368">in un'espressione: ${ROOT_video1bitrate}</span><span class="sxs-lookup"><span data-stu-id="19615-368">within an expression: ${ROOT_video1bitrate}</span></span>

<span data-ttu-id="19615-369">Completare ora il gruppo "Streaming Bitrates" pubblicando anche la velocità in bit della traccia audio.</span><span class="sxs-lookup"><span data-stu-id="19615-369">Let's complete the "Streaming Bitrates" group by publishing our audio track bitrate on it as well.</span></span> <span data-ttu-id="19615-370">Nelle proprietà del codificatore AAC cercare l'impostazione Bitrate e scegliere Publish dal menu a discesa accanto a essa.</span><span class="sxs-lookup"><span data-stu-id="19615-370">Within the properties of the AAC Encoder, search for the Bitrate setting and select Publish from the dropdown next to it.</span></span> <span data-ttu-id="19615-371">Eseguire la pubblicazione nella radice del grafico con il nome "audio1bitrate" e il nome visualizzato "Audio 1 Bitrate" nel gruppo personalizzato "Streaming Bitrates".</span><span class="sxs-lookup"><span data-stu-id="19615-371">Publish to the root of the graph with name "audio1bitrate" and display name "Audio 1 Bitrate" within our custom group "Streaming Bitrates".</span></span>

![Finestra di dialogo di pubblicazione per la velocità in bit audio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-audio-bitrate.png)

<span data-ttu-id="19615-373">*Finestra di dialogo di pubblicazione per la velocità in bit audio*</span><span class="sxs-lookup"><span data-stu-id="19615-373">*Publishing dialog for audio bitrate*</span></span>

![Proprietà video e audio risultanti nella radice](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-resulting-video-and-audio-props-on-root.png)

<span data-ttu-id="19615-375">*Proprietà video e audio risultanti nella radice*</span><span class="sxs-lookup"><span data-stu-id="19615-375">*Resulting video and audio props on root*</span></span>

<span data-ttu-id="19615-376">Si noti che, modificando uno dei tre valori, vengono riconfigurati e modificati anche i valori nei rispettivi componenti a cui sono collegati (e da cui sono stati pubblicati).</span><span class="sxs-lookup"><span data-stu-id="19615-376">Note that changing any of those three values also re-configures and changes the values on the respective components they are linked with (and where published from).</span></span>

### <span data-ttu-id="19615-377"><a id="MXF_to__multibitrate_MP4_output_files"></a>Fare in modo che i nomi file di output generati si basino sui valori delle proprietà pubblicati</span><span class="sxs-lookup"><span data-stu-id="19615-377"><a id="MXF_to__multibitrate_MP4_output_files"></a>Have generated output file names rely on published property values</span></span>
<span data-ttu-id="19615-378">Invece di impostare come hardcoded i nomi file generati, ora è possibile modificare l'espressione del nome file in ogni componente File Output in modo che si basi sulle proprietà delle velocità in bit pubblicate nella radice del grafico.</span><span class="sxs-lookup"><span data-stu-id="19615-378">Instead of hardcoding our generated file names, we can now change our filename expression on each of the File Output components to rely on the bitrate properties we just published on the graph root.</span></span> <span data-ttu-id="19615-379">Iniziando dal primo componente File Output, trovare la proprietà File e modificare l'espressione in questo modo:</span><span class="sxs-lookup"><span data-stu-id="19615-379">Starting with our first file output, find the File property and edit the expression like this:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video1bitrate}kbps.MP4

<span data-ttu-id="19615-380">I diversi parametri di questa espressione sono accessibili e possono essere immessi premendo il simbolo di dollaro sulla tastiera mentre è attiva la finestra dell'espressione.</span><span class="sxs-lookup"><span data-stu-id="19615-380">The different parameters in this expression can be accessed and entered by hitting the dollar sign on the keyboard while in the expression window.</span></span> <span data-ttu-id="19615-381">Uno dei parametri disponibili è la proprietà video1bitrate pubblicata prima.</span><span class="sxs-lookup"><span data-stu-id="19615-381">One of the available parameters is our video1bitrate property which we published earlier.</span></span>

![Accesso ai parametri in un'espressione](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-accessing-parameters-within-an-expression.png)

<span data-ttu-id="19615-383">*Accesso ai parametri in un'espressione*</span><span class="sxs-lookup"><span data-stu-id="19615-383">*Accessing parameters within an expression*</span></span>

<span data-ttu-id="19615-384">Eseguire le stesse operazioni per il componente File Output per il secondo video:</span><span class="sxs-lookup"><span data-stu-id="19615-384">Do the same for the file output for our second video:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video2bitrate}kbps.MP4

<span data-ttu-id="19615-385">e per il componente File Output solo audio:</span><span class="sxs-lookup"><span data-stu-id="19615-385">and for the audio-only file output:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_audio1bitrate}bps_audio.MP4

<span data-ttu-id="19615-386">Se ora si modifica la velocità in bit per uno dei file video o audio, il rispettivo codificatore verrà riconfigurato e la convenzione dei nomi file basata sulla velocità in bit verrà rispettata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="19615-386">If we now change the bitrate for any of the video or audio files, the respective encoder will be reconfigured and the bitrate-based file name convention will be honored all automatic.</span></span>

## <span data-ttu-id="19615-387"><a id="thumbnails_to__multibitrate_MP4"></a>Aggiunta di anteprime all'output MP4 a velocità in bit multipla</span><span class="sxs-lookup"><span data-stu-id="19615-387"><a id="thumbnails_to__multibitrate_MP4"></a>Adding thumbnails to multibitrate MP4 output</span></span>
<span data-ttu-id="19615-388">Partendo da un flusso di lavoro che genera [un output MP4 a velocità in bit multipla da un input MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), verrà ora esaminata l'aggiunta di anteprime all'output.</span><span class="sxs-lookup"><span data-stu-id="19615-388">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into adding thumbnails to the output.</span></span>

### <span data-ttu-id="19615-389"><a id="thumbnails_to__multibitrate_MP4_overview"></a>Panoramica del flusso di lavoro a cui aggiungere le anteprime</span><span class="sxs-lookup"><span data-stu-id="19615-389"><a id="thumbnails_to__multibitrate_MP4_overview"></a>Workflow overview to add thumbnails to</span></span>
![Flusso di lavoro MP4 a velocità in bit multipla da cui iniziare](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-start-from.png)

<span data-ttu-id="19615-391">*Flusso di lavoro MP4 a velocità in bit multipla da cui iniziare*</span><span class="sxs-lookup"><span data-stu-id="19615-391">*Multibitrate MP4 workflow to start from*</span></span>

### <span data-ttu-id="19615-392"><a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>Aggiunta della codifica JPG</span><span class="sxs-lookup"><span data-stu-id="19615-392"><a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>Adding JPG Encoding</span></span>
<span data-ttu-id="19615-393">La base della generazione delle anteprime sarà il componente JPG Encoder, usato per l'output di file JPG.</span><span class="sxs-lookup"><span data-stu-id="19615-393">The heart of our thumbnail generation will be the JPG Encoder component, able to output JPG files.</span></span>

![JPG Encoder](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-jpg-encoder.png)

<span data-ttu-id="19615-395">*JPG Encoder*</span><span class="sxs-lookup"><span data-stu-id="19615-395">*JPG Encoder*</span></span>

<span data-ttu-id="19615-396">Non è tuttavia possibile connettere direttamente il flusso Uncompressed Video dal componente Media File Input al codificatore JPG.</span><span class="sxs-lookup"><span data-stu-id="19615-396">We cannot however directly connect our Uncompressed Video stream from the Media File Input into the JPG encoder.</span></span> <span data-ttu-id="19615-397">È invece previsto che gli vengano passati i singoli fotogrammi.</span><span class="sxs-lookup"><span data-stu-id="19615-397">Instead, it expects to be handed individual frames.</span></span> <span data-ttu-id="19615-398">Questa operazione può essere eseguita con il componente Video Frame Gate.</span><span class="sxs-lookup"><span data-stu-id="19615-398">This, we can do through the Video Frame Gate component.</span></span>

![Connessione di un'attività di controllo dei fotogrammi al codificatore JPG](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-frame-gate-to-jpg-encoder.png)

<span data-ttu-id="19615-400">*Connessione di un'attività di controllo dei fotogrammi al codificatore JPG*</span><span class="sxs-lookup"><span data-stu-id="19615-400">*Connecting a frame gate to the JPG encoder*</span></span>

<span data-ttu-id="19615-401">L'attività di controllo dei fotogrammi consente a un fotogramma video di passare dopo un intervallo stabilito di secondi o di fotogrammi.</span><span class="sxs-lookup"><span data-stu-id="19615-401">The frame gate once every so many seconds or frames allows a video frame to pass.</span></span> <span data-ttu-id="19615-402">L'intervallo e l'offset temporale con cui questa operazione viene eseguita sono configurabili nelle proprietà.</span><span class="sxs-lookup"><span data-stu-id="19615-402">The interval and the time offset with which this happens is configurable in the properties.</span></span>

![Proprietà di Video Frame Gate](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-video-frame-gate-properties.png)

<span data-ttu-id="19615-404">*Proprietà di Video Frame Gate*</span><span class="sxs-lookup"><span data-stu-id="19615-404">*Video Frame Gate properties*</span></span>

<span data-ttu-id="19615-405">Verrà ora creata un'anteprima ogni minuto impostando la modalità su Time (seconds) e l'intervallo su 60.</span><span class="sxs-lookup"><span data-stu-id="19615-405">Let's create a thumbnail every minute by setting the mode to Time (seconds) and the Interval to 60.</span></span>

### <span data-ttu-id="19615-406"><a id="thumbnails_to__multibitrate_MP4_color_space"></a>Gestione della conversione dello spazio colore</span><span class="sxs-lookup"><span data-stu-id="19615-406"><a id="thumbnails_to__multibitrate_MP4_color_space"></a>Dealing with Color Space conversion</span></span>
<span data-ttu-id="19615-407">Anche se a questo punto può sembrare logico connettere entrambi i pin Uncompressed Video dell'attività di controllo dei fotogrammi e di Media File Input, se si esegue l'operazione viene visualizzato un avviso.</span><span class="sxs-lookup"><span data-stu-id="19615-407">While it would seem logical both Uncompressed Video pins of the frame gate and the Media File Input can now be connected, we would get a warning if we would do so.</span></span>

![Errore relativo allo spazio color di input](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-input-color-space-error.png)

<span data-ttu-id="19615-409">*Errore relativo allo spazio color di input*</span><span class="sxs-lookup"><span data-stu-id="19615-409">*Input color space error*</span></span>

<span data-ttu-id="19615-410">Infatti il modo in cui le informazioni sui colori sono rappresentate nel flusso video non compresso e non elaborato originale, proveniente dal file MXF, è diverso da quello previsto per il codificatore JPG.</span><span class="sxs-lookup"><span data-stu-id="19615-410">This is because the way in which colour information is represented in our original raw uncompressed video stream, coming from our MXF, is different from what the JPG Encoder is expecting.</span></span> <span data-ttu-id="19615-411">In particolare, è previsto il flusso di un cosiddetto "spazio colore" "RGB" o "gradazioni di grigio".</span><span class="sxs-lookup"><span data-stu-id="19615-411">More specifically, a so-called "color space" of "RGB" or "Grayscale" is expected to flow in.</span></span> <span data-ttu-id="19615-412">Al flusso video in entrata di Video Frame Gate dovrà quindi essere prima applicata una conversione relativa allo spazio colore.</span><span class="sxs-lookup"><span data-stu-id="19615-412">This means that the Video Frame Gate's inbound video stream will need to have a conversion applied regarding its color space first.</span></span>

<span data-ttu-id="19615-413">Trascinare nel flusso di lavoro Color Space Converter - Intel e connetterlo all'attività di controllo dei fotogrammi.</span><span class="sxs-lookup"><span data-stu-id="19615-413">Drag onto the workflow the Color Space Converter - Intel and connect it to our frame gate.</span></span>

![Connessione di un convertitore dello spazio colore](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-color-space-convertor.png)

<span data-ttu-id="19615-415">*Connessione di un convertitore dello spazio colore*</span><span class="sxs-lookup"><span data-stu-id="19615-415">*Connecting a Color Space Convertor*</span></span>

<span data-ttu-id="19615-416">Nella finestra delle proprietà selezionare la voce BGR 24 nell'elenco Preset.</span><span class="sxs-lookup"><span data-stu-id="19615-416">In the properties window, pick the BGR 24 entry from the Preset list.</span></span>

### <span data-ttu-id="19615-417"><a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>Scrittura delle anteprime</span><span class="sxs-lookup"><span data-stu-id="19615-417"><a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>Writing the thumbnails</span></span>
<span data-ttu-id="19615-418">Diversamente dai video MP4, il componente JPG Encoder genererà più di un file.</span><span class="sxs-lookup"><span data-stu-id="19615-418">Different from our MP4 video's, the JPG Encoder component will output more than one file.</span></span> <span data-ttu-id="19615-419">Per gestire i file, è possibile usare un componente Scene Search JPG File Writer, che accetterà le anteprime JPG in ingresso e le trascriverà, con un numero diverso come suffisso per ogni nome file.</span><span class="sxs-lookup"><span data-stu-id="19615-419">In order to deal with this, a Scene Search JPG File Writer component can be used: it will take the incoming JPG thumbnails and write them out, each filename being suffixed by a different number.</span></span> <span data-ttu-id="19615-420">Il numero indica in genere il numero di secondi/unità nel flusso da cui l'anteprima è stata disegnata.</span><span class="sxs-lookup"><span data-stu-id="19615-420">(The number typically indicating the number of seconds/units in the stream which the thumbnail was drawn from.)</span></span>

![Introduzione di Scene Search JPG File Writer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer.png)

<span data-ttu-id="19615-422">*Introduzione di Scene Search JPG File Writer*</span><span class="sxs-lookup"><span data-stu-id="19615-422">*Introducing the Scene Search JPG File Writer*</span></span>

<span data-ttu-id="19615-423">Configurare la proprietà Output Folder Path con l'espressione: ${ROOT_outputWriteDirectory}</span><span class="sxs-lookup"><span data-stu-id="19615-423">Configure the Output Folder Path property with the expression: ${ROOT_outputWriteDirectory}</span></span>

<span data-ttu-id="19615-424">e la proprietà Filename Prefix con:</span><span class="sxs-lookup"><span data-stu-id="19615-424">and the Filename Prefix property with:</span></span>

    ${ROOT_sourceFileBaseName}_thumb_

<span data-ttu-id="19615-425">Il prefisso determinerà come vengono denominati i file delle anteprime.</span><span class="sxs-lookup"><span data-stu-id="19615-425">The prefix will determine how the thumbnail files are being named.</span></span> <span data-ttu-id="19615-426">Come suffisso verrà usato un numero indicante la posizione dell'anteprima nel flusso.</span><span class="sxs-lookup"><span data-stu-id="19615-426">They will be suffixed with a number indicating the thumb's position in the stream.</span></span>

![Proprietà di Scene Search JPG File Writer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer-properties.png)

<span data-ttu-id="19615-428">*Proprietà di Scene Search JPG File Writer*</span><span class="sxs-lookup"><span data-stu-id="19615-428">*Scene Search JPG File Writer properties*</span></span>

<span data-ttu-id="19615-429">Connettere Scene Search JPG File Writer al nodo Output File/Asset.</span><span class="sxs-lookup"><span data-stu-id="19615-429">Connect the Scene Search JPG File Writer to the Output File/Asset node.</span></span>

### <span data-ttu-id="19615-430"><a id="thumbnails_to__multibitrate_MP4_errors"></a>Rilevamento di errori in un flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="19615-430"><a id="thumbnails_to__multibitrate_MP4_errors"></a>Detecting errors in a workflow</span></span>
<span data-ttu-id="19615-431">Connettere l'input di Color Space Converter nell'output video non compresso non elaborato.</span><span class="sxs-lookup"><span data-stu-id="19615-431">Connect the input of the color space converter to the raw uncompressed video output.</span></span> <span data-ttu-id="19615-432">Ora effettuare un'esecuzione di test locale per il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="19615-432">Now perform a local test run for the workflow.</span></span> <span data-ttu-id="19615-433">È probabile che l'esecuzione del flusso di lavoro venga arrestata improvvisamente e il componente in cui si è verificato un errore venga indicato con un bordo rosso:</span><span class="sxs-lookup"><span data-stu-id="19615-433">There's a good chance the workflow will suddenly stop executing and indicate with a red outline on the component that encountered an error:</span></span>

![Errore di Color Space Converter](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error.png)

<span data-ttu-id="19615-435">*Errore di Color Space Converter*</span><span class="sxs-lookup"><span data-stu-id="19615-435">*Color Space Converter error*</span></span>

<span data-ttu-id="19615-436">Fare clic sull'icona con la "E" rossa nell'angolo in alto a destra del componente Color Space Converter per visualizzare il motivo per cui il tentativo di codifica non è riuscito.</span><span class="sxs-lookup"><span data-stu-id="19615-436">Click the little red "E" icon in the top right corner of the Color Space Converter component to see what's the reason the encoding attempt failed.</span></span>

![Finestra di dialogo dell'errore di Color Space Converter](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error-dialog.png)

<span data-ttu-id="19615-438">*Finestra di dialogo dell'errore di Color Space Converter*</span><span class="sxs-lookup"><span data-stu-id="19615-438">*Color Space Converter error dialog*</span></span>

<span data-ttu-id="19615-439">Come si può notare, lo standard dello spazio colore in entrata per Color Space Converter deve essere rec601 per la conversione richiesta di YUV in RGB.</span><span class="sxs-lookup"><span data-stu-id="19615-439">It turns out, as you can see, that the incoming color space standard for the color space converter has to be rec601 for our requested conversion of YUV to RGB.</span></span> <span data-ttu-id="19615-440">Sembra che il flusso non indichi rec601.</span><span class="sxs-lookup"><span data-stu-id="19615-440">Apparently our stream doesn't indicate it's rec601.</span></span> <span data-ttu-id="19615-441">Rec 601 è uno standard per la codifica dei segnali video analogici interlacciati nel formato video digitale.</span><span class="sxs-lookup"><span data-stu-id="19615-441">(Rec 601 is a standard for encoding interlaced analog video signals in digital video form.</span></span> <span data-ttu-id="19615-442">Specifica un'area attiva che copre 720 campioni di luminanza e 360 campioni di crominanza per linea.</span><span class="sxs-lookup"><span data-stu-id="19615-442">It specifies an active region covering 720 luminance samples and 360 chrominance samples per line.</span></span> <span data-ttu-id="19615-443">Il sistema di codifica dei colori è noto come YCbCr 4:2:2.</span><span class="sxs-lookup"><span data-stu-id="19615-443">The color encoding system is known as YCbCr 4:2:2.)</span></span>

<span data-ttu-id="19615-444">Per risolvere il problema, si indicherà nei metadati del flusso che si sta usando contenuto rec601.</span><span class="sxs-lookup"><span data-stu-id="19615-444">To fix this, we'll indicate on the metadata of our stream that we're dealing with rec601 content.</span></span> <span data-ttu-id="19615-445">A questo scopo, verrà usato un componente Video Data Type Updater, che verrà inserito tra l'origine non elaborata e il componente di conversione dello spazio colore.</span><span class="sxs-lookup"><span data-stu-id="19615-445">To do so we'll use a Video Data Type Updater component, which we'll put in between our raw source and the color space conversion component.</span></span> <span data-ttu-id="19615-446">Questo strumento di aggiornamento del tipo di dati consente l'aggiornamento manuale di alcune proprietà del tipo di dati video.</span><span class="sxs-lookup"><span data-stu-id="19615-446">This data type updater allows for the manual update of certain video data type properties.</span></span> <span data-ttu-id="19615-447">Configurarlo in modo che Color Space Standard indichi "Rec 601".</span><span class="sxs-lookup"><span data-stu-id="19615-447">Configure it to indicate a Color Space Standard of "Rec 601".</span></span> <span data-ttu-id="19615-448">In questo modo Video Data Type Updater contrassegnerà il flusso con lo spazio colore "Rec 601" se non è ancora stato definito alcuno spazio colore.</span><span class="sxs-lookup"><span data-stu-id="19615-448">This will cause the Video Data Type Updater to tag the stream with the "Rec 601" color space if there was no color space defined yet.</span></span> <span data-ttu-id="19615-449">Eseguirà l'override dei metadati esistenti, solo se è stata selezionata la casella di controllo Override.</span><span class="sxs-lookup"><span data-stu-id="19615-449">(It will not override any existing metadata, unless the Override checkbox was checked.)</span></span>

![Aggiornamento di Color Space Standard in Data Type Updater](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-update-color-space-standard-on-data-type.png)

<span data-ttu-id="19615-451">*Aggiornamento di Color Space Standard in Data Type Updater*</span><span class="sxs-lookup"><span data-stu-id="19615-451">*Updating Color Space Standard on the Data Type Updater*</span></span>

### <span data-ttu-id="19615-452"><a id="thumbnails_to__multibitrate_MP4_finish"></a>Flusso di lavoro completato</span><span class="sxs-lookup"><span data-stu-id="19615-452"><a id="thumbnails_to__multibitrate_MP4_finish"></a>Finished Workflow</span></span>
<span data-ttu-id="19615-453">Ora che il flusso di lavoro è stato completato, effettuare un'altra esecuzione di test per assicurarsi che vengano superati.</span><span class="sxs-lookup"><span data-stu-id="19615-453">Now that our our workflow is finished, do another test run to see it pass.</span></span>

![Flusso di lavoro completato per l'output di più MP4 con anteprime](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-for-multi-mp4-thumbnails.png)

<span data-ttu-id="19615-455">*Flusso di lavoro completato per l'output di più MP4 con anteprime*</span><span class="sxs-lookup"><span data-stu-id="19615-455">*Finished workflow for multi-mp4 output with thumbnails*</span></span>

## <span data-ttu-id="19615-456"><a id="time_based_trim"></a>Taglio basato sull'ora dell'output MP4 a velocità in bit multipla</span><span class="sxs-lookup"><span data-stu-id="19615-456"><a id="time_based_trim"></a>Time-based trimming of multibitrate MP4 output</span></span>
<span data-ttu-id="19615-457">Partendo da un flusso di lavoro che genera [un output MP4 a velocità in bit multipla da un input MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), verrà ora esaminato il taglio del video di origine basato su timestamp.</span><span class="sxs-lookup"><span data-stu-id="19615-457">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into trimming the source video based on time-stamps.</span></span>

### <span data-ttu-id="19615-458"><a id="time_based_trim_start"></a>Panoramica del flusso di lavoro a cui iniziare ad aggiungere il taglio</span><span class="sxs-lookup"><span data-stu-id="19615-458"><a id="time_based_trim_start"></a>Workflow overview to start adding trimming to</span></span>
![Flusso di lavoro iniziale a cui aggiungere il taglio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow-to-add-trimming.png)

<span data-ttu-id="19615-460">*Flusso di lavoro iniziale a cui aggiungere il taglio*</span><span class="sxs-lookup"><span data-stu-id="19615-460">*Starting workflow to add trimming to*</span></span>

### <span data-ttu-id="19615-461"><a id="time_based_trim_use_stream_trimmer"></a>Uso di Stream Trimmer</span><span class="sxs-lookup"><span data-stu-id="19615-461"><a id="time_based_trim_use_stream_trimmer"></a>Using the Stream Trimmer</span></span>
<span data-ttu-id="19615-462">Il componente Stream Trimmer consente anche di tagliare l'inizio e la fine di un flusso di input in base alle informazioni sugli intervalli (secondi, minuti...). Il trimmer non supporta il taglio basato su fotogramma.</span><span class="sxs-lookup"><span data-stu-id="19615-462">The Stream Trimmer component allows to trim the beginning and ending of an input stream base on timing information (seconds, minutes, ...). The trimmer does not support frame-based trimming.</span></span>

![Stream Trimmer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-stream-trimmer.png)

<span data-ttu-id="19615-464">*Stream Trimmer*</span><span class="sxs-lookup"><span data-stu-id="19615-464">*Stream Trimmer*</span></span>

<span data-ttu-id="19615-465">Invece di collegare direttamente i codificatori AVC e Speaker Position Assigner a Media File Input, tra di essi verrà inserito Stream Trimmer</span><span class="sxs-lookup"><span data-stu-id="19615-465">Instead of linking the AVC encoders and speaker position assigner to the Media File Input directly, we'll put in between those the stream trimmer.</span></span> <span data-ttu-id="19615-466">(uno per il segnale video e uno per il segnale audio con interleave).</span><span class="sxs-lookup"><span data-stu-id="19615-466">(One for the video signal and one for the interleaved audio signal.)</span></span>

![Inserire Stream Trimmer in mezzo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-put-stream-trimmer-in-between.png)

<span data-ttu-id="19615-468">*Inserire Stream Trimmer in mezzo*</span><span class="sxs-lookup"><span data-stu-id="19615-468">*Put Stream Trimmer in between*</span></span>

<span data-ttu-id="19615-469">Ora il trimmer verrà configurato per poter elaborare solo il video e l'audio tra 15 secondi e 60 secondi nel video.</span><span class="sxs-lookup"><span data-stu-id="19615-469">Let's configure the trimmer so that we will only process video and audio between 15 seconds and 60 seconds in the video.</span></span>

<span data-ttu-id="19615-470">Andare alle proprietà di Video Stream Trimmer e configurare entrambe le proprietà Start Time (15 secondi) ed End Time (60 secondi).</span><span class="sxs-lookup"><span data-stu-id="19615-470">Go to the properties of the Video Stream Trimmer and configure both Start Time (15s) and End Time (60s) properties.</span></span> <span data-ttu-id="19615-471">Entrambi i trimmer audio e video verranno pubblicati nella radice del flusso di lavoro per verificare che siano sempre configurati sugli stessi valori di inizio e di fine.</span><span class="sxs-lookup"><span data-stu-id="19615-471">To make sure both our audio and video trimmer are always configured to the same start and end values, we will publish those to the root of the workflow.</span></span>

![Pubblicare la proprietà Start Time da Stream Trimmer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-start-time-from-stream-trimmer.png)

<span data-ttu-id="19615-473">*Pubblicare la proprietà Start Time da Stream Trimmer*</span><span class="sxs-lookup"><span data-stu-id="19615-473">*Publish start time property from Stream Trimmer*</span></span>

![Finestra di dialogo Publish Property per Start Time](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-start-time.png)

<span data-ttu-id="19615-475">*Finestra di dialogo Publish Property per Start Time*</span><span class="sxs-lookup"><span data-stu-id="19615-475">*Publish property dialog for start time*</span></span>

![Finestra di dialogo Publish Property per End Time](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-end-time.png)

<span data-ttu-id="19615-477">*Finestra di dialogo Publish Property per End Time*</span><span class="sxs-lookup"><span data-stu-id="19615-477">*Publish property dialog for end time*</span></span>

<span data-ttu-id="19615-478">Se ora si osserva la radice del flusso di lavoro, si noterà che entrambe le proprietà sono ben visualizzate e configurabili direttamente.</span><span class="sxs-lookup"><span data-stu-id="19615-478">If we now inspect the root of our workflow, both properties will be neatly displayed and configurable from there.</span></span>

![Proprietà pubblicate disponibili nella radice](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-properties-available-on-root.png)

<span data-ttu-id="19615-480">*Proprietà pubblicate disponibili nella radice*</span><span class="sxs-lookup"><span data-stu-id="19615-480">*Published properties available on root*</span></span>

<span data-ttu-id="19615-481">Aprire ora le proprietà di taglio dal trimmer audio e configurare sia l'ora di inizio che quella di fine con un'espressione che faccia riferimento alle proprietà pubblicate nella radice del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="19615-481">Now open the trimming properties from the audio trimmer and configure both start and end times with an expression that refers to the published properties on the root of our workflow.</span></span>

<span data-ttu-id="19615-482">Per l'ora di inizio del taglio dell'audio:</span><span class="sxs-lookup"><span data-stu-id="19615-482">For the audio trimming start time:</span></span>

    ${ROOT_TrimmingStartTime}

<span data-ttu-id="19615-483">e per l'ora di fine:</span><span class="sxs-lookup"><span data-stu-id="19615-483">and for its end time:</span></span>

    ${ROOT_TrimmingEndTime}

### <span data-ttu-id="19615-484"><a id="time_based_trim_finish"></a>Flusso di lavoro completato</span><span class="sxs-lookup"><span data-stu-id="19615-484"><a id="time_based_trim_finish"></a>Finished Workflow</span></span>
![Flusso di lavoro completato](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-time-base-trimming.png)

<span data-ttu-id="19615-486">*Flusso di lavoro completato*</span><span class="sxs-lookup"><span data-stu-id="19615-486">*Finished Workflow*</span></span>

## <span data-ttu-id="19615-487"><a id="scripting"></a>Introduzione al componente con script</span><span class="sxs-lookup"><span data-stu-id="19615-487"><a id="scripting"></a>Introducing the Scripted Component</span></span>
<span data-ttu-id="19615-488">I componenti con script possono eseguire script arbitrari durante le fasi di esecuzione del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="19615-488">Scripted Components can execute arbitrary scripts during the execution phases of our workflow.</span></span> <span data-ttu-id="19615-489">Possono essere eseguiti quattro diversi script, tutti con caratteristiche specifiche e con la propria posizione nel ciclo di vita del flusso di lavoro:</span><span class="sxs-lookup"><span data-stu-id="19615-489">There are four different scripts that can be executed, each with specific characteristics and their own place in the workflow life-cycle:</span></span>

* <span data-ttu-id="19615-490">**commandScript**</span><span class="sxs-lookup"><span data-stu-id="19615-490">**commandScript**</span></span>
* <span data-ttu-id="19615-491">**realizeScript**</span><span class="sxs-lookup"><span data-stu-id="19615-491">**realizeScript**</span></span>
* <span data-ttu-id="19615-492">**processInputScript**</span><span class="sxs-lookup"><span data-stu-id="19615-492">**processInputScript**</span></span>
* <span data-ttu-id="19615-493">**lifeCycleScript**</span><span class="sxs-lookup"><span data-stu-id="19615-493">**lifeCycleScript**</span></span>

<span data-ttu-id="19615-494">La documentazione del componente con script li illustra più dettagliatamente.</span><span class="sxs-lookup"><span data-stu-id="19615-494">The documentation of the Scripted Component goes in more detail for each of the above.</span></span> <span data-ttu-id="19615-495">Nella [sezione seguente](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), il componente di scripting **realizeScript** viene usato per costruire un file xml con un elenco di clip non appena il flusso di lavoro viene avviato.</span><span class="sxs-lookup"><span data-stu-id="19615-495">In [the following section](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), the **realizeScript** scripting component is used to construct a cliplist xml on the fly when the workflow starts.</span></span> <span data-ttu-id="19615-496">Questo script viene chiamato durante la configurazione del componente, che viene eseguita solo una volta nel ciclo di vita.</span><span class="sxs-lookup"><span data-stu-id="19615-496">This script is called during the component setup, which happens only once in it's lifecycle.</span></span>

### <span data-ttu-id="19615-497"><a id="scripting_hello_world"></a>Scripting in un flusso di lavoro: hello world</span><span class="sxs-lookup"><span data-stu-id="19615-497"><a id="scripting_hello_world"></a>Scripting within a workflow: hello world</span></span>
<span data-ttu-id="19615-498">Trascinare un componente con script sull'area di progettazione e rinominarlo (ad esempio, "SetClipListXML").</span><span class="sxs-lookup"><span data-stu-id="19615-498">Drag a Scripted Component onto the designer surface and rename it (for example, "SetClipListXML").</span></span>

![Aggiunta di un componente con script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

<span data-ttu-id="19615-500">*Aggiunta di un componente con script*</span><span class="sxs-lookup"><span data-stu-id="19615-500">*Adding a Scripted Component*</span></span>

<span data-ttu-id="19615-501">Quando si esaminano le proprietà del componente con script, vengono visualizzati i quattro diversi tipi di script, tutti configurabili in uno script diverso.</span><span class="sxs-lookup"><span data-stu-id="19615-501">When you inspect the properties of the Scripted Component, the four different script types will be shown, each configurable to a different script.</span></span>

![Proprietà del componente con script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

<span data-ttu-id="19615-503">*Proprietà del componente con script*</span><span class="sxs-lookup"><span data-stu-id="19615-503">*Scripted Component properties*</span></span>

<span data-ttu-id="19615-504">Cancellare il contenuto di processInputScript e aprire l'editor per realizeScript.</span><span class="sxs-lookup"><span data-stu-id="19615-504">Clear the processInputScript and open the editor for the realizeScript.</span></span> <span data-ttu-id="19615-505">La configurazione è stata eseguita ed è possibile avviare lo script.</span><span class="sxs-lookup"><span data-stu-id="19615-505">Now we're set up and ready to start scripting.</span></span>

<span data-ttu-id="19615-506">Gli script vengono scritti in Groovy, un linguaggio di scripting compilato in modo dinamico per la piattaforma Java, che mantiene la compatibilità con Java.</span><span class="sxs-lookup"><span data-stu-id="19615-506">Scripts are written in Groovy, a dynamically compiled scripting language for the Java platform that retains compatibility with Java.</span></span> <span data-ttu-id="19615-507">La maggior parte del codice Java è effettivamente codice Groovy valido.</span><span class="sxs-lookup"><span data-stu-id="19615-507">Actually, most Java code is valid Groovy code.</span></span>

<span data-ttu-id="19615-508">Verrà ora scritto un semplice script di Groovy hello world nel contesto di realizeScript.</span><span class="sxs-lookup"><span data-stu-id="19615-508">Let's write a simple hello world groovy script in the context of our realizeScript.</span></span> <span data-ttu-id="19615-509">Immettere nell'editor quanto segue:</span><span class="sxs-lookup"><span data-stu-id="19615-509">Enter the following in the editor:</span></span>

    node.log("hello world");

<span data-ttu-id="19615-510">Ora effettuare un'esecuzione di test locale.</span><span class="sxs-lookup"><span data-stu-id="19615-510">Now execute a local test run.</span></span> <span data-ttu-id="19615-511">Dopo questa esecuzione, esaminare (nella scheda System del componente con script) la proprietà Logs.</span><span class="sxs-lookup"><span data-stu-id="19615-511">After this run, inspect (through the System tab on the Scripted Component) the Logs property.</span></span>

![Output di log hello world](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output.png)

<span data-ttu-id="19615-513">*Output di log hello world*</span><span class="sxs-lookup"><span data-stu-id="19615-513">*Hello world log output*</span></span>

<span data-ttu-id="19615-514">L'oggetto nodo su cui viene chiamato il metodo log, fa riferimento al "nodo" corrente, ovvero al componente in cui si sta creando lo script.</span><span class="sxs-lookup"><span data-stu-id="19615-514">The node object we call the log method on, refers to our current "node" or the component we're scripting within.</span></span> <span data-ttu-id="19615-515">Ogni componente ha di per sé la possibilità di creare l'output dei dati di registrazione, disponibili nella scheda System. In questo caso, viene creato l'output del valore letterale stringa "hello world".</span><span class="sxs-lookup"><span data-stu-id="19615-515">Every component as such has the ability to output logging data, available through the system tab. In this case, we output the string literal "hello world".</span></span> <span data-ttu-id="19615-516">È importante comprendere che questo si rivela un prezioso strumento di debug perché offre informazioni dettagliate sulle operazioni effettivamente eseguite dallo script.</span><span class="sxs-lookup"><span data-stu-id="19615-516">Important to understand here is that this can prove to be an invaluable debugging tool, providing you with insight on what the script is actually doing.</span></span>

<span data-ttu-id="19615-517">Dall'ambiente di scripting è anche possibile accedere alle proprietà degli altri componenti.</span><span class="sxs-lookup"><span data-stu-id="19615-517">From within our scripting environment, we also have access to properties on other components.</span></span> <span data-ttu-id="19615-518">Provare a eseguire quanto segue:</span><span class="sxs-lookup"><span data-stu-id="19615-518">Try this:</span></span>

    //inspect current node:
    def nodepath = node.getNodePath();
    node.log("this node path: " + nodepath);

    //walking up to other nodes:
    def parentnode = node.getParentNode();
    def parentnodepath = parentnode.getNodePath();
    node.log("parent node path: " + parentnodepath);

    //read properties from a node:
    def sourceFileExt = parentnode.getPropertyAsString( "sourceFileExtension", null );
    def sourceFileName = parentnode.getPropertyAsString("sourceFileBaseName", null);
    node.log("source file name with extension " + sourceFileExt + " is: " + sourceFileName);

<span data-ttu-id="19615-519">La finestra dei log visualizzerà quanto segue:</span><span class="sxs-lookup"><span data-stu-id="19615-519">Our log window will show us the following:</span></span>

![Output dei log per l'accesso ai percorsi dei nodi](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output2.png)

<span data-ttu-id="19615-521">*Output dei log per l'accesso ai percorsi dei nodi*</span><span class="sxs-lookup"><span data-stu-id="19615-521">*Log output for accessing node paths*</span></span>

## <span data-ttu-id="19615-522"><a id="frame_based_trim"></a>Taglio basato sul fotogramma dell'output MP4 a velocità in bit multipla</span><span class="sxs-lookup"><span data-stu-id="19615-522"><a id="frame_based_trim"></a>Frame-based trimming of multibitrate MP4 output</span></span>
<span data-ttu-id="19615-523">Partendo da un flusso di lavoro che genera [un output MP4 a velocità in bit multipla da un input MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), verrà ora esaminato il taglio del video di origine basato sui conteggi dei fotogrammi.</span><span class="sxs-lookup"><span data-stu-id="19615-523">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into trimming the source video based on frame counts.</span></span>

### <span data-ttu-id="19615-524"><a id="frame_based_trim_start"></a>Panoramica del progetto a cui iniziare ad aggiungere il taglio</span><span class="sxs-lookup"><span data-stu-id="19615-524"><a id="frame_based_trim_start"></a>Blueprint overview to start adding trimming to</span></span>
![Flusso di lavoro a cui iniziare ad aggiungere il taglio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-workflow-start-adding-trimming-to.png)

<span data-ttu-id="19615-526">*Flusso di lavoro a cui iniziare ad aggiungere il taglio*</span><span class="sxs-lookup"><span data-stu-id="19615-526">*Workflow to start adding trimming to*</span></span>

### <span data-ttu-id="19615-527"><a id="frame_based_trim_clip_list"></a>Uso di Clip List XML</span><span class="sxs-lookup"><span data-stu-id="19615-527"><a id="frame_based_trim_clip_list"></a>Using the Clip List XML</span></span>
<span data-ttu-id="19615-528">In tutte le esercitazioni precedenti sul flusso di lavoro è stato usato il componente Media File Input come origine di input video.</span><span class="sxs-lookup"><span data-stu-id="19615-528">In all previous workflow tutorials, we used the Media File Input component as our video input source.</span></span> <span data-ttu-id="19615-529">Per questo specifico scenario, si userà invece il componente Clip List Source.</span><span class="sxs-lookup"><span data-stu-id="19615-529">For this specific scenario though, we'll be using the Clip List Source component instead.</span></span> <span data-ttu-id="19615-530">Si noti che questo non è il modo migliore di procedere. Usare Clip List Source solo quando è effettivamente necessario (come nel caso seguente, in cui si usano le funzionalità di taglio dell'elenco di clip).</span><span class="sxs-lookup"><span data-stu-id="19615-530">Note that this should not be the preferred way of working; only use the Clip List Source when there's a real reason to do so (like in the below case, where we're making use of the clip list trimming capabilities).</span></span>

<span data-ttu-id="19615-531">Per passare da Media File Input a Clip List Source, trascinare il componente Clip List Source sull'area di progettazione e connettere il pin Clip List XML al nodo Clip List XML di Progettazione flussi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="19615-531">To switch from our Media File Input to the Clip List Source, drag the Clip List Source component onto the design surface and connect the Clip List XML pin to the Clip List XML node of the workflow designer.</span></span> <span data-ttu-id="19615-532">Clip List Source verrà popolato con i pin di output, in base al video di input.</span><span class="sxs-lookup"><span data-stu-id="19615-532">This should populate the Clip List Source with output pins, according to our input video.</span></span> <span data-ttu-id="19615-533">Connettere ora i pin Uncompressed Video e Uncompressed Audio da Clip List Source ai rispettivi codificatori AVC e ad Audio Stream Interleaver.</span><span class="sxs-lookup"><span data-stu-id="19615-533">Now connect the Uncompressed Video and Uncompressed Audio pins from the the Clip List Source to the respective AVC Encoders and Audio Stream Interleaver.</span></span> <span data-ttu-id="19615-534">Ora rimuovere Media File Input.</span><span class="sxs-lookup"><span data-stu-id="19615-534">Now remove the Media File Input.</span></span>

![Sostituire Media File Input con Clip List Source](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-replaced-media-file-with-clip-source.png)

<span data-ttu-id="19615-536">*Sostituire Media File Input con Clip List Source*</span><span class="sxs-lookup"><span data-stu-id="19615-536">*Replaced the Media File Input with the Clip List Source*</span></span>

<span data-ttu-id="19615-537">Il componente Clip List Source accetta "Clip List XML" come input.</span><span class="sxs-lookup"><span data-stu-id="19615-537">The Clip List Source component takes as its input a "Clip List XML".</span></span> <span data-ttu-id="19615-538">Quando si seleziona il file di origine con cui eseguire il test in locale, questo file XML dell'elenco di clip viene automaticamente popolato.</span><span class="sxs-lookup"><span data-stu-id="19615-538">When selecting the source file to test with locally, this clip list xml is auto-populated for you.</span></span>

![Proprietà Clip List XML popolata automaticamente](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-auto-populated-clip-list-xml-property.png)

<span data-ttu-id="19615-540">*Proprietà Clip List XML popolata automaticamente*</span><span class="sxs-lookup"><span data-stu-id="19615-540">*Auto-populated Clip List XML property*</span></span>

<span data-ttu-id="19615-541">Se si osserva meglio il file XML, ecco come appare:</span><span class="sxs-lookup"><span data-stu-id="19615-541">Looking a bit closer to the xml, this is how it looks like:</span></span>

![Finestra di dialogo di modifica dell'elenco di clip](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-edit-clip-list-dialog.png)

<span data-ttu-id="19615-543">*Finestra di dialogo di modifica dell'elenco di clip*</span><span class="sxs-lookup"><span data-stu-id="19615-543">*Edit clip list dialog*</span></span>

<span data-ttu-id="19615-544">Questo, tuttavia, non rispecchia le funzionalità del file XML dell'elenco di clip.</span><span class="sxs-lookup"><span data-stu-id="19615-544">This however does not reflect the capabilities of the clip list xml.</span></span> <span data-ttu-id="19615-545">Una possibilità è quella di aggiungere un elemento "Trim" sia sotto l'origine video che sotto quella audio, in questo modo:</span><span class="sxs-lookup"><span data-stu-id="19615-545">One option we have is to add a "Trim" element under both the video and audio source, like this:</span></span>

![Aggiunta di un elemento trim all'elenco di clip](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-trim-element-to-clip-list.png)

<span data-ttu-id="19615-547">*Aggiunta di un elemento trim all'elenco di clip*</span><span class="sxs-lookup"><span data-stu-id="19615-547">*Adding a trim element to the clip list*</span></span>

<span data-ttu-id="19615-548">Se si modifica il file XML dell'elenco di clip come indicato sopra e si esegue un test locale, si noterà che il video è stato tagliato correttamente tra i 10 e i 20 secondi.</span><span class="sxs-lookup"><span data-stu-id="19615-548">If you modify the clip list xml like this above and perform a local test run, you'll see the video correctly been trimmed between 10 and 20 seconds in the video.</span></span>

<span data-ttu-id="19615-549">Contrariamente a quanto accade quando si effettua un'esecuzione locale, questo stesso file XML dell'elenco di clip non avrà lo stesso effetto se applicato a un flusso di lavoro eseguito in Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="19615-549">Contrary to what happens when you do a local run though, this very same cliplist xml would not have the same effect when applied in a workflow that runs in Azure Media Services.</span></span> <span data-ttu-id="19615-550">Quando Codificatore premium di Azure viene avviato, il file XML dell'elenco di clip viene generato di nuovo ogni volta, in base al file di input assegnato al processo di codifica.</span><span class="sxs-lookup"><span data-stu-id="19615-550">When Azure Premium Encoder starts, the cliplist xml is generated every time again, based on the input file the encoding job was given.</span></span> <span data-ttu-id="19615-551">Quindi verrà purtroppo eseguito l'override delle eventuali modifiche apportate al file XML.</span><span class="sxs-lookup"><span data-stu-id="19615-551">This means that any changes we do on the xml would unfortunately be overridden.</span></span>

<span data-ttu-id="19615-552">Per evitare che il file XML dell'elenco di clip venga cancellato quando viene avviato un processo di codifica, è possibile rigenerarlo subito dopo l'avvio del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="19615-552">To counter the cliplist xml being wiped when an encoding job is started, we can re-generate it on the fly just after the start of our workflow.</span></span> <span data-ttu-id="19615-553">Tali azioni personalizzate possono essere eseguite con un cosiddetto "componente con script".</span><span class="sxs-lookup"><span data-stu-id="19615-553">Such custom actions can be taken through what is called a "Scripted Component".</span></span> <span data-ttu-id="19615-554">Per altre informazioni, vedere [Introduzione al componente con script](media-services-media-encoder-premium-workflow-tutorials.md#scripting).</span><span class="sxs-lookup"><span data-stu-id="19615-554">For more information, see [Introducing the Scripted Component](media-services-media-encoder-premium-workflow-tutorials.md#scripting).</span></span>

<span data-ttu-id="19615-555">Trascinare un componente con script sull'area di progettazione e rinominarlo SetClipListXML.</span><span class="sxs-lookup"><span data-stu-id="19615-555">Drag a Scripted Component onto the designer surface and rename it to "SetClipListXML".</span></span>

![Aggiunta di un componente con script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

<span data-ttu-id="19615-557">*Aggiunta di un componente con script*</span><span class="sxs-lookup"><span data-stu-id="19615-557">*Adding a Scripted Component*</span></span>

<span data-ttu-id="19615-558">Quando si esaminano le proprietà del componente con script, vengono visualizzati i quattro diversi tipi di script, tutti configurabili in uno script diverso.</span><span class="sxs-lookup"><span data-stu-id="19615-558">When you inspect the properties of the Scripted Component, the four different script types will be shown, each configurable to a different script.</span></span>

![Proprietà del componente con script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

<span data-ttu-id="19615-560">*Proprietà del componente con script*</span><span class="sxs-lookup"><span data-stu-id="19615-560">*Scripted Component properties*</span></span>

### <span data-ttu-id="19615-561"><a id="frame_based_trim_modify_clip_list"></a>Modifica dell'elenco di clip da un componente con script</span><span class="sxs-lookup"><span data-stu-id="19615-561"><a id="frame_based_trim_modify_clip_list"></a>Modifying the clip list from a Scripted Component</span></span>
<span data-ttu-id="19615-562">Prima di poter riscrivere il file XML dell'elenco di clip generato durante l'avvio del flusso di lavoro, sarà necessario l'accesso alla proprietà e ai contenuti del file XML.</span><span class="sxs-lookup"><span data-stu-id="19615-562">Before we can re-write the cliplist xml that is generated during workflow startup, we'll need to have access to the cliplist xml property and contents.</span></span> <span data-ttu-id="19615-563">A questo scopo, è possibile usare il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="19615-563">We can do so like this:</span></span>

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: " + clipListXML);

![Elenco di clip in entrata da registrare](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-incoming-clip-list-logged.png)

<span data-ttu-id="19615-565">*Elenco di clip in entrata da registrare*</span><span class="sxs-lookup"><span data-stu-id="19615-565">*Incoming clip list being logged*</span></span>

<span data-ttu-id="19615-566">Prima di tutto è necessario determinare da quale punto a quale punto si vuole tagliare il video.</span><span class="sxs-lookup"><span data-stu-id="19615-566">First we need a way to determine from which point till which point we want to trim the video.</span></span> <span data-ttu-id="19615-567">Per facilitare l'operazione agli utenti del flusso di lavoro meno esperti, pubblicare due proprietà nella radice del grafico.</span><span class="sxs-lookup"><span data-stu-id="19615-567">To make this convenient to the less-technical user of the workflow, publish two properties to the root of the graph.</span></span> <span data-ttu-id="19615-568">A questo scopo, fare clic con il pulsante destro del mouse sull'area di progettazione e scegliere "Add Property":</span><span class="sxs-lookup"><span data-stu-id="19615-568">To do this, right click the designer surface and select "Add Property":</span></span>

* <span data-ttu-id="19615-569">Prima proprietà: "ClippingTimeStart" di tipo: "TIMECODE"</span><span class="sxs-lookup"><span data-stu-id="19615-569">First property: "ClippingTimeStart" of type: "TIMECODE"</span></span>
* <span data-ttu-id="19615-570">Seconda proprietà: "ClippingTimeEnd" di tipo: "TIMECODE"</span><span class="sxs-lookup"><span data-stu-id="19615-570">Second property: "ClippingTimeEnd" of type: "TIMECODE"</span></span>

![Finestra di dialogo Add Property per l'ora di inizio del ritaglio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-start-time.png)

<span data-ttu-id="19615-572">*Finestra di dialogo Add Property per l'ora di inizio del ritaglio*</span><span class="sxs-lookup"><span data-stu-id="19615-572">*Add Property dialog for clipping start time*</span></span>

![Proprietà degli orari di ritaglio pubblicate nella radice del flusso di lavoro](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-time-props.png)

<span data-ttu-id="19615-574">*Proprietà degli orari di ritaglio pubblicate nella radice del flusso di lavoro*</span><span class="sxs-lookup"><span data-stu-id="19615-574">*Published clipping time props on workflow root*</span></span>

<span data-ttu-id="19615-575">Configurare entrambe le proprietà su un valore appropriato:</span><span class="sxs-lookup"><span data-stu-id="19615-575">Configure both properties to a suitable value:</span></span>

![Configurare le proprietà di inizio e di fine del ritaglio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configure-clip-start-end-prop.png)

<span data-ttu-id="19615-577">*Configurare le proprietà di inizio e di fine del ritaglio*</span><span class="sxs-lookup"><span data-stu-id="19615-577">*Configure the clipping start and end properties*</span></span>

<span data-ttu-id="19615-578">Ora dallo script è possibile accedere a entrambe le proprietà, in questo modo:</span><span class="sxs-lookup"><span data-stu-id="19615-578">Now, from within our script, we can access both properties, like this:</span></span>

    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    node.log("clipping start: " + clipstart);
    node.log("clipping end: " + clipend);

![Finestra dei log che mostra l'inizio e la fine del ritaglio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-show-start-end-clip.png)

<span data-ttu-id="19615-580">*Finestra dei log che mostra l'inizio e la fine del ritaglio*</span><span class="sxs-lookup"><span data-stu-id="19615-580">*Log window showing start and end of clipping*</span></span>

<span data-ttu-id="19615-581">Verranno ora analizzate le stringhe del time code in un formato più facile da usare, con una semplice espressione regolare:</span><span class="sxs-lookup"><span data-stu-id="19615-581">Let's parse the timecode strings into a more convenient to use form, using a simple regular expression:</span></span>

    //parse the start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse the end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);
    node.log("framerate end is: " + endframerate);

![Finestra dei log con l'output del time code analizzato](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-output-parsed-timecode.png)

<span data-ttu-id="19615-583">*Finestra dei log con l'output del time code analizzato*</span><span class="sxs-lookup"><span data-stu-id="19615-583">*Log window with output of parsed timecode*</span></span>

<span data-ttu-id="19615-584">Con queste informazioni a disposizione, ora è possibile modificare il file XML dell'elenco di clip per poter rispecchiare le ore di inizio e di fine per il ritaglio accurato dei fotogrammi desiderati del filmato.</span><span class="sxs-lookup"><span data-stu-id="19615-584">With this information at hand, we can now modify the cliplist xml to reflect the start and end times for the desired frame-accurate clipping of the movie.</span></span>

![Codice di script per aggiungere elementi trim](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-trim-elements.png)

<span data-ttu-id="19615-586">*Codice di script per aggiungere elementi trim*</span><span class="sxs-lookup"><span data-stu-id="19615-586">*Script code to add trim elements*</span></span>

<span data-ttu-id="19615-587">Queste modifiche sono state apportate con normali operazioni di manipolazione delle stringhe.</span><span class="sxs-lookup"><span data-stu-id="19615-587">This was done through normal string manipulation operations.</span></span> <span data-ttu-id="19615-588">Il file XML dell'elenco di clip modificato risultante è stato scritto di nuovo nella proprietà clipListXML nella radice del flusso di lavoro con il metodo "setProperty".</span><span class="sxs-lookup"><span data-stu-id="19615-588">The resulting modified clip list xml is written back to the clipListXML property on the workflow root through the "setProperty" method.</span></span> <span data-ttu-id="19615-589">La finestra dei log dopo un'altra esecuzione di test visualizzerà quanto segue:</span><span class="sxs-lookup"><span data-stu-id="19615-589">The log window after another test run would show us the following:</span></span>

![Registrazione dell'elenco di clip risultante](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-result-clip-list.png)

<span data-ttu-id="19615-591">*Registrazione dell'elenco di clip risultante*</span><span class="sxs-lookup"><span data-stu-id="19615-591">*Logging the resulting clip list*</span></span>

<span data-ttu-id="19615-592">Effettuare un'esecuzione di test per visualizzare come i flussi video e audio sono stati tagliati.</span><span class="sxs-lookup"><span data-stu-id="19615-592">Do a test-run to see how the video and audio streams have been clipped.</span></span> <span data-ttu-id="19615-593">Quando si effettueranno altre esecuzioni di test con valori diversi per i punti di taglio, si noterà che tali valori non verranno tenuti in considerazione</span><span class="sxs-lookup"><span data-stu-id="19615-593">As you'll do more than one test-run with different values for the trimming points, you'll notice that those will not be taken into account however!</span></span> <span data-ttu-id="19615-594">perché la finestra di progettazione, diversamente dal runtime di Azure, NON esegue l'override del file XML dell'elenco di clip a ogni esecuzione.</span><span class="sxs-lookup"><span data-stu-id="19615-594">The reason for this is that the designer, unlike the Azure runtime, does NOT override the cliplist xml every run.</span></span> <span data-ttu-id="19615-595">Per questo motivo solo la prima volta che si impostano i punti di entrata e di uscita il file XML viene trasformato, invece tutte le altre volte la clausola guard (if(clipListXML.indexOf("<trim>") == -1)) impedirà al flusso di lavoro di aggiungere un altro elemento trim se ne è già presente uno.</span><span class="sxs-lookup"><span data-stu-id="19615-595">This means that only the very first time you have set the in and out points, will cause the xml to transform, all the other times, our guard clause (if(clipListXML.indexOf("<trim>") == -1)) will prevent the workflow from adding another trim element when there's already one present.</span></span>

<span data-ttu-id="19615-596">Per semplificare il test locale del flusso di lavoro, è consigliabile aggiungere un codice di manutenzione che controlla se è già presente un elemento trim.</span><span class="sxs-lookup"><span data-stu-id="19615-596">To make our workflow convenient to test locally, we best add some house-keeping code that inspects if a trim element was already present.</span></span> <span data-ttu-id="19615-597">In questo caso, è possibile rimuoverlo prima di continuare a modificare il file XML con i nuovi valori.</span><span class="sxs-lookup"><span data-stu-id="19615-597">If so, we can remove it before continuing by modifying the xml with the new values.</span></span> <span data-ttu-id="19615-598">Invece di usare le normali manipolazioni di stringa, è probabilmente più sicuro eseguire questa operazione con l'analisi del modello a oggetti XML effettivo.</span><span class="sxs-lookup"><span data-stu-id="19615-598">Rather than using plain string manipulations, it's probably safer to do this through real xml object model parsing.</span></span>

<span data-ttu-id="19615-599">Prima di poter aggiungere tale codice, è tuttavia necessario aggiungere alcune istruzioni import all'inizio dello script:</span><span class="sxs-lookup"><span data-stu-id="19615-599">Before we can add such code though, we'll need to add a number of import statements at the start of our script first:</span></span>

    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

<span data-ttu-id="19615-600">Ora è possibile aggiungere il codice di pulizia necessario:</span><span class="sxs-lookup"><span data-stu-id="19615-600">After this, we can add the required cleaning code:</span></span>

    //for local testing: delete any pre-existing trim elements from the clip list xml by parsing the xml into a DOM:
    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find the trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements,dom,XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about to delete any existing trim nodes");
     //delete the trim nodes:
    elementsToDelete.each{
        e -> e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize the modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

<span data-ttu-id="19615-601">Questo codice viene inserito esattamente sopra il punto in cui si aggiungono gli elementi trim nel file XML dell'elenco di clip.</span><span class="sxs-lookup"><span data-stu-id="19615-601">This code goes just above the point at which we add the trim elements to the cliplist xml.</span></span>

<span data-ttu-id="19615-602">A questo punto, è possibile eseguire e modificare il flusso di lavoro come si preferisce, applicando ogni volta le modifiche.</span><span class="sxs-lookup"><span data-stu-id="19615-602">At this point, we can run and modify our workflow as much as we want while having the changes applied ever time.</span></span>    

### <span data-ttu-id="19615-603"><a id="frame_based_trim_clippingenabled_prop"></a>Aggiunta di una pratica proprietà ClippingEnabled</span><span class="sxs-lookup"><span data-stu-id="19615-603"><a id="frame_based_trim_clippingenabled_prop"></a>Adding a ClippingEnabled convenience property</span></span>
<span data-ttu-id="19615-604">Poiché non sempre è necessario usare la funzionalità di taglio, il flusso di lavoro verrà completato aggiungendo un pratico flag booleano che indica se si vuole abilitare o meno il taglio/ritaglio.</span><span class="sxs-lookup"><span data-stu-id="19615-604">As you might not always want trimming to happen, let's finish off our workflow by adding a convenient boolean flag that indicates whether or not we want to enable trimming / clipping.</span></span>

<span data-ttu-id="19615-605">Come prima, pubblicare nella radice del flusso di lavoro una nuova proprietà denominata "ClippingEnabled" di tipo "BOOLEAN".</span><span class="sxs-lookup"><span data-stu-id="19615-605">Just as before, publish a new property to the root of our workflow called "ClippingEnabled" of type "BOOLEAN".</span></span>

![Pubblicare una proprietà per l'abilitazione del ritaglio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-enable-clip.png)

<span data-ttu-id="19615-607">*Pubblicare una proprietà per l'abilitazione del ritaglio*</span><span class="sxs-lookup"><span data-stu-id="19615-607">*Published a property for enabling clipping*</span></span>

<span data-ttu-id="19615-608">Con la semplice clausola guard seguente, è possibile controllare se il taglio è necessario e decidere se l'elenco di clip deve essere modificato o meno.</span><span class="sxs-lookup"><span data-stu-id="19615-608">With the below simple guard clause, we can check if trimming is required and decide if our clip list as such needs to be modified or not.</span></span>

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }


### <span data-ttu-id="19615-609"><a id="code"></a>Codice completo</span><span class="sxs-lookup"><span data-stu-id="19615-609"><a id="code"></a>Complete code</span></span>
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

    //parse the start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse the end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);

    node.log("framerate end is: " + endframerate);

    //for local testing: delete any pre-existing trim elements
    //from the clip list xml by parsing the xml into a DOM:

    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find the trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements, dom, XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about to delete any existing trim nodes");
    //delete the trim nodes:
    elementsToDelete.each{ e ->
        e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize the modified clip list xml dom into a string:
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

    //add trim elements to cliplist xml
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


## <a name="also-see"></a><span data-ttu-id="19615-610">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="19615-610">Also see</span></span>
[<span data-ttu-id="19615-611">Introduzione alla codifica Premium in Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="19615-611">Introducing Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)

[<span data-ttu-id="19615-612">Come usare la codifica Premium in Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="19615-612">How to Use Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)

[<span data-ttu-id="19615-613">Codifica di contenuti su richiesta con Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="19615-613">Encoding On-Demand Content with Azure Media Service</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)

[<span data-ttu-id="19615-614">Codec e formati del flusso di lavoro Premium del codificatore multimediale</span><span class="sxs-lookup"><span data-stu-id="19615-614">Media Encoder Premium Workflow Formats and Codecs</span></span>](media-services-premium-workflow-encoder-formats.md)

[<span data-ttu-id="19615-615">File del flusso di lavoro di esempio</span><span class="sxs-lookup"><span data-stu-id="19615-615">Sample workflow files</span></span>](http://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows)

[<span data-ttu-id="19615-616">Strumento di esplorazione di Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="19615-616">Azure Media Services Explorer tool</span></span>](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a><span data-ttu-id="19615-617">Percorsi di apprendimento di Media Services</span><span class="sxs-lookup"><span data-stu-id="19615-617">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="19615-618">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="19615-618">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
