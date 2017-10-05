---
title: "Eseguire i carichi di lavoro di Azure Batch su macchine virtuali convenienti con priorità bassa (anteprima) | Microsoft Docs"
description: "Informazioni su come eseguire il provisioning di macchine virtuali con priorità bassa per ridurre i costi dei carichi di lavoro di Azure Batch."
services: batch
author: mscurrell
manager: timlt
ms.assetid: dc6ba151-1718-468a-b455-2da549225ab2
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.workload: na
ms.date: 07/21/2017
ms.author: markscu
ms.openlocfilehash: 9bf0ac322020d8a8453011c3207c1930175db6d3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="use-low-priority-vms-with-batch-preview"></a><span data-ttu-id="88697-103">Usare le VM con priorità bassa in Batch (anteprima)</span><span class="sxs-lookup"><span data-stu-id="88697-103">Use low-priority VMs with Batch (Preview)</span></span>

<span data-ttu-id="88697-104">Azure Batch offre macchine virtuali con priorità bassa per ridurre i costi dei carichi di lavoro Batch.</span><span class="sxs-lookup"><span data-stu-id="88697-104">Azure Batch offers low-priorty virtual machines (VMs) to reduce the cost of Batch workloads.</span></span> <span data-ttu-id="88697-105">Le macchine virtuali con priorità bassa rendono possibili nuovi tipi di carichi di lavoro Batch, assicurando una grande quantità di potenza di calcolo risultando anche economica.</span><span class="sxs-lookup"><span data-stu-id="88697-105">Low-priority VMs make new types of Batch workloads possible by providing a large amount of compute power that is also economical.</span></span>

<span data-ttu-id="88697-106">Le macchine virtuali con priorità bassa sfruttano la capacità in eccesso di Azure.</span><span class="sxs-lookup"><span data-stu-id="88697-106">Low-priority VMs take advantage of surplus capacity in Azure.</span></span> <span data-ttu-id="88697-107">Quando si specificano le macchine virtuali con priorità bassa nei pool, Azure Batch può usare automaticamente questo surplus quando disponibile.</span><span class="sxs-lookup"><span data-stu-id="88697-107">When you specify low-priority VMs in your pools, Azure Batch can automatically use this surplus when available.</span></span>

<span data-ttu-id="88697-108">Il compromesso per l'uso di macchine virtuali con priorità bassa è che queste macchine virtuali possono essere interrotte quando non c'è capacità in surplus in Azure.</span><span class="sxs-lookup"><span data-stu-id="88697-108">The tradeoff for using low-priority VMs is that those VMs may be preempted when no surplus capacity is available in Azure.</span></span> <span data-ttu-id="88697-109">Per questo motivo, le macchine virtuali con priorità bassa sono più adatte per determinati tipi di carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="88697-109">For this reason, low-priority VMs are most suitable for certain types of workloads.</span></span> <span data-ttu-id="88697-110">Usare le macchine virtuali con priorità bassa per carichi di lavoro di batch ed elaborazione asincrona in cui il tempo di completamento del processo è flessibile e il lavoro viene distribuito su più macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="88697-110">Use low-priority VMs for batch and asynchronous processing workloads where the job completion time is flexible and the work is distributed across many VMs.</span></span>

<span data-ttu-id="88697-111">Le macchine virtuali con priorità bassa sono decisamente meno dispendiose delle macchine virtuali dedicate.</span><span class="sxs-lookup"><span data-stu-id="88697-111">Low-priority VMs are significantly less expensive than dedicated VMs.</span></span> <span data-ttu-id="88697-112">Per i dettagli sui prezzi vedere [Prezzi dei Batch](https://azure.microsoft.com/pricing/details/batch/).</span><span class="sxs-lookup"><span data-stu-id="88697-112">For pricing details, see [Batch Pricing](https://azure.microsoft.com/pricing/details/batch/).</span></span>

<span data-ttu-id="88697-113">Per un'analisi aggiuntiva delle macchine virtuali con priorità bassa, vedere l'annuncio del post di blog: [Batch computing at a fraction of the price](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/) (Batch computing a prezzi ridotti).</span><span class="sxs-lookup"><span data-stu-id="88697-113">For an additional discussion of low-priority VMs, see the blog post announcement: [Batch computing at a fraction of the price](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="88697-114">Le macchine virtuali con priorità bassa sono attualmente in anteprima e sono disponibili solo per i carichi di lavoro in esecuzione in Batch.</span><span class="sxs-lookup"><span data-stu-id="88697-114">Low-priority VMs are currently in preview, and are available only for workloads running in Batch.</span></span> 
>
>

## <a name="use-cases-for-low-priority-vms"></a><span data-ttu-id="88697-115">Casi di uso per le macchine virtuali con priorità bassa</span><span class="sxs-lookup"><span data-stu-id="88697-115">Use cases for low-priority VMs</span></span>

<span data-ttu-id="88697-116">Considerando le caratteristiche delle macchine virtuali con priorità bassa, quali carichi di lavoro possono e non sono usarle?</span><span class="sxs-lookup"><span data-stu-id="88697-116">Given the characteristics of low-priority VMs, what workloads can and cannot use them?</span></span> <span data-ttu-id="88697-117">In generale, i carichi di elaborazione batch sono la soluzione ideale, quando i processi sono suddivisi in più attività in parallelo o viene eseguita la scalabilità orizzontale su più processi che vengono distribuiti tra più macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="88697-117">In general, batch processing workloads are a good fit, as jobs are broken into many parallel tasks or there are many jobs that are scaled out and distributed across many VMs.</span></span>

-   <span data-ttu-id="88697-118">Per ottimizzare l'uso della capacità in eccedenza in Azure, è possibile eseguire una scalabilità orizzontale su processi appropriati.</span><span class="sxs-lookup"><span data-stu-id="88697-118">To maximize use of surplus capacity in Azure, suitable jobs can scale out.</span></span>

-   <span data-ttu-id="88697-119">In alcuni casi le macchine virtuali potrebbero non essere disponibili o possono essere interrotte, il che comporterà una riduzione della capacità per i processi e può provocare un'interruzione e una riesecuzione delle attività.</span><span class="sxs-lookup"><span data-stu-id="88697-119">Occasionally VMs may not be available or will be preempted, which will result in reduced capacity for jobs and may lead to task interruption and reruns.</span></span> <span data-ttu-id="88697-120">I processi devono pertanto essere flessibili nel periodo in cui potrebbero essere eseguiti.</span><span class="sxs-lookup"><span data-stu-id="88697-120">Jobs must therefore be flexible in the time they can take to run.</span></span>

-   <span data-ttu-id="88697-121">I processi con attività più lunghe potrebbero subire maggiormente gli effetti se vengono interrotti.</span><span class="sxs-lookup"><span data-stu-id="88697-121">Jobs with longer tasks may be impacted more if interrupted.</span></span> <span data-ttu-id="88697-122">Se attività con tempi di esecuzione lunghi implementano il checkpoint per salvare l'avanzamento durante l'esecuzione, l'impatto dell'interruzione è decisamente minore.</span><span class="sxs-lookup"><span data-stu-id="88697-122">If long-running tasks implement checkpointing to save progress as they execute, then the impact of interruption would be far less.</span></span> <span data-ttu-id="88697-123">Le attività con tempi di esecuzione più brevi tendono a funzionare meglio con macchine virtuali con priorità bassa poiché l'impatto dell'interruzione è decisamente minore.</span><span class="sxs-lookup"><span data-stu-id="88697-123">Tasks with shorter execution times tend to work best with low-priority VMs as the impact of interruption is far less.</span></span>

-   <span data-ttu-id="88697-124">I processi MPI con tempi di esecuzione lunghi che usano più macchine virtuali non sono adatti all'uso di macchine virtuali con priorità bassa poiché una VM interrotta causerà probabilmente la necessità riesecuzione del processo.</span><span class="sxs-lookup"><span data-stu-id="88697-124">Long-running MPI jobs that utilize multiple VMs are not well suited to use low-priority VMs as one preempted VM will likely lead to the whole job having to be run again.</span></span>

<span data-ttu-id="88697-125">Esempi di casi d'uso di elaborazione batch adatti all'uso di macchine virtuali con priorità bassa sono:</span><span class="sxs-lookup"><span data-stu-id="88697-125">Some examples of batch processing use cases well suited to use low-priority VMs are:</span></span>

-   <span data-ttu-id="88697-126">**Sviluppo e test**: in particolare, se sono in fase di sviluppo soluzioni su larga scala, è possibile realizzare risparmi significativi.</span><span class="sxs-lookup"><span data-stu-id="88697-126">**Development and testing**: In particular, if large-scale solutions are being developed significant savings can be realized.</span></span> <span data-ttu-id="88697-127">Tutti i tipi di test possono trarre vantaggio, ma i test di carico su larga scala e i test di regressione ne traggono il miglio uso.</span><span class="sxs-lookup"><span data-stu-id="88697-127">All types of testing can benefit, but large-scale load testing and regression testing are great uses.</span></span>

-   <span data-ttu-id="88697-128">**Integrazione della capacità su richiesta**: le macchine virtuali con priorità bassa possono essere usate per integrare le normali macchine virtuali dedicate. Quando disponibili, i processi possono essere ridimensionati e pertanto possono essere completati più rapidamente a un costo inferiore, quando non sono disponibili, sono presenti le macchine virtuali dedicate di base.</span><span class="sxs-lookup"><span data-stu-id="88697-128">**Supplementing on-demand capacity**: Low-priority VMs can be used to supplement regular dedicated VMs - when available, jobs can scale and therefore complete quicker for lower cost; when not available, the baseline of dedicated VMs are available.</span></span>

-   <span data-ttu-id="88697-129">**Tempi di esecuzione del processo flessibili**: se c'è flessibilità nei tempi di completamento dei processi, le possibili cadute di capacità vengono considerate tollerabili; i processi delle macchine virtuali con priorità bassa, per giunta, verranno eseguiti spesso più rapidamente e a costi inferiori.</span><span class="sxs-lookup"><span data-stu-id="88697-129">**Flexible job execution time**: If there is flexibility in the time jobs have to complete, then potential drops in capacity can be tolerated; however, with the addition of low-priority VMs jobs will frequently run faster and for a lower cost.</span></span>

<span data-ttu-id="88697-130">È possibile configurare i pool di batch per usare macchine virtuali con priorità bassa in diversi modi, a seconda della flessibilità dei tempi di esecuzione del processo:</span><span class="sxs-lookup"><span data-stu-id="88697-130">Batch pools can be configured to use low-priority VMs in a few ways, depending on the flexibility in job execution time:</span></span>

-   <span data-ttu-id="88697-131">Le macchine virtuali con priorità bassa possono essere usate esclusivamente in un pool e Batch dovrà soltanto recuperare le capacità interrotte se disponibile.</span><span class="sxs-lookup"><span data-stu-id="88697-131">Low-priority VMs can solely be used in a pool and Batch will simply recover any preempted capacity when available.</span></span> <span data-ttu-id="88697-132">Questo è il modo più conveniente per eseguire i processi poiché vengono usate solo le macchine virtuali con priorità bassa.</span><span class="sxs-lookup"><span data-stu-id="88697-132">This is the cheapest way to execute jobs as only low-priority VMs are used.</span></span>

-   <span data-ttu-id="88697-133">Le macchine virtuali con priorità bassa possono essere usate in combinazione con macchine virtuali dedicate predefinite di base.</span><span class="sxs-lookup"><span data-stu-id="88697-133">Low-priority VMs can be used in conjunction with a fixed baseline of dedicated VMs.</span></span> <span data-ttu-id="88697-134">Il numero fisso di macchine virtuali dedicate garantisce che ci sia sempre una certa capacità per mantenere l'avanzamento del processo.</span><span class="sxs-lookup"><span data-stu-id="88697-134">The fixed number of dedicated VMs ensures there is always some capacity to keep a job progressing.</span></span>

-   <span data-ttu-id="88697-135">Può verificarsi una combinazione dinamica di macchine virtuali dedicate e con priorità bassa, in modo che le macchine virtuali con priorità bassa più economiche vengano usate esclusivamente quando disponibili, mentre le capacità delle macchine virtuali dedicate a prezzo pieno vengono aumentate quando necessario, per mantenere una quantità minima di capacità disponibile al fine di far avanzare il processo.</span><span class="sxs-lookup"><span data-stu-id="88697-135">There can be dynamic mix of dedicated and low-priority VMs, so that the cheaper low-priority VMs are solely used when available, but the full-priced dedicated VMs are scaled up when required, to keep a minimum amount of capacity available to keep the jobs progressing.</span></span>

## <a name="batch-support-for-low-priority-vms"></a><span data-ttu-id="88697-136">Supporto batch per le macchine virtuali con priorità bassa</span><span class="sxs-lookup"><span data-stu-id="88697-136">Batch support for low-priority VMs</span></span>

<span data-ttu-id="88697-137">Azure Batch offre diverse funzionalità che semplificano l'uso e i vantaggi dalle macchine virtuali con priorità bassa:</span><span class="sxs-lookup"><span data-stu-id="88697-137">Azure Batch provides several capabilities that make it easy to consume and benefit from low-priority VMs:</span></span>

-   <span data-ttu-id="88697-138">I pool di batch può contenere sia macchine virtuali dedicate che macchine virtuali con priorità bassa.</span><span class="sxs-lookup"><span data-stu-id="88697-138">Batch pools can contain both dedicated VMs and low-priority VMs.</span></span> <span data-ttu-id="88697-139">Il numero di ciascun tipo di macchina virtuale può essere specificato al momento della creazione di un nuovo pool o della modifica di un pool esistente, tramite l'operazione di ridimensionamento esplicito o la scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="88697-139">The number of each type of VM can be specified when a pool is created, or changed at any time for an existing pool, using the explicit resize operation or using auto-scale.</span></span> <span data-ttu-id="88697-140">L'invio di attività e processi può rimanere invariato e non deve riguardare necessariamente i tipi di macchine virtuali nel pool.</span><span class="sxs-lookup"><span data-stu-id="88697-140">Job and task submission can remain unchanged and do not need to be concerned with the VM types in the pool.</span></span> <span data-ttu-id="88697-141">È anche possibile che un pool usi soltanto le macchine virtuali con priorità bassa per eseguire processi nel modo più economico possibile, e che avvii macchine virtuali dedicate se la capacità scende al di sotto di una soglia minima, per mantenere i processi in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="88697-141">It is also possible to have a pool completely use low-priority VMs to run jobs as cheaply as possible, but spin up dedicated VMs if the capacity drops below a minimum threshold, to keep jobs running.</span></span>

-   <span data-ttu-id="88697-142">I pool di batch tentano automaticamente di puntare al numero di macchine virtuali con priorità bassa.</span><span class="sxs-lookup"><span data-stu-id="88697-142">Batch pools automatically seek to the target number of low-priority VMs.</span></span> <span data-ttu-id="88697-143">Se le macchine virtuali vengono interrotte, Batch tenterà di sostituire la capacità persa e di tornare all'obiettivo.</span><span class="sxs-lookup"><span data-stu-id="88697-143">If VMs are preempted, then Batch will attempt to replace the lost capacity and return to the target.</span></span>

-   <span data-ttu-id="88697-144">Nel caso di interruzioni di attività, Batch rileverà e riaccoderà automaticamente le attività da eseguire di nuovo.</span><span class="sxs-lookup"><span data-stu-id="88697-144">In the case of tasks being interrupted, Batch will detect and automatically requeue tasks to be run again.</span></span>

-   <span data-ttu-id="88697-145">Le macchine virtuali con priorità bassa hanno una quota di code diversa rispetto a quella delle VM dedicate.</span><span class="sxs-lookup"><span data-stu-id="88697-145">Low-priority VMs have a core quota that differs from that of dedicated VMs.</span></span> 
    <span data-ttu-id="88697-146">La quota per le macchine virtuali con priorità bassa è superiore a quella delle VM dedicate, perché le macchine virtuali con priorità bassa sono meno costose.</span><span class="sxs-lookup"><span data-stu-id="88697-146">The quote for low-priority VMs is higher than that of dedicated VMs, because low-priority VMs cost less.</span></span> <span data-ttu-id="88697-147">Per altre informazioni, vedere [Quote e limiti del servizio Batch](batch-quota-limit.md#resource-quotas).</span><span class="sxs-lookup"><span data-stu-id="88697-147">See [Batch service quotas and limits](batch-quota-limit.md#resource-quotas) for more information.</span></span>    

> [!NOTE]
> <span data-ttu-id="88697-148">Le macchine virtuali con priorità bassa non sono attualmente supportate per gli account di Batch in cui la modalità di allocazione del pool è impostata su [Sottoscrizione utente](batch-account-create-portal.md#user-subscription-mode).</span><span class="sxs-lookup"><span data-stu-id="88697-148">Low-priority VMs are not currently supported for Batch accounts where the pool allocation mode is set to [User subscription](batch-account-create-portal.md#user-subscription-mode).</span></span>
>
>

## <a name="create-and-update-pools"></a><span data-ttu-id="88697-149">Crea e aggiornare i pool</span><span class="sxs-lookup"><span data-stu-id="88697-149">Create and update pools</span></span>

<span data-ttu-id="88697-150">Un pool Batch può contenere sia macchine virtuali dedicate sia VM con priorità bassa, definite anche nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="88697-150">A Batch pool can contain both dedicated and low-priority VMs (also referred to as compute nodes).</span></span> <span data-ttu-id="88697-151">È possibile impostare il numero di nodi di calcolo sia per le macchine virtuali dedicate sia per le VM con priorità bassa.</span><span class="sxs-lookup"><span data-stu-id="88697-151">You can set the target number of compute nodes for both dedicated and low-priority VMs.</span></span> <span data-ttu-id="88697-152">Il numero di nodi di destinazione specifica il numero di macchine virtuali che si desidera avere nel pool.</span><span class="sxs-lookup"><span data-stu-id="88697-152">The target number of nodes specifies the number of VMs you want to have in the pool.</span></span>

<span data-ttu-id="88697-153">Ad esempio, per creare un pool con le macchine virtuali del servizio cloud di Azure con una destinazione di 5 VM dedicate e 20 macchine virtuali con priorità bassa:</span><span class="sxs-lookup"><span data-stu-id="88697-153">For example, to create a pool using Azure cloud service VMs with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

```csharp
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: "cspool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard_D2_v2",
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4") // WS 2012 R2
);
```

<span data-ttu-id="88697-154">Per creare un pool con le macchine virtuali di Azure, in questo caso le macchine virtuali Linux, con una destinazione di 5 VM dedicate e 20 macchine virtuali con priorità bassa:</span><span class="sxs-lookup"><span data-stu-id="88697-154">To create a pool using Azure virtual machines (in this case Linux VMs) with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

```csharp
ImageReference imageRef = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "16.04.0-LTS",
    version: "latest");

// Create the pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration("batch.node.ubuntu 16.04", imageRef);

pool = batchClient.PoolOperations.CreatePool(
    poolId: "vmpool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard\_D2\_v2",
    virtualMachineConfiguration: virtualMachineConfiguration);
```

<span data-ttu-id="88697-155">È possibile ottenere il numero corrente di nodi sia per le macchine virtuali dedicate che per quelle con priorità bassa:</span><span class="sxs-lookup"><span data-stu-id="88697-155">You can get the current number of nodes for both dedicated and low-priority VMs:</span></span>

```csharp
int? numDedicated = pool1.CurrentDedicatedComputeNodes;
int? numLowPri = pool1.CurrentLowPriorityComputeNodes;
```

<span data-ttu-id="88697-156">I nodi pool dispongono di una proprietà che indica se il nodo è una macchina virtuale dedicata o con priorità bassa:</span><span class="sxs-lookup"><span data-stu-id="88697-156">Pool nodes have a property to indicate if the node is a dedicated or low-priority VM:</span></span>

```csharp
bool? isNodeDedicated = poolNode.IsDedicated;
```

<span data-ttu-id="88697-157">Quando uno o più nodi in un pool vengono interrotti, un'operazione di elenco dei nodi nel pool continuerà a restituire i nodi, il numero corrente di nodi con priorità bassa rimarrà invariato, mentre lo stato di tali nodi sarà impostato su **Annullato**.</span><span class="sxs-lookup"><span data-stu-id="88697-157">When one or more nodes in a pool are preempted, a list nodes operation on the pool will still return those nodes, the current number of low-priority nodes will remain unchanged, but those nodes will have their state set to the **Preempted** state.</span></span> <span data-ttu-id="88697-158">Batch tenterà di individuare le macchine virtuali di sostituzione e, se l'operazione ha esito positivo, i nodi avranno lo stato **Creazione in corso** e poi **Avvio in corso** prima di essere disponibili per l'esecuzione di attività, come avviene per i nuovi nodi.</span><span class="sxs-lookup"><span data-stu-id="88697-158">Batch will attempt to find replacement VMs and, if successful, the nodes will go through **Creating** and then **Starting** states before becoming available for task execution, just like new nodes.</span></span>

## <a name="scale-a-pool-containing-low-priority-vms"></a><span data-ttu-id="88697-159">Ridimensionare un pool che contiene macchine virtuali con priorità bassa</span><span class="sxs-lookup"><span data-stu-id="88697-159">Scale a pool containing low-priority VMs</span></span>

<span data-ttu-id="88697-160">Così come avviene per i pool costituiti esclusivamente da macchine virtuali dedicate, è possibile ridimensionare un pool che contiene macchine virtuali con priorità bassa chiamando il metodo di ridimensionamento o mediante la scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="88697-160">As with pools solely consisting of dedicated VMs, it is possible to scale a pool containing low-priority VMs by calling the Resize method or by using auto-scale.</span></span>

<span data-ttu-id="88697-161">L'operazione di ridimensionamento del pool richiede un secondo parametro facoltativo che aggiorna il valore di **targetLowPriorityNodes**:</span><span class="sxs-lookup"><span data-stu-id="88697-161">The pool resize operation takes a second optional parameter that updates the value of **targetLowPriorityNodes**:</span></span>

```csharp
pool.Resize(targetDedicatedComputeNodes: 0, targetLowPriorityComputeNodes: 25);
```

<span data-ttu-id="88697-162">La formula di scalabilità automatica del pool supporta le macchine virtuali con priorità bassa nel seguente modo:</span><span class="sxs-lookup"><span data-stu-id="88697-162">The pool auto-scale formula supports low-priority VMs as follows:</span></span>

-   <span data-ttu-id="88697-163">È possibile ottenere o impostare il valore della variabile definita dal servizio **$TargetLowPriorityNodes**.</span><span class="sxs-lookup"><span data-stu-id="88697-163">You can get or set the value of the service-defined variable **$TargetLowPriorityNodes**.</span></span>

-   <span data-ttu-id="88697-164">È possibile ottenere il valore della variabile definita dal servizio **$CurrentLowPriorityNodes**.</span><span class="sxs-lookup"><span data-stu-id="88697-164">You can get the value of the service-defined variable **$CurrentLowPriorityNodes**.</span></span>

-   <span data-ttu-id="88697-165">È possibile ottenere il valore della variabile definita dal servizio **$PreemptedNodeCount**.</span><span class="sxs-lookup"><span data-stu-id="88697-165">You can get the value of the service-defined variable **$PreemptedNodeCount**.</span></span> 
    <span data-ttu-id="88697-166">Questa variabile restituisce il numero di nodi con lo stato Annullato e consente di aumentare o ridurre il numero di nodi dedicati, a seconda del numero di nodi di annullati che non sono disponibili.</span><span class="sxs-lookup"><span data-stu-id="88697-166">This variable returns the number of nodes in the preempted state and allows you to scale up or down the number of dedicated nodes, depending on the number of preempted nodes that are unavailable.</span></span>

## <a name="jobs-and-tasks"></a><span data-ttu-id="88697-167">Processi e attività</span><span class="sxs-lookup"><span data-stu-id="88697-167">Jobs and tasks</span></span>

<span data-ttu-id="88697-168">I processi e le attività richiedono un supporto minimo per nodi con priorità bassa. L'unico supporto è il seguente:</span><span class="sxs-lookup"><span data-stu-id="88697-168">Jobs and tasks require very little support for low-priority nodes; the only support is as follows:</span></span>

-   <span data-ttu-id="88697-169">La proprietà JobManagerTask di un processo ha una nuova proprietà, **AllowLowPriorityNode**.</span><span class="sxs-lookup"><span data-stu-id="88697-169">The JobManagerTask property of a job has a new property, **AllowLowPriorityNode**.</span></span> 
    <span data-ttu-id="88697-170">Quando questa proprietà è true, è possibile programmare le attività di gestione dei processi su un nodo dedicato o su un nodo con priorità bassa.</span><span class="sxs-lookup"><span data-stu-id="88697-170">When this property is true, the job manager task can be scheduled on either a dedicated or low-priority node.</span></span> <span data-ttu-id="88697-171">Se questa proprietà è false, l'attività di gestione dei processi verrà programmata solo per un nodo dedicato.</span><span class="sxs-lookup"><span data-stu-id="88697-171">If this property is false, the job manager task will be scheduled to a dedicated node only.</span></span>

-   <span data-ttu-id="88697-172">Per un'applicazione di attività è disponibile una [variabile di ambiente](batch-compute-node-environment-variables.md), in modo da determinarne l'esecuzione su un nodo dedicato o con priorità bassa.</span><span class="sxs-lookup"><span data-stu-id="88697-172">An [environment variable](batch-compute-node-environment-variables.md) is available to a task application so that it can determine whether it is running on a low-priority or dedicated node.</span></span> <span data-ttu-id="88697-173">La variabile di ambiente è AZ_BATCH_NODE_IS_DEDICATED.</span><span class="sxs-lookup"><span data-stu-id="88697-173">The environment variable is AZ_BATCH_NODE_IS_DEDICATED.</span></span>

## <a name="handling-preemption"></a><span data-ttu-id="88697-174">Gestione delle priorità</span><span class="sxs-lookup"><span data-stu-id="88697-174">Handling preemption</span></span>

<span data-ttu-id="88697-175">Le macchine virtuali in alcuni casi possono essere interrotte. In questo caso, Batch effettua le seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="88697-175">VMs may occasionally be preempted; when this happens, Batch does the following:</span></span>

-   <span data-ttu-id="88697-176">Le macchine virtuali interrotte hanno lo stato aggiornato ad **Annullato**.</span><span class="sxs-lookup"><span data-stu-id="88697-176">The preempted VMs have their state updated to **Preempted**.</span></span>
-   <span data-ttu-id="88697-177">Se sulle macchine virtuali di un nodo annullato vi erano delle attività in esecuzione, queste vengono riaccodate e rieseguire.</span><span class="sxs-lookup"><span data-stu-id="88697-177">If tasks were running on the preempted node VMs, then those tasks are requeued and run again.</span></span>
-   <span data-ttu-id="88697-178">La macchina virtuale viene eliminata in modo efficace e tutti i dati memorizzati in locale nella macchina virtuale andranno persi.</span><span class="sxs-lookup"><span data-stu-id="88697-178">The VM is effectively deleted, leading to any data stored locally on the VM being lost.</span></span>
-   <span data-ttu-id="88697-179">Il pool tenta continuamente raggiungere il numero stabilito di nodi con priorità bassa disponibili.</span><span class="sxs-lookup"><span data-stu-id="88697-179">The pool continually attempts to reach the target number of low-priority nodes available.</span></span> <span data-ttu-id="88697-180">Quando viene individuata una capacità di sostituzione, i nodi mantengono il proprio ID, ma vengono inizializzati di nuovo, attraversando gli stati **Creazione in corso** e **Avvio in corso** prima che siano disponibili per la pianificazione delle attività.</span><span class="sxs-lookup"><span data-stu-id="88697-180">When replacement capacity is found, the nodes keep their ids, but are re-initialized, going through **Creating** and **Starting** states before they are available for task scheduling.</span></span>
-   <span data-ttu-id="88697-181">Il numero delle priorità è disponibile come metrica nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="88697-181">Preemption counts are available as a metric in the Azure portal.</span></span>

## <a name="metrics"></a><span data-ttu-id="88697-182">Metriche</span><span class="sxs-lookup"><span data-stu-id="88697-182">Metrics</span></span>

<span data-ttu-id="88697-183">Per i nodi con priorità bassa sono disponibili nuove metriche nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="88697-183">New metrics are available in the [Azure portal](https://portal.azure.com) for low-priority nodes.</span></span> <span data-ttu-id="88697-184">Le metriche sono:</span><span class="sxs-lookup"><span data-stu-id="88697-184">These metrics are:</span></span>

- <span data-ttu-id="88697-185">Numero di nodi a bassa priorità</span><span class="sxs-lookup"><span data-stu-id="88697-185">Low-Priority Node Count</span></span>
- <span data-ttu-id="88697-186">Numero di core a bassa priorità</span><span class="sxs-lookup"><span data-stu-id="88697-186">Low-Priority Core Count</span></span> 
- <span data-ttu-id="88697-187">Numero di nodi annullati</span><span class="sxs-lookup"><span data-stu-id="88697-187">Preempted Node Count</span></span>

<span data-ttu-id="88697-188">Per visualizzare le metriche nel portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="88697-188">To view metrics in the Azure portal:</span></span>

1. <span data-ttu-id="88697-189">Passare all'account Batch nel portale e visualizzare le impostazioni per l'account Batch.</span><span class="sxs-lookup"><span data-stu-id="88697-189">Navigate to your Batch account in the portal, and view the settings for your Batch account.</span></span>
2. <span data-ttu-id="88697-190">Selezionare **Metrica** dalla sezione **Monitoraggio**.</span><span class="sxs-lookup"><span data-stu-id="88697-190">Select **Metrics** from the **Monitoring** section.</span></span>
3. <span data-ttu-id="88697-191">Selezionare le metriche da usare dall'elenco **Metriche disponibili**.</span><span class="sxs-lookup"><span data-stu-id="88697-191">Select the metrics you desire from the **Available Metrics** list.</span></span>

![Metriche per i nodi a priorità bassa](media/batch-low-pri-vms/low-pri-metrics.png)

## <a name="next-steps"></a><span data-ttu-id="88697-193">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="88697-193">Next steps</span></span>

* <span data-ttu-id="88697-194">Vedere [Panoramica sulle funzionalità di Batch per sviluppatori](batch-api-basics.md)per informazioni essenziali per chiunque si prepari all'uso di Batch.</span><span class="sxs-lookup"><span data-stu-id="88697-194">Read the [Batch feature overview for developers](batch-api-basics.md), essential information for anyone preparing to use Batch.</span></span> <span data-ttu-id="88697-195">L'articolo contiene informazioni più dettagliate sulle risorse del servizio Batch, ad esempio pool, nodi, processi e attività, e sulle numerose funzionalità delle API che è possibile usare durante la compilazione dell'applicazione Batch.</span><span class="sxs-lookup"><span data-stu-id="88697-195">The article contains more detailed information about Batch service resources like pools, nodes, jobs, and tasks, and the many API features that you can use while building your Batch application.</span></span>
* <span data-ttu-id="88697-196">Informazioni sulle [API e gli strumenti di Batch](batch-apis-tools.md) disponibili per la compilazione di soluzioni Batch.</span><span class="sxs-lookup"><span data-stu-id="88697-196">Learn about the [Batch APIs and tools](batch-apis-tools.md) available for building Batch solutions.</span></span>
