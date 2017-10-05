---
title: "Analisi di flusso di Azure: ottimizzare il processo per l'uso efficiente delle unità di streaming | Documentazione Microsoft"
description: "Procedure consigliate di query per la scalabilità e le prestazioni in Analisi di flusso di Azure."
keywords: "unità di streaming, prestazioni delle query"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 1441a5df4fd92abf85763ca9a1512503b1a0da56
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="optimize-your-job-to-use-streaming-units-efficiently"></a><span data-ttu-id="f7dc5-104">Ottimizzare il processo per l'uso efficiente delle unità di streaming</span><span class="sxs-lookup"><span data-stu-id="f7dc5-104">Optimize your job to use Streaming Units efficiently</span></span>

<span data-ttu-id="f7dc5-105">Analisi di flusso di Azure aggrega il "peso" delle prestazioni dell'esecuzione di un processo in unità di streaming.</span><span class="sxs-lookup"><span data-stu-id="f7dc5-105">Azure Stream Analytics aggregates the performance "weight" of running a job into Streaming Units (SUs).</span></span> <span data-ttu-id="f7dc5-106">Le unità di streaming rappresentano le risorse di elaborazione che vengono usate per eseguire un processo.</span><span class="sxs-lookup"><span data-stu-id="f7dc5-106">SUs represent the computing resources that are consumed to execute a job.</span></span> <span data-ttu-id="f7dc5-107">Le unità di streaming descrivono la capacità relativa di elaborazione di eventi in base a una misurazione combinata di CPU, memoria e frequenze di lettura e scrittura.</span><span class="sxs-lookup"><span data-stu-id="f7dc5-107">SUs provide a way to describe the relative event processing capacity based on a blended measure of CPU, memory, and read and write rates.</span></span> <span data-ttu-id="f7dc5-108">Questa capacità consente di concentrarsi sulla logica della query, senza dover conoscere il funzionamento delle prestazioni del livello di archiviazione, allocare memoria per il processo manualmente e approssimare il numero di memorie centrali di CPU necessario per eseguire il processo in modo tempestivo.</span><span class="sxs-lookup"><span data-stu-id="f7dc5-108">This capacity lets you focus on the query logic and removes you from needing to know storage tier performance considerations, allocate memory for your job manually, and approximate the CPU core-count needed to run your job in a timely manner.</span></span>

## <a name="how-many-sus-are-required-for-a-job"></a><span data-ttu-id="f7dc5-109">Quante unità di streaming sono necessarie per un processo?</span><span class="sxs-lookup"><span data-stu-id="f7dc5-109">How many SUs are required for a job?</span></span>

<span data-ttu-id="f7dc5-110">Il numero di unità di streaming necessarie per un particolare processo dipende dalla configurazione della partizione per gli input e dalla query definita nel processo.</span><span class="sxs-lookup"><span data-stu-id="f7dc5-110">Choosing the number of required SUs for a particular job depends on the partition configuration for the inputs and the query that's defined within the job.</span></span> <span data-ttu-id="f7dc5-111">Il pannello **Scala** consente di impostare il numero corretto di unità di streaming.</span><span class="sxs-lookup"><span data-stu-id="f7dc5-111">The **Scale** blade allows you to set the right number of SUs.</span></span> <span data-ttu-id="f7dc5-112">È consigliabile allocare più unità di streaming di quelle necessarie.</span><span class="sxs-lookup"><span data-stu-id="f7dc5-112">It is a best practice to allocate more SUs than needed.</span></span> <span data-ttu-id="f7dc5-113">Il motore di elaborazione di Analisi di flusso è ottimizzato per la latenza e la velocità effettiva al costo di allocazione di memoria aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="f7dc5-113">The Stream Analytics processing engine optimizes for latency and throughput at the cost of allocating additional memory.</span></span>

<span data-ttu-id="f7dc5-114">In generale la procedura consigliata consiste nell'iniziare con 6 unità di streaming per le query che non usano *PARTITION BY*.</span><span class="sxs-lookup"><span data-stu-id="f7dc5-114">In general, the best practice is to start with 6 SUs for queries that don't use *PARTITION BY*.</span></span> <span data-ttu-id="f7dc5-115">Quindi determinare un punto di svolta usando un metodo di valutazione e correzione degli errori in cui si modifica il numero di unità di streaming dopo aver passato quantità rappresentative di dati ed esaminato la metrica di utilizzo %Utilization delle unità di streaming.</span><span class="sxs-lookup"><span data-stu-id="f7dc5-115">Then determine the sweet spot by using a trial and error method in which you modify the number of SUs after you pass representative amounts of data and examine the SU %Utilization metric.</span></span>

<span data-ttu-id="f7dc5-116">Analisi di flusso di Azure conserva gli eventi in una finestra denominata "buffer di riordino" prima di avviare qualsiasi elaborazione.</span><span class="sxs-lookup"><span data-stu-id="f7dc5-116">Azure Stream Analytics keeps events in a window called the “reorder buffer” before it starts any processing.</span></span> <span data-ttu-id="f7dc5-117">Gli eventi vengono ordinati all'interno della finestra di riordino in base all'orario e le operazioni successive vengono eseguite sugli eventi ordinati in sequenza temporale.</span><span class="sxs-lookup"><span data-stu-id="f7dc5-117">Events are sorted within the reorder window by time, and subsequent operations are performed on the temporally sorted events.</span></span> <span data-ttu-id="f7dc5-118">Riordinare gli eventi in base all'ora garantisce che l'operatore abbia visibilità su tutti gli eventi nell'intervallo di tempo stabilito.</span><span class="sxs-lookup"><span data-stu-id="f7dc5-118">Reordering events by time ensures that the operator has visibility into all the events in the stipulated timeframe.</span></span> <span data-ttu-id="f7dc5-119">Consente inoltre all'operatore di eseguire l'elaborazione necessaria e produrre un output.</span><span class="sxs-lookup"><span data-stu-id="f7dc5-119">It also lets the operator perform the requisite processing and produce an output.</span></span> <span data-ttu-id="f7dc5-120">Un effetto collaterale di questo meccanismo è che l'elaborazione viene posticipata del tempo corrispondente alla durata della finestra di riordino.</span><span class="sxs-lookup"><span data-stu-id="f7dc5-120">A side effect of this mechanism is that processing is delayed by the duration of the reorder window.</span></span> <span data-ttu-id="f7dc5-121">Il footprint di memoria del processo (che influisce sul consumo delle unità di streaming) è una funzione le cui dimensioni corrispondono alla finestra di riordino e al numero di eventi che contiene.</span><span class="sxs-lookup"><span data-stu-id="f7dc5-121">The memory footprint of the job (which affects SU consumption) is a function of the size of this reorder window and the number of events contained within it.</span></span>

> [!NOTE]
> <span data-ttu-id="f7dc5-122">Quando il numero di lettori cambia durante gli aggiornamenti del processo, vengono scritti avvisi temporanei nei log di controllo.</span><span class="sxs-lookup"><span data-stu-id="f7dc5-122">When the number of readers changes during job upgrades, transient warnings are written to audit logs.</span></span> <span data-ttu-id="f7dc5-123">I processi di Analisi di flusso vengono ripristinati automaticamente da questi problemi temporanei.</span><span class="sxs-lookup"><span data-stu-id="f7dc5-123">Stream Analytics jobs automatically recover from these transient issues.</span></span>

## <a name="common-high-memory-causes-for-high-su-usage-for-running-jobs"></a><span data-ttu-id="f7dc5-124">Cause comuni di memoria elevata per l'utilizzo elevato delle unità di streaming per i processi in esecuzione</span><span class="sxs-lookup"><span data-stu-id="f7dc5-124">Common high-memory causes for high SU usage for running jobs</span></span>

### <a name="high-cardinality-for-group-by"></a><span data-ttu-id="f7dc5-125">Elevata cardinalità di GROUP BY</span><span class="sxs-lookup"><span data-stu-id="f7dc5-125">High cardinality for GROUP BY</span></span>

<span data-ttu-id="f7dc5-126">La cardinalità degli eventi in ingresso determina l'uso della memoria per il processo.</span><span class="sxs-lookup"><span data-stu-id="f7dc5-126">The cardinality of incoming events dictates memory usage for the job.</span></span>

<span data-ttu-id="f7dc5-127">Ad esempio, in `SELECT count(*) from input group by clustered, tumblingwindow (minutes, 5)` la cardinalità della query è rappresentata dal numero associato a **cluster**.</span><span class="sxs-lookup"><span data-stu-id="f7dc5-127">For example, in `SELECT count(*) from input group by clustered, tumblingwindow (minutes, 5)`, the number associated with **clustered** is the cardinality of the query.</span></span>

<span data-ttu-id="f7dc5-128">Per limitare i problemi causati dalla cardinalità elevata, scalare orizzontalmente la query aumentando le partizioni mediante **PARTITION BY**.</span><span class="sxs-lookup"><span data-stu-id="f7dc5-128">To mitigate issues that are caused by high cardinality, scale out the query by increasing partitions using **PARTITION BY**.</span></span>

```
Select count(*) from input
Partition By clusterid
GROUP BY clustered tumblingwindow (minutes, 5)
```

<span data-ttu-id="f7dc5-129">Il numero di *cluster* rappresenta qui la cardinalità di GROUP BY.</span><span class="sxs-lookup"><span data-stu-id="f7dc5-129">The number of *clustered* is the cardinality of GROUP BY here.</span></span>

<span data-ttu-id="f7dc5-130">Dopo il partizionamento della query, viene distribuita su più nodi.</span><span class="sxs-lookup"><span data-stu-id="f7dc5-130">After the query is partitioned, it is spread out over multiple nodes.</span></span> <span data-ttu-id="f7dc5-131">Di conseguenza il numero di eventi in arrivo in ogni nodo diminuisce, riducendo così la dimensione del buffer di riordino.</span><span class="sxs-lookup"><span data-stu-id="f7dc5-131">As a result, the number of events coming into each node is reduced, which in turn reduces the size of the reorder buffer.</span></span> <span data-ttu-id="f7dc5-132">È inoltre consigliabile partizionare le partizioni dell'hub eventi in base all'ID partizione.</span><span class="sxs-lookup"><span data-stu-id="f7dc5-132">You should also partition event hub partitions by partitionid.</span></span>

### <a name="high-unmatched-event-count-for-join"></a><span data-ttu-id="f7dc5-133">Elevata quantità di eventi senza corrispondenza per JOIN</span><span class="sxs-lookup"><span data-stu-id="f7dc5-133">High unmatched event count for JOIN</span></span>

<span data-ttu-id="f7dc5-134">Il numero di eventi senza corrispondenza in un JOIN influisce sull'uso della memoria per la query.</span><span class="sxs-lookup"><span data-stu-id="f7dc5-134">The number of unmatched events in a JOIN affects the memory utilization of the query.</span></span> <span data-ttu-id="f7dc5-135">Ad esempio, si consideri una query che cerca il numero di impressioni di un annuncio che generano clic:</span><span class="sxs-lookup"><span data-stu-id="f7dc5-135">For example, take a query that is looking to find the number of ad impressions that generates clicks:</span></span>

```
SELECT id from clicks INNER JOIN,
impressions on impressions.id = clicks.id AND DATEDIFF(hour, impressions, clicks) between 0 AND 10
```

<span data-ttu-id="f7dc5-136">In questo scenario è possibile che vengano visualizzati molti annunci e siano generati pochi clic.</span><span class="sxs-lookup"><span data-stu-id="f7dc5-136">In this scenario, it is possible that many ads are shown and few clicks are generated.</span></span> <span data-ttu-id="f7dc5-137">Un risultato come questo richiede che il processo mantenga tutti gli eventi nell'intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="f7dc5-137">Such a result would require the job to keep all the events within the time window.</span></span> <span data-ttu-id="f7dc5-138">La quantità di memoria consumata è proporzionale alle dimensioni della finestra e alla frequenza degli eventi.</span><span class="sxs-lookup"><span data-stu-id="f7dc5-138">The amount of memory consumed is proportional to the window size and event rate.</span></span> 

<span data-ttu-id="f7dc5-139">Per evitare questa situazione, scalare orizzontalmente la query aumentando le partizioni tramite PARTITION BY.</span><span class="sxs-lookup"><span data-stu-id="f7dc5-139">To mitigate this situation, scale out the query by increasing partitions by using PARTITION BY.</span></span> 

<span data-ttu-id="f7dc5-140">Dopo il partizionamento della query, viene distribuita su più nodi di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="f7dc5-140">After the query is partitioned, it is spread out over multiple processing nodes.</span></span> <span data-ttu-id="f7dc5-141">Di conseguenza il numero di eventi in arrivo in ogni nodo diminuisce, riducendo così la dimensione del buffer di riordino.</span><span class="sxs-lookup"><span data-stu-id="f7dc5-141">As a result, the number of events coming into each node is reduced, which in turn reduces the size of the reorder buffer.</span></span>

### <a name="large-number-of-out-of-order-events"></a><span data-ttu-id="f7dc5-142">Quantità elevata di eventi fuori sequenza</span><span class="sxs-lookup"><span data-stu-id="f7dc5-142">Large number of out of order events</span></span> 

<span data-ttu-id="f7dc5-143">Un numero elevato di eventi fuori sequenza per un lungo intervallo di tempo causerà l'aumento della dimensione del "buffer di riordino".</span><span class="sxs-lookup"><span data-stu-id="f7dc5-143">A large number of out of order events within a large time window causes the size of the "reorder buffer" to be larger.</span></span> <span data-ttu-id="f7dc5-144">Per mitigare questa situazione, scalare la query aumentando le partizioni tramite PARTITION BY.</span><span class="sxs-lookup"><span data-stu-id="f7dc5-144">To mitigate this situation, scale the query by increasing partitions by using PARTITION BY.</span></span> <span data-ttu-id="f7dc5-145">Dopo il partizionamento della query, viene distribuita su più nodi.</span><span class="sxs-lookup"><span data-stu-id="f7dc5-145">After the query is partitioned, it is spread out over multiple nodes.</span></span> <span data-ttu-id="f7dc5-146">Di conseguenza il numero di eventi in arrivo in ogni nodo diminuisce, riducendo così la dimensione del buffer di riordino.</span><span class="sxs-lookup"><span data-stu-id="f7dc5-146">As a result, the number of events coming into each node is reduced, which in turn reduces the size of the reorder buffer.</span></span> 


## <a name="get-help"></a><span data-ttu-id="f7dc5-147">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="f7dc5-147">Get help</span></span>
<span data-ttu-id="f7dc5-148">Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="f7dc5-148">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7dc5-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f7dc5-149">Next steps</span></span>
* [<span data-ttu-id="f7dc5-150">Introduzione ad Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="f7dc5-150">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="f7dc5-151">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="f7dc5-151">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="f7dc5-152">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="f7dc5-152">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="f7dc5-153">Informazioni di riferimento sul linguaggio di query di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="f7dc5-153">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="f7dc5-154">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="f7dc5-154">Azure Stream Analytics Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
