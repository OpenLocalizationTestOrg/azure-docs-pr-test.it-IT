---
title: aaaAnalyze i supporti tramite hello portale di Azure | Documenti Microsoft
description: Questo argomento viene illustrato come tooprocess hello di file multimediali con processori di contenuti multimediali Analitica Media (MP) utilizzando il portale di Azure.
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
ms.openlocfilehash: d549c0315cd58c3771420379316b4f2ad3c2cea6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-media-using-hello-azure-portal"></a><span data-ttu-id="e9c5c-103">Analizzare i file multimediali usando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e9c5c-103">Analyze your media using hello Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="e9c5c-104">toocomplete questa esercitazione, è necessario un account di Azure.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-104">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="e9c5c-105">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e9c5c-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

## <a name="overview"></a><span data-ttu-id="e9c5c-106">Panoramica</span><span class="sxs-lookup"><span data-stu-id="e9c5c-106">Overview</span></span>
<span data-ttu-id="e9c5c-107">Azure Media Services Analitica è una raccolta di riconoscimento vocale e visione componenti (scala enterprise, conformità, sicurezza e portata globale) che rendono più semplice per aziende e organizzazioni tooderive ricavare informazioni utili dai file di video.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-107">Azure Media Services Analytics is a collection of speech and vision components (at enterprise scale, compliance, security and global reach) that make it easier for organizations and enterprises tooderive actionable insights from their video files.</span></span> <span data-ttu-id="e9c5c-108">Per una panoramica più dettagliata di Analisi Servizi multimediali, vedere [questo](media-services-analytics-overview.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-108">For more detailed overview of Azure Media Services Analytics see [this](media-services-analytics-overview.md) topic.</span></span> 

<span data-ttu-id="e9c5c-109">Questo argomento viene illustrato come tooprocess hello di file multimediali con processori di contenuti multimediali Analitica Media (MP) utilizzando il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-109">This topic discusses how tooprocess your media with Media Analytics media processors (MPs) using hello Azure portal.</span></span> <span data-ttu-id="e9c5c-110">I processori di contenuti multimediali di Analisi Servizi multimediali producono file MP4 o JSON.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-110">Media Analytics MPs produce MP4 files or JSON files.</span></span> <span data-ttu-id="e9c5c-111">Se un processore di contenuti multimediali ha prodotto un file MP4, è possibile scaricare progressivamente file hello.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-111">If a media processor produced an MP4 file, you can progressively download hello file.</span></span> <span data-ttu-id="e9c5c-112">Se un processore di contenuti multimediali ha prodotto un file JSON, è possibile scaricare file hello da hello archiviazione blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-112">If a media processor produced a JSON file, you can download hello file from hello Azure blob storage.</span></span> 

## <a name="choose-an-asset-that-you-want-tooanalyze"></a><span data-ttu-id="e9c5c-113">Scegliere una risorsa che si desidera tooanalyze</span><span class="sxs-lookup"><span data-stu-id="e9c5c-113">Choose an asset that you want tooanalyze</span></span>
1. <span data-ttu-id="e9c5c-114">In hello [portale di Azure](https://portal.azure.com/), selezionare l'account di servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-114">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="e9c5c-115">In hello **impostazioni** selezionare **asset**.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-115">In hello **Settings** window, select **Assets**.</span></span>  
   <span data-ttu-id="e9c5c-116">.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-116">.</span></span>
    <span data-ttu-id="e9c5c-117">![Analizzare i video](./media/media-services-portal-analyze/media-services-portal-analyze001.png)</span><span class="sxs-lookup"><span data-stu-id="e9c5c-117">![Analyze videos](./media/media-services-portal-analyze/media-services-portal-analyze001.png)</span></span>
3. <span data-ttu-id="e9c5c-118">Asset selezionare hello che si desidera hello tooanalyze e premere **Analizza** pulsante.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-118">Select hello asset that you would like tooanalyze and press hello **Analyze** button.</span></span>
   
    ![Analizzare i video](./media/media-services-portal-analyze/media-services-portal-analyze002.png)
4. <span data-ttu-id="e9c5c-120">In hello **asset di file multimediali di processo con supporto Analitica** finestra, processore hello selezionare.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-120">In hello **Process media asset with  Media Analytics** window, select hello processor.</span></span> 
   
    <span data-ttu-id="e9c5c-121">il resto di Hello di hello articolo spiega come e perché toouse ogni processore.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-121">hello rest of hello article explains why and how toouse each processor.</span></span> 
5. <span data-ttu-id="e9c5c-122">Premere **crea** toohello avviare un processo.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-122">Press **Create** toohello start a job.</span></span>

## <a name="azure-media-indexer"></a><span data-ttu-id="e9c5c-123">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="e9c5c-123">Azure Media Indexer</span></span>
<span data-ttu-id="e9c5c-124">Hello **Azure Media Indexer** processore di contenuti multimediali consente di file multimediali toomake e ricerca, contenuto, nonché generare tracce sottotitoli codificate chiuse.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-124">hello **Azure Media Indexer** media processor enables you toomake media files and content searchable, as well as generate closed captioning tracks.</span></span> <span data-ttu-id="e9c5c-125">Questa sezione offre alcuni dettagli sulle opzioni che è possibile specificare per questo Management Pack.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-125">This sections gives some details about options that you can specify for this MP.</span></span>

![Analizzare i video](./media/media-services-portal-analyze/media-services-portal-analyze003.png)

### <a name="language"></a><span data-ttu-id="e9c5c-127">Lingua</span><span class="sxs-lookup"><span data-stu-id="e9c5c-127">Language</span></span>
<span data-ttu-id="e9c5c-128">Hello riconosciuto nel file multimediale hello toobe di linguaggio naturale.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-128">hello natural language toobe recognized in hello multimedia file.</span></span> <span data-ttu-id="e9c5c-129">ad esempio l'inglese o lo spagnolo.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-129">For example, English or Spanish.</span></span> 

### <a name="captions"></a><span data-ttu-id="e9c5c-130">Sottotitoli</span><span class="sxs-lookup"><span data-stu-id="e9c5c-130">Captions</span></span>
<span data-ttu-id="e9c5c-131">È possibile scegliere un formato di sottotitoli che verrà generato dal contenuto.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-131">You can choose a caption format that will be generated from your content.</span></span> <span data-ttu-id="e9c5c-132">Un processo di indicizzazione possa generare file di sottotitoli nel hello seguenti formati:</span><span class="sxs-lookup"><span data-stu-id="e9c5c-132">An indexing job can generate closed caption files in hello following formats:</span></span>  

* <span data-ttu-id="e9c5c-133">**SAMI**</span><span class="sxs-lookup"><span data-stu-id="e9c5c-133">**SAMI**</span></span>
* <span data-ttu-id="e9c5c-134">**TTML**</span><span class="sxs-lookup"><span data-stu-id="e9c5c-134">**TTML**</span></span>
* <span data-ttu-id="e9c5c-135">**WebVTT**</span><span class="sxs-lookup"><span data-stu-id="e9c5c-135">**WebVTT**</span></span>

<span data-ttu-id="e9c5c-136">Chiuso i file di didascalia (CC) in questi formati possono essere utilizzati toomake audio e video file toopeople accessibile con problemi uditivi.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-136">Closed Caption (CC) files in these formats can be used toomake audio and video files accessible toopeople with hearing disability.</span></span>

### <a name="aib-file"></a><span data-ttu-id="e9c5c-137">File aib</span><span class="sxs-lookup"><span data-stu-id="e9c5c-137">AIB file</span></span>
<span data-ttu-id="e9c5c-138">Selezionare questa opzione se si sarebbe simile toogenerate hello Audio indice Blob file per l'utilizzo con hello IFilter di Server SQL personalizzata.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-138">Select this option if you would like toogenerate hello Audio Index Blob file for use with hello custom SQL Server IFilter.</span></span> <span data-ttu-id="e9c5c-139">Per altre informazioni, vedere [questo](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blog.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-139">For more information, see [this](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blog.</span></span>

### <a name="keywords"></a><span data-ttu-id="e9c5c-140">Parole chiave</span><span class="sxs-lookup"><span data-stu-id="e9c5c-140">Keywords</span></span>
<span data-ttu-id="e9c5c-141">Selezionare questa opzione se si desidera toogenerate un file XML di parole chiave.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-141">Select this option if you would like toogenerate a keywords XML file.</span></span> <span data-ttu-id="e9c5c-142">Questo file contiene parole chiave estratte da contenuti vocali hello, con la frequenza e informazioni relative all'offset.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-142">This file contains keywords extracted from hello speech content, with frequency and offset information.</span></span>

### <a name="job-name"></a><span data-ttu-id="e9c5c-143">Nome processo</span><span class="sxs-lookup"><span data-stu-id="e9c5c-143">Job name</span></span>
<span data-ttu-id="e9c5c-144">Nome descrittivo che consente di identificare il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-144">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="e9c5c-145">[Questo](media-services-portal-check-job-progress.md) articolo viene descritto come è possibile monitorare lo stato di avanzamento hello di un processo.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-145">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="e9c5c-146">File di output</span><span class="sxs-lookup"><span data-stu-id="e9c5c-146">Output file</span></span>
<span data-ttu-id="e9c5c-147">Nome descrittivo che consente di identificare il contenuto di output di hello.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-147">A friendly name that lets you identify hello output content.</span></span> 

## <a name="azure-media-hyperlapse"></a><span data-ttu-id="e9c5c-148">Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="e9c5c-148">Azure Media Hyperlapse</span></span>
<span data-ttu-id="e9c5c-149">Azure Media Hyperlapse è un processore multimediale che crea fluidi video in time-lapse da contenuti registrati in prima persona o da fotocamere d'azione.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-149">Azure Media Hyperlapse is an MP that creates smooth time-lapsed videos from first-person or action-camera content.</span></span>  <span data-ttu-id="e9c5c-150">Per altre informazioni, vedere [questo](media-services-hyperlapse-content.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-150">For more information, see [this](media-services-hyperlapse-content.md) topic.</span></span> <span data-ttu-id="e9c5c-151">Questa sezione offre alcuni dettagli sulle opzioni che è possibile specificare per questo Management Pack.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-151">This sections gives some details about options that you can specify for this MP.</span></span>

![Analizzare i video](./media/media-services-portal-analyze/media-services-portal-analyze004.png)

### <a name="speed"></a><span data-ttu-id="e9c5c-153">Velocità</span><span class="sxs-lookup"><span data-stu-id="e9c5c-153">Speed</span></span>
<span data-ttu-id="e9c5c-154">Specificare la velocità di hello con cui toospeed i video di input hello.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-154">Specify hello speed with which toospeed up hello input video.</span></span> <span data-ttu-id="e9c5c-155">output di Hello è una copia trasformata stabilizzare e tempo trascorso di video di input hello.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-155">hello output is a stabilized and time-lapsed rendition of hello input video.</span></span>

### <a name="job-name"></a><span data-ttu-id="e9c5c-156">Nome processo</span><span class="sxs-lookup"><span data-stu-id="e9c5c-156">Job name</span></span>
<span data-ttu-id="e9c5c-157">Nome descrittivo che consente di identificare il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-157">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="e9c5c-158">[Questo](media-services-portal-check-job-progress.md) articolo viene descritto come è possibile monitorare lo stato di avanzamento hello di un processo.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-158">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="e9c5c-159">File di output</span><span class="sxs-lookup"><span data-stu-id="e9c5c-159">Output file</span></span>
<span data-ttu-id="e9c5c-160">Nome descrittivo che consente di identificare il contenuto di output di hello.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-160">A friendly name that lets you identify hello output content.</span></span> 

## <a name="azure-media-face-detector"></a><span data-ttu-id="e9c5c-161">Rilevamento multimediale volti di Azure</span><span class="sxs-lookup"><span data-stu-id="e9c5c-161">Azure Media Face Detector</span></span>
<span data-ttu-id="e9c5c-162">Hello **Azure Media faccia Rilevatore** processore di contenuti multimediali (MP) consente di toocount, i movimenti di avanzamento e anche la partecipazione di destinatari misuratore e reazione tramite facciale.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-162">hello **Azure Media Face Detector** media processor (MP) enables you toocount, track movements, and even gauge audience participation and reaction via facial expressions.</span></span> <span data-ttu-id="e9c5c-163">Questo servizio contiene due funzionalità:</span><span class="sxs-lookup"><span data-stu-id="e9c5c-163">This service contains two features:</span></span> 

* <span data-ttu-id="e9c5c-164">**Rilevamento volti**</span><span class="sxs-lookup"><span data-stu-id="e9c5c-164">**Face detection**</span></span>
  
    <span data-ttu-id="e9c5c-165">Il Rilevamento volti rileva e monitora i volti umani all'interno di un video.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-165">Face detection finds and tracks human faces within a video.</span></span> <span data-ttu-id="e9c5c-166">Più caratteri tipografici possono essere rilevati e successivamente essere rilevate man mano che vengono spostati, con hello ora e il percorso dei metadati restituiti in un file JSON.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-166">Multiple faces can be detected and subsequently be tracked as they move around, with hello time and location metadata returned in a JSON file.</span></span> <span data-ttu-id="e9c5c-167">Durante il rilevamento, verrà eseguito un tentativo toogive un toohello ID coerenza stesso faccia mentre persona hello è spostamento sullo schermo, anche se è nascosto o lasciare brevemente il frame di hello.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-167">During tracking, it will attempt toogive a consistent ID toohello same face while hello person is moving around on screen, even if they are obstructed or briefly leave hello frame.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="e9c5c-168">Questo servizio non esegue il riconoscimento facciale.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-168">This services does not perform facial recognition.</span></span> <span data-ttu-id="e9c5c-169">Persona che lascia frame hello o diventa nascosto per troppo tempo verrà assegnato un nuovo ID quando viene restituita.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-169">An individual who leaves hello frame or becomes obstructed for too long will be given a new ID when they return.</span></span>
  > 
  > 
* <span data-ttu-id="e9c5c-170">**Rilevamento emozioni**</span><span class="sxs-lookup"><span data-stu-id="e9c5c-170">**Emotion detection**</span></span>
  
    <span data-ttu-id="e9c5c-171">Rilevamento emozioni è un componente facoltativo di hello processore di contenuti multimediali di rilevamento viso restituisce analisi su più attributi affettivi da facce hello rilevate, tra cui "Happiness", sadness, paura, anger e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-171">Emotion Detection is an optional component of hello Face Detection Media Processor that returns analysis on multiple emotional attributes from hello faces detected, including happiness, sadness, fear, anger, and more.</span></span> 

![Analizzare i video](./media/media-services-portal-analyze/media-services-portal-analyze005.png)

### <a name="detection-mode"></a><span data-ttu-id="e9c5c-173">Modalità di rilevamento</span><span class="sxs-lookup"><span data-stu-id="e9c5c-173">Detection mode</span></span>
<span data-ttu-id="e9c5c-174">Una delle seguenti modalità hello può essere utilizzata da processore hello:</span><span class="sxs-lookup"><span data-stu-id="e9c5c-174">One of hello following modes can be used by hello processor:</span></span>

* <span data-ttu-id="e9c5c-175">rilevamento volti</span><span class="sxs-lookup"><span data-stu-id="e9c5c-175">face detection</span></span>
* <span data-ttu-id="e9c5c-176">rilevamento emozioni per volto</span><span class="sxs-lookup"><span data-stu-id="e9c5c-176">per face emotion detection</span></span>
* <span data-ttu-id="e9c5c-177">rilevamento emozioni aggregato</span><span class="sxs-lookup"><span data-stu-id="e9c5c-177">aggregate emotion detection</span></span>

### <a name="job-name"></a><span data-ttu-id="e9c5c-178">Nome processo</span><span class="sxs-lookup"><span data-stu-id="e9c5c-178">Job name</span></span>
<span data-ttu-id="e9c5c-179">Nome descrittivo che consente di identificare il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-179">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="e9c5c-180">[Questo](media-services-portal-check-job-progress.md) articolo viene descritto come è possibile monitorare lo stato di avanzamento hello di un processo.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-180">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="e9c5c-181">File di output</span><span class="sxs-lookup"><span data-stu-id="e9c5c-181">Output file</span></span>
<span data-ttu-id="e9c5c-182">Nome descrittivo che consente di identificare il contenuto di output di hello.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-182">A friendly name that lets you identify hello output content.</span></span> 

## <a name="azure-media-motion-detector"></a><span data-ttu-id="e9c5c-183">Rilevatore multimediale di movimento Azure</span><span class="sxs-lookup"><span data-stu-id="e9c5c-183">Azure Media Motion Detector</span></span>
<span data-ttu-id="e9c5c-184">Hello **rilevatore di movimento di Azure Media** Abilita processore (MP) supporti tooefficiently si identificano le sezioni di interesse all'interno di un video in caso contrario lungo e procede senza interruzioni.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-184">hello **Azure Media Motion Detector** media processor (MP) enables you tooefficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="e9c5c-185">Rilevamento del movimento utilizzabile in camera statico riprese tooidentify sezioni del video hello in cui viene effettuato lo spostamento.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-185">Motion detection can be used on static camera footage tooidentify sections of hello video where motion occurs.</span></span> <span data-ttu-id="e9c5c-186">Genera un file JSON che contiene i metadati con i timestamp e hello delimitazione area in cui si è verificato l'evento hello.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-186">It generates a JSON file containing a metadata with timestamps and hello bounding region where hello event occurred.</span></span>

<span data-ttu-id="e9c5c-187">Mirata feed video di sicurezza, questa tecnologia è in grado di toocategorize movimento in eventi rilevanti e falsi positivi, ad esempio shadows e modifiche di illuminazione.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-187">Targeted towards security video feeds, this technology is able toocategorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="e9c5c-188">Ciò consente gli avvisi di sicurezza toogenerate dai feed di fotocamera senza viene posta indesiderata con gli eventi non rilevanti infiniti, pur essendo momenti tooextract in grado di interesse da video sorveglianza estremamente lunghi.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-188">This allows you toogenerate security alerts from camera feeds without being spammed with endless irrelevant events, while being able tooextract moments of interest from extremely long surveillance videos.</span></span>

![Analizzare i video](./media/media-services-portal-analyze/media-services-portal-analyze006.png)

## <a name="azure-media-video-thumbnails"></a><span data-ttu-id="e9c5c-190">Anteprime video multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="e9c5c-190">Azure Media Video Thumbnails</span></span>
<span data-ttu-id="e9c5c-191">Questo processore consentono di creare riepiloghi dei video lunghi selezionando automaticamente interessanti frammenti video di origine hello.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-191">This processor can help you create summaries of long videos by automatically selecting interesting snippets from hello source video.</span></span> <span data-ttu-id="e9c5c-192">Ciò è utile quando si desidera tooprovide una rapida panoramica delle quali tooexpect in un video di lunga durata.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-192">This is useful when you want tooprovide a quick overview of what tooexpect in a long video.</span></span> <span data-ttu-id="e9c5c-193">Per informazioni dettagliate ed esempi, vedere [tooCreate Usa Azure Media Video miniature un riepilogo di Video](media-services-video-summarization.md)</span><span class="sxs-lookup"><span data-stu-id="e9c5c-193">For detailed information and examples, see [Use Azure Media Video Thumbnails tooCreate a Video Summarization](media-services-video-summarization.md)</span></span>

![Analizzare i video](./media/media-services-portal-analyze/media-services-portal-analyze008.png)

### <a name="job-name"></a><span data-ttu-id="e9c5c-195">Nome processo</span><span class="sxs-lookup"><span data-stu-id="e9c5c-195">Job name</span></span>
<span data-ttu-id="e9c5c-196">Nome descrittivo che consente di identificare il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-196">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="e9c5c-197">[Questo](media-services-portal-check-job-progress.md) articolo viene descritto come è possibile monitorare lo stato di avanzamento hello di un processo.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-197">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="e9c5c-198">File di output</span><span class="sxs-lookup"><span data-stu-id="e9c5c-198">Output file</span></span>
<span data-ttu-id="e9c5c-199">Nome descrittivo che consente di identificare il contenuto di output di hello.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-199">A friendly name that lets you identify hello output content.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e9c5c-200">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e9c5c-200">Next steps</span></span>
<span data-ttu-id="e9c5c-201">Visualizzare i percorsi di apprendimento di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-201">View Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e9c5c-202">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="e9c5c-202">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

