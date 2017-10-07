---
title: aaa Analitica di flusso di Azure basate sui dati debug tramite il diagramma di processo hello | Documenti Microsoft
description: Risoluzione dei problemi con il processo di flusso Analitica metriche e Diagramma processo hello.
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
ms.openlocfilehash: 1af884d485bebb06b034da01a13f7f8240516571
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="data-driven-debugging-by-using-hello-job-diagram"></a><span data-ttu-id="128a7-103">Il debug con il diagramma di processo hello guidate dai dati</span><span class="sxs-lookup"><span data-stu-id="128a7-103">Data-driven debugging by using hello job diagram</span></span>

<span data-ttu-id="128a7-104">diagramma di processo Hello su hello **monitoraggio** pannello nel portale di Azure hello consentono di visualizzare la pipeline di processo.</span><span class="sxs-lookup"><span data-stu-id="128a7-104">hello job diagram on hello **Monitoring** blade in hello Azure portal can help you visualize your job pipeline.</span></span> <span data-ttu-id="128a7-105">Mostra gli input, gli output e i passaggi delle query.</span><span class="sxs-lookup"><span data-stu-id="128a7-105">It shows inputs, outputs, and query steps.</span></span> <span data-ttu-id="128a7-106">È possibile usare le metriche hello di hello processo diagramma tooexamine per ogni passaggio, toomore isolare rapidamente origine hello di un problema durante la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="128a7-106">You can use hello job diagram tooexamine hello metrics for each step, toomore quickly isolate hello source of a problem when you troubleshoot issues.</span></span>

## <a name="using-hello-job-diagram"></a><span data-ttu-id="128a7-107">Utilizzando il diagramma di processo hello</span><span class="sxs-lookup"><span data-stu-id="128a7-107">Using hello job diagram</span></span>

<span data-ttu-id="128a7-108">Nel portale di Azure hello mentre in un processo di flusso Analitica, in **supporto + risoluzione dei problemi**selezionare **Diagramma processo**:</span><span class="sxs-lookup"><span data-stu-id="128a7-108">In hello Azure portal, while in a Stream Analytics job, under **SUPPORT + TROUBLESHOOTING**, select **Job diagram**:</span></span>

![Diagramma di processo con metriche - posizione](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-1.png)

<span data-ttu-id="128a7-110">Selezionare ogni sezione corrispondente di hello toosee query passaggio in un riquadro di modifica di query.</span><span class="sxs-lookup"><span data-stu-id="128a7-110">Select each query step toosee hello corresponding section in a query editing pane.</span></span> <span data-ttu-id="128a7-111">Viene visualizzato un grafico di metrica per il passaggio di hello in un riquadro inferiore della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="128a7-111">A metric chart for hello step is displayed in a lower pane on hello page.</span></span>

![Diagramma di processo con metriche - processo di base](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-2.png)

<span data-ttu-id="128a7-113">Selezionare le partizioni di hello toosee di input dell'hub eventi di Azure hello **...**</span><span class="sxs-lookup"><span data-stu-id="128a7-113">toosee hello partitions of hello Azure Event Hubs input, select **. . .**</span></span> <span data-ttu-id="128a7-114">Si apre il menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="128a7-114">A context menu appears.</span></span> <span data-ttu-id="128a7-115">È inoltre possibile visualizzare unione input hello.</span><span class="sxs-lookup"><span data-stu-id="128a7-115">You also can see hello input merger.</span></span>

![Diagramma di processo con metriche - espandere la partizione](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-3.png)

<span data-ttu-id="128a7-117">grafico metrica hello di toosee per una singola partizione, il nodo di partizione selezionare hello.</span><span class="sxs-lookup"><span data-stu-id="128a7-117">toosee hello metric chart for only a single partition, select hello partition node.</span></span> <span data-ttu-id="128a7-118">le metriche Hello vengono visualizzate nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="128a7-118">hello metrics are shown at hello bottom of hello page.</span></span>

![Diagramma di processo con metriche - altre metriche](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-4.png)

<span data-ttu-id="128a7-120">grafico delle metriche di hello toosee per una fusione, nodo unione hello selezionare.</span><span class="sxs-lookup"><span data-stu-id="128a7-120">toosee hello metrics chart for a merger, select hello merger node.</span></span> <span data-ttu-id="128a7-121">Hello seguente grafico mostra che gli eventi non sono stati rimossi o modificati.</span><span class="sxs-lookup"><span data-stu-id="128a7-121">hello following chart shows that no events were dropped or adjusted.</span></span>

![Diagramma di processo con metriche - griglia](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-5.png)

<span data-ttu-id="128a7-123">dettagli di hello toosee del valore della metrica hello e l'ora, il grafico toohello punto.</span><span class="sxs-lookup"><span data-stu-id="128a7-123">toosee hello details of hello metric value and time, point toohello chart.</span></span>

![Diagramma di processo con metriche - puntare con il mouse](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-6.png)

## <a name="troubleshoot-by-using-metrics"></a><span data-ttu-id="128a7-125">Risolvere i problemi mediante le metriche</span><span class="sxs-lookup"><span data-stu-id="128a7-125">Troubleshoot by using metrics</span></span>

<span data-ttu-id="128a7-126">Hello **QueryLastProcessedTime** metrica indica quando un passaggio specifico ha ricevuto dati.</span><span class="sxs-lookup"><span data-stu-id="128a7-126">hello **QueryLastProcessedTime** metric indicates when a specific step received data.</span></span> <span data-ttu-id="128a7-127">Osservando la topologia hello, è possibile lavorare all'indietro da hello output processore toosee il passaggio non riceve dati.</span><span class="sxs-lookup"><span data-stu-id="128a7-127">By looking at hello topology, you can work backward from hello output processor toosee which step is not receiving data.</span></span> <span data-ttu-id="128a7-128">Se un passaggio non ottiene i dati, passare passaggio della query toohello subito prima.</span><span class="sxs-lookup"><span data-stu-id="128a7-128">If a step is not getting data, go toohello query step just before it.</span></span> <span data-ttu-id="128a7-129">Verificare se il passaggio della query precedente hello è un intervallo di tempo e se è trascorso tempo sufficiente toooutput dati.</span><span class="sxs-lookup"><span data-stu-id="128a7-129">Check whether hello preceding query step has a time window, and if enough time has passed for it toooutput data.</span></span> <span data-ttu-id="128a7-130">(Si noti che ora windows sono ora bloccati toohello.)</span><span class="sxs-lookup"><span data-stu-id="128a7-130">(Note that time windows are snapped toohello hour.)</span></span>
 
<span data-ttu-id="128a7-131">Se hello passaggio della query precedente è un processore di input, utilizzare hello di hello metriche input toohelp risposte seguenti domande di destinazione.</span><span class="sxs-lookup"><span data-stu-id="128a7-131">If hello preceding query step is an input processor, use hello input metrics toohelp answer hello following targeted questions.</span></span> <span data-ttu-id="128a7-132">Esse consentono di determinare se un processo sta ricevendo dati dalle sue origini di input.</span><span class="sxs-lookup"><span data-stu-id="128a7-132">They can help you determine whether a job is getting data from its input sources.</span></span> <span data-ttu-id="128a7-133">Se la query hello è partizionata, è possibile esaminare ogni partizione.</span><span class="sxs-lookup"><span data-stu-id="128a7-133">If hello query is partitioned, examine each partition.</span></span>
 
### <a name="how-much-data-is-being-read"></a><span data-ttu-id="128a7-134">Quanti dati vengono letti?</span><span class="sxs-lookup"><span data-stu-id="128a7-134">How much data is being read?</span></span>

*   <span data-ttu-id="128a7-135">**InputEventsSourcesTotal** hello numero di unità di dati di lettura.</span><span class="sxs-lookup"><span data-stu-id="128a7-135">**InputEventsSourcesTotal** is hello number of data units read.</span></span> <span data-ttu-id="128a7-136">Salve, ad esempio, numero di BLOB.</span><span class="sxs-lookup"><span data-stu-id="128a7-136">For example, hello number of blobs.</span></span>
*   <span data-ttu-id="128a7-137">**InputEventsTotal** hello numero di eventi di lettura.</span><span class="sxs-lookup"><span data-stu-id="128a7-137">**InputEventsTotal** is hello number of events read.</span></span> <span data-ttu-id="128a7-138">Questa metrica è disponibile per ogni partizione.</span><span class="sxs-lookup"><span data-stu-id="128a7-138">This metric is available per partition.</span></span>
*   <span data-ttu-id="128a7-139">**InputEventsInBytesTotal** hello numero di byte letti.</span><span class="sxs-lookup"><span data-stu-id="128a7-139">**InputEventsInBytesTotal** is hello number of bytes read.</span></span>
*   <span data-ttu-id="128a7-140">**InputEventsLastArrivalTime** viene aggiornato con l'ora di accodamento di ogni evento ricevuto.</span><span class="sxs-lookup"><span data-stu-id="128a7-140">**InputEventsLastArrivalTime** is updated with every received event's enqueued time.</span></span>
 
### <a name="is-time-moving-forward-if-actual-events-are-read-punctuation-might-not-be-issued"></a><span data-ttu-id="128a7-141">L'ora viene spostata in avanti?</span><span class="sxs-lookup"><span data-stu-id="128a7-141">Is time moving forward?</span></span> <span data-ttu-id="128a7-142">Se vengono letti eventi reali, potrebbe non essere generata la punteggiatura.</span><span class="sxs-lookup"><span data-stu-id="128a7-142">If actual events are read, punctuation might not be issued.</span></span>

*   <span data-ttu-id="128a7-143">**InputEventsLastPunctuationTime** indica un segno di punteggiatura emissione tookeep ora spostare in avanti.</span><span class="sxs-lookup"><span data-stu-id="128a7-143">**InputEventsLastPunctuationTime** indicates when a punctuation was issued tookeep time moving forward.</span></span> <span data-ttu-id="128a7-144">Se la punteggiatura non viene generata, il flusso di dati può bloccarsi.</span><span class="sxs-lookup"><span data-stu-id="128a7-144">If punctuation is not issued, data flow can get blocked.</span></span>
 
### <a name="are-there-any-errors-in-hello-input"></a><span data-ttu-id="128a7-145">Sono presenti errori di input hello?</span><span class="sxs-lookup"><span data-stu-id="128a7-145">Are there any errors in hello input?</span></span>

*   <span data-ttu-id="128a7-146">**InputEventsEventDataNullTotal** è un conteggio degli eventi con dati Null.</span><span class="sxs-lookup"><span data-stu-id="128a7-146">**InputEventsEventDataNullTotal** is a count of events that have null data.</span></span>
*   <span data-ttu-id="128a7-147">**InputEventsSerializerErrorsTotal** è un conteggio degli eventi che non è stato possibile deserializzare correttamente.</span><span class="sxs-lookup"><span data-stu-id="128a7-147">**InputEventsSerializerErrorsTotal** is a count of events that could not be deserialized correctly.</span></span>
*   <span data-ttu-id="128a7-148">**InputEventsDegradedTotal** è un conteggio degli eventi che sono stati interessati da un problema diverso dalla deserializzazione.</span><span class="sxs-lookup"><span data-stu-id="128a7-148">**InputEventsDegradedTotal** is a count of events that had an issue other than with deserialization.</span></span>
 
### <a name="are-events-being-dropped-or-adjusted"></a><span data-ttu-id="128a7-149">Vengono eliminati o modificati eventi?</span><span class="sxs-lookup"><span data-stu-id="128a7-149">Are events being dropped or adjusted?</span></span>

*   <span data-ttu-id="128a7-150">**InputEventsEarlyTotal** hello numero di eventi con un timestamp dell'applicazione prima di limite massimo di hello.</span><span class="sxs-lookup"><span data-stu-id="128a7-150">**InputEventsEarlyTotal** is hello number of events that have an application timestamp before hello high watermark.</span></span>
*   <span data-ttu-id="128a7-151">**InputEventsLateTotal** hello numero di eventi con un timestamp dell'applicazione dopo il limite massimo di hello.</span><span class="sxs-lookup"><span data-stu-id="128a7-151">**InputEventsLateTotal** is hello number of events that have an application timestamp after hello high watermark.</span></span>
*   <span data-ttu-id="128a7-152">**InputEventsDroppedBeforeApplicationStartTimeTotal** è hello numero di eventi eliminato prima dell'ora di inizio processo hello.</span><span class="sxs-lookup"><span data-stu-id="128a7-152">**InputEventsDroppedBeforeApplicationStartTimeTotal** is hello number events dropped before hello job start time.</span></span>
 
### <a name="are-we-falling-behind-in-reading-data"></a><span data-ttu-id="128a7-153">Si sta verificando un ritardo nella lettura dei dati?</span><span class="sxs-lookup"><span data-stu-id="128a7-153">Are we falling behind in reading data?</span></span>

*   <span data-ttu-id="128a7-154">**InputEventsSourcesBackloggedTotal** indica quanti messaggi più necessario toobe di lettura per gli input di hub eventi e IoT Hub di Azure.</span><span class="sxs-lookup"><span data-stu-id="128a7-154">**InputEventsSourcesBackloggedTotal** tells you how many more messages need toobe read for Event Hubs and Azure IoT Hub inputs.</span></span>


## <a name="get-help"></a><span data-ttu-id="128a7-155">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="128a7-155">Get help</span></span>
<span data-ttu-id="128a7-156">Per ottenere assistenza aggiuntiva, provare ad accedere al [forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="128a7-156">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="128a7-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="128a7-157">Next steps</span></span>
* [<span data-ttu-id="128a7-158">Introduzione tooStream Analitica</span><span class="sxs-lookup"><span data-stu-id="128a7-158">Introduction tooStream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="128a7-159">Introduzione ad Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="128a7-159">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="128a7-160">Scalabilità dei processi di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="128a7-160">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="128a7-161">Informazioni di riferimento sul linguaggio di query di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="128a7-161">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="128a7-162">Informazioni di riferimento sull'API REST di gestione di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="128a7-162">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
