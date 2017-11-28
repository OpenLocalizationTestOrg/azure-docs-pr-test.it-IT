---
title: aaaReliableConcurrentQueue in Azure Service Fabric
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
ms.openlocfilehash: 78a9905996b9ab265c1288d2b49753638d7bc445
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooreliableconcurrentqueue-in-azure-service-fabric"></a><span data-ttu-id="f35ec-103">Introduzione tooReliableConcurrentQueue in Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f35ec-103">Introduction tooReliableConcurrentQueue in Azure Service Fabric</span></span>
<span data-ttu-id="f35ec-104">La coda simultanea affidabile è una coda replicata, transazionale e asincrona che assicura concorrenza elevata per le operazioni di accodamento e rimozione dalla coda.</span><span class="sxs-lookup"><span data-stu-id="f35ec-104">Reliable Concurrent Queue is an asynchronous, transactional, and replicated queue which features high concurrency for enqueue and dequeue operations.</span></span> <span data-ttu-id="f35ec-105">È progettato toodeliver una velocità effettiva elevata e bassa latenza ordinando abbassando hello strict FIFO fornito da [coda affidabile](https://msdn.microsoft.com/library/azure/dn971527.aspx) e fornisce invece un ordinamento di sforzo.</span><span class="sxs-lookup"><span data-stu-id="f35ec-105">It is designed toodeliver high throughput and low latency by relaxing hello strict FIFO ordering provided by [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) and instead provides a best-effort ordering.</span></span>

## <a name="apis"></a><span data-ttu-id="f35ec-106">API</span><span class="sxs-lookup"><span data-stu-id="f35ec-106">APIs</span></span>

|<span data-ttu-id="f35ec-107">Coda simultanea</span><span class="sxs-lookup"><span data-stu-id="f35ec-107">Concurrent Queue</span></span>                |<span data-ttu-id="f35ec-108">Coda simultanea affidabile</span><span class="sxs-lookup"><span data-stu-id="f35ec-108">Reliable Concurrent Queue</span></span>                                         |
|--------------------------------|------------------------------------------------------------------|
| <span data-ttu-id="f35ec-109">void Enqueue(T item)</span><span class="sxs-lookup"><span data-stu-id="f35ec-109">void Enqueue(T item)</span></span>           | <span data-ttu-id="f35ec-110">Task EnqueueAsync(ITransaction tx, T item)</span><span class="sxs-lookup"><span data-stu-id="f35ec-110">Task EnqueueAsync(ITransaction tx, T item)</span></span>                       |
| <span data-ttu-id="f35ec-111">bool TryDequeue(out T result)</span><span class="sxs-lookup"><span data-stu-id="f35ec-111">bool TryDequeue(out T result)</span></span>  | <span data-ttu-id="f35ec-112">Task< ConditionalValue < T > > TryDequeueAsync(ITransaction tx)</span><span class="sxs-lookup"><span data-stu-id="f35ec-112">Task< ConditionalValue < T > > TryDequeueAsync(ITransaction tx)</span></span>  |
| <span data-ttu-id="f35ec-113">int Count()</span><span class="sxs-lookup"><span data-stu-id="f35ec-113">int Count()</span></span>                    | <span data-ttu-id="f35ec-114">long Count()</span><span class="sxs-lookup"><span data-stu-id="f35ec-114">long Count()</span></span>                                                     |

## <a name="comparison-with-reliable-queuehttpsmsdnmicrosoftcomlibraryazuredn971527aspx"></a><span data-ttu-id="f35ec-115">Confronto con la [coda affidabile](https://msdn.microsoft.com/library/azure/dn971527.aspx)</span><span class="sxs-lookup"><span data-stu-id="f35ec-115">Comparison with [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx)</span></span>

<span data-ttu-id="f35ec-116">Coda simultanea affidabile è disponibile un'alternativa troppo[coda affidabile](https://msdn.microsoft.com/library/azure/dn971527.aspx).</span><span class="sxs-lookup"><span data-stu-id="f35ec-116">Reliable Concurrent Queue is offered as an alternative too[Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx).</span></span> <span data-ttu-id="f35ec-117">Deve essere usata nei casi in cui non è necessario l'ordine FIFO in modo vincolante poiché l'ordine FIFO richiede un compromesso in termini di concorrenza.</span><span class="sxs-lookup"><span data-stu-id="f35ec-117">It should be used in cases where strict FIFO ordering is not required, as guaranteeing FIFO requires a tradeoff with concurrency.</span></span>  <span data-ttu-id="f35ec-118">[Coda affidabile](https://msdn.microsoft.com/library/azure/dn971527.aspx) utilizza blocchi tooenforce FIFO ordinamento con tooenqueue consentiti al massimo una transazione e la maggior parte di una transazione consentita toodequeue alla volta.</span><span class="sxs-lookup"><span data-stu-id="f35ec-118">[Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) uses locks tooenforce FIFO ordering, with at most one transaction allowed tooenqueue and at most one transaction allowed toodequeue at a time.</span></span> <span data-ttu-id="f35ec-119">In confronto, affidabile simultanee nella coda vengono ridotti i hello ordinamento vincolo e consente a qualsiasi numero toointerleave transazioni simultanee loro enqueue e operazioni di rimozione dalla coda.</span><span class="sxs-lookup"><span data-stu-id="f35ec-119">In comparison, Reliable Concurrent Queue relaxes hello ordering constraint and allows any number concurrent transactions toointerleave their enqueue and dequeue operations.</span></span> <span data-ttu-id="f35ec-120">L'ordine sforzo è fornito, tuttavia, hello ordinamento relativo di due valori in una coda simultanea affidabile può mai essere garantita.</span><span class="sxs-lookup"><span data-stu-id="f35ec-120">Best-effort ordering is provided, however hello relative ordering of two values in a Reliable Concurrent Queue can never be guaranteed.</span></span>

<span data-ttu-id="f35ec-121">La coda simultanea affidabile garantisce maggiore velocità effettiva e latenza ridotta rispetto alla [coda affidabile](https://msdn.microsoft.com/library/azure/dn971527.aspx) ogni volta che sono presenti più transazioni simultanee che eseguono operazioni di accodamento e/o rimozione dalla coda.</span><span class="sxs-lookup"><span data-stu-id="f35ec-121">Reliable Concurrent Queue provides higher throughput and lower latency than [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) whenever there are multiple concurrent transactions performing enqueues and/or dequeues.</span></span>

<span data-ttu-id="f35ec-122">Un esempio di caso d'uso per hello ReliableConcurrentQueue è hello [Message Queue](https://en.wikipedia.org/wiki/Message_queue) scenario.</span><span class="sxs-lookup"><span data-stu-id="f35ec-122">A sample use case for hello ReliableConcurrentQueue is hello [Message Queue](https://en.wikipedia.org/wiki/Message_queue) scenario.</span></span> <span data-ttu-id="f35ec-123">In questo scenario, uno o più produttori messaggio creare e aggiungere elementi toohello coda e il pull dei messaggi dalla coda di hello di uno o più consumer di messaggi e li elaborano.</span><span class="sxs-lookup"><span data-stu-id="f35ec-123">In this scenario, one or more message producers create and add items toohello queue, and one or more message consumers pull messages from hello queue and process them.</span></span> <span data-ttu-id="f35ec-124">Più producer e consumer può lavorare in modo indipendente, utilizzando le transazioni simultanee nella coda di hello tooprocess ordine.</span><span class="sxs-lookup"><span data-stu-id="f35ec-124">Multiple producers and consumers can work independently, using concurrent transactions in order tooprocess hello queue.</span></span>

## <a name="usage-guidelines"></a><span data-ttu-id="f35ec-125">Linee guida per l'uso</span><span class="sxs-lookup"><span data-stu-id="f35ec-125">Usage Guidelines</span></span>
* <span data-ttu-id="f35ec-126">coda Hello prevede che gli elementi di hello in coda hello hanno un periodo di memorizzazione bassa.</span><span class="sxs-lookup"><span data-stu-id="f35ec-126">hello queue expects that hello items in hello queue have a low retention period.</span></span> <span data-ttu-id="f35ec-127">Ovvero elementi hello sarebbero non rimanere nella coda di hello per molto tempo.</span><span class="sxs-lookup"><span data-stu-id="f35ec-127">That is, hello items would not stay in hello queue for a long time.</span></span>
* <span data-ttu-id="f35ec-128">coda di Hello non garantisce l'ordine FIFO strict.</span><span class="sxs-lookup"><span data-stu-id="f35ec-128">hello queue does not guarantee strict FIFO ordering.</span></span>
* <span data-ttu-id="f35ec-129">coda di Hello non legge il proprio scritture.</span><span class="sxs-lookup"><span data-stu-id="f35ec-129">hello queue does not read its own writes.</span></span> <span data-ttu-id="f35ec-130">Se un elemento viene accodato all'interno di una transazione, non sarà visibile tooa dequeuer all'interno di hello stessa transazione.</span><span class="sxs-lookup"><span data-stu-id="f35ec-130">If an item is enqueued within a transaction, it will not be visible tooa dequeuer within hello same transaction.</span></span>
* <span data-ttu-id="f35ec-131">Le rimozioni dalla coda non sono isolate tra loro.</span><span class="sxs-lookup"><span data-stu-id="f35ec-131">Dequeues are not isolated from each other.</span></span> <span data-ttu-id="f35ec-132">Se l'elemento *A* viene rimosso dalla coda nella transazione *txnA*, anche se *txnA* non viene eseguito, elemento *A* non sarà visibile tooa simultanee transazione *txnB*.</span><span class="sxs-lookup"><span data-stu-id="f35ec-132">If item *A* is dequeued in transaction *txnA*, even though *txnA* is not committed, item *A* would not be visible tooa concurrent transaction *txnB*.</span></span>  <span data-ttu-id="f35ec-133">Se *txnA* , interrompe *A* diventerà visibile troppo*txnB* immediatamente.</span><span class="sxs-lookup"><span data-stu-id="f35ec-133">If *txnA* aborts, *A* will become visible too*txnB* immediately.</span></span>
* <span data-ttu-id="f35ec-134">*TryPeekAsync* comportamento può essere implementato usando un *TryDequeueAsync* e quindi l'interruzione delle transazioni hello.</span><span class="sxs-lookup"><span data-stu-id="f35ec-134">*TryPeekAsync* behavior can be implemented by using a *TryDequeueAsync* and then aborting hello transaction.</span></span> <span data-ttu-id="f35ec-135">Un esempio è reperibile nella sezione modelli di programmazione hello.</span><span class="sxs-lookup"><span data-stu-id="f35ec-135">An example of this can be found in hello Programming Patterns section.</span></span>
* <span data-ttu-id="f35ec-136">Il conteggio non è transazionale.</span><span class="sxs-lookup"><span data-stu-id="f35ec-136">Count is non-transactional.</span></span> <span data-ttu-id="f35ec-137">Può essere utilizzato tooget un'idea del numero di hello di elementi nella coda di hello, ma rappresenta un punto nel tempo e non può essere ritenuto affidabile.</span><span class="sxs-lookup"><span data-stu-id="f35ec-137">It can be used tooget an idea of hello number of elements in hello queue, but represents a point-in-time and cannot be relied upon.</span></span>
* <span data-ttu-id="f35ec-138">L'elaborazione in hello costosa elementi rimossi dalla coda non devono essere eseguiti mentre hello transazione è attiva, tooavoid transazioni a esecuzione prolungata che potrebbero avere un impatto sulle prestazioni nel sistema hello.</span><span class="sxs-lookup"><span data-stu-id="f35ec-138">Expensive processing on hello dequeued items should not be performed while hello transaction is active, tooavoid long-running transactions which may have a performance impact on hello system.</span></span>

## <a name="code-snippets"></a><span data-ttu-id="f35ec-139">Frammenti di codice</span><span class="sxs-lookup"><span data-stu-id="f35ec-139">Code Snippets</span></span>
<span data-ttu-id="f35ec-140">Ecco alcuni frammenti di codice e i relativi output previsti.</span><span class="sxs-lookup"><span data-stu-id="f35ec-140">Let us look at a few code snippets and their expected outputs.</span></span> <span data-ttu-id="f35ec-141">La gestione delle eccezioni viene ignorata in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="f35ec-141">Exception handling is ignored in this section.</span></span>

### <a name="enqueueasync"></a><span data-ttu-id="f35ec-142">EnqueueAsync</span><span class="sxs-lookup"><span data-stu-id="f35ec-142">EnqueueAsync</span></span>
<span data-ttu-id="f35ec-143">Ecco alcuni frammenti di codice per l'uso di EnqueueAsync con i relativi output previsti.</span><span class="sxs-lookup"><span data-stu-id="f35ec-143">Here are a few code snippets for using EnqueueAsync followed by their expected outputs.</span></span>

- <span data-ttu-id="f35ec-144">*Caso 1: Singola attività di accodamento*</span><span class="sxs-lookup"><span data-stu-id="f35ec-144">*Case 1: Single Enqueue Task*</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="f35ec-145">Si supponga che l'attività hello completata correttamente e che non esistevano Nessuna transazione simultanea Modifica coda hello.</span><span class="sxs-lookup"><span data-stu-id="f35ec-145">Assume that hello task completed successfully, and that there were no concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="f35ec-146">Hello utente potrà quindi aspettarsi elementi hello toocontain della coda di hello in uno dei seguenti ordini hello:</span><span class="sxs-lookup"><span data-stu-id="f35ec-146">hello user can expect hello queue toocontain hello items in any of hello following orders:</span></span>

> <span data-ttu-id="f35ec-147">10, 20</span><span class="sxs-lookup"><span data-stu-id="f35ec-147">10, 20</span></span>

> <span data-ttu-id="f35ec-148">20, 10</span><span class="sxs-lookup"><span data-stu-id="f35ec-148">20, 10</span></span>


- <span data-ttu-id="f35ec-149">*Caso 2: Attività di accodamento in parallelo*</span><span class="sxs-lookup"><span data-stu-id="f35ec-149">*Case 2: Parallel Enqueue Task*</span></span>

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

<span data-ttu-id="f35ec-150">Si supponga che le attività di hello completato, che l'attività hello vengano eseguiti in parallelo e che si sono verificati non altre transazioni simultanee Modifica coda hello.</span><span class="sxs-lookup"><span data-stu-id="f35ec-150">Assume that hello tasks completed successfully, that hello tasks ran in parallel, and that there were no other concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="f35ec-151">È non possibile eseguire alcuna inferenza sull'ordine di hello di elementi nella coda di hello.</span><span class="sxs-lookup"><span data-stu-id="f35ec-151">No inference can be made about hello order of items in hello queue.</span></span> <span data-ttu-id="f35ec-152">Per questo frammento di codice, gli elementi di hello vengano visualizzati in uno dei 4 hello!</span><span class="sxs-lookup"><span data-stu-id="f35ec-152">For this code snippet, hello items may appear in any of hello 4!</span></span> <span data-ttu-id="f35ec-153">ordinamenti possibili.</span><span class="sxs-lookup"><span data-stu-id="f35ec-153">possible orderings.</span></span>  <span data-ttu-id="f35ec-154">coda Hello tenterà elementi hello tookeep in ordine di hello originale (accodato), ma può essere forzato tooreorder loro scadenza tooconcurrent operazioni o errori.</span><span class="sxs-lookup"><span data-stu-id="f35ec-154">hello queue will attempt tookeep hello items in hello original (enqueued) order, but may be forced tooreorder them due tooconcurrent operations or faults.</span></span>


### <a name="dequeueasync"></a><span data-ttu-id="f35ec-155">DequeueAsync</span><span class="sxs-lookup"><span data-stu-id="f35ec-155">DequeueAsync</span></span>
<span data-ttu-id="f35ec-156">Ecco alcuni frammenti di codice per l'utilizzo di TryDequeueAsync seguito dall'output di hello previsto.</span><span class="sxs-lookup"><span data-stu-id="f35ec-156">Here are a few code snippets for using TryDequeueAsync followed by hello expected outputs.</span></span> <span data-ttu-id="f35ec-157">Si supponga di che tale coda hello è già popolato con i seguenti elementi nella coda di hello hello:</span><span class="sxs-lookup"><span data-stu-id="f35ec-157">Assume that hello queue is already populated with hello following items in hello queue:</span></span>
> <span data-ttu-id="f35ec-158">10, 20, 30, 40, 50, 60</span><span class="sxs-lookup"><span data-stu-id="f35ec-158">10, 20, 30, 40, 50, 60</span></span>

- <span data-ttu-id="f35ec-159">*Caso 1: Singola attività di rimozione dalla coda*</span><span class="sxs-lookup"><span data-stu-id="f35ec-159">*Case 1: Single Dequeue Task*</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="f35ec-160">Si supponga che l'attività hello completata correttamente e che non esistevano Nessuna transazione simultanea Modifica coda hello.</span><span class="sxs-lookup"><span data-stu-id="f35ec-160">Assume that hello task completed successfully, and that there were no concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="f35ec-161">Poiché è non possibile eseguire alcuna inferenza sull'ordine di hello di elementi di hello nella coda di hello, tutti e tre elementi hello potrebbe da rimuovere dalla coda, in qualsiasi ordine.</span><span class="sxs-lookup"><span data-stu-id="f35ec-161">Since no inference can be made about hello order of hello items in hello queue, any three of hello items may be dequeued, in any order.</span></span> <span data-ttu-id="f35ec-162">coda Hello tenterà elementi hello tookeep in ordine di hello originale (accodato), ma può essere forzato tooreorder loro scadenza tooconcurrent operazioni o errori.</span><span class="sxs-lookup"><span data-stu-id="f35ec-162">hello queue will attempt tookeep hello items in hello original (enqueued) order, but may be forced tooreorder them due tooconcurrent operations or faults.</span></span>  

- <span data-ttu-id="f35ec-163">*Caso 2: Attività di rimozione dalla coda in parallelo*</span><span class="sxs-lookup"><span data-stu-id="f35ec-163">*Case 2: Parallel Dequeue Task*</span></span>

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

<span data-ttu-id="f35ec-164">Si supponga che le attività di hello completato, che l'attività hello vengano eseguiti in parallelo e che si sono verificati non altre transazioni simultanee Modifica coda hello.</span><span class="sxs-lookup"><span data-stu-id="f35ec-164">Assume that hello tasks completed successfully, that hello tasks ran in parallel, and that there were no other concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="f35ec-165">Poiché nessun inferenza può essere effettuata sull'ordine di hello di elementi di hello nella coda di hello hello elenchi *dequeue1* e *dequeue2* conterrà ogni due elementi, in qualsiasi ordine.</span><span class="sxs-lookup"><span data-stu-id="f35ec-165">Since no inference can be made about hello order of hello items in hello queue, hello lists *dequeue1* and *dequeue2* will each contain any two items, in any order.</span></span>

<span data-ttu-id="f35ec-166">lo stesso elemento verrà Hello *non* entrambi gli elenchi.</span><span class="sxs-lookup"><span data-stu-id="f35ec-166">hello same item will *not* appear in both lists.</span></span> <span data-ttu-id="f35ec-167">Di conseguenza, se dequeue1 contiene i valori *10*, *30*, dequeue2 conterrà i valori *20* e *40*.</span><span class="sxs-lookup"><span data-stu-id="f35ec-167">Hence, if dequeue1 has *10*, *30*, then dequeue2 would have *20*, *40*.</span></span>

- <span data-ttu-id="f35ec-168">*Caso 3: ordine di rimozione dalla coda con interruzione della transazione*</span><span class="sxs-lookup"><span data-stu-id="f35ec-168">*Case 3: Dequeue Ordering With Transaction Abort*</span></span>

<span data-ttu-id="f35ec-169">L'interruzione di una transazione con in transito rimuove dalla coda riporta elementi hello sul vertice hello della coda di hello.</span><span class="sxs-lookup"><span data-stu-id="f35ec-169">Aborting a transaction with in-flight dequeues puts hello items back on hello head of hello queue.</span></span> <span data-ttu-id="f35ec-170">ordine di Hello in cui gli elementi di hello vengano rimessi sul vertice hello della coda di hello non è garantito.</span><span class="sxs-lookup"><span data-stu-id="f35ec-170">hello order in which hello items are put back on hello head of hello queue is not guaranteed.</span></span> <span data-ttu-id="f35ec-171">Esaminiamo hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="f35ec-171">Let us look at hello following code:</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    // Abort hello transaction
    await txn.AbortAsync();
}
```
<span data-ttu-id="f35ec-172">Si supponga che sono stati rimossi dalla coda di elementi hello in hello seguente ordine:</span><span class="sxs-lookup"><span data-stu-id="f35ec-172">Assume that hello items were dequeued in hello following order:</span></span>
> <span data-ttu-id="f35ec-173">10, 20</span><span class="sxs-lookup"><span data-stu-id="f35ec-173">10, 20</span></span>

<span data-ttu-id="f35ec-174">Quando si interrotta la transazione hello, hello sarebbe possibile aggiungere elementi head toohello posteriore della coda di hello in uno dei seguenti ordini hello:</span><span class="sxs-lookup"><span data-stu-id="f35ec-174">When we abort hello transaction, hello items would be added back toohello head of hello queue in any of hello following orders:</span></span>
> <span data-ttu-id="f35ec-175">10, 20</span><span class="sxs-lookup"><span data-stu-id="f35ec-175">10, 20</span></span>

> <span data-ttu-id="f35ec-176">20, 10</span><span class="sxs-lookup"><span data-stu-id="f35ec-176">20, 10</span></span>

<span data-ttu-id="f35ec-177">Hello lo stesso vale per tutti i casi in cui la transazione hello non è stato *eseguito*.</span><span class="sxs-lookup"><span data-stu-id="f35ec-177">hello same is true for all cases where hello transaction was not successfully *Committed*.</span></span>

## <a name="programming-patterns"></a><span data-ttu-id="f35ec-178">Modelli di programmazione</span><span class="sxs-lookup"><span data-stu-id="f35ec-178">Programming Patterns</span></span>
<span data-ttu-id="f35ec-179">In questa sezione verranno esaminati alcuni modelli di programmazione che possono risultare utili usando ReliableConcurrentQueue.</span><span class="sxs-lookup"><span data-stu-id="f35ec-179">In this section, let us look at a few programming patterns that might be helpful in using ReliableConcurrentQueue.</span></span>

### <a name="batch-dequeues"></a><span data-ttu-id="f35ec-180">Rimozioni dalla coda in batch</span><span class="sxs-lookup"><span data-stu-id="f35ec-180">Batch Dequeues</span></span>
<span data-ttu-id="f35ec-181">Consigliato di un modello di programmazione sia per hello consumer attività toobatch la rimuove dalla coda anziché eseguire una rimozione dalla coda contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="f35ec-181">A recommended programming pattern is for hello consumer task toobatch its dequeues instead of performing one dequeue at a time.</span></span> <span data-ttu-id="f35ec-182">utente di Hello può scegliere toothrottle ritardi tra le dimensioni del batch ogni batch o hello.</span><span class="sxs-lookup"><span data-stu-id="f35ec-182">hello user can choose toothrottle delays between every batch or hello batch size.</span></span> <span data-ttu-id="f35ec-183">Hello frammento di codice seguente viene illustrato questo modello di programmazione.</span><span class="sxs-lookup"><span data-stu-id="f35ec-183">hello following code snippet shows this programming model.</span></span>  <span data-ttu-id="f35ec-184">Si noti che in questo esempio, l'elaborazione di hello viene eseguita dopo il commit della transazione hello in modo se un errore toooccur durante l'elaborazione, hello elementi non elaborati andranno persi senza essere stato trasformato.</span><span class="sxs-lookup"><span data-stu-id="f35ec-184">Note that in this example, hello processing is done after hello transaction is committed, so if a fault were toooccur while processing, hello unprocessed items will be lost without having been processed.</span></span>  <span data-ttu-id="f35ec-185">In alternativa, è possibile eseguire l'elaborazione di hello nell'ambito della transazione hello, tuttavia questo può avere un impatto negativo sulle prestazioni e richiede una gestione degli elementi di hello già elaborato.</span><span class="sxs-lookup"><span data-stu-id="f35ec-185">Alternatively, hello processing can be done within hello transaction's scope, however this may have a negative impact on performance and requires handling of hello items already processed.</span></span>

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
                // If an item was dequeued, add toohello buffer for processing
                processItems.Add(ret.Value);
            }
            else
            {
                // else break hello for loop
                break;
            }
        }

        await txn.CommitAsync();
    }

    // Process hello dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }

    int delayFactor = batchSize - processItems.Count;
    await Task.Delay(TimeSpan.FromMilliseconds(delayMs * delayFactor), cancellationToken);
}
```

### <a name="best-effort-notification-based-processing"></a><span data-ttu-id="f35ec-186">Elaborazione basata su notifica con il migliore sforzo</span><span class="sxs-lookup"><span data-stu-id="f35ec-186">Best-Effort Notification-Based Processing</span></span>
<span data-ttu-id="f35ec-187">Un altro modello di programmazione interessano utilizza hello conteggio API.</span><span class="sxs-lookup"><span data-stu-id="f35ec-187">Another interesting programming pattern uses hello Count API.</span></span> <span data-ttu-id="f35ec-188">In questo caso, è possibile implementare l'elaborazione sforzo basato sulla notifica per la coda di hello.</span><span class="sxs-lookup"><span data-stu-id="f35ec-188">Here, we can implement best-effort notification-based processing for hello queue.</span></span> <span data-ttu-id="f35ec-189">coda di Hello conteggio può essere utilizzato toothrottle un accodamento o un'attività di rimozione dalla coda.</span><span class="sxs-lookup"><span data-stu-id="f35ec-189">hello queue Count can be used toothrottle an enqueue or a dequeue task.</span></span>  <span data-ttu-id="f35ec-190">Si noti che nell'esempio precedente hello, poiché l'elaborazione di hello avviene all'esterno della transazione hello, gli elementi non elaborati potrebbero essere persi se si verifica un errore durante l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="f35ec-190">Note that as in hello previous example, since hello processing occurs outside hello transaction, unprocessed items may be lost if a fault occurs during processing.</span></span>

```
int threshold = 5;
long delayMs = 1000;

while(!cancellationToken.IsCancellationRequested)
{
    while (this.Queue.Count < threshold)
    {
        cancellationToken.ThrowIfCancellationRequested();

        // If hello queue does not have hello threshold number of items, delay hello task and check again
        await Task.Delay(TimeSpan.FromMilliseconds(delayMs), cancellationToken);
    }

    // If there are approximately threshold number of items, try and process hello queue

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
                // If an item was dequeued, add toohello buffer for processing
                processItems.Add(ret.Value);
            }
        } while (processItems.Count < threshold && ret.HasValue);

        await txn.CommitAsync();
    }

    // Process hello dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
}
```

### <a name="best-effort-drain"></a><span data-ttu-id="f35ec-191">Svuotamento in base al migliore sforzo</span><span class="sxs-lookup"><span data-stu-id="f35ec-191">Best-Effort Drain</span></span>
<span data-ttu-id="f35ec-192">Lo svuotamento della coda di hello non può essere garantito scadenza toohello natura simultanee hello della struttura di dati.</span><span class="sxs-lookup"><span data-stu-id="f35ec-192">A drain of hello queue cannot be guaranteed due toohello concurrent nature of hello data structure.</span></span>  <span data-ttu-id="f35ec-193">È possibile che, anche se nessuna operazione utente sulla coda hello sono in transito, tooTryDequeueAsync una determinata chiamata non può restituire un elemento che in precedenza era accodati e il commit.</span><span class="sxs-lookup"><span data-stu-id="f35ec-193">It is possible that, even if no user operations on hello queue are in-flight, a particular call tooTryDequeueAsync may not return an item which was previously enqueued and committed.</span></span>  <span data-ttu-id="f35ec-194">elemento accodato Hello è garantita troppo*infine* diventano visibili toodequeue, ma senza un meccanismo di comunicazione fuori banda, un consumer indipendente non è in grado di tale coda hello ha raggiunto un stato stabile anche se tutti i sono stati interrotti i producer e alcuna nuova operazione di accodamento non sono consentite.</span><span class="sxs-lookup"><span data-stu-id="f35ec-194">hello enqueued item is guaranteed too*eventually* become visible toodequeue, however without an out-of-band communication mechanism, an independent consumer cannot know that hello queue has reached a steady-state even if all producers have been stopped and no new enqueue operations are allowed.</span></span> <span data-ttu-id="f35ec-195">Operazione di svuotamento hello è pertanto sforzo come implementati sotto.</span><span class="sxs-lookup"><span data-stu-id="f35ec-195">Thus, hello drain operation is best-effort as implemented below.</span></span>

<span data-ttu-id="f35ec-196">utente Hello deve arrestare tutte le successive producer e attività del consumer e attendere qualsiasi toocommit le transazioni in transito o di interruzione, prima di tentare di coda hello toodrain.</span><span class="sxs-lookup"><span data-stu-id="f35ec-196">hello user should stop all further producer and consumer tasks, and wait for any in-flight transactions toocommit or abort, before attempting toodrain hello queue.</span></span>  <span data-ttu-id="f35ec-197">Se l'utente hello conosce il numero di hello previsto di elementi nella coda di hello, è possibile impostare una notifica che segnala che sono stati rimossi dalla coda di tutti gli elementi.</span><span class="sxs-lookup"><span data-stu-id="f35ec-197">If hello user knows hello expected number of items in hello queue, they can set up a notification which signals that all items have been dequeued.</span></span>

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
                // Buffer hello dequeues
                processItems.Add(ret.Value);
            }
        } while (ret.HasValue && processItems.Count < batchSize);

        await txn.CommitAsync();
    }

    // Process hello dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
} while (ret.HasValue);
```

### <a name="peek"></a><span data-ttu-id="f35ec-198">Visualizzazione</span><span class="sxs-lookup"><span data-stu-id="f35ec-198">Peek</span></span>
<span data-ttu-id="f35ec-199">ReliableConcurrentQueue non fornisce hello *TryPeekAsync* api.</span><span class="sxs-lookup"><span data-stu-id="f35ec-199">ReliableConcurrentQueue does not provide hello *TryPeekAsync* api.</span></span> <span data-ttu-id="f35ec-200">Gli utenti possono ottenere peek hello semantica utilizzando un *TryDequeueAsync* e quindi l'interruzione delle transazioni hello.</span><span class="sxs-lookup"><span data-stu-id="f35ec-200">Users can get hello peek semantic by using a *TryDequeueAsync* and then aborting hello transaction.</span></span> <span data-ttu-id="f35ec-201">In questo esempio rimuove dalla coda vengono elaborati solo se è maggiore del valore dell'elemento hello *10*.</span><span class="sxs-lookup"><span data-stu-id="f35ec-201">In this example, dequeues are processed only if hello item's value is greater than *10*.</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    ConditionalValue ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);
    bool valueProcessed = false;

    if (ret.HasValue)
    {
        if (ret.Value > 10)
        {
            // Process hello item
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

## <a name="must-read"></a><span data-ttu-id="f35ec-202">Da leggere</span><span class="sxs-lookup"><span data-stu-id="f35ec-202">Must Read</span></span>
* [<span data-ttu-id="f35ec-203">Avvio rapido a Reliable Services di Microsoft Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f35ec-203">Reliable Services Quick Start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="f35ec-204">Lavorare con le raccolte Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="f35ec-204">Working with Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="f35ec-205">Notifiche di Reliable Services</span><span class="sxs-lookup"><span data-stu-id="f35ec-205">Reliable Services notifications</span></span>](service-fabric-reliable-services-notifications.md)
* [<span data-ttu-id="f35ec-206">Eseguire il backup e il ripristino di Reliable Services (ripristino di emergenza)</span><span class="sxs-lookup"><span data-stu-id="f35ec-206">Reliable Services Backup and Restore (Disaster Recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="f35ec-207">Reliable State Manager configuration (Configurazione di Reliable State Manager)</span><span class="sxs-lookup"><span data-stu-id="f35ec-207">Reliable State Manager Configuration</span></span>](service-fabric-reliable-services-configuration.md)
* [<span data-ttu-id="f35ec-208">Introduzione ai servizi API Web di Microsoft Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f35ec-208">Getting Started with Service Fabric Web API Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="f35ec-209">Utilizzo avanzato di hello modello di programmazione di servizi affidabili</span><span class="sxs-lookup"><span data-stu-id="f35ec-209">Advanced Usage of hello Reliable Services Programming Model</span></span>](service-fabric-reliable-services-advanced-usage.md)
* [<span data-ttu-id="f35ec-210">Guida di riferimento per gli sviluppatori per Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="f35ec-210">Developer Reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
