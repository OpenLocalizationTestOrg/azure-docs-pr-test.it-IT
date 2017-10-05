---
title: "Ridimensionare i processi di analisi di flusso per aumentare la velocità effettiva | Microsoft Docs"
description: "Informazioni su come ridimensionare i processi di Analisi di flusso configurando partizioni di input, ottimizzando la definizione di query e impostando le unità di streaming del processo."
keywords: flusso di dati, elaborazione del flusso di dati, ottimizzare analisi
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 7e857ddb-71dd-4537-b7ab-4524335d7b35
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/22/2017
ms.author: jeffstok
ms.openlocfilehash: ab894976c72ea3785d7f58e51b3dd64511e1e8e3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="scale-azure-stream-analytics-jobs-to-increase-stream-data-processing-throughput"></a><span data-ttu-id="38774-104">Ridimensionare i processi di Analisi di flusso di Azure per aumentare la velocità effettiva dell'elaborazione dei flussi di dati</span><span class="sxs-lookup"><span data-stu-id="38774-104">Scale Azure Stream Analytics jobs to increase stream data processing throughput</span></span>
<span data-ttu-id="38774-105">Questo articolo illustra come ottimizzare una query per aumentare la velocità effettiva per i processi di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="38774-105">This article shows you how to tune a Stream Analytics query to increase throughput for Streaming Analytics jobs.</span></span> <span data-ttu-id="38774-106">Si apprenderà come ridimensionare tali processi configurando partizioni di input, ottimizzando la definizione di query, calcolando e impostando le *unità di streaming* dei processi.</span><span class="sxs-lookup"><span data-stu-id="38774-106">You learn how to scale Stream Analytics jobs by configuring input partitions, tuning the analytics query definition, and calculating and setting job *streaming units* (SUs).</span></span> 

## <a name="what-are-the-parts-of-a-stream-analytics-job"></a><span data-ttu-id="38774-107">Quali sono le parti di un processo di Analisi di flusso?</span><span class="sxs-lookup"><span data-stu-id="38774-107">What are the parts of a Stream Analytics job?</span></span>
<span data-ttu-id="38774-108">Una definizione del processo di Analisi di flusso include input, query e output.</span><span class="sxs-lookup"><span data-stu-id="38774-108">A Stream Analytics job definition includes inputs, a query, and output.</span></span> <span data-ttu-id="38774-109">Gli input sono le origini da cui il processo legge il flusso di dati,</span><span class="sxs-lookup"><span data-stu-id="38774-109">Inputs are where the job reads the data stream from.</span></span> <span data-ttu-id="38774-110">la query viene usata per trasformare il flusso di input dei dati e l'output è la destinazione a cui il processo invia i risultati.</span><span class="sxs-lookup"><span data-stu-id="38774-110">The query is used to transform the data input stream, and the output is where the job sends the job results to.</span></span>  

<span data-ttu-id="38774-111">Un processo richiede almeno un'origine di input per il flusso dei dati.</span><span class="sxs-lookup"><span data-stu-id="38774-111">A job requires at least one input source for data streaming.</span></span> <span data-ttu-id="38774-112">L'origine dell'input del flusso dei dati può essere archiviata in un hub eventi di Azure o in una risorsa di archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="38774-112">The data stream input source can be stored in an Azure event hub or in Azure blob storage.</span></span> <span data-ttu-id="38774-113">Per altre informazioni, vedere [Introduzione all'analisi di flusso di Azure](stream-analytics-introduction.md) e [Introduzione all'uso dell'analisi di flusso di Azure](stream-analytics-real-time-fraud-detection.md).</span><span class="sxs-lookup"><span data-stu-id="38774-113">For more information, see [Introduction to Azure Stream Analytics](stream-analytics-introduction.md) and [Get started using Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md).</span></span>

## <a name="partitions-in-event-hubs-and-azure-storage"></a><span data-ttu-id="38774-114">Partizioni negli hub eventi e nell'archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="38774-114">Partitions in event hubs and Azure storage</span></span>
<span data-ttu-id="38774-115">Il ridimensionamento di un processo di Analisi di flusso sfrutta i vantaggi offerti dall'uso di partizioni nell'input o nell'output.</span><span class="sxs-lookup"><span data-stu-id="38774-115">Scaling a Stream Analytics job takes advantage of partitions in the input or output.</span></span> <span data-ttu-id="38774-116">Il partizionamento consente di suddividere i dati in subset in base a una chiave di partizione.</span><span class="sxs-lookup"><span data-stu-id="38774-116">Partitioning lets you divide data into subsets based on a partition key.</span></span> <span data-ttu-id="38774-117">Un processo che utilizza i dati, come avviene per i processi di Analisi di flusso, può utilizzare diverse partizioni e scrivervi in parallelo, aumentando così la velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="38774-117">A process that consumes the data (such as a Streaming Analytics job) can consume and write different partitions in parallel, which increases throughput.</span></span> <span data-ttu-id="38774-118">Quando si usa Analisi di flusso, è possibile sfruttare il partizionamento negli hub eventi e nell'archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="38774-118">When you work with Streaming Analytics, you can take advantage of partitioning in event hubs and in Blob storage.</span></span> 

<span data-ttu-id="38774-119">Per altre informazioni sulle partizioni, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="38774-119">For more information about partitions, see the following articles:</span></span>

* [<span data-ttu-id="38774-120">Panoramica delle funzionalità di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="38774-120">Event Hubs features overview</span></span>](../event-hubs/event-hubs-features.md#partitions)
* [<span data-ttu-id="38774-121">Partizionamento dei dati</span><span class="sxs-lookup"><span data-stu-id="38774-121">Data partitioning</span></span>](https://docs.microsoft.com/azure/architecture/best-practices/data-partitioning#partitioning-azure-blob-storage)


## <a name="streaming-units-sus"></a><span data-ttu-id="38774-122">Unità di streaming</span><span class="sxs-lookup"><span data-stu-id="38774-122">Streaming units (SUs)</span></span>
<span data-ttu-id="38774-123">Le unità di streaming rappresentano le risorse e la potenza di elaborazione necessarie per eseguire un processo di Analisi di flusso di Azure.</span><span class="sxs-lookup"><span data-stu-id="38774-123">Streaming units (SUs) represent the resources and computing power that are required in order to execute an Azure Stream Analytics job.</span></span> <span data-ttu-id="38774-124">Le unità di streaming descrivono la capacità relativa di elaborazione di eventi in base a una misurazione combinata di CPU, memoria e frequenze di lettura e scrittura.</span><span class="sxs-lookup"><span data-stu-id="38774-124">SUs provide a way to describe the relative event processing capacity based on a blended measure of CPU, memory, and read and write rates.</span></span> <span data-ttu-id="38774-125">Ogni unità di streaming corrisponde a circa 1 MB al secondo di velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="38774-125">Each SU corresponds to roughly 1 MB/second of throughput.</span></span> 

<span data-ttu-id="38774-126">Il numero di unità di streaming necessarie per un particolare processo dipende dalla configurazione delle partizioni per gli input e dalla query definita per il processo.</span><span class="sxs-lookup"><span data-stu-id="38774-126">Choosing how many SUs are required for a particular job depends on the partition configuration for the inputs and on the query defined for the job.</span></span> <span data-ttu-id="38774-127">È prevista una quota massima di unità di streaming che è possibile selezionare per un processo.</span><span class="sxs-lookup"><span data-stu-id="38774-127">You can select up to your quota in SUs for a job.</span></span> <span data-ttu-id="38774-128">Per impostazione predefinita, ogni sottoscrizione di Azure ha una quota massima di 50 unità di streaming per tutti i processi di analisi in un'area specifica.</span><span class="sxs-lookup"><span data-stu-id="38774-128">By default, each Azure subscription has a quota of up to 50 SUs for all the analytics jobs in a specific region.</span></span> <span data-ttu-id="38774-129">Per superare la quota massima di unità di streaming per le sottoscrizioni, contattare il [supporto tecnico Microsoft](http://support.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="38774-129">To increase SUs for your subscriptions beyond this quota, contact [Microsoft Support](http://support.microsoft.com).</span></span> <span data-ttu-id="38774-130">I valori validi di unità di streaming per processo sono 1, 3, 6 e poi a salire, con incrementi di 6.</span><span class="sxs-lookup"><span data-stu-id="38774-130">Valid values for SUs per job are 1, 3, 6, and up in increments of 6.</span></span>

## <a name="embarrassingly-parallel-jobs"></a><span data-ttu-id="38774-131">Processi perfettamente paralleli</span><span class="sxs-lookup"><span data-stu-id="38774-131">Embarrassingly parallel jobs</span></span>
<span data-ttu-id="38774-132">Un processo *perfettamente parallelo* è lo scenario più scalabile che può presentarsi in Analisi di flusso di Azure.</span><span class="sxs-lookup"><span data-stu-id="38774-132">An *embarrassingly parallel* job is the most scalable scenario we have in Azure Stream Analytics.</span></span> <span data-ttu-id="38774-133">Connette una partizione dell'input inviato a un'istanza della query a una partizione dell'output.</span><span class="sxs-lookup"><span data-stu-id="38774-133">It connects one partition of the input to one instance of the query to one partition of the output.</span></span> <span data-ttu-id="38774-134">Questo parallelismo presenta i requisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="38774-134">This parallelism has the following requirements:</span></span>

1. <span data-ttu-id="38774-135">Se la logica di query richiede che la stessa chiave venga elaborata dalla stessa istanza di query, è necessario verificare che gli eventi siano diretti alla stessa partizione dell'input.</span><span class="sxs-lookup"><span data-stu-id="38774-135">If your query logic depends on the same key being processed by the same query instance, you must make sure that the events go to the same partition of your input.</span></span> <span data-ttu-id="38774-136">Per gli hub eventi, questo significa che per i dati di evento deve essere impostata la proprietà **PartitionKey**.</span><span class="sxs-lookup"><span data-stu-id="38774-136">For event hubs, this means that the event data must have the **PartitionKey** value set.</span></span> <span data-ttu-id="38774-137">In alternativa, è possibile usare mittenti partizionati.</span><span class="sxs-lookup"><span data-stu-id="38774-137">Alternatively, you can use partitioned senders.</span></span> <span data-ttu-id="38774-138">Per l'archiviazione BLOB, questo significa che gli eventi vengono inviati alla stessa cartella di partizione.</span><span class="sxs-lookup"><span data-stu-id="38774-138">For blob storage, this means that the events are sent to the same partition folder.</span></span> <span data-ttu-id="38774-139">Se la logica di query non richiede che la stessa chiave venga elaborata dalla stessa istanza di query, è possibile ignorare questo requisito.</span><span class="sxs-lookup"><span data-stu-id="38774-139">If your query logic does not require the same key to be processed by the same query instance, you can ignore this requirement.</span></span> <span data-ttu-id="38774-140">Un esempio di questa logica è offerto da una query semplice select-project-filter.</span><span class="sxs-lookup"><span data-stu-id="38774-140">An example of this logic would be a simple select-project-filter query.</span></span>  

2. <span data-ttu-id="38774-141">Quando i dati sono disposti a livello di input, si deve verificare che la query sia partizionata.</span><span class="sxs-lookup"><span data-stu-id="38774-141">Once the data is laid out on the input side, you must make sure that your query is partitioned.</span></span> <span data-ttu-id="38774-142">A questo scopo, è necessario usare la clausola **Partition By** in tutti i passaggi.</span><span class="sxs-lookup"><span data-stu-id="38774-142">This requires you to use **Partition By** in all the steps.</span></span> <span data-ttu-id="38774-143">È possibile eseguire più passaggi, ma tutti devono essere partizionati con la stessa chiave.</span><span class="sxs-lookup"><span data-stu-id="38774-143">Multiple steps are allowed, but they all must be partitioned by the same key.</span></span> <span data-ttu-id="38774-144">Per ottenere un processo completamente parallelo, è attualmente necessario impostare la chiave di partizionamento su **PartitionId**.</span><span class="sxs-lookup"><span data-stu-id="38774-144">Currently, the partitioning key must be set to **PartitionId** in order for the job to be fully parallel.</span></span>  

3. <span data-ttu-id="38774-145">Solo gli hub eventi e l'archiviazione BLOB supportano attualmente l'output partizionato.</span><span class="sxs-lookup"><span data-stu-id="38774-145">Currently only event hubs and blob storage support partitioned output.</span></span> <span data-ttu-id="38774-146">Per l'output degli hub eventi, è necessario configurare la chiave di partizione come **PartitionId**.</span><span class="sxs-lookup"><span data-stu-id="38774-146">For event hub output, you must configure the partition key to be **PartitionId**.</span></span> <span data-ttu-id="38774-147">Per l'output dell'archiviazione BLOB, non è necessario eseguire operazioni.</span><span class="sxs-lookup"><span data-stu-id="38774-147">For blob storage output, you don't have to do anything.</span></span>  

4. <span data-ttu-id="38774-148">Il numero delle partizioni di input deve essere uguale a quello delle partizioni di output.</span><span class="sxs-lookup"><span data-stu-id="38774-148">The number of input partitions must equal the number of output partitions.</span></span> <span data-ttu-id="38774-149">L'output dell'archiviazione BLOB attualmente non supporta le partizioni,</span><span class="sxs-lookup"><span data-stu-id="38774-149">Blob storage output doesn't currently support partitions.</span></span> <span data-ttu-id="38774-150">ma questo non è un problema perché lo schema di partizionamento viene ereditato dalla query upstream.</span><span class="sxs-lookup"><span data-stu-id="38774-150">But that's okay, because it inherits the partitioning scheme of the upstream query.</span></span> <span data-ttu-id="38774-151">Ecco alcuni esempi di valori di partizioni che consentono un processo perfettamente parallelo:</span><span class="sxs-lookup"><span data-stu-id="38774-151">Here are examples of partition values that allow a fully parallel job:</span></span>  

   * <span data-ttu-id="38774-152">8 partizioni di input di hub eventi e 8 partizioni di output di hub eventi</span><span class="sxs-lookup"><span data-stu-id="38774-152">8 event hub input partitions and 8 event hub output partitions</span></span>
   * <span data-ttu-id="38774-153">8 partizioni di input di hub eventi e output di archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="38774-153">8 event hub input partitions and blob storage output</span></span>  
   * <span data-ttu-id="38774-154">8 partizioni di input di archiviazione BLOB e output di archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="38774-154">8 blob storage input partitions and blob storage output</span></span>  
   * <span data-ttu-id="38774-155">8 partizioni di input di archiviazione BLOB e 8 partizioni di output di hub eventi</span><span class="sxs-lookup"><span data-stu-id="38774-155">8 blob storage input partitions and 8 event hub output partitions</span></span>  

<span data-ttu-id="38774-156">Le sezioni seguenti illustrano alcuni esempi di scenari perfettamente paralleli.</span><span class="sxs-lookup"><span data-stu-id="38774-156">The following sections discuss some example scenarios that are embarrassingly parallel.</span></span>

### <a name="simple-query"></a><span data-ttu-id="38774-157">Query semplice</span><span class="sxs-lookup"><span data-stu-id="38774-157">Simple query</span></span>

* <span data-ttu-id="38774-158">Input: hub eventi con 8 partizioni</span><span class="sxs-lookup"><span data-stu-id="38774-158">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="38774-159">Output: hub eventi con 8 partizioni</span><span class="sxs-lookup"><span data-stu-id="38774-159">Output: Event hub with 8 partitions</span></span>

<span data-ttu-id="38774-160">Query:</span><span class="sxs-lookup"><span data-stu-id="38774-160">Query:</span></span>

    SELECT TollBoothId
    FROM Input1 Partition By PartitionId
    WHERE TollBoothId > 100

<span data-ttu-id="38774-161">Questa query è un filtro semplice.</span><span class="sxs-lookup"><span data-stu-id="38774-161">This query is a simple filter.</span></span> <span data-ttu-id="38774-162">Non è pertanto necessario preoccuparsi del partizionamento dell'input inviato all'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="38774-162">Therefore, we don't need to worry about partitioning the input that is being sent to the event hub.</span></span> <span data-ttu-id="38774-163">Si noti che la query include la clausola **Partition By PartitionId** e quindi il requisito 2 illustrato in precedenza è pienamente soddisfatto.</span><span class="sxs-lookup"><span data-stu-id="38774-163">Notice that the query includes **Partition By PartitionId**, so it fulfills requirement #2 from earlier.</span></span> <span data-ttu-id="38774-164">A livello di output, è necessario configurare l'output dell'hub eventi nel processo in modo che la chiave di partizione sia impostata su **PartitionId**.</span><span class="sxs-lookup"><span data-stu-id="38774-164">For the output, we need to configure the event hub output in the job to have the parition key set to **PartitionId**.</span></span> <span data-ttu-id="38774-165">È infine necessario verificare che il numero delle partizioni di input sia uguale a quello delle partizioni di output.</span><span class="sxs-lookup"><span data-stu-id="38774-165">One last check is to make sure that the number of input partitions is equal to the number of output partitions.</span></span>

### <a name="query-with-a-grouping-key"></a><span data-ttu-id="38774-166">Query con chiave di raggruppamento</span><span class="sxs-lookup"><span data-stu-id="38774-166">Query with a grouping key</span></span>

* <span data-ttu-id="38774-167">Input: hub eventi con 8 partizioni</span><span class="sxs-lookup"><span data-stu-id="38774-167">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="38774-168">Output: archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="38774-168">Output: Blob storage</span></span>

<span data-ttu-id="38774-169">Query:</span><span class="sxs-lookup"><span data-stu-id="38774-169">Query:</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="38774-170">Questa query include una chiave di raggruppamento.</span><span class="sxs-lookup"><span data-stu-id="38774-170">This query has a grouping key.</span></span> <span data-ttu-id="38774-171">La stessa chiave deve pertanto essere elaborata dalla stessa istanza di query. Ciò significa che gli eventi devono essere inviati all'hub eventi in modo partizionato.</span><span class="sxs-lookup"><span data-stu-id="38774-171">Therefore, the same key needs to be processed by the same query instance, which means that events must be sent to the event hub in a partitioned manner.</span></span> <span data-ttu-id="38774-172">Ma quale chiave è necessario usare?</span><span class="sxs-lookup"><span data-stu-id="38774-172">But which key should be used?</span></span> <span data-ttu-id="38774-173">**PartitionId** corrisponde a un concetto della logica di processo.</span><span class="sxs-lookup"><span data-stu-id="38774-173">**PartitionId** is a job-logic concept.</span></span> <span data-ttu-id="38774-174">La chiave effettiva di cui occuparsi è **TollBoothId** e quindi il valore di **PartitionKey** dei dati di evento deve essere **TollBoothId**.</span><span class="sxs-lookup"><span data-stu-id="38774-174">The key we actually care about is **TollBoothId**, so the **PartitionKey** value of the event data should be **TollBoothId**.</span></span> <span data-ttu-id="38774-175">A questo scopo è necessario impostare **Partition By** su **PartitionId** nella query.</span><span class="sxs-lookup"><span data-stu-id="38774-175">We do this in the query by setting **Partition By** to **PartitionId**.</span></span> <span data-ttu-id="38774-176">Poiché l'output è costituito dall'archiviazione BLOB, non occorre preoccuparsi di configurare un valore di chiave di partizione, come definito dal requisito 4.</span><span class="sxs-lookup"><span data-stu-id="38774-176">Since the output is blob storage, we don't need to worry about configuring a partition key value, as per requirement #4.</span></span>

### <a name="multi-step-query-with-a-grouping-key"></a><span data-ttu-id="38774-177">Query a più passaggi con chiave di raggruppamento</span><span class="sxs-lookup"><span data-stu-id="38774-177">Multi-step query with a grouping key</span></span>
* <span data-ttu-id="38774-178">Input: hub eventi con 8 partizioni</span><span class="sxs-lookup"><span data-stu-id="38774-178">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="38774-179">Output: istanza di hub eventi con 8 partizioni</span><span class="sxs-lookup"><span data-stu-id="38774-179">Output: Event hub instance with 8 partitions</span></span>

<span data-ttu-id="38774-180">Query:</span><span class="sxs-lookup"><span data-stu-id="38774-180">Query:</span></span>

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="38774-181">Questa query include una chiave di raggruppamento ed è quindi necessario che la stessa chiave venga elaborata dalla stessa istanza di query.</span><span class="sxs-lookup"><span data-stu-id="38774-181">This query has a grouping key, so the same key needs to be processed by the same query instance.</span></span> <span data-ttu-id="38774-182">È possibile adottare la stessa strategia usata nell'esempio precedente.</span><span class="sxs-lookup"><span data-stu-id="38774-182">We can use the same strategy as in the previous example.</span></span> <span data-ttu-id="38774-183">In questo caso, la query è articolata in più passaggi.</span><span class="sxs-lookup"><span data-stu-id="38774-183">In this case, the query has multiple steps.</span></span> <span data-ttu-id="38774-184">Per ogni passaggio è presente la clausola **Partition By PartitionID**?</span><span class="sxs-lookup"><span data-stu-id="38774-184">Does each step have **Partition By PartitionId**?</span></span> <span data-ttu-id="38774-185">Sì, quindi la query soddisfa il requisito 3.</span><span class="sxs-lookup"><span data-stu-id="38774-185">Yes, so the query fulfills requirement #3.</span></span> <span data-ttu-id="38774-186">A livello di output, è necessario impostare la chiave di partizione su **PartitionId**, come descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="38774-186">For the output, we need to set the partition key to **PartitionId**, as discussed earlier.</span></span> <span data-ttu-id="38774-187">Si può anche osservare che il numero di partizioni dell'output è identico a quello dell'input.</span><span class="sxs-lookup"><span data-stu-id="38774-187">We can also see that it has the same number of partitions as the input.</span></span>

## <a name="example-scenarios-that-are-not-embarrassingly-parallel"></a><span data-ttu-id="38774-188">Esempi di scenari *non* perfettamente paralleli</span><span class="sxs-lookup"><span data-stu-id="38774-188">Example scenarios that are *not* embarrassingly parallel</span></span>

<span data-ttu-id="38774-189">Nella sezione precedente sono stati presentati alcuni scenari perfettamente paralleli.</span><span class="sxs-lookup"><span data-stu-id="38774-189">In the previous section, we showed some embarrassingly parallel scenarios.</span></span> <span data-ttu-id="38774-190">In questa sezione si illustreranno scenari che non soddisfano tutti i requisiti di parallelismo perfetto.</span><span class="sxs-lookup"><span data-stu-id="38774-190">In this section, we discuss scenarios that don't meet all the requirements to be embarrassingly parallel.</span></span> 

### <a name="mismatched-partition-count"></a><span data-ttu-id="38774-191">Numero di partizioni non corrispondente</span><span class="sxs-lookup"><span data-stu-id="38774-191">Mismatched partition count</span></span>
* <span data-ttu-id="38774-192">Input: hub eventi con 8 partizioni</span><span class="sxs-lookup"><span data-stu-id="38774-192">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="38774-193">Output: hub eventi con 32 partizioni</span><span class="sxs-lookup"><span data-stu-id="38774-193">Output: Event hub with 32 partitions</span></span>

<span data-ttu-id="38774-194">In questo caso, la query non è rilevante.</span><span class="sxs-lookup"><span data-stu-id="38774-194">In this case, it doesn't matter what the query is.</span></span> <span data-ttu-id="38774-195">Se il numero delle partizioni di input non corrisponde a quello delle partizioni di output, la topologia non è perfettamente parallela.</span><span class="sxs-lookup"><span data-stu-id="38774-195">If the input partition count doesn't match the output partition count, the topology isn't embarrassingly parallel.</span></span>

### <a name="not-using-event-hubs-or-blob-storage-as-output"></a><span data-ttu-id="38774-196">Uso di un output diverso da hub eventi o archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="38774-196">Not using event hubs or blob storage as output</span></span>
* <span data-ttu-id="38774-197">Input: hub eventi con 8 partizioni</span><span class="sxs-lookup"><span data-stu-id="38774-197">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="38774-198">Output: Power BI</span><span class="sxs-lookup"><span data-stu-id="38774-198">Output: PowerBI</span></span>

<span data-ttu-id="38774-199">L'output Power BI attualmente non supporta il partizionamento.</span><span class="sxs-lookup"><span data-stu-id="38774-199">PowerBI output doesn't currently support partitioning.</span></span> <span data-ttu-id="38774-200">Pertanto, questo scenario non è perfettamente parallelo.</span><span class="sxs-lookup"><span data-stu-id="38774-200">Therefore, this scenario is not embarrassingly parallel.</span></span>

### <a name="multi-step-query-with-different-partition-by-values"></a><span data-ttu-id="38774-201">Query a più passaggi con valori diversi per Partition By</span><span class="sxs-lookup"><span data-stu-id="38774-201">Multi-step query with different Partition By values</span></span>
* <span data-ttu-id="38774-202">Input: hub eventi con 8 partizioni</span><span class="sxs-lookup"><span data-stu-id="38774-202">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="38774-203">Output: hub eventi con 8 partizioni</span><span class="sxs-lookup"><span data-stu-id="38774-203">Output: Event hub with 8 partitions</span></span>

<span data-ttu-id="38774-204">Query:</span><span class="sxs-lookup"><span data-stu-id="38774-204">Query:</span></span>

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By TollBoothId
    GROUP BY TumblingWindow(minute, 3), TollBoothId

<span data-ttu-id="38774-205">Come è possibile osservare, il secondo passaggio usa **TollBoothId** come chiave di partizionamento, a differenza del primo passaggio.</span><span class="sxs-lookup"><span data-stu-id="38774-205">As you can see, the second step uses **TollBoothId** as the partitioning key.</span></span> <span data-ttu-id="38774-206">È quindi necessario eseguire una riproduzione in ordine casuale.</span><span class="sxs-lookup"><span data-stu-id="38774-206">This step is not the same as the first step, and it therefore requires us to do a shuffle.</span></span> 

<span data-ttu-id="38774-207">Gli esempi precedenti illustrano alcuni processi di Analisi di flusso che sono o non sono conformi a una topologia perfettamente parallela.</span><span class="sxs-lookup"><span data-stu-id="38774-207">The preceding examples show some Stream Analytics jobs that conform to (or don't) an embarrassingly parallel topology.</span></span> <span data-ttu-id="38774-208">Se sono conformi, possono raggiungere il livello massimo di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="38774-208">If they do conform, they have the potential for maximum scale.</span></span> <span data-ttu-id="38774-209">Per i processi che non rientrano in nessuno di questi profili, in futuro saranno disponibili aggiornamenti con le linee guida per il ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="38774-209">For jobs that don't fit one of these profiles, scaling guidance will be available in future updates.</span></span> <span data-ttu-id="38774-210">Per il momento, seguire le indicazioni generali riportate nelle sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="38774-210">For now, use the general guidance in the following sections.</span></span>

## <a name="calculate-the-maximum-streaming-units-of-a-job"></a><span data-ttu-id="38774-211">Calcolare il numero massimo di unità di streaming di un processo</span><span class="sxs-lookup"><span data-stu-id="38774-211">Calculate the maximum streaming units of a job</span></span>
<span data-ttu-id="38774-212">Il numero totale di unità di streaming che possono essere usate da un processo di Analisi dei flussi dipende dal numero di passaggi nella query definita per il processo e dal numero di partizioni per ogni passaggio.</span><span class="sxs-lookup"><span data-stu-id="38774-212">The total number of streaming units that can be used by a Stream Analytics job depends on the number of steps in the query defined for the job and the number of partitions for each step.</span></span>

### <a name="steps-in-a-query"></a><span data-ttu-id="38774-213">Passaggi in una query</span><span class="sxs-lookup"><span data-stu-id="38774-213">Steps in a query</span></span>
<span data-ttu-id="38774-214">Una query può includere uno o più passaggi.</span><span class="sxs-lookup"><span data-stu-id="38774-214">A query can have one or many steps.</span></span> <span data-ttu-id="38774-215">Ogni passaggio è una sottoquery definita mediante la parola chiave **WITH**.</span><span class="sxs-lookup"><span data-stu-id="38774-215">Each step is a subquery defined by the **WITH** keyword.</span></span> <span data-ttu-id="38774-216">Anche la query esterna alla parola chiave **WITH** (una sola query) viene contata come passaggio. Ad esempio, l'istruzione **SELECT** nella query seguente:</span><span class="sxs-lookup"><span data-stu-id="38774-216">The query that is outside the **WITH** keyword (one query only) is also counted as a step, such as the **SELECT** statement in the following query:</span></span>

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute,3), TollBoothId

<span data-ttu-id="38774-217">Questa query include due passaggi.</span><span class="sxs-lookup"><span data-stu-id="38774-217">This query has two steps.</span></span>

> [!NOTE]
> <span data-ttu-id="38774-218">Questa query viene illustrata in dettaglio più avanti nell'articolo.</span><span class="sxs-lookup"><span data-stu-id="38774-218">This query is discussed in more detail later in the article.</span></span>
>  

### <a name="partition-a-step"></a><span data-ttu-id="38774-219">Partizionamento di un passaggio</span><span class="sxs-lookup"><span data-stu-id="38774-219">Partition a step</span></span>
<span data-ttu-id="38774-220">Il partizionamento di un passaggio richiede le condizioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="38774-220">Partitioning a step requires the following conditions:</span></span>

* <span data-ttu-id="38774-221">L'origine di input deve essere partizionata.</span><span class="sxs-lookup"><span data-stu-id="38774-221">The input source must be partitioned.</span></span> 
* <span data-ttu-id="38774-222">L'istruzione **SELECT** della query deve leggere da un'origine di input partizionata.</span><span class="sxs-lookup"><span data-stu-id="38774-222">The **SELECT** statement of the query must read from a partitioned input source.</span></span>
* <span data-ttu-id="38774-223">La query all'interno del passaggio deve includere la parola chiave **Partition By**.</span><span class="sxs-lookup"><span data-stu-id="38774-223">The query within the step must have the **Partition By** keyword.</span></span>

<span data-ttu-id="38774-224">Quando una query è partizionata, gli eventi di input vengono elaborati e aggregati in gruppi separati di partizioni e per ogni gruppo vengono generati eventi di output.</span><span class="sxs-lookup"><span data-stu-id="38774-224">When a query is partitioned, the input events are processed and aggregated in separate partition groups, and outputs events are generated for each of the groups.</span></span> <span data-ttu-id="38774-225">Se si vuole un aggregato combinato, è necessario creare un secondo passaggio non partizionato per l'aggregazione.</span><span class="sxs-lookup"><span data-stu-id="38774-225">If you want a combined aggregate, you must create a second non-partitioned step to aggregate.</span></span>

### <a name="calculate-the-max-streaming-units-for-a-job"></a><span data-ttu-id="38774-226">Calcolare il numero massimo di unità di streaming per un processo</span><span class="sxs-lookup"><span data-stu-id="38774-226">Calculate the max streaming units for a job</span></span>
<span data-ttu-id="38774-227">Per un processo di Analisi di flusso, l'insieme di tutti i passaggi non partizionati può raggiungere un massimo di sei unità di streaming.</span><span class="sxs-lookup"><span data-stu-id="38774-227">All non-partitioned steps together can scale up to six streaming units (SUs) for a Stream Analytics job.</span></span> <span data-ttu-id="38774-228">Per aggiungere altre unità, è necessario partizionare un passaggio.</span><span class="sxs-lookup"><span data-stu-id="38774-228">To add SUs, a step must be partitioned.</span></span> <span data-ttu-id="38774-229">Ogni partizione può includere sei unità di streaming.</span><span class="sxs-lookup"><span data-stu-id="38774-229">Each partition can have six SUs.</span></span>

<table border="1">
<tr><th><span data-ttu-id="38774-230">Query</span><span class="sxs-lookup"><span data-stu-id="38774-230">Query</span></span></th><th><span data-ttu-id="38774-231">Numero massimo di unità di streaming per il processo</span><span class="sxs-lookup"><span data-stu-id="38774-231">Max SUs for the job</span></span></th></td>

<tr><td>
<ul>
<li><span data-ttu-id="38774-232">La query contiene un unico passaggio.</span><span class="sxs-lookup"><span data-stu-id="38774-232">The query contains one step.</span></span></li>
<li><span data-ttu-id="38774-233">Il passaggio non è partizionato.</span><span class="sxs-lookup"><span data-stu-id="38774-233">The step is not partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="38774-234">6</span><span class="sxs-lookup"><span data-stu-id="38774-234">6</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="38774-235">Il flusso di dati di input è suddiviso in 3 partizioni.</span><span class="sxs-lookup"><span data-stu-id="38774-235">The input data stream is partitioned by 3.</span></span></li>
<li><span data-ttu-id="38774-236">La query contiene un unico passaggio.</span><span class="sxs-lookup"><span data-stu-id="38774-236">The query contains one step.</span></span></li>
<li><span data-ttu-id="38774-237">Il passaggio è partizionato.</span><span class="sxs-lookup"><span data-stu-id="38774-237">The step is partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="38774-238">18</span><span class="sxs-lookup"><span data-stu-id="38774-238">18</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="38774-239">La query contiene due passaggi.</span><span class="sxs-lookup"><span data-stu-id="38774-239">The query contains two steps.</span></span></li>
<li><span data-ttu-id="38774-240">Nessuno dei passaggi è partizionato.</span><span class="sxs-lookup"><span data-stu-id="38774-240">Neither of the steps is partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="38774-241">6</span><span class="sxs-lookup"><span data-stu-id="38774-241">6</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="38774-242">Il flusso di dati di input è suddiviso in 3 partizioni.</span><span class="sxs-lookup"><span data-stu-id="38774-242">The input data stream is partitioned by 3.</span></span></li>
<li><span data-ttu-id="38774-243">La query contiene due passaggi.</span><span class="sxs-lookup"><span data-stu-id="38774-243">The query contains two steps.</span></span> <span data-ttu-id="38774-244">Il passaggio di input viene partizionato, al contrario del secondo passaggio.</span><span class="sxs-lookup"><span data-stu-id="38774-244">The input step is partitioned and the second step is not.</span></span></li>
<li><span data-ttu-id="38774-245">L'istruzione <strong>SELECT</strong> legge dall'input partizionato.</span><span class="sxs-lookup"><span data-stu-id="38774-245">The <strong>SELECT</strong> statement reads from the partitioned input.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="38774-246">24 (18 per i passaggi partizionati + 6 per i passaggi non partizionati)</span><span class="sxs-lookup"><span data-stu-id="38774-246">24 (18 for partitioned steps + 6 for non-partitioned steps)</span></span></td></tr>
</table>

### <a name="examples-of-scaling"></a><span data-ttu-id="38774-247">Esempi di ridimensionamento</span><span class="sxs-lookup"><span data-stu-id="38774-247">Examples of scaling</span></span>

<span data-ttu-id="38774-248">La query seguente calcola il numero di automobili che passano per una stazione di pedaggio con tre caselli in un intervallo di tre minuti.</span><span class="sxs-lookup"><span data-stu-id="38774-248">The following query calculates the number of cars within a three-minute window going through a toll station that has three tollbooths.</span></span> <span data-ttu-id="38774-249">Il numero di unità di streaming di questa query può essere aumentato fino a sei.</span><span class="sxs-lookup"><span data-stu-id="38774-249">This query can be scaled up to six SUs.</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="38774-250">Per usare più unità di streaming per la query, è necessario che il flusso di dati di input e la query siano entrambi partizionati.</span><span class="sxs-lookup"><span data-stu-id="38774-250">To use more SUs for the query, both the input data stream and the query must be partitioned.</span></span> <span data-ttu-id="38774-251">Se il partizionamento del flusso di dati è impostato su 3, la query modificata seguente può essere ridimensionata fino a un massimo di 18 unità di streaming:</span><span class="sxs-lookup"><span data-stu-id="38774-251">Since the data stream partition is set to 3, the following modified query can be scaled up to 18 SUs:</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="38774-252">Quando una query è partizionata, gli eventi di input vengono elaborati e aggregati in gruppi di partizioni separati</span><span class="sxs-lookup"><span data-stu-id="38774-252">When a query is partitioned, the input events are processed and aggregated in separate partition groups.</span></span> <span data-ttu-id="38774-253">e vengono anche generati eventi di output per ognuno dei gruppi.</span><span class="sxs-lookup"><span data-stu-id="38774-253">Output events are also generated for each of the groups.</span></span> <span data-ttu-id="38774-254">Quando il campo **GROUP BY** non corrisponde alla chiave di partizione nel flusso di dati di input, il partizionamento può causare risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="38774-254">Partitioning can cause some unexpected results when the **GROUP BY** field is not the partition key in the input data stream.</span></span> <span data-ttu-id="38774-255">Ad esempio, il campo **TollBoothId** nella query precedente non corrisponde alla chiave di partizione **Input1**.</span><span class="sxs-lookup"><span data-stu-id="38774-255">For example, the **TollBoothId** field in the previous query is not the partition key of **Input1**.</span></span> <span data-ttu-id="38774-256">I dati provenienti dal casello 1 possono pertanto essere distribuiti in più partizioni.</span><span class="sxs-lookup"><span data-stu-id="38774-256">The result is that the data from TollBooth #1 can be spread in multiple partitions.</span></span>

<span data-ttu-id="38774-257">Le singole partizioni di **Input1** verranno elaborate separatamente da Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="38774-257">Each of the **Input1** partitions will be processed separately by Stream Analytics.</span></span> <span data-ttu-id="38774-258">Verranno pertanto creati più record del conteggio relativo al passaggio di automobili dallo stesso casello nella stessa finestra a cascata.</span><span class="sxs-lookup"><span data-stu-id="38774-258">As a result, multiple records of the car count for the same tollbooth in the same Tumbling window will be created.</span></span> <span data-ttu-id="38774-259">Se la chiave di partizione di input non può essere modificata, è possibile risolvere questo problema aggiungendo un altro passaggio non di partizione, come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="38774-259">If the input partition key can't be changed, this problem can be fixed by adding a non-partition step, as in the following example:</span></span>

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute, 3), TollBoothId

<span data-ttu-id="38774-260">Per questa query è possibile aumentare il numero di unità di streaming fino a 24.</span><span class="sxs-lookup"><span data-stu-id="38774-260">This query can be scaled to 24 SUs.</span></span>

> [!NOTE]
> <span data-ttu-id="38774-261">Se si uniscono due flussi, verificare che tali flussi siano partizionati in base alla chiave di partizione della colonna usata per le unioni.</span><span class="sxs-lookup"><span data-stu-id="38774-261">If you are joining two streams, make sure that the streams are partitioned by the partition key of the column that you use to create the joins.</span></span> <span data-ttu-id="38774-262">Controllare inoltre che in entrambi i flussi sia presente lo stesso numero di partizioni.</span><span class="sxs-lookup"><span data-stu-id="38774-262">Also make sure that you have the same number of partitions in both streams.</span></span>
> 
> 

## <a name="configure-stream-analytics-streaming-units"></a><span data-ttu-id="38774-263">Configurare le unità di streaming di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="38774-263">Configure Stream Analytics streaming units</span></span>

1. <span data-ttu-id="38774-264">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="38774-264">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="38774-265">Nell'elenco delle risorse trovare il processo di Analisi di flusso da ridimensionare e aprirlo.</span><span class="sxs-lookup"><span data-stu-id="38774-265">In the list of resources, find the Stream Analytics job that you want to scale and then open it.</span></span>
3. <span data-ttu-id="38774-266">Nel pannello del processo, in **Configura**, fare clic su **Scale** (Ridimensiona).</span><span class="sxs-lookup"><span data-stu-id="38774-266">In the job blade, under **Configure**, click **Scale**.</span></span>

    ![Configurazione del processo di Analisi di flusso nel portale di Azure][img.stream.analytics.preview.portal.settings.scale]

4. <span data-ttu-id="38774-268">Usare il dispositivo di scorrimento per impostare le unità di streaming per il processo.</span><span class="sxs-lookup"><span data-stu-id="38774-268">Use the slider to set the SUs for the job.</span></span> <span data-ttu-id="38774-269">Si noti che è possibile definire solo impostazioni specifiche delle unità di streaming.</span><span class="sxs-lookup"><span data-stu-id="38774-269">Notice that you are limited to specific SU settings.</span></span>


## <a name="monitor-job-performance"></a><span data-ttu-id="38774-270">Monitorare le prestazioni del processo</span><span class="sxs-lookup"><span data-stu-id="38774-270">Monitor job performance</span></span>
<span data-ttu-id="38774-271">Nel portale di Azure è possibile rilevare la velocità effettiva di un processo:</span><span class="sxs-lookup"><span data-stu-id="38774-271">Using the Azure portal, you can track the throughput of a job:</span></span>

![Processi di monitoraggio di Analisi dei flussi di Azure][img.stream.analytics.monitor.job]

<span data-ttu-id="38774-273">Calcolare la velocità effettiva prevista del carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="38774-273">Calculate the expected throughput of the workload.</span></span> <span data-ttu-id="38774-274">Se la velocità effettiva è inferiore al previsto, ottimizzare la partizione di input e la query, quindi aggiungere unità di streaming al processo.</span><span class="sxs-lookup"><span data-stu-id="38774-274">If the throughput is less than expected, tune the input partition, tune the query, and add SUs to your job.</span></span>


## <a name="visualize-stream-analytics-throughput-at-scale-the-raspberry-pi-scenario"></a><span data-ttu-id="38774-275">Visualizzare la velocità effettiva di Analisi di flusso su larga scala: scenario Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="38774-275">Visualize Stream Analytics throughput at scale: the Raspberry Pi scenario</span></span>
<span data-ttu-id="38774-276">Per illustrare la scalabilità dei processi di Analisi di flusso, è stato eseguito un esperimento in base all'input di un dispositivo Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="38774-276">To help you understand how Stream Analytics jobs scale, we performed an experiment based on input from a Raspberry Pi device.</span></span> <span data-ttu-id="38774-277">L'esperimento ha consentito di osservare l'effetto prodotto da più unità di streaming e partizioni sulla velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="38774-277">This experiment let us see the effect on throughput of multiple streaming units and partitions.</span></span>

<span data-ttu-id="38774-278">In questo scenario il dispositivo invia i dati dei sensori (client) a un hub eventi.</span><span class="sxs-lookup"><span data-stu-id="38774-278">In this scenario, the device sends sensor data (clients) to an event hub.</span></span> <span data-ttu-id="38774-279">Analisi di flusso elabora i dati e invia come output un avviso o dati statistici a un altro hub eventi.</span><span class="sxs-lookup"><span data-stu-id="38774-279">Streaming Analytics processes the data and sends an alert or statistics as an output to another event hub.</span></span> 

<span data-ttu-id="38774-280">Il client invia i dati dei sensori in formato JSON</span><span class="sxs-lookup"><span data-stu-id="38774-280">The client sends sensor data in JSON format.</span></span> <span data-ttu-id="38774-281">e anche l'output dei dati è in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="38774-281">The data output is also in JSON format.</span></span> <span data-ttu-id="38774-282">L'aspetto dei dati sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="38774-282">The data looks like this:</span></span>

    {"devicetime":"2014-12-11T02:24:56.8850110Z","hmdt":42.7,"temp":72.6,"prss":98187.75,"lght":0.38,"dspl":"R-PI Olivier's Office"}

<span data-ttu-id="38774-283">La query seguente consente di inviare un avviso quando una luce si spegne:</span><span class="sxs-lookup"><span data-stu-id="38774-283">The following query is used to send an alert when a light is switched off:</span></span>

    SELECT AVG(lght),
     "LightOff" as AlertText
    FROM input TIMESTAMP
    BY devicetime
     WHERE
        lght< 0.05 GROUP BY TumblingWindow(second, 1)

### <a name="measure-throughput"></a><span data-ttu-id="38774-284">Misurare la velocità effettiva</span><span class="sxs-lookup"><span data-stu-id="38774-284">Measure throughput</span></span>

<span data-ttu-id="38774-285">In questo contesto la velocità effettiva è la quantità di dati di input elaborata da Analisi di flusso in un determinato intervallo di tempo</span><span class="sxs-lookup"><span data-stu-id="38774-285">In this context, throughput is the amount of input data processed by Stream Analytics in a fixed amount of time.</span></span> <span data-ttu-id="38774-286">(10 minuti). Per ottenere la velocità effettiva di elaborazione ottimale per i dati di input, l'input del flusso dei dati e la query sono stati partizionati.</span><span class="sxs-lookup"><span data-stu-id="38774-286">(We measured for 10 minutes.) To achieve the best processing throughput for the input data, both the data stream input and the query were  partitioned.</span></span> <span data-ttu-id="38774-287">Nella query è stato incluso **COUNT()** per misurare il numero di eventi di input che sono stati elaborati.</span><span class="sxs-lookup"><span data-stu-id="38774-287">We included **COUNT()** in the query to measure how many input events were processed.</span></span> <span data-ttu-id="38774-288">Per essere certi che il processo non rimanesse semplicemente in attesa dell'arrivo di eventi di input, ogni partizione dell'hub eventi di input è stata precaricata con circa 300 MB di dati di input.</span><span class="sxs-lookup"><span data-stu-id="38774-288">To make sure the job was not simply waiting for input events to come, each partition of the input event hub was preloaded with about 300 MB of input data.</span></span>

<span data-ttu-id="38774-289">La tabella seguente mostra i risultati ottenuti aumentando il numero di unità di streaming e il numero di partizioni corrispondenti negli hub eventi.</span><span class="sxs-lookup"><span data-stu-id="38774-289">The following table shows the results we saw when we increased the number of streaming units and the corresponding partition counts in event hubs.</span></span>  

<table border="1">
<tr><th><span data-ttu-id="38774-290">Partizioni di input</span><span class="sxs-lookup"><span data-stu-id="38774-290">Input Partitions</span></span></th><th><span data-ttu-id="38774-291">Partizioni di output</span><span class="sxs-lookup"><span data-stu-id="38774-291">Output Partitions</span></span></th><th><span data-ttu-id="38774-292">Unità di streaming</span><span class="sxs-lookup"><span data-stu-id="38774-292">Streaming Units</span></span></th><th><span data-ttu-id="38774-293">Velocità effettiva sostenuta</span><span class="sxs-lookup"><span data-stu-id="38774-293">Sustained Throughput</span></span>
</th></td>

<tr><td><span data-ttu-id="38774-294">12</span><span class="sxs-lookup"><span data-stu-id="38774-294">12</span></span></td>
<td><span data-ttu-id="38774-295">12</span><span class="sxs-lookup"><span data-stu-id="38774-295">12</span></span></td>
<td><span data-ttu-id="38774-296">6</span><span class="sxs-lookup"><span data-stu-id="38774-296">6</span></span></td>
<td><span data-ttu-id="38774-297">4,06 MB/s</span><span class="sxs-lookup"><span data-stu-id="38774-297">4.06 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="38774-298">12</span><span class="sxs-lookup"><span data-stu-id="38774-298">12</span></span></td>
<td><span data-ttu-id="38774-299">12</span><span class="sxs-lookup"><span data-stu-id="38774-299">12</span></span></td>
<td><span data-ttu-id="38774-300">12</span><span class="sxs-lookup"><span data-stu-id="38774-300">12</span></span></td>
<td><span data-ttu-id="38774-301">8,06 MB/s</span><span class="sxs-lookup"><span data-stu-id="38774-301">8.06 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="38774-302">48</span><span class="sxs-lookup"><span data-stu-id="38774-302">48</span></span></td>
<td><span data-ttu-id="38774-303">48</span><span class="sxs-lookup"><span data-stu-id="38774-303">48</span></span></td>
<td><span data-ttu-id="38774-304">48</span><span class="sxs-lookup"><span data-stu-id="38774-304">48</span></span></td>
<td><span data-ttu-id="38774-305">38,32 MB/s</span><span class="sxs-lookup"><span data-stu-id="38774-305">38.32 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="38774-306">192</span><span class="sxs-lookup"><span data-stu-id="38774-306">192</span></span></td>
<td><span data-ttu-id="38774-307">192</span><span class="sxs-lookup"><span data-stu-id="38774-307">192</span></span></td>
<td><span data-ttu-id="38774-308">192</span><span class="sxs-lookup"><span data-stu-id="38774-308">192</span></span></td>
<td><span data-ttu-id="38774-309">172,67 MB/s</span><span class="sxs-lookup"><span data-stu-id="38774-309">172.67 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="38774-310">480</span><span class="sxs-lookup"><span data-stu-id="38774-310">480</span></span></td>
<td><span data-ttu-id="38774-311">480</span><span class="sxs-lookup"><span data-stu-id="38774-311">480</span></span></td>
<td><span data-ttu-id="38774-312">480</span><span class="sxs-lookup"><span data-stu-id="38774-312">480</span></span></td>
<td><span data-ttu-id="38774-313">454,27 MB/s</span><span class="sxs-lookup"><span data-stu-id="38774-313">454.27 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="38774-314">720</span><span class="sxs-lookup"><span data-stu-id="38774-314">720</span></span></td>
<td><span data-ttu-id="38774-315">720</span><span class="sxs-lookup"><span data-stu-id="38774-315">720</span></span></td>
<td><span data-ttu-id="38774-316">720</span><span class="sxs-lookup"><span data-stu-id="38774-316">720</span></span></td>
<td><span data-ttu-id="38774-317">609,69 MB/s</span><span class="sxs-lookup"><span data-stu-id="38774-317">609.69 MB/s</span></span></td>
</tr>
</table>

<span data-ttu-id="38774-318">Il grafico seguente illustra la relazione tra unità di streaming e velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="38774-318">And the following graph shows a visualization of the relationship between SUs and throughput.</span></span>

![img.stream.analytics.perfgraph][img.stream.analytics.perfgraph]

## <a name="get-help"></a><span data-ttu-id="38774-320">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="38774-320">Get help</span></span>
<span data-ttu-id="38774-321">Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="38774-321">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="38774-322">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="38774-322">Next steps</span></span>
* [<span data-ttu-id="38774-323">Introduzione ad Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="38774-323">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="38774-324">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="38774-324">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="38774-325">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="38774-325">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="38774-326">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="38774-326">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Image references-->

[img.stream.analytics.monitor.job]: ./media/stream-analytics-scale-jobs/StreamAnalytics.job.monitor-NewPortal.png
[img.stream.analytics.configure.scale]: ./media/stream-analytics-scale-jobs/StreamAnalytics.configure.scale.png
[img.stream.analytics.perfgraph]: ./media/stream-analytics-scale-jobs/perf.png
[img.stream.analytics.streaming.units.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsStreamingUnitsExample.jpg
[img.stream.analytics.preview.portal.settings.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsPreviewPortalJobSettings-NewPortal.png   

<!--Link references-->

[microsoft.support]: http://support.microsoft.com
[azure.management.portal]: http://manage.windowsazure.com
[azure.event.hubs.developer.guide]: http://msdn.microsoft.com/library/azure/dn789972.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

