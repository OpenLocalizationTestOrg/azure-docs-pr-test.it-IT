---
title: Debug guidato dai dati di Analisi di flusso di Azure mediante il diagramma del processo di debug | Documentazione Microsoft
description: Risoluzione dei problemi del processo di Analisi di flusso mediante il diagramma di processo e le metriche.
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/01/2017
ms.author: jeffstok
ms.openlocfilehash: 4e5949232e8377b7697eaebf96eacdc31c4f5422
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="data-driven-debugging-by-using-the-job-diagram"></a><span data-ttu-id="2bb7a-103">Debug guidato dai dati mediante il diagramma di processo</span><span class="sxs-lookup"><span data-stu-id="2bb7a-103">Data-driven debugging by using the job diagram</span></span>

<span data-ttu-id="2bb7a-104">Il diagramma di processo nel pannello **Monitoraggio** del portale di Azure consente di visualizzare la pipeline di processo.</span><span class="sxs-lookup"><span data-stu-id="2bb7a-104">The job diagram on the **Monitoring** blade in the Azure portal can help you visualize your job pipeline.</span></span> <span data-ttu-id="2bb7a-105">Mostra gli input, gli output e i passaggi delle query.</span><span class="sxs-lookup"><span data-stu-id="2bb7a-105">It shows inputs, outputs, and query steps.</span></span> <span data-ttu-id="2bb7a-106">È possibile usare il diagramma di processo per esaminare le metriche per ogni passaggio, al fine di isolare più rapidamente l'origine di un problema durante la sua risoluzione.</span><span class="sxs-lookup"><span data-stu-id="2bb7a-106">You can use the job diagram to examine the metrics for each step, to more quickly isolate the source of a problem when you troubleshoot issues.</span></span>

## <a name="using-the-job-diagram"></a><span data-ttu-id="2bb7a-107">Uso del diagramma di processo</span><span class="sxs-lookup"><span data-stu-id="2bb7a-107">Using the job diagram</span></span>

<span data-ttu-id="2bb7a-108">Nel portale di Azure, durante un processo di Analisi di flusso, sotto **SUPPORTO E RISOLUZIONE DEI PROBLEMI** selezionare **Diagramma del processo**:</span><span class="sxs-lookup"><span data-stu-id="2bb7a-108">In the Azure portal, while in a Stream Analytics job, under **SUPPORT + TROUBLESHOOTING**, select **Job diagram**:</span></span>

![Diagramma di processo con metriche - posizione](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-1.png)

<span data-ttu-id="2bb7a-110">Selezionare ciascun passaggio della query per vedere la sezione corrispondente nel riquadro di modifica query.</span><span class="sxs-lookup"><span data-stu-id="2bb7a-110">Select each query step to see the corresponding section in a query editing pane.</span></span> <span data-ttu-id="2bb7a-111">Viene visualizzato il grafico della metrica relativo al passaggio in un riquadro inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="2bb7a-111">A metric chart for the step is displayed in a lower pane on the page.</span></span>

![Diagramma di processo con metriche - processo di base](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-2.png)

<span data-ttu-id="2bb7a-113">Per vedere le partizioni dell'input di Hub eventi di Azure, selezionare **...**</span><span class="sxs-lookup"><span data-stu-id="2bb7a-113">To see the partitions of the Azure Event Hubs input, select **. . .**</span></span> <span data-ttu-id="2bb7a-114">Si apre il menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="2bb7a-114">A context menu appears.</span></span> <span data-ttu-id="2bb7a-115">È possibile vedere anche la fusione dell'input.</span><span class="sxs-lookup"><span data-stu-id="2bb7a-115">You also can see the input merger.</span></span>

![Diagramma di processo con metriche - espandere la partizione](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-3.png)

<span data-ttu-id="2bb7a-117">Per vedere il grafico delle metrica per una singola partizione, selezionare il nodo della partizione.</span><span class="sxs-lookup"><span data-stu-id="2bb7a-117">To see the metric chart for only a single partition, select the partition node.</span></span> <span data-ttu-id="2bb7a-118">Le metriche sono visualizzate nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="2bb7a-118">The metrics are shown at the bottom of the page.</span></span>

![Diagramma di processo con metriche - altre metriche](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-4.png)

<span data-ttu-id="2bb7a-120">Per vedere il grafico delle metriche per una fusione, selezionare il nodo della fusione.</span><span class="sxs-lookup"><span data-stu-id="2bb7a-120">To see the metrics chart for a merger, select the merger node.</span></span> <span data-ttu-id="2bb7a-121">Il diagramma seguente mostra che nessun evento è stato eliminato o regolato.</span><span class="sxs-lookup"><span data-stu-id="2bb7a-121">The following chart shows that no events were dropped or adjusted.</span></span>

![Diagramma di processo con metriche - griglia](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-5.png)

<span data-ttu-id="2bb7a-123">Per vedere i dettagli del valore e ora delle metriche, puntare sul grafico.</span><span class="sxs-lookup"><span data-stu-id="2bb7a-123">To see the details of the metric value and time, point to the chart.</span></span>

![Diagramma di processo con metriche - puntare con il mouse](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-6.png)

## <a name="troubleshoot-by-using-metrics"></a><span data-ttu-id="2bb7a-125">Risolvere i problemi mediante le metriche</span><span class="sxs-lookup"><span data-stu-id="2bb7a-125">Troubleshoot by using metrics</span></span>

<span data-ttu-id="2bb7a-126">La metrica **QueryLastProcessedTime** indica quando un determinato passaggio ha ricevuto dati.</span><span class="sxs-lookup"><span data-stu-id="2bb7a-126">The **QueryLastProcessedTime** metric indicates when a specific step received data.</span></span> <span data-ttu-id="2bb7a-127">Osservando la topologia, è possibile procedere a ritroso dal processore di output per vedere quale passaggio non riceve dati.</span><span class="sxs-lookup"><span data-stu-id="2bb7a-127">By looking at the topology, you can work backward from the output processor to see which step is not receiving data.</span></span> <span data-ttu-id="2bb7a-128">Se un passaggio non riceve dati, andare al passaggio di query subito prima.</span><span class="sxs-lookup"><span data-stu-id="2bb7a-128">If a step is not getting data, go to the query step just before it.</span></span> <span data-ttu-id="2bb7a-129">Controllare se il passaggio di query precedente ha un intervallo di tempo e se è trascorso un tempo sufficiente perché possa emettere dati.</span><span class="sxs-lookup"><span data-stu-id="2bb7a-129">Check whether the preceding query step has a time window, and if enough time has passed for it to output data.</span></span> <span data-ttu-id="2bb7a-130">(Notare che gli intervalli di tempo vengono bloccati all'ora).</span><span class="sxs-lookup"><span data-stu-id="2bb7a-130">(Note that time windows are snapped to the hour.)</span></span>
 
<span data-ttu-id="2bb7a-131">Se il passaggio di query precedente è un processore di input, usare le metriche di input per rispondere alle seguenti domande mirate.</span><span class="sxs-lookup"><span data-stu-id="2bb7a-131">If the preceding query step is an input processor, use the input metrics to help answer the following targeted questions.</span></span> <span data-ttu-id="2bb7a-132">Esse consentono di determinare se un processo sta ricevendo dati dalle sue origini di input.</span><span class="sxs-lookup"><span data-stu-id="2bb7a-132">They can help you determine whether a job is getting data from its input sources.</span></span> <span data-ttu-id="2bb7a-133">Se viene eseguito il partizionamento della query, esaminare ogni partizione.</span><span class="sxs-lookup"><span data-stu-id="2bb7a-133">If the query is partitioned, examine each partition.</span></span>
 
### <a name="how-much-data-is-being-read"></a><span data-ttu-id="2bb7a-134">Quanti dati vengono letti?</span><span class="sxs-lookup"><span data-stu-id="2bb7a-134">How much data is being read?</span></span>

*   <span data-ttu-id="2bb7a-135">**InputEventsSourcesTotal** è il numero di unità di dati lette.</span><span class="sxs-lookup"><span data-stu-id="2bb7a-135">**InputEventsSourcesTotal** is the number of data units read.</span></span> <span data-ttu-id="2bb7a-136">Ad esempio il numero di BLOB.</span><span class="sxs-lookup"><span data-stu-id="2bb7a-136">For example, the number of blobs.</span></span>
*   <span data-ttu-id="2bb7a-137">**InputEventsTotal** è il numero di eventi letti.</span><span class="sxs-lookup"><span data-stu-id="2bb7a-137">**InputEventsTotal** is the number of events read.</span></span> <span data-ttu-id="2bb7a-138">Questa metrica è disponibile per ogni partizione.</span><span class="sxs-lookup"><span data-stu-id="2bb7a-138">This metric is available per partition.</span></span>
*   <span data-ttu-id="2bb7a-139">**InputEventsInBytesTotal** è il numero di byte letti.</span><span class="sxs-lookup"><span data-stu-id="2bb7a-139">**InputEventsInBytesTotal** is the number of bytes read.</span></span>
*   <span data-ttu-id="2bb7a-140">**InputEventsLastArrivalTime** viene aggiornato con l'ora di accodamento di ogni evento ricevuto.</span><span class="sxs-lookup"><span data-stu-id="2bb7a-140">**InputEventsLastArrivalTime** is updated with every received event's enqueued time.</span></span>
 
### <a name="is-time-moving-forward-if-actual-events-are-read-punctuation-might-not-be-issued"></a><span data-ttu-id="2bb7a-141">L'ora viene spostata in avanti?</span><span class="sxs-lookup"><span data-stu-id="2bb7a-141">Is time moving forward?</span></span> <span data-ttu-id="2bb7a-142">Se vengono letti eventi reali, potrebbe non essere generata la punteggiatura.</span><span class="sxs-lookup"><span data-stu-id="2bb7a-142">If actual events are read, punctuation might not be issued.</span></span>

*   <span data-ttu-id="2bb7a-143">**InputEventsLastPunctuationTime** specifica quando è stata generata la punteggiatura per indicare lo spostamento in avanti dell'ora.</span><span class="sxs-lookup"><span data-stu-id="2bb7a-143">**InputEventsLastPunctuationTime** indicates when a punctuation was issued to keep time moving forward.</span></span> <span data-ttu-id="2bb7a-144">Se la punteggiatura non viene generata, il flusso di dati può bloccarsi.</span><span class="sxs-lookup"><span data-stu-id="2bb7a-144">If punctuation is not issued, data flow can get blocked.</span></span>
 
### <a name="are-there-any-errors-in-the-input"></a><span data-ttu-id="2bb7a-145">Sono presenti errori nell'input?</span><span class="sxs-lookup"><span data-stu-id="2bb7a-145">Are there any errors in the input?</span></span>

*   <span data-ttu-id="2bb7a-146">**InputEventsEventDataNullTotal** è un conteggio degli eventi con dati Null.</span><span class="sxs-lookup"><span data-stu-id="2bb7a-146">**InputEventsEventDataNullTotal** is a count of events that have null data.</span></span>
*   <span data-ttu-id="2bb7a-147">**InputEventsSerializerErrorsTotal** è un conteggio degli eventi che non è stato possibile deserializzare correttamente.</span><span class="sxs-lookup"><span data-stu-id="2bb7a-147">**InputEventsSerializerErrorsTotal** is a count of events that could not be deserialized correctly.</span></span>
*   <span data-ttu-id="2bb7a-148">**InputEventsDegradedTotal** è un conteggio degli eventi che sono stati interessati da un problema diverso dalla deserializzazione.</span><span class="sxs-lookup"><span data-stu-id="2bb7a-148">**InputEventsDegradedTotal** is a count of events that had an issue other than with deserialization.</span></span>
 
### <a name="are-events-being-dropped-or-adjusted"></a><span data-ttu-id="2bb7a-149">Vengono eliminati o modificati eventi?</span><span class="sxs-lookup"><span data-stu-id="2bb7a-149">Are events being dropped or adjusted?</span></span>

*   <span data-ttu-id="2bb7a-150">**InputEventsEarlyTotal** è il numero degli eventi con un timestamp applicazione precedente il limite massimo.</span><span class="sxs-lookup"><span data-stu-id="2bb7a-150">**InputEventsEarlyTotal** is the number of events that have an application timestamp before the high watermark.</span></span>
*   <span data-ttu-id="2bb7a-151">**InputEventsLateTotal** è il numero degli eventi con un timestamp applicazione successivo al limite massimo.</span><span class="sxs-lookup"><span data-stu-id="2bb7a-151">**InputEventsLateTotal** is the number of events that have an application timestamp after the high watermark.</span></span>
*   <span data-ttu-id="2bb7a-152">**InputEventsDroppedBeforeApplicationStartTimeTotal** è il numero degli eventi eliminati prima dell'ora di inizio del processo.</span><span class="sxs-lookup"><span data-stu-id="2bb7a-152">**InputEventsDroppedBeforeApplicationStartTimeTotal** is the number events dropped before the job start time.</span></span>
 
### <a name="are-we-falling-behind-in-reading-data"></a><span data-ttu-id="2bb7a-153">Si sta verificando un ritardo nella lettura dei dati?</span><span class="sxs-lookup"><span data-stu-id="2bb7a-153">Are we falling behind in reading data?</span></span>

*   <span data-ttu-id="2bb7a-154">**InputEventsSourcesBackloggedTotal** indica quanti altri messaggi devono essere letti per gli input di Hub eventi e dell'hub IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="2bb7a-154">**InputEventsSourcesBackloggedTotal** tells you how many more messages need to be read for Event Hubs and Azure IoT Hub inputs.</span></span>


## <a name="get-help"></a><span data-ttu-id="2bb7a-155">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="2bb7a-155">Get help</span></span>
<span data-ttu-id="2bb7a-156">Per ottenere assistenza aggiuntiva, provare ad accedere al [forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="2bb7a-156">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2bb7a-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2bb7a-157">Next steps</span></span>
* [<span data-ttu-id="2bb7a-158">Presentazione di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="2bb7a-158">Introduction to Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="2bb7a-159">Introduzione ad Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="2bb7a-159">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="2bb7a-160">Scalabilità dei processi di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="2bb7a-160">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="2bb7a-161">Informazioni di riferimento sul linguaggio di query di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="2bb7a-161">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="2bb7a-162">Informazioni di riferimento sull'API REST di gestione di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="2bb7a-162">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
