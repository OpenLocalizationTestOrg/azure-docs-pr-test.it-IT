---
title: "Azure flusso Analitica: Ottimizzare il toouse processo unità di Streaming in modo efficiente | Documenti Microsoft"
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
ms.openlocfilehash: 5ad98b34d625190a879260f54c9eff0294e230cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-job-toouse-streaming-units-efficiently"></a><span data-ttu-id="8697d-104">Ottimizzare in modo efficiente il toouse processo unità di Streaming</span><span class="sxs-lookup"><span data-stu-id="8697d-104">Optimize your job toouse Streaming Units efficiently</span></span>

<span data-ttu-id="8697d-105">Azure flusso Analitica aggrega prestazioni hello "peso" dell'esecuzione di un processo in unità di Streaming (SUs).</span><span class="sxs-lookup"><span data-stu-id="8697d-105">Azure Stream Analytics aggregates hello performance "weight" of running a job into Streaming Units (SUs).</span></span> <span data-ttu-id="8697d-106">SUs rappresentano hello risorse elaborazione tooexecute utilizzato un processo.</span><span class="sxs-lookup"><span data-stu-id="8697d-106">SUs represent hello computing resources that are consumed tooexecute a job.</span></span> <span data-ttu-id="8697d-107">SUs forniscono un modo toodescribe hello relativo evento basata su una misura combinata di CPU, memoria, capacità di elaborazione, leggere e scrivere tariffe.</span><span class="sxs-lookup"><span data-stu-id="8697d-107">SUs provide a way toodescribe hello relative event processing capacity based on a blended measure of CPU, memory, and read and write rates.</span></span> <span data-ttu-id="8697d-108">Questo consente di capacità di concentrarsi sulla logica della query hello e rimuove la necessità di considerazioni sulle prestazioni di livello archiviazione tooknow, allocare memoria per il processo manualmente e approssimativo toorun core-numero necessario di hello CPU del processo in modo tempestivo.</span><span class="sxs-lookup"><span data-stu-id="8697d-108">This capacity lets you focus on hello query logic and removes you from needing tooknow storage tier performance considerations, allocate memory for your job manually, and approximate hello CPU core-count needed toorun your job in a timely manner.</span></span>

## <a name="how-many-sus-are-required-for-a-job"></a><span data-ttu-id="8697d-109">Quante unità di streaming sono necessarie per un processo?</span><span class="sxs-lookup"><span data-stu-id="8697d-109">How many SUs are required for a job?</span></span>

<span data-ttu-id="8697d-110">Scegliere il numero di hello di SUs necessari per un determinato processo dipende dalla configurazione di partizione hello per input hello e query hello è definito all'interno del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="8697d-110">Choosing hello number of required SUs for a particular job depends on hello partition configuration for hello inputs and hello query that's defined within hello job.</span></span> <span data-ttu-id="8697d-111">Hello **scala** pannello consente hello tooset numeri a destra di SUs.</span><span class="sxs-lookup"><span data-stu-id="8697d-111">hello **Scale** blade allows you tooset hello right number of SUs.</span></span> <span data-ttu-id="8697d-112">È una procedura consigliata tooallocate SUs più del necessario.</span><span class="sxs-lookup"><span data-stu-id="8697d-112">It is a best practice tooallocate more SUs than needed.</span></span> <span data-ttu-id="8697d-113">il motore di elaborazione Analitica flusso Hello Ottimizza per la latenza e velocità effettiva al costo di hello di allocazione di memoria aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="8697d-113">hello Stream Analytics processing engine optimizes for latency and throughput at hello cost of allocating additional memory.</span></span>

<span data-ttu-id="8697d-114">In generale, consigliata hello è toostart con 6 SUs per le query che non usano *PARTITION BY*.</span><span class="sxs-lookup"><span data-stu-id="8697d-114">In general, hello best practice is toostart with 6 SUs for queries that don't use *PARTITION BY*.</span></span> <span data-ttu-id="8697d-115">Determinare quindi ideale hello utilizzando un metodo di prove ed errori nel quale si modifica il numero di hello di SUs dopo è passare rappresentativo quantità di dati ed esaminare metrica di utilizzo % SU hello.</span><span class="sxs-lookup"><span data-stu-id="8697d-115">Then determine hello sweet spot by using a trial and error method in which you modify hello number of SUs after you pass representative amounts of data and examine hello SU %Utilization metric.</span></span>

<span data-ttu-id="8697d-116">Azure Analitica flusso mantiene gli eventi in una finestra denominata hello "Riordina buffer" prima di avviare qualsiasi elaborazione.</span><span class="sxs-lookup"><span data-stu-id="8697d-116">Azure Stream Analytics keeps events in a window called hello “reorder buffer” before it starts any processing.</span></span> <span data-ttu-id="8697d-117">Gli eventi vengono ordinati nella finestra di riordino hello tempo e operazioni successive vengono eseguite sugli eventi hello temporaneamente ordinato.</span><span class="sxs-lookup"><span data-stu-id="8697d-117">Events are sorted within hello reorder window by time, and subsequent operations are performed on hello temporally sorted events.</span></span> <span data-ttu-id="8697d-118">Riordinare gli eventi da tempo garantisce che l'operatore hello dispone della visibilità in tutti gli eventi di hello in hello stipulata intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="8697d-118">Reordering events by time ensures that hello operator has visibility into all hello events in hello stipulated timeframe.</span></span> <span data-ttu-id="8697d-119">Consente inoltre operatore hello elaborazione necessarie hello e produrre un output.</span><span class="sxs-lookup"><span data-stu-id="8697d-119">It also lets hello operator perform hello requisite processing and produce an output.</span></span> <span data-ttu-id="8697d-120">Un effetto collaterale di questo meccanismo è che l'elaborazione viene ritardata per la durata della finestra di riordino hello hello.</span><span class="sxs-lookup"><span data-stu-id="8697d-120">A side effect of this mechanism is that processing is delayed by hello duration of hello reorder window.</span></span> <span data-ttu-id="8697d-121">footprint di memoria Hello del processo di hello (che influisce su consumo SU) è una funzione della dimensione hello di questo numero di finestra e hello riordino degli eventi in esso contenuti.</span><span class="sxs-lookup"><span data-stu-id="8697d-121">hello memory footprint of hello job (which affects SU consumption) is a function of hello size of this reorder window and hello number of events contained within it.</span></span>

> [!NOTE]
> <span data-ttu-id="8697d-122">Quando il numero di hello di lettori cambia durante gli aggiornamenti di processi, avvisi temporanei vengono scritti tooaudit log.</span><span class="sxs-lookup"><span data-stu-id="8697d-122">When hello number of readers changes during job upgrades, transient warnings are written tooaudit logs.</span></span> <span data-ttu-id="8697d-123">I processi di Analisi di flusso vengono ripristinati automaticamente da questi problemi temporanei.</span><span class="sxs-lookup"><span data-stu-id="8697d-123">Stream Analytics jobs automatically recover from these transient issues.</span></span>

## <a name="common-high-memory-causes-for-high-su-usage-for-running-jobs"></a><span data-ttu-id="8697d-124">Cause comuni di memoria elevata per l'utilizzo elevato delle unità di streaming per i processi in esecuzione</span><span class="sxs-lookup"><span data-stu-id="8697d-124">Common high-memory causes for high SU usage for running jobs</span></span>

### <a name="high-cardinality-for-group-by"></a><span data-ttu-id="8697d-125">Elevata cardinalità di GROUP BY</span><span class="sxs-lookup"><span data-stu-id="8697d-125">High cardinality for GROUP BY</span></span>

<span data-ttu-id="8697d-126">utilizzo della memoria per il processo di hello determina la cardinalità Hello di eventi in entrata.</span><span class="sxs-lookup"><span data-stu-id="8697d-126">hello cardinality of incoming events dictates memory usage for hello job.</span></span>

<span data-ttu-id="8697d-127">Ad esempio, in `SELECT count(*) from input group by clustered, tumblingwindow (minutes, 5)`, hello numero associato **cluster** è cardinalità hello di query hello.</span><span class="sxs-lookup"><span data-stu-id="8697d-127">For example, in `SELECT count(*) from input group by clustered, tumblingwindow (minutes, 5)`, hello number associated with **clustered** is hello cardinality of hello query.</span></span>

<span data-ttu-id="8697d-128">toomitigate problemi causati dalla cardinalità elevata, scalabilità query hello aumentando partizioni utilizzando **PARTITION BY**.</span><span class="sxs-lookup"><span data-stu-id="8697d-128">toomitigate issues that are caused by high cardinality, scale out hello query by increasing partitions using **PARTITION BY**.</span></span>

```
Select count(*) from input
Partition By clusterid
GROUP BY clustered tumblingwindow (minutes, 5)
```

<span data-ttu-id="8697d-129">numero di Hello *cluster* è cardinalità hello del gruppo da qui.</span><span class="sxs-lookup"><span data-stu-id="8697d-129">hello number of *clustered* is hello cardinality of GROUP BY here.</span></span>

<span data-ttu-id="8697d-130">Dopo che la query hello è partizionata, viene ripartito su più nodi.</span><span class="sxs-lookup"><span data-stu-id="8697d-130">After hello query is partitioned, it is spread out over multiple nodes.</span></span> <span data-ttu-id="8697d-131">Di conseguenza, il numero di hello di eventi in arrivo in ogni nodo è ridotto, che a sua volta consente di ridurre hello dimensioni del buffer di riordino hello.</span><span class="sxs-lookup"><span data-stu-id="8697d-131">As a result, hello number of events coming into each node is reduced, which in turn reduces hello size of hello reorder buffer.</span></span> <span data-ttu-id="8697d-132">È inoltre consigliabile partizionare le partizioni dell'hub eventi in base all'ID partizione.</span><span class="sxs-lookup"><span data-stu-id="8697d-132">You should also partition event hub partitions by partitionid.</span></span>

### <a name="high-unmatched-event-count-for-join"></a><span data-ttu-id="8697d-133">Elevata quantità di eventi senza corrispondenza per JOIN</span><span class="sxs-lookup"><span data-stu-id="8697d-133">High unmatched event count for JOIN</span></span>

<span data-ttu-id="8697d-134">numero di Hello di eventi non corrispondenti in un JOIN influisce hello quantità di memoria utilizzata query hello.</span><span class="sxs-lookup"><span data-stu-id="8697d-134">hello number of unmatched events in a JOIN affects hello memory utilization of hello query.</span></span> <span data-ttu-id="8697d-135">Ad esempio, eseguire una query che esegue la ricerca toofind hello svariate impressioni ad che genera l'errore clic:</span><span class="sxs-lookup"><span data-stu-id="8697d-135">For example, take a query that is looking toofind hello number of ad impressions that generates clicks:</span></span>

```
SELECT id from clicks INNER JOIN,
impressions on impressions.id = clicks.id AND DATEDIFF(hour, impressions, clicks) between 0 AND 10
```

<span data-ttu-id="8697d-136">In questo scenario è possibile che vengano visualizzati molti annunci e siano generati pochi clic.</span><span class="sxs-lookup"><span data-stu-id="8697d-136">In this scenario, it is possible that many ads are shown and few clicks are generated.</span></span> <span data-ttu-id="8697d-137">Questo errore richiederebbe hello processo tookeep tutti gli eventi di hello in hello intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="8697d-137">Such a result would require hello job tookeep all hello events within hello time window.</span></span> <span data-ttu-id="8697d-138">quantità di Hello di memoria utilizzata è di tipo tasso di dimensioni e di eventi finestra toohello proporzionale.</span><span class="sxs-lookup"><span data-stu-id="8697d-138">hello amount of memory consumed is proportional toohello window size and event rate.</span></span> 

<span data-ttu-id="8697d-139">toomitigate questa situazione, la scalabilità orizzontale query hello aumentando partizioni tramite PARTITION BY.</span><span class="sxs-lookup"><span data-stu-id="8697d-139">toomitigate this situation, scale out hello query by increasing partitions by using PARTITION BY.</span></span> 

<span data-ttu-id="8697d-140">Dopo che la query hello è partizionata, viene ripartito su più nodi di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="8697d-140">After hello query is partitioned, it is spread out over multiple processing nodes.</span></span> <span data-ttu-id="8697d-141">Di conseguenza, il numero di hello di eventi in arrivo in ogni nodo è ridotto, che a sua volta consente di ridurre hello dimensioni del buffer di riordino hello.</span><span class="sxs-lookup"><span data-stu-id="8697d-141">As a result, hello number of events coming into each node is reduced, which in turn reduces hello size of hello reorder buffer.</span></span>

### <a name="large-number-of-out-of-order-events"></a><span data-ttu-id="8697d-142">Quantità elevata di eventi fuori sequenza</span><span class="sxs-lookup"><span data-stu-id="8697d-142">Large number of out of order events</span></span> 

<span data-ttu-id="8697d-143">Un numero elevato di eventi non in ordine all'interno di un intervallo di tempo di grandi dimensioni comporta dimensioni hello di hello "riordinare buffer" toobe più grande.</span><span class="sxs-lookup"><span data-stu-id="8697d-143">A large number of out of order events within a large time window causes hello size of hello "reorder buffer" toobe larger.</span></span> <span data-ttu-id="8697d-144">toomitigate questa situazione, query hello scala aumentando partizioni tramite PARTITION BY.</span><span class="sxs-lookup"><span data-stu-id="8697d-144">toomitigate this situation, scale hello query by increasing partitions by using PARTITION BY.</span></span> <span data-ttu-id="8697d-145">Dopo che la query hello è partizionata, viene ripartito su più nodi.</span><span class="sxs-lookup"><span data-stu-id="8697d-145">After hello query is partitioned, it is spread out over multiple nodes.</span></span> <span data-ttu-id="8697d-146">Di conseguenza, il numero di hello di eventi in arrivo in ogni nodo è ridotto, che a sua volta consente di ridurre hello dimensioni del buffer di riordino hello.</span><span class="sxs-lookup"><span data-stu-id="8697d-146">As a result, hello number of events coming into each node is reduced, which in turn reduces hello size of hello reorder buffer.</span></span> 


## <a name="get-help"></a><span data-ttu-id="8697d-147">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="8697d-147">Get help</span></span>
<span data-ttu-id="8697d-148">Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="8697d-148">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8697d-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8697d-149">Next steps</span></span>
* [<span data-ttu-id="8697d-150">Introduzione tooAzure flusso Analitica</span><span class="sxs-lookup"><span data-stu-id="8697d-150">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="8697d-151">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="8697d-151">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="8697d-152">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="8697d-152">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="8697d-153">Informazioni di riferimento sul linguaggio di query di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="8697d-153">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="8697d-154">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="8697d-154">Azure Stream Analytics Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
