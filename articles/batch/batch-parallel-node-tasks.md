---
title: "le attività in parallelo toouse aaaRun le risorse di calcolo in modo efficiente - Azure Batch | Documenti Microsoft"
description: "Aumenta l'efficienza e si riducono i costi usando meno nodi di calcolo ed eseguendo attività simultanee in ogni nodo dei pool di Azure Batch"
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 538a067c-1f6e-44eb-a92b-8d51c33d3e1a
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 05df4b7d8e0bc595168a97faa231b7c90fe81980
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-tasks-concurrently-toomaximize-usage-of-batch-compute-nodes"></a>Eseguire attività contemporaneamente toomaximize utilizzo dei nodi di calcolo di Batch 

Eseguendo più attività contemporaneamente in ogni nodo di calcolo nel pool di Batch di Azure, è possibile ottimizzare l'utilizzo delle risorse a un numero ridotto di nodi nel pool di hello. Per alcuni carichi di lavoro, questo può consentire tempi di processo più brevi e riduzione del costo.

Mentre alcuni scenari di trarre vantaggio da dedicare tutti singola attività tooa da un nodo risorse, diverse situazioni vantaggioso consentendo a più attività tooshare tali risorse:

* **Ridurre al minimo il trasferimento dei dati** quando le attività sono in grado di tooshare dati. In questo scenario, è possibile ridurre notevolmente i costi di trasferimento di dati tramite la copia di dati condivisi tooa minor numero di nodi e l'esecuzione di attività in parallelo in ogni nodo. Ciò vale soprattutto se nodo copiato tooeach toobe di hello dati deve essere trasferito tra aree geografiche.
* **Ottimizzazione dell'utilizzo della memoria** quando le attività richiedono quantità di memoria elevate ma solo per brevi periodi di tempo e in ore variabili durante l'esecuzione. È possibile utilizzare un numero inferiore, ma di dimensioni maggiori, i nodi con più memoria tooefficiently gestiscono picchi di questo tipo di calcolo. Questi nodi dispongono di più attività in esecuzione in parallelo in ogni nodo, ma ogni attività richiederebbe di molta memoria dei nodi hello in momenti diversi.
* **Riduzione dei limiti del numero di nodi** quando è necessaria la comunicazione tra nodi all'interno di un pool. Pool configurati per la comunicazione tra i nodi sono attualmente limitate too50 nodi di calcolo. Se ogni nodo in un pool di questo tipo è in grado di tooexecute attività in parallelo, un numero maggiore di attività può essere eseguito contemporaneamente.
* **La replica di un cluster di calcolo locale**, ad esempio quando si sposta innanzitutto un tooAzure ambiente di calcolo. Se la soluzione locale corrente viene eseguita più attività per ogni nodo di calcolo, è possibile aumentare il numero massimo di hello delle attività nodo toomore fedelmente che la configurazione.

## <a name="example-scenario"></a>Scenario di esempio
Come un esempio tooillustrate hello vantaggi dell'esecuzione dell'attività parallel, si supponga che l'applicazione di attività presenta i requisiti di CPU e memoria in modo che [Standard\_D1](../cloud-services/cloud-services-sizes-specs.md) nodi sono sufficienti. Tuttavia, in ordine toofinish hello processo nel tempo hello necessarie sono necessarie 1.000 di questi nodi.

Invece di usare nodi Standard\_D1 con 1 core CPU, è possibile usare nodi [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) con 16 core ognuno e abilitare l'esecuzione parallela delle attività. Sarà quindi possibile usare *un numero di nodi inferiore di 16 volte* e invece di 1.000 nodi ne serviranno solo 63. Inoltre, se il file di applicazione di grandi dimensioni o dati di riferimento sono necessari per ogni nodo, efficienza e la durata del processo vengono nuovamente migliorate poiché i dati di hello vengono copiati tooonly 16 nodi.

## <a name="enable-parallel-task-execution"></a>Abilitare l'esecuzione parallela di attività
Configurare i nodi di calcolo per l'esecuzione di attività in parallelo a livello di pool hello. Libreria .NET di Batch di hello impostare hello [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] proprietà quando si crea un pool. Se si utilizza l'API REST di Batch di hello, impostare hello [maxTasksPerNode] [ rest_addpool] elemento nel corpo della richiesta hello durante la creazione del pool.

Azure Batch consente tooset numero massimo di attività per ogni nodo toofour volte (x 4) hello numero di core di nodo. Ad esempio, se hello pool viene configurata con nodi di dimensione "Grande" (quattro core), quindi `maxTasksPerNode` può essere impostato too16. Per informazioni dettagliate sul numero di hello di core per ognuna delle dimensioni di hello nodo, vedere [dimensioni per i servizi Cloud](../cloud-services/cloud-services-sizes-specs.md). Per ulteriori informazioni sui limiti di servizio, vedere [quote e limiti per il servizio Azure Batch hello](batch-quota-limit.md).

> [!TIP]
> Essere tootake che in hello account `maxTasksPerNode` valore quando si costruisce un [formula di scalabilità automatica] [ enable_autoscaling] per il pool. Ad esempio, l'impatto di un aumento delle attività per nodo può influire in modo significativo su una formula che valuta `$RunningTasks` . Per altre informazioni, vedere [Ridimensionare automaticamente i nodi di calcolo in un pool di Azure Batch](batch-automatic-scaling.md) .
>
>

## <a name="distribution-of-tasks"></a>Distribuzione delle attività
Quando i nodi di calcolo hello in un pool possono eseguire le attività contemporaneamente, è importante toospecify come si desidera toobe attività hello distribuite tra i nodi nel pool di hello hello.

Utilizzando hello [CloudPool.TaskSchedulingPolicy] [ task_schedule] proprietà, è possibile specificare che l'attività devono essere assegnate in modo uniforme in tutti i nodi nel pool di hello ("distribuzione"). Oppure è possibile specificare che come numero di possibili attività deve essere assegnato tooeach nodo prima di attività assegnate nodo tooanother nel pool di hello ("documento").

Un esempio di come questa funzionalità è utile, è consigliabile pool hello di [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodi (nell'esempio hello sopra) che è configurato con un [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] valore pari a 16. Se hello [CloudPool.TaskSchedulingPolicy] [ task_schedule] è configurato con un [ComputeNodeFillType] [ fill_type] di *Pack*, è necessario ottimizzare l'utilizzo di tutti i 16 core di ogni nodo e consentire un [il ridimensionamento automatico pool](batch-automatic-scaling.md) tooprune i nodi inutilizzati dal pool hello (nodi senza attività assegnato). Ciò consente di ridurre al minimo l'utilizzo delle risorse e di generare un risparmio sui costi.

## <a name="batch-net-example"></a>Esempio per Batch .NET
Questo [.NET per Batch] [ api_net] il frammento di codice API Mostra toocreate una richiesta a un pool che contiene quattro nodi di grandi dimensioni con un massimo di quattro attività per ogni nodo. Specifica un criterio che compilerà ogni nodo con le attività precedenti tooassigning attività tooanother nel pool di hello di pianificazione di attività. Per ulteriori informazioni sull'aggiunta di pool utilizzando hello API .NET di Batch, vedere [BatchClient.PoolOperations.CreatePool][poolcreate_net].

```csharp
CloudPool pool =
    batchClient.PoolOperations.CreatePool(
        poolId: "mypool",
        targetDedicatedComputeNodes: 4
        virtualMachineSize: "large",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

pool.MaxTasksPerComputeNode = 4;
pool.TaskSchedulingPolicy = new TaskSchedulingPolicy(ComputeNodeFillType.Pack);
pool.Commit();
```

## <a name="batch-rest-example"></a>Esempio per Batch REST
Questo [Batch REST] [ api_rest] API frammento viene illustrato un toocreate richiesta un pool che contiene due nodi di grandi dimensioni con un massimo di quattro attività per ogni nodo. Per ulteriori informazioni sull'aggiunta di pool utilizzando hello API REST, vedere [aggiungere un account del pool di tooan][rest_addpool].

```json
{
  "odata.metadata":"https://myaccount.myregion.batch.azure.com/$metadata#pools/@Element",
  "id":"mypool",
  "vmSize":"large",
  "cloudServiceConfiguration": {
    "osFamily":"4",
    "targetOSVersion":"*",
  }
  "targetDedicatedComputeNodes":2,
  "maxTasksPerNode":4,
  "enableInterNodeCommunication":true,
}
```

> [!NOTE]
> È possibile impostare hello `maxTasksPerNode` elemento e [MaxTasksPerComputeNode] [ maxtasks_net] proprietà solo al momento della creazione del pool. e non possono essere modificati una volta che il pool è stato creato.
>
>

## <a name="code-sample"></a>Esempio di codice
Hello [ParallelNodeTasks] [ parallel_tasks_sample] progetto in GitHub di seguito viene illustrato l'utilizzo di hello di hello [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] proprietà.

Questa applicazione console c# utilizza hello [.NET per Batch] [ api_net] toocreate libreria un pool con una o più nodi di calcolo. Viene eseguito un numero configurabile di attività per tali carico variabile toosimulate di nodi. Output di un'applicazione hello specifica quali nodi eseguita ogni attività. un'applicazione Hello fornisce inoltre un riepilogo dei parametri del processo hello e durata. di seguito è riportata nella parte riepilogo Hello dell'output di hello di due esecuzioni diverse dell'applicazione di esempio hello.

```
Nodes: 1
Node size: large
Max tasks per node: 1
Tasks: 32
Duration: 00:30:01.4638023
```

prima esecuzione di Hello hello applicazione di esempio viene illustrato che con un singolo nodo nel pool di hello e impostazione di hello di un'attività per ogni nodo, la durata del processo hello è in 30 minuti.

```
Nodes: 1
Node size: large
Max tasks per node: 4
Tasks: 32
Duration: 00:08:48.2423500
```

Hello seconda esecuzione di hello esempio mostra una diminuzione significativa la durata del processo. Questo avviene perché il pool di hello è stato configurato con quattro attività per ogni nodo, che consente di processo hello toocomplete esecuzione di attività in parallelo in circa un quarto di tempo hello.

> [!NOTE]
> Durata processo Hello nei riepiloghi di hello sopra non include ora di creazione del pool. Ciascuno dei processi di hello precedenti è stato inviato toopreviously creato pool sono stati i cui nodi di calcolo in hello *Idle* dello stato in fase di invio.
>
>

## <a name="next-steps"></a>Passaggi successivi
### <a name="batch-explorer-heat-map"></a>Mappa termica di Batch Explorer
Hello [Azure Batch Explorer][batch_explorer], uno di hello Azure Batch [applicazioni di esempio][github_samples], contiene un *mappa termica* funzionalità che fornisce una visualizzazione dell'esecuzione dell'attività. Quando si sta eseguendo l'hello [ParallelTasks] [ parallel_tasks_sample] applicazione di esempio, è possibile utilizzare hello mappa termica con funzionalità tooeasily visualizzare esecuzione hello di attività in parallelo in ogni nodo.

![Mappa termica di Batch Explorer][1]

*La mappa termica di Batch Explorer mostra un pool di quattro nodi, in cui ogni nodo esegue attualmente quattro attività*

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[enable_autoscaling]: https://msdn.microsoft.com/library/azure/dn820173.aspx
[fill_type]: https://msdn.microsoft.com/library/microsoft.azure.batch.common.computenodefilltype.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[maxtasks_net]: http://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.maxtaskspercomputenode.aspx
[rest_addpool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[parallel_tasks_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/ParallelTasks
[poolcreate_net]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[task_schedule]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudpool.taskschedulingpolicy.aspx

[1]: ./media/batch-parallel-node-tasks\heat_map.png
