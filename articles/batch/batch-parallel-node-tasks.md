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
# <a name="run-tasks-concurrently-toomaximize-usage-of-batch-compute-nodes"></a><span data-ttu-id="4cbd1-103">Eseguire attività contemporaneamente toomaximize utilizzo dei nodi di calcolo di Batch</span><span class="sxs-lookup"><span data-stu-id="4cbd1-103">Run tasks concurrently toomaximize usage of Batch compute nodes</span></span> 

<span data-ttu-id="4cbd1-104">Eseguendo più attività contemporaneamente in ogni nodo di calcolo nel pool di Batch di Azure, è possibile ottimizzare l'utilizzo delle risorse a un numero ridotto di nodi nel pool di hello.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-104">By running more than one task simultaneously on each compute node in your Azure Batch pool, you can maximize resource usage on a smaller number of nodes in hello pool.</span></span> <span data-ttu-id="4cbd1-105">Per alcuni carichi di lavoro, questo può consentire tempi di processo più brevi e riduzione del costo.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-105">For some workloads, this can result in shorter job times and lower cost.</span></span>

<span data-ttu-id="4cbd1-106">Mentre alcuni scenari di trarre vantaggio da dedicare tutti singola attività tooa da un nodo risorse, diverse situazioni vantaggioso consentendo a più attività tooshare tali risorse:</span><span class="sxs-lookup"><span data-stu-id="4cbd1-106">While some scenarios benefit from dedicating all of a node's resources tooa single task, several situations benefit from allowing multiple tasks tooshare those resources:</span></span>

* <span data-ttu-id="4cbd1-107">**Ridurre al minimo il trasferimento dei dati** quando le attività sono in grado di tooshare dati.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-107">**Minimizing data transfer** when tasks are able tooshare data.</span></span> <span data-ttu-id="4cbd1-108">In questo scenario, è possibile ridurre notevolmente i costi di trasferimento di dati tramite la copia di dati condivisi tooa minor numero di nodi e l'esecuzione di attività in parallelo in ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-108">In this scenario, you can dramatically reduce data transfer charges by copying shared data tooa smaller number of nodes and executing tasks in parallel on each node.</span></span> <span data-ttu-id="4cbd1-109">Ciò vale soprattutto se nodo copiato tooeach toobe di hello dati deve essere trasferito tra aree geografiche.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-109">This especially applies if hello data toobe copied tooeach node must be transferred between geographic regions.</span></span>
* <span data-ttu-id="4cbd1-110">**Ottimizzazione dell'utilizzo della memoria** quando le attività richiedono quantità di memoria elevate ma solo per brevi periodi di tempo e in ore variabili durante l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-110">**Maximizing memory usage** when tasks require a large amount of memory, but only during short periods of time, and at variable times during execution.</span></span> <span data-ttu-id="4cbd1-111">È possibile utilizzare un numero inferiore, ma di dimensioni maggiori, i nodi con più memoria tooefficiently gestiscono picchi di questo tipo di calcolo.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-111">You can employ fewer, but larger, compute nodes with more memory tooefficiently handle such spikes.</span></span> <span data-ttu-id="4cbd1-112">Questi nodi dispongono di più attività in esecuzione in parallelo in ogni nodo, ma ogni attività richiederebbe di molta memoria dei nodi hello in momenti diversi.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-112">These nodes would have multiple tasks running in parallel on each node, but each task would take advantage of hello nodes' plentiful memory at different times.</span></span>
* <span data-ttu-id="4cbd1-113">**Riduzione dei limiti del numero di nodi** quando è necessaria la comunicazione tra nodi all'interno di un pool.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-113">**Mitigating node number limits** when inter-node communication is required within a pool.</span></span> <span data-ttu-id="4cbd1-114">Pool configurati per la comunicazione tra i nodi sono attualmente limitate too50 nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-114">Currently, pools configured for inter-node communication are limited too50 compute nodes.</span></span> <span data-ttu-id="4cbd1-115">Se ogni nodo in un pool di questo tipo è in grado di tooexecute attività in parallelo, un numero maggiore di attività può essere eseguito contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-115">If each node in such a pool is able tooexecute tasks in parallel, a greater number of tasks can be executed simultaneously.</span></span>
* <span data-ttu-id="4cbd1-116">**La replica di un cluster di calcolo locale**, ad esempio quando si sposta innanzitutto un tooAzure ambiente di calcolo.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-116">**Replicating an on-premises compute cluster**, such as when you first move a compute environment tooAzure.</span></span> <span data-ttu-id="4cbd1-117">Se la soluzione locale corrente viene eseguita più attività per ogni nodo di calcolo, è possibile aumentare il numero massimo di hello delle attività nodo toomore fedelmente che la configurazione.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-117">If your current on-premises solution executes multiple tasks per compute node, you can increase hello maximum number of node tasks toomore closely mirror that configuration.</span></span>

## <a name="example-scenario"></a><span data-ttu-id="4cbd1-118">Scenario di esempio</span><span class="sxs-lookup"><span data-stu-id="4cbd1-118">Example scenario</span></span>
<span data-ttu-id="4cbd1-119">Come un esempio tooillustrate hello vantaggi dell'esecuzione dell'attività parallel, si supponga che l'applicazione di attività presenta i requisiti di CPU e memoria in modo che [Standard\_D1](../cloud-services/cloud-services-sizes-specs.md) nodi sono sufficienti.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-119">As an example tooillustrate hello benefits of parallel task execution, let's say that your task application has CPU and memory requirements such that [Standard\_D1](../cloud-services/cloud-services-sizes-specs.md) nodes are sufficient.</span></span> <span data-ttu-id="4cbd1-120">Tuttavia, in ordine toofinish hello processo nel tempo hello necessarie sono necessarie 1.000 di questi nodi.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-120">But, in order toofinish hello job in hello required time, 1,000 of these nodes are needed.</span></span>

<span data-ttu-id="4cbd1-121">Invece di usare nodi Standard\_D1 con 1 core CPU, è possibile usare nodi [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) con 16 core ognuno e abilitare l'esecuzione parallela delle attività.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-121">Instead of using Standard\_D1 nodes that have 1 CPU core, you could use [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes that have 16 cores each, and enable parallel task execution.</span></span> <span data-ttu-id="4cbd1-122">Sarà quindi possibile usare *un numero di nodi inferiore di 16 volte* e invece di 1.000 nodi ne serviranno solo 63.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-122">Therefore, *16 times fewer nodes* could be used--instead of 1,000 nodes, only 63 would be required.</span></span> <span data-ttu-id="4cbd1-123">Inoltre, se il file di applicazione di grandi dimensioni o dati di riferimento sono necessari per ogni nodo, efficienza e la durata del processo vengono nuovamente migliorate poiché i dati di hello vengono copiati tooonly 16 nodi.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-123">Additionally, if large application files or reference data are required for each node, job duration and efficiency are again improved since hello data is copied tooonly 16 nodes.</span></span>

## <a name="enable-parallel-task-execution"></a><span data-ttu-id="4cbd1-124">Abilitare l'esecuzione parallela di attività</span><span class="sxs-lookup"><span data-stu-id="4cbd1-124">Enable parallel task execution</span></span>
<span data-ttu-id="4cbd1-125">Configurare i nodi di calcolo per l'esecuzione di attività in parallelo a livello di pool hello.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-125">You configure compute nodes for parallel task execution at hello pool level.</span></span> <span data-ttu-id="4cbd1-126">Libreria .NET di Batch di hello impostare hello [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] proprietà quando si crea un pool.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-126">With hello Batch .NET library, set hello [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property when you create a pool.</span></span> <span data-ttu-id="4cbd1-127">Se si utilizza l'API REST di Batch di hello, impostare hello [maxTasksPerNode] [ rest_addpool] elemento nel corpo della richiesta hello durante la creazione del pool.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-127">If you are using hello Batch REST API, set hello [maxTasksPerNode][rest_addpool] element in hello request body during pool creation.</span></span>

<span data-ttu-id="4cbd1-128">Azure Batch consente tooset numero massimo di attività per ogni nodo toofour volte (x 4) hello numero di core di nodo.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-128">Azure Batch allows you tooset maximum tasks per node up toofour times (4x) hello number of node cores.</span></span> <span data-ttu-id="4cbd1-129">Ad esempio, se hello pool viene configurata con nodi di dimensione "Grande" (quattro core), quindi `maxTasksPerNode` può essere impostato too16.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-129">For example, if hello pool is configured with nodes of size "Large" (four cores), then `maxTasksPerNode` may be set too16.</span></span> <span data-ttu-id="4cbd1-130">Per informazioni dettagliate sul numero di hello di core per ognuna delle dimensioni di hello nodo, vedere [dimensioni per i servizi Cloud](../cloud-services/cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="4cbd1-130">For details on hello number of cores for each of hello node sizes, see [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md).</span></span> <span data-ttu-id="4cbd1-131">Per ulteriori informazioni sui limiti di servizio, vedere [quote e limiti per il servizio Azure Batch hello](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="4cbd1-131">For more information on service limits, see [Quotas and limits for hello Azure Batch service](batch-quota-limit.md).</span></span>

> [!TIP]
> <span data-ttu-id="4cbd1-132">Essere tootake che in hello account `maxTasksPerNode` valore quando si costruisce un [formula di scalabilità automatica] [ enable_autoscaling] per il pool.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-132">Be sure tootake into account hello `maxTasksPerNode` value when you construct an [autoscale formula][enable_autoscaling] for your pool.</span></span> <span data-ttu-id="4cbd1-133">Ad esempio, l'impatto di un aumento delle attività per nodo può influire in modo significativo su una formula che valuta `$RunningTasks` .</span><span class="sxs-lookup"><span data-stu-id="4cbd1-133">For example, a formula that evaluates `$RunningTasks` could be dramatically affected by an increase in tasks per node.</span></span> <span data-ttu-id="4cbd1-134">Per altre informazioni, vedere [Ridimensionare automaticamente i nodi di calcolo in un pool di Azure Batch](batch-automatic-scaling.md) .</span><span class="sxs-lookup"><span data-stu-id="4cbd1-134">See [Automatically scale compute nodes in an Azure Batch pool](batch-automatic-scaling.md) for more information.</span></span>
>
>

## <a name="distribution-of-tasks"></a><span data-ttu-id="4cbd1-135">Distribuzione delle attività</span><span class="sxs-lookup"><span data-stu-id="4cbd1-135">Distribution of tasks</span></span>
<span data-ttu-id="4cbd1-136">Quando i nodi di calcolo hello in un pool possono eseguire le attività contemporaneamente, è importante toospecify come si desidera toobe attività hello distribuite tra i nodi nel pool di hello hello.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-136">When hello compute nodes in a pool can execute tasks concurrently, it's important toospecify how you want hello tasks toobe distributed across hello nodes in hello pool.</span></span>

<span data-ttu-id="4cbd1-137">Utilizzando hello [CloudPool.TaskSchedulingPolicy] [ task_schedule] proprietà, è possibile specificare che l'attività devono essere assegnate in modo uniforme in tutti i nodi nel pool di hello ("distribuzione").</span><span class="sxs-lookup"><span data-stu-id="4cbd1-137">By using hello [CloudPool.TaskSchedulingPolicy][task_schedule] property, you can specify that tasks should be assigned evenly across all nodes in hello pool ("spreading").</span></span> <span data-ttu-id="4cbd1-138">Oppure è possibile specificare che come numero di possibili attività deve essere assegnato tooeach nodo prima di attività assegnate nodo tooanother nel pool di hello ("documento").</span><span class="sxs-lookup"><span data-stu-id="4cbd1-138">Or you can specify that as many tasks as possible should be assigned tooeach node before tasks are assigned tooanother node in hello pool ("packing").</span></span>

<span data-ttu-id="4cbd1-139">Un esempio di come questa funzionalità è utile, è consigliabile pool hello di [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodi (nell'esempio hello sopra) che è configurato con un [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] valore pari a 16.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-139">As an example of how this feature is valuable, consider hello pool of [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes (in hello example above) that is configured with a [CloudPool.MaxTasksPerComputeNode][maxtasks_net] value of 16.</span></span> <span data-ttu-id="4cbd1-140">Se hello [CloudPool.TaskSchedulingPolicy] [ task_schedule] è configurato con un [ComputeNodeFillType] [ fill_type] di *Pack*, è necessario ottimizzare l'utilizzo di tutti i 16 core di ogni nodo e consentire un [il ridimensionamento automatico pool](batch-automatic-scaling.md) tooprune i nodi inutilizzati dal pool hello (nodi senza attività assegnato).</span><span class="sxs-lookup"><span data-stu-id="4cbd1-140">If hello [CloudPool.TaskSchedulingPolicy][task_schedule] is configured with a [ComputeNodeFillType][fill_type] of *Pack*, it would maximize usage of all 16 cores of each node and allow an [autoscaling pool](batch-automatic-scaling.md) tooprune unused nodes from hello pool (nodes without any tasks assigned).</span></span> <span data-ttu-id="4cbd1-141">Ciò consente di ridurre al minimo l'utilizzo delle risorse e di generare un risparmio sui costi.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-141">This minimizes resource usage and saves money.</span></span>

## <a name="batch-net-example"></a><span data-ttu-id="4cbd1-142">Esempio per Batch .NET</span><span class="sxs-lookup"><span data-stu-id="4cbd1-142">Batch .NET example</span></span>
<span data-ttu-id="4cbd1-143">Questo [.NET per Batch] [ api_net] il frammento di codice API Mostra toocreate una richiesta a un pool che contiene quattro nodi di grandi dimensioni con un massimo di quattro attività per ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-143">This [Batch .NET][api_net] API code snippet shows a request toocreate a pool that contains four large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="4cbd1-144">Specifica un criterio che compilerà ogni nodo con le attività precedenti tooassigning attività tooanother nel pool di hello di pianificazione di attività.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-144">It specifies a task scheduling policy that will fill each node with tasks prior tooassigning tasks tooanother node in hello pool.</span></span> <span data-ttu-id="4cbd1-145">Per ulteriori informazioni sull'aggiunta di pool utilizzando hello API .NET di Batch, vedere [BatchClient.PoolOperations.CreatePool][poolcreate_net].</span><span class="sxs-lookup"><span data-stu-id="4cbd1-145">For more information on adding pools by using hello Batch .NET API, see [BatchClient.PoolOperations.CreatePool][poolcreate_net].</span></span>

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

## <a name="batch-rest-example"></a><span data-ttu-id="4cbd1-146">Esempio per Batch REST</span><span class="sxs-lookup"><span data-stu-id="4cbd1-146">Batch REST example</span></span>
<span data-ttu-id="4cbd1-147">Questo [Batch REST] [ api_rest] API frammento viene illustrato un toocreate richiesta un pool che contiene due nodi di grandi dimensioni con un massimo di quattro attività per ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-147">This [Batch REST][api_rest] API snippet shows a request toocreate a pool that contains two large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="4cbd1-148">Per ulteriori informazioni sull'aggiunta di pool utilizzando hello API REST, vedere [aggiungere un account del pool di tooan][rest_addpool].</span><span class="sxs-lookup"><span data-stu-id="4cbd1-148">For more information on adding pools by using hello REST API, see [Add a pool tooan account][rest_addpool].</span></span>

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
> <span data-ttu-id="4cbd1-149">È possibile impostare hello `maxTasksPerNode` elemento e [MaxTasksPerComputeNode] [ maxtasks_net] proprietà solo al momento della creazione del pool.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-149">You can set hello `maxTasksPerNode` element and [MaxTasksPerComputeNode][maxtasks_net] property only at pool creation time.</span></span> <span data-ttu-id="4cbd1-150">e non possono essere modificati una volta che il pool è stato creato.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-150">They cannot be modified after a pool has already been created.</span></span>
>
>

## <a name="code-sample"></a><span data-ttu-id="4cbd1-151">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="4cbd1-151">Code sample</span></span>
<span data-ttu-id="4cbd1-152">Hello [ParallelNodeTasks] [ parallel_tasks_sample] progetto in GitHub di seguito viene illustrato l'utilizzo di hello di hello [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] proprietà.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-152">hello [ParallelNodeTasks][parallel_tasks_sample] project on GitHub illustrates hello use of hello [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property.</span></span>

<span data-ttu-id="4cbd1-153">Questa applicazione console c# utilizza hello [.NET per Batch] [ api_net] toocreate libreria un pool con una o più nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-153">This C# console application uses hello [Batch .NET][api_net] library toocreate a pool with one or more compute nodes.</span></span> <span data-ttu-id="4cbd1-154">Viene eseguito un numero configurabile di attività per tali carico variabile toosimulate di nodi.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-154">It executes a configurable number of tasks on those nodes toosimulate variable load.</span></span> <span data-ttu-id="4cbd1-155">Output di un'applicazione hello specifica quali nodi eseguita ogni attività.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-155">Output from hello application specifies which nodes executed each task.</span></span> <span data-ttu-id="4cbd1-156">un'applicazione Hello fornisce inoltre un riepilogo dei parametri del processo hello e durata.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-156">hello application also provides a summary of hello job parameters and duration.</span></span> <span data-ttu-id="4cbd1-157">di seguito è riportata nella parte riepilogo Hello dell'output di hello di due esecuzioni diverse dell'applicazione di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-157">hello summary portion of hello output from two different runs of hello sample application appears below.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 1
Tasks: 32
Duration: 00:30:01.4638023
```

<span data-ttu-id="4cbd1-158">prima esecuzione di Hello hello applicazione di esempio viene illustrato che con un singolo nodo nel pool di hello e impostazione di hello di un'attività per ogni nodo, la durata del processo hello è in 30 minuti.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-158">hello first execution of hello sample application shows that with a single node in hello pool and hello default setting of one task per node, hello job duration is over 30 minutes.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 4
Tasks: 32
Duration: 00:08:48.2423500
```

<span data-ttu-id="4cbd1-159">Hello seconda esecuzione di hello esempio mostra una diminuzione significativa la durata del processo.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-159">hello second run of hello sample shows a significant decrease in job duration.</span></span> <span data-ttu-id="4cbd1-160">Questo avviene perché il pool di hello è stato configurato con quattro attività per ogni nodo, che consente di processo hello toocomplete esecuzione di attività in parallelo in circa un quarto di tempo hello.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-160">This is because hello pool was configured with four tasks per node, which allows for parallel task execution toocomplete hello job in nearly a quarter of hello time.</span></span>

> [!NOTE]
> <span data-ttu-id="4cbd1-161">Durata processo Hello nei riepiloghi di hello sopra non include ora di creazione del pool.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-161">hello job durations in hello summaries above do not include pool creation time.</span></span> <span data-ttu-id="4cbd1-162">Ciascuno dei processi di hello precedenti è stato inviato toopreviously creato pool sono stati i cui nodi di calcolo in hello *Idle* dello stato in fase di invio.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-162">Each of hello jobs above was submitted toopreviously created pools whose compute nodes were in hello *Idle* state at submission time.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="4cbd1-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4cbd1-163">Next steps</span></span>
### <a name="batch-explorer-heat-map"></a><span data-ttu-id="4cbd1-164">Mappa termica di Batch Explorer</span><span class="sxs-lookup"><span data-stu-id="4cbd1-164">Batch Explorer Heat Map</span></span>
<span data-ttu-id="4cbd1-165">Hello [Azure Batch Explorer][batch_explorer], uno di hello Azure Batch [applicazioni di esempio][github_samples], contiene un *mappa termica* funzionalità che fornisce una visualizzazione dell'esecuzione dell'attività.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-165">hello [Azure Batch Explorer][batch_explorer], one of hello Azure Batch [sample applications][github_samples], contains a *Heat Map* feature that provides visualization of task execution.</span></span> <span data-ttu-id="4cbd1-166">Quando si sta eseguendo l'hello [ParallelTasks] [ parallel_tasks_sample] applicazione di esempio, è possibile utilizzare hello mappa termica con funzionalità tooeasily visualizzare esecuzione hello di attività in parallelo in ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="4cbd1-166">When you're executing hello [ParallelTasks][parallel_tasks_sample] sample application, you can use hello Heat Map feature tooeasily visualize hello execution of parallel tasks on each node.</span></span>

![Mappa termica di Batch Explorer][1]

<span data-ttu-id="4cbd1-168">*La mappa termica di Batch Explorer mostra un pool di quattro nodi, in cui ogni nodo esegue attualmente quattro attività*</span><span class="sxs-lookup"><span data-stu-id="4cbd1-168">*Batch Explorer Heat Map showing a pool of four nodes, with each node currently executing four tasks*</span></span>

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
