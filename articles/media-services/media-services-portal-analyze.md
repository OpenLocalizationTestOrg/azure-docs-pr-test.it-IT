---
title: Analizzare i contenuti multimediali usando il portale di Azure | Microsoft Docs
description: Questo argomento illustra come elaborare i contenuti multimediali con processori di contenuti multimediali (MP) di Analisi Servizi multimediali tramite il portale di Azure.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 22032aef0cc8b7b015503043028873e70c21ee85
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="analyze-your-media-using-the-azure-portal"></a><span data-ttu-id="c0530-103">Analizzare i contenuti multimediali usando il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c0530-103">Analyze your media using the Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="c0530-104">Per completare l'esercitazione, è necessario un account Azure.</span><span class="sxs-lookup"><span data-stu-id="c0530-104">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="c0530-105">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c0530-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

## <a name="overview"></a><span data-ttu-id="c0530-106">Panoramica</span><span class="sxs-lookup"><span data-stu-id="c0530-106">Overview</span></span>
<span data-ttu-id="c0530-107">Analisi Servizi multimediali è una raccolta di componenti per sintesi vocale e visione artificiale, con conformità, sicurezza e copertura globale di livello enterprise, che semplificano alle aziende e alle organizzazioni l'acquisizione di informazioni dettagliate dai file video.</span><span class="sxs-lookup"><span data-stu-id="c0530-107">Azure Media Services Analytics is a collection of speech and vision components (at enterprise scale, compliance, security and global reach) that make it easier for organizations and enterprises to derive actionable insights from their video files.</span></span> <span data-ttu-id="c0530-108">Per una panoramica più dettagliata di Analisi Servizi multimediali, vedere [questo](media-services-analytics-overview.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="c0530-108">For more detailed overview of Azure Media Services Analytics see [this](media-services-analytics-overview.md) topic.</span></span> 

<span data-ttu-id="c0530-109">Questo argomento illustra come elaborare i contenuti multimediali con processori di contenuti multimediali (MP) di Analisi Servizi multimediali tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c0530-109">This topic discusses how to process your media with Media Analytics media processors (MPs) using the Azure portal.</span></span> <span data-ttu-id="c0530-110">I processori di contenuti multimediali di Analisi Servizi multimediali producono file MP4 o JSON.</span><span class="sxs-lookup"><span data-stu-id="c0530-110">Media Analytics MPs produce MP4 files or JSON files.</span></span> <span data-ttu-id="c0530-111">Se un processore di contenuti multimediali produce un file MP4, è possibile scaricare progressivamente il file.</span><span class="sxs-lookup"><span data-stu-id="c0530-111">If a media processor produced an MP4 file, you can progressively download the file.</span></span> <span data-ttu-id="c0530-112">Se un processore di contenuti multimediali produce un file JSON, è possibile scaricare il file dall'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="c0530-112">If a media processor produced a JSON file, you can download the file from the Azure blob storage.</span></span> 

## <a name="choose-an-asset-that-you-want-to-analyze"></a><span data-ttu-id="c0530-113">Scegliere un asset da analizzare</span><span class="sxs-lookup"><span data-stu-id="c0530-113">Choose an asset that you want to analyze</span></span>
1. <span data-ttu-id="c0530-114">Nel [portale di Azure ](https://portal.azure.com/) selezionare l'account Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="c0530-114">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="c0530-115">Nella finestra **Impostazioni** selezionare **Asset**.</span><span class="sxs-lookup"><span data-stu-id="c0530-115">In the **Settings** window, select **Assets**.</span></span>  
   <span data-ttu-id="c0530-116">.</span><span class="sxs-lookup"><span data-stu-id="c0530-116">.</span></span>
    <span data-ttu-id="c0530-117">![Analizzare i video](./media/media-services-portal-analyze/media-services-portal-analyze001.png)</span><span class="sxs-lookup"><span data-stu-id="c0530-117">![Analyze videos](./media/media-services-portal-analyze/media-services-portal-analyze001.png)</span></span>
3. <span data-ttu-id="c0530-118">Selezionare l'asset da analizzare e premere il pulsante **Analizza**.</span><span class="sxs-lookup"><span data-stu-id="c0530-118">Select the asset that you would like to analyze and press the **Analyze** button.</span></span>
   
    ![Analizzare i video](./media/media-services-portal-analyze/media-services-portal-analyze002.png)
4. <span data-ttu-id="c0530-120">Nella finestra **Elabora l'asset di file multimediale con Analisi Servizi multimediali** selezionare il processore.</span><span class="sxs-lookup"><span data-stu-id="c0530-120">In the **Process media asset with  Media Analytics** window, select the processor.</span></span> 
   
    <span data-ttu-id="c0530-121">Il resto dell'articolo spiega i motivi e le modalità per usare ogni processore.</span><span class="sxs-lookup"><span data-stu-id="c0530-121">The rest of the article explains why and how to use each processor.</span></span> 
5. <span data-ttu-id="c0530-122">Premere **Crea** per iniziare un processo.</span><span class="sxs-lookup"><span data-stu-id="c0530-122">Press **Create** to the start a job.</span></span>

## <a name="azure-media-indexer"></a><span data-ttu-id="c0530-123">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="c0530-123">Azure Media Indexer</span></span>
<span data-ttu-id="c0530-124">Il processore di contenuti multimediali **Azure Media Indexer** consente di rendere disponibili per la ricerca file e contenuti multimediali, oltre a generare tracce per i sottotitoli codificati.</span><span class="sxs-lookup"><span data-stu-id="c0530-124">The **Azure Media Indexer** media processor enables you to make media files and content searchable, as well as generate closed captioning tracks.</span></span> <span data-ttu-id="c0530-125">Questa sezione offre alcuni dettagli sulle opzioni che è possibile specificare per questo Management Pack.</span><span class="sxs-lookup"><span data-stu-id="c0530-125">This sections gives some details about options that you can specify for this MP.</span></span>

![Analizzare i video](./media/media-services-portal-analyze/media-services-portal-analyze003.png)

### <a name="language"></a><span data-ttu-id="c0530-127">Linguaggio</span><span class="sxs-lookup"><span data-stu-id="c0530-127">Language</span></span>
<span data-ttu-id="c0530-128">Linguaggio naturale da riconoscere nel file multimediale,</span><span class="sxs-lookup"><span data-stu-id="c0530-128">The natural language to be recognized in the multimedia file.</span></span> <span data-ttu-id="c0530-129">ad esempio l'inglese o lo spagnolo.</span><span class="sxs-lookup"><span data-stu-id="c0530-129">For example, English or Spanish.</span></span> 

### <a name="captions"></a><span data-ttu-id="c0530-130">Sottotitoli</span><span class="sxs-lookup"><span data-stu-id="c0530-130">Captions</span></span>
<span data-ttu-id="c0530-131">È possibile scegliere un formato di sottotitoli che verrà generato dal contenuto.</span><span class="sxs-lookup"><span data-stu-id="c0530-131">You can choose a caption format that will be generated from your content.</span></span> <span data-ttu-id="c0530-132">Un processo di indicizzazione può generare file di sottotitoli codificati nei formati seguenti:</span><span class="sxs-lookup"><span data-stu-id="c0530-132">An indexing job can generate closed caption files in the following formats:</span></span>  

* <span data-ttu-id="c0530-133">**SAMI**</span><span class="sxs-lookup"><span data-stu-id="c0530-133">**SAMI**</span></span>
* <span data-ttu-id="c0530-134">**TTML**</span><span class="sxs-lookup"><span data-stu-id="c0530-134">**TTML**</span></span>
* <span data-ttu-id="c0530-135">**WebVTT**</span><span class="sxs-lookup"><span data-stu-id="c0530-135">**WebVTT**</span></span>

<span data-ttu-id="c0530-136">I file di sottotitoli codificati con questi formati possono essere utili per rendere i file audio e video accessibili alle persone con problemi uditivi.</span><span class="sxs-lookup"><span data-stu-id="c0530-136">Closed Caption (CC) files in these formats can be used to make audio and video files accessible to people with hearing disability.</span></span>

### <a name="aib-file"></a><span data-ttu-id="c0530-137">File aib</span><span class="sxs-lookup"><span data-stu-id="c0530-137">AIB file</span></span>
<span data-ttu-id="c0530-138">Selezionare questa opzione per generare il file Audio Index Blob per l'uso con SQL Server IFilter personalizzato.</span><span class="sxs-lookup"><span data-stu-id="c0530-138">Select this option if you would like to generate the Audio Index Blob file for use with the custom SQL Server IFilter.</span></span> <span data-ttu-id="c0530-139">Per altre informazioni, vedere [questo](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blog.</span><span class="sxs-lookup"><span data-stu-id="c0530-139">For more information, see [this](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blog.</span></span>

### <a name="keywords"></a><span data-ttu-id="c0530-140">Parole chiave</span><span class="sxs-lookup"><span data-stu-id="c0530-140">Keywords</span></span>
<span data-ttu-id="c0530-141">Selezionare questa opzione per generare un file XML di parole chiave.</span><span class="sxs-lookup"><span data-stu-id="c0530-141">Select this option if you would like to generate a keywords XML file.</span></span> <span data-ttu-id="c0530-142">Questo file contiene parole chiave estratte da contenuti vocali, con informazioni sulla frequenza e sull'offset.</span><span class="sxs-lookup"><span data-stu-id="c0530-142">This file contains keywords extracted from the speech content, with frequency and offset information.</span></span>

### <a name="job-name"></a><span data-ttu-id="c0530-143">Nome processo</span><span class="sxs-lookup"><span data-stu-id="c0530-143">Job name</span></span>
<span data-ttu-id="c0530-144">Nome descrittivo che consente di identificare il processo.</span><span class="sxs-lookup"><span data-stu-id="c0530-144">A friendly name that lets you identify the job.</span></span> <span data-ttu-id="c0530-145">[Questo](media-services-portal-check-job-progress.md) articolo descrive come è possibile monitorare lo stato di avanzamento di un processo.</span><span class="sxs-lookup"><span data-stu-id="c0530-145">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="c0530-146">File di output</span><span class="sxs-lookup"><span data-stu-id="c0530-146">Output file</span></span>
<span data-ttu-id="c0530-147">Nome descrittivo che consente di identificare il contenuto di output.</span><span class="sxs-lookup"><span data-stu-id="c0530-147">A friendly name that lets you identify the output content.</span></span> 

## <a name="azure-media-hyperlapse"></a><span data-ttu-id="c0530-148">Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="c0530-148">Azure Media Hyperlapse</span></span>
<span data-ttu-id="c0530-149">Azure Media Hyperlapse è un processore multimediale che crea fluidi video in time-lapse da contenuti registrati in prima persona o da fotocamere d'azione.</span><span class="sxs-lookup"><span data-stu-id="c0530-149">Azure Media Hyperlapse is an MP that creates smooth time-lapsed videos from first-person or action-camera content.</span></span>  <span data-ttu-id="c0530-150">Per altre informazioni, vedere [questo](media-services-hyperlapse-content.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="c0530-150">For more information, see [this](media-services-hyperlapse-content.md) topic.</span></span> <span data-ttu-id="c0530-151">Questa sezione offre alcuni dettagli sulle opzioni che è possibile specificare per questo Management Pack.</span><span class="sxs-lookup"><span data-stu-id="c0530-151">This sections gives some details about options that you can specify for this MP.</span></span>

![Analizzare i video](./media/media-services-portal-analyze/media-services-portal-analyze004.png)

### <a name="speed"></a><span data-ttu-id="c0530-153">Velocità</span><span class="sxs-lookup"><span data-stu-id="c0530-153">Speed</span></span>
<span data-ttu-id="c0530-154">Specificare la velocità di riproduzione del video di input.</span><span class="sxs-lookup"><span data-stu-id="c0530-154">Specify the speed with which to speed up the input video.</span></span> <span data-ttu-id="c0530-155">L'output è costituito da un rendering stabilizzato e in time-lapse del video di input.</span><span class="sxs-lookup"><span data-stu-id="c0530-155">The output is a stabilized and time-lapsed rendition of the input video.</span></span>

### <a name="job-name"></a><span data-ttu-id="c0530-156">Nome processo</span><span class="sxs-lookup"><span data-stu-id="c0530-156">Job name</span></span>
<span data-ttu-id="c0530-157">Nome descrittivo che consente di identificare il processo.</span><span class="sxs-lookup"><span data-stu-id="c0530-157">A friendly name that lets you identify the job.</span></span> <span data-ttu-id="c0530-158">[Questo](media-services-portal-check-job-progress.md) articolo descrive come è possibile monitorare lo stato di avanzamento di un processo.</span><span class="sxs-lookup"><span data-stu-id="c0530-158">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="c0530-159">File di output</span><span class="sxs-lookup"><span data-stu-id="c0530-159">Output file</span></span>
<span data-ttu-id="c0530-160">Nome descrittivo che consente di identificare il contenuto di output.</span><span class="sxs-lookup"><span data-stu-id="c0530-160">A friendly name that lets you identify the output content.</span></span> 

## <a name="azure-media-face-detector"></a><span data-ttu-id="c0530-161">Rilevamento multimediale volti di Azure</span><span class="sxs-lookup"><span data-stu-id="c0530-161">Azure Media Face Detector</span></span>
<span data-ttu-id="c0530-162">Il processore di contenuti multimediali **Rilevamento multimediale volti di Azure** consente di contare, monitorare i movimenti e persino di valutare la partecipazione e le reazioni del pubblico in base alle espressioni del volto.</span><span class="sxs-lookup"><span data-stu-id="c0530-162">The **Azure Media Face Detector** media processor (MP) enables you to count, track movements, and even gauge audience participation and reaction via facial expressions.</span></span> <span data-ttu-id="c0530-163">Questo servizio contiene due funzionalità:</span><span class="sxs-lookup"><span data-stu-id="c0530-163">This service contains two features:</span></span> 

* <span data-ttu-id="c0530-164">**Rilevamento volti**</span><span class="sxs-lookup"><span data-stu-id="c0530-164">**Face detection**</span></span>
  
    <span data-ttu-id="c0530-165">Il Rilevamento volti rileva e monitora i volti umani all'interno di un video.</span><span class="sxs-lookup"><span data-stu-id="c0530-165">Face detection finds and tracks human faces within a video.</span></span> <span data-ttu-id="c0530-166">È possibile rilevare e monitorare diversi volti mentre le persone si muovono; i metadati relativi a ora e luogo vengono restituiti in un file JSON.</span><span class="sxs-lookup"><span data-stu-id="c0530-166">Multiple faces can be detected and subsequently be tracked as they move around, with the time and location metadata returned in a JSON file.</span></span> <span data-ttu-id="c0530-167">Durante il monitoraggio, il sistema tenterà di assegnare sempre lo stesso ID al volto mentre la persona si muove sullo schermo, anche se è nascosta o se esce brevemente dall'inquadratura.</span><span class="sxs-lookup"><span data-stu-id="c0530-167">During tracking, it will attempt to give a consistent ID to the same face while the person is moving around on screen, even if they are obstructed or briefly leave the frame.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="c0530-168">Questo servizio non esegue il riconoscimento facciale.</span><span class="sxs-lookup"><span data-stu-id="c0530-168">This services does not perform facial recognition.</span></span> <span data-ttu-id="c0530-169">Se una persona esce dall'inquadratura o viene nascosta troppo a lungo, al suo ritorno le verrà assegnato un nuovo ID.</span><span class="sxs-lookup"><span data-stu-id="c0530-169">An individual who leaves the frame or becomes obstructed for too long will be given a new ID when they return.</span></span>
  > 
  > 
* <span data-ttu-id="c0530-170">**Rilevamento emozioni**</span><span class="sxs-lookup"><span data-stu-id="c0530-170">**Emotion detection**</span></span>
  
    <span data-ttu-id="c0530-171">Il Rilevamento emozioni è un componente facoltativo del Processore multimediale di rilevamento volti che restituisce un'analisi di vari attributi emotivi dei volti rilevati, inclusi la felicità, la paura, la tristezza, la rabbia e altre emozioni.</span><span class="sxs-lookup"><span data-stu-id="c0530-171">Emotion Detection is an optional component of the Face Detection Media Processor that returns analysis on multiple emotional attributes from the faces detected, including happiness, sadness, fear, anger, and more.</span></span> 

![Analizzare i video](./media/media-services-portal-analyze/media-services-portal-analyze005.png)

### <a name="detection-mode"></a><span data-ttu-id="c0530-173">Modalità di rilevamento</span><span class="sxs-lookup"><span data-stu-id="c0530-173">Detection mode</span></span>
<span data-ttu-id="c0530-174">Il processore può usare una delle modalità seguenti:</span><span class="sxs-lookup"><span data-stu-id="c0530-174">One of the following modes can be used by the processor:</span></span>

* <span data-ttu-id="c0530-175">rilevamento volti</span><span class="sxs-lookup"><span data-stu-id="c0530-175">face detection</span></span>
* <span data-ttu-id="c0530-176">rilevamento emozioni per volto</span><span class="sxs-lookup"><span data-stu-id="c0530-176">per face emotion detection</span></span>
* <span data-ttu-id="c0530-177">rilevamento emozioni aggregato</span><span class="sxs-lookup"><span data-stu-id="c0530-177">aggregate emotion detection</span></span>

### <a name="job-name"></a><span data-ttu-id="c0530-178">Nome processo</span><span class="sxs-lookup"><span data-stu-id="c0530-178">Job name</span></span>
<span data-ttu-id="c0530-179">Nome descrittivo che consente di identificare il processo.</span><span class="sxs-lookup"><span data-stu-id="c0530-179">A friendly name that lets you identify the job.</span></span> <span data-ttu-id="c0530-180">[Questo](media-services-portal-check-job-progress.md) articolo descrive come è possibile monitorare lo stato di avanzamento di un processo.</span><span class="sxs-lookup"><span data-stu-id="c0530-180">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="c0530-181">File di output</span><span class="sxs-lookup"><span data-stu-id="c0530-181">Output file</span></span>
<span data-ttu-id="c0530-182">Nome descrittivo che consente di identificare il contenuto di output.</span><span class="sxs-lookup"><span data-stu-id="c0530-182">A friendly name that lets you identify the output content.</span></span> 

## <a name="azure-media-motion-detector"></a><span data-ttu-id="c0530-183">Rilevatore multimediale di movimento Azure</span><span class="sxs-lookup"><span data-stu-id="c0530-183">Azure Media Motion Detector</span></span>
<span data-ttu-id="c0530-184">Il processore di contenuti multimediali **Rilevatore multimediale di movimento Azure** consente di identificare in modo efficace le sezioni interessanti all'interno di un video altrimenti lungo e privo di eventi.</span><span class="sxs-lookup"><span data-stu-id="c0530-184">The **Azure Media Motion Detector** media processor (MP) enables you to efficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="c0530-185">Il rilevamento di movimento può essere usato nei filmati statici della videocamera per individuare le sezioni del video in cui si verificano movimenti.</span><span class="sxs-lookup"><span data-stu-id="c0530-185">Motion detection can be used on static camera footage to identify sections of the video where motion occurs.</span></span> <span data-ttu-id="c0530-186">Viene generato un file JSON contenente i metadati con i timestamp e l'area di delimitazione in cui si è verificato l'evento.</span><span class="sxs-lookup"><span data-stu-id="c0530-186">It generates a JSON file containing a metadata with timestamps and the bounding region where the event occurred.</span></span>

<span data-ttu-id="c0530-187">Questa tecnologia, destinata alle trasmissioni video di sicurezza, è in grado di classificare i movimenti in eventi rilevanti e falsi positivi, ad esempio variazioni di luminosità e delle ombre.</span><span class="sxs-lookup"><span data-stu-id="c0530-187">Targeted towards security video feeds, this technology is able to categorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="c0530-188">In questo modo è possibile generare avvisi di sicurezza dalle trasmissioni della videocamera senza che venga segnalata una serie infinita di eventi irrilevanti e al contempo estrarre i momenti di interesse da video di sorveglianza estremamente lunghi.</span><span class="sxs-lookup"><span data-stu-id="c0530-188">This allows you to generate security alerts from camera feeds without being spammed with endless irrelevant events, while being able to extract moments of interest from extremely long surveillance videos.</span></span>

![Analizzare i video](./media/media-services-portal-analyze/media-services-portal-analyze006.png)

## <a name="azure-media-video-thumbnails"></a><span data-ttu-id="c0530-190">Anteprime video multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="c0530-190">Azure Media Video Thumbnails</span></span>
<span data-ttu-id="c0530-191">Questo processore consente di creare un riepilogo per video lunghi selezionando in modo automatico frammenti interessanti del video di origine.</span><span class="sxs-lookup"><span data-stu-id="c0530-191">This processor can help you create summaries of long videos by automatically selecting interesting snippets from the source video.</span></span> <span data-ttu-id="c0530-192">Questa funzione risulta particolarmente utile quando si intende creare una panoramica rapida dei contenuti offerti nella versione più lunga del video.</span><span class="sxs-lookup"><span data-stu-id="c0530-192">This is useful when you want to provide a quick overview of what to expect in a long video.</span></span> <span data-ttu-id="c0530-193">Per informazioni dettagliate ed esempi, vedere [Uso delle anteprime video multimediali di Azure per creare un riepilogo video](media-services-video-summarization.md)</span><span class="sxs-lookup"><span data-stu-id="c0530-193">For detailed information and examples, see [Use Azure Media Video Thumbnails to Create a Video Summarization](media-services-video-summarization.md)</span></span>

![Analizzare i video](./media/media-services-portal-analyze/media-services-portal-analyze008.png)

### <a name="job-name"></a><span data-ttu-id="c0530-195">Nome processo</span><span class="sxs-lookup"><span data-stu-id="c0530-195">Job name</span></span>
<span data-ttu-id="c0530-196">Nome descrittivo che consente di identificare il processo.</span><span class="sxs-lookup"><span data-stu-id="c0530-196">A friendly name that lets you identify the job.</span></span> <span data-ttu-id="c0530-197">[Questo](media-services-portal-check-job-progress.md) articolo descrive come è possibile monitorare lo stato di avanzamento di un processo.</span><span class="sxs-lookup"><span data-stu-id="c0530-197">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="c0530-198">File di output</span><span class="sxs-lookup"><span data-stu-id="c0530-198">Output file</span></span>
<span data-ttu-id="c0530-199">Nome descrittivo che consente di identificare il contenuto di output.</span><span class="sxs-lookup"><span data-stu-id="c0530-199">A friendly name that lets you identify the output content.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c0530-200">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c0530-200">Next steps</span></span>
<span data-ttu-id="c0530-201">Visualizzare i percorsi di apprendimento di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="c0530-201">View Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c0530-202">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="c0530-202">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

