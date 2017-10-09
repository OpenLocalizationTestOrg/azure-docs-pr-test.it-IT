---
title: i caratteri tipografici aaaRedact con Azure Media Analitica | Documenti Microsoft
description: "In questo argomento viene illustrato come è rivolto tooredact con analitica multimediali di Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5b6d8b8c-5f4d-4fef-b3d6-dc22c6b5a0f5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako;
ms.openlocfilehash: 1f5688a8c6374151c526a9c702b904d8c3e46164
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics"></a><span data-ttu-id="e517b-103">Offuscare i volti con Analisi Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="e517b-103">Redact faces with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="e517b-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="e517b-104">Overview</span></span>
<span data-ttu-id="e517b-105">**Azure Media Redactor** è un [Azure Media Analitica](media-services-analytics-overview.md) processore di contenuti multimediali (MP) che offre redazione faccia scalabile nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="e517b-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in hello cloud.</span></span> <span data-ttu-id="e517b-106">Adattamento faccia consente si toomodify video in facce tooblur ordine dei singoli utenti selezionati.</span><span class="sxs-lookup"><span data-stu-id="e517b-106">Face redaction enables you toomodify your video in order tooblur faces of selected individuals.</span></span> <span data-ttu-id="e517b-107">È opportuno toouse hello faccia redazione servizio pubblica sicurezza e i supporti di notizie negli scenari in.</span><span class="sxs-lookup"><span data-stu-id="e517b-107">You may want toouse hello face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="e517b-108">Pochi minuti di riprese che contiene più caratteri tipografici possono richiedere ore tooredact manualmente, ma con questa faccia hello servizio processo di adattamento richiederà solo alcuni semplici passaggi.</span><span class="sxs-lookup"><span data-stu-id="e517b-108">A few minutes of footage that contains multiple faces can take hours tooredact manually, but with this service hello face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="e517b-109">Per altre informazioni, vedere [questo](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span><span class="sxs-lookup"><span data-stu-id="e517b-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="e517b-110">In questo argomento fornisce informazioni dettagliate sulle **Azure Media Redactor** e Mostra come toouse con Media Services SDK per .NET.</span><span class="sxs-lookup"><span data-stu-id="e517b-110">This topic gives details about **Azure Media Redactor** and shows how toouse it with Media Services SDK for .NET.</span></span>

<span data-ttu-id="e517b-111">Hello **Azure Media Redactor** Management Pack è attualmente in anteprima.</span><span class="sxs-lookup"><span data-stu-id="e517b-111">hello **Azure Media Redactor** MP is currently in Preview.</span></span> <span data-ttu-id="e517b-112">È disponibile in tutte le aree di Azure pubbliche, nonché nei data center cinesi e del governo degli USA.</span><span class="sxs-lookup"><span data-stu-id="e517b-112">It is available in all public Azure regions as well as US Government and China data centers.</span></span> <span data-ttu-id="e517b-113">Al momento questa versione di anteprima è disponibile gratuitamente.</span><span class="sxs-lookup"><span data-stu-id="e517b-113">This preview is currently free of charge.</span></span> 

## <a name="face-redaction-modes"></a><span data-ttu-id="e517b-114">Modalità per l'offuscamento dei volti</span><span class="sxs-lookup"><span data-stu-id="e517b-114">Face redaction modes</span></span>
<span data-ttu-id="e517b-115">Adattamento facciale works rilevando facce in ogni frame di video e rilevamento viso hello oggetto entrambi avanti e indietro nel tempo, in modo che hello stessa persona può essere sfocatura dagli altri angoli anche.</span><span class="sxs-lookup"><span data-stu-id="e517b-115">Facial redaction works by detecting faces in every frame of video and tracking hello face object both forwards and backwards in time, so that hello same individual can be blurred from other angles as well.</span></span> <span data-ttu-id="e517b-116">Hello il processo di adattamento automatico è molto complesso e non producono sempre 100% dell'output desiderata per questo motivo che Analitica supporti sono disponibili un paio di modi output finale di toomodify hello.</span><span class="sxs-lookup"><span data-stu-id="e517b-116">hello automated redaction process is very complex and does not always produce 100% of desired output, for this reason Media Analytics provides you with a couple of ways toomodify hello final output.</span></span>

<span data-ttu-id="e517b-117">In modalità automatica tooa aggiunta, è un flusso di lavoro in due passaggi che consente di hello selezione/deserializzare-selection di facce trovate tramite un elenco di ID.</span><span class="sxs-lookup"><span data-stu-id="e517b-117">In addition tooa fully automatic mode, there is a two-pass workflow which allows hello selection/de-selection of found faces via a list of IDs.</span></span> <span data-ttu-id="e517b-118">Inoltre, toomake arbitrario per hello regolazioni frame MP utilizza un file di metadati in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="e517b-118">Also, toomake arbitrary per frame adjustments hello MP uses a metadata file in JSON format.</span></span> <span data-ttu-id="e517b-119">Il flusso di lavoro è suddiviso nelle modalità **analisi** e **offuscamento**.</span><span class="sxs-lookup"><span data-stu-id="e517b-119">This workflow is split into **Analyze** and **Redact** modes.</span></span> <span data-ttu-id="e517b-120">È possibile combinare due modalità di hello in un unico passaggio che esegue entrambe le attività in un processo. Questa modalità è detta **combinata**.</span><span class="sxs-lookup"><span data-stu-id="e517b-120">You can combine hello two modes in a single pass that runs both tasks in one job; this mode is called **Combined**.</span></span>

### <a name="combined-mode"></a><span data-ttu-id="e517b-121">Modalità combinata</span><span class="sxs-lookup"><span data-stu-id="e517b-121">Combined mode</span></span>
<span data-ttu-id="e517b-122">Questa modalità produce automaticamente un file mp4 offuscato senza alcun input manuale.</span><span class="sxs-lookup"><span data-stu-id="e517b-122">This will produce a redacted mp4 automatically without any manual input.</span></span>

| <span data-ttu-id="e517b-123">Fase</span><span class="sxs-lookup"><span data-stu-id="e517b-123">Stage</span></span> | <span data-ttu-id="e517b-124">File Name</span><span class="sxs-lookup"><span data-stu-id="e517b-124">File Name</span></span> | <span data-ttu-id="e517b-125">Note</span><span class="sxs-lookup"><span data-stu-id="e517b-125">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e517b-126">Asset di input</span><span class="sxs-lookup"><span data-stu-id="e517b-126">Input asset</span></span> |<span data-ttu-id="e517b-127">foo.bar</span><span class="sxs-lookup"><span data-stu-id="e517b-127">foo.bar</span></span> |<span data-ttu-id="e517b-128">Video in formato WMV, MOV o MP4</span><span class="sxs-lookup"><span data-stu-id="e517b-128">Video in WMV, MOV, or MP4 format</span></span> |
| <span data-ttu-id="e517b-129">Configurazione di input</span><span class="sxs-lookup"><span data-stu-id="e517b-129">Input config</span></span> |<span data-ttu-id="e517b-130">Set di impostazioni di configurazione del processo</span><span class="sxs-lookup"><span data-stu-id="e517b-130">Job configuration preset</span></span> |<span data-ttu-id="e517b-131">{'version':'1.0', 'options': {'mode':'combined'}}</span><span class="sxs-lookup"><span data-stu-id="e517b-131">{'version':'1.0', 'options': {'mode':'combined'}}</span></span> |
| <span data-ttu-id="e517b-132">Asset di output</span><span class="sxs-lookup"><span data-stu-id="e517b-132">Output asset</span></span> |<span data-ttu-id="e517b-133">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="e517b-133">foo_redacted.mp4</span></span> |<span data-ttu-id="e517b-134">Video con sfocatura applicata</span><span class="sxs-lookup"><span data-stu-id="e517b-134">Video with blurring applied</span></span> |

#### <a name="input-example"></a><span data-ttu-id="e517b-135">Esempio di input:</span><span class="sxs-lookup"><span data-stu-id="e517b-135">Input example:</span></span>
[<span data-ttu-id="e517b-136">Guardare il video</span><span class="sxs-lookup"><span data-stu-id="e517b-136">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fed99001d-72ee-4f91-9fc0-cd530d0adbbc%2FDancing.mp4)

#### <a name="output-example"></a><span data-ttu-id="e517b-137">Esempio di output:</span><span class="sxs-lookup"><span data-stu-id="e517b-137">Output example:</span></span>
[<span data-ttu-id="e517b-138">Guardare il video</span><span class="sxs-lookup"><span data-stu-id="e517b-138">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc6608001-e5da-429b-9ec8-d69d8f3bfc79%2Fdance_redacted.mp4)

### <a name="analyze-mode"></a><span data-ttu-id="e517b-139">Modalità analisi</span><span class="sxs-lookup"><span data-stu-id="e517b-139">Analyze mode</span></span>
<span data-ttu-id="e517b-140">Hello **analizzare** passaggio del flusso di lavoro in due passaggi hello accetta un input video e produce un file JSON di percorsi faccia e immagini jpg di ogni rilevato tipo di carattere.</span><span class="sxs-lookup"><span data-stu-id="e517b-140">hello **analyze** pass of hello two-pass workflow takes a video input and produces a JSON file of face locations, and jpg images of each detected face.</span></span>

| <span data-ttu-id="e517b-141">Fase</span><span class="sxs-lookup"><span data-stu-id="e517b-141">Stage</span></span> | <span data-ttu-id="e517b-142">File Name</span><span class="sxs-lookup"><span data-stu-id="e517b-142">File Name</span></span> | <span data-ttu-id="e517b-143">Note</span><span class="sxs-lookup"><span data-stu-id="e517b-143">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e517b-144">Asset di input</span><span class="sxs-lookup"><span data-stu-id="e517b-144">Input asset</span></span> |<span data-ttu-id="e517b-145">foo.bar</span><span class="sxs-lookup"><span data-stu-id="e517b-145">foo.bar</span></span> |<span data-ttu-id="e517b-146">Video in formato WMV, MPV o MP4</span><span class="sxs-lookup"><span data-stu-id="e517b-146">Video in WMV, MPV, or MP4 format</span></span> |
| <span data-ttu-id="e517b-147">Configurazione di input</span><span class="sxs-lookup"><span data-stu-id="e517b-147">Input config</span></span> |<span data-ttu-id="e517b-148">Set di impostazioni di configurazione del processo</span><span class="sxs-lookup"><span data-stu-id="e517b-148">Job configuration preset</span></span> |<span data-ttu-id="e517b-149">{'version':'1.0', 'options': {'mode':'analyze'}}</span><span class="sxs-lookup"><span data-stu-id="e517b-149">{'version':'1.0', 'options': {'mode':'analyze'}}</span></span> |
| <span data-ttu-id="e517b-150">Asset di output</span><span class="sxs-lookup"><span data-stu-id="e517b-150">Output asset</span></span> |<span data-ttu-id="e517b-151">foo_annotations.json</span><span class="sxs-lookup"><span data-stu-id="e517b-151">foo_annotations.json</span></span> |<span data-ttu-id="e517b-152">Dati di annotazione delle posizioni dei volti in formato JSON,</span><span class="sxs-lookup"><span data-stu-id="e517b-152">Annotation data of face locations in JSON format.</span></span> <span data-ttu-id="e517b-153">Questo può essere modificato dal hello utente toomodify hello sfocatura rettangoli di selezione.</span><span class="sxs-lookup"><span data-stu-id="e517b-153">This can be edited by hello user toomodify hello blurring bounding boxes.</span></span> <span data-ttu-id="e517b-154">Vedere l'esempio di seguito.</span><span class="sxs-lookup"><span data-stu-id="e517b-154">See sample below.</span></span> |
| <span data-ttu-id="e517b-155">Asset di output</span><span class="sxs-lookup"><span data-stu-id="e517b-155">Output asset</span></span> |<span data-ttu-id="e517b-156">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span><span class="sxs-lookup"><span data-stu-id="e517b-156">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span></span> |<span data-ttu-id="e517b-157">Un'immagine jpg ritagliata di ogni rilevato tipo di carattere, in cui il numero di hello indica labelId hello del carattere tipografico hello</span><span class="sxs-lookup"><span data-stu-id="e517b-157">A cropped jpg of each detected face, where hello number indicates hello labelId of hello face</span></span> |

#### <a name="output-example"></a><span data-ttu-id="e517b-158">Esempio di output:</span><span class="sxs-lookup"><span data-stu-id="e517b-158">Output example:</span></span>

    {
      "version": 1,
      "timescale": 24000,
      "offset": 0,
      "framerate": 23.976,
      "width": 1280,
      "height": 720,
      "fragments": [
        {
          "start": 0,
          "duration": 48048,
          "interval": 1001,
          "events": [
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [
              {
                "index": 13,
                "id": 1138,
                "x": 0.29537,
                "y": -0.18987,
                "width": 0.36239,
                "height": 0.80335
              },
              {
                "index": 13,
                "id": 2028,
                "x": 0.60427,
                "y": 0.16098,
                "width": 0.26958,
                "height": 0.57943
              }
            ],

    … truncated

### <a name="redact-mode"></a><span data-ttu-id="e517b-159">Modalità offuscamento</span><span class="sxs-lookup"><span data-stu-id="e517b-159">Redact mode</span></span>
<span data-ttu-id="e517b-160">secondo passaggio del flusso di lavoro hello di Hello accetta un numero maggiore di input che devono essere combinati in un singolo asset.</span><span class="sxs-lookup"><span data-stu-id="e517b-160">hello second pass of hello workflow takes a larger number of inputs that must be combined into a single asset.</span></span>

<span data-ttu-id="e517b-161">Questo include un elenco di ID tooblur video originale hello e annotazioni hello JSON.</span><span class="sxs-lookup"><span data-stu-id="e517b-161">This includes a list of IDs tooblur, hello original video, and hello annotations JSON.</span></span> <span data-ttu-id="e517b-162">Questa modalità utilizza hello annotazioni tooapply sfocatura nel video di input hello.</span><span class="sxs-lookup"><span data-stu-id="e517b-162">This mode uses hello annotations tooapply blurring on hello input video.</span></span>

<span data-ttu-id="e517b-163">Hello output di analisi hello non include video originale hello.</span><span class="sxs-lookup"><span data-stu-id="e517b-163">hello output from hello Analyze pass does not include hello original video.</span></span> <span data-ttu-id="e517b-164">Hello video deve toobe caricato nell'asset di input per l'attività in modalità Redact hello hello e selezionato come file primario hello.</span><span class="sxs-lookup"><span data-stu-id="e517b-164">hello video needs toobe uploaded into hello input asset for hello Redact mode task and selected as hello primary file.</span></span>

| <span data-ttu-id="e517b-165">Fase</span><span class="sxs-lookup"><span data-stu-id="e517b-165">Stage</span></span> | <span data-ttu-id="e517b-166">File Name</span><span class="sxs-lookup"><span data-stu-id="e517b-166">File Name</span></span> | <span data-ttu-id="e517b-167">Note</span><span class="sxs-lookup"><span data-stu-id="e517b-167">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e517b-168">Asset di input</span><span class="sxs-lookup"><span data-stu-id="e517b-168">Input asset</span></span> |<span data-ttu-id="e517b-169">foo.bar</span><span class="sxs-lookup"><span data-stu-id="e517b-169">foo.bar</span></span> |<span data-ttu-id="e517b-170">Video in formato WMV, MPV o MP4.</span><span class="sxs-lookup"><span data-stu-id="e517b-170">Video in WMV, MPV, or MP4 format.</span></span> <span data-ttu-id="e517b-171">Stesso video del passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="e517b-171">Same video as in step 1.</span></span> |
| <span data-ttu-id="e517b-172">Asset di input</span><span class="sxs-lookup"><span data-stu-id="e517b-172">Input asset</span></span> |<span data-ttu-id="e517b-173">foo_annotations.json</span><span class="sxs-lookup"><span data-stu-id="e517b-173">foo_annotations.json</span></span> |<span data-ttu-id="e517b-174">File di metadati delle annotazioni della prima fase, con modifiche facoltative.</span><span class="sxs-lookup"><span data-stu-id="e517b-174">annotations metadata file from phase one, with optional modifications.</span></span> |
| <span data-ttu-id="e517b-175">Asset di input</span><span class="sxs-lookup"><span data-stu-id="e517b-175">Input asset</span></span> |<span data-ttu-id="e517b-176">foo_IDList.txt (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="e517b-176">foo_IDList.txt (Optional)</span></span> |<span data-ttu-id="e517b-177">Elenco del carattere tipografico tooredact ID separati da facoltativa nuova riga.</span><span class="sxs-lookup"><span data-stu-id="e517b-177">Optional new line separated list of face IDs tooredact.</span></span> <span data-ttu-id="e517b-178">Se viene lasciato vuoto, vengono sfocati tutti i volti.</span><span class="sxs-lookup"><span data-stu-id="e517b-178">If left blank, this blurs all faces.</span></span> |
| <span data-ttu-id="e517b-179">Configurazione di input</span><span class="sxs-lookup"><span data-stu-id="e517b-179">Input config</span></span> |<span data-ttu-id="e517b-180">Set di impostazioni di configurazione del processo</span><span class="sxs-lookup"><span data-stu-id="e517b-180">Job configuration preset</span></span> |<span data-ttu-id="e517b-181">{'version':'1.0', 'options': {'mode':'redact'}}</span><span class="sxs-lookup"><span data-stu-id="e517b-181">{'version':'1.0', 'options': {'mode':'redact'}}</span></span> |
| <span data-ttu-id="e517b-182">Asset di output</span><span class="sxs-lookup"><span data-stu-id="e517b-182">Output asset</span></span> |<span data-ttu-id="e517b-183">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="e517b-183">foo_redacted.mp4</span></span> |<span data-ttu-id="e517b-184">Video con sfocatura applicata in base alle annotazioni.</span><span class="sxs-lookup"><span data-stu-id="e517b-184">Video with blurring applied based on annotations</span></span> |

#### <a name="example-output"></a><span data-ttu-id="e517b-185">Output di esempio</span><span class="sxs-lookup"><span data-stu-id="e517b-185">Example output</span></span>
<span data-ttu-id="e517b-186">Questo è l'output di hello da un IDList con un ID selezionato.</span><span class="sxs-lookup"><span data-stu-id="e517b-186">This is hello output from an IDList with one ID selected.</span></span>

[<span data-ttu-id="e517b-187">Guardare il video</span><span class="sxs-lookup"><span data-stu-id="e517b-187">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fad6e24a2-4f9c-46ee-9fa7-bf05e20d19ac%2Fdance_redacted1.mp4)

<span data-ttu-id="e517b-188">Esempio foo_IDList.txt</span><span class="sxs-lookup"><span data-stu-id="e517b-188">Example foo_IDList.txt</span></span>
 
     1
     2
     3

## <a name="blur-types"></a><span data-ttu-id="e517b-189">Tipi di sfocature</span><span class="sxs-lookup"><span data-stu-id="e517b-189">Blur types</span></span>

<span data-ttu-id="e517b-190">In hello **combinata** o **Redact** modalità, sono disponibili 5 sfocatura diverse modalità, è possibile scegliere tra mediante la configurazione di input JSON hello: **bassa**, **Med**, **Elevata**, **Debug**, e **nero**.</span><span class="sxs-lookup"><span data-stu-id="e517b-190">In hello **Combined** or **Redact** mode, there are 5 different blur modes you can choose from via hello JSON input configuration: **Low**, **Med**, **High**, **Debug**, and **Black**.</span></span> <span data-ttu-id="e517b-191">Per impostazione predefinita, viene usata **Med**.</span><span class="sxs-lookup"><span data-stu-id="e517b-191">By default **Med** is used.</span></span>

<span data-ttu-id="e517b-192">È possibile trovare esempi di hello sfocatura tipi più avanti.</span><span class="sxs-lookup"><span data-stu-id="e517b-192">You can find samples of hello blur types below.</span></span>

### <a name="example-json"></a><span data-ttu-id="e517b-193">JSON di esempio:</span><span class="sxs-lookup"><span data-stu-id="e517b-193">Example JSON:</span></span>

    {'version':'1.0', 'options': {'Mode': 'Combined', 'BlurType': 'High'}}

#### <a name="low"></a><span data-ttu-id="e517b-194">Basso</span><span class="sxs-lookup"><span data-stu-id="e517b-194">Low</span></span>

![Basso](./media/media-services-face-redaction/blur1.png)
 
#### <a name="med"></a><span data-ttu-id="e517b-196">Med</span><span class="sxs-lookup"><span data-stu-id="e517b-196">Med</span></span>

![Med](./media/media-services-face-redaction/blur2.png)

#### <a name="high"></a><span data-ttu-id="e517b-198">Alto</span><span class="sxs-lookup"><span data-stu-id="e517b-198">High</span></span>

![Alto](./media/media-services-face-redaction/blur3.png)

#### <a name="debug"></a><span data-ttu-id="e517b-200">Debug</span><span class="sxs-lookup"><span data-stu-id="e517b-200">Debug</span></span>

![Debug](./media/media-services-face-redaction/blur4.png)

#### <a name="black"></a><span data-ttu-id="e517b-202">Nero</span><span class="sxs-lookup"><span data-stu-id="e517b-202">Black</span></span>

![Nero](./media/media-services-face-redaction/blur5.png)

## <a name="elements-of-hello-output-json-file"></a><span data-ttu-id="e517b-204">Elementi hello JSON del file di output</span><span class="sxs-lookup"><span data-stu-id="e517b-204">Elements of hello output JSON file</span></span>

<span data-ttu-id="e517b-205">Hello redazione MP fornisce il rilevamento di percorso faccia ad alta precisione e rilevamento in grado di rilevare il too64 viso umana in un frame video.</span><span class="sxs-lookup"><span data-stu-id="e517b-205">hello Redaction MP provides high precision face location detection and tracking that can detect up too64 human faces in a video frame.</span></span> <span data-ttu-id="e517b-206">Volti frontali forniscono risultati ottimali hello, mentre i caratteri tipografici lato e facce di piccole dimensioni (minore o uguale a too24x24 pixel) rappresentano una sfida.</span><span class="sxs-lookup"><span data-stu-id="e517b-206">Frontal faces provide hello best results, while side faces and small faces (less than or equal too24x24 pixels) are challenging.</span></span>

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

## <a name="net-sample-code"></a><span data-ttu-id="e517b-207">Codice di esempio .NET</span><span class="sxs-lookup"><span data-stu-id="e517b-207">.NET sample code</span></span>

<span data-ttu-id="e517b-208">esempio Hello programma mostra come:</span><span class="sxs-lookup"><span data-stu-id="e517b-208">hello following program shows how to:</span></span>

1. <span data-ttu-id="e517b-209">Creare un asset e caricare un file multimediale nell'asset hello.</span><span class="sxs-lookup"><span data-stu-id="e517b-209">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="e517b-210">Creare un processo con un'attività di adattamento faccia basata su un file di configurazione che contiene i seguenti set di impostazioni json hello.</span><span class="sxs-lookup"><span data-stu-id="e517b-210">Create a job with a face redaction task based on a configuration file that contains hello following json preset.</span></span> 
   
        {'version':'1.0', 'options': {'mode':'combined'}}
3. <span data-ttu-id="e517b-211">Scaricare i file JSON di output di hello.</span><span class="sxs-lookup"><span data-stu-id="e517b-211">Download hello output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="e517b-212">Creare e configurare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e517b-212">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="e517b-213">Configurare l'ambiente di sviluppo e di popolare il file app. config hello con informazioni di connessione, come descritto in [lo sviluppo di servizi multimediali con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="e517b-213">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="e517b-214">Esempio</span><span class="sxs-lookup"><span data-stu-id="e517b-214">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace FaceRedaction
    {
        class Program
        {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // Field for service context.
        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Run hello FaceRedaction job.
            var asset = RunFaceRedactionJob(@"C:\supportFiles\FaceRedaction\SomeFootage.mp4",
                        @"C:\supportFiles\FaceRedaction\config.json");

            // Download hello job output asset.
            DownloadAsset(asset, @"C:\supportFiles\FaceRedaction\Output");
        }

        static IAsset RunFaceRedactionJob(string inputMediaFilePath, string configurationFile)
        {
            // Create an asset and upload hello input media file toostorage.
            IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Face Redaction Input Asset",
            AssetCreationOptions.None);

            // Declare a new job.
            IJob job = _context.Jobs.Create("My Face Redaction Job");

            // Get a reference tooAzure Media Redactor.
            string MediaProcessorName = "Azure Media Redactor";

            var processor = GetLatestMediaProcessorByName(MediaProcessorName);

            // Read configuration from hello specified file.
            string configuration = File.ReadAllText(configurationFile);

            // Create a task with hello encoding details, using a string preset.
            ITask task = job.Tasks.AddNew("My Face Redaction Task",
            processor,
            configuration,
            TaskOptions.None);

            // Specify hello input asset.
            task.InputAssets.Add(asset);

            // Add an output asset toocontain hello results of hello job.
            task.OutputAssets.AddNew("My Face Redaction Output Asset", AssetCreationOptions.None);

            // Use hello following event handler toocheck job progress.  
            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

            // Launch hello job.
            job.Submit();

            // Check job execution and wait for job toofinish.
            Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

            progressJobTask.Wait();

            // If job state is Error, hello event handling
            // method for job progress should log errors.  Here we check
            // for error state and exit if needed.
            if (job.State == JobState.Error)
            {
            ErrorDetail error = job.Tasks.First().ErrorDetails.First();
            Console.WriteLine(string.Format("Error: {0}. {1}",
                            error.Code,
                            error.Message));
            return null;
            }

            return job.OutputMediaAssets[0];
        }

        static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
        {
            IAsset asset = _context.Assets.Create(assetName, options);

            var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
            assetFile.Upload(filePath);

            return asset;
        }

        static void DownloadAsset(IAsset asset, string outputDirectory)
        {
            foreach (IAssetFile file in asset.AssetFiles)
            {
            file.Download(Path.Combine(outputDirectory, file.Name));
            }
        }

        static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors
            .Where(p => p.Name == mediaProcessorName)
            .ToList()
            .OrderBy(p => new Version(p.Version))
            .LastOrDefault();

            if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                   mediaProcessorName));

            return processor;
        }

        static private void StateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine("Job state changed event:");
            Console.WriteLine("  Previous state: " + e.PreviousState);
            Console.WriteLine("  Current state: " + e.CurrentState);

            switch (e.CurrentState)
            {
            case JobState.Finished:
                Console.WriteLine();
                Console.WriteLine("Job is finished.");
                Console.WriteLine();
                break;
            case JobState.Canceling:
            case JobState.Queued:
            case JobState.Scheduled:
            case JobState.Processing:
                Console.WriteLine("Please wait...\n");
                break;
            case JobState.Canceled:
            case JobState.Error:
                // Cast sender as a job.
                IJob job = (IJob)sender;
                // Display or log error details as needed.
                // LogJobStop(job.Id);
                break;
            default:
                break;
            }
        }
        }
    }

## <a name="next-steps"></a><span data-ttu-id="e517b-215">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e517b-215">Next steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e517b-216">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="e517b-216">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="e517b-217">Collegamenti correlati</span><span class="sxs-lookup"><span data-stu-id="e517b-217">Related links</span></span>
[<span data-ttu-id="e517b-218">Panoramica di Analisi servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="e517b-218">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="e517b-219">Demo di Analisi servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="e517b-219">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

