---
title: Offuscare i volti con Analisi Servizi multimediali di Azure | Documentazione Microsoft
description: Questo argomento illustra come offuscare i volti con Analisi Servizi multimediali di Azure.
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
ms.openlocfilehash: 747f3ae1a7484515083c590942de3da22568cd39
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="redact-faces-with-azure-media-analytics"></a><span data-ttu-id="cf27f-103">Offuscare i volti con Analisi Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="cf27f-103">Redact faces with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="cf27f-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="cf27f-104">Overview</span></span>
<span data-ttu-id="cf27f-105">**Azure Media Redactor** è un processore di contenuti multimediali di [Analisi Servizi multimediali di Azure](media-services-analytics-overview.md) che offre funzionalità scalabili di offuscamento dei volti nel cloud.</span><span class="sxs-lookup"><span data-stu-id="cf27f-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in the cloud.</span></span> <span data-ttu-id="cf27f-106">L'offuscamento dei volti consente di modificare un video per sfocare i volti di persone selezionate.</span><span class="sxs-lookup"><span data-stu-id="cf27f-106">Face redaction enables you to modify your video in order to blur faces of selected individuals.</span></span> <span data-ttu-id="cf27f-107">Può essere opportuno usare tale servizio in scenari di pubblica sicurezza e notizie giornalistiche.</span><span class="sxs-lookup"><span data-stu-id="cf27f-107">You may want to use the face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="cf27f-108">Offuscare manualmente alcuni minuti di filmato contenenti più volti può richiedere ore, ma con questo servizio il processo di offuscamento dei volti richiederà pochi semplici passaggi.</span><span class="sxs-lookup"><span data-stu-id="cf27f-108">A few minutes of footage that contains multiple faces can take hours to redact manually, but with this service the face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="cf27f-109">Per altre informazioni, vedere [questo](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span><span class="sxs-lookup"><span data-stu-id="cf27f-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="cf27f-110">Questo argomento contiene informazioni dettagliate su **Azure Media Redactor** e illustra come usare questa funzionalità con Media Services SDK per .NET.</span><span class="sxs-lookup"><span data-stu-id="cf27f-110">This topic gives details about **Azure Media Redactor** and shows how to use it with Media Services SDK for .NET.</span></span>

<span data-ttu-id="cf27f-111">Il processore di contenuti multimediali **Azure Media Redactor** è attualmente in anteprima.</span><span class="sxs-lookup"><span data-stu-id="cf27f-111">The **Azure Media Redactor** MP is currently in Preview.</span></span> <span data-ttu-id="cf27f-112">È disponibile in tutte le aree di Azure pubbliche, nonché nei data center cinesi e del governo degli USA.</span><span class="sxs-lookup"><span data-stu-id="cf27f-112">It is available in all public Azure regions as well as US Government and China data centers.</span></span> <span data-ttu-id="cf27f-113">Al momento questa versione di anteprima è disponibile gratuitamente.</span><span class="sxs-lookup"><span data-stu-id="cf27f-113">This preview is currently free of charge.</span></span> 

## <a name="face-redaction-modes"></a><span data-ttu-id="cf27f-114">Modalità per l'offuscamento dei volti</span><span class="sxs-lookup"><span data-stu-id="cf27f-114">Face redaction modes</span></span>
<span data-ttu-id="cf27f-115">La funzionalità di offuscamento dei volti rileva i volti in ogni fotogramma del video e monitora l'oggetto volto avanti e indietro nel tempo in modo da consentire la sfocatura della stessa persona anche da altre angolazioni.</span><span class="sxs-lookup"><span data-stu-id="cf27f-115">Facial redaction works by detecting faces in every frame of video and tracking the face object both forwards and backwards in time, so that the same individual can be blurred from other angles as well.</span></span> <span data-ttu-id="cf27f-116">Il processo di offuscamento automatizzato è molto complesso e non sempre produce al 100% l'output desiderato. Per tale motivo, Analisi Servizi multimediali offre alcuni modi per modificare l'output finale.</span><span class="sxs-lookup"><span data-stu-id="cf27f-116">The automated redaction process is very complex and does not always produce 100% of desired output, for this reason Media Analytics provides you with a couple of ways to modify the final output.</span></span>

<span data-ttu-id="cf27f-117">In aggiunta a una modalità interamente automatica, esiste un flusso di lavoro in due passaggi che consente di selezionare/deselezionare i volti trovati tramite un elenco di ID.</span><span class="sxs-lookup"><span data-stu-id="cf27f-117">In addition to a fully automatic mode, there is a two-pass workflow which allows the selection/de-selection of found faces via a list of IDs.</span></span> <span data-ttu-id="cf27f-118">Per apportare modifiche arbitrarie per singolo fotogramma, inoltre, il processore di contenuti multimediali usa un file di metadati in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="cf27f-118">Also, to make arbitrary per frame adjustments the MP uses a metadata file in JSON format.</span></span> <span data-ttu-id="cf27f-119">Il flusso di lavoro è suddiviso nelle modalità **analisi** e **offuscamento**.</span><span class="sxs-lookup"><span data-stu-id="cf27f-119">This workflow is split into **Analyze** and **Redact** modes.</span></span> <span data-ttu-id="cf27f-120">È possibile combinare le due modalità in un singolo passaggio che esegue entrambe le attività in un unico processo. Questa modalità è detta **combinata**.</span><span class="sxs-lookup"><span data-stu-id="cf27f-120">You can combine the two modes in a single pass that runs both tasks in one job; this mode is called **Combined**.</span></span>

### <a name="combined-mode"></a><span data-ttu-id="cf27f-121">Modalità combinata</span><span class="sxs-lookup"><span data-stu-id="cf27f-121">Combined mode</span></span>
<span data-ttu-id="cf27f-122">Questa modalità produce automaticamente un file mp4 offuscato senza alcun input manuale.</span><span class="sxs-lookup"><span data-stu-id="cf27f-122">This will produce a redacted mp4 automatically without any manual input.</span></span>

| <span data-ttu-id="cf27f-123">Fase</span><span class="sxs-lookup"><span data-stu-id="cf27f-123">Stage</span></span> | <span data-ttu-id="cf27f-124">File Name</span><span class="sxs-lookup"><span data-stu-id="cf27f-124">File Name</span></span> | <span data-ttu-id="cf27f-125">Note</span><span class="sxs-lookup"><span data-stu-id="cf27f-125">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cf27f-126">Asset di input</span><span class="sxs-lookup"><span data-stu-id="cf27f-126">Input asset</span></span> |<span data-ttu-id="cf27f-127">foo.bar</span><span class="sxs-lookup"><span data-stu-id="cf27f-127">foo.bar</span></span> |<span data-ttu-id="cf27f-128">Video in formato WMV, MOV o MP4</span><span class="sxs-lookup"><span data-stu-id="cf27f-128">Video in WMV, MOV, or MP4 format</span></span> |
| <span data-ttu-id="cf27f-129">Configurazione di input</span><span class="sxs-lookup"><span data-stu-id="cf27f-129">Input config</span></span> |<span data-ttu-id="cf27f-130">Set di impostazioni di configurazione del processo</span><span class="sxs-lookup"><span data-stu-id="cf27f-130">Job configuration preset</span></span> |<span data-ttu-id="cf27f-131">{'version':'1.0', 'options': {'mode':'combined'}}</span><span class="sxs-lookup"><span data-stu-id="cf27f-131">{'version':'1.0', 'options': {'mode':'combined'}}</span></span> |
| <span data-ttu-id="cf27f-132">Asset di output</span><span class="sxs-lookup"><span data-stu-id="cf27f-132">Output asset</span></span> |<span data-ttu-id="cf27f-133">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="cf27f-133">foo_redacted.mp4</span></span> |<span data-ttu-id="cf27f-134">Video con sfocatura applicata</span><span class="sxs-lookup"><span data-stu-id="cf27f-134">Video with blurring applied</span></span> |

#### <a name="input-example"></a><span data-ttu-id="cf27f-135">Esempio di input:</span><span class="sxs-lookup"><span data-stu-id="cf27f-135">Input example:</span></span>
[<span data-ttu-id="cf27f-136">Guardare il video</span><span class="sxs-lookup"><span data-stu-id="cf27f-136">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fed99001d-72ee-4f91-9fc0-cd530d0adbbc%2FDancing.mp4)

#### <a name="output-example"></a><span data-ttu-id="cf27f-137">Esempio di output:</span><span class="sxs-lookup"><span data-stu-id="cf27f-137">Output example:</span></span>
[<span data-ttu-id="cf27f-138">Guardare il video</span><span class="sxs-lookup"><span data-stu-id="cf27f-138">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc6608001-e5da-429b-9ec8-d69d8f3bfc79%2Fdance_redacted.mp4)

### <a name="analyze-mode"></a><span data-ttu-id="cf27f-139">Modalità analisi</span><span class="sxs-lookup"><span data-stu-id="cf27f-139">Analyze mode</span></span>
<span data-ttu-id="cf27f-140">Nel flusso di lavoro in due passaggi, il passaggio dell' **analisi** usa un input video e produce un file JSON di posizioni di volti e immagini jpg di ogni volto rilevato.</span><span class="sxs-lookup"><span data-stu-id="cf27f-140">The **analyze** pass of the two-pass workflow takes a video input and produces a JSON file of face locations, and jpg images of each detected face.</span></span>

| <span data-ttu-id="cf27f-141">Fase</span><span class="sxs-lookup"><span data-stu-id="cf27f-141">Stage</span></span> | <span data-ttu-id="cf27f-142">File Name</span><span class="sxs-lookup"><span data-stu-id="cf27f-142">File Name</span></span> | <span data-ttu-id="cf27f-143">Note</span><span class="sxs-lookup"><span data-stu-id="cf27f-143">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cf27f-144">Asset di input</span><span class="sxs-lookup"><span data-stu-id="cf27f-144">Input asset</span></span> |<span data-ttu-id="cf27f-145">foo.bar</span><span class="sxs-lookup"><span data-stu-id="cf27f-145">foo.bar</span></span> |<span data-ttu-id="cf27f-146">Video in formato WMV, MPV o MP4</span><span class="sxs-lookup"><span data-stu-id="cf27f-146">Video in WMV, MPV, or MP4 format</span></span> |
| <span data-ttu-id="cf27f-147">Configurazione di input</span><span class="sxs-lookup"><span data-stu-id="cf27f-147">Input config</span></span> |<span data-ttu-id="cf27f-148">Set di impostazioni di configurazione del processo</span><span class="sxs-lookup"><span data-stu-id="cf27f-148">Job configuration preset</span></span> |<span data-ttu-id="cf27f-149">{'version':'1.0', 'options': {'mode':'analyze'}}</span><span class="sxs-lookup"><span data-stu-id="cf27f-149">{'version':'1.0', 'options': {'mode':'analyze'}}</span></span> |
| <span data-ttu-id="cf27f-150">Asset di output</span><span class="sxs-lookup"><span data-stu-id="cf27f-150">Output asset</span></span> |<span data-ttu-id="cf27f-151">foo_annotations.json</span><span class="sxs-lookup"><span data-stu-id="cf27f-151">foo_annotations.json</span></span> |<span data-ttu-id="cf27f-152">Dati di annotazione delle posizioni dei volti in formato JSON,</span><span class="sxs-lookup"><span data-stu-id="cf27f-152">Annotation data of face locations in JSON format.</span></span> <span data-ttu-id="cf27f-153">modificabili dall'utente per modificare i rettangoli di selezione della sfocatura.</span><span class="sxs-lookup"><span data-stu-id="cf27f-153">This can be edited by the user to modify the blurring bounding boxes.</span></span> <span data-ttu-id="cf27f-154">Vedere l'esempio di seguito.</span><span class="sxs-lookup"><span data-stu-id="cf27f-154">See sample below.</span></span> |
| <span data-ttu-id="cf27f-155">Asset di output</span><span class="sxs-lookup"><span data-stu-id="cf27f-155">Output asset</span></span> |<span data-ttu-id="cf27f-156">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span><span class="sxs-lookup"><span data-stu-id="cf27f-156">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span></span> |<span data-ttu-id="cf27f-157">File jpg ritagliato di ogni volto rilevato, in cui il numero indica l'ID etichetta del volto</span><span class="sxs-lookup"><span data-stu-id="cf27f-157">A cropped jpg of each detected face, where the number indicates the labelId of the face</span></span> |

#### <a name="output-example"></a><span data-ttu-id="cf27f-158">Esempio di output:</span><span class="sxs-lookup"><span data-stu-id="cf27f-158">Output example:</span></span>

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

### <a name="redact-mode"></a><span data-ttu-id="cf27f-159">Modalità offuscamento</span><span class="sxs-lookup"><span data-stu-id="cf27f-159">Redact mode</span></span>
<span data-ttu-id="cf27f-160">Il secondo passaggio del flusso di lavoro usa un numero superiore di input che devono essere combinati in un singolo asset.</span><span class="sxs-lookup"><span data-stu-id="cf27f-160">The second pass of the workflow takes a larger number of inputs that must be combined into a single asset.</span></span>

<span data-ttu-id="cf27f-161">Gli input includono un elenco di ID da sfocare, il video originale e il file JSON delle annotazioni.</span><span class="sxs-lookup"><span data-stu-id="cf27f-161">This includes a list of IDs to blur, the original video, and the annotations JSON.</span></span> <span data-ttu-id="cf27f-162">Questa modalità usa le annotazioni per applicare la sfocatura nel video di input.</span><span class="sxs-lookup"><span data-stu-id="cf27f-162">This mode uses the annotations to apply blurring on the input video.</span></span>

<span data-ttu-id="cf27f-163">L'output del passaggio dell'analisi non include il video originale.</span><span class="sxs-lookup"><span data-stu-id="cf27f-163">The output from the Analyze pass does not include the original video.</span></span> <span data-ttu-id="cf27f-164">Il video deve essere caricato nell'asset di input per l'attività della modalità offuscamento ed essere selezionato come file primario.</span><span class="sxs-lookup"><span data-stu-id="cf27f-164">The video needs to be uploaded into the input asset for the Redact mode task and selected as the primary file.</span></span>

| <span data-ttu-id="cf27f-165">Fase</span><span class="sxs-lookup"><span data-stu-id="cf27f-165">Stage</span></span> | <span data-ttu-id="cf27f-166">File Name</span><span class="sxs-lookup"><span data-stu-id="cf27f-166">File Name</span></span> | <span data-ttu-id="cf27f-167">Note</span><span class="sxs-lookup"><span data-stu-id="cf27f-167">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cf27f-168">Asset di input</span><span class="sxs-lookup"><span data-stu-id="cf27f-168">Input asset</span></span> |<span data-ttu-id="cf27f-169">foo.bar</span><span class="sxs-lookup"><span data-stu-id="cf27f-169">foo.bar</span></span> |<span data-ttu-id="cf27f-170">Video in formato WMV, MPV o MP4.</span><span class="sxs-lookup"><span data-stu-id="cf27f-170">Video in WMV, MPV, or MP4 format.</span></span> <span data-ttu-id="cf27f-171">Stesso video del passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="cf27f-171">Same video as in step 1.</span></span> |
| <span data-ttu-id="cf27f-172">Asset di input</span><span class="sxs-lookup"><span data-stu-id="cf27f-172">Input asset</span></span> |<span data-ttu-id="cf27f-173">foo_annotations.json</span><span class="sxs-lookup"><span data-stu-id="cf27f-173">foo_annotations.json</span></span> |<span data-ttu-id="cf27f-174">File di metadati delle annotazioni della prima fase, con modifiche facoltative.</span><span class="sxs-lookup"><span data-stu-id="cf27f-174">annotations metadata file from phase one, with optional modifications.</span></span> |
| <span data-ttu-id="cf27f-175">Asset di input</span><span class="sxs-lookup"><span data-stu-id="cf27f-175">Input asset</span></span> |<span data-ttu-id="cf27f-176">foo_IDList.txt (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="cf27f-176">foo_IDList.txt (Optional)</span></span> |<span data-ttu-id="cf27f-177">Elenco facoltativo separato da caratteri di nuova riga di ID volto da offuscare.</span><span class="sxs-lookup"><span data-stu-id="cf27f-177">Optional new line separated list of face IDs to redact.</span></span> <span data-ttu-id="cf27f-178">Se viene lasciato vuoto, vengono sfocati tutti i volti.</span><span class="sxs-lookup"><span data-stu-id="cf27f-178">If left blank, this blurs all faces.</span></span> |
| <span data-ttu-id="cf27f-179">Configurazione di input</span><span class="sxs-lookup"><span data-stu-id="cf27f-179">Input config</span></span> |<span data-ttu-id="cf27f-180">Set di impostazioni di configurazione del processo</span><span class="sxs-lookup"><span data-stu-id="cf27f-180">Job configuration preset</span></span> |<span data-ttu-id="cf27f-181">{'version':'1.0', 'options': {'mode':'redact'}}</span><span class="sxs-lookup"><span data-stu-id="cf27f-181">{'version':'1.0', 'options': {'mode':'redact'}}</span></span> |
| <span data-ttu-id="cf27f-182">Asset di output</span><span class="sxs-lookup"><span data-stu-id="cf27f-182">Output asset</span></span> |<span data-ttu-id="cf27f-183">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="cf27f-183">foo_redacted.mp4</span></span> |<span data-ttu-id="cf27f-184">Video con sfocatura applicata in base alle annotazioni.</span><span class="sxs-lookup"><span data-stu-id="cf27f-184">Video with blurring applied based on annotations</span></span> |

#### <a name="example-output"></a><span data-ttu-id="cf27f-185">Output di esempio</span><span class="sxs-lookup"><span data-stu-id="cf27f-185">Example output</span></span>
<span data-ttu-id="cf27f-186">Questo output viene ottenuto da un elenco di ID con un ID selezionato.</span><span class="sxs-lookup"><span data-stu-id="cf27f-186">This is the output from an IDList with one ID selected.</span></span>

[<span data-ttu-id="cf27f-187">Guardare il video</span><span class="sxs-lookup"><span data-stu-id="cf27f-187">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fad6e24a2-4f9c-46ee-9fa7-bf05e20d19ac%2Fdance_redacted1.mp4)

<span data-ttu-id="cf27f-188">Esempio foo_IDList.txt</span><span class="sxs-lookup"><span data-stu-id="cf27f-188">Example foo_IDList.txt</span></span>
 
     1
     2
     3

## <a name="blur-types"></a><span data-ttu-id="cf27f-189">Tipi di sfocature</span><span class="sxs-lookup"><span data-stu-id="cf27f-189">Blur types</span></span>

<span data-ttu-id="cf27f-190">Nella modalità **Combined** o **Redact**, sono disponibili 5 modalità di sfocatura diverse tra cui scegliere tramite la configurazione di input JSON: **Low**, **Med**, **High**, **Debug** e **Black**.</span><span class="sxs-lookup"><span data-stu-id="cf27f-190">In the **Combined** or **Redact** mode, there are 5 different blur modes you can choose from via the JSON input configuration: **Low**, **Med**, **High**, **Debug**, and **Black**.</span></span> <span data-ttu-id="cf27f-191">Per impostazione predefinita, viene usata **Med**.</span><span class="sxs-lookup"><span data-stu-id="cf27f-191">By default **Med** is used.</span></span>

<span data-ttu-id="cf27f-192">Di seguito sono riportati alcuni esempi dei tipi di sfocature.</span><span class="sxs-lookup"><span data-stu-id="cf27f-192">You can find samples of the blur types below.</span></span>

### <a name="example-json"></a><span data-ttu-id="cf27f-193">JSON di esempio:</span><span class="sxs-lookup"><span data-stu-id="cf27f-193">Example JSON:</span></span>

    {'version':'1.0', 'options': {'Mode': 'Combined', 'BlurType': 'High'}}

#### <a name="low"></a><span data-ttu-id="cf27f-194">Basso</span><span class="sxs-lookup"><span data-stu-id="cf27f-194">Low</span></span>

![Basso](./media/media-services-face-redaction/blur1.png)
 
#### <a name="med"></a><span data-ttu-id="cf27f-196">Med</span><span class="sxs-lookup"><span data-stu-id="cf27f-196">Med</span></span>

![Med](./media/media-services-face-redaction/blur2.png)

#### <a name="high"></a><span data-ttu-id="cf27f-198">Alto</span><span class="sxs-lookup"><span data-stu-id="cf27f-198">High</span></span>

![Alto](./media/media-services-face-redaction/blur3.png)

#### <a name="debug"></a><span data-ttu-id="cf27f-200">Debug</span><span class="sxs-lookup"><span data-stu-id="cf27f-200">Debug</span></span>

![Debug](./media/media-services-face-redaction/blur4.png)

#### <a name="black"></a><span data-ttu-id="cf27f-202">Nero</span><span class="sxs-lookup"><span data-stu-id="cf27f-202">Black</span></span>

![Nero](./media/media-services-face-redaction/blur5.png)

## <a name="elements-of-the-output-json-file"></a><span data-ttu-id="cf27f-204">Elementi del file di output JSON</span><span class="sxs-lookup"><span data-stu-id="cf27f-204">Elements of the output JSON file</span></span>

<span data-ttu-id="cf27f-205">Il processore di contenuti multimediali per l'offuscamento offre funzionalità di rilevamento della posizione e monitoraggio dei volti ad alta precisione che possono rilevare fino a 64 volti umani in un fotogramma video.</span><span class="sxs-lookup"><span data-stu-id="cf27f-205">The Redaction MP provides high precision face location detection and tracking that can detect up to 64 human faces in a video frame.</span></span> <span data-ttu-id="cf27f-206">Le riprese anteriori producono risultati ottimali, mentre profili e volti di piccole dimensioni (inferiori o uguali a 24x24 pixel) presentano alcune problematiche.</span><span class="sxs-lookup"><span data-stu-id="cf27f-206">Frontal faces provide the best results, while side faces and small faces (less than or equal to 24x24 pixels) are challenging.</span></span>

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

## <a name="net-sample-code"></a><span data-ttu-id="cf27f-207">Codice di esempio .NET</span><span class="sxs-lookup"><span data-stu-id="cf27f-207">.NET sample code</span></span>

<span data-ttu-id="cf27f-208">Il programma seguente illustra come:</span><span class="sxs-lookup"><span data-stu-id="cf27f-208">The following program shows how to:</span></span>

1. <span data-ttu-id="cf27f-209">Creare un asset e caricare un file multimediale nell'asset.</span><span class="sxs-lookup"><span data-stu-id="cf27f-209">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="cf27f-210">Creare un processo con un'attività di offuscamento dei volti in base a un file di configurazione contenente il set di impostazioni JSON seguente.</span><span class="sxs-lookup"><span data-stu-id="cf27f-210">Create a job with a face redaction task based on a configuration file that contains the following json preset.</span></span> 
   
        {'version':'1.0', 'options': {'mode':'combined'}}
3. <span data-ttu-id="cf27f-211">Scaricare i file JSON di output.</span><span class="sxs-lookup"><span data-stu-id="cf27f-211">Download the output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="cf27f-212">Creare e configurare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cf27f-212">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="cf27f-213">Configurare l'ambiente di sviluppo e popolare il file app.config con le informazioni di connessione, come descritto in [Sviluppo di applicazioni di Servizi multimediali con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="cf27f-213">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="cf27f-214">Esempio</span><span class="sxs-lookup"><span data-stu-id="cf27f-214">Example</span></span>

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
        // Read values from the App.config file.
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

            // Run the FaceRedaction job.
            var asset = RunFaceRedactionJob(@"C:\supportFiles\FaceRedaction\SomeFootage.mp4",
                        @"C:\supportFiles\FaceRedaction\config.json");

            // Download the job output asset.
            DownloadAsset(asset, @"C:\supportFiles\FaceRedaction\Output");
        }

        static IAsset RunFaceRedactionJob(string inputMediaFilePath, string configurationFile)
        {
            // Create an asset and upload the input media file to storage.
            IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Face Redaction Input Asset",
            AssetCreationOptions.None);

            // Declare a new job.
            IJob job = _context.Jobs.Create("My Face Redaction Job");

            // Get a reference to Azure Media Redactor.
            string MediaProcessorName = "Azure Media Redactor";

            var processor = GetLatestMediaProcessorByName(MediaProcessorName);

            // Read configuration from the specified file.
            string configuration = File.ReadAllText(configurationFile);

            // Create a task with the encoding details, using a string preset.
            ITask task = job.Tasks.AddNew("My Face Redaction Task",
            processor,
            configuration,
            TaskOptions.None);

            // Specify the input asset.
            task.InputAssets.Add(asset);

            // Add an output asset to contain the results of the job.
            task.OutputAssets.AddNew("My Face Redaction Output Asset", AssetCreationOptions.None);

            // Use the following event handler to check job progress.  
            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

            // Launch the job.
            job.Submit();

            // Check job execution and wait for job to finish.
            Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

            progressJobTask.Wait();

            // If job state is Error, the event handling
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

## <a name="next-steps"></a><span data-ttu-id="cf27f-215">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cf27f-215">Next steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="cf27f-216">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="cf27f-216">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="cf27f-217">Collegamenti correlati</span><span class="sxs-lookup"><span data-stu-id="cf27f-217">Related links</span></span>
[<span data-ttu-id="cf27f-218">Panoramica di Analisi servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="cf27f-218">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="cf27f-219">Demo di Analisi servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="cf27f-219">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

