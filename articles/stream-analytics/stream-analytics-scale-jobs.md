---
title: "velocità effettiva tooincrease i processi di flusso Analitica aaaScale | Documenti Microsoft"
description: "Informazioni su come i processi di flusso Analitica tooscale per la configurazione delle partizioni di input, l'ottimizzazione di definizione della query hello e impostazione processo unità di streaming."
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
ms.openlocfilehash: 4ba8f6b2f8bfebd52cfa07696b501b42cda21f75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-azure-stream-analytics-jobs-tooincrease-stream-data-processing-throughput"></a><span data-ttu-id="0a48c-104">Velocità effettiva di elaborazione dei dati di scala Analitica di flusso di Azure processi tooincrease flusso</span><span class="sxs-lookup"><span data-stu-id="0a48c-104">Scale Azure Stream Analytics jobs tooincrease stream data processing throughput</span></span>
<span data-ttu-id="0a48c-105">In questo articolo viene illustrato come eseguire una query tooincrease velocità effettiva per i processi di Streaming Analitica tootune Analitica un flusso.</span><span class="sxs-lookup"><span data-stu-id="0a48c-105">This article shows you how tootune a Stream Analytics query tooincrease throughput for Streaming Analytics jobs.</span></span> <span data-ttu-id="0a48c-106">Si apprenderà come tooscale Analitica di flusso dei processi tramite la configurazione di input di partizioni, definizione di query di ottimizzazione analitica hello e processo di calcolo e l'impostazione *unità di streaming* (SUs).</span><span class="sxs-lookup"><span data-stu-id="0a48c-106">You learn how tooscale Stream Analytics jobs by configuring input partitions, tuning hello analytics query definition, and calculating and setting job *streaming units* (SUs).</span></span> 

## <a name="what-are-hello-parts-of-a-stream-analytics-job"></a><span data-ttu-id="0a48c-107">Quali sono le parti di un processo di flusso Analitica hello?</span><span class="sxs-lookup"><span data-stu-id="0a48c-107">What are hello parts of a Stream Analytics job?</span></span>
<span data-ttu-id="0a48c-108">Una definizione del processo di Analisi di flusso include input, query e output.</span><span class="sxs-lookup"><span data-stu-id="0a48c-108">A Stream Analytics job definition includes inputs, a query, and output.</span></span> <span data-ttu-id="0a48c-109">Gli input sono in cui il processo di hello legge il flusso di dati hello da.</span><span class="sxs-lookup"><span data-stu-id="0a48c-109">Inputs are where hello job reads hello data stream from.</span></span> <span data-ttu-id="0a48c-110">query Hello è usato tootransform hello dati flusso di input e output di hello è quale processo hello invia i risultati del processo hello per.</span><span class="sxs-lookup"><span data-stu-id="0a48c-110">hello query is used tootransform hello data input stream, and hello output is where hello job sends hello job results to.</span></span>  

<span data-ttu-id="0a48c-111">Un processo richiede almeno un'origine di input per il flusso dei dati.</span><span class="sxs-lookup"><span data-stu-id="0a48c-111">A job requires at least one input source for data streaming.</span></span> <span data-ttu-id="0a48c-112">Hello origine di input flusso di dati può essere archiviati in un hub di eventi di Azure o nell'archiviazione blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="0a48c-112">hello data stream input source can be stored in an Azure event hub or in Azure blob storage.</span></span> <span data-ttu-id="0a48c-113">Per ulteriori informazioni, vedere [tooAzure introduzione Analitica flusso](stream-analytics-introduction.md) e [iniziare a usare Azure flusso Analitica](stream-analytics-real-time-fraud-detection.md).</span><span class="sxs-lookup"><span data-stu-id="0a48c-113">For more information, see [Introduction tooAzure Stream Analytics](stream-analytics-introduction.md) and [Get started using Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md).</span></span>

## <a name="partitions-in-event-hubs-and-azure-storage"></a><span data-ttu-id="0a48c-114">Partizioni negli hub eventi e nell'archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="0a48c-114">Partitions in event hubs and Azure storage</span></span>
<span data-ttu-id="0a48c-115">Ridimensionamento di un processo di flusso Analitica si avvale di partizioni hello input o output.</span><span class="sxs-lookup"><span data-stu-id="0a48c-115">Scaling a Stream Analytics job takes advantage of partitions in hello input or output.</span></span> <span data-ttu-id="0a48c-116">Il partizionamento consente di suddividere i dati in subset in base a una chiave di partizione.</span><span class="sxs-lookup"><span data-stu-id="0a48c-116">Partitioning lets you divide data into subsets based on a partition key.</span></span> <span data-ttu-id="0a48c-117">Un processo che utilizza dati hello (ad esempio, un processo di Streaming Analitica) può utilizzare e scrivere le varie partizioni in parallelo, con conseguente aumento della velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="0a48c-117">A process that consumes hello data (such as a Streaming Analytics job) can consume and write different partitions in parallel, which increases throughput.</span></span> <span data-ttu-id="0a48c-118">Quando si usa Analisi di flusso, è possibile sfruttare il partizionamento negli hub eventi e nell'archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="0a48c-118">When you work with Streaming Analytics, you can take advantage of partitioning in event hubs and in Blob storage.</span></span> 

<span data-ttu-id="0a48c-119">Per ulteriori informazioni sulle partizioni, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="0a48c-119">For more information about partitions, see hello following articles:</span></span>

* [<span data-ttu-id="0a48c-120">Panoramica delle funzionalità di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="0a48c-120">Event Hubs features overview</span></span>](../event-hubs/event-hubs-features.md#partitions)
* [<span data-ttu-id="0a48c-121">Partizionamento dei dati</span><span class="sxs-lookup"><span data-stu-id="0a48c-121">Data partitioning</span></span>](https://docs.microsoft.com/azure/architecture/best-practices/data-partitioning#partitioning-azure-blob-storage)


## <a name="streaming-units-sus"></a><span data-ttu-id="0a48c-122">Unità di streaming</span><span class="sxs-lookup"><span data-stu-id="0a48c-122">Streaming units (SUs)</span></span>
<span data-ttu-id="0a48c-123">Unità (SUs) rappresentano hello risorse di flusso e di elaborazione necessarie in ordine tooexecute un processo Analitica di flusso di Azure.</span><span class="sxs-lookup"><span data-stu-id="0a48c-123">Streaming units (SUs) represent hello resources and computing power that are required in order tooexecute an Azure Stream Analytics job.</span></span> <span data-ttu-id="0a48c-124">SUs forniscono un modo toodescribe hello relativo evento basata su una misura combinata di CPU, memoria, capacità di elaborazione, leggere e scrivere tariffe.</span><span class="sxs-lookup"><span data-stu-id="0a48c-124">SUs provide a way toodescribe hello relative event processing capacity based on a blended measure of CPU, memory, and read and write rates.</span></span> <span data-ttu-id="0a48c-125">Ogni SU corrisponde tooroughly 1 MB al secondo di velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="0a48c-125">Each SU corresponds tooroughly 1 MB/second of throughput.</span></span> 

<span data-ttu-id="0a48c-126">Scelta di SUs quanti sono necessari per un determinato processo dipende dalla configurazione della partizione per gli input hello hello e hello query definita per il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="0a48c-126">Choosing how many SUs are required for a particular job depends on hello partition configuration for hello inputs and on hello query defined for hello job.</span></span> <span data-ttu-id="0a48c-127">È possibile selezionare le quote tooyour in SUs per un processo.</span><span class="sxs-lookup"><span data-stu-id="0a48c-127">You can select up tooyour quota in SUs for a job.</span></span> <span data-ttu-id="0a48c-128">Per impostazione predefinita, ogni sottoscrizione di Azure prevede una quota di backup SUs too50 per tutti i processi di hello analitica in un'area specifica.</span><span class="sxs-lookup"><span data-stu-id="0a48c-128">By default, each Azure subscription has a quota of up too50 SUs for all hello analytics jobs in a specific region.</span></span> <span data-ttu-id="0a48c-129">tooincrease SUs per le sottoscrizioni oltre questa quota, contattare [supporto Microsoft](http://support.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="0a48c-129">tooincrease SUs for your subscriptions beyond this quota, contact [Microsoft Support](http://support.microsoft.com).</span></span> <span data-ttu-id="0a48c-130">I valori validi di unità di streaming per processo sono 1, 3, 6 e poi a salire, con incrementi di 6.</span><span class="sxs-lookup"><span data-stu-id="0a48c-130">Valid values for SUs per job are 1, 3, 6, and up in increments of 6.</span></span>

## <a name="embarrassingly-parallel-jobs"></a><span data-ttu-id="0a48c-131">Processi perfettamente paralleli</span><span class="sxs-lookup"><span data-stu-id="0a48c-131">Embarrassingly parallel jobs</span></span>
<span data-ttu-id="0a48c-132">Un *imbarazzantemente parallele* processo è uno scenario di hello più scalabile in Azure flusso Analitica è disponibile.</span><span class="sxs-lookup"><span data-stu-id="0a48c-132">An *embarrassingly parallel* job is hello most scalable scenario we have in Azure Stream Analytics.</span></span> <span data-ttu-id="0a48c-133">Si connette una partizione di istanza di input tooone hello della partizione di tooone hello query di output di hello.</span><span class="sxs-lookup"><span data-stu-id="0a48c-133">It connects one partition of hello input tooone instance of hello query tooone partition of hello output.</span></span> <span data-ttu-id="0a48c-134">Il parallelismo è hello seguenti requisiti:</span><span class="sxs-lookup"><span data-stu-id="0a48c-134">This parallelism has hello following requirements:</span></span>

1. <span data-ttu-id="0a48c-135">Se la logica di query dipende dalla stessa chiave in fase di elaborazione hello da hello stessa istanza di query, è necessario assicurarsi che gli eventi di hello vanno toohello stessa partizione dell'input.</span><span class="sxs-lookup"><span data-stu-id="0a48c-135">If your query logic depends on hello same key being processed by hello same query instance, you must make sure that hello events go toohello same partition of your input.</span></span> <span data-ttu-id="0a48c-136">Per gli hub di eventi, ciò significa che i dati di evento hello devono disporre di hello **PartitionKey** valore impostato.</span><span class="sxs-lookup"><span data-stu-id="0a48c-136">For event hubs, this means that hello event data must have hello **PartitionKey** value set.</span></span> <span data-ttu-id="0a48c-137">In alternativa, è possibile usare mittenti partizionati.</span><span class="sxs-lookup"><span data-stu-id="0a48c-137">Alternatively, you can use partitioned senders.</span></span> <span data-ttu-id="0a48c-138">Per l'archiviazione blob, ciò significa che gli eventi di hello vengono inviati toohello stessa cartella della partizione.</span><span class="sxs-lookup"><span data-stu-id="0a48c-138">For blob storage, this means that hello events are sent toohello same partition folder.</span></span> <span data-ttu-id="0a48c-139">Se la logica di query non richiede la stessa chiave toobe elaborati hello da hello stessa istanza di query, è possibile ignorare questo requisito.</span><span class="sxs-lookup"><span data-stu-id="0a48c-139">If your query logic does not require hello same key toobe processed by hello same query instance, you can ignore this requirement.</span></span> <span data-ttu-id="0a48c-140">Un esempio di questa logica è offerto da una query semplice select-project-filter.</span><span class="sxs-lookup"><span data-stu-id="0a48c-140">An example of this logic would be a simple select-project-filter query.</span></span>  

2. <span data-ttu-id="0a48c-141">Una volta dati hello sono disposto sul lato di input hello, è necessario assicurarsi che la query è partizionata.</span><span class="sxs-lookup"><span data-stu-id="0a48c-141">Once hello data is laid out on hello input side, you must make sure that your query is partitioned.</span></span> <span data-ttu-id="0a48c-142">Questa operazione richiede il toouse **Partition By** in tutte le fasi di hello.</span><span class="sxs-lookup"><span data-stu-id="0a48c-142">This requires you toouse **Partition By** in all hello steps.</span></span> <span data-ttu-id="0a48c-143">Sono consentiti più passaggi, ma essi devono essere partizionati da hello stessa chiave.</span><span class="sxs-lookup"><span data-stu-id="0a48c-143">Multiple steps are allowed, but they all must be partitioned by hello same key.</span></span> <span data-ttu-id="0a48c-144">Attualmente, hello chiave di partizionamento deve essere impostato troppo**PartitionId** affinché hello processo toobe completamente parallelo.</span><span class="sxs-lookup"><span data-stu-id="0a48c-144">Currently, hello partitioning key must be set too**PartitionId** in order for hello job toobe fully parallel.</span></span>  

3. <span data-ttu-id="0a48c-145">Solo gli hub eventi e l'archiviazione BLOB supportano attualmente l'output partizionato.</span><span class="sxs-lookup"><span data-stu-id="0a48c-145">Currently only event hubs and blob storage support partitioned output.</span></span> <span data-ttu-id="0a48c-146">Per l'output di hub eventi, è necessario configurare toobe chiave di partizione hello **PartitionId**.</span><span class="sxs-lookup"><span data-stu-id="0a48c-146">For event hub output, you must configure hello partition key toobe **PartitionId**.</span></span> <span data-ttu-id="0a48c-147">Per l'output di archiviazione blob, non è necessario toodo nulla.</span><span class="sxs-lookup"><span data-stu-id="0a48c-147">For blob storage output, you don't have toodo anything.</span></span>  

4. <span data-ttu-id="0a48c-148">numero di Hello di partizioni di input deve essere uguale hello numero di partizioni di output.</span><span class="sxs-lookup"><span data-stu-id="0a48c-148">hello number of input partitions must equal hello number of output partitions.</span></span> <span data-ttu-id="0a48c-149">L'output dell'archiviazione BLOB attualmente non supporta le partizioni,</span><span class="sxs-lookup"><span data-stu-id="0a48c-149">Blob storage output doesn't currently support partitions.</span></span> <span data-ttu-id="0a48c-150">Ma che non costituisce un problema, perché eredita hello schema della query a monte hello di partizionamento.</span><span class="sxs-lookup"><span data-stu-id="0a48c-150">But that's okay, because it inherits hello partitioning scheme of hello upstream query.</span></span> <span data-ttu-id="0a48c-151">Ecco alcuni esempi di valori di partizioni che consentono un processo perfettamente parallelo:</span><span class="sxs-lookup"><span data-stu-id="0a48c-151">Here are examples of partition values that allow a fully parallel job:</span></span>  

   * <span data-ttu-id="0a48c-152">8 partizioni di input di hub eventi e 8 partizioni di output di hub eventi</span><span class="sxs-lookup"><span data-stu-id="0a48c-152">8 event hub input partitions and 8 event hub output partitions</span></span>
   * <span data-ttu-id="0a48c-153">8 partizioni di input di hub eventi e output di archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="0a48c-153">8 event hub input partitions and blob storage output</span></span>  
   * <span data-ttu-id="0a48c-154">8 partizioni di input di archiviazione BLOB e output di archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="0a48c-154">8 blob storage input partitions and blob storage output</span></span>  
   * <span data-ttu-id="0a48c-155">8 partizioni di input di archiviazione BLOB e 8 partizioni di output di hub eventi</span><span class="sxs-lookup"><span data-stu-id="0a48c-155">8 blob storage input partitions and 8 event hub output partitions</span></span>  

<span data-ttu-id="0a48c-156">Hello nelle sezioni seguenti vengono illustrano alcuni scenari di esempio imbarazzantemente parallele.</span><span class="sxs-lookup"><span data-stu-id="0a48c-156">hello following sections discuss some example scenarios that are embarrassingly parallel.</span></span>

### <a name="simple-query"></a><span data-ttu-id="0a48c-157">Query semplice</span><span class="sxs-lookup"><span data-stu-id="0a48c-157">Simple query</span></span>

* <span data-ttu-id="0a48c-158">Input: hub eventi con 8 partizioni</span><span class="sxs-lookup"><span data-stu-id="0a48c-158">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="0a48c-159">Output: hub eventi con 8 partizioni</span><span class="sxs-lookup"><span data-stu-id="0a48c-159">Output: Event hub with 8 partitions</span></span>

<span data-ttu-id="0a48c-160">Query:</span><span class="sxs-lookup"><span data-stu-id="0a48c-160">Query:</span></span>

    SELECT TollBoothId
    FROM Input1 Partition By PartitionId
    WHERE TollBoothId > 100

<span data-ttu-id="0a48c-161">Questa query è un filtro semplice.</span><span class="sxs-lookup"><span data-stu-id="0a48c-161">This query is a simple filter.</span></span> <span data-ttu-id="0a48c-162">Pertanto, non è necessario tooworry sul partizionamento input hello inviato toohello hub di eventi.</span><span class="sxs-lookup"><span data-stu-id="0a48c-162">Therefore, we don't need tooworry about partitioning hello input that is being sent toohello event hub.</span></span> <span data-ttu-id="0a48c-163">Sono incluse query hello **partizione da PartitionId**, in modo che soddisfi i requisiti #2 precedenti.</span><span class="sxs-lookup"><span data-stu-id="0a48c-163">Notice that hello query includes **Partition By PartitionId**, so it fulfills requirement #2 from earlier.</span></span> <span data-ttu-id="0a48c-164">Per l'output di hello, dobbiamo output di hub di eventi tooconfigure hello in hello processo toohave hello partizione set di chiavi troppo**PartitionId**.</span><span class="sxs-lookup"><span data-stu-id="0a48c-164">For hello output, we need tooconfigure hello event hub output in hello job toohave hello parition key set too**PartitionId**.</span></span> <span data-ttu-id="0a48c-165">Ultimo uno controllo è toomake assicurarsi che il numero di hello delle partizioni di input sia uguale toohello numero di partizioni di output.</span><span class="sxs-lookup"><span data-stu-id="0a48c-165">One last check is toomake sure that hello number of input partitions is equal toohello number of output partitions.</span></span>

### <a name="query-with-a-grouping-key"></a><span data-ttu-id="0a48c-166">Query con chiave di raggruppamento</span><span class="sxs-lookup"><span data-stu-id="0a48c-166">Query with a grouping key</span></span>

* <span data-ttu-id="0a48c-167">Input: hub eventi con 8 partizioni</span><span class="sxs-lookup"><span data-stu-id="0a48c-167">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="0a48c-168">Output: archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="0a48c-168">Output: Blob storage</span></span>

<span data-ttu-id="0a48c-169">Query:</span><span class="sxs-lookup"><span data-stu-id="0a48c-169">Query:</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="0a48c-170">Questa query include una chiave di raggruppamento.</span><span class="sxs-lookup"><span data-stu-id="0a48c-170">This query has a grouping key.</span></span> <span data-ttu-id="0a48c-171">Pertanto, hello stesso toobe esigenze chiave elaborati dalla stessa query di istanza, il che significa che gli eventi devono essere inviati toohello hub di eventi in modo partizionato hello.</span><span class="sxs-lookup"><span data-stu-id="0a48c-171">Therefore, hello same key needs toobe processed by hello same query instance, which means that events must be sent toohello event hub in a partitioned manner.</span></span> <span data-ttu-id="0a48c-172">Ma quale chiave è necessario usare?</span><span class="sxs-lookup"><span data-stu-id="0a48c-172">But which key should be used?</span></span> <span data-ttu-id="0a48c-173">**PartitionId** corrisponde a un concetto della logica di processo.</span><span class="sxs-lookup"><span data-stu-id="0a48c-173">**PartitionId** is a job-logic concept.</span></span> <span data-ttu-id="0a48c-174">chiave Hello interessante effettivamente **TollBoothId**, pertanto hello **PartitionKey** valore dei dati di evento hello deve essere **TollBoothId**.</span><span class="sxs-lookup"><span data-stu-id="0a48c-174">hello key we actually care about is **TollBoothId**, so hello **PartitionKey** value of hello event data should be **TollBoothId**.</span></span> <span data-ttu-id="0a48c-175">Prepariamo queste query hello impostando **Partition By** troppo**PartitionId**.</span><span class="sxs-lookup"><span data-stu-id="0a48c-175">We do this in hello query by setting **Partition By** too**PartitionId**.</span></span> <span data-ttu-id="0a48c-176">Poiché l'output di hello nell'archiviazione blob, non è necessario tooworry sulla configurazione di un valore di chiave di partizione, in base ai requisiti #4.</span><span class="sxs-lookup"><span data-stu-id="0a48c-176">Since hello output is blob storage, we don't need tooworry about configuring a partition key value, as per requirement #4.</span></span>

### <a name="multi-step-query-with-a-grouping-key"></a><span data-ttu-id="0a48c-177">Query a più passaggi con chiave di raggruppamento</span><span class="sxs-lookup"><span data-stu-id="0a48c-177">Multi-step query with a grouping key</span></span>
* <span data-ttu-id="0a48c-178">Input: hub eventi con 8 partizioni</span><span class="sxs-lookup"><span data-stu-id="0a48c-178">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="0a48c-179">Output: istanza di hub eventi con 8 partizioni</span><span class="sxs-lookup"><span data-stu-id="0a48c-179">Output: Event hub instance with 8 partitions</span></span>

<span data-ttu-id="0a48c-180">Query:</span><span class="sxs-lookup"><span data-stu-id="0a48c-180">Query:</span></span>

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="0a48c-181">La query contiene una chiave di raggruppamento, pertanto hello stesso toobe esigenze chiave elaborata hello stessa istanza di query.</span><span class="sxs-lookup"><span data-stu-id="0a48c-181">This query has a grouping key, so hello same key needs toobe processed by hello same query instance.</span></span> <span data-ttu-id="0a48c-182">È possibile utilizzare hello stessa strategia esempio hello precedente.</span><span class="sxs-lookup"><span data-stu-id="0a48c-182">We can use hello same strategy as in hello previous example.</span></span> <span data-ttu-id="0a48c-183">In questo caso, query hello prevede diversi passaggi.</span><span class="sxs-lookup"><span data-stu-id="0a48c-183">In this case, hello query has multiple steps.</span></span> <span data-ttu-id="0a48c-184">Per ogni passaggio è presente la clausola **Partition By PartitionID**?</span><span class="sxs-lookup"><span data-stu-id="0a48c-184">Does each step have **Partition By PartitionId**?</span></span> <span data-ttu-id="0a48c-185">Sì, in modo da query hello soddisfa requisito #3.</span><span class="sxs-lookup"><span data-stu-id="0a48c-185">Yes, so hello query fulfills requirement #3.</span></span> <span data-ttu-id="0a48c-186">Per l'output di hello, dobbiamo chiave di partizione hello tooset troppo**PartitionId**, come descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="0a48c-186">For hello output, we need tooset hello partition key too**PartitionId**, as discussed earlier.</span></span> <span data-ttu-id="0a48c-187">È inoltre possibile notare che hello stesso numero di partizioni come input hello.</span><span class="sxs-lookup"><span data-stu-id="0a48c-187">We can also see that it has hello same number of partitions as hello input.</span></span>

## <a name="example-scenarios-that-are-not-embarrassingly-parallel"></a><span data-ttu-id="0a48c-188">Esempi di scenari *non* perfettamente paralleli</span><span class="sxs-lookup"><span data-stu-id="0a48c-188">Example scenarios that are *not* embarrassingly parallel</span></span>

<span data-ttu-id="0a48c-189">Nella sezione precedente hello, abbiamo anche mostrato alcuni scenari imbarazzantemente parallele.</span><span class="sxs-lookup"><span data-stu-id="0a48c-189">In hello previous section, we showed some embarrassingly parallel scenarios.</span></span> <span data-ttu-id="0a48c-190">In questa sezione sono illustrati scenari che non soddisfano tutti hello requisiti toobe imbarazzantemente parallele.</span><span class="sxs-lookup"><span data-stu-id="0a48c-190">In this section, we discuss scenarios that don't meet all hello requirements toobe embarrassingly parallel.</span></span> 

### <a name="mismatched-partition-count"></a><span data-ttu-id="0a48c-191">Numero di partizioni non corrispondente</span><span class="sxs-lookup"><span data-stu-id="0a48c-191">Mismatched partition count</span></span>
* <span data-ttu-id="0a48c-192">Input: hub eventi con 8 partizioni</span><span class="sxs-lookup"><span data-stu-id="0a48c-192">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="0a48c-193">Output: hub eventi con 32 partizioni</span><span class="sxs-lookup"><span data-stu-id="0a48c-193">Output: Event hub with 32 partitions</span></span>

<span data-ttu-id="0a48c-194">In questo caso, non è importante è la query che hello.</span><span class="sxs-lookup"><span data-stu-id="0a48c-194">In this case, it doesn't matter what hello query is.</span></span> <span data-ttu-id="0a48c-195">Se il numero di partizioni di input di hello non corrisponde a numero di partizioni di output di hello, non è una topologia hello imbarazzantemente parallela.</span><span class="sxs-lookup"><span data-stu-id="0a48c-195">If hello input partition count doesn't match hello output partition count, hello topology isn't embarrassingly parallel.</span></span>

### <a name="not-using-event-hubs-or-blob-storage-as-output"></a><span data-ttu-id="0a48c-196">Uso di un output diverso da hub eventi o archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="0a48c-196">Not using event hubs or blob storage as output</span></span>
* <span data-ttu-id="0a48c-197">Input: hub eventi con 8 partizioni</span><span class="sxs-lookup"><span data-stu-id="0a48c-197">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="0a48c-198">Output: Power BI</span><span class="sxs-lookup"><span data-stu-id="0a48c-198">Output: PowerBI</span></span>

<span data-ttu-id="0a48c-199">L'output Power BI attualmente non supporta il partizionamento.</span><span class="sxs-lookup"><span data-stu-id="0a48c-199">PowerBI output doesn't currently support partitioning.</span></span> <span data-ttu-id="0a48c-200">Pertanto, questo scenario non è perfettamente parallelo.</span><span class="sxs-lookup"><span data-stu-id="0a48c-200">Therefore, this scenario is not embarrassingly parallel.</span></span>

### <a name="multi-step-query-with-different-partition-by-values"></a><span data-ttu-id="0a48c-201">Query a più passaggi con valori diversi per Partition By</span><span class="sxs-lookup"><span data-stu-id="0a48c-201">Multi-step query with different Partition By values</span></span>
* <span data-ttu-id="0a48c-202">Input: hub eventi con 8 partizioni</span><span class="sxs-lookup"><span data-stu-id="0a48c-202">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="0a48c-203">Output: hub eventi con 8 partizioni</span><span class="sxs-lookup"><span data-stu-id="0a48c-203">Output: Event hub with 8 partitions</span></span>

<span data-ttu-id="0a48c-204">Query:</span><span class="sxs-lookup"><span data-stu-id="0a48c-204">Query:</span></span>

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By TollBoothId
    GROUP BY TumblingWindow(minute, 3), TollBoothId

<span data-ttu-id="0a48c-205">Come si può notare, secondo passaggio hello Usa **TollBoothId** come chiave di partizionamento hello.</span><span class="sxs-lookup"><span data-stu-id="0a48c-205">As you can see, hello second step uses **TollBoothId** as hello partitioning key.</span></span> <span data-ttu-id="0a48c-206">Questo passaggio è non hello stesso come primo passaggio hello e pertanto richiede ci toodo una casuale.</span><span class="sxs-lookup"><span data-stu-id="0a48c-206">This step is not hello same as hello first step, and it therefore requires us toodo a shuffle.</span></span> 

<span data-ttu-id="0a48c-207">Hello esempi precedenti alcuni processi di flusso Analitica conformi troppo (o non) una topologia imbarazzantemente parallela.</span><span class="sxs-lookup"><span data-stu-id="0a48c-207">hello preceding examples show some Stream Analytics jobs that conform too(or don't) an embarrassingly parallel topology.</span></span> <span data-ttu-id="0a48c-208">Se devono essere conformi, hanno potenziale hello per la massima scalabilità.</span><span class="sxs-lookup"><span data-stu-id="0a48c-208">If they do conform, they have hello potential for maximum scale.</span></span> <span data-ttu-id="0a48c-209">Per i processi che non rientrano in nessuno di questi profili, in futuro saranno disponibili aggiornamenti con le linee guida per il ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="0a48c-209">For jobs that don't fit one of these profiles, scaling guidance will be available in future updates.</span></span> <span data-ttu-id="0a48c-210">Per il momento, utilizzare indicazioni generali hello hello le sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="0a48c-210">For now, use hello general guidance in hello following sections.</span></span>

## <a name="calculate-hello-maximum-streaming-units-of-a-job"></a><span data-ttu-id="0a48c-211">Unità di streaming massimo hello di un processo di calcolo</span><span class="sxs-lookup"><span data-stu-id="0a48c-211">Calculate hello maximum streaming units of a job</span></span>
<span data-ttu-id="0a48c-212">numero totale di Hello di unità di streaming che può essere utilizzato da un processo di flusso Analitica dipende dal numero di hello dei passaggi in query hello è definito per il processo di hello e numero di hello di partizioni per ogni passaggio.</span><span class="sxs-lookup"><span data-stu-id="0a48c-212">hello total number of streaming units that can be used by a Stream Analytics job depends on hello number of steps in hello query defined for hello job and hello number of partitions for each step.</span></span>

### <a name="steps-in-a-query"></a><span data-ttu-id="0a48c-213">Passaggi in una query</span><span class="sxs-lookup"><span data-stu-id="0a48c-213">Steps in a query</span></span>
<span data-ttu-id="0a48c-214">Una query può includere uno o più passaggi.</span><span class="sxs-lookup"><span data-stu-id="0a48c-214">A query can have one or many steps.</span></span> <span data-ttu-id="0a48c-215">Ogni passaggio è una sottoquery definita da hello **WITH** (parola chiave).</span><span class="sxs-lookup"><span data-stu-id="0a48c-215">Each step is a subquery defined by hello **WITH** keyword.</span></span> <span data-ttu-id="0a48c-216">query di Hello di fuori di hello **WITH** (parola chiave) (solo per una query) è anch'essa conteggiata come un passaggio, ad esempio hello **selezionare** istruzione hello seguente query:</span><span class="sxs-lookup"><span data-stu-id="0a48c-216">hello query that is outside hello **WITH** keyword (one query only) is also counted as a step, such as hello **SELECT** statement in hello following query:</span></span>

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute,3), TollBoothId

<span data-ttu-id="0a48c-217">Questa query include due passaggi.</span><span class="sxs-lookup"><span data-stu-id="0a48c-217">This query has two steps.</span></span>

> [!NOTE]
> <span data-ttu-id="0a48c-218">Questa query viene illustrata in dettaglio più avanti in articolo hello.</span><span class="sxs-lookup"><span data-stu-id="0a48c-218">This query is discussed in more detail later in hello article.</span></span>
>  

### <a name="partition-a-step"></a><span data-ttu-id="0a48c-219">Partizionamento di un passaggio</span><span class="sxs-lookup"><span data-stu-id="0a48c-219">Partition a step</span></span>
<span data-ttu-id="0a48c-220">Partizionamento di un passaggio necessario hello seguenti condizioni:</span><span class="sxs-lookup"><span data-stu-id="0a48c-220">Partitioning a step requires hello following conditions:</span></span>

* <span data-ttu-id="0a48c-221">origine di input Hello deve essere partizionato.</span><span class="sxs-lookup"><span data-stu-id="0a48c-221">hello input source must be partitioned.</span></span> 
* <span data-ttu-id="0a48c-222">Hello **selezionare** istruzione di query hello deve leggere da un'origine di input partizionata.</span><span class="sxs-lookup"><span data-stu-id="0a48c-222">hello **SELECT** statement of hello query must read from a partitioned input source.</span></span>
* <span data-ttu-id="0a48c-223">query di Hello all'interno di passaggio hello deve avere hello **Partition By** (parola chiave).</span><span class="sxs-lookup"><span data-stu-id="0a48c-223">hello query within hello step must have hello **Partition By** keyword.</span></span>

<span data-ttu-id="0a48c-224">Quando una query è partizionata, gli eventi di input hello sono partizione separata elaborati e aggregati in gruppi e gli eventi di output vengono generati per ognuno dei gruppi di hello.</span><span class="sxs-lookup"><span data-stu-id="0a48c-224">When a query is partitioned, hello input events are processed and aggregated in separate partition groups, and outputs events are generated for each of hello groups.</span></span> <span data-ttu-id="0a48c-225">Se si desidera una funzione di aggregazione combinato, è necessario creare un secondo tooaggregate passaggio non partizionata.</span><span class="sxs-lookup"><span data-stu-id="0a48c-225">If you want a combined aggregate, you must create a second non-partitioned step tooaggregate.</span></span>

### <a name="calculate-hello-max-streaming-units-for-a-job"></a><span data-ttu-id="0a48c-226">Calcolare il numero massimo hello unità per un processo di streaming</span><span class="sxs-lookup"><span data-stu-id="0a48c-226">Calculate hello max streaming units for a job</span></span>
<span data-ttu-id="0a48c-227">Tutti i passaggi non partizionata insieme possono scalare in verticale toosix unità (SUs) per un processo di flusso Analitica di streaming.</span><span class="sxs-lookup"><span data-stu-id="0a48c-227">All non-partitioned steps together can scale up toosix streaming units (SUs) for a Stream Analytics job.</span></span> <span data-ttu-id="0a48c-228">SUs tooadd, un passaggio devono essere partizionati.</span><span class="sxs-lookup"><span data-stu-id="0a48c-228">tooadd SUs, a step must be partitioned.</span></span> <span data-ttu-id="0a48c-229">Ogni partizione può includere sei unità di streaming.</span><span class="sxs-lookup"><span data-stu-id="0a48c-229">Each partition can have six SUs.</span></span>

<table border="1">
<tr><th><span data-ttu-id="0a48c-230">Query</span><span class="sxs-lookup"><span data-stu-id="0a48c-230">Query</span></span></th><th><span data-ttu-id="0a48c-231">SUs Max per processo hello</span><span class="sxs-lookup"><span data-stu-id="0a48c-231">Max SUs for hello job</span></span></th></td>

<tr><td>
<ul>
<li><span data-ttu-id="0a48c-232">query Hello contiene un unico passaggio.</span><span class="sxs-lookup"><span data-stu-id="0a48c-232">hello query contains one step.</span></span></li>
<li><span data-ttu-id="0a48c-233">passaggio di Hello non è partizionata.</span><span class="sxs-lookup"><span data-stu-id="0a48c-233">hello step is not partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="0a48c-234">6</span><span class="sxs-lookup"><span data-stu-id="0a48c-234">6</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="0a48c-235">flusso di dati di input Hello viene partizionata in base a 3.</span><span class="sxs-lookup"><span data-stu-id="0a48c-235">hello input data stream is partitioned by 3.</span></span></li>
<li><span data-ttu-id="0a48c-236">query Hello contiene un unico passaggio.</span><span class="sxs-lookup"><span data-stu-id="0a48c-236">hello query contains one step.</span></span></li>
<li><span data-ttu-id="0a48c-237">passaggio di Hello è partizionata.</span><span class="sxs-lookup"><span data-stu-id="0a48c-237">hello step is partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="0a48c-238">18</span><span class="sxs-lookup"><span data-stu-id="0a48c-238">18</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="0a48c-239">query Hello contiene due passi.</span><span class="sxs-lookup"><span data-stu-id="0a48c-239">hello query contains two steps.</span></span></li>
<li><span data-ttu-id="0a48c-240">Nessuno dei passaggi di hello è partizionata.</span><span class="sxs-lookup"><span data-stu-id="0a48c-240">Neither of hello steps is partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="0a48c-241">6</span><span class="sxs-lookup"><span data-stu-id="0a48c-241">6</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="0a48c-242">flusso di dati di input Hello viene partizionata in base a 3.</span><span class="sxs-lookup"><span data-stu-id="0a48c-242">hello input data stream is partitioned by 3.</span></span></li>
<li><span data-ttu-id="0a48c-243">query Hello contiene due passi.</span><span class="sxs-lookup"><span data-stu-id="0a48c-243">hello query contains two steps.</span></span> <span data-ttu-id="0a48c-244">passaggio di input Hello è partizionata e secondo passaggio hello non lo è.</span><span class="sxs-lookup"><span data-stu-id="0a48c-244">hello input step is partitioned and hello second step is not.</span></span></li>
<li><span data-ttu-id="0a48c-245">Hello <strong>selezionare</strong> istruzione legge da un input hello partizionata.</span><span class="sxs-lookup"><span data-stu-id="0a48c-245">hello <strong>SELECT</strong> statement reads from hello partitioned input.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="0a48c-246">24 (18 per i passaggi partizionati + 6 per i passaggi non partizionati)</span><span class="sxs-lookup"><span data-stu-id="0a48c-246">24 (18 for partitioned steps + 6 for non-partitioned steps)</span></span></td></tr>
</table>

### <a name="examples-of-scaling"></a><span data-ttu-id="0a48c-247">Esempi di ridimensionamento</span><span class="sxs-lookup"><span data-stu-id="0a48c-247">Examples of scaling</span></span>

<span data-ttu-id="0a48c-248">Hello nella query seguente calcola il numero di hello di automobili in una finestra di tre minuti passando un casello con tre tollbooths.</span><span class="sxs-lookup"><span data-stu-id="0a48c-248">hello following query calculates hello number of cars within a three-minute window going through a toll station that has three tollbooths.</span></span> <span data-ttu-id="0a48c-249">Questa query può essere ridimensionato verso l'alto toosix SUs.</span><span class="sxs-lookup"><span data-stu-id="0a48c-249">This query can be scaled up toosix SUs.</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="0a48c-250">toouse più SUs per hello query, entrambi hello flusso dati di input e query hello devono essere partizionati.</span><span class="sxs-lookup"><span data-stu-id="0a48c-250">toouse more SUs for hello query, both hello input data stream and hello query must be partitioned.</span></span> <span data-ttu-id="0a48c-251">Poiché la partizione di flusso di dati hello è impostata too3, hello query modificata seguente può essere ridimensionato verso l'alto too18 SUs:</span><span class="sxs-lookup"><span data-stu-id="0a48c-251">Since hello data stream partition is set too3, hello following modified query can be scaled up too18 SUs:</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="0a48c-252">Quando una query è partizionata, gli eventi di input hello vengono elaborati e aggregati in gruppi di una partizione separata.</span><span class="sxs-lookup"><span data-stu-id="0a48c-252">When a query is partitioned, hello input events are processed and aggregated in separate partition groups.</span></span> <span data-ttu-id="0a48c-253">Gli eventi di output vengono inoltre generati per ognuno dei gruppi di hello.</span><span class="sxs-lookup"><span data-stu-id="0a48c-253">Output events are also generated for each of hello groups.</span></span> <span data-ttu-id="0a48c-254">Partizionamento può causare alcuni risultati imprevisti quando hello **GROUP BY** campo non è una chiave di partizione hello nel flusso di dati di input hello.</span><span class="sxs-lookup"><span data-stu-id="0a48c-254">Partitioning can cause some unexpected results when hello **GROUP BY** field is not hello partition key in hello input data stream.</span></span> <span data-ttu-id="0a48c-255">Ad esempio, hello **TollBoothId** campo nella query precedente hello non è una chiave di partizione hello di **Input1**.</span><span class="sxs-lookup"><span data-stu-id="0a48c-255">For example, hello **TollBoothId** field in hello previous query is not hello partition key of **Input1**.</span></span> <span data-ttu-id="0a48c-256">il risultato di Hello è tale hello dati da casello #1 possono essere distribuiti in più partizioni.</span><span class="sxs-lookup"><span data-stu-id="0a48c-256">hello result is that hello data from TollBooth #1 can be spread in multiple partitions.</span></span>

<span data-ttu-id="0a48c-257">Ognuno di hello **Input1** partizioni saranno elaborate separatamente dal flusso Analitica.</span><span class="sxs-lookup"><span data-stu-id="0a48c-257">Each of hello **Input1** partitions will be processed separately by Stream Analytics.</span></span> <span data-ttu-id="0a48c-258">Di conseguenza, più record del numero di automobili hello per hello stesso casello in hello stessa finestra a cascata verrà creato.</span><span class="sxs-lookup"><span data-stu-id="0a48c-258">As a result, multiple records of hello car count for hello same tollbooth in hello same Tumbling window will be created.</span></span> <span data-ttu-id="0a48c-259">Se non è possibile modificare la chiave di partizione input hello, questo problema può essere risolto aggiungendo un passaggio non partizione, come in hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="0a48c-259">If hello input partition key can't be changed, this problem can be fixed by adding a non-partition step, as in hello following example:</span></span>

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute, 3), TollBoothId

<span data-ttu-id="0a48c-260">Questa query può essere scalato too24 SUs.</span><span class="sxs-lookup"><span data-stu-id="0a48c-260">This query can be scaled too24 SUs.</span></span>

> [!NOTE]
> <span data-ttu-id="0a48c-261">Se si siano unendo in join due flussi, assicurarsi che i flussi di hello vengono partizionati dalla chiave di partizione hello della colonna hello utilizzare toocreate hello join.</span><span class="sxs-lookup"><span data-stu-id="0a48c-261">If you are joining two streams, make sure that hello streams are partitioned by hello partition key of hello column that you use toocreate hello joins.</span></span> <span data-ttu-id="0a48c-262">Assicurarsi inoltre di aver hello stesso numero di partizioni in entrambi i flussi.</span><span class="sxs-lookup"><span data-stu-id="0a48c-262">Also make sure that you have hello same number of partitions in both streams.</span></span>
> 
> 

## <a name="configure-stream-analytics-streaming-units"></a><span data-ttu-id="0a48c-263">Configurare le unità di streaming di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="0a48c-263">Configure Stream Analytics streaming units</span></span>

1. <span data-ttu-id="0a48c-264">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0a48c-264">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0a48c-265">Nell'elenco di hello delle risorse, trovare il processo di flusso Analitica di hello tooscale desiderati e quindi aprirlo.</span><span class="sxs-lookup"><span data-stu-id="0a48c-265">In hello list of resources, find hello Stream Analytics job that you want tooscale and then open it.</span></span>
3. <span data-ttu-id="0a48c-266">In hello processo pannello in **configura**, fare clic su **scala**.</span><span class="sxs-lookup"><span data-stu-id="0a48c-266">In hello job blade, under **Configure**, click **Scale**.</span></span>

    ![Configurazione del processo di Analisi di flusso nel portale di Azure][img.stream.analytics.preview.portal.settings.scale]

4. <span data-ttu-id="0a48c-268">Utilizzare hello dispositivo di scorrimento tooset hello SUs per processo hello.</span><span class="sxs-lookup"><span data-stu-id="0a48c-268">Use hello slider tooset hello SUs for hello job.</span></span> <span data-ttu-id="0a48c-269">Si noti che le impostazioni SU toospecific limitato.</span><span class="sxs-lookup"><span data-stu-id="0a48c-269">Notice that you are limited toospecific SU settings.</span></span>


## <a name="monitor-job-performance"></a><span data-ttu-id="0a48c-270">Monitorare le prestazioni del processo</span><span class="sxs-lookup"><span data-stu-id="0a48c-270">Monitor job performance</span></span>
<span data-ttu-id="0a48c-271">Utilizza hello portale di Azure, è possibile tenere traccia della velocità effettiva hello di un processo:</span><span class="sxs-lookup"><span data-stu-id="0a48c-271">Using hello Azure portal, you can track hello throughput of a job:</span></span>

![Processi di monitoraggio di Analisi dei flussi di Azure][img.stream.analytics.monitor.job]

<span data-ttu-id="0a48c-273">Calcolare la velocità effettiva hello previsto del carico di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="0a48c-273">Calculate hello expected throughput of hello workload.</span></span> <span data-ttu-id="0a48c-274">Se la velocità effettiva hello è inferiore al previsto, ottimizzare partizione input hello, ottimizzare la query hello e aggiungere SUs tooyour processo.</span><span class="sxs-lookup"><span data-stu-id="0a48c-274">If hello throughput is less than expected, tune hello input partition, tune hello query, and add SUs tooyour job.</span></span>


## <a name="visualize-stream-analytics-throughput-at-scale-hello-raspberry-pi-scenario"></a><span data-ttu-id="0a48c-275">Visualizzare la velocità effettiva Analitica flusso a livello di scalabilità: scenario Pi Raspberry hello</span><span class="sxs-lookup"><span data-stu-id="0a48c-275">Visualize Stream Analytics throughput at scale: hello Raspberry Pi scenario</span></span>
<span data-ttu-id="0a48c-276">toohelp che è comprendere le modalità di scalabilità dei processi di flusso Analitica, è stata eseguita un esperimento in base all'input da un dispositivo Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="0a48c-276">toohelp you understand how Stream Analytics jobs scale, we performed an experiment based on input from a Raspberry Pi device.</span></span> <span data-ttu-id="0a48c-277">Questo esperimento farci vedere hello effetto sulla velocità effettiva di più unità di streaming e partizioni.</span><span class="sxs-lookup"><span data-stu-id="0a48c-277">This experiment let us see hello effect on throughput of multiple streaming units and partitions.</span></span>

<span data-ttu-id="0a48c-278">In questo scenario, il dispositivo hello invia hub di eventi tooan sensore dati (client).</span><span class="sxs-lookup"><span data-stu-id="0a48c-278">In this scenario, hello device sends sensor data (clients) tooan event hub.</span></span> <span data-ttu-id="0a48c-279">Streaming Analitica elabora dati hello e invia un avviso o nelle statistiche come un hub di eventi di output tooanother.</span><span class="sxs-lookup"><span data-stu-id="0a48c-279">Streaming Analytics processes hello data and sends an alert or statistics as an output tooanother event hub.</span></span> 

<span data-ttu-id="0a48c-280">client Hello invia i dati del sensore in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="0a48c-280">hello client sends sensor data in JSON format.</span></span> <span data-ttu-id="0a48c-281">anche l'output di Hello dati è in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="0a48c-281">hello data output is also in JSON format.</span></span> <span data-ttu-id="0a48c-282">dati Hello sono simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="0a48c-282">hello data looks like this:</span></span>

    {"devicetime":"2014-12-11T02:24:56.8850110Z","hmdt":42.7,"temp":72.6,"prss":98187.75,"lght":0.38,"dspl":"R-PI Olivier's Office"}

<span data-ttu-id="0a48c-283">Hello seguente query è toosend usato un avviso quando una luce è disattivata:</span><span class="sxs-lookup"><span data-stu-id="0a48c-283">hello following query is used toosend an alert when a light is switched off:</span></span>

    SELECT AVG(lght),
     "LightOff" as AlertText
    FROM input TIMESTAMP
    BY devicetime
     WHERE
        lght< 0.05 GROUP BY TumblingWindow(second, 1)

### <a name="measure-throughput"></a><span data-ttu-id="0a48c-284">Misurare la velocità effettiva</span><span class="sxs-lookup"><span data-stu-id="0a48c-284">Measure throughput</span></span>

<span data-ttu-id="0a48c-285">In questo contesto, velocità effettiva è quantità hello dei dati di input elaborati dal flusso Analitica in un periodo di tempo stabilito.</span><span class="sxs-lookup"><span data-stu-id="0a48c-285">In this context, throughput is hello amount of input data processed by Stream Analytics in a fixed amount of time.</span></span> <span data-ttu-id="0a48c-286">(È misurato per 10 minuti). dati di input tooachieve hello migliore elaborazione velocità effettiva per hello, sia i dati hello flusso di input e sono stati partizionati query hello.</span><span class="sxs-lookup"><span data-stu-id="0a48c-286">(We measured for 10 minutes.) tooachieve hello best processing throughput for hello input data, both hello data stream input and hello query were  partitioned.</span></span> <span data-ttu-id="0a48c-287">Sono inclusi **Count ()** in hello query toomeasure sono stati elaborati come molti eventi di input.</span><span class="sxs-lookup"><span data-stu-id="0a48c-287">We included **COUNT()** in hello query toomeasure how many input events were processed.</span></span> <span data-ttu-id="0a48c-288">processo hello che toomake non semplicemente attendendo toocome gli eventi di input, ogni partizione dell'hub di eventi di input hello è stato precaricato con circa 300 MB di dati di input.</span><span class="sxs-lookup"><span data-stu-id="0a48c-288">toomake sure hello job was not simply waiting for input events toocome, each partition of hello input event hub was preloaded with about 300 MB of input data.</span></span>

<span data-ttu-id="0a48c-289">Hello nella tabella seguente sono illustrati i risultati di hello che è stato illustrato quando è stato aumentato il numero di hello di unità di streaming e partizione corrispondente hello conteggi nell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="0a48c-289">hello following table shows hello results we saw when we increased hello number of streaming units and hello corresponding partition counts in event hubs.</span></span>  

<table border="1">
<tr><th><span data-ttu-id="0a48c-290">Partizioni di input</span><span class="sxs-lookup"><span data-stu-id="0a48c-290">Input Partitions</span></span></th><th><span data-ttu-id="0a48c-291">Partizioni di output</span><span class="sxs-lookup"><span data-stu-id="0a48c-291">Output Partitions</span></span></th><th><span data-ttu-id="0a48c-292">Unità di streaming</span><span class="sxs-lookup"><span data-stu-id="0a48c-292">Streaming Units</span></span></th><th><span data-ttu-id="0a48c-293">Velocità effettiva sostenuta</span><span class="sxs-lookup"><span data-stu-id="0a48c-293">Sustained Throughput</span></span>
</th></td>

<tr><td><span data-ttu-id="0a48c-294">12</span><span class="sxs-lookup"><span data-stu-id="0a48c-294">12</span></span></td>
<td><span data-ttu-id="0a48c-295">12</span><span class="sxs-lookup"><span data-stu-id="0a48c-295">12</span></span></td>
<td><span data-ttu-id="0a48c-296">6</span><span class="sxs-lookup"><span data-stu-id="0a48c-296">6</span></span></td>
<td><span data-ttu-id="0a48c-297">4,06 MB/s</span><span class="sxs-lookup"><span data-stu-id="0a48c-297">4.06 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="0a48c-298">12</span><span class="sxs-lookup"><span data-stu-id="0a48c-298">12</span></span></td>
<td><span data-ttu-id="0a48c-299">12</span><span class="sxs-lookup"><span data-stu-id="0a48c-299">12</span></span></td>
<td><span data-ttu-id="0a48c-300">12</span><span class="sxs-lookup"><span data-stu-id="0a48c-300">12</span></span></td>
<td><span data-ttu-id="0a48c-301">8,06 MB/s</span><span class="sxs-lookup"><span data-stu-id="0a48c-301">8.06 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="0a48c-302">48</span><span class="sxs-lookup"><span data-stu-id="0a48c-302">48</span></span></td>
<td><span data-ttu-id="0a48c-303">48</span><span class="sxs-lookup"><span data-stu-id="0a48c-303">48</span></span></td>
<td><span data-ttu-id="0a48c-304">48</span><span class="sxs-lookup"><span data-stu-id="0a48c-304">48</span></span></td>
<td><span data-ttu-id="0a48c-305">38,32 MB/s</span><span class="sxs-lookup"><span data-stu-id="0a48c-305">38.32 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="0a48c-306">192</span><span class="sxs-lookup"><span data-stu-id="0a48c-306">192</span></span></td>
<td><span data-ttu-id="0a48c-307">192</span><span class="sxs-lookup"><span data-stu-id="0a48c-307">192</span></span></td>
<td><span data-ttu-id="0a48c-308">192</span><span class="sxs-lookup"><span data-stu-id="0a48c-308">192</span></span></td>
<td><span data-ttu-id="0a48c-309">172,67 MB/s</span><span class="sxs-lookup"><span data-stu-id="0a48c-309">172.67 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="0a48c-310">480</span><span class="sxs-lookup"><span data-stu-id="0a48c-310">480</span></span></td>
<td><span data-ttu-id="0a48c-311">480</span><span class="sxs-lookup"><span data-stu-id="0a48c-311">480</span></span></td>
<td><span data-ttu-id="0a48c-312">480</span><span class="sxs-lookup"><span data-stu-id="0a48c-312">480</span></span></td>
<td><span data-ttu-id="0a48c-313">454,27 MB/s</span><span class="sxs-lookup"><span data-stu-id="0a48c-313">454.27 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="0a48c-314">720</span><span class="sxs-lookup"><span data-stu-id="0a48c-314">720</span></span></td>
<td><span data-ttu-id="0a48c-315">720</span><span class="sxs-lookup"><span data-stu-id="0a48c-315">720</span></span></td>
<td><span data-ttu-id="0a48c-316">720</span><span class="sxs-lookup"><span data-stu-id="0a48c-316">720</span></span></td>
<td><span data-ttu-id="0a48c-317">609,69 MB/s</span><span class="sxs-lookup"><span data-stu-id="0a48c-317">609.69 MB/s</span></span></td>
</tr>
</table>

<span data-ttu-id="0a48c-318">E hello grafico seguente viene illustrata una visualizzazione della relazione hello tra SUs e la velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="0a48c-318">And hello following graph shows a visualization of hello relationship between SUs and throughput.</span></span>

![img.stream.analytics.perfgraph][img.stream.analytics.perfgraph]

## <a name="get-help"></a><span data-ttu-id="0a48c-320">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="0a48c-320">Get help</span></span>
<span data-ttu-id="0a48c-321">Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="0a48c-321">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a48c-322">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0a48c-322">Next steps</span></span>
* [<span data-ttu-id="0a48c-323">Introduzione tooAzure flusso Analitica</span><span class="sxs-lookup"><span data-stu-id="0a48c-323">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="0a48c-324">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="0a48c-324">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="0a48c-325">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="0a48c-325">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="0a48c-326">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="0a48c-326">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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

