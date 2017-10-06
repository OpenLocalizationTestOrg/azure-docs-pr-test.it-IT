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
# <a name="introduction-tooreliableconcurrentqueue-in-azure-service-fabric"></a>Introduzione tooReliableConcurrentQueue in Azure Service Fabric
La coda simultanea affidabile è una coda replicata, transazionale e asincrona che assicura concorrenza elevata per le operazioni di accodamento e rimozione dalla coda. È progettato toodeliver una velocità effettiva elevata e bassa latenza ordinando abbassando hello strict FIFO fornito da [coda affidabile](https://msdn.microsoft.com/library/azure/dn971527.aspx) e fornisce invece un ordinamento di sforzo.

## <a name="apis"></a>API

|Coda simultanea                |Coda simultanea affidabile                                         |
|--------------------------------|------------------------------------------------------------------|
| void Enqueue(T item)           | Task EnqueueAsync(ITransaction tx, T item)                       |
| bool TryDequeue(out T result)  | Task< ConditionalValue < T > > TryDequeueAsync(ITransaction tx)  |
| int Count()                    | long Count()                                                     |

## <a name="comparison-with-reliable-queuehttpsmsdnmicrosoftcomlibraryazuredn971527aspx"></a>Confronto con la [coda affidabile](https://msdn.microsoft.com/library/azure/dn971527.aspx)

Coda simultanea affidabile è disponibile un'alternativa troppo[coda affidabile](https://msdn.microsoft.com/library/azure/dn971527.aspx). Deve essere usata nei casi in cui non è necessario l'ordine FIFO in modo vincolante poiché l'ordine FIFO richiede un compromesso in termini di concorrenza.  [Coda affidabile](https://msdn.microsoft.com/library/azure/dn971527.aspx) utilizza blocchi tooenforce FIFO ordinamento con tooenqueue consentiti al massimo una transazione e la maggior parte di una transazione consentita toodequeue alla volta. In confronto, affidabile simultanee nella coda vengono ridotti i hello ordinamento vincolo e consente a qualsiasi numero toointerleave transazioni simultanee loro enqueue e operazioni di rimozione dalla coda. L'ordine sforzo è fornito, tuttavia, hello ordinamento relativo di due valori in una coda simultanea affidabile può mai essere garantita.

La coda simultanea affidabile garantisce maggiore velocità effettiva e latenza ridotta rispetto alla [coda affidabile](https://msdn.microsoft.com/library/azure/dn971527.aspx) ogni volta che sono presenti più transazioni simultanee che eseguono operazioni di accodamento e/o rimozione dalla coda.

Un esempio di caso d'uso per hello ReliableConcurrentQueue è hello [Message Queue](https://en.wikipedia.org/wiki/Message_queue) scenario. In questo scenario, uno o più produttori messaggio creare e aggiungere elementi toohello coda e il pull dei messaggi dalla coda di hello di uno o più consumer di messaggi e li elaborano. Più producer e consumer può lavorare in modo indipendente, utilizzando le transazioni simultanee nella coda di hello tooprocess ordine.

## <a name="usage-guidelines"></a>Linee guida per l'uso
* coda Hello prevede che gli elementi di hello in coda hello hanno un periodo di memorizzazione bassa. Ovvero elementi hello sarebbero non rimanere nella coda di hello per molto tempo.
* coda di Hello non garantisce l'ordine FIFO strict.
* coda di Hello non legge il proprio scritture. Se un elemento viene accodato all'interno di una transazione, non sarà visibile tooa dequeuer all'interno di hello stessa transazione.
* Le rimozioni dalla coda non sono isolate tra loro. Se l'elemento *A* viene rimosso dalla coda nella transazione *txnA*, anche se *txnA* non viene eseguito, elemento *A* non sarà visibile tooa simultanee transazione *txnB*.  Se *txnA* , interrompe *A* diventerà visibile troppo*txnB* immediatamente.
* *TryPeekAsync* comportamento può essere implementato usando un *TryDequeueAsync* e quindi l'interruzione delle transazioni hello. Un esempio è reperibile nella sezione modelli di programmazione hello.
* Il conteggio non è transazionale. Può essere utilizzato tooget un'idea del numero di hello di elementi nella coda di hello, ma rappresenta un punto nel tempo e non può essere ritenuto affidabile.
* L'elaborazione in hello costosa elementi rimossi dalla coda non devono essere eseguiti mentre hello transazione è attiva, tooavoid transazioni a esecuzione prolungata che potrebbero avere un impatto sulle prestazioni nel sistema hello.

## <a name="code-snippets"></a>Frammenti di codice
Ecco alcuni frammenti di codice e i relativi output previsti. La gestione delle eccezioni viene ignorata in questa sezione.

### <a name="enqueueasync"></a>EnqueueAsync
Ecco alcuni frammenti di codice per l'uso di EnqueueAsync con i relativi output previsti.

- *Caso 1: Singola attività di accodamento*

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}
```

Si supponga che l'attività hello completata correttamente e che non esistevano Nessuna transazione simultanea Modifica coda hello. Hello utente potrà quindi aspettarsi elementi hello toocontain della coda di hello in uno dei seguenti ordini hello:

> 10, 20

> 20, 10


- *Caso 2: Attività di accodamento in parallelo*

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

Si supponga che le attività di hello completato, che l'attività hello vengano eseguiti in parallelo e che si sono verificati non altre transazioni simultanee Modifica coda hello. È non possibile eseguire alcuna inferenza sull'ordine di hello di elementi nella coda di hello. Per questo frammento di codice, gli elementi di hello vengano visualizzati in uno dei 4 hello! ordinamenti possibili.  coda Hello tenterà elementi hello tookeep in ordine di hello originale (accodato), ma può essere forzato tooreorder loro scadenza tooconcurrent operazioni o errori.


### <a name="dequeueasync"></a>DequeueAsync
Ecco alcuni frammenti di codice per l'utilizzo di TryDequeueAsync seguito dall'output di hello previsto. Si supponga di che tale coda hello è già popolato con i seguenti elementi nella coda di hello hello:
> 10, 20, 30, 40, 50, 60

- *Caso 1: Singola attività di rimozione dalla coda*

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    await txn.CommitAsync();
}
```

Si supponga che l'attività hello completata correttamente e che non esistevano Nessuna transazione simultanea Modifica coda hello. Poiché è non possibile eseguire alcuna inferenza sull'ordine di hello di elementi di hello nella coda di hello, tutti e tre elementi hello potrebbe da rimuovere dalla coda, in qualsiasi ordine. coda Hello tenterà elementi hello tookeep in ordine di hello originale (accodato), ma può essere forzato tooreorder loro scadenza tooconcurrent operazioni o errori.  

- *Caso 2: Attività di rimozione dalla coda in parallelo*

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

Si supponga che le attività di hello completato, che l'attività hello vengano eseguiti in parallelo e che si sono verificati non altre transazioni simultanee Modifica coda hello. Poiché nessun inferenza può essere effettuata sull'ordine di hello di elementi di hello nella coda di hello hello elenchi *dequeue1* e *dequeue2* conterrà ogni due elementi, in qualsiasi ordine.

lo stesso elemento verrà Hello *non* entrambi gli elenchi. Di conseguenza, se dequeue1 contiene i valori *10*, *30*, dequeue2 conterrà i valori *20* e *40*.

- *Caso 3: ordine di rimozione dalla coda con interruzione della transazione*

L'interruzione di una transazione con in transito rimuove dalla coda riporta elementi hello sul vertice hello della coda di hello. ordine di Hello in cui gli elementi di hello vengano rimessi sul vertice hello della coda di hello non è garantito. Esaminiamo hello seguente codice:

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    // Abort hello transaction
    await txn.AbortAsync();
}
```
Si supponga che sono stati rimossi dalla coda di elementi hello in hello seguente ordine:
> 10, 20

Quando si interrotta la transazione hello, hello sarebbe possibile aggiungere elementi head toohello posteriore della coda di hello in uno dei seguenti ordini hello:
> 10, 20

> 20, 10

Hello lo stesso vale per tutti i casi in cui la transazione hello non è stato *eseguito*.

## <a name="programming-patterns"></a>Modelli di programmazione
In questa sezione verranno esaminati alcuni modelli di programmazione che possono risultare utili usando ReliableConcurrentQueue.

### <a name="batch-dequeues"></a>Rimozioni dalla coda in batch
Consigliato di un modello di programmazione sia per hello consumer attività toobatch la rimuove dalla coda anziché eseguire una rimozione dalla coda contemporaneamente. utente di Hello può scegliere toothrottle ritardi tra le dimensioni del batch ogni batch o hello. Hello frammento di codice seguente viene illustrato questo modello di programmazione.  Si noti che in questo esempio, l'elaborazione di hello viene eseguita dopo il commit della transazione hello in modo se un errore toooccur durante l'elaborazione, hello elementi non elaborati andranno persi senza essere stato trasformato.  In alternativa, è possibile eseguire l'elaborazione di hello nell'ambito della transazione hello, tuttavia questo può avere un impatto negativo sulle prestazioni e richiede una gestione degli elementi di hello già elaborato.

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

### <a name="best-effort-notification-based-processing"></a>Elaborazione basata su notifica con il migliore sforzo
Un altro modello di programmazione interessano utilizza hello conteggio API. In questo caso, è possibile implementare l'elaborazione sforzo basato sulla notifica per la coda di hello. coda di Hello conteggio può essere utilizzato toothrottle un accodamento o un'attività di rimozione dalla coda.  Si noti che nell'esempio precedente hello, poiché l'elaborazione di hello avviene all'esterno della transazione hello, gli elementi non elaborati potrebbero essere persi se si verifica un errore durante l'elaborazione.

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

### <a name="best-effort-drain"></a>Svuotamento in base al migliore sforzo
Lo svuotamento della coda di hello non può essere garantito scadenza toohello natura simultanee hello della struttura di dati.  È possibile che, anche se nessuna operazione utente sulla coda hello sono in transito, tooTryDequeueAsync una determinata chiamata non può restituire un elemento che in precedenza era accodati e il commit.  elemento accodato Hello è garantita troppo*infine* diventano visibili toodequeue, ma senza un meccanismo di comunicazione fuori banda, un consumer indipendente non è in grado di tale coda hello ha raggiunto un stato stabile anche se tutti i sono stati interrotti i producer e alcuna nuova operazione di accodamento non sono consentite. Operazione di svuotamento hello è pertanto sforzo come implementati sotto.

utente Hello deve arrestare tutte le successive producer e attività del consumer e attendere qualsiasi toocommit le transazioni in transito o di interruzione, prima di tentare di coda hello toodrain.  Se l'utente hello conosce il numero di hello previsto di elementi nella coda di hello, è possibile impostare una notifica che segnala che sono stati rimossi dalla coda di tutti gli elementi.

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

### <a name="peek"></a>Visualizzazione
ReliableConcurrentQueue non fornisce hello *TryPeekAsync* api. Gli utenti possono ottenere peek hello semantica utilizzando un *TryDequeueAsync* e quindi l'interruzione delle transazioni hello. In questo esempio rimuove dalla coda vengono elaborati solo se è maggiore del valore dell'elemento hello *10*.

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

## <a name="must-read"></a>Da leggere
* [Avvio rapido a Reliable Services di Microsoft Azure Service Fabric](service-fabric-reliable-services-quick-start.md)
* [Lavorare con le raccolte Reliable Collections](service-fabric-work-with-reliable-collections.md)
* [Notifiche di Reliable Services](service-fabric-reliable-services-notifications.md)
* [Eseguire il backup e il ripristino di Reliable Services (ripristino di emergenza)](service-fabric-reliable-services-backup-restore.md)
* [Reliable State Manager configuration (Configurazione di Reliable State Manager)](service-fabric-reliable-services-configuration.md)
* [Introduzione ai servizi API Web di Microsoft Azure Service Fabric](service-fabric-reliable-services-communication-webapi.md)
* [Utilizzo avanzato di hello modello di programmazione di servizi affidabili](service-fabric-reliable-services-advanced-usage.md)
* [Guida di riferimento per gli sviluppatori per Reliable Collections](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
