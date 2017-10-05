---
title: ReliableConcurrentQueue in Azure Service Fabric
description: "ReliableConcurrentQueue è una coda ad alta velocità effettiva che consente operazioni di accodamento e rimozione dalla coda in parallelo."
services: service-fabric
documentationcenter: .net
author: sangarg
manager: timlt
editor: raja,tyadam,masnider,vturecek
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: sangarg
ms.openlocfilehash: 122cb48149477f295a65b8ee623c647b6db10a86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-reliableconcurrentqueue-in-azure-service-fabric"></a><span data-ttu-id="e59eb-103">Introduzione a ReliableConcurrentQueue in Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e59eb-103">Introduction to ReliableConcurrentQueue in Azure Service Fabric</span></span>
<span data-ttu-id="e59eb-104">La coda simultanea affidabile è una coda replicata, transazionale e asincrona che assicura concorrenza elevata per le operazioni di accodamento e rimozione dalla coda.</span><span class="sxs-lookup"><span data-stu-id="e59eb-104">Reliable Concurrent Queue is an asynchronous, transactional, and replicated queue which features high concurrency for enqueue and dequeue operations.</span></span> <span data-ttu-id="e59eb-105">È progettata per offrire velocità effettiva elevata e bassa latenza allentando il vincolo di ordinamento FIFO fornito dalla [coda affidabile](https://msdn.microsoft.com/library/azure/dn971527.aspx) e fornisce invece un ordinamento in base al migliore sforzo.</span><span class="sxs-lookup"><span data-stu-id="e59eb-105">It is designed to deliver high throughput and low latency by relaxing the strict FIFO ordering provided by [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) and instead provides a best-effort ordering.</span></span>

## <a name="apis"></a><span data-ttu-id="e59eb-106">API</span><span class="sxs-lookup"><span data-stu-id="e59eb-106">APIs</span></span>

|<span data-ttu-id="e59eb-107">Coda simultanea</span><span class="sxs-lookup"><span data-stu-id="e59eb-107">Concurrent Queue</span></span>                |<span data-ttu-id="e59eb-108">Coda simultanea affidabile</span><span class="sxs-lookup"><span data-stu-id="e59eb-108">Reliable Concurrent Queue</span></span>                                         |
|--------------------------------|------------------------------------------------------------------|
| <span data-ttu-id="e59eb-109">void Enqueue(T item)</span><span class="sxs-lookup"><span data-stu-id="e59eb-109">void Enqueue(T item)</span></span>           | <span data-ttu-id="e59eb-110">Task EnqueueAsync(ITransaction tx, T item)</span><span class="sxs-lookup"><span data-stu-id="e59eb-110">Task EnqueueAsync(ITransaction tx, T item)</span></span>                       |
| <span data-ttu-id="e59eb-111">bool TryDequeue(out T result)</span><span class="sxs-lookup"><span data-stu-id="e59eb-111">bool TryDequeue(out T result)</span></span>  | <span data-ttu-id="e59eb-112">Task< ConditionalValue < T > > TryDequeueAsync(ITransaction tx)</span><span class="sxs-lookup"><span data-stu-id="e59eb-112">Task< ConditionalValue < T > > TryDequeueAsync(ITransaction tx)</span></span>  |
| <span data-ttu-id="e59eb-113">int Count()</span><span class="sxs-lookup"><span data-stu-id="e59eb-113">int Count()</span></span>                    | <span data-ttu-id="e59eb-114">long Count()</span><span class="sxs-lookup"><span data-stu-id="e59eb-114">long Count()</span></span>                                                     |

## <a name="comparison-with-reliable-queuehttpsmsdnmicrosoftcomlibraryazuredn971527aspx"></a><span data-ttu-id="e59eb-115">Confronto con la [coda affidabile](https://msdn.microsoft.com/library/azure/dn971527.aspx)</span><span class="sxs-lookup"><span data-stu-id="e59eb-115">Comparison with [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx)</span></span>

<span data-ttu-id="e59eb-116">La coda simultanea affidabile è disponibile come alternativa alla [coda affidabile](https://msdn.microsoft.com/library/azure/dn971527.aspx).</span><span class="sxs-lookup"><span data-stu-id="e59eb-116">Reliable Concurrent Queue is offered as an alternative to [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx).</span></span> <span data-ttu-id="e59eb-117">Deve essere usata nei casi in cui non è necessario l'ordine FIFO in modo vincolante poiché l'ordine FIFO richiede un compromesso in termini di concorrenza.</span><span class="sxs-lookup"><span data-stu-id="e59eb-117">It should be used in cases where strict FIFO ordering is not required, as guaranteeing FIFO requires a tradeoff with concurrency.</span></span>  <span data-ttu-id="e59eb-118">La [coda affidabile](https://msdn.microsoft.com/library/azure/dn971527.aspx) usa i blocchi per applicare l'ordinamento FIFO, consentendo al massimo una transazione per l'accodamento e al massimo una transazione per la rimozione dalla coda.</span><span class="sxs-lookup"><span data-stu-id="e59eb-118">[Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) uses locks to enforce FIFO ordering, with at most one transaction allowed to enqueue and at most one transaction allowed to dequeue at a time.</span></span> <span data-ttu-id="e59eb-119">La coda simultanea affidabile allenta invece il vincolo di ordinamento e consente a un qualsiasi numero di transazioni simultanee di interfoliare le operazioni di accodamento e rimozione dalla coda.</span><span class="sxs-lookup"><span data-stu-id="e59eb-119">In comparison, Reliable Concurrent Queue relaxes the ordering constraint and allows any number concurrent transactions to interleave their enqueue and dequeue operations.</span></span> <span data-ttu-id="e59eb-120">Viene fornito l'ordinamento in base al migliore sforzo; tuttavia non è mai possibile garantire l'ordinamento dei due valori in una coda simultanea affidabile.</span><span class="sxs-lookup"><span data-stu-id="e59eb-120">Best-effort ordering is provided, however the relative ordering of two values in a Reliable Concurrent Queue can never be guaranteed.</span></span>

<span data-ttu-id="e59eb-121">La coda simultanea affidabile garantisce maggiore velocità effettiva e latenza ridotta rispetto alla [coda affidabile](https://msdn.microsoft.com/library/azure/dn971527.aspx) ogni volta che sono presenti più transazioni simultanee che eseguono operazioni di accodamento e/o rimozione dalla coda.</span><span class="sxs-lookup"><span data-stu-id="e59eb-121">Reliable Concurrent Queue provides higher throughput and lower latency than [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) whenever there are multiple concurrent transactions performing enqueues and/or dequeues.</span></span>

<span data-ttu-id="e59eb-122">Un esempio di caso d'uso per ReliableConcurrentQueue è lo scenario della [coda di messaggi](https://en.wikipedia.org/wiki/Message_queue).</span><span class="sxs-lookup"><span data-stu-id="e59eb-122">A sample use case for the ReliableConcurrentQueue is the [Message Queue](https://en.wikipedia.org/wiki/Message_queue) scenario.</span></span> <span data-ttu-id="e59eb-123">In questo scenario uno o più producer di messaggi creano e aggiungono elementi nella coda e uno o più consumer di messaggi prelevano i messaggi dalla coda e li elaborano.</span><span class="sxs-lookup"><span data-stu-id="e59eb-123">In this scenario, one or more message producers create and add items to the queue, and one or more message consumers pull messages from the queue and process them.</span></span> <span data-ttu-id="e59eb-124">Più producer e consumer possono operare in modo indipendente usando le transazioni simultanee per elaborare la coda.</span><span class="sxs-lookup"><span data-stu-id="e59eb-124">Multiple producers and consumers can work independently, using concurrent transactions in order to process the queue.</span></span>

## <a name="usage-guidelines"></a><span data-ttu-id="e59eb-125">Linee guida per l'uso</span><span class="sxs-lookup"><span data-stu-id="e59eb-125">Usage Guidelines</span></span>
* <span data-ttu-id="e59eb-126">Il periodo di conservazione previsto per gli elementi nella coda è minimo,</span><span class="sxs-lookup"><span data-stu-id="e59eb-126">The queue expects that the items in the queue have a low retention period.</span></span> <span data-ttu-id="e59eb-127">ovvero gli elementi non rimangono nella coda per molto tempo.</span><span class="sxs-lookup"><span data-stu-id="e59eb-127">That is, the items would not stay in the queue for a long time.</span></span>
* <span data-ttu-id="e59eb-128">La coda non garantisce l'ordine FIFO in modo vincolante.</span><span class="sxs-lookup"><span data-stu-id="e59eb-128">The queue does not guarantee strict FIFO ordering.</span></span>
* <span data-ttu-id="e59eb-129">La coda non legge le proprie scritture.</span><span class="sxs-lookup"><span data-stu-id="e59eb-129">The queue does not read its own writes.</span></span> <span data-ttu-id="e59eb-130">Se un elemento viene accodato all'interno di una transazione, non sarà visibile a un dequeuer all'interno della stessa transazione.</span><span class="sxs-lookup"><span data-stu-id="e59eb-130">If an item is enqueued within a transaction, it will not be visible to a dequeuer within the same transaction.</span></span>
* <span data-ttu-id="e59eb-131">Le rimozioni dalla coda non sono isolate tra loro.</span><span class="sxs-lookup"><span data-stu-id="e59eb-131">Dequeues are not isolated from each other.</span></span> <span data-ttu-id="e59eb-132">Se l'elemento *A* viene rimosso dalla coda nella transazione *txnA*, anche se non viene eseguito il commit di *txnA*, l'elemento *A* non sarà visibile a una transazione simultanea *txnB*.</span><span class="sxs-lookup"><span data-stu-id="e59eb-132">If item *A* is dequeued in transaction *txnA*, even though *txnA* is not committed, item *A* would not be visible to a concurrent transaction *txnB*.</span></span>  <span data-ttu-id="e59eb-133">Se la transazione *txnA* viene interrotta, *A* diventa immediatamente visibile alla transazione *txnB*.</span><span class="sxs-lookup"><span data-stu-id="e59eb-133">If *txnA* aborts, *A* will become visible to *txnB* immediately.</span></span>
* <span data-ttu-id="e59eb-134">Il comportamento di *TryPeekAsync* può essere implementato usando un *TryDequeueAsync* e quindi interrompendo la transazione.</span><span class="sxs-lookup"><span data-stu-id="e59eb-134">*TryPeekAsync* behavior can be implemented by using a *TryDequeueAsync* and then aborting the transaction.</span></span> <span data-ttu-id="e59eb-135">Un esempio in proposito è reperibile nella sezione relativa ai modelli di programmazione.</span><span class="sxs-lookup"><span data-stu-id="e59eb-135">An example of this can be found in the Programming Patterns section.</span></span>
* <span data-ttu-id="e59eb-136">Il conteggio non è transazionale.</span><span class="sxs-lookup"><span data-stu-id="e59eb-136">Count is non-transactional.</span></span> <span data-ttu-id="e59eb-137">Può dare un'idea del numero di elementi in una coda, ma rappresenta un valore temporizzato e non può essere ritenuto affidabile.</span><span class="sxs-lookup"><span data-stu-id="e59eb-137">It can be used to get an idea of the number of elements in the queue, but represents a point-in-time and cannot be relied upon.</span></span>
* <span data-ttu-id="e59eb-138">Non è opportuno eseguire un'elaborazione dispendiosa sugli elementi rimossi dalla coda mentre la transazione è attiva per evitare transazioni ad esecuzione prolungata che possono impattare sulle prestazioni del sistema.</span><span class="sxs-lookup"><span data-stu-id="e59eb-138">Expensive processing on the dequeued items should not be performed while the transaction is active, to avoid long-running transactions which may have a performance impact on the system.</span></span>

## <a name="code-snippets"></a><span data-ttu-id="e59eb-139">Frammenti di codice</span><span class="sxs-lookup"><span data-stu-id="e59eb-139">Code Snippets</span></span>
<span data-ttu-id="e59eb-140">Ecco alcuni frammenti di codice e i relativi output previsti.</span><span class="sxs-lookup"><span data-stu-id="e59eb-140">Let us look at a few code snippets and their expected outputs.</span></span> <span data-ttu-id="e59eb-141">La gestione delle eccezioni viene ignorata in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="e59eb-141">Exception handling is ignored in this section.</span></span>

### <a name="enqueueasync"></a><span data-ttu-id="e59eb-142">EnqueueAsync</span><span class="sxs-lookup"><span data-stu-id="e59eb-142">EnqueueAsync</span></span>
<span data-ttu-id="e59eb-143">Ecco alcuni frammenti di codice per l'uso di EnqueueAsync con i relativi output previsti.</span><span class="sxs-lookup"><span data-stu-id="e59eb-143">Here are a few code snippets for using EnqueueAsync followed by their expected outputs.</span></span>

- <span data-ttu-id="e59eb-144">*Caso 1: Singola attività di accodamento*</span><span class="sxs-lookup"><span data-stu-id="e59eb-144">*Case 1: Single Enqueue Task*</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="e59eb-145">Si supponga che l'attività sia stata completata e che non siano presenti transazioni simultanee che modificano la coda.</span><span class="sxs-lookup"><span data-stu-id="e59eb-145">Assume that the task completed successfully, and that there were no concurrent transactions modifying the queue.</span></span> <span data-ttu-id="e59eb-146">L'utente può presupporre che la coda contenga gli elementi in uno dei seguenti ordini:</span><span class="sxs-lookup"><span data-stu-id="e59eb-146">The user can expect the queue to contain the items in any of the following orders:</span></span>

> <span data-ttu-id="e59eb-147">10, 20</span><span class="sxs-lookup"><span data-stu-id="e59eb-147">10, 20</span></span>

> <span data-ttu-id="e59eb-148">20, 10</span><span class="sxs-lookup"><span data-stu-id="e59eb-148">20, 10</span></span>


- <span data-ttu-id="e59eb-149">*Caso 2: Attività di accodamento in parallelo*</span><span class="sxs-lookup"><span data-stu-id="e59eb-149">*Case 2: Parallel Enqueue Task*</span></span>

```
// Parallel Task 1
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}

// Parallel Task 2
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 30, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 40, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="e59eb-150">Si supponga che le attività siano state completate, che siano state eseguite in parallelo e che non sono presenti altre transazioni concorrenti che modificano la coda.</span><span class="sxs-lookup"><span data-stu-id="e59eb-150">Assume that the tasks completed successfully, that the tasks ran in parallel, and that there were no other concurrent transactions modifying the queue.</span></span> <span data-ttu-id="e59eb-151">Non è possibile eseguire alcuna inferenza sull'ordine degli elementi nella coda.</span><span class="sxs-lookup"><span data-stu-id="e59eb-151">No inference can be made about the order of items in the queue.</span></span> <span data-ttu-id="e59eb-152">Per questo frammento di codice, gli elementi possono comparire in uno qualsiasi dei 4</span><span class="sxs-lookup"><span data-stu-id="e59eb-152">For this code snippet, the items may appear in any of the 4!</span></span> <span data-ttu-id="e59eb-153">ordinamenti possibili.</span><span class="sxs-lookup"><span data-stu-id="e59eb-153">possible orderings.</span></span>  <span data-ttu-id="e59eb-154">La coda tenterà di mantenere gli elementi nell'ordine (in coda) originale, ma potrebbe essere necessario eseguire un riordino a causa di operazioni simultanee o errori.</span><span class="sxs-lookup"><span data-stu-id="e59eb-154">The queue will attempt to keep the items in the original (enqueued) order, but may be forced to reorder them due to concurrent operations or faults.</span></span>


### <a name="dequeueasync"></a><span data-ttu-id="e59eb-155">DequeueAsync</span><span class="sxs-lookup"><span data-stu-id="e59eb-155">DequeueAsync</span></span>
<span data-ttu-id="e59eb-156">Ecco alcuni frammenti di codice per l'uso di TryDequeueAsync con i relativi output previsti.</span><span class="sxs-lookup"><span data-stu-id="e59eb-156">Here are a few code snippets for using TryDequeueAsync followed by the expected outputs.</span></span> <span data-ttu-id="e59eb-157">Si supponga che la coda sia già stata popolata con i seguenti elementi nella coda:</span><span class="sxs-lookup"><span data-stu-id="e59eb-157">Assume that the queue is already populated with the following items in the queue:</span></span>
> <span data-ttu-id="e59eb-158">10, 20, 30, 40, 50, 60</span><span class="sxs-lookup"><span data-stu-id="e59eb-158">10, 20, 30, 40, 50, 60</span></span>

- <span data-ttu-id="e59eb-159">*Caso 1: Singola attività di rimozione dalla coda*</span><span class="sxs-lookup"><span data-stu-id="e59eb-159">*Case 1: Single Dequeue Task*</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="e59eb-160">Si supponga che l'attività sia stata completata e che non siano presenti transazioni simultanee che modificano la coda.</span><span class="sxs-lookup"><span data-stu-id="e59eb-160">Assume that the task completed successfully, and that there were no concurrent transactions modifying the queue.</span></span> <span data-ttu-id="e59eb-161">Poiché non è possibile eseguire alcuna inferenza sull'ordine degli elementi nella coda, tutti e tre gli elementi possono essere rimossi dalla coda in qualsiasi ordine.</span><span class="sxs-lookup"><span data-stu-id="e59eb-161">Since no inference can be made about the order of the items in the queue, any three of the items may be dequeued, in any order.</span></span> <span data-ttu-id="e59eb-162">La coda tenterà di mantenere gli elementi nell'ordine (in coda) originale, ma potrebbe essere necessario eseguire un riordino a causa di operazioni simultanee o errori.</span><span class="sxs-lookup"><span data-stu-id="e59eb-162">The queue will attempt to keep the items in the original (enqueued) order, but may be forced to reorder them due to concurrent operations or faults.</span></span>  

- <span data-ttu-id="e59eb-163">*Caso 2: Attività di rimozione dalla coda in parallelo*</span><span class="sxs-lookup"><span data-stu-id="e59eb-163">*Case 2: Parallel Dequeue Task*</span></span>

```
// Parallel Task 1
List<int> dequeue1;
using (var txn = this.StateManager.CreateTransaction())
{
    dequeue1.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;
    dequeue1.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;

    await txn.CommitAsync();
}

// Parallel Task 2
List<int> dequeue2;
using (var txn = this.StateManager.CreateTransaction())
{
    dequeue2.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;
    dequeue2.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;

    await txn.CommitAsync();
}
```

<span data-ttu-id="e59eb-164">Si supponga che le attività siano state completate, che siano state eseguite in parallelo e che non sono presenti altre transazioni concorrenti che modificano la coda.</span><span class="sxs-lookup"><span data-stu-id="e59eb-164">Assume that the tasks completed successfully, that the tasks ran in parallel, and that there were no other concurrent transactions modifying the queue.</span></span> <span data-ttu-id="e59eb-165">Poiché non può essere eseguita alcuna inferenza sull'ordine degli elementi nella coda, gli elenchi *dequeue1* e *dequeue2* conterranno i due elementi in qualsiasi ordine.</span><span class="sxs-lookup"><span data-stu-id="e59eb-165">Since no inference can be made about the order of the items in the queue, the lists *dequeue1* and *dequeue2* will each contain any two items, in any order.</span></span>

<span data-ttu-id="e59eb-166">Lo stesso elemento *non* sarà presente in entrambi gli elenchi.</span><span class="sxs-lookup"><span data-stu-id="e59eb-166">The same item will *not* appear in both lists.</span></span> <span data-ttu-id="e59eb-167">Di conseguenza, se dequeue1 contiene i valori *10*, *30*, dequeue2 conterrà i valori *20* e *40*.</span><span class="sxs-lookup"><span data-stu-id="e59eb-167">Hence, if dequeue1 has *10*, *30*, then dequeue2 would have *20*, *40*.</span></span>

- <span data-ttu-id="e59eb-168">*Caso 3: ordine di rimozione dalla coda con interruzione della transazione*</span><span class="sxs-lookup"><span data-stu-id="e59eb-168">*Case 3: Dequeue Ordering With Transaction Abort*</span></span>

<span data-ttu-id="e59eb-169">L'interruzione di una transazione con rimozioni delle coda in transito riporta gli elementi all'inizio della coda.</span><span class="sxs-lookup"><span data-stu-id="e59eb-169">Aborting a transaction with in-flight dequeues puts the items back on the head of the queue.</span></span> <span data-ttu-id="e59eb-170">L'ordine in cui gli elementi vengono reinseriti all'inizio della coda non è garantito.</span><span class="sxs-lookup"><span data-stu-id="e59eb-170">The order in which the items are put back on the head of the queue is not guaranteed.</span></span> <span data-ttu-id="e59eb-171">Esaminare il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="e59eb-171">Let us look at the following code:</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    // Abort the transaction
    await txn.AbortAsync();
}
```
<span data-ttu-id="e59eb-172">Si supponga che gli elementi siano stati rimossi dalla coda nell'ordine seguente:</span><span class="sxs-lookup"><span data-stu-id="e59eb-172">Assume that the items were dequeued in the following order:</span></span>
> <span data-ttu-id="e59eb-173">10, 20</span><span class="sxs-lookup"><span data-stu-id="e59eb-173">10, 20</span></span>

<span data-ttu-id="e59eb-174">Quando si interrompe la transazione, gli elementi vengono inseriti di nuovo all'inizio della coda in uno dei seguenti ordini:</span><span class="sxs-lookup"><span data-stu-id="e59eb-174">When we abort the transaction, the items would be added back to the head of the queue in any of the following orders:</span></span>
> <span data-ttu-id="e59eb-175">10, 20</span><span class="sxs-lookup"><span data-stu-id="e59eb-175">10, 20</span></span>

> <span data-ttu-id="e59eb-176">20, 10</span><span class="sxs-lookup"><span data-stu-id="e59eb-176">20, 10</span></span>

<span data-ttu-id="e59eb-177">Lo stesso vale per tutti i casi in cui la transazione non è stata *eseguita* correttamente.</span><span class="sxs-lookup"><span data-stu-id="e59eb-177">The same is true for all cases where the transaction was not successfully *Committed*.</span></span>

## <a name="programming-patterns"></a><span data-ttu-id="e59eb-178">Modelli di programmazione</span><span class="sxs-lookup"><span data-stu-id="e59eb-178">Programming Patterns</span></span>
<span data-ttu-id="e59eb-179">In questa sezione verranno esaminati alcuni modelli di programmazione che possono risultare utili usando ReliableConcurrentQueue.</span><span class="sxs-lookup"><span data-stu-id="e59eb-179">In this section, let us look at a few programming patterns that might be helpful in using ReliableConcurrentQueue.</span></span>

### <a name="batch-dequeues"></a><span data-ttu-id="e59eb-180">Rimozioni dalla coda in batch</span><span class="sxs-lookup"><span data-stu-id="e59eb-180">Batch Dequeues</span></span>
<span data-ttu-id="e59eb-181">Un modello di programmazione consigliato per l'attività di tipo consumer è inserire in batch le operazioni di rimozione dalla coda, anziché eseguire una rimozione alla volta.</span><span class="sxs-lookup"><span data-stu-id="e59eb-181">A recommended programming pattern is for the consumer task to batch its dequeues instead of performing one dequeue at a time.</span></span> <span data-ttu-id="e59eb-182">L'utente può scegliere di limitare i ritardi tra ogni batch o la dimensione del batch.</span><span class="sxs-lookup"><span data-stu-id="e59eb-182">The user can choose to throttle delays between every batch or the batch size.</span></span> <span data-ttu-id="e59eb-183">Il frammento di codice seguente illustra questo modello di programmazione.</span><span class="sxs-lookup"><span data-stu-id="e59eb-183">The following code snippet shows this programming model.</span></span>  <span data-ttu-id="e59eb-184">Si noti che in questo esempio l'elaborazione viene eseguita dopo il commit della transazione e pertanto se si verifica un errore durante l'elaborazione, gli elementi non elaborati andranno persi senza essere stati elaborati.</span><span class="sxs-lookup"><span data-stu-id="e59eb-184">Note that in this example, the processing is done after the transaction is committed, so if a fault were to occur while processing, the unprocessed items will be lost without having been processed.</span></span>  <span data-ttu-id="e59eb-185">In alternativa, l'elaborazione può essere eseguita nell'ambito della transazione, ma ciò potrebbe avere un impatto negativo sulle prestazioni e richiede la gestione degli elementi già elaborati.</span><span class="sxs-lookup"><span data-stu-id="e59eb-185">Alternatively, the processing can be done within the transaction's scope, however this may have a negative impact on performance and requires handling of the items already processed.</span></span>

```
int batchSize = 5;
long delayMs = 100;

while(!cancellationToken.IsCancellationRequested)
{
    // Buffer for dequeued items
    List<int> processItems = new List<int>();

    using (var txn = this.StateManager.CreateTransaction())
    {
        ConditionalValue<int> ret;

        for(int i = 0; i < batchSize; ++i)
        {
            ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);

            if (ret.HasValue)
            {
                // If an item was dequeued, add to the buffer for processing
                processItems.Add(ret.Value);
            }
            else
            {
                // else break the for loop
                break;
            }
        }

        await txn.CommitAsync();
    }

    // Process the dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }

    int delayFactor = batchSize - processItems.Count;
    await Task.Delay(TimeSpan.FromMilliseconds(delayMs * delayFactor), cancellationToken);
}
```

### <a name="best-effort-notification-based-processing"></a><span data-ttu-id="e59eb-186">Elaborazione basata su notifica con il migliore sforzo</span><span class="sxs-lookup"><span data-stu-id="e59eb-186">Best-Effort Notification-Based Processing</span></span>
<span data-ttu-id="e59eb-187">Un altro modello di programmazione interessante usa l'API di conteggio.</span><span class="sxs-lookup"><span data-stu-id="e59eb-187">Another interesting programming pattern uses the Count API.</span></span> <span data-ttu-id="e59eb-188">In questo caso è possibile implementare l'elaborazione basata su notifica con il migliore sforzo per la coda.</span><span class="sxs-lookup"><span data-stu-id="e59eb-188">Here, we can implement best-effort notification-based processing for the queue.</span></span> <span data-ttu-id="e59eb-189">Il conteggio della coda consente di limitare un'attività di accodamento o di rimozione dalla coda.</span><span class="sxs-lookup"><span data-stu-id="e59eb-189">The queue Count can be used to throttle an enqueue or a dequeue task.</span></span>  <span data-ttu-id="e59eb-190">Si noti che, come nell'esempio precedente, poiché l'elaborazione si verifica all'esterno della transazione, gli elementi non elaborati potrebbero essere persi in caso di errore durante l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="e59eb-190">Note that as in the previous example, since the processing occurs outside the transaction, unprocessed items may be lost if a fault occurs during processing.</span></span>

```
int threshold = 5;
long delayMs = 1000;

while(!cancellationToken.IsCancellationRequested)
{
    while (this.Queue.Count < threshold)
    {
        cancellationToken.ThrowIfCancellationRequested();

        // If the queue does not have the threshold number of items, delay the task and check again
        await Task.Delay(TimeSpan.FromMilliseconds(delayMs), cancellationToken);
    }

    // If there are approximately threshold number of items, try and process the queue

    // Buffer for dequeued items
    List<int> processItems = new List<int>();

    using (var txn = this.StateManager.CreateTransaction())
    {
        ConditionalValue<int> ret;

        do
        {
            ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);

            if (ret.HasValue)
            {
                // If an item was dequeued, add to the buffer for processing
                processItems.Add(ret.Value);
            }
        } while (processItems.Count < threshold && ret.HasValue);

        await txn.CommitAsync();
    }

    // Process the dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
}
```

### <a name="best-effort-drain"></a><span data-ttu-id="e59eb-191">Svuotamento in base al migliore sforzo</span><span class="sxs-lookup"><span data-stu-id="e59eb-191">Best-Effort Drain</span></span>
<span data-ttu-id="e59eb-192">Lo svuotamento della coda non può essere garantito a causa della natura simultanea della struttura di dati.</span><span class="sxs-lookup"><span data-stu-id="e59eb-192">A drain of the queue cannot be guaranteed due to the concurrent nature of the data structure.</span></span>  <span data-ttu-id="e59eb-193">È possibile che, anche se non è in corso alcuna operazione dell'utente nella coda, una chiamata specifica a TryDequeueAsync possa non restituire un elemento che in precedenza era stato accodato e di cui era stato eseguito il commit.</span><span class="sxs-lookup"><span data-stu-id="e59eb-193">It is possible that, even if no user operations on the queue are in-flight, a particular call to TryDequeueAsync may not return an item which was previously enqueued and committed.</span></span>  <span data-ttu-id="e59eb-194">L'elemento accodato *alla fine* diventerà visibile per la rimozione dalla coda; tuttavia senza un meccanismo di comunicazione fuori banda, un consumer indipendente non può sapere se la coda ha raggiunto uno stato stabile, anche se sono stati arrestati tutti i producer e non sono consentite nuove operazione di accodamento.</span><span class="sxs-lookup"><span data-stu-id="e59eb-194">The enqueued item is guaranteed to *eventually* become visible to dequeue, however without an out-of-band communication mechanism, an independent consumer cannot know that the queue has reached a steady-state even if all producers have been stopped and no new enqueue operations are allowed.</span></span> <span data-ttu-id="e59eb-195">Di conseguenza l'operazione di svuotamento avviene in base al migliore sforzo, come implementato di seguito.</span><span class="sxs-lookup"><span data-stu-id="e59eb-195">Thus, the drain operation is best-effort as implemented below.</span></span>

<span data-ttu-id="e59eb-196">L'utente deve arrestare tutte le successive attività di producer e consumer e attendere il commit o l'interruzione delle transazioni in transito prima di tentare di svuotare la coda.</span><span class="sxs-lookup"><span data-stu-id="e59eb-196">The user should stop all further producer and consumer tasks, and wait for any in-flight transactions to commit or abort, before attempting to drain the queue.</span></span>  <span data-ttu-id="e59eb-197">Se conosce il numero previsto di elementi nella coda, l'utente può impostare una notifica che segnala che tutti gli elementi sono stati rimossi dalla coda.</span><span class="sxs-lookup"><span data-stu-id="e59eb-197">If the user knows the expected number of items in the queue, they can set up a notification which signals that all items have been dequeued.</span></span>

```
int numItemsDequeued;
int batchSize = 5;

ConditionalValue ret;

do
{
    List<int> processItems = new List<int>();

    using (var txn = this.StateManager.CreateTransaction())
    {
        do
        {
            ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);

            if(ret.HasValue)
            {
                // Buffer the dequeues
                processItems.Add(ret.Value);
            }
        } while (ret.HasValue && processItems.Count < batchSize);

        await txn.CommitAsync();
    }

    // Process the dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
} while (ret.HasValue);
```

### <a name="peek"></a><span data-ttu-id="e59eb-198">Visualizzazione</span><span class="sxs-lookup"><span data-stu-id="e59eb-198">Peek</span></span>
<span data-ttu-id="e59eb-199">ReliableConcurrentQueue non fornisce l'API *TryPeekAsync*.</span><span class="sxs-lookup"><span data-stu-id="e59eb-199">ReliableConcurrentQueue does not provide the *TryPeekAsync* api.</span></span> <span data-ttu-id="e59eb-200">Gli utenti possono ottenere la visualizzazione semantica usando *TryDequeueAsync* e quindi interrompendo la transazione.</span><span class="sxs-lookup"><span data-stu-id="e59eb-200">Users can get the peek semantic by using a *TryDequeueAsync* and then aborting the transaction.</span></span> <span data-ttu-id="e59eb-201">In questo esempio le rimozioni dalla coda vengono elaborate solo se il valore dell'elemento è maggiore di *10*.</span><span class="sxs-lookup"><span data-stu-id="e59eb-201">In this example, dequeues are processed only if the item's value is greater than *10*.</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    ConditionalValue ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);
    bool valueProcessed = false;

    if (ret.HasValue)
    {
        if (ret.Value > 10)
        {
            // Process the item
            Console.WriteLine("Value : " + ret.Value);
            valueProcessed = true;
        }
    }

    if (valueProcessed)
    {
        await txn.CommitAsync();    
    }
    else
    {
        await txn.AbortAsync();
    }
}
```

## <a name="must-read"></a><span data-ttu-id="e59eb-202">Da leggere</span><span class="sxs-lookup"><span data-stu-id="e59eb-202">Must Read</span></span>
* [<span data-ttu-id="e59eb-203">Avvio rapido a Reliable Services di Microsoft Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e59eb-203">Reliable Services Quick Start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="e59eb-204">Lavorare con le raccolte Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="e59eb-204">Working with Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="e59eb-205">Notifiche di Reliable Services</span><span class="sxs-lookup"><span data-stu-id="e59eb-205">Reliable Services notifications</span></span>](service-fabric-reliable-services-notifications.md)
* [<span data-ttu-id="e59eb-206">Eseguire il backup e il ripristino di Reliable Services (ripristino di emergenza)</span><span class="sxs-lookup"><span data-stu-id="e59eb-206">Reliable Services Backup and Restore (Disaster Recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="e59eb-207">Reliable State Manager configuration (Configurazione di Reliable State Manager)</span><span class="sxs-lookup"><span data-stu-id="e59eb-207">Reliable State Manager Configuration</span></span>](service-fabric-reliable-services-configuration.md)
* [<span data-ttu-id="e59eb-208">Introduzione ai servizi API Web di Microsoft Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e59eb-208">Getting Started with Service Fabric Web API Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="e59eb-209">Uso avanzato del modello di programmazione Reliable Services</span><span class="sxs-lookup"><span data-stu-id="e59eb-209">Advanced Usage of the Reliable Services Programming Model</span></span>](service-fabric-reliable-services-advanced-usage.md)
* [<span data-ttu-id="e59eb-210">Guida di riferimento per gli sviluppatori per Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="e59eb-210">Developer Reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
