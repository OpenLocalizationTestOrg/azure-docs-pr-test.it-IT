---
title: aaaDetect faccia ed emozioni con Azure Media Analitica | Documenti Microsoft
description: "In questo argomento viene illustrato come è rivolto toodetect ed emozioni con Azure Media Analitica."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5ca4692c-23f1-451d-9d82-cbc8bf0fd707
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/18/2017
ms.author: milanga;juliako;
ms.openlocfilehash: f58d81d82dde08a694cdb4d92c6bab6a40a9c157
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="detect-face-and-emotion-with-azure-media-analytics"></a><span data-ttu-id="0591e-103">Rilevare volti ed emozioni con Analisi servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="0591e-103">Detect Face and Emotion with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="0591e-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="0591e-104">Overview</span></span>
<span data-ttu-id="0591e-105">Hello **Azure Media faccia Rilevatore** processore di contenuti multimediali (MP) consente di toocount, i movimenti di avanzamento e anche la partecipazione di destinatari misuratore e reazione tramite facciale.</span><span class="sxs-lookup"><span data-stu-id="0591e-105">hello **Azure Media Face Detector** media processor (MP) enables you toocount, track movements, and even gauge audience participation and reaction via facial expressions.</span></span> <span data-ttu-id="0591e-106">Questo servizio contiene due funzionalità:</span><span class="sxs-lookup"><span data-stu-id="0591e-106">This service contains two features:</span></span> 

* <span data-ttu-id="0591e-107">**Rilevamento volti**</span><span class="sxs-lookup"><span data-stu-id="0591e-107">**Face detection**</span></span>
  
    <span data-ttu-id="0591e-108">Il Rilevamento volti rileva e monitora i volti umani all'interno di un video.</span><span class="sxs-lookup"><span data-stu-id="0591e-108">Face detection finds and tracks human faces within a video.</span></span> <span data-ttu-id="0591e-109">Più caratteri tipografici possono essere rilevati e successivamente essere rilevate man mano che vengono spostati, con hello ora e il percorso dei metadati restituiti in un file JSON.</span><span class="sxs-lookup"><span data-stu-id="0591e-109">Multiple faces can be detected and subsequently be tracked as they move around, with hello time and location metadata returned in a JSON file.</span></span> <span data-ttu-id="0591e-110">Durante il rilevamento, verrà eseguito un tentativo toogive un toohello ID coerenza stesso faccia mentre persona hello è spostamento sullo schermo, anche se è nascosto o lasciare brevemente il frame di hello.</span><span class="sxs-lookup"><span data-stu-id="0591e-110">During tracking, it will attempt toogive a consistent ID toohello same face while hello person is moving around on screen, even if they are obstructed or briefly leave hello frame.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="0591e-111">Questo servizio non esegue il riconoscimento facciale.</span><span class="sxs-lookup"><span data-stu-id="0591e-111">This service does not perform facial recognition.</span></span> <span data-ttu-id="0591e-112">Persona che lascia frame hello o diventa nascosto per troppo tempo verrà assegnato un nuovo ID quando viene restituita.</span><span class="sxs-lookup"><span data-stu-id="0591e-112">An individual who leaves hello frame or becomes obstructed for too long will be given a new ID when they return.</span></span>
  > 
  > 
* <span data-ttu-id="0591e-113">**Rilevamento emozioni**</span><span class="sxs-lookup"><span data-stu-id="0591e-113">**Emotion detection**</span></span>
  
    <span data-ttu-id="0591e-114">Rilevamento emozioni è un componente facoltativo di hello processore di contenuti multimediali di rilevamento viso restituisce analisi su più attributi affettivi da facce hello rilevate, tra cui "Happiness", sadness, paura, anger e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="0591e-114">Emotion Detection is an optional component of hello Face Detection Media Processor that returns analysis on multiple emotional attributes from hello faces detected, including happiness, sadness, fear, anger, and more.</span></span> 

<span data-ttu-id="0591e-115">Hello **Azure Media faccia Rilevatore** Management Pack è attualmente in anteprima.</span><span class="sxs-lookup"><span data-stu-id="0591e-115">hello **Azure Media Face Detector** MP is currently in Preview.</span></span>

<span data-ttu-id="0591e-116">In questo argomento fornisce informazioni dettagliate sulle **Azure Media faccia Rilevatore** e Mostra come toouse con Media Services SDK per .NET.</span><span class="sxs-lookup"><span data-stu-id="0591e-116">This topic gives details about  **Azure Media Face Detector** and shows how toouse it with Media Services SDK for .NET.</span></span>

## <a name="face-detector-input-files"></a><span data-ttu-id="0591e-117">File di input di Rilevamento volti</span><span class="sxs-lookup"><span data-stu-id="0591e-117">Face Detector input files</span></span>
<span data-ttu-id="0591e-118">File video.</span><span class="sxs-lookup"><span data-stu-id="0591e-118">Video files.</span></span> <span data-ttu-id="0591e-119">Attualmente, è supportato i seguenti formati hello: MOV o MP4 e WMV.</span><span class="sxs-lookup"><span data-stu-id="0591e-119">Currently, hello following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="face-detector-output-files"></a><span data-ttu-id="0591e-120">File di output di Rilevamento volti</span><span class="sxs-lookup"><span data-stu-id="0591e-120">Face Detector output files</span></span>
<span data-ttu-id="0591e-121">API di rilevamento e il rilevamento di faccia Hello fornisce il rilevamento di percorso faccia ad alta precisione e il rilevamento in grado di rilevare il too64 viso umana in un video.</span><span class="sxs-lookup"><span data-stu-id="0591e-121">hello face detection and tracking API provides high precision face location detection and tracking that can detect up too64 human faces in a video.</span></span> <span data-ttu-id="0591e-122">Volti frontali forniscono risultati ottimali hello, mentre i caratteri tipografici lato e facce di piccole dimensioni (minore o uguale a too24x24 pixel) potrebbe non essere accurata.</span><span class="sxs-lookup"><span data-stu-id="0591e-122">Frontal faces provide hello best results, while side faces and small faces (less than or equal too24x24 pixels) might not be as accurate.</span></span>

<span data-ttu-id="0591e-123">Hello facce rilevate e di rilevamento vengono restituite con le coordinate (sinistro, superiore, larghezza e altezza) che indica la posizione hello di facce nell'immagine di hello in pixel, nonché di un viso ID numerico che indica il rilevamento di tale persona hello.</span><span class="sxs-lookup"><span data-stu-id="0591e-123">hello detected and tracked faces are returned with coordinates (left, top, width, and height) indicating hello location of faces in hello image in pixels, as well as a face ID number indicating hello tracking of that individual.</span></span> <span data-ttu-id="0591e-124">Numeri di ID tipo di carattere sono tooreset soggetta a circostanze quando frontale hello viene smarrito o sovrapposta nel frame hello, risultante in alcune persone più ID di assegnazione.</span><span class="sxs-lookup"><span data-stu-id="0591e-124">Face ID numbers are prone tooreset under circumstances when hello frontal face is lost or overlapped in hello frame, resulting in some individuals getting assigned multiple IDs.</span></span>

## <span data-ttu-id="0591e-125"><a id="output_elements"></a>Elementi hello JSON del file di output</span><span class="sxs-lookup"><span data-stu-id="0591e-125"><a id="output_elements"></a>Elements of hello output JSON file</span></span>

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

<span data-ttu-id="0591e-126">Rilevatore faccia utilizza tecniche di frammentazione (in cui i metadati di hello possono essere suddiviso in blocchi basati sul tempo ed è possibile scaricare solo gli elementi necessari) e la segmentazione (in cui gli eventi di hello sono suddivise in caso di ricevono troppo grande).</span><span class="sxs-lookup"><span data-stu-id="0591e-126">Face Detector uses techniques of fragmentation (where hello metadata can be broken up in time-based chunks and you can download only what you need), and segmentation (where hello events are broken up in case they get too large).</span></span> <span data-ttu-id="0591e-127">Alcune semplici calcoli consentono di trasformare i dati di hello.</span><span class="sxs-lookup"><span data-stu-id="0591e-127">Some simple calculations can help you transform hello data.</span></span> <span data-ttu-id="0591e-128">Se ad esempio un evento è iniziato in corrispondenza di 6300 (scatti), con una scala cronologica di 2997 (scatti al secondo) e una frequenza di fotogrammi di 29,97 (fotogrammi al secondo):</span><span class="sxs-lookup"><span data-stu-id="0591e-128">For example, if an event started at 6300 (ticks), with a timescale of 2997 (ticks/sec) and framerate of 29.97 (frames/sec), then:</span></span>

* <span data-ttu-id="0591e-129">Inizio/Scala cronologica = 2,1 secondi</span><span class="sxs-lookup"><span data-stu-id="0591e-129">Start/Timescale = 2.1 seconds</span></span>
* <span data-ttu-id="0591e-130">Secondi x frequenza di fotogrammi = 63 fotogrammi</span><span class="sxs-lookup"><span data-stu-id="0591e-130">Seconds x Framerate = 63 frames</span></span>

## <a name="face-detection-input-and-output-example"></a><span data-ttu-id="0591e-131">Esempio di input e output di rilevamento volti</span><span class="sxs-lookup"><span data-stu-id="0591e-131">Face detection input and output example</span></span>
### <a name="input-video"></a><span data-ttu-id="0591e-132">Video di input</span><span class="sxs-lookup"><span data-stu-id="0591e-132">Input video</span></span>
[<span data-ttu-id="0591e-133">Video di input</span><span class="sxs-lookup"><span data-stu-id="0591e-133">Input Video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a><span data-ttu-id="0591e-134">Configurazione delle attività (set di impostazioni)</span><span class="sxs-lookup"><span data-stu-id="0591e-134">Task configuration (preset)</span></span>
<span data-ttu-id="0591e-135">Quando si crea un'attività con **Rilevamento multimediale volti di Azure**, è necessario specificare un set di impostazioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="0591e-135">When creating a task with **Azure Media Face Detector**, you must specify a configuration preset.</span></span> <span data-ttu-id="0591e-136">Hello seguente set di impostazioni di configurazione è solo per il rilevamento di tipo di carattere.</span><span class="sxs-lookup"><span data-stu-id="0591e-136">hello following configuration preset is just for face detection.</span></span>

    {
      "version":"1.0",
      "options":{
          "TrackingMode": "Fast"
      }
    }

#### <a name="attribute-descriptions"></a><span data-ttu-id="0591e-137">Descrizioni degli attributi</span><span class="sxs-lookup"><span data-stu-id="0591e-137">Attribute descriptions</span></span>
| <span data-ttu-id="0591e-138">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="0591e-138">Attribute name</span></span> | <span data-ttu-id="0591e-139">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0591e-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0591e-140">Mode</span><span class="sxs-lookup"><span data-stu-id="0591e-140">Mode</span></span> |<span data-ttu-id="0591e-141">Fast: velocità di elaborazione elevata, ma meno accurata (impostazione predefinita).</span><span class="sxs-lookup"><span data-stu-id="0591e-141">Fast - fast processing speed, but less accurate (default).</span></span>|

### <a name="json-output"></a><span data-ttu-id="0591e-142">Output JSON</span><span class="sxs-lookup"><span data-stu-id="0591e-142">JSON output</span></span>
<span data-ttu-id="0591e-143">esempio dell'output JSON seguente Hello è stato troncato.</span><span class="sxs-lookup"><span data-stu-id="0591e-143">hello following example of JSON output was truncated.</span></span>

    {
    "version": 1,
    "timescale": 30000,
    "offset": 0,
    "framerate": 29.97,
    "width": 1280,
    "height": 720,
    "fragments": [
        {
        "start": 0,
        "duration": 60060
        },
        {
        "start": 60060,
        "duration": 60060,
        "interval": 1001,
        "events": [
            [
            {
                "id": 0,
                "x": 0.519531,
                "y": 0.180556,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517969,
                "y": 0.181944,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517187,
                "y": 0.183333,
                "width": 0.0851562,
                "height": 0.151389
            }
            ],

        . . . 

## <a name="emotion-detection-input-and-output-example"></a><span data-ttu-id="0591e-144">Esempio di input e output di Rilevamento emozioni</span><span class="sxs-lookup"><span data-stu-id="0591e-144">Emotion detection input and output example</span></span>
### <a name="input-video"></a><span data-ttu-id="0591e-145">Video di input</span><span class="sxs-lookup"><span data-stu-id="0591e-145">Input video</span></span>
[<span data-ttu-id="0591e-146">Video di input</span><span class="sxs-lookup"><span data-stu-id="0591e-146">Input Video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a><span data-ttu-id="0591e-147">Configurazione delle attività (set di impostazioni)</span><span class="sxs-lookup"><span data-stu-id="0591e-147">Task configuration (preset)</span></span>
<span data-ttu-id="0591e-148">Quando si crea un'attività con **Rilevamento multimediale volti di Azure**, è necessario specificare un set di impostazioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="0591e-148">When creating a task with **Azure Media Face Detector**, you must specify a configuration preset.</span></span> <span data-ttu-id="0591e-149">Hello seguente set di impostazioni di configurazione specifica toocreate che JSON basato sul rilevamento emozioni hello.</span><span class="sxs-lookup"><span data-stu-id="0591e-149">hello following configuration preset specifies toocreate JSON based on hello emotion detection.</span></span>

    {
      "version": "1.0",
      "options": {
        "aggregateEmotionWindowMs": "987",
        "mode": "aggregateEmotion",
        "aggregateEmotionIntervalMs": "342"
      }
    }


#### <a name="attribute-descriptions"></a><span data-ttu-id="0591e-150">Descrizioni degli attributi</span><span class="sxs-lookup"><span data-stu-id="0591e-150">Attribute descriptions</span></span>
| <span data-ttu-id="0591e-151">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="0591e-151">Attribute name</span></span> | <span data-ttu-id="0591e-152">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0591e-152">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0591e-153">Mode</span><span class="sxs-lookup"><span data-stu-id="0591e-153">Mode</span></span> |<span data-ttu-id="0591e-154">Faces: solo rilevamento viso.</span><span class="sxs-lookup"><span data-stu-id="0591e-154">Faces: Only face detection.</span></span><br/><span data-ttu-id="0591e-155">PerFaceEmotion: restituisce un'emozione in modo indipendente per ogni rilevamento viso.</span><span class="sxs-lookup"><span data-stu-id="0591e-155">PerFaceEmotion: Return emotion independently for each face detection.</span></span><br/><span data-ttu-id="0591e-156">AggregateEmotion: restituzione dei valori medi delle emozioni per tutti i volti nel fotogramma.</span><span class="sxs-lookup"><span data-stu-id="0591e-156">AggregateEmotion: Return average emotion values for all faces in frame.</span></span> |
| <span data-ttu-id="0591e-157">AggregateEmotionWindowMs</span><span class="sxs-lookup"><span data-stu-id="0591e-157">AggregateEmotionWindowMs</span></span> |<span data-ttu-id="0591e-158">Va usato se è selezionata la modalità AggregateEmotion.</span><span class="sxs-lookup"><span data-stu-id="0591e-158">Use if AggregateEmotion mode selected.</span></span> <span data-ttu-id="0591e-159">Specifica il periodo di hello del video tooproduce usato ogni risultato aggregato, in millisecondi.</span><span class="sxs-lookup"><span data-stu-id="0591e-159">Specifies hello length of video used tooproduce each aggregate result, in milliseconds.</span></span> |
| <span data-ttu-id="0591e-160">AggregateEmotionIntervalMs</span><span class="sxs-lookup"><span data-stu-id="0591e-160">AggregateEmotionIntervalMs</span></span> |<span data-ttu-id="0591e-161">Va usato se è selezionata la modalità AggregateEmotion.</span><span class="sxs-lookup"><span data-stu-id="0591e-161">Use if AggregateEmotion mode selected.</span></span> <span data-ttu-id="0591e-162">Specifica con quale aggregazione tooproduce frequenza risultati.</span><span class="sxs-lookup"><span data-stu-id="0591e-162">Specifies with what frequency tooproduce aggregate results.</span></span> |

#### <a name="aggregate-defaults"></a><span data-ttu-id="0591e-163">Impostazioni predefinite degli aggregati</span><span class="sxs-lookup"><span data-stu-id="0591e-163">Aggregate defaults</span></span>
<span data-ttu-id="0591e-164">Di seguito sono consigliati i valori per la finestra di aggregazione hello e le impostazioni dell'intervallo.</span><span class="sxs-lookup"><span data-stu-id="0591e-164">Below are recommended values for hello aggregate window and interval settings.</span></span> <span data-ttu-id="0591e-165">Il valore di AggregateEmotionWindowMs non deve essere maggiore del valore di AggregateEmotionIntervalMs.</span><span class="sxs-lookup"><span data-stu-id="0591e-165">AggregateEmotionWindowMs should be longer than AggregateEmotionIntervalMs.</span></span>

|| <span data-ttu-id="0591e-166">Impostazioni predefinite</span><span class="sxs-lookup"><span data-stu-id="0591e-166">Defaults(s)</span></span> | <span data-ttu-id="0591e-167">Min(s)</span><span class="sxs-lookup"><span data-stu-id="0591e-167">Min(s)</span></span> | <span data-ttu-id="0591e-168">Max(s)</span><span class="sxs-lookup"><span data-stu-id="0591e-168">Max(s)</span></span> |
|--- | --- | --- | --- |
| <span data-ttu-id="0591e-169">AggregateEmotionWindowMs</span><span class="sxs-lookup"><span data-stu-id="0591e-169">AggregateEmotionWindowMs</span></span> |<span data-ttu-id="0591e-170">0,5</span><span class="sxs-lookup"><span data-stu-id="0591e-170">0.5</span></span> |<span data-ttu-id="0591e-171">2</span><span class="sxs-lookup"><span data-stu-id="0591e-171">2</span></span> |<span data-ttu-id="0591e-172">0,25</span><span class="sxs-lookup"><span data-stu-id="0591e-172">0.25</span></span>|
| <span data-ttu-id="0591e-173">AggregateEmotionIntervalMs</span><span class="sxs-lookup"><span data-stu-id="0591e-173">AggregateEmotionIntervalMs</span></span> |<span data-ttu-id="0591e-174">0,5</span><span class="sxs-lookup"><span data-stu-id="0591e-174">0.5</span></span> |<span data-ttu-id="0591e-175">1</span><span class="sxs-lookup"><span data-stu-id="0591e-175">1</span></span> |<span data-ttu-id="0591e-176">0,25</span><span class="sxs-lookup"><span data-stu-id="0591e-176">0.25</span></span>|

### <a name="json-output"></a><span data-ttu-id="0591e-177">Output JSON</span><span class="sxs-lookup"><span data-stu-id="0591e-177">JSON output</span></span>
<span data-ttu-id="0591e-178">Output JSON per l'emozione aggregata (troncato):</span><span class="sxs-lookup"><span data-stu-id="0591e-178">JSON output for aggregate emotion (truncated):</span></span>

    {
     "version": 1,
     "timescale": 30000,
     "offset": 0,
     "framerate": 29.97,
     "width": 1280,
     "height": 720,
     "fragments": [
       {
         "start": 0,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ]
         ]
       },
       {
         "start": 60060,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0.688541,
                 "happiness": 0.0586323,
                 "surprise": 0.227184,
                 "sadness": 0.00945675,
                 "anger": 0.00592107,
                 "disgust": 0.00154993,
                 "fear": 0.00450447,
                 "contempt": 0.0042109
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,

## <a name="limitations"></a><span data-ttu-id="0591e-179">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="0591e-179">Limitations</span></span>
* <span data-ttu-id="0591e-180">formati video input Hello supportato includono MP4, MOV e WMV.</span><span class="sxs-lookup"><span data-stu-id="0591e-180">hello supported input video formats include MP4, MOV, and WMV.</span></span>
* <span data-ttu-id="0591e-181">intervallo di dimensioni faccia rilevabili Hello è too2048x2048 24 x 24 pixel.</span><span class="sxs-lookup"><span data-stu-id="0591e-181">hello detectable face size range is 24x24 too2048x2048 pixels.</span></span> <span data-ttu-id="0591e-182">i caratteri tipografici Hello da questo intervallo non venga rilevati.</span><span class="sxs-lookup"><span data-stu-id="0591e-182">hello faces out of this range will not be detected.</span></span>
* <span data-ttu-id="0591e-183">Per ogni video, numero massimo di hello di facce restituito è 64.</span><span class="sxs-lookup"><span data-stu-id="0591e-183">For each video, hello maximum number of faces returned is 64.</span></span>
* <span data-ttu-id="0591e-184">Non è possibile rilevare alcuni volti a causa di problemi di tootechnical; ad esempio grandi faccia angoli (head-posa) e occlusione di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="0591e-184">Some faces may not be detected due tootechnical challenges; e.g. very large face angles (head-pose), and large occlusion.</span></span> <span data-ttu-id="0591e-185">Volti frontali e di prossimità anteriore avere risultati migliori hello.</span><span class="sxs-lookup"><span data-stu-id="0591e-185">Frontal and near-frontal faces have hello best results.</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="0591e-186">Codice di esempio .NET</span><span class="sxs-lookup"><span data-stu-id="0591e-186">.NET sample code</span></span>

<span data-ttu-id="0591e-187">esempio Hello programma mostra come:</span><span class="sxs-lookup"><span data-stu-id="0591e-187">hello following program shows how to:</span></span>

1. <span data-ttu-id="0591e-188">Creare un asset e caricare un file multimediale nell'asset hello.</span><span class="sxs-lookup"><span data-stu-id="0591e-188">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="0591e-189">Creare un processo con un'attività di rilevamento viso in base a un file di configurazione che contiene i seguenti set di impostazioni json hello.</span><span class="sxs-lookup"><span data-stu-id="0591e-189">Create a job with a face detection task based on a configuration file that contains hello following json preset.</span></span> 
   
        {
            "version": "1.0"
        }
3. <span data-ttu-id="0591e-190">Scaricare i file JSON di output di hello.</span><span class="sxs-lookup"><span data-stu-id="0591e-190">Download hello output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="0591e-191">Creare e configurare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0591e-191">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="0591e-192">Configurare l'ambiente di sviluppo e di popolare il file app. config hello con informazioni di connessione, come descritto in [lo sviluppo di servizi multimediali con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="0591e-192">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="0591e-193">Esempio</span><span class="sxs-lookup"><span data-stu-id="0591e-193">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace FaceDetection
    {
        class Program
        {
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

                // Run hello FaceDetection job.
                var asset = RunFaceDetectionJob(@"C:\supportFiles\FaceDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\FaceDetection\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\FaceDetection\Output");
            }

            static IAsset RunFaceDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Face Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Face Detection Job");

                // Get a reference tooAzure Media Face Detector.
                string MediaProcessorName = "Azure Media Face Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Face Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Face Detectoion Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="0591e-194">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="0591e-194">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0591e-195">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="0591e-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="0591e-196">Collegamenti correlati</span><span class="sxs-lookup"><span data-stu-id="0591e-196">Related links</span></span>
[<span data-ttu-id="0591e-197">Panoramica di Analisi servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="0591e-197">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="0591e-198">Demo di Analisi servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="0591e-198">Azure Media Analytics demos</span></span>](http://amslabs.azurewebsites.net/demos/Analytics.html)

