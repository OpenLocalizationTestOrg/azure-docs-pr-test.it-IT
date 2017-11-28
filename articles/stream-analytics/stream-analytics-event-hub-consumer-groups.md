---
title: aaaDebug Analitica di flusso di Azure con i ricevitori di eventi hub | Documenti Microsoft
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
ms.openlocfilehash: 89821e6273151de43b5e42d907e547c939e24824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="debug-azure-stream-analytics-with-event-hub-receivers"></a><span data-ttu-id="72fe5-104">Eseguire il debug di Analisi di flusso di Azure con i ricevitori dell'hub eventi</span><span class="sxs-lookup"><span data-stu-id="72fe5-104">Debug Azure Stream Analytics with event hub receivers</span></span>

<span data-ttu-id="72fe5-105">Azure flusso Analitica tooingest o output dei dati da un processo, è possibile utilizzare gli hub di eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="72fe5-105">You can use Azure Event Hubs in Azure Stream Analytics tooingest or output data from a job.</span></span> <span data-ttu-id="72fe5-106">Una procedura consigliata per l'uso di hub eventi è toouse più gruppi di consumer, scalabilità processo tooensure.</span><span class="sxs-lookup"><span data-stu-id="72fe5-106">A best practice for using Event Hubs is toouse multiple consumer groups, tooensure job scalability.</span></span> <span data-ttu-id="72fe5-107">Uno dei motivi è che il numero di hello di lettori nel processo di flusso Analitica hello un input specifico riguarda il numero di hello di lettori in un gruppo di consumer singolo.</span><span class="sxs-lookup"><span data-stu-id="72fe5-107">One reason is that hello number of readers in hello Stream Analytics job for a specific input affects hello number of readers in a single consumer group.</span></span> <span data-ttu-id="72fe5-108">numero preciso di Hello di ricevitori è basato sui dettagli di implementazione interna per la logica della topologia di scalabilità orizzontale hello.</span><span class="sxs-lookup"><span data-stu-id="72fe5-108">hello precise number of receivers is based on internal implementation details for hello scale-out topology logic.</span></span> <span data-ttu-id="72fe5-109">numero di Hello di ricevitori non è esposta esternamente.</span><span class="sxs-lookup"><span data-stu-id="72fe5-109">hello number of receivers is not exposed externally.</span></span> <span data-ttu-id="72fe5-110">numero di Hello di lettori può cambiare in fase di inizio processo hello o durante gli aggiornamenti di processo.</span><span class="sxs-lookup"><span data-stu-id="72fe5-110">hello number of readers can change either at hello job start time or during job upgrades.</span></span>

> [!NOTE]
> <span data-ttu-id="72fe5-111">Quando il numero di hello di lettori cambia durante l'aggiornamento di un processo, gli avvisi temporanei vengono scritti tooaudit log.</span><span class="sxs-lookup"><span data-stu-id="72fe5-111">When hello number of readers changes during a job upgrade, transient warnings are written tooaudit logs.</span></span> <span data-ttu-id="72fe5-112">I processi di Analisi di flusso vengono ripristinati automaticamente da questi problemi temporanei.</span><span class="sxs-lookup"><span data-stu-id="72fe5-112">Stream Analytics jobs automatically recover from these transient issues.</span></span>

## <a name="number-of-readers-per-partition-exceeds-event-hubs-limit-of-five"></a><span data-ttu-id="72fe5-113">Il numero di lettori per partizione supera il limite di cinque hub eventi</span><span class="sxs-lookup"><span data-stu-id="72fe5-113">Number of readers per partition exceeds Event Hubs limit of five</span></span>

<span data-ttu-id="72fe5-114">Gli scenari in cui hello numero di lettori per ogni partizione supera il limite di hub eventi hello di cinque includono seguente hello:</span><span class="sxs-lookup"><span data-stu-id="72fe5-114">Scenarios in which hello number of readers per partition exceeds hello Event Hubs limit of five include hello following:</span></span>

* <span data-ttu-id="72fe5-115">Più istruzioni SELECT: se si utilizzano più istruzioni SELECT che fanno riferimento troppo**stesso** hub eventi di input, ogni istruzione SELECT fa sì che un nuovo toobe ricevitore creato.</span><span class="sxs-lookup"><span data-stu-id="72fe5-115">Multiple SELECT statements: If you use multiple SELECT statements that refer too**same** event hub input, each SELECT statement causes a new receiver toobe created.</span></span>
* <span data-ttu-id="72fe5-116">UNIONE: Quando si utilizza un'unione, è possibile toohave più input che fanno riferimento toohello **stesso** gruppo di hub e consumer di eventi.</span><span class="sxs-lookup"><span data-stu-id="72fe5-116">UNION: When you use a UNION, it's possible toohave multiple inputs that refer toohello **same** event hub and consumer group.</span></span>
* <span data-ttu-id="72fe5-117">Self-JOIN: Quando si usa un'operazione SELF JOIN, è possibile toorefer toohello **stesso** hub di eventi più volte.</span><span class="sxs-lookup"><span data-stu-id="72fe5-117">SELF JOIN: When you use a SELF JOIN operation, it's possible toorefer toohello **same** event hub multiple times.</span></span>

## <a name="solution"></a><span data-ttu-id="72fe5-118">Soluzione</span><span class="sxs-lookup"><span data-stu-id="72fe5-118">Solution</span></span>

<span data-ttu-id="72fe5-119">Hello procedure consigliate seguenti consente di attenuare gli scenari in cui hello numero di lettori per ogni partizione supera il limite di hub eventi hello di cinque.</span><span class="sxs-lookup"><span data-stu-id="72fe5-119">hello following best practices can help mitigate scenarios in which hello number of readers per partition exceeds hello Event Hubs limit of five.</span></span>

### <a name="split-your-query-into-multiple-steps-by-using-a-with-clause"></a><span data-ttu-id="72fe5-120">Suddividere la query in più passaggi usando una clausola WITH</span><span class="sxs-lookup"><span data-stu-id="72fe5-120">Split your query into multiple steps by using a WITH clause</span></span>

<span data-ttu-id="72fe5-121">clausola WITH Hello specifica un set di risultati denominato temporaneo che è possibile fare riferimento a una clausola FROM nella query hello.</span><span class="sxs-lookup"><span data-stu-id="72fe5-121">hello WITH clause specifies a temporary named result set that can be referenced by a FROM clause in hello query.</span></span> <span data-ttu-id="72fe5-122">Definire una clausola WITH hello in ambito di esecuzione hello di una singola istruzione SELECT.</span><span class="sxs-lookup"><span data-stu-id="72fe5-122">You define hello WITH clause in hello execution scope of a single SELECT statement.</span></span>

<span data-ttu-id="72fe5-123">Ad esempio, invece di questa query:</span><span class="sxs-lookup"><span data-stu-id="72fe5-123">For example, instead of this query:</span></span>

```
SELECT foo 
INTO output1
FROM inputEventHub

SELECT bar
INTO output2
FROM inputEventHub 
…
```

<span data-ttu-id="72fe5-124">Usare questa query:</span><span class="sxs-lookup"><span data-stu-id="72fe5-124">Use this query:</span></span>

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

### <a name="ensure-that-inputs-bind-toodifferent-consumer-groups"></a><span data-ttu-id="72fe5-125">Verificare che gli input associano gruppi di consumer toodifferent</span><span class="sxs-lookup"><span data-stu-id="72fe5-125">Ensure that inputs bind toodifferent consumer groups</span></span>

<span data-ttu-id="72fe5-126">Per le query in cui tre o più input sono connesso toohello consumer di hub eventi stesso gruppo, creare gruppi di consumer distinto.</span><span class="sxs-lookup"><span data-stu-id="72fe5-126">For queries in which three or more inputs are connected toohello same Event Hubs consumer group, create separate consumer groups.</span></span> <span data-ttu-id="72fe5-127">Ciò richiede la creazione di hello di input flusso Analitica aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="72fe5-127">This requires hello creation of additional Stream Analytics inputs.</span></span>


## <a name="get-help"></a><span data-ttu-id="72fe5-128">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="72fe5-128">Get help</span></span>
<span data-ttu-id="72fe5-129">Per ottenere assistenza aggiuntiva, provare ad accedere al [forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="72fe5-129">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="72fe5-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="72fe5-130">Next steps</span></span>
* [<span data-ttu-id="72fe5-131">Introduzione tooStream Analitica</span><span class="sxs-lookup"><span data-stu-id="72fe5-131">Introduction tooStream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="72fe5-132">Introduzione ad Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="72fe5-132">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="72fe5-133">Scalabilità dei processi di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="72fe5-133">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="72fe5-134">Informazioni di riferimento sul linguaggio di query di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="72fe5-134">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="72fe5-135">Informazioni di riferimento sull'API REST di gestione di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="72fe5-135">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
