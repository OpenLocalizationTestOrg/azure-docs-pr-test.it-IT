---
title: Rilevare i movimenti con Analisi Servizi multimediali di Azure | Microsoft Docs
description: Il processore di contenuti multimediali Rilevatore multimediale di movimento Azure consente di identificare in modo efficace le sezioni interessanti all'interno di un video altrimenti lungo e privo di eventi.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: d144f813-1a55-442f-a895-5c4cb6d0aeae
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: milanga;juliako;
ms.openlocfilehash: 115ad9dfd88062f23d5d17eed8897ce5d2ca8484
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="detect-motions-with-azure-media-analytics"></a><span data-ttu-id="9e7da-103">Rilevare i movimenti con Analisi servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="9e7da-103">Detect Motions with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="9e7da-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="9e7da-104">Overview</span></span>
<span data-ttu-id="9e7da-105">Il processore di contenuti multimediali **Rilevatore multimediale di movimento Azure** consente di identificare in modo efficace le sezioni interessanti all'interno di un video altrimenti lungo e privo di eventi.</span><span class="sxs-lookup"><span data-stu-id="9e7da-105">The **Azure Media Motion Detector** media processor (MP) enables you to efficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="9e7da-106">Il rilevamento di movimento può essere usato nei filmati statici della videocamera per individuare le sezioni del video in cui si verificano movimenti.</span><span class="sxs-lookup"><span data-stu-id="9e7da-106">Motion detection can be used on static camera footage to identify sections of the video where motion occurs.</span></span> <span data-ttu-id="9e7da-107">Viene generato un file JSON contenente i metadati con i timestamp e l'area di delimitazione in cui si è verificato l'evento.</span><span class="sxs-lookup"><span data-stu-id="9e7da-107">It generates a JSON file containing a metadata with timestamps and the bounding region where the event occurred.</span></span>

<span data-ttu-id="9e7da-108">Questa tecnologia, destinata alle trasmissioni video di sicurezza, è in grado di classificare i movimenti in eventi rilevanti e falsi positivi, ad esempio variazioni di luminosità e delle ombre.</span><span class="sxs-lookup"><span data-stu-id="9e7da-108">Targeted towards security video feeds, this technology is able to categorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="9e7da-109">In questo modo è possibile generare avvisi di sicurezza dalle trasmissioni della videocamera senza che venga segnalata una serie infinita di eventi irrilevanti e al contempo estrarre i momenti di interesse da video di sorveglianza estremamente lunghi.</span><span class="sxs-lookup"><span data-stu-id="9e7da-109">This allows you to generate security alerts from camera feeds without being spammed with endless irrelevant events, while being able to extract moments of interest from extremely long surveillance videos.</span></span>

<span data-ttu-id="9e7da-110">Attualmente il processore multimediale **Rilevatore multimediale di movimento Azure** è disponibile in Anteprima.</span><span class="sxs-lookup"><span data-stu-id="9e7da-110">The **Azure Media Motion Detector** MP is currently in Preview.</span></span>

<span data-ttu-id="9e7da-111">Questo argomento illustra dettagliatamente il **Azure Media Motion Detector** e spiega come usare questa funzionalità con Media Services .NET SDK</span><span class="sxs-lookup"><span data-stu-id="9e7da-111">This topic gives details about  **Azure Media Motion Detector** and shows how to use it with Media Services SDK for .NET</span></span>

## <a name="motion-detector-input-files"></a><span data-ttu-id="9e7da-112">File di input di Rilevatore di movimento</span><span class="sxs-lookup"><span data-stu-id="9e7da-112">Motion Detector input files</span></span>
<span data-ttu-id="9e7da-113">File video.</span><span class="sxs-lookup"><span data-stu-id="9e7da-113">Video files.</span></span> <span data-ttu-id="9e7da-114">Attualmente sono supportati i formati seguenti: MP4, MOV e WMV.</span><span class="sxs-lookup"><span data-stu-id="9e7da-114">Currently, the following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration-preset"></a><span data-ttu-id="9e7da-115">Configurazione delle attività (set di impostazioni)</span><span class="sxs-lookup"><span data-stu-id="9e7da-115">Task configuration (preset)</span></span>
<span data-ttu-id="9e7da-116">Quando si crea un'attività con **Azure Media Motion Detector**è necessario specificare un set di impostazioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="9e7da-116">When creating a task with **Azure Media Motion Detector**, you must specify a configuration preset.</span></span> 

### <a name="parameters"></a><span data-ttu-id="9e7da-117">Parametri</span><span class="sxs-lookup"><span data-stu-id="9e7da-117">Parameters</span></span>
<span data-ttu-id="9e7da-118">È possibile usare i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="9e7da-118">You can use the following parameters:</span></span>

| <span data-ttu-id="9e7da-119">Nome</span><span class="sxs-lookup"><span data-stu-id="9e7da-119">Name</span></span> | <span data-ttu-id="9e7da-120">Opzioni</span><span class="sxs-lookup"><span data-stu-id="9e7da-120">Options</span></span> | <span data-ttu-id="9e7da-121">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9e7da-121">Description</span></span> | <span data-ttu-id="9e7da-122">Default</span><span class="sxs-lookup"><span data-stu-id="9e7da-122">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9e7da-123">sensitivityLevel</span><span class="sxs-lookup"><span data-stu-id="9e7da-123">sensitivityLevel</span></span> |<span data-ttu-id="9e7da-124">Stringa:'low', 'medium', 'high'</span><span class="sxs-lookup"><span data-stu-id="9e7da-124">String:'low', 'medium', 'high'</span></span> |<span data-ttu-id="9e7da-125">Imposta il livello di sensibilità per la segnalazione dei movimenti.</span><span class="sxs-lookup"><span data-stu-id="9e7da-125">Sets the sensitivity level at which motions is reported.</span></span> <span data-ttu-id="9e7da-126">Modificare per ridurre il numero di falsi positivi.</span><span class="sxs-lookup"><span data-stu-id="9e7da-126">Adjust this to adjust amount of false positives.</span></span> |<span data-ttu-id="9e7da-127">'medium'</span><span class="sxs-lookup"><span data-stu-id="9e7da-127">'medium'</span></span> |
| <span data-ttu-id="9e7da-128">frameSamplingValue</span><span class="sxs-lookup"><span data-stu-id="9e7da-128">frameSamplingValue</span></span> |<span data-ttu-id="9e7da-129">Intero positivo</span><span class="sxs-lookup"><span data-stu-id="9e7da-129">Positive integer</span></span> |<span data-ttu-id="9e7da-130">Imposta la frequenza di esecuzione dell'algoritmo.</span><span class="sxs-lookup"><span data-stu-id="9e7da-130">Sets the frequency at which algorithm runs.</span></span> <span data-ttu-id="9e7da-131">1 indica a ogni fotogramma, 2 a un fotogramma su due e così via.</span><span class="sxs-lookup"><span data-stu-id="9e7da-131">1 equals every frame, 2 means every 2nd frame, and so on.</span></span> |<span data-ttu-id="9e7da-132">1</span><span class="sxs-lookup"><span data-stu-id="9e7da-132">1</span></span> |
| <span data-ttu-id="9e7da-133">detectLightChange</span><span class="sxs-lookup"><span data-stu-id="9e7da-133">detectLightChange</span></span> |<span data-ttu-id="9e7da-134">Booleano: 'true', 'false'</span><span class="sxs-lookup"><span data-stu-id="9e7da-134">Boolean:'true', 'false'</span></span> |<span data-ttu-id="9e7da-135">Indica se vengono segnalate le variazioni di luce nei risultati</span><span class="sxs-lookup"><span data-stu-id="9e7da-135">Sets whether light changes are reported in the results</span></span> |<span data-ttu-id="9e7da-136">'False'</span><span class="sxs-lookup"><span data-stu-id="9e7da-136">'False'</span></span> |
| <span data-ttu-id="9e7da-137">mergeTimeThreshold</span><span class="sxs-lookup"><span data-stu-id="9e7da-137">mergeTimeThreshold</span></span> |<span data-ttu-id="9e7da-138">Xs-time: Hh:mm:ss</span><span class="sxs-lookup"><span data-stu-id="9e7da-138">Xs-time: Hh:mm:ss</span></span><br/><span data-ttu-id="9e7da-139">Esempio: 00:00:03</span><span class="sxs-lookup"><span data-stu-id="9e7da-139">Example: 00:00:03</span></span> |<span data-ttu-id="9e7da-140">Specifica l'intervallo di tempo tra eventi di movimento in cui 2 eventi verranno combinati e segnalati come 1 evento.</span><span class="sxs-lookup"><span data-stu-id="9e7da-140">Specifies the time window between motion events where 2 events will be combined and reported as 1.</span></span> |<span data-ttu-id="9e7da-141">00:00:00</span><span class="sxs-lookup"><span data-stu-id="9e7da-141">00:00:00</span></span> |
| <span data-ttu-id="9e7da-142">detectionZones</span><span class="sxs-lookup"><span data-stu-id="9e7da-142">detectionZones</span></span> |<span data-ttu-id="9e7da-143">Matrice di zone di rilevamento:</span><span class="sxs-lookup"><span data-stu-id="9e7da-143">An array of detection zones:</span></span><br/><span data-ttu-id="9e7da-144">- La zona di rilevamento è una matrice di 3 o più punti</span><span class="sxs-lookup"><span data-stu-id="9e7da-144">- Detection Zone is an array of 3 or more points</span></span><br/><span data-ttu-id="9e7da-145">- Il punto è una coordinata x e y da 0 a 1.</span><span class="sxs-lookup"><span data-stu-id="9e7da-145">- Point is a x and y coordinate from 0 to 1.</span></span> |<span data-ttu-id="9e7da-146">Descrive l'elenco delle zone di rilevamento poligonali da usare.</span><span class="sxs-lookup"><span data-stu-id="9e7da-146">Describes the list of polygonal detection zones to be used.</span></span><br/><span data-ttu-id="9e7da-147">I risultati verranno visualizzati con le zone come ID, dove la prima è 'id':0</span><span class="sxs-lookup"><span data-stu-id="9e7da-147">Results will be reported with the zones as an ID, with the first one being 'id':0</span></span> |<span data-ttu-id="9e7da-148">Singola zona che copre l'intero fotogramma.</span><span class="sxs-lookup"><span data-stu-id="9e7da-148">Single zone which covers the entire frame.</span></span> |

### <a name="json-example"></a><span data-ttu-id="9e7da-149">Esempio di JSON</span><span class="sxs-lookup"><span data-stu-id="9e7da-149">JSON example</span></span>
    {
      "version": "1.0",
      "options": {
        "sensitivityLevel": "medium",
        "frameSamplingValue": 1,
        "detectLightChange": "False",
        "mergeTimeThreshold":
        "00:00:02",
        "detectionZones": [
          [
            {"x": 0, "y": 0},
            {"x": 0.5, "y": 0},
            {"x": 0, "y": 1}
           ],
          [
            {"x": 0.3, "y": 0.3},
            {"x": 0.55, "y": 0.3},
            {"x": 0.8, "y": 0.3},
            {"x": 0.8, "y": 0.55},
            {"x": 0.8, "y": 0.8},
            {"x": 0.55, "y": 0.8},
            {"x": 0.3, "y": 0.8},
            {"x": 0.3, "y": 0.55}
          ]
        ]
      }
    }


## <a name="motion-detector-output-files"></a><span data-ttu-id="9e7da-150">File di output di Rilevatore di movimento</span><span class="sxs-lookup"><span data-stu-id="9e7da-150">Motion Detector output files</span></span>
<span data-ttu-id="9e7da-151">Un processo di rilevamento del movimento restituirà un file JSON nell'asset di output che descrive gli avvisi di movimento e le relative categorie all'interno del video.</span><span class="sxs-lookup"><span data-stu-id="9e7da-151">A motion detection job will return a JSON file in the output asset which describes the motion alerts, and their categories, within the video.</span></span> <span data-ttu-id="9e7da-152">Il file conterrà informazioni sull'ora e sulla durata dei movimenti rilevati nel video.</span><span class="sxs-lookup"><span data-stu-id="9e7da-152">The file will contain information about the time and duration of motion detected in the video.</span></span>

<span data-ttu-id="9e7da-153">L'API Rilevatore di movimento fornisce indicatori se sono presenti oggetti in movimento in un video con sfondo fisso, ad esempio un video di sorveglianza.</span><span class="sxs-lookup"><span data-stu-id="9e7da-153">The Motion Detector API provides indicators once there are objects in motion in a fixed background video (e.g. a surveillance video).</span></span> <span data-ttu-id="9e7da-154">Rilevatore di movimento è in grado di ridurre i falsi allarmi, ad esempio variazioni di luminosità e di ombreggiatura.</span><span class="sxs-lookup"><span data-stu-id="9e7da-154">The Motion Detector is trained to reduce false alarms, such as lighting and shadow changes.</span></span> <span data-ttu-id="9e7da-155">Le limitazioni correnti degli algoritmi includono video con visione notturna, oggetti semi-trasparenti e oggetti di piccole dimensioni.</span><span class="sxs-lookup"><span data-stu-id="9e7da-155">Current limitations of the algorithms include night vision videos, semi-transparent objects, and small objects.</span></span>

### <span data-ttu-id="9e7da-156"><a id="output_elements"></a>Elementi del file di output JSON</span><span class="sxs-lookup"><span data-stu-id="9e7da-156"><a id="output_elements"></a>Elements of the output JSON file</span></span>
> [!NOTE]
> <span data-ttu-id="9e7da-157">Nella versione più recente, il formato di output JSON è stato modificato e può rappresentare una modifica di rilievo per alcuni clienti.</span><span class="sxs-lookup"><span data-stu-id="9e7da-157">In the latest release, the Output JSON format has changed and may represent a breaking change for some customers.</span></span>
> 
> 

<span data-ttu-id="9e7da-158">La tabella seguente illustra gli elementi del file di output JSON.</span><span class="sxs-lookup"><span data-stu-id="9e7da-158">The following table describes elements of the output JSON file.</span></span>

| <span data-ttu-id="9e7da-159">Elemento</span><span class="sxs-lookup"><span data-stu-id="9e7da-159">Element</span></span> | <span data-ttu-id="9e7da-160">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9e7da-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9e7da-161">Versione</span><span class="sxs-lookup"><span data-stu-id="9e7da-161">Version</span></span> |<span data-ttu-id="9e7da-162">Indica la versione dell'API Video.</span><span class="sxs-lookup"><span data-stu-id="9e7da-162">This refers to the version of the Video API.</span></span> <span data-ttu-id="9e7da-163">La versione corrente è 2.</span><span class="sxs-lookup"><span data-stu-id="9e7da-163">The current version is 2.</span></span> |
| <span data-ttu-id="9e7da-164">Scala cronologica</span><span class="sxs-lookup"><span data-stu-id="9e7da-164">Timescale</span></span> |<span data-ttu-id="9e7da-165">"Scatti" al secondo del video.</span><span class="sxs-lookup"><span data-stu-id="9e7da-165">"Ticks" per second of the video.</span></span> |
| <span data-ttu-id="9e7da-166">Offset</span><span class="sxs-lookup"><span data-stu-id="9e7da-166">Offset</span></span> |<span data-ttu-id="9e7da-167">Differenza di orario dei timestamp in "scatti".</span><span class="sxs-lookup"><span data-stu-id="9e7da-167">The time offset for timestamps in "ticks".</span></span> <span data-ttu-id="9e7da-168">Nella versione 1.0 delle API Video, questo valore è sempre 0.</span><span class="sxs-lookup"><span data-stu-id="9e7da-168">In version 1.0 of Video APIs, this will always be 0.</span></span> <span data-ttu-id="9e7da-169">Negli scenari futuri supportati questo valore potrebbe cambiare.</span><span class="sxs-lookup"><span data-stu-id="9e7da-169">In future scenarios we support, this value may change.</span></span> |
| <span data-ttu-id="9e7da-170">Frequenza fotogrammi</span><span class="sxs-lookup"><span data-stu-id="9e7da-170">Framerate</span></span> |<span data-ttu-id="9e7da-171">Fotogrammi al secondo del video.</span><span class="sxs-lookup"><span data-stu-id="9e7da-171">Frames per second of the video.</span></span> |
| <span data-ttu-id="9e7da-172">Larghezza, altezza</span><span class="sxs-lookup"><span data-stu-id="9e7da-172">Width, Height</span></span> |<span data-ttu-id="9e7da-173">Indica la larghezza e l'altezza del video in pixel.</span><span class="sxs-lookup"><span data-stu-id="9e7da-173">Refers to the width and height of the video in pixels.</span></span> |
| <span data-ttu-id="9e7da-174">Inizia</span><span class="sxs-lookup"><span data-stu-id="9e7da-174">Start</span></span> |<span data-ttu-id="9e7da-175">Il timestamp di inizio in "scatti".</span><span class="sxs-lookup"><span data-stu-id="9e7da-175">The start timestamp in "ticks".</span></span> |
| <span data-ttu-id="9e7da-176">Durata</span><span class="sxs-lookup"><span data-stu-id="9e7da-176">Duration</span></span> |<span data-ttu-id="9e7da-177">La lunghezza dell'evento in "scatti".</span><span class="sxs-lookup"><span data-stu-id="9e7da-177">The length of the event, in "ticks".</span></span> |
| <span data-ttu-id="9e7da-178">Interval</span><span class="sxs-lookup"><span data-stu-id="9e7da-178">Interval</span></span> |<span data-ttu-id="9e7da-179">L'intervallo di ogni voce dell'evento in "scatti".</span><span class="sxs-lookup"><span data-stu-id="9e7da-179">The interval of each entry in the event, in "ticks".</span></span> |
| <span data-ttu-id="9e7da-180">Eventi</span><span class="sxs-lookup"><span data-stu-id="9e7da-180">Events</span></span> |<span data-ttu-id="9e7da-181">Ogni frammento di evento contiene i movimenti rilevati nella durata specificata.</span><span class="sxs-lookup"><span data-stu-id="9e7da-181">Each event fragment contains the motion detected within that time duration.</span></span> |
| <span data-ttu-id="9e7da-182">Tipo</span><span class="sxs-lookup"><span data-stu-id="9e7da-182">Type</span></span> |<span data-ttu-id="9e7da-183">Nella versione corrente questo valore è sempre "2" per il movimento generico.</span><span class="sxs-lookup"><span data-stu-id="9e7da-183">In the current version, this is always ‘2’ for generic motion.</span></span> <span data-ttu-id="9e7da-184">Questa etichetta offre alle API Video la flessibilità necessaria per classificare i movimenti nelle versioni future.</span><span class="sxs-lookup"><span data-stu-id="9e7da-184">This label gives Video APIs the flexibility to categorize motion in future versions.</span></span> |
| <span data-ttu-id="9e7da-185">RegionID</span><span class="sxs-lookup"><span data-stu-id="9e7da-185">RegionID</span></span> |<span data-ttu-id="9e7da-186">Come spiegato in precedenza, in questa versione questo valore è sempre 0.</span><span class="sxs-lookup"><span data-stu-id="9e7da-186">As explained above, this will always be 0 in this version.</span></span> <span data-ttu-id="9e7da-187">Questa etichetta offre alle API Video la flessibilità necessaria per individuare i movimenti in varie aree nelle versioni future.</span><span class="sxs-lookup"><span data-stu-id="9e7da-187">This label gives Video API the flexibility to find motion in various regions in future versions.</span></span> |
| <span data-ttu-id="9e7da-188">Regioni</span><span class="sxs-lookup"><span data-stu-id="9e7da-188">Regions</span></span> |<span data-ttu-id="9e7da-189">Si riferisce all'area del video in cui si presta particolare attenzione al movimento.</span><span class="sxs-lookup"><span data-stu-id="9e7da-189">Refers to the area in your video where you care about motion.</span></span> <br/><br/><span data-ttu-id="9e7da-190">-"id" rappresenta l'area: in questa versione ne è presente una sola, ID 0.</span><span class="sxs-lookup"><span data-stu-id="9e7da-190">-"id" represents the region area – in this version there is only one, ID 0.</span></span> <br/><span data-ttu-id="9e7da-191">-"type" rappresenta la forma dell'area importante per il movimento.</span><span class="sxs-lookup"><span data-stu-id="9e7da-191">-"type" represents the shape of the region you care about for motion.</span></span> <span data-ttu-id="9e7da-192">Sono attualmente supportati "rectangle" e "polygon".</span><span class="sxs-lookup"><span data-stu-id="9e7da-192">Currently, "rectangle" and "polygon" are supported.</span></span><br/> <span data-ttu-id="9e7da-193">Se è stato specificato "rectangle", le dimensioni dell'area saranno X, Y, larghezza e altezza.</span><span class="sxs-lookup"><span data-stu-id="9e7da-193">If you specified "rectangle", the region has dimensions in X, Y, Width, and Height.</span></span> <span data-ttu-id="9e7da-194">Le coordinate X e Y rappresentano le coordinate XY in alto a sinistra nell'area in una scala normalizzata da 0,0 a 1,0.</span><span class="sxs-lookup"><span data-stu-id="9e7da-194">The X and Y coordinates represent the upper left hand XY coordinates of the region in a normalized scale of 0.0 to 1.0.</span></span> <span data-ttu-id="9e7da-195">La larghezza e l'altezza rappresentano le dimensioni dell'area in una scala normalizzata da 0,0 a 1,0.</span><span class="sxs-lookup"><span data-stu-id="9e7da-195">The width and height represent the size of the region in a normalized scale of 0.0 to 1.0.</span></span> <span data-ttu-id="9e7da-196">Nella versione corrente, X, Y, larghezza e altezza sono sempre 0, 0 e 1, 1.</span><span class="sxs-lookup"><span data-stu-id="9e7da-196">In the current version, X, Y, Width, and Height are always fixed at 0, 0 and 1, 1.</span></span> <br/><span data-ttu-id="9e7da-197">Se è stato specificato "polygon", le dimensioni dell'area saranno in punti.</span><span class="sxs-lookup"><span data-stu-id="9e7da-197">If you specified "polygon", the region has dimensions in points.</span></span> <br/> |
| <span data-ttu-id="9e7da-198">Frammenti</span><span class="sxs-lookup"><span data-stu-id="9e7da-198">Fragments</span></span> |<span data-ttu-id="9e7da-199">I metadati sono suddivisi in segmenti diversi, detti frammenti.</span><span class="sxs-lookup"><span data-stu-id="9e7da-199">The metadata is chunked up into different segments called fragments.</span></span> <span data-ttu-id="9e7da-200">Ogni frammento contiene un inizio, una durata, un numero di intervallo e uno o più eventi.</span><span class="sxs-lookup"><span data-stu-id="9e7da-200">Each fragment contains a start, duration, interval number, and event(s).</span></span> <span data-ttu-id="9e7da-201">Un frammento privo di eventi significa che non è stato rilevato alcun movimento in corrispondenza dell'ora di inizio e della durata.</span><span class="sxs-lookup"><span data-stu-id="9e7da-201">A fragment with no events means that no motion was detected during that start time and duration.</span></span> |
| <span data-ttu-id="9e7da-202">Parentesi quadre []</span><span class="sxs-lookup"><span data-stu-id="9e7da-202">Brackets []</span></span> |<span data-ttu-id="9e7da-203">Ogni parentesi rappresenta un intervallo nell'evento.</span><span class="sxs-lookup"><span data-stu-id="9e7da-203">Each bracket represents one interval in the event.</span></span> <span data-ttu-id="9e7da-204">Le parentesi vuote in un intervallo indicano che è non stato rilevato alcun movimento.</span><span class="sxs-lookup"><span data-stu-id="9e7da-204">Empty brackets for that interval means that no motion was detected.</span></span> |
| <span data-ttu-id="9e7da-205">locations</span><span class="sxs-lookup"><span data-stu-id="9e7da-205">locations</span></span> |<span data-ttu-id="9e7da-206">Questa nuova voce nell'elenco degli eventi indica le posizioni in cui si è verificato il movimento.</span><span class="sxs-lookup"><span data-stu-id="9e7da-206">This new entry under events lists the location where the motion occurred.</span></span> <span data-ttu-id="9e7da-207">È un dato più specifico delle zone di rilevamento.</span><span class="sxs-lookup"><span data-stu-id="9e7da-207">This is more specific than the detection zones.</span></span> |

<span data-ttu-id="9e7da-208">Di seguito è riportato un esempio di output JSON</span><span class="sxs-lookup"><span data-stu-id="9e7da-208">The following is a JSON output example</span></span>

    {
      "version": 2,
      "timescale": 23976,
      "offset": 0,
      "framerate": 24,
      "width": 1280,
      "height": 720,
      "regions": [
        {
          "id": 0,
          "type": "polygon",
          "points": [{'x': 0, 'y': 0},
            {'x': 0.5, 'y': 0},
            {'x': 0, 'y': 1}]
        }
      ],
      "fragments": [
        {
          "start": 0,
          "duration": 226765
        },
        {
          "start": 226765,
          "duration": 47952,
          "interval": 999,
          "events": [
            [
              {
                "type": 2,
                "typeName": "motion",
                "locations": [
                  {
                    "x": 0.004184,
                    "y": 0.007463,
                    "width": 0.991667,
                    "height": 0.985185
                  }
                ],
                "regionId": 0
              }
            ],

    …
## <a name="limitations"></a><span data-ttu-id="9e7da-209">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="9e7da-209">Limitations</span></span>
* <span data-ttu-id="9e7da-210">I formati video di input supportati includono MP4, MOV e WMV.</span><span class="sxs-lookup"><span data-stu-id="9e7da-210">The supported input video formats include MP4, MOV, and WMV.</span></span>
* <span data-ttu-id="9e7da-211">Il rilevamento di movimento è ottimizzato per i video a sfondo fisso.</span><span class="sxs-lookup"><span data-stu-id="9e7da-211">Motion Detection is optimized for stationary background videos.</span></span> <span data-ttu-id="9e7da-212">L'algoritmo mira alla riduzione dei falsi allarmi, ad esempio le variazioni di luce e ombra.</span><span class="sxs-lookup"><span data-stu-id="9e7da-212">The algorithm focuses on reducing false alarms, such as lighting changes, and shadows.</span></span>
* <span data-ttu-id="9e7da-213">È possibile che alcuni movimenti non vengano rilevati per problemi tecnici, ad esempio video con visione notturna, oggetti semi-trasparenti e oggetti di piccole dimensioni.</span><span class="sxs-lookup"><span data-stu-id="9e7da-213">Some motion may not be detected due to technical challenges; e.g. night vision videos, semi-transparent objects, and small objects.</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="9e7da-214">Codice di esempio .NET</span><span class="sxs-lookup"><span data-stu-id="9e7da-214">.NET sample code</span></span>

<span data-ttu-id="9e7da-215">Il programma seguente illustra come:</span><span class="sxs-lookup"><span data-stu-id="9e7da-215">The following program shows how to:</span></span>

1. <span data-ttu-id="9e7da-216">Creare un asset e caricare un file multimediale nell'asset.</span><span class="sxs-lookup"><span data-stu-id="9e7da-216">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="9e7da-217">Creare un processo con un'attività di rilevamento movimento video in base al file di configurazione che contiene il set di impostazioni JSON seguente.</span><span class="sxs-lookup"><span data-stu-id="9e7da-217">Create a job with a video motion detection task based on a configuration file that contains the following json preset.</span></span> 
   
        {
          "Version": "1.0",
          "Options": {
            "SensitivityLevel": "medium",
            "FrameSamplingValue": 1,
            "DetectLightChange": "False",
            "MergeTimeThreshold":
            "00:00:02",
            "DetectionZones": [
              [
                {"x": 0, "y": 0},
                {"x": 0.5, "y": 0},
                {"x": 0, "y": 1}
               ],
              [
                {"x": 0.3, "y": 0.3},
                {"x": 0.55, "y": 0.3},
                {"x": 0.8, "y": 0.3},
                {"x": 0.8, "y": 0.55},
                {"x": 0.8, "y": 0.8},
                {"x": 0.55, "y": 0.8},
                {"x": 0.3, "y": 0.8},
                {"x": 0.3, "y": 0.55}
              ]
            ]
          }
        }
3. <span data-ttu-id="9e7da-218">Scaricare i file JSON di output.</span><span class="sxs-lookup"><span data-stu-id="9e7da-218">Download the output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="9e7da-219">Creare e configurare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9e7da-219">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="9e7da-220">Configurare l'ambiente di sviluppo e popolare il file app.config con le informazioni di connessione, come descritto in [Sviluppo di applicazioni di Servizi multimediali con .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="9e7da-220">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="9e7da-221">Esempio</span><span class="sxs-lookup"><span data-stu-id="9e7da-221">Example</span></span>


    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace VideoMotionDetection
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

                // Run the VideoMotionDetection job.
                var asset = RunVideoMotionDetectionJob(@"C:\supportFiles\VideoMotionDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoMotionDetection\config.json");

                // Download the job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoMotionDetection\Output");
            }

            static IAsset RunVideoMotionDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload the input media file to storage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Motion Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Motion Detection Job");

                // Get a reference to Azure Media Motion Detector.
                string MediaProcessorName = "Azure Media Motion Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from the specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with the encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Motion Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify the input asset.
                task.InputAssets.Add(asset);

                // Add an output asset to contain the results of the job.
                task.OutputAssets.AddNew("My Video Motion Detectoion Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="9e7da-222">Percorsi di apprendimento di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="9e7da-222">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9e7da-223">Fornire commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="9e7da-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="9e7da-224">Collegamenti correlati</span><span class="sxs-lookup"><span data-stu-id="9e7da-224">Related links</span></span>
[<span data-ttu-id="9e7da-225">Blog di Azure Media Motion Detector</span><span class="sxs-lookup"><span data-stu-id="9e7da-225">Azure Media Services Motion Detector blog</span></span>](https://azure.microsoft.com/blog/motion-detector-update/)

[<span data-ttu-id="9e7da-226">Panoramica di Analisi servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="9e7da-226">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="9e7da-227">Demo di Analisi servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="9e7da-227">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

