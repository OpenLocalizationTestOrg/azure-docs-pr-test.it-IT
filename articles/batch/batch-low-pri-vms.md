---
title: "carichi di lavoro di Azure Batch aaaRun in economiche macchine virtuali con priorità bassa (anteprima) | Documenti Microsoft"
description: "Informazioni su come hello di tooreduce macchine virtuali con priorità bassa tooprovision costo dei carichi di lavoro di Azure Batch."
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
ms.openlocfilehash: 91a5e89a819d05583e6b146932d925e217b4be4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-low-priority-vms-with-batch-preview"></a><span data-ttu-id="12849-103">Usare le VM con priorità bassa in Batch (anteprima)</span><span class="sxs-lookup"><span data-stu-id="12849-103">Use low-priority VMs with Batch (Preview)</span></span>

<span data-ttu-id="12849-104">Azure Batch offre un costo hello tooreduce limitati al virtuali (VM) dei carichi di lavoro di Batch.</span><span class="sxs-lookup"><span data-stu-id="12849-104">Azure Batch offers low-priorty virtual machines (VMs) tooreduce hello cost of Batch workloads.</span></span> <span data-ttu-id="12849-105">Le macchine virtuali con priorità bassa rendono possibili nuovi tipi di carichi di lavoro Batch, assicurando una grande quantità di potenza di calcolo risultando anche economica.</span><span class="sxs-lookup"><span data-stu-id="12849-105">Low-priority VMs make new types of Batch workloads possible by providing a large amount of compute power that is also economical.</span></span>

<span data-ttu-id="12849-106">Le macchine virtuali con priorità bassa sfruttano la capacità in eccesso di Azure.</span><span class="sxs-lookup"><span data-stu-id="12849-106">Low-priority VMs take advantage of surplus capacity in Azure.</span></span> <span data-ttu-id="12849-107">Quando si specificano le macchine virtuali con priorità bassa nei pool, Azure Batch può usare automaticamente questo surplus quando disponibile.</span><span class="sxs-lookup"><span data-stu-id="12849-107">When you specify low-priority VMs in your pools, Azure Batch can automatically use this surplus when available.</span></span>

<span data-ttu-id="12849-108">compromesso di Hello per l'utilizzo di macchine virtuali con priorità bassa è che tali macchine virtuali possono essere interrotta quando nessun surplus della capacità è disponibile in Azure.</span><span class="sxs-lookup"><span data-stu-id="12849-108">hello tradeoff for using low-priority VMs is that those VMs may be preempted when no surplus capacity is available in Azure.</span></span> <span data-ttu-id="12849-109">Per questo motivo, le macchine virtuali con priorità bassa sono più adatte per determinati tipi di carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="12849-109">For this reason, low-priority VMs are most suitable for certain types of workloads.</span></span> <span data-ttu-id="12849-110">Utilizzare le macchine virtuali con priorità bassa per l'elaborazione asincrona di carichi di lavoro in cui tempo di completamento del processo di hello è flessibile e lavoro hello viene distribuito tra più macchine virtuali e batch.</span><span class="sxs-lookup"><span data-stu-id="12849-110">Use low-priority VMs for batch and asynchronous processing workloads where hello job completion time is flexible and hello work is distributed across many VMs.</span></span>

<span data-ttu-id="12849-111">Le macchine virtuali con priorità bassa sono decisamente meno dispendiose delle macchine virtuali dedicate.</span><span class="sxs-lookup"><span data-stu-id="12849-111">Low-priority VMs are significantly less expensive than dedicated VMs.</span></span> <span data-ttu-id="12849-112">Per i dettagli sui prezzi vedere [Prezzi dei Batch](https://azure.microsoft.com/pricing/details/batch/).</span><span class="sxs-lookup"><span data-stu-id="12849-112">For pricing details, see [Batch Pricing](https://azure.microsoft.com/pricing/details/batch/).</span></span>

<span data-ttu-id="12849-113">Per un approfondimento delle macchine virtuali con priorità bassa, vedere l'annuncio del post di blog hello: [Batch calcolo a una frazione del prezzo di hello](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).</span><span class="sxs-lookup"><span data-stu-id="12849-113">For an additional discussion of low-priority VMs, see hello blog post announcement: [Batch computing at a fraction of hello price](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="12849-114">Le macchine virtuali con priorità bassa sono attualmente in anteprima e sono disponibili solo per i carichi di lavoro in esecuzione in Batch.</span><span class="sxs-lookup"><span data-stu-id="12849-114">Low-priority VMs are currently in preview, and are available only for workloads running in Batch.</span></span> 
>
>

## <a name="use-cases-for-low-priority-vms"></a><span data-ttu-id="12849-115">Casi di uso per le macchine virtuali con priorità bassa</span><span class="sxs-lookup"><span data-stu-id="12849-115">Use cases for low-priority VMs</span></span>

<span data-ttu-id="12849-116">Considerando caratteristiche hello di macchine virtuali con priorità bassa, quali carichi di lavoro può e non è possibile utilizzarli?</span><span class="sxs-lookup"><span data-stu-id="12849-116">Given hello characteristics of low-priority VMs, what workloads can and cannot use them?</span></span> <span data-ttu-id="12849-117">In generale, i carichi di elaborazione batch sono la soluzione ideale, quando i processi sono suddivisi in più attività in parallelo o viene eseguita la scalabilità orizzontale su più processi che vengono distribuiti tra più macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="12849-117">In general, batch processing workloads are a good fit, as jobs are broken into many parallel tasks or there are many jobs that are scaled out and distributed across many VMs.</span></span>

-   <span data-ttu-id="12849-118">utilizzo di toomaximize di surplus della capacità nei processi di Azure, adatti possibile scalare orizzontalmente.</span><span class="sxs-lookup"><span data-stu-id="12849-118">toomaximize use of surplus capacity in Azure, suitable jobs can scale out.</span></span>

-   <span data-ttu-id="12849-119">In alcuni casi le macchine virtuali potrebbero non essere disponibili o per essere interrotta, comporterà la riduzione della capacità per i processi che possono causare repliche e l'interruzione tootask.</span><span class="sxs-lookup"><span data-stu-id="12849-119">Occasionally VMs may not be available or will be preempted, which will result in reduced capacity for jobs and may lead tootask interruption and reruns.</span></span> <span data-ttu-id="12849-120">I processi devono pertanto essere flessibili nel tempo hello che possono assumere toorun.</span><span class="sxs-lookup"><span data-stu-id="12849-120">Jobs must therefore be flexible in hello time they can take toorun.</span></span>

-   <span data-ttu-id="12849-121">I processi con attività più lunghe potrebbero subire maggiormente gli effetti se vengono interrotti.</span><span class="sxs-lookup"><span data-stu-id="12849-121">Jobs with longer tasks may be impacted more if interrupted.</span></span> <span data-ttu-id="12849-122">Se l'attività di implementano lo stato di avanzamento di checkpoint toosave mentre vengono eseguite con esecuzione prolungata, quindi l'impatto dell'interruzione sarebbe decisamente minore.</span><span class="sxs-lookup"><span data-stu-id="12849-122">If long-running tasks implement checkpointing toosave progress as they execute, then the impact of interruption would be far less.</span></span> <span data-ttu-id="12849-123">Attività con tempi di esecuzione inferiore tendono toowork meglio con le macchine virtuali con priorità bassa come impatto hello di interruzione è molto inferiore.</span><span class="sxs-lookup"><span data-stu-id="12849-123">Tasks with shorter execution times tend toowork best with low-priority VMs as hello impact of interruption is far less.</span></span>

-   <span data-ttu-id="12849-124">I processi MPI che utilizzano più macchine virtuali non sono adatti toouse con esecuzione prolungata macchine virtuali con priorità bassa come una macchina virtuale superata verranno probabilmente lead toohello intero processo eseguiva toobe nuovamente.</span><span class="sxs-lookup"><span data-stu-id="12849-124">Long-running MPI jobs that utilize multiple VMs are not well suited toouse low-priority VMs as one preempted VM will likely lead toohello whole job having toobe run again.</span></span>

<span data-ttu-id="12849-125">Alcuni esempi di elaborazione batch usano toouse adatto a casi sono macchine virtuali con priorità bassa:</span><span class="sxs-lookup"><span data-stu-id="12849-125">Some examples of batch processing use cases well suited toouse low-priority VMs are:</span></span>

-   <span data-ttu-id="12849-126">**Sviluppo e test**: in particolare, se sono in fase di sviluppo soluzioni su larga scala, è possibile realizzare risparmi significativi.</span><span class="sxs-lookup"><span data-stu-id="12849-126">**Development and testing**: In particular, if large-scale solutions are being developed significant savings can be realized.</span></span> <span data-ttu-id="12849-127">Tutti i tipi di test possono trarre vantaggio, ma i test di carico su larga scala e i test di regressione ne traggono il miglio uso.</span><span class="sxs-lookup"><span data-stu-id="12849-127">All types of testing can benefit, but large-scale load testing and regression testing are great uses.</span></span>

-   <span data-ttu-id="12849-128">**Integrazione di capacità su richiesta**: le macchine virtuali con priorità bassa possono essere utilizzate per integrare le macchine virtuali regular dedicate - scalare e pertanto completare più rapidamente a un costo inferiore quando è disponibile, i processi; quando non è disponibile, hello della linea di base di dedicato le macchine virtuali sono disponibili.</span><span class="sxs-lookup"><span data-stu-id="12849-128">**Supplementing on-demand capacity**: Low-priority VMs can be used to supplement regular dedicated VMs - when available, jobs can scale and therefore complete quicker for lower cost; when not available, hello baseline of dedicated VMs are available.</span></span>

-   <span data-ttu-id="12849-129">**Tempo di esecuzione processo flessibile**: se è disponibile una flessibilità in processi timer hello è toocomplete, quindi cadute potenziale di capacità è possibile tollerare; tuttavia hello aggiunta dei processi di macchine virtuali con priorità bassa frequenza eseguirà più velocemente e con un costo inferiore.</span><span class="sxs-lookup"><span data-stu-id="12849-129">**Flexible job execution time**: If there is flexibility in hello time jobs have toocomplete, then potential drops in capacity can be tolerated; however, with hello addition of low-priority VMs jobs will frequently run faster and for a lower cost.</span></span>

<span data-ttu-id="12849-130">Pool di batch può essere configurato toouse macchine virtuali con priorità bassa in diversi modi, a seconda flessibilità hello in fase di esecuzione del processo:</span><span class="sxs-lookup"><span data-stu-id="12849-130">Batch pools can be configured toouse low-priority VMs in a few ways, depending on hello flexibility in job execution time:</span></span>

-   <span data-ttu-id="12849-131">Le macchine virtuali con priorità bassa possono essere usate esclusivamente in un pool e Batch dovrà soltanto recuperare le capacità interrotte se disponibile.</span><span class="sxs-lookup"><span data-stu-id="12849-131">Low-priority VMs can solely be used in a pool and Batch will simply recover any preempted capacity when available.</span></span> <span data-ttu-id="12849-132">Si tratta di processi di tooexecute modo più economici hello come vengono utilizzate le macchine virtuali solo con priorità bassa.</span><span class="sxs-lookup"><span data-stu-id="12849-132">This is hello cheapest way tooexecute jobs as only low-priority VMs are used.</span></span>

-   <span data-ttu-id="12849-133">Le macchine virtuali con priorità bassa possono essere usate in combinazione con macchine virtuali dedicate predefinite di base.</span><span class="sxs-lookup"><span data-stu-id="12849-133">Low-priority VMs can be used in conjunction with a fixed baseline of dedicated VMs.</span></span> <span data-ttu-id="12849-134">Hello numero fisso di macchine virtuali dedicate garantisce che vi siano sempre alcune tookeep capacità un avanzamento del processo.</span><span class="sxs-lookup"><span data-stu-id="12849-134">hello fixed number of dedicated VMs ensures there is always some capacity tookeep a job progressing.</span></span>

-   <span data-ttu-id="12849-135">Può essere dinamica combinazione di macchine virtuali con priorità bassa e dedicate, in modo che più economiche macchine virtuali con priorità bassa vengono utilizzate esclusivamente quando è disponibile, ma le macchine virtuali hello con un prezzo full dedicato vengono ridimensionate quando richiesto, tookeep una quantità minima di processi di capacità disponibile tookeep hello avanzamento.</span><span class="sxs-lookup"><span data-stu-id="12849-135">There can be dynamic mix of dedicated and low-priority VMs, so that the cheaper low-priority VMs are solely used when available, but hello full-priced dedicated VMs are scaled up when required, tookeep a minimum amount of capacity available tookeep hello jobs progressing.</span></span>

## <a name="batch-support-for-low-priority-vms"></a><span data-ttu-id="12849-136">Supporto batch per le macchine virtuali con priorità bassa</span><span class="sxs-lookup"><span data-stu-id="12849-136">Batch support for low-priority VMs</span></span>

<span data-ttu-id="12849-137">Azure Batch offre diverse funzionalità che rendono facilmente tooconsume e trarre vantaggio dalle macchine virtuali con priorità bassa:</span><span class="sxs-lookup"><span data-stu-id="12849-137">Azure Batch provides several capabilities that make it easy tooconsume and benefit from low-priority VMs:</span></span>

-   <span data-ttu-id="12849-138">I pool di batch può contenere sia macchine virtuali dedicate che macchine virtuali con priorità bassa.</span><span class="sxs-lookup"><span data-stu-id="12849-138">Batch pools can contain both dedicated VMs and low-priority VMs.</span></span> <span data-ttu-id="12849-139">Quando un pool viene creato o modificato in qualsiasi momento per un pool esistente, tramite l'operazione di ridimensionamento esplicita hello o scalabilità automatica, è possibile specificare il numero di Hello di ogni tipo di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="12849-139">hello number of each type of VM can be specified when a pool is created, or changed at any time for an existing pool, using hello explicit resize operation or using auto-scale.</span></span> <span data-ttu-id="12849-140">Invio di processi e delle attività può rimanere invariato e non è necessario preoccuparsi di tipi di macchine Virtuali hello nel pool di hello.</span><span class="sxs-lookup"><span data-stu-id="12849-140">Job and task submission can remain unchanged and do not need to be concerned with hello VM types in hello pool.</span></span> <span data-ttu-id="12849-141">È inoltre possibile toohave un pool completamente utilizzare processi toorun di macchine virtuali con priorità bassa come economici possibile, ma di spin up dedicate macchine virtuali se la capacità di hello scende di sotto di una soglia minima, per mantenere i processi in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="12849-141">It is also possible toohave a pool completely use low-priority VMs toorun jobs as cheaply as possible, but spin up dedicated VMs if hello capacity drops below a minimum threshold, to keep jobs running.</span></span>

-   <span data-ttu-id="12849-142">Pool di batch di posizionamento automaticamente toohello numero di macchine virtuali con priorità bassa.</span><span class="sxs-lookup"><span data-stu-id="12849-142">Batch pools automatically seek toohello target number of low-priority VMs.</span></span> <span data-ttu-id="12849-143">Se le macchine virtuali vengono sostituite, Batch tenterà hello tooreplace perdita capacità e la destinazione toohello restituito.</span><span class="sxs-lookup"><span data-stu-id="12849-143">If VMs are preempted, then Batch will attempt tooreplace hello lost capacity and return toohello target.</span></span>

-   <span data-ttu-id="12849-144">Nel caso di hello di attività viene interrotta, Batch rileverà e automaticamente riaccodare toobe attività eseguire di nuovo.</span><span class="sxs-lookup"><span data-stu-id="12849-144">In hello case of tasks being interrupted, Batch will detect and automatically requeue tasks toobe run again.</span></span>

-   <span data-ttu-id="12849-145">Le macchine virtuali con priorità bassa hanno una quota di code diversa rispetto a quella delle VM dedicate.</span><span class="sxs-lookup"><span data-stu-id="12849-145">Low-priority VMs have a core quota that differs from that of dedicated VMs.</span></span> 
    <span data-ttu-id="12849-146">Hello offerta per le macchine virtuali con priorità bassa è superiore a quello delle macchine virtuali dedicate, perché le macchine virtuali con priorità bassa costano inferiori.</span><span class="sxs-lookup"><span data-stu-id="12849-146">hello quote for low-priority VMs is higher than that of dedicated VMs, because low-priority VMs cost less.</span></span> <span data-ttu-id="12849-147">Per altre informazioni, vedere [Quote e limiti del servizio Batch](batch-quota-limit.md#resource-quotas).</span><span class="sxs-lookup"><span data-stu-id="12849-147">See [Batch service quotas and limits](batch-quota-limit.md#resource-quotas) for more information.</span></span>    

> [!NOTE]
> <span data-ttu-id="12849-148">Macchine virtuali con priorità bassa non sono attualmente supportate per gli account Batch in modalità di allocazione del pool di hello è impostata troppo[sottoscrizione utente](batch-account-create-portal.md#user-subscription-mode).</span><span class="sxs-lookup"><span data-stu-id="12849-148">Low-priority VMs are not currently supported for Batch accounts where hello pool allocation mode is set too[User subscription](batch-account-create-portal.md#user-subscription-mode).</span></span>
>
>

## <a name="create-and-update-pools"></a><span data-ttu-id="12849-149">Crea e aggiornare i pool</span><span class="sxs-lookup"><span data-stu-id="12849-149">Create and update pools</span></span>

<span data-ttu-id="12849-150">Un pool di Batch può contenere le macchine virtuali sia dedicate e con priorità bassa (anche noto tooas nodi di calcolo).</span><span class="sxs-lookup"><span data-stu-id="12849-150">A Batch pool can contain both dedicated and low-priority VMs (also referred tooas compute nodes).</span></span> <span data-ttu-id="12849-151">È possibile impostare il numero di destinazione hello di nodi di calcolo per le macchine virtuali sia dedicate e con priorità bassa.</span><span class="sxs-lookup"><span data-stu-id="12849-151">You can set hello target number of compute nodes for both dedicated and low-priority VMs.</span></span> <span data-ttu-id="12849-152">numero di nodi di destinazione Hello specifica hello numero di macchine virtuali desiderate toohave nel pool di hello.</span><span class="sxs-lookup"><span data-stu-id="12849-152">hello target number of nodes specifies hello number of VMs you want toohave in hello pool.</span></span>

<span data-ttu-id="12849-153">Ad esempio, toocreate un pool usando il servizio cloud di Azure le macchine virtuali con una destinazione di 5 dedicato macchine virtuali e 20 macchine virtuali con priorità bassa:</span><span class="sxs-lookup"><span data-stu-id="12849-153">For example, toocreate a pool using Azure cloud service VMs with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

```csharp
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: "cspool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard_D2_v2",
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4") // WS 2012 R2
);
```

<span data-ttu-id="12849-154">toocreate un pool con macchine virtuali di Azure (in questo caso, le macchine virtuali Linux) con una destinazione di 5 dedicato macchine virtuali e 20 macchine virtuali con priorità bassa:</span><span class="sxs-lookup"><span data-stu-id="12849-154">toocreate a pool using Azure virtual machines (in this case Linux VMs) with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

```csharp
ImageReference imageRef = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "16.04.0-LTS",
    version: "latest");

// Create hello pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration("batch.node.ubuntu 16.04", imageRef);

pool = batchClient.PoolOperations.CreatePool(
    poolId: "vmpool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard\_D2\_v2",
    virtualMachineConfiguration: virtualMachineConfiguration);
```

<span data-ttu-id="12849-155">È possibile ottenere il numero corrente di hello dei nodi per le macchine virtuali sia dedicate e con priorità bassa:</span><span class="sxs-lookup"><span data-stu-id="12849-155">You can get hello current number of nodes for both dedicated and low-priority VMs:</span></span>

```csharp
int? numDedicated = pool1.CurrentDedicatedComputeNodes;
int? numLowPri = pool1.CurrentLowPriorityComputeNodes;
```

<span data-ttu-id="12849-156">I nodi del pool sono tooindicate una proprietà se il nodo di hello è una macchina virtuale dedicata o con priorità bassa:</span><span class="sxs-lookup"><span data-stu-id="12849-156">Pool nodes have a property tooindicate if hello node is a dedicated or low-priority VM:</span></span>

```csharp
bool? isNodeDedicated = poolNode.IsDedicated;
```

<span data-ttu-id="12849-157">Quando vengono interrotti uno o più nodi in un pool, un'operazione di elenco nodi del pool continuerà a restituire i nodi, hello numero corrente di nodi con priorità bassa rimane invariata, ma tali nodi avrà il relativo stato è impostato toothe **annullato**stato.</span><span class="sxs-lookup"><span data-stu-id="12849-157">When one or more nodes in a pool are preempted, a list nodes operation on the pool will still return those nodes, hello current number of low-priority nodes will remain unchanged, but those nodes will have their state set toothe **Preempted** state.</span></span> <span data-ttu-id="12849-158">Batch tenterà toofind sostituzione, le macchine virtuali e, se ha esito positivo, i nodi di hello verranno esaminate **creazione** e quindi **iniziale** stati prima di essere rese disponibili per l'esecuzione di attività, come i nuovi nodi.</span><span class="sxs-lookup"><span data-stu-id="12849-158">Batch will attempt toofind replacement VMs and, if successful, hello nodes will go through **Creating** and then **Starting** states before becoming available for task execution, just like new nodes.</span></span>

## <a name="scale-a-pool-containing-low-priority-vms"></a><span data-ttu-id="12849-159">Ridimensionare un pool che contiene macchine virtuali con priorità bassa</span><span class="sxs-lookup"><span data-stu-id="12849-159">Scale a pool containing low-priority VMs</span></span>

<span data-ttu-id="12849-160">Come con pool esclusivamente costituito da macchine virtuali dedicate, è possibili tooscale una pool che contiene con priorità bassa VM chiamando il metodo di ridimensionamento hello o con scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="12849-160">As with pools solely consisting of dedicated VMs, it is possible tooscale a pool containing low-priority VMs by calling hello Resize method or by using auto-scale.</span></span>

<span data-ttu-id="12849-161">operazione di ridimensionamento pool Hello accetta un parametro di secondo parametro facoltativo che aggiorna il valore di **targetLowPriorityNodes**:</span><span class="sxs-lookup"><span data-stu-id="12849-161">hello pool resize operation takes a second optional parameter that updates the value of **targetLowPriorityNodes**:</span></span>

```csharp
pool.Resize(targetDedicatedComputeNodes: 0, targetLowPriorityComputeNodes: 25);
```

<span data-ttu-id="12849-162">formula di scalabilità automatica pool Hello supporta le macchine virtuali con priorità bassa, come segue:</span><span class="sxs-lookup"><span data-stu-id="12849-162">hello pool auto-scale formula supports low-priority VMs as follows:</span></span>

-   <span data-ttu-id="12849-163">È possibile ottenere o impostare il valore di hello della variabile definito dal servizio hello **$TargetLowPriorityNodes**.</span><span class="sxs-lookup"><span data-stu-id="12849-163">You can get or set hello value of hello service-defined variable **$TargetLowPriorityNodes**.</span></span>

-   <span data-ttu-id="12849-164">È possibile ottenere il valore di hello della variabile definito dal servizio hello **$CurrentLowPriorityNodes**.</span><span class="sxs-lookup"><span data-stu-id="12849-164">You can get hello value of hello service-defined variable **$CurrentLowPriorityNodes**.</span></span>

-   <span data-ttu-id="12849-165">È possibile ottenere il valore di hello della variabile definito dal servizio hello **$PreemptedNodeCount**.</span><span class="sxs-lookup"><span data-stu-id="12849-165">You can get hello value of hello service-defined variable **$PreemptedNodeCount**.</span></span> 
    <span data-ttu-id="12849-166">Questa variabile restituisce il numero di hello di nodi in hello stato interrotto e consente di aumentare o diminuire il numero di hello dei nodi dedicati, in base al numero di hello di nodi di annullamento che non sono disponibili.</span><span class="sxs-lookup"><span data-stu-id="12849-166">This variable returns hello number of nodes in hello preempted state and allows you to scale up or down hello number of dedicated nodes, depending on hello number of preempted nodes that are unavailable.</span></span>

## <a name="jobs-and-tasks"></a><span data-ttu-id="12849-167">Processi e attività</span><span class="sxs-lookup"><span data-stu-id="12849-167">Jobs and tasks</span></span>

<span data-ttu-id="12849-168">Processi e attività richiedono il supporto minimo per i nodi con priorità bassa. è supportata solo Hello è indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="12849-168">Jobs and tasks require very little support for low-priority nodes; hello only support is as follows:</span></span>

-   <span data-ttu-id="12849-169">Hello JobManagerTask proprietà di un processo ha una nuova proprietà, **AllowLowPriorityNode**.</span><span class="sxs-lookup"><span data-stu-id="12849-169">hello JobManagerTask property of a job has a new property, **AllowLowPriorityNode**.</span></span> 
    <span data-ttu-id="12849-170">Quando questa proprietà è true, è possibile programmare attività del gestore processi hello in un nodo dedicato o con priorità bassa.</span><span class="sxs-lookup"><span data-stu-id="12849-170">When this property is true, hello job manager task can be scheduled on either a dedicated or low-priority node.</span></span> <span data-ttu-id="12849-171">Se questa proprietà è false, attività del gestore processi hello sarà tooa pianificato solo nodo dedicato.</span><span class="sxs-lookup"><span data-stu-id="12849-171">If this property is false, hello job manager task will be scheduled tooa dedicated node only.</span></span>

-   <span data-ttu-id="12849-172">Un [variabile di ambiente](batch-compute-node-environment-variables.md) è disponibile tooa applicazione attività in modo che possa determinare se è in esecuzione in un nodo con priorità bassa o dedicato.</span><span class="sxs-lookup"><span data-stu-id="12849-172">An [environment variable](batch-compute-node-environment-variables.md) is available tooa task application so that it can determine whether it is running on a low-priority or dedicated node.</span></span> <span data-ttu-id="12849-173">variabile di ambiente Hello è AZ_BATCH_NODE_IS_DEDICATED.</span><span class="sxs-lookup"><span data-stu-id="12849-173">hello environment variable is AZ_BATCH_NODE_IS_DEDICATED.</span></span>

## <a name="handling-preemption"></a><span data-ttu-id="12849-174">Gestione delle priorità</span><span class="sxs-lookup"><span data-stu-id="12849-174">Handling preemption</span></span>

<span data-ttu-id="12849-175">Macchine virtuali in alcuni casi possono essere interrotta; In questo caso, hello Batch seguenti:</span><span class="sxs-lookup"><span data-stu-id="12849-175">VMs may occasionally be preempted; when this happens, Batch does hello following:</span></span>

-   <span data-ttu-id="12849-176">le macchine virtuali interrotto Hello avere lo stato di aggiornamento troppo**annullato**.</span><span class="sxs-lookup"><span data-stu-id="12849-176">hello preempted VMs have their state updated too**Preempted**.</span></span>
-   <span data-ttu-id="12849-177">Se l'attività in esecuzione in hello superata macchine virtuali del nodo, queste attività vengono reinserito nella coda e quindi eseguire di nuovo.</span><span class="sxs-lookup"><span data-stu-id="12849-177">If tasks were running on hello preempted node VMs, then those tasks are requeued and run again.</span></span>
-   <span data-ttu-id="12849-178">Hello macchina virtuale viene eliminata in modo efficace, iniziali tooany dati archiviati localmente nelle hello VM andrà perduta.</span><span class="sxs-lookup"><span data-stu-id="12849-178">hello VM is effectively deleted, leading tooany data stored locally on hello VM being lost.</span></span>
-   <span data-ttu-id="12849-179">pool di Hello tenterà continuamente tooreach hello destinazione numerosi nodi con priorità bassa disponibili.</span><span class="sxs-lookup"><span data-stu-id="12849-179">hello pool continually attempts tooreach hello target number of low-priority nodes available.</span></span> <span data-ttu-id="12849-180">Quando viene individuata una capacità di sostituzione, i nodi mantengono il proprio ID, ma vengono inizializzati di nuovo, attraversando gli stati **Creazione in corso** e **Avvio in corso** prima che siano disponibili per la pianificazione delle attività.</span><span class="sxs-lookup"><span data-stu-id="12849-180">When replacement capacity is found, the nodes keep their ids, but are re-initialized, going through **Creating** and **Starting** states before they are available for task scheduling.</span></span>
-   <span data-ttu-id="12849-181">Conteggi di priorità sono disponibili come metrica in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="12849-181">Preemption counts are available as a metric in hello Azure portal.</span></span>

## <a name="metrics"></a><span data-ttu-id="12849-182">Metrica</span><span class="sxs-lookup"><span data-stu-id="12849-182">Metrics</span></span>

<span data-ttu-id="12849-183">Nuova metrica è disponibile in hello [portale di Azure](https://portal.azure.com) per i nodi con priorità bassa.</span><span class="sxs-lookup"><span data-stu-id="12849-183">New metrics are available in hello [Azure portal](https://portal.azure.com) for low-priority nodes.</span></span> <span data-ttu-id="12849-184">Le metriche sono:</span><span class="sxs-lookup"><span data-stu-id="12849-184">These metrics are:</span></span>

- <span data-ttu-id="12849-185">Numero di nodi a bassa priorità</span><span class="sxs-lookup"><span data-stu-id="12849-185">Low-Priority Node Count</span></span>
- <span data-ttu-id="12849-186">Numero di core a bassa priorità</span><span class="sxs-lookup"><span data-stu-id="12849-186">Low-Priority Core Count</span></span> 
- <span data-ttu-id="12849-187">Numero di nodi annullati</span><span class="sxs-lookup"><span data-stu-id="12849-187">Preempted Node Count</span></span>

<span data-ttu-id="12849-188">metriche tooview in hello portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="12849-188">tooview metrics in hello Azure portal:</span></span>

1. <span data-ttu-id="12849-189">Passare tooyour account Batch nel portale di hello e visualizzare le impostazioni di hello per l'account Batch.</span><span class="sxs-lookup"><span data-stu-id="12849-189">Navigate tooyour Batch account in hello portal, and view hello settings for your Batch account.</span></span>
2. <span data-ttu-id="12849-190">Selezionare **metriche** da hello **monitoraggio** sezione.</span><span class="sxs-lookup"><span data-stu-id="12849-190">Select **Metrics** from hello **Monitoring** section.</span></span>
3. <span data-ttu-id="12849-191">Selezionare le metriche di hello desiderate hello **le metriche disponibili** elenco.</span><span class="sxs-lookup"><span data-stu-id="12849-191">Select hello metrics you desire from hello **Available Metrics** list.</span></span>

![Metriche per i nodi a priorità bassa](media/batch-low-pri-vms/low-pri-metrics.png)

## <a name="next-steps"></a><span data-ttu-id="12849-193">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="12849-193">Next steps</span></span>

* <span data-ttu-id="12849-194">Hello lettura [Cenni preliminari sulla funzionalità di Batch per gli sviluppatori](batch-api-basics.md), informazioni essenziale per chiunque preparazione toouse Batch.</span><span class="sxs-lookup"><span data-stu-id="12849-194">Read hello [Batch feature overview for developers](batch-api-basics.md), essential information for anyone preparing toouse Batch.</span></span> <span data-ttu-id="12849-195">articolo Hello contiene informazioni più dettagliate sulle risorse del servizio Batch come pool di nodi, processi e attività e hello molte funzionalità dell'API che è possibile utilizzare durante la compilazione dell'applicazione di Batch.</span><span class="sxs-lookup"><span data-stu-id="12849-195">hello article contains more detailed information about Batch service resources like pools, nodes, jobs, and tasks, and hello many API features that you can use while building your Batch application.</span></span>
* <span data-ttu-id="12849-196">Informazioni su hello [Batch API e strumenti](batch-apis-tools.md) disponibili per la creazione di soluzioni di Batch.</span><span class="sxs-lookup"><span data-stu-id="12849-196">Learn about hello [Batch APIs and tools](batch-apis-tools.md) available for building Batch solutions.</span></span>
