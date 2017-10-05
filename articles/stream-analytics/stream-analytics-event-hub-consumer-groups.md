---
title: Eseguire il debug di Analisi di flusso di Azure con i ricevitori dell'hub eventi | Documentazione Microsoft
description: Procedure consigliate di query per considerare i gruppi di consumer dell'hub eventi nei processi di Analisi di flusso.
keywords: limite dell'hub eventi, gruppo di consumer
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
ms.openlocfilehash: 145981d0b5eff0c574c5012c85f43a6318ba4126
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="debug-azure-stream-analytics-with-event-hub-receivers"></a><span data-ttu-id="ece3f-104">Eseguire il debug di Analisi di flusso di Azure con i ricevitori dell'hub eventi</span><span class="sxs-lookup"><span data-stu-id="ece3f-104">Debug Azure Stream Analytics with event hub receivers</span></span>

<span data-ttu-id="ece3f-105">È possibile usare gli hub eventi di Analisi di flusso di Azure per inserire o estrarre dati da un processo.</span><span class="sxs-lookup"><span data-stu-id="ece3f-105">You can use Azure Event Hubs in Azure Stream Analytics to ingest or output data from a job.</span></span> <span data-ttu-id="ece3f-106">Una procedura consigliata per l'utilizzo dell'hub eventi è usare più gruppi di consumer in modo da garantire la scalabilità del processo.</span><span class="sxs-lookup"><span data-stu-id="ece3f-106">A best practice for using Event Hubs is to use multiple consumer groups, to ensure job scalability.</span></span> <span data-ttu-id="ece3f-107">Uno dei motivi è che il numero di lettori del processo di Analisi di flusso per uno specifico input influisce sul numero dei lettori di un singolo gruppo di consumer.</span><span class="sxs-lookup"><span data-stu-id="ece3f-107">One reason is that the number of readers in the Stream Analytics job for a specific input affects the number of readers in a single consumer group.</span></span> <span data-ttu-id="ece3f-108">Il numero preciso di ricevitori si basa sui dettagli di implementazione interna per la logica della topologia con scalabilità orizzontale.</span><span class="sxs-lookup"><span data-stu-id="ece3f-108">The precise number of receivers is based on internal implementation details for the scale-out topology logic.</span></span> <span data-ttu-id="ece3f-109">Il numero di ricevitori non viene esposto esternamente.</span><span class="sxs-lookup"><span data-stu-id="ece3f-109">The number of receivers is not exposed externally.</span></span> <span data-ttu-id="ece3f-110">Il numero di lettori può cambiare al momento di inizio del processo o durante gli aggiornamenti del processo.</span><span class="sxs-lookup"><span data-stu-id="ece3f-110">The number of readers can change either at the job start time or during job upgrades.</span></span>

> [!NOTE]
> <span data-ttu-id="ece3f-111">Quando il numero di lettori cambia durante un aggiornamento del processo, vengono scritti avvisi temporanei nei log di controllo.</span><span class="sxs-lookup"><span data-stu-id="ece3f-111">When the number of readers changes during a job upgrade, transient warnings are written to audit logs.</span></span> <span data-ttu-id="ece3f-112">I processi di Analisi di flusso vengono ripristinati automaticamente da questi problemi temporanei.</span><span class="sxs-lookup"><span data-stu-id="ece3f-112">Stream Analytics jobs automatically recover from these transient issues.</span></span>

## <a name="number-of-readers-per-partition-exceeds-event-hubs-limit-of-five"></a><span data-ttu-id="ece3f-113">Il numero di lettori per partizione supera il limite di cinque hub eventi</span><span class="sxs-lookup"><span data-stu-id="ece3f-113">Number of readers per partition exceeds Event Hubs limit of five</span></span>

<span data-ttu-id="ece3f-114">Gli scenari in cui il numero di lettori per ogni partizione supera il limite di cinque hub eventi comprendono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="ece3f-114">Scenarios in which the number of readers per partition exceeds the Event Hubs limit of five include the following:</span></span>

* <span data-ttu-id="ece3f-115">Più istruzioni SELECT: se si usano più istruzioni SELECT che fanno riferimento allo **stesso** input dell'hub eventi, ogni istruzione SELECT fa sì che venga creato un nuovo ricevitore.</span><span class="sxs-lookup"><span data-stu-id="ece3f-115">Multiple SELECT statements: If you use multiple SELECT statements that refer to **same** event hub input, each SELECT statement causes a new receiver to be created.</span></span>
* <span data-ttu-id="ece3f-116">UNION: quando si usa UNION, è possibile avere più input che si riferiscono allo **stesso** hub eventi e gruppo di consumer.</span><span class="sxs-lookup"><span data-stu-id="ece3f-116">UNION: When you use a UNION, it's possible to have multiple inputs that refer to the **same** event hub and consumer group.</span></span>
* <span data-ttu-id="ece3f-117">SELF JOIN: quando si usa un'operazione SELF JOIN è possibile fare riferimento allo **stesso** hub eventi più volte.</span><span class="sxs-lookup"><span data-stu-id="ece3f-117">SELF JOIN: When you use a SELF JOIN operation, it's possible to refer to the **same** event hub multiple times.</span></span>

## <a name="solution"></a><span data-ttu-id="ece3f-118">Soluzione</span><span class="sxs-lookup"><span data-stu-id="ece3f-118">Solution</span></span>

<span data-ttu-id="ece3f-119">Le procedure consigliate seguenti possono aiutare a mitigare gli scenari in cui il numero di lettori per ogni partizione supera il limite di cinque hub eventi.</span><span class="sxs-lookup"><span data-stu-id="ece3f-119">The following best practices can help mitigate scenarios in which the number of readers per partition exceeds the Event Hubs limit of five.</span></span>

### <a name="split-your-query-into-multiple-steps-by-using-a-with-clause"></a><span data-ttu-id="ece3f-120">Suddividere la query in più passaggi usando una clausola WITH</span><span class="sxs-lookup"><span data-stu-id="ece3f-120">Split your query into multiple steps by using a WITH clause</span></span>

<span data-ttu-id="ece3f-121">La clausola WITH specifica un set di risultati con nome temporaneo a cui è possibile fare riferimento mediante una clausola FROM nella query.</span><span class="sxs-lookup"><span data-stu-id="ece3f-121">The WITH clause specifies a temporary named result set that can be referenced by a FROM clause in the query.</span></span> <span data-ttu-id="ece3f-122">La clausola WITH viene definita nell'ambito di esecuzione di una singola istruzione SELECT.</span><span class="sxs-lookup"><span data-stu-id="ece3f-122">You define the WITH clause in the execution scope of a single SELECT statement.</span></span>

<span data-ttu-id="ece3f-123">Ad esempio, invece di questa query:</span><span class="sxs-lookup"><span data-stu-id="ece3f-123">For example, instead of this query:</span></span>

```
SELECT foo 
INTO output1
FROM inputEventHub

SELECT bar
INTO output2
FROM inputEventHub 
…
```

<span data-ttu-id="ece3f-124">Usare questa query:</span><span class="sxs-lookup"><span data-stu-id="ece3f-124">Use this query:</span></span>

```
WITH input (
   SELECT * FROM inputEventHub
) as data

SELECT foo
INTO output1
FROM data

SELECT bar
INTO output2
FROM data
…
```

### <a name="ensure-that-inputs-bind-to-different-consumer-groups"></a><span data-ttu-id="ece3f-125">Assicurarsi che gli input siano associati a gruppi di consumer diversi</span><span class="sxs-lookup"><span data-stu-id="ece3f-125">Ensure that inputs bind to different consumer groups</span></span>

<span data-ttu-id="ece3f-126">Per le query in cui tre o più input sono connessi allo stesso gruppo di consumer di hub eventi, creare gruppi di consumer separati.</span><span class="sxs-lookup"><span data-stu-id="ece3f-126">For queries in which three or more inputs are connected to the same Event Hubs consumer group, create separate consumer groups.</span></span> <span data-ttu-id="ece3f-127">Ciò richiede la creazione di input di Analisi di flusso aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="ece3f-127">This requires the creation of additional Stream Analytics inputs.</span></span>


## <a name="get-help"></a><span data-ttu-id="ece3f-128">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="ece3f-128">Get help</span></span>
<span data-ttu-id="ece3f-129">Per ottenere assistenza aggiuntiva, provare ad accedere al [forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="ece3f-129">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ece3f-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ece3f-130">Next steps</span></span>
* [<span data-ttu-id="ece3f-131">Presentazione di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="ece3f-131">Introduction to Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="ece3f-132">Introduzione ad Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="ece3f-132">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="ece3f-133">Scalabilità dei processi di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="ece3f-133">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="ece3f-134">Informazioni di riferimento sul linguaggio di query di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="ece3f-134">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="ece3f-135">Informazioni di riferimento sull'API REST di gestione di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="ece3f-135">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
