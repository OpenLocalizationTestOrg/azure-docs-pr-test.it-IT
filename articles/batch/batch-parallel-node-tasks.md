---
title: "Eseguire attività in parallelo per usare le risorse di calcolo in modo efficiente: Azure Batch | Documentazione Microsoft"
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
ms.openlocfilehash: 6903552d907a1ddb21d3b678e2d224b4b5e35b77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="run-tasks-concurrently-to-maximize-usage-of-batch-compute-nodes"></a><span data-ttu-id="3e364-103">Eseguire attività contemporaneamente per ottimizzare l'uso dei nodi di calcolo Batch</span><span class="sxs-lookup"><span data-stu-id="3e364-103">Run tasks concurrently to maximize usage of Batch compute nodes</span></span> 

<span data-ttu-id="3e364-104">Eseguendo più attività contemporaneamente in ogni nodo di calcolo nel pool di Azure Batch, è possibile ottimizzare l'utilizzo delle risorse in un numero inferiore di nodi nel pool.</span><span class="sxs-lookup"><span data-stu-id="3e364-104">By running more than one task simultaneously on each compute node in your Azure Batch pool, you can maximize resource usage on a smaller number of nodes in the pool.</span></span> <span data-ttu-id="3e364-105">Per alcuni carichi di lavoro, questo può consentire tempi di processo più brevi e riduzione del costo.</span><span class="sxs-lookup"><span data-stu-id="3e364-105">For some workloads, this can result in shorter job times and lower cost.</span></span>

<span data-ttu-id="3e364-106">In alcuni scenari è utile che le risorse di un nodo siano dedicate a una singola attività, ma in molti casi è consigliabile che più attività possano condividere tali risorse:</span><span class="sxs-lookup"><span data-stu-id="3e364-106">While some scenarios benefit from dedicating all of a node's resources to a single task, several situations benefit from allowing multiple tasks to share those resources:</span></span>

* <span data-ttu-id="3e364-107">**Riduzione dei trasferimenti di dati** nei casi in cui le risorse possono condividere i dati.</span><span class="sxs-lookup"><span data-stu-id="3e364-107">**Minimizing data transfer** when tasks are able to share data.</span></span> <span data-ttu-id="3e364-108">In questo scenario, è possibile ridurre notevolmente i costi di trasferimento dei dati copiando i dati condivisi in un numero inferiore di nodi ed eseguendo le attività in parallelo in ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="3e364-108">In this scenario, you can dramatically reduce data transfer charges by copying shared data to a smaller number of nodes and executing tasks in parallel on each node.</span></span> <span data-ttu-id="3e364-109">Questa opzione è praticabile soprattutto se i dati da copiare in ogni nodo devono essere trasferiti tra aree geografiche.</span><span class="sxs-lookup"><span data-stu-id="3e364-109">This especially applies if the data to be copied to each node must be transferred between geographic regions.</span></span>
* <span data-ttu-id="3e364-110">**Ottimizzazione dell'utilizzo della memoria** quando le attività richiedono quantità di memoria elevate ma solo per brevi periodi di tempo e in ore variabili durante l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="3e364-110">**Maximizing memory usage** when tasks require a large amount of memory, but only during short periods of time, and at variable times during execution.</span></span> <span data-ttu-id="3e364-111">È possibile usare un numero minore di istanze dei nodi, ma di dimensioni maggiori e con più memoria per gestire in modo efficiente i picchi.</span><span class="sxs-lookup"><span data-stu-id="3e364-111">You can employ fewer, but larger, compute nodes with more memory to efficiently handle such spikes.</span></span> <span data-ttu-id="3e364-112">Queste istanze dei nodi avranno più attività in esecuzione in parallelo su ogni nodo, ma ogni attività può sfruttare i vantaggi offerti dall'uso di una memoria con molti nodi in momenti diversi.</span><span class="sxs-lookup"><span data-stu-id="3e364-112">These nodes would have multiple tasks running in parallel on each node, but each task would take advantage of the nodes' plentiful memory at different times.</span></span>
* <span data-ttu-id="3e364-113">**Riduzione dei limiti del numero di nodi** quando è necessaria la comunicazione tra nodi all'interno di un pool.</span><span class="sxs-lookup"><span data-stu-id="3e364-113">**Mitigating node number limits** when inter-node communication is required within a pool.</span></span> <span data-ttu-id="3e364-114">Attualmente, per i pool configurati per la comunicazione tra nodi è previsto un limite di 50 nodi di calcolo,</span><span class="sxs-lookup"><span data-stu-id="3e364-114">Currently, pools configured for inter-node communication are limited to 50 compute nodes.</span></span> <span data-ttu-id="3e364-115">quindi, se ogni nodo nel pool può eseguire attività in parallelo, è possibile eseguire simultaneamente un maggior numero di attività.</span><span class="sxs-lookup"><span data-stu-id="3e364-115">If each node in such a pool is able to execute tasks in parallel, a greater number of tasks can be executed simultaneously.</span></span>
* <span data-ttu-id="3e364-116">**Replica di un cluster di elaborazione locale**, ad esempio durante il primo spostamento di un ambiente di calcolo in Azure.</span><span class="sxs-lookup"><span data-stu-id="3e364-116">**Replicating an on-premises compute cluster**, such as when you first move a compute environment to Azure.</span></span> <span data-ttu-id="3e364-117">Se la soluzione locale corrente esegue più attività per ogni nodo di calcolo, è possibile aumentare il numero massimo di attività dei nodi per rispecchiare maggiormente tale configurazione.</span><span class="sxs-lookup"><span data-stu-id="3e364-117">If your current on-premises solution executes multiple tasks per compute node, you can increase the maximum number of node tasks to more closely mirror that configuration.</span></span>

## <a name="example-scenario"></a><span data-ttu-id="3e364-118">Scenario di esempio</span><span class="sxs-lookup"><span data-stu-id="3e364-118">Example scenario</span></span>
<span data-ttu-id="3e364-119">Per mostrare i vantaggi dell'esecuzione parallela di attività, si supponga che l'applicazione delle attività abbia requisiti di CPU e memoria che possono essere soddisfatti da dimensioni del nodo [Standard\_D1](../cloud-services/cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="3e364-119">As an example to illustrate the benefits of parallel task execution, let's say that your task application has CPU and memory requirements such that [Standard\_D1](../cloud-services/cloud-services-sizes-specs.md) nodes are sufficient.</span></span> <span data-ttu-id="3e364-120">Per poter terminare il processo nei tempi previsti sono tuttavia necessari 1.000 nodi.</span><span class="sxs-lookup"><span data-stu-id="3e364-120">But, in order to finish the job in the required time, 1,000 of these nodes are needed.</span></span>

<span data-ttu-id="3e364-121">Invece di usare nodi Standard\_D1 con 1 core CPU, è possibile usare nodi [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) con 16 core ognuno e abilitare l'esecuzione parallela delle attività.</span><span class="sxs-lookup"><span data-stu-id="3e364-121">Instead of using Standard\_D1 nodes that have 1 CPU core, you could use [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes that have 16 cores each, and enable parallel task execution.</span></span> <span data-ttu-id="3e364-122">Sarà quindi possibile usare *un numero di nodi inferiore di 16 volte* e invece di 1.000 nodi ne serviranno solo 63.</span><span class="sxs-lookup"><span data-stu-id="3e364-122">Therefore, *16 times fewer nodes* could be used--instead of 1,000 nodes, only 63 would be required.</span></span> <span data-ttu-id="3e364-123">Se ogni nodo usa file dell'applicazione o dati di riferimento di grandi dimensioni, è anche possibile ottimizzare la durata e l'efficienza dei processi perché i dati vengono copiati solo in 16 nodi.</span><span class="sxs-lookup"><span data-stu-id="3e364-123">Additionally, if large application files or reference data are required for each node, job duration and efficiency are again improved since the data is copied to only 16 nodes.</span></span>

## <a name="enable-parallel-task-execution"></a><span data-ttu-id="3e364-124">Abilitare l'esecuzione parallela di attività</span><span class="sxs-lookup"><span data-stu-id="3e364-124">Enable parallel task execution</span></span>
<span data-ttu-id="3e364-125">I nodi di calcolo per l'esecuzione di attività parallele vengono configurati a livello di pool.</span><span class="sxs-lookup"><span data-stu-id="3e364-125">You configure compute nodes for parallel task execution at the pool level.</span></span> <span data-ttu-id="3e364-126">Con la libreria Batch .NET, impostare la proprietà [CloudPool.MaxTasksPerComputeNode][maxtasks_net] durante la creazione di un pool.</span><span class="sxs-lookup"><span data-stu-id="3e364-126">With the Batch .NET library, set the [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property when you create a pool.</span></span> <span data-ttu-id="3e364-127">Se si usa l'API REST Batch, impostare l'elemento [maxTasksPerNode][rest_addpool] nel corpo della richiesta durante la creazione del pool.</span><span class="sxs-lookup"><span data-stu-id="3e364-127">If you are using the Batch REST API, set the [maxTasksPerNode][rest_addpool] element in the request body during pool creation.</span></span>

<span data-ttu-id="3e364-128">Con Azure Batch è possibile impostare il numero massimo di attività consentite per nodo fino a quattro volte (4x) il numero di core del nodo.</span><span class="sxs-lookup"><span data-stu-id="3e364-128">Azure Batch allows you to set maximum tasks per node up to four times (4x) the number of node cores.</span></span> <span data-ttu-id="3e364-129">Ad esempio, se il pool è configurato con nodi di grandi dimensioni (quattro core), è possibile impostare il valore di `maxTasksPerNode` su 16.</span><span class="sxs-lookup"><span data-stu-id="3e364-129">For example, if the pool is configured with nodes of size "Large" (four cores), then `maxTasksPerNode` may be set to 16.</span></span> <span data-ttu-id="3e364-130">Per informazioni dettagliate sul numero di core per ognuna delle dimensioni del nodo, vedere [Dimensioni dei servizi cloud](../cloud-services/cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="3e364-130">For details on the number of cores for each of the node sizes, see [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md).</span></span> <span data-ttu-id="3e364-131">Per altre informazioni sui limiti del servizio, vedere [Quote e limiti per il servizio Azure Batch](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="3e364-131">For more information on service limits, see [Quotas and limits for the Azure Batch service](batch-quota-limit.md).</span></span>

> [!TIP]
> <span data-ttu-id="3e364-132">Verificare di tener conto del valore `maxTasksPerNode` durante la creazione di una [formula di scalabilità automatica][enable_autoscaling] per il pool.</span><span class="sxs-lookup"><span data-stu-id="3e364-132">Be sure to take into account the `maxTasksPerNode` value when you construct an [autoscale formula][enable_autoscaling] for your pool.</span></span> <span data-ttu-id="3e364-133">Ad esempio, l'impatto di un aumento delle attività per nodo può influire in modo significativo su una formula che valuta `$RunningTasks` .</span><span class="sxs-lookup"><span data-stu-id="3e364-133">For example, a formula that evaluates `$RunningTasks` could be dramatically affected by an increase in tasks per node.</span></span> <span data-ttu-id="3e364-134">Per altre informazioni, vedere [Ridimensionare automaticamente i nodi di calcolo in un pool di Azure Batch](batch-automatic-scaling.md) .</span><span class="sxs-lookup"><span data-stu-id="3e364-134">See [Automatically scale compute nodes in an Azure Batch pool](batch-automatic-scaling.md) for more information.</span></span>
>
>

## <a name="distribution-of-tasks"></a><span data-ttu-id="3e364-135">Distribuzione delle attività</span><span class="sxs-lookup"><span data-stu-id="3e364-135">Distribution of tasks</span></span>
<span data-ttu-id="3e364-136">Quando i nodi di calcolo in un pool possono eseguire attività simultaneamente, è importante specificare come distribuire le attività tra i nodi nel pool.</span><span class="sxs-lookup"><span data-stu-id="3e364-136">When the compute nodes in a pool can execute tasks concurrently, it's important to specify how you want the tasks to be distributed across the nodes in the pool.</span></span>

<span data-ttu-id="3e364-137">La proprietà [CloudPool.TaskSchedulingPolicy][task_schedule] consente di specificare che le attività vengano assegnate in modo uniforme in tutti i nodi del pool ("distribuzione").</span><span class="sxs-lookup"><span data-stu-id="3e364-137">By using the [CloudPool.TaskSchedulingPolicy][task_schedule] property, you can specify that tasks should be assigned evenly across all nodes in the pool ("spreading").</span></span> <span data-ttu-id="3e364-138">In alternativa, è possibile specificare che più attività possibili vengano assegnate a ciascun nodo prima di essere assegnate a un altro nodo del pool ("imballaggio").</span><span class="sxs-lookup"><span data-stu-id="3e364-138">Or you can specify that as many tasks as possible should be assigned to each node before tasks are assigned to another node in the pool ("packing").</span></span>

<span data-ttu-id="3e364-139">Per comprendere l'importanza di questa funzionalità, si consideri il pool di nodi [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) (nell'esempio precedente) configurato con un valore per [CloudPool.MaxTasksPerComputeNode][maxtasks_net] pari a 16.</span><span class="sxs-lookup"><span data-stu-id="3e364-139">As an example of how this feature is valuable, consider the pool of [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes (in the example above) that is configured with a [CloudPool.MaxTasksPerComputeNode][maxtasks_net] value of 16.</span></span> <span data-ttu-id="3e364-140">Se [CloudPool.TaskSchedulingPolicy][task_schedule] è configurato con un tipo [ComputeNodeFillType][fill_type] per *Pack*, viene ottimizzato l'uso di tutti i 16 core di ogni nodo e, per i [pool con scalabilità automatica](batch-automatic-scaling.md), è possibile escludere dal pool i nodi non usati, cioè quelli a cui non sono assegnate attività.</span><span class="sxs-lookup"><span data-stu-id="3e364-140">If the [CloudPool.TaskSchedulingPolicy][task_schedule] is configured with a [ComputeNodeFillType][fill_type] of *Pack*, it would maximize usage of all 16 cores of each node and allow an [autoscaling pool](batch-automatic-scaling.md) to prune unused nodes from the pool (nodes without any tasks assigned).</span></span> <span data-ttu-id="3e364-141">Ciò consente di ridurre al minimo l'utilizzo delle risorse e di generare un risparmio sui costi.</span><span class="sxs-lookup"><span data-stu-id="3e364-141">This minimizes resource usage and saves money.</span></span>

## <a name="batch-net-example"></a><span data-ttu-id="3e364-142">Esempio per Batch .NET</span><span class="sxs-lookup"><span data-stu-id="3e364-142">Batch .NET example</span></span>
<span data-ttu-id="3e364-143">Questo frammento di codice dell'API [Batch .NET][api_net] specifica una richiesta per creare un pool contenente quattro nodi di grandi dimensioni con un massimo di quattro attività per nodo.</span><span class="sxs-lookup"><span data-stu-id="3e364-143">This [Batch .NET][api_net] API code snippet shows a request to create a pool that contains four large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="3e364-144">Specifica i criteri di pianificazione delle attività che definiscono le attività da inserire in ogni nodo prima di assegnarle a un altro nodo nel pool.</span><span class="sxs-lookup"><span data-stu-id="3e364-144">It specifies a task scheduling policy that will fill each node with tasks prior to assigning tasks to another node in the pool.</span></span> <span data-ttu-id="3e364-145">Per altre informazioni sull'aggiunta di pool con l'API Batch .NET, vedere [BatchClient.PoolOperations.CreatePool][poolcreate_net].</span><span class="sxs-lookup"><span data-stu-id="3e364-145">For more information on adding pools by using the Batch .NET API, see [BatchClient.PoolOperations.CreatePool][poolcreate_net].</span></span>

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

## <a name="batch-rest-example"></a><span data-ttu-id="3e364-146">Esempio per Batch REST</span><span class="sxs-lookup"><span data-stu-id="3e364-146">Batch REST example</span></span>
<span data-ttu-id="3e364-147">Questo frammento di codice dell'API [REST Batch][api_rest] specifica una richiesta per creare un pool contenente due nodi di grandi dimensioni con un massimo di quattro attività per nodo.</span><span class="sxs-lookup"><span data-stu-id="3e364-147">This [Batch REST][api_rest] API snippet shows a request to create a pool that contains two large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="3e364-148">Per altre informazioni sull'aggiunta di pool con l'API REST, vedere [Aggiungere un pool a un account][rest_addpool].</span><span class="sxs-lookup"><span data-stu-id="3e364-148">For more information on adding pools by using the REST API, see [Add a pool to an account][rest_addpool].</span></span>

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
> <span data-ttu-id="3e364-149">L'elemento `maxTasksPerNode` e la proprietà [MaxTasksPerComputeNode][maxtasks_net] possono essere impostati solo al momento della creazione del pool.</span><span class="sxs-lookup"><span data-stu-id="3e364-149">You can set the `maxTasksPerNode` element and [MaxTasksPerComputeNode][maxtasks_net] property only at pool creation time.</span></span> <span data-ttu-id="3e364-150">e non possono essere modificati una volta che il pool è stato creato.</span><span class="sxs-lookup"><span data-stu-id="3e364-150">They cannot be modified after a pool has already been created.</span></span>
>
>

## <a name="code-sample"></a><span data-ttu-id="3e364-151">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="3e364-151">Code sample</span></span>
<span data-ttu-id="3e364-152">Il progetto [ParallelNodeTasks][parallel_tasks_sample] in GitHub illustra l'uso della proprietà [CloudPool.MaxTasksPerComputeNode][maxtasks_net].</span><span class="sxs-lookup"><span data-stu-id="3e364-152">The [ParallelNodeTasks][parallel_tasks_sample] project on GitHub illustrates the use of the [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property.</span></span>

<span data-ttu-id="3e364-153">Questa applicazione console C# usa la libreria [Batch .NET][api_net] per creare un pool con uno o più nodi di calcolo</span><span class="sxs-lookup"><span data-stu-id="3e364-153">This C# console application uses the [Batch .NET][api_net] library to create a pool with one or more compute nodes.</span></span> <span data-ttu-id="3e364-154">ed esegue un numero configurabile di attività su tali nodi per simulare un carico variabile.</span><span class="sxs-lookup"><span data-stu-id="3e364-154">It executes a configurable number of tasks on those nodes to simulate variable load.</span></span> <span data-ttu-id="3e364-155">L'output dell'applicazione specifica quali nodi eseguono una specifica attività.</span><span class="sxs-lookup"><span data-stu-id="3e364-155">Output from the application specifies which nodes executed each task.</span></span> <span data-ttu-id="3e364-156">L'applicazione fornisce inoltre un riepilogo dei parametri e della durata del processo.</span><span class="sxs-lookup"><span data-stu-id="3e364-156">The application also provides a summary of the job parameters and duration.</span></span> <span data-ttu-id="3e364-157">Di seguito è visualizzato la parte relativa al riepilogo dell'output da due diverse esecuzioni dell'applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="3e364-157">The summary portion of the output from two different runs of the sample application appears below.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 1
Tasks: 32
Duration: 00:30:01.4638023
```

<span data-ttu-id="3e364-158">La prima esecuzione dell'applicazione di esempio mostra che con un singolo nodo nel pool e con l'impostazione predefinita di un'attività per nodo, la durata del processo è superiore a 30 minuti.</span><span class="sxs-lookup"><span data-stu-id="3e364-158">The first execution of the sample application shows that with a single node in the pool and the default setting of one task per node, the job duration is over 30 minutes.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 4
Tasks: 32
Duration: 00:08:48.2423500
```

<span data-ttu-id="3e364-159">La seconda esecuzione dell'esempio illustra una diminuzione significativa nella durata del processo.</span><span class="sxs-lookup"><span data-stu-id="3e364-159">The second run of the sample shows a significant decrease in job duration.</span></span> <span data-ttu-id="3e364-160">In questo modo il pool è stato configurato con quattro attività per ogni nodo, consentendo all'esecuzione di attività parallele di completare il processo in circa un quarto del tempo.</span><span class="sxs-lookup"><span data-stu-id="3e364-160">This is because the pool was configured with four tasks per node, which allows for parallel task execution to complete the job in nearly a quarter of the time.</span></span>

> [!NOTE]
> <span data-ttu-id="3e364-161">Le durate del processo nei riepiloghi precedenti non includono il tempo di creazione del pool.</span><span class="sxs-lookup"><span data-stu-id="3e364-161">The job durations in the summaries above do not include pool creation time.</span></span> <span data-ttu-id="3e364-162">Tutti i processi precedenti sono stati inviati a pool creati in precedenza, i cui nodi di calcolo si trovavano nello stato *inattivo* al momento dell'invio.</span><span class="sxs-lookup"><span data-stu-id="3e364-162">Each of the jobs above was submitted to previously created pools whose compute nodes were in the *Idle* state at submission time.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="3e364-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3e364-163">Next steps</span></span>
### <a name="batch-explorer-heat-map"></a><span data-ttu-id="3e364-164">Mappa termica di Batch Explorer</span><span class="sxs-lookup"><span data-stu-id="3e364-164">Batch Explorer Heat Map</span></span>
<span data-ttu-id="3e364-165">[Azure Batch Explorer][batch_explorer], una delle [applicazioni di esempio][github_samples] di Azure Batch, contiene una funzionalità *Mappa termica* che consente di visualizzare l'esecuzione dell'attività.</span><span class="sxs-lookup"><span data-stu-id="3e364-165">The [Azure Batch Explorer][batch_explorer], one of the Azure Batch [sample applications][github_samples], contains a *Heat Map* feature that provides visualization of task execution.</span></span> <span data-ttu-id="3e364-166">Durante l'esecuzione dell'applicazione di esempio [ParallelTasks][parallel_tasks_sample], è possibile usare la funzionalità Mappa termica per visualizzare facilmente l'esecuzione delle attività parallele in ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="3e364-166">When you're executing the [ParallelTasks][parallel_tasks_sample] sample application, you can use the Heat Map feature to easily visualize the execution of parallel tasks on each node.</span></span>

![Mappa termica di Batch Explorer][1]

<span data-ttu-id="3e364-168">*La mappa termica di Batch Explorer mostra un pool di quattro nodi, in cui ogni nodo esegue attualmente quattro attività*</span><span class="sxs-lookup"><span data-stu-id="3e364-168">*Batch Explorer Heat Map showing a pool of four nodes, with each node currently executing four tasks*</span></span>

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
