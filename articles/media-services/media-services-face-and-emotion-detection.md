---
title: Rilevare volti ed emozioni con Analisi Servizi multimediali di Azure | Microsoft Docs
description: Questo argomento illustra come rilevare volti ed emozioni con Analisi Servizi multimediali di Azure.
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
ms.openlocfilehash: d7f3bc6c0d21db7adbb0c16c752d4ce49e99da5a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="detect-face-and-emotion-with-azure-media-analytics"></a><span data-ttu-id="7abad-103">Rilevare volti ed emozioni con Analisi servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="7abad-103">Detect Face and Emotion with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="7abad-104">Overview</span><span class="sxs-lookup"><span data-stu-id="7abad-104">Overview</span></span>
<span data-ttu-id="7abad-105">Il processore di contenuti multimediali **Rilevamento multimediale volti di Azure** consente di contare, monitorare i movimenti e persino di valutare la partecipazione e le reazioni del pubblico in base alle espressioni del volto.</span><span class="sxs-lookup"><span data-stu-id="7abad-105">The **Azure Media Face Detector** media processor (MP) enables you to count, track movements, and even gauge audience participation and reaction via facial expressions.</span></span> <span data-ttu-id="7abad-106">Questo servizio contiene due funzionalità:</span><span class="sxs-lookup"><span data-stu-id="7abad-106">This service contains two features:</span></span> 

* <span data-ttu-id="7abad-107">**Rilevamento volti**</span><span class="sxs-lookup"><span data-stu-id="7abad-107">**Face detection**</span></span>
  
    <span data-ttu-id="7abad-108">Il Rilevamento volti rileva e monitora i volti umani all'interno di un video.</span><span class="sxs-lookup"><span data-stu-id="7abad-108">Face detection finds and tracks human faces within a video.</span></span> <span data-ttu-id="7abad-109">È possibile rilevare e monitorare diversi volti mentre le persone si muovono; i metadati relativi a ora e luogo vengono restituiti in un file JSON.</span><span class="sxs-lookup"><span data-stu-id="7abad-109">Multiple faces can be detected and subsequently be tracked as they move around, with the time and location metadata returned in a JSON file.</span></span> <span data-ttu-id="7abad-110">Durante il monitoraggio, il sistema tenterà di assegnare sempre lo stesso ID al volto mentre la persona si muove sullo schermo, anche se è nascosta o se esce brevemente dall'inquadratura.</span><span class="sxs-lookup"><span data-stu-id="7abad-110">During tracking, it will attempt to give a consistent ID to the same face while the person is moving around on screen, even if they are obstructed or briefly leave the frame.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="7abad-111">Questo servizio non esegue il riconoscimento facciale.</span><span class="sxs-lookup"><span data-stu-id="7abad-111">This service does not perform facial recognition.</span></span> <span data-ttu-id="7abad-112">Se una persona esce dall'inquadratura o viene nascosta troppo a lungo, al suo ritorno le verrà assegnato un nuovo ID.</span><span class="sxs-lookup"><span data-stu-id="7abad-112">An individual who leaves the frame or becomes obstructed for too long will be given a new ID when they return.</span></span>
  > 
  > 
* <span data-ttu-id="7abad-113">**Rilevamento emozioni**</span><span class="sxs-lookup"><span data-stu-id="7abad-113">**Emotion detection**</span></span>
  
    <span data-ttu-id="7abad-114">Il Rilevamento emozioni è un componente facoltativo del Processore multimediale di rilevamento volti che restituisce un'analisi di vari attributi emotivi dei volti rilevati, inclusi la felicità, la paura, la tristezza, la rabbia e altre emozioni.</span><span class="sxs-lookup"><span data-stu-id="7abad-114">Emotion Detection is an optional component of the Face Detection Media Processor that returns analysis on multiple emotional attributes from the faces detected, including happiness, sadness, fear, anger, and more.</span></span> 

<span data-ttu-id="7abad-115">Attualmente il processore multimediale **Rilevamento multimediale volti di Azure** è disponibile in Anteprima.</span><span class="sxs-lookup"><span data-stu-id="7abad-115">The **Azure Media Face Detector** MP is currently in Preview.</span></span>

<span data-ttu-id="7abad-116">Questo argomento contiene informazioni dettagliate su **Azure Media Face Detector** e illustra come usare questa funzionalità con Media Services .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="7abad-116">This topic gives details about  **Azure Media Face Detector** and shows how to use it with Media Services SDK for .NET.</span></span>

## <a name="face-detector-input-files"></a><span data-ttu-id="7abad-117">File di input di Rilevamento volti</span><span class="sxs-lookup"><span data-stu-id="7abad-117">Face Detector input files</span></span>
<span data-ttu-id="7abad-118">File video.</span><span class="sxs-lookup"><span data-stu-id="7abad-118">Video files.</span></span> <span data-ttu-id="7abad-119">Attualmente sono supportati i formati seguenti: MP4, MOV e WMV.</span><span class="sxs-lookup"><span data-stu-id="7abad-119">Currently, the following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="face-detector-output-files"></a><span data-ttu-id="7abad-120">File di output di Rilevamento volti</span><span class="sxs-lookup"><span data-stu-id="7abad-120">Face Detector output files</span></span>
<span data-ttu-id="7abad-121">L'API per il rilevamento e monitoraggio volti offre il rilevamento e il monitoraggio volti ad alta precisione ed è in grado di rilevare fino a 64 volti umani in un video.</span><span class="sxs-lookup"><span data-stu-id="7abad-121">The face detection and tracking API provides high precision face location detection and tracking that can detect up to 64 human faces in a video.</span></span> <span data-ttu-id="7abad-122">Le riprese anteriori producono i risultati migliori, mentre i profili e i volti piccoli (inferiori o uguali a 24x24 pixel) non garantiscono altrettanta precisione.</span><span class="sxs-lookup"><span data-stu-id="7abad-122">Frontal faces provide the best results, while side faces and small faces (less than or equal to 24x24 pixels) might not be as accurate.</span></span>

<span data-ttu-id="7abad-123">I volti rilevati e monitorati vengono restituiti con coordinate (sinistra, superiore, larghezza e altezza) indicanti la posizione dei volti nell'immagine in pixel e un codice ID del volto che indica il monitoraggio della persona.</span><span class="sxs-lookup"><span data-stu-id="7abad-123">The detected and tracked faces are returned with coordinates (left, top, width, and height) indicating the location of faces in the image in pixels, as well as a face ID number indicating the tracking of that individual.</span></span> <span data-ttu-id="7abad-124">I codici ID del volto sono soggetti a ripristino quando le riprese non sono frontali o sono sovrapposte nel fotogramma, causando l'assegnazione di diversi ID alla stessa persona.</span><span class="sxs-lookup"><span data-stu-id="7abad-124">Face ID numbers are prone to reset under circumstances when the frontal face is lost or overlapped in the frame, resulting in some individuals getting assigned multiple IDs.</span></span>

## <span data-ttu-id="7abad-125"><a id="output_elements"></a>Elementi del file di output JSON</span><span class="sxs-lookup"><span data-stu-id="7abad-125"><a id="output_elements"></a>Elements of the output JSON file</span></span>

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

<span data-ttu-id="7abad-126">Il rilevatore di volti usa tecniche di frammentazione, che consentono di suddividere i metadati in blocchi basati sul tempo e di scaricare solo gli elementi necessari, e di segmentazione, che consentono di suddividere gli eventi se diventano troppo grandi.</span><span class="sxs-lookup"><span data-stu-id="7abad-126">Face Detector uses techniques of fragmentation (where the metadata can be broken up in time-based chunks and you can download only what you need), and segmentation (where the events are broken up in case they get too large).</span></span> <span data-ttu-id="7abad-127">Alcuni semplici calcoli consentono di trasformare i dati.</span><span class="sxs-lookup"><span data-stu-id="7abad-127">Some simple calculations can help you transform the data.</span></span> <span data-ttu-id="7abad-128">Se ad esempio un evento è iniziato in corrispondenza di 6300 (scatti), con una scala cronologica di 2997 (scatti al secondo) e una frequenza di fotogrammi di 29,97 (fotogrammi al secondo):</span><span class="sxs-lookup"><span data-stu-id="7abad-128">For example, if an event started at 6300 (ticks), with a timescale of 2997 (ticks/sec) and framerate of 29.97 (frames/sec), then:</span></span>

* <span data-ttu-id="7abad-129">Inizio/Scala cronologica = 2,1 secondi</span><span class="sxs-lookup"><span data-stu-id="7abad-129">Start/Timescale = 2.1 seconds</span></span>
* <span data-ttu-id="7abad-130">Secondi x frequenza di fotogrammi = 63 fotogrammi</span><span class="sxs-lookup"><span data-stu-id="7abad-130">Seconds x Framerate = 63 frames</span></span>

## <a name="face-detection-input-and-output-example"></a><span data-ttu-id="7abad-131">Esempio di input e output di rilevamento volti</span><span class="sxs-lookup"><span data-stu-id="7abad-131">Face detection input and output example</span></span>
### <a name="input-video"></a><span data-ttu-id="7abad-132">Video di input</span><span class="sxs-lookup"><span data-stu-id="7abad-132">Input video</span></span>
[<span data-ttu-id="7abad-133">Video di input</span><span class="sxs-lookup"><span data-stu-id="7abad-133">Input Video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a><span data-ttu-id="7abad-134">Configurazione delle attività (set di impostazioni)</span><span class="sxs-lookup"><span data-stu-id="7abad-134">Task configuration (preset)</span></span>
<span data-ttu-id="7abad-135">Quando si crea un'attività con **Rilevamento multimediale volti di Azure**, è necessario specificare un set di impostazioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="7abad-135">When creating a task with **Azure Media Face Detector**, you must specify a configuration preset.</span></span> <span data-ttu-id="7abad-136">Il set di impostazioni di configurazione seguente serve unicamente per il rilevamento volti.</span><span class="sxs-lookup"><span data-stu-id="7abad-136">The following configuration preset is just for face detection.</span></span>

    {
      "version":"1.0",
      "options":{
          "TrackingMode": "Fast"
      }
    }

#### <a name="attribute-descriptions"></a><span data-ttu-id="7abad-137">Descrizioni degli attributi</span><span class="sxs-lookup"><span data-stu-id="7abad-137">Attribute descriptions</span></span>
| <span data-ttu-id="7abad-138">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="7abad-138">Attribute name</span></span> | <span data-ttu-id="7abad-139">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7abad-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7abad-140">Mode</span><span class="sxs-lookup"><span data-stu-id="7abad-140">Mode</span></span> |<span data-ttu-id="7abad-141">Fast: velocità di elaborazione elevata, ma meno accurata (impostazione predefinita).</span><span class="sxs-lookup"><span data-stu-id="7abad-141">Fast - fast processing speed, but less accurate (default).</span></span>|

### <a name="json-output"></a><span data-ttu-id="7abad-142">Output JSON</span><span class="sxs-lookup"><span data-stu-id="7abad-142">JSON output</span></span>
<span data-ttu-id="7abad-143">L'esempio seguente di output JSON è stato troncato.</span><span class="sxs-lookup"><span data-stu-id="7abad-143">The following example of JSON output was truncated.</span></span>

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

## <a name="emotion-detection-input-and-output-example"></a><span data-ttu-id="7abad-144">Esempio di input e output di Rilevamento emozioni</span><span class="sxs-lookup"><span data-stu-id="7abad-144">Emotion detection input and output example</span></span>
### <a name="input-video"></a><span data-ttu-id="7abad-145">Video di input</span><span class="sxs-lookup"><span data-stu-id="7abad-145">Input video</span></span>
[<span data-ttu-id="7abad-146">Video di input</span><span class="sxs-lookup"><span data-stu-id="7abad-146">Input Video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a><span data-ttu-id="7abad-147">Configurazione delle attività (set di impostazioni)</span><span class="sxs-lookup"><span data-stu-id="7abad-147">Task configuration (preset)</span></span>
<span data-ttu-id="7abad-148">Quando si crea un'attività con **Rilevamento multimediale volti di Azure**, è necessario specificare un set di impostazioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="7abad-148">When creating a task with **Azure Media Face Detector**, you must specify a configuration preset.</span></span> <span data-ttu-id="7abad-149">Il set di impostazioni di configurazione seguente specifica la creazione del file JSON in base al Rilevamento emozioni.</span><span class="sxs-lookup"><span data-stu-id="7abad-149">The following configuration preset specifies to create JSON based on the emotion detection.</span></span>

    {
      "version": "1.0",
      "options": {
        "aggregateEmotionWindowMs": "987",
        "mode": "aggregateEmotion",
        "aggregateEmotionIntervalMs": "342"
      }
    }


#### <a name="attribute-descriptions"></a><span data-ttu-id="7abad-150">Descrizioni degli attributi</span><span class="sxs-lookup"><span data-stu-id="7abad-150">Attribute descriptions</span></span>
| <span data-ttu-id="7abad-151">Nome attributo</span><span class="sxs-lookup"><span data-stu-id="7abad-151">Attribute name</span></span> | <span data-ttu-id="7abad-152">Descrizione</span><span class="sxs-lookup"><span data-stu-id="7abad-152">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7abad-153">Mode</span><span class="sxs-lookup"><span data-stu-id="7abad-153">Mode</span></span> |<span data-ttu-id="7abad-154">Faces: solo rilevamento viso.</span><span class="sxs-lookup"><span data-stu-id="7abad-154">Faces: Only face detection.</span></span><br/><span data-ttu-id="7abad-155">PerFaceEmotion: restituisce un'emozione in modo indipendente per ogni rilevamento viso.</span><span class="sxs-lookup"><span data-stu-id="7abad-155">PerFaceEmotion: Return emotion independently for each face detection.</span></span><br/><span data-ttu-id="7abad-156">AggregateEmotion: restituzione dei valori medi delle emozioni per tutti i volti nel fotogramma.</span><span class="sxs-lookup"><span data-stu-id="7abad-156">AggregateEmotion: Return average emotion values for all faces in frame.</span></span> |
| <span data-ttu-id="7abad-157">AggregateEmotionWindowMs</span><span class="sxs-lookup"><span data-stu-id="7abad-157">AggregateEmotionWindowMs</span></span> |<span data-ttu-id="7abad-158">Va usato se è selezionata la modalità AggregateEmotion.</span><span class="sxs-lookup"><span data-stu-id="7abad-158">Use if AggregateEmotion mode selected.</span></span> <span data-ttu-id="7abad-159">Specifica la lunghezza del video usato per produrre ogni risultato aggregato, in millisecondi.</span><span class="sxs-lookup"><span data-stu-id="7abad-159">Specifies the length of video used to produce each aggregate result, in milliseconds.</span></span> |
| <span data-ttu-id="7abad-160">AggregateEmotionIntervalMs</span><span class="sxs-lookup"><span data-stu-id="7abad-160">AggregateEmotionIntervalMs</span></span> |<span data-ttu-id="7abad-161">Va usato se è selezionata la modalità AggregateEmotion.</span><span class="sxs-lookup"><span data-stu-id="7abad-161">Use if AggregateEmotion mode selected.</span></span> <span data-ttu-id="7abad-162">Specifica con quale frequenza produrre risultati aggregati.</span><span class="sxs-lookup"><span data-stu-id="7abad-162">Specifies with what frequency to produce aggregate results.</span></span> |

#### <a name="aggregate-defaults"></a><span data-ttu-id="7abad-163">Impostazioni predefinite degli aggregati</span><span class="sxs-lookup"><span data-stu-id="7abad-163">Aggregate defaults</span></span>
<span data-ttu-id="7abad-164">Di seguito sono specificati i valori consigliati per la finestra di aggregazione e le impostazioni di intervallo.</span><span class="sxs-lookup"><span data-stu-id="7abad-164">Below are recommended values for the aggregate window and interval settings.</span></span> <span data-ttu-id="7abad-165">Il valore di AggregateEmotionWindowMs non deve essere maggiore del valore di AggregateEmotionIntervalMs.</span><span class="sxs-lookup"><span data-stu-id="7abad-165">AggregateEmotionWindowMs should be longer than AggregateEmotionIntervalMs.</span></span>

|| <span data-ttu-id="7abad-166">Impostazioni predefinite</span><span class="sxs-lookup"><span data-stu-id="7abad-166">Defaults(s)</span></span> | <span data-ttu-id="7abad-167">Min(s)</span><span class="sxs-lookup"><span data-stu-id="7abad-167">Min(s)</span></span> | <span data-ttu-id="7abad-168">Max(s)</span><span class="sxs-lookup"><span data-stu-id="7abad-168">Max(s)</span></span> |
|--- | --- | --- | --- |
| <span data-ttu-id="7abad-169">AggregateEmotionWindowMs</span><span class="sxs-lookup"><span data-stu-id="7abad-169">AggregateEmotionWindowMs</span></span> |<span data-ttu-id="7abad-170">0,5</span><span class="sxs-lookup"><span data-stu-id="7abad-170">0.5</span></span> |<span data-ttu-id="7abad-171">2</span><span class="sxs-lookup"><span data-stu-id="7abad-171">2</span></span> |<span data-ttu-id="7abad-172">0,25</span><span class="sxs-lookup"><span data-stu-id="7abad-172">0.25</span></span>|
| <span data-ttu-id="7abad-173">AggregateEmotionIntervalMs</span><span class="sxs-lookup"><span data-stu-id="7abad-173">AggregateEmotionIntervalMs</span></span> |<span data-ttu-id="7abad-174">0,5</span><span class="sxs-lookup"><span data-stu-id="7abad-174">0.5</span></span> |<span data-ttu-id="7abad-175">1</span><span class="sxs-lookup"><span data-stu-id="7abad-175">1</span></span> |<span data-ttu-id="7abad-176">0,25</span><span class="sxs-lookup"><span data-stu-id="7abad-176">0.25</span></span>|

### <a name="json-output"></a><span data-ttu-id="7abad-177">Output JSON</span><span class="sxs-lookup"><span data-stu-id="7abad-177">JSON output</span></span>
<span data-ttu-id="7abad-178">Output JSON per l'emozione aggregata (troncato):</span><span class="sxs-lookup"><span data-stu-id="7abad-178">JSON output for aggregate emotion (truncated):</span></span>

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

## <a name="limitations"></a><span data-ttu-id="7abad-179">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="7abad-179">Limitations</span></span>
* <span data-ttu-id="7abad-180">I formati video di input supportati includono MP4, MOV e WMV.</span><span class="sxs-lookup"><span data-stu-id="7abad-180">The supported input video formats include MP4, MOV, and WMV.</span></span>
* <span data-ttu-id="7abad-181">L'intervallo delle dimensioni rilevabili del volto è da 24x24 a 2048x2048 pixel.</span><span class="sxs-lookup"><span data-stu-id="7abad-181">The detectable face size range is 24x24 to 2048x2048 pixels.</span></span> <span data-ttu-id="7abad-182">I volti al di fuori di questo intervallo non vengono rilevati.</span><span class="sxs-lookup"><span data-stu-id="7abad-182">The faces out of this range will not be detected.</span></span>
* <span data-ttu-id="7abad-183">Il numero massimo di volti restituiti per ogni video è 64.</span><span class="sxs-lookup"><span data-stu-id="7abad-183">For each video, the maximum number of faces returned is 64.</span></span>
* <span data-ttu-id="7abad-184">È possibile che alcuni volti non vengano rilevati per problemi tecnici, ad esempio angoli del volto molto grandi (durante le pose) e grandi occlusioni.</span><span class="sxs-lookup"><span data-stu-id="7abad-184">Some faces may not be detected due to technical challenges; e.g. very large face angles (head-pose), and large occlusion.</span></span> <span data-ttu-id="7abad-185">Le riprese frontali e quasi frontali producono i risultati migliori.</span><span class="sxs-lookup"><span data-stu-id="7abad-185">Frontal and near-frontal faces have the best results.</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="7abad-186">Codice di esempio .NET</span><span class="sxs-lookup"><span data-stu-id="7abad-186">.NET sample code</span></span>

<span data-ttu-id="7abad-187">Il programma seguente illustra come:</span><span class="sxs-lookup"><span data-stu-id="7abad-187">The following program shows how to:</span></span>

1. <span data-ttu-id="7abad-188">Creare un asset e caricare un file multimediale nell'asset.</span><span class="sxs-lookup"><span data-stu-id="7abad-188">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="7abad-189">Creare un processo con un'attività di rilevamento viso in base al file di configurazione che contiene il set di impostazioni JSON seguente.</span><span class="sxs-lookup"><span data-stu-id="7abad-189">Create a job with a face detection task based on a configuration file that contains the following json preset.</span></span> 
   
        {
            "version": "1.0"
        }
3. <span data-ttu-id="7abad-190">Scaricare i file JSON di output.</span><span class="sxs-lookup"><span data-stu-id="7abad-190">Download the output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="7abad-191">Creare e configurare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7abad-191">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="7abad-192">Configurare l'ambiente di sviluppo e popolare il file app.config con le informazioni di connessione, come descritto in [Sviluppo di applicazioni di Servizi multimediali con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="7abad-192">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="7abad-193">Esempio</span><span class="sxs-lookup"><span data-stu-id="7abad-193">Example</span></span>

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

                // Run the FaceDetection job.
                var asset = RunFaceDetectionJob(@"C:\supportFiles\FaceDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\FaceDetection\config.json");

                // Download the job output asset.
                DownloadAsset(asset, @"C:\supportFiles\FaceDetection\Output");
            }

            static IAsset RunFaceDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload the input media file to storage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Face Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Face Detection Job");

                // Get a reference to Azure Media Face Detector.
                string MediaProcessorName = "Azure Media Face Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from the specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with the encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Face Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify the input asset.
                task.InputAssets.Add(asset);

                // Add an output asset to contain the results of the job.
                task.OutputAssets.AddNew("My Face Detectoion Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="7abad-194">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="7abad-194">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="7abad-195">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="7abad-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="7abad-196">Collegamenti correlati</span><span class="sxs-lookup"><span data-stu-id="7abad-196">Related links</span></span>
[<span data-ttu-id="7abad-197">Panoramica di Analisi servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="7abad-197">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="7abad-198">Demo di Analisi servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="7abad-198">Azure Media Analytics demos</span></span>](http://amslabs.azurewebsites.net/demos/Analytics.html)

