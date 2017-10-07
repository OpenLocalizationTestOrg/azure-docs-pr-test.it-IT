---
title: "multi-istanza aaaUse attività applicazioni MPI toorun - Azure Batch | Documenti Microsoft"
description: "Informazioni su come le applicazioni di interfaccia MPI (Message Passing) tooexecute utilizzando hello multi-istanza attività digitano in Batch di Azure."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 83e34bd7-a027-4b1b-8314-759384719327
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: 5/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b0e3295a6aeb76267c26d5504bcff59de3dc5e22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-multi-instance-tasks-toorun-message-passing-interface-mpi-applications-in-batch"></a><span data-ttu-id="704ff-103">Utilizzare le applicazioni multi-istanza attività toorun interfaccia MPI (Message Passing) in Batch</span><span class="sxs-lookup"><span data-stu-id="704ff-103">Use multi-instance tasks toorun Message Passing Interface (MPI) applications in Batch</span></span>

<span data-ttu-id="704ff-104">Attività di multi-istanza consentono toorun un'attività di Azure Batch in più nodi di calcolo contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="704ff-104">Multi-instance tasks allow you toorun an Azure Batch task on multiple compute nodes simultaneously.</span></span> <span data-ttu-id="704ff-105">e di abilitare scenari high performance computing, ad esempio le applicazioni MPI (Message Passing Interface) in Batch.</span><span class="sxs-lookup"><span data-stu-id="704ff-105">These tasks enable high performance computing scenarios like Message Passing Interface (MPI) applications in Batch.</span></span> <span data-ttu-id="704ff-106">In questo articolo viene illustrato come attività di multi-istanza tooexecute utilizzando hello [.NET per Batch] [ api_net] libreria.</span><span class="sxs-lookup"><span data-stu-id="704ff-106">In this article, you learn how tooexecute multi-instance tasks using hello [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> <span data-ttu-id="704ff-107">Mentre hello esempi in questo articolo illustrano .NET per Batch, MS-MPI, nodi di calcolo di Windows, concetti di attività di multi-istanza hello descritti di seguito sono applicabili tooother piattaforme e tecnologie (Python e Intel MPI in nodi di Linux, ad esempio).</span><span class="sxs-lookup"><span data-stu-id="704ff-107">While hello examples in this article focus on Batch .NET, MS-MPI, and Windows compute nodes, hello multi-instance task concepts discussed here are applicable tooother platforms and technologies (Python and Intel MPI on Linux nodes, for example).</span></span>
>
>

## <a name="multi-instance-task-overview"></a><span data-ttu-id="704ff-108">Panoramica sulle attività a istanze multiple</span><span class="sxs-lookup"><span data-stu-id="704ff-108">Multi-instance task overview</span></span>
<span data-ttu-id="704ff-109">Nel Batch, ogni attività sono in genere eseguita in un singolo nodo di calcolo, si invia più attività tooa processo e hello servizio Batch Pianifica ogni attività per l'esecuzione in un nodo.</span><span class="sxs-lookup"><span data-stu-id="704ff-109">In Batch, each task is normally executed on a single compute node--you submit multiple tasks tooa job, and hello Batch service schedules each task for execution on a node.</span></span> <span data-ttu-id="704ff-110">Tuttavia, tramite la configurazione di un'attività **le impostazioni di multi-istanza**, richiedere a Batch tooinstead creare un'attività principale e diverse sottoattività che vengono quindi eseguite su più nodi.</span><span class="sxs-lookup"><span data-stu-id="704ff-110">However, by configuring a task's **multi-instance settings**, you tell Batch tooinstead create one primary task and several subtasks that are then executed on multiple nodes.</span></span>

<span data-ttu-id="704ff-111">![Panoramica sulle attività a istanze multiple][1]</span><span class="sxs-lookup"><span data-stu-id="704ff-111">![Multi-instance task overview][1]</span></span>

<span data-ttu-id="704ff-112">Quando si invia un'attività con il processo di multi-istanza impostazioni tooa, Batch vengono eseguite diverse attività toomulti-istanza univoca di passaggi:</span><span class="sxs-lookup"><span data-stu-id="704ff-112">When you submit a task with multi-instance settings tooa job, Batch performs several steps unique toomulti-instance tasks:</span></span>

1. <span data-ttu-id="704ff-113">Hello servizio Batch crea uno **primario** e diversi **sottoattività** in base alle impostazioni di multi-istanza hello.</span><span class="sxs-lookup"><span data-stu-id="704ff-113">hello Batch service creates one **primary** and several **subtasks** based on hello multi-instance settings.</span></span> <span data-ttu-id="704ff-114">numero totale di Hello di attività (primaria e tutte le sottoattività) corrisponde a svariati hello **istanze** (nodi di calcolo) specificato nelle impostazioni di multi-istanza hello.</span><span class="sxs-lookup"><span data-stu-id="704ff-114">hello total number of tasks (primary plus all subtasks) matches hello number of **instances** (compute nodes) you specify in hello multi-instance settings.</span></span>
2. <span data-ttu-id="704ff-115">Batch consente di definire uno dei hello nodi di calcolo come hello **master**, e le pianificazioni hello tooexecute attività principale sul master hello.</span><span class="sxs-lookup"><span data-stu-id="704ff-115">Batch designates one of hello compute nodes as hello **master**, and schedules hello primary task tooexecute on hello master.</span></span> <span data-ttu-id="704ff-116">Consente di pianificare hello sottoattività tooexecute nel resto di hello dell'attività multi-istanza toohello allocato di nodi di calcolo di hello, uno sottoattività per ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="704ff-116">It schedules hello subtasks tooexecute on hello remainder of hello compute nodes allocated toohello multi-instance task, one subtask per node.</span></span>
3. <span data-ttu-id="704ff-117">scaricare Hello primaria e tutte le attività **file di risorse comuni** specificati nelle impostazioni di multi-istanza hello.</span><span class="sxs-lookup"><span data-stu-id="704ff-117">hello primary and all subtasks download any **common resource files** you specify in hello multi-instance settings.</span></span>
4. <span data-ttu-id="704ff-118">Dopo aver scaricato il file di risorse comuni hello, hello primaria e le sottoattività eseguire hello **comando coordinamento** specificati nelle impostazioni di multi-istanza hello.</span><span class="sxs-lookup"><span data-stu-id="704ff-118">After hello common resource files have been downloaded, hello primary and subtasks execute hello **coordination command** you specify in hello multi-instance settings.</span></span> <span data-ttu-id="704ff-119">comando di coordinamento Hello è nodi tooprepare in genere utilizzate per l'esecuzione di attività hello.</span><span class="sxs-lookup"><span data-stu-id="704ff-119">hello coordination command is typically used tooprepare nodes for executing hello task.</span></span> <span data-ttu-id="704ff-120">Può trattarsi di avvio di servizi in background (ad esempio [Microsoft MPI][msmpi_msdn]del `smpd.exe`) e verificare che i nodi di hello siano pronti tooprocess i messaggi tra i nodi.</span><span class="sxs-lookup"><span data-stu-id="704ff-120">This can include starting background services (such as [Microsoft MPI][msmpi_msdn]'s `smpd.exe`) and verifying that hello nodes are ready tooprocess inter-node messages.</span></span>
5. <span data-ttu-id="704ff-121">attività principale Hello esegue hello **comando applicazione** sul nodo principale hello *dopo* comando coordinamento hello è stata completata correttamente hello primaria e tutte le sottoattività.</span><span class="sxs-lookup"><span data-stu-id="704ff-121">hello primary task executes hello **application command** on hello master node *after* hello coordination command has been completed successfully by hello primary and all subtasks.</span></span> <span data-ttu-id="704ff-122">comando applicazione Hello è hello riga di comando hello multi-istanza attività stessa e viene eseguito solo da attività principale hello.</span><span class="sxs-lookup"><span data-stu-id="704ff-122">hello application command is hello command line of hello multi-instance task itself, and is executed only by hello primary task.</span></span> <span data-ttu-id="704ff-123">In una soluzione basata su [MS-MPI][msmpi_msdn], qui viene eseguita l'applicazione abilitata per MPI tramite `mpiexec.exe`.</span><span class="sxs-lookup"><span data-stu-id="704ff-123">In an [MS-MPI][msmpi_msdn]-based solution, this is where you execute your MPI-enabled application using `mpiexec.exe`.</span></span>

> [!NOTE]
> <span data-ttu-id="704ff-124">Se è funzionalmente distinto, hello "attività di multi-istanza" non è un tipo di attività univoco come hello [StartTask] [ net_starttask] o [JobPreparationTask] [ net_jobprep].</span><span class="sxs-lookup"><span data-stu-id="704ff-124">Though it is functionally distinct, hello "multi-instance task" is not a unique task type like hello [StartTask][net_starttask] or [JobPreparationTask][net_jobprep].</span></span> <span data-ttu-id="704ff-125">attività di multi-istanza Hello è semplicemente un'attività di Batch standard ([CloudTask] [ net_task] in .NET per Batch) sono state configurate le cui impostazioni di multi-istanza.</span><span class="sxs-lookup"><span data-stu-id="704ff-125">hello multi-instance task is simply a standard Batch task ([CloudTask][net_task] in Batch .NET) whose multi-instance settings have been configured.</span></span> <span data-ttu-id="704ff-126">In questo articolo verrà fatto riferimento toothis come hello **attività multi-istanza**.</span><span class="sxs-lookup"><span data-stu-id="704ff-126">In this article, we refer toothis as hello **multi-instance task**.</span></span>
>
>

## <a name="requirements-for-multi-instance-tasks"></a><span data-ttu-id="704ff-127">Requisiti delle attività a istanze multiple</span><span class="sxs-lookup"><span data-stu-id="704ff-127">Requirements for multi-instance tasks</span></span>
<span data-ttu-id="704ff-128">Per le attività a istanze multiple è necessario un pool in cui sia **abilitata la comunicazione tra i nodi** e **disabilitata l'esecuzione di attività simultanee**.</span><span class="sxs-lookup"><span data-stu-id="704ff-128">Multi-instance tasks require a pool with **inter-node communication enabled**, and with **concurrent task execution disabled**.</span></span> <span data-ttu-id="704ff-129">esecuzione di attività simultanee toodisable, hello set [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) too1 di proprietà.</span><span class="sxs-lookup"><span data-stu-id="704ff-129">toodisable concurrent task execution, set hello [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) property too1.</span></span>

<span data-ttu-id="704ff-130">Questo frammento di codice viene illustrato come le attività utilizzando una libreria .NET di Batch di hello toocreate un pool per multi-istanza.</span><span class="sxs-lookup"><span data-stu-id="704ff-130">This code snippet shows how toocreate a pool for multi-instance tasks using hello Batch .NET library.</span></span>

```csharp
CloudPool myCloudPool =
    myBatchClient.PoolOperations.CreatePool(
        poolId: "MultiInstanceSamplePool",
        targetDedicatedComputeNodes: 3
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Multi-instance tasks require inter-node communication, and those nodes
// must run only one task at a time.
myCloudPool.InterComputeNodeCommunicationEnabled = true;
myCloudPool.MaxTasksPerComputeNode = 1;
```

> [!NOTE]
> <span data-ttu-id="704ff-131">Se si tenta di toorun disabilitata un'attività a più istanze in un pool con le comunicazioni, o con un *maxTasksPerNode* valore maggiore di 1, l'attività hello non è pianificata come mai - all'infinito rimane nello stato "attivo" hello.</span><span class="sxs-lookup"><span data-stu-id="704ff-131">If you try toorun a multi-instance task in a pool with internode communication disabled, or with a *maxTasksPerNode* value greater than 1, hello task is never scheduled--it remains indefinitely in hello "active" state.</span></span> 
>
> <span data-ttu-id="704ff-132">Le attività a istanze multiple possono essere eseguite solo in nodi di pool creati dopo il 14 dicembre 2015.</span><span class="sxs-lookup"><span data-stu-id="704ff-132">Multi-instance tasks can execute only on nodes in pools created after 14 December 2015.</span></span>
>
>

### <a name="use-a-starttask-tooinstall-mpi"></a><span data-ttu-id="704ff-133">Utilizzare un tooinstall StartTask MPI</span><span class="sxs-lookup"><span data-stu-id="704ff-133">Use a StartTask tooinstall MPI</span></span>
<span data-ttu-id="704ff-134">toorun di applicazioni MPI con un'attività a più istanze, è necessario innanzitutto tooinstall un'implementazione MPI (MS-MPI o MPI Intel, ad esempio) sui nodi di calcolo hello nel pool di hello.</span><span class="sxs-lookup"><span data-stu-id="704ff-134">toorun MPI applications with a multi-instance task, you first need tooinstall an MPI implementation (MS-MPI or Intel MPI, for example) on hello compute nodes in hello pool.</span></span> <span data-ttu-id="704ff-135">Si tratta di un toouse tempestivamente un [StartTask][net_starttask], che viene eseguito ogni volta che un nodo viene aggiunto un pool o viene riavviato.</span><span class="sxs-lookup"><span data-stu-id="704ff-135">This is a good time toouse a [StartTask][net_starttask], which executes whenever a node joins a pool, or is restarted.</span></span> <span data-ttu-id="704ff-136">Questo frammento di codice crea un StartTask che specifica il pacchetto di installazione hello MS-MPI come un [file di risorse][net_resourcefile].</span><span class="sxs-lookup"><span data-stu-id="704ff-136">This code snippet creates a StartTask that specifies hello MS-MPI setup package as a [resource file][net_resourcefile].</span></span> <span data-ttu-id="704ff-137">riga di comando dell'attività di avvio Hello viene eseguita dopo che il file di risorse di hello è scaricato toohello nodo.</span><span class="sxs-lookup"><span data-stu-id="704ff-137">hello start task's command line is executed after hello resource file is downloaded toohello node.</span></span> <span data-ttu-id="704ff-138">In questo caso, la riga di comando hello esegue un'installazione automatica di MS-MPI.</span><span class="sxs-lookup"><span data-stu-id="704ff-138">In this case, hello command line performs an unattended install of MS-MPI.</span></span>

```csharp
// Create a StartTask for hello pool which we use for installing MS-MPI on
// hello nodes as they join hello pool (or when they are restarted).
StartTask startTask = new StartTask
{
    CommandLine = "cmd /c MSMpiSetup.exe -unattend -force",
    ResourceFiles = new List<ResourceFile> { new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MSMpiSetup.exe", "MSMpiSetup.exe") },
    UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin)),
    WaitForSuccess = true
};
myCloudPool.StartTask = startTask;

// Commit hello fully configured pool toohello Batch service tooactually create
// hello pool and its compute nodes.
await myCloudPool.CommitAsync();
```

### <a name="remote-direct-memory-access-rdma"></a><span data-ttu-id="704ff-139">Accesso diretto a memoria remota (RDMA)</span><span class="sxs-lookup"><span data-stu-id="704ff-139">Remote direct memory access (RDMA)</span></span>
<span data-ttu-id="704ff-140">Quando si sceglie un [dimensioni che supportano RDMA](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) , ad esempio A9 per hello nodi di calcolo nel pool di Batch, l'applicazione MPI può usufruire di prestazioni elevate, bassa latenza diretto a memoria remota (RDMA) di accesso di rete di Azure.</span><span class="sxs-lookup"><span data-stu-id="704ff-140">When you choose an [RDMA-capable size](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) such as A9 for hello compute nodes in your Batch pool, your MPI application can take advantage of Azure's high-performance, low-latency remote direct memory access (RDMA) network.</span></span>

<span data-ttu-id="704ff-141">Cercare le dimensioni di hello specificate come "Che supporta RDMA" in hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="704ff-141">Look for hello sizes specified as "RDMA capable" in hello following articles:</span></span>

* <span data-ttu-id="704ff-142">Pool **CloudServiceConfiguration**</span><span class="sxs-lookup"><span data-stu-id="704ff-142">**CloudServiceConfiguration** pools</span></span>

  * <span data-ttu-id="704ff-143">[Dimensioni dei servizi cloud](../cloud-services/cloud-services-sizes-specs.md) (solo Windows)</span><span class="sxs-lookup"><span data-stu-id="704ff-143">[Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md) (Windows only)</span></span>
* <span data-ttu-id="704ff-144">Pool **VirtualMachineConfiguration**</span><span class="sxs-lookup"><span data-stu-id="704ff-144">**VirtualMachineConfiguration** pools</span></span>

  * <span data-ttu-id="704ff-145">[Dimensioni delle macchine virtuali in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)</span><span class="sxs-lookup"><span data-stu-id="704ff-145">[Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)</span></span>
  * <span data-ttu-id="704ff-146">[Dimensioni delle macchine virtuali in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)</span><span class="sxs-lookup"><span data-stu-id="704ff-146">[Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)</span></span>

> [!NOTE]
> <span data-ttu-id="704ff-147">vantaggio tootake RDMA in [nodi di calcolo Linux](batch-linux-nodes.md), è necessario utilizzare **Intel MPI** nei nodi hello.</span><span class="sxs-lookup"><span data-stu-id="704ff-147">tootake advantage of RDMA on [Linux compute nodes](batch-linux-nodes.md), you must use **Intel MPI** on hello nodes.</span></span> <span data-ttu-id="704ff-148">Per ulteriori informazioni sui pool CloudServiceConfiguration e VirtualMachineConfiguration, vedere la sezione Pool di hello hello [Cenni preliminari sulle funzionalità di Batch](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="704ff-148">For more information on CloudServiceConfiguration and VirtualMachineConfiguration pools, see hello Pool section of hello [Batch feature overview](batch-api-basics.md).</span></span>
>
>

## <a name="create-a-multi-instance-task-with-batch-net"></a><span data-ttu-id="704ff-149">Creare un'attività a istanze multiple con Batch .NET</span><span class="sxs-lookup"><span data-stu-id="704ff-149">Create a multi-instance task with Batch .NET</span></span>
<span data-ttu-id="704ff-150">Ora che abbiamo trattato requisiti pool hello e installazione del pacchetto MPI, creare attività di multi-istanza hello.</span><span class="sxs-lookup"><span data-stu-id="704ff-150">Now that we've covered hello pool requirements and MPI package installation, let's create hello multi-instance task.</span></span> <span data-ttu-id="704ff-151">In questo frammento di codice viene creato un oggetto [CloudTask][net_task] standard e viene quindi configurata la relativa proprietà [MultiInstanceSettings][net_multiinstance_prop].</span><span class="sxs-lookup"><span data-stu-id="704ff-151">In this snippet, we create a standard [CloudTask][net_task], then configure its [MultiInstanceSettings][net_multiinstance_prop] property.</span></span> <span data-ttu-id="704ff-152">Come accennato in precedenza, hello multi-istanza attività non è un tipo di attività distinto, ma un'attività Batch standard configurato con le impostazioni di multi-istanza.</span><span class="sxs-lookup"><span data-stu-id="704ff-152">As mentioned earlier, hello multi-instance task is not a distinct task type, but a standard Batch task configured with multi-instance settings.</span></span>

```csharp
// Create hello multi-instance task. Its command line is hello "application command"
// and will be executed *only* by hello primary, and only after hello primary and
// subtasks execute hello CoordinationCommandLine.
CloudTask myMultiInstanceTask = new CloudTask(id: "mymultiinstancetask",
    commandline: "cmd /c mpiexec.exe -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe");

// Configure hello task's MultiInstanceSettings. hello CoordinationCommandLine will be executed by
// hello primary and all subtasks.
myMultiInstanceTask.MultiInstanceSettings =
    new MultiInstanceSettings(numberOfNodes) {
    CoordinationCommandLine = @"cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d",
    CommonResourceFiles = new List<ResourceFile> {
    new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MyMPIApplication.exe",
                     "MyMPIApplication.exe")
    }
};

// Submit hello task toohello job. Batch will take care of splitting it into subtasks and
// scheduling them for execution on hello nodes.
await myBatchClient.JobOperations.AddTaskAsync("mybatchjob", myMultiInstanceTask);
```

## <a name="primary-task-and-subtasks"></a><span data-ttu-id="704ff-153">Attività primaria e sottoattività</span><span class="sxs-lookup"><span data-stu-id="704ff-153">Primary task and subtasks</span></span>
<span data-ttu-id="704ff-154">Quando si crea hello le impostazioni di multi-istanza per un'attività, viene specificato il numero di hello dei nodi di calcolo che sono attività hello tooexecute.</span><span class="sxs-lookup"><span data-stu-id="704ff-154">When you create hello multi-instance settings for a task, you specify hello number of compute nodes that are tooexecute hello task.</span></span> <span data-ttu-id="704ff-155">Quando si inviano processi di tooa attività hello, hello servizio Batch crea uno **primario** attività e sufficiente **sottoattività** che insieme corrispondente hello al numero di nodi specificato.</span><span class="sxs-lookup"><span data-stu-id="704ff-155">When you submit hello task tooa job, hello Batch service creates one **primary** task and enough **subtasks** that together match hello number of nodes you specified.</span></span>

<span data-ttu-id="704ff-156">Queste attività vengono assegnate un id di tipo integer nell'intervallo di hello 0 troppo*numberOfInstances* - 1.</span><span class="sxs-lookup"><span data-stu-id="704ff-156">These tasks are assigned an integer id in hello range of 0 too*numberOfInstances* - 1.</span></span> <span data-ttu-id="704ff-157">Hello attività con id 0 è hello primario e tutti gli altri ID sono sottoattività.</span><span class="sxs-lookup"><span data-stu-id="704ff-157">hello task with id 0 is hello primary task, and all other ids are subtasks.</span></span> <span data-ttu-id="704ff-158">Ad esempio, se si crea hello seguendo le impostazioni di multi-istanza per un'attività, attività principale hello avrebbe un id pari a 0 e hello sottoattività avrebbe ID 1 a 9.</span><span class="sxs-lookup"><span data-stu-id="704ff-158">For example, if you create hello following multi-instance settings for a task, hello primary task would have an id of 0, and hello subtasks would have ids 1 through 9.</span></span>

```csharp
int numberOfNodes = 10;
myMultiInstanceTask.MultiInstanceSettings = new MultiInstanceSettings(numberOfNodes);
```

### <a name="master-node"></a><span data-ttu-id="704ff-159">Nodo master</span><span class="sxs-lookup"><span data-stu-id="704ff-159">Master node</span></span>
<span data-ttu-id="704ff-160">Quando si invia un'attività a più istanze, hello servizio Batch ne definisce uno di hello nodi di calcolo come nodo "master" hello e pianificazioni hello tooexecute attività principale nel nodo principale hello.</span><span class="sxs-lookup"><span data-stu-id="704ff-160">When you submit a multi-instance task, hello Batch service designates one of hello compute nodes as hello "master" node, and schedules hello primary task tooexecute on hello master node.</span></span> <span data-ttu-id="704ff-161">Hello sottoattività sono pianificati tooexecute nel resto di hello dei nodi di hello allocata toohello attività di multi-istanza.</span><span class="sxs-lookup"><span data-stu-id="704ff-161">hello subtasks are scheduled tooexecute on hello remainder of hello nodes allocated toohello multi-instance task.</span></span>

## <a name="coordination-command"></a><span data-ttu-id="704ff-162">comando di coordinamento</span><span class="sxs-lookup"><span data-stu-id="704ff-162">Coordination command</span></span>
<span data-ttu-id="704ff-163">Hello **comando coordinamento** viene eseguito sia hello primaria e le sottoattività.</span><span class="sxs-lookup"><span data-stu-id="704ff-163">hello **coordination command** is executed by both hello primary and subtasks.</span></span>

<span data-ttu-id="704ff-164">chiamata di Hello del comando di coordinamento hello sta bloccando - Batch non viene eseguito il comando dell'applicazione hello fino a quando il comando di coordinamento hello ha restituito correttamente per tutte le sottoattività.</span><span class="sxs-lookup"><span data-stu-id="704ff-164">hello invocation of hello coordination command is blocking--Batch does not execute hello application command until hello coordination command has returned successfully for all subtasks.</span></span> <span data-ttu-id="704ff-165">comando coordinamento Hello deve pertanto avviare tutti i servizi in background necessarie, verificare che siano pronti per l'utilizzo e uscire.</span><span class="sxs-lookup"><span data-stu-id="704ff-165">hello coordination command should therefore start any required background services, verify that they are ready for use, and then exit.</span></span> <span data-ttu-id="704ff-166">Questo comando di coordinamento per una soluzione utilizzando la versione 7 MS-MPI, ad esempio, avvia il servizio SMPD hello nel nodo di hello, quindi viene chiuso:</span><span class="sxs-lookup"><span data-stu-id="704ff-166">For example, this coordination command for a solution using MS-MPI version 7 starts hello SMPD service on hello node, then exits:</span></span>

```
cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d
```

<span data-ttu-id="704ff-167">Si noti hello utilizzo di `start` in questo comando di coordinamento.</span><span class="sxs-lookup"><span data-stu-id="704ff-167">Note hello use of `start` in this coordination command.</span></span> <span data-ttu-id="704ff-168">Questa operazione è necessaria perché hello `smpd.exe` applicazione non viene restituito immediatamente dopo l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="704ff-168">This is required because hello `smpd.exe` application does not return immediately after execution.</span></span> <span data-ttu-id="704ff-169">Senza usare hello hello [avviare] [ cmd_start] dei comandi, non verrà restituito da questo comando di coordinamento e pertanto bloccano hello applicazione esecuzione comando.</span><span class="sxs-lookup"><span data-stu-id="704ff-169">Without hello use of hello [start][cmd_start] command, this coordination command would not return, and would therefore block hello application command from running.</span></span>

## <a name="application-command"></a><span data-ttu-id="704ff-170">Comando applicazione</span><span class="sxs-lookup"><span data-stu-id="704ff-170">Application command</span></span>
<span data-ttu-id="704ff-171">Una volta attività principale hello e tutte le attività terminata l'esecuzione di comandi di coordinamento hello, riga di comando dell'attività di hello multi-istanza viene eseguita dall'attività primaria hello *solo*.</span><span class="sxs-lookup"><span data-stu-id="704ff-171">Once hello primary task and all subtasks have finished executing hello coordination command, hello multi-instance task's command line is executed by hello primary task *only*.</span></span> <span data-ttu-id="704ff-172">Viene chiamato questo hello **comando applicazione** toodistinguish dal comando di coordinamento hello.</span><span class="sxs-lookup"><span data-stu-id="704ff-172">We call this hello **application command** toodistinguish it from hello coordination command.</span></span>

<span data-ttu-id="704ff-173">Per le applicazioni di MS-MPI, utilizzare hello tooexecute comando applicazione dell'applicazione abilitata MPI con `mpiexec.exe`.</span><span class="sxs-lookup"><span data-stu-id="704ff-173">For MS-MPI applications, use hello application command tooexecute your MPI-enabled application with `mpiexec.exe`.</span></span> <span data-ttu-id="704ff-174">Di seguito è riportato, a titolo di esempio, il comando applicazione per una soluzione con MS-MPI versione 7:</span><span class="sxs-lookup"><span data-stu-id="704ff-174">For example, here is an application command for a solution using MS-MPI version 7:</span></span>

```
cmd /c ""%MSMPI_BIN%\mpiexec.exe"" -c 1 -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe
```

> [!NOTE]
> <span data-ttu-id="704ff-175">Poiché MS-MPI `mpiexec.exe` utilizza hello `CCP_NODES` variabile per impostazione predefinita (vedere [le variabili di ambiente](#environment-variables)) esempio hello esclusa applicazione riga di comando riportata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="704ff-175">Because MS-MPI's `mpiexec.exe` uses hello `CCP_NODES` variable by default (see [Environment variables](#environment-variables)) hello example application command line above excludes it.</span></span>
>
>

## <a name="environment-variables"></a><span data-ttu-id="704ff-176">Variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="704ff-176">Environment variables</span></span>
<span data-ttu-id="704ff-177">Crea più batch [le variabili di ambiente] [ msdn_env_var] attività istanza toomulti specifica hello nodi allocata tooa attività di più istanze di calcolo.</span><span class="sxs-lookup"><span data-stu-id="704ff-177">Batch creates several [environment variables][msdn_env_var] specific toomulti-instance tasks on hello compute nodes allocated tooa multi-instance task.</span></span> <span data-ttu-id="704ff-178">Le righe di comando di coordinamento e l'applicazione può fare riferimento a queste variabili di ambiente, possono hello script e programmi che vengono eseguiti.</span><span class="sxs-lookup"><span data-stu-id="704ff-178">Your coordination and application command lines can reference these environment variables, as can hello scripts and programs they execute.</span></span>

<span data-ttu-id="704ff-179">Hello seguenti variabili di ambiente vengono create dal servizio Batch hello per l'utilizzo dalle attività di multi-istanza:</span><span class="sxs-lookup"><span data-stu-id="704ff-179">hello following environment variables are created by hello Batch service for use by multi-instance tasks:</span></span>

* `CCP_NODES`
* `AZ_BATCH_NODE_LIST`
* `AZ_BATCH_HOST_LIST`
* `AZ_BATCH_MASTER_NODE`
* `AZ_BATCH_TASK_SHARED_DIR`
* `AZ_BATCH_IS_CURRENT_NODE_MASTER`

<span data-ttu-id="704ff-180">Per i dettagli completi su questi e hello altri Batch calcolo nodo variabili di ambiente, inclusi i contenuti e la visibilità, vedere [le variabili di ambiente nodo di calcolo][msdn_env_var].</span><span class="sxs-lookup"><span data-stu-id="704ff-180">For full details on these and hello other Batch compute node environment variables, including their contents and visibility, see [Compute node environment variables][msdn_env_var].</span></span>

> [!TIP]
> <span data-ttu-id="704ff-181">Nell'esempio di codice Hello MPI Linux Batch contiene un esempio di come è possibile usare alcune di queste variabili di ambiente.</span><span class="sxs-lookup"><span data-stu-id="704ff-181">hello Batch Linux MPI code sample contains an example of how several of these environment variables can be used.</span></span> <span data-ttu-id="704ff-182">Hello [coordinamento cmd] [ coord_cmd_example] Bash script Scarica i file di input e di applicazione comune da archiviazione di Azure, consente a una condivisione di File System NFS (Network) nel nodo principale hello e configura hello altri nodi allocato attività multi-istanza toohello come i client NFS.</span><span class="sxs-lookup"><span data-stu-id="704ff-182">hello [coordination-cmd][coord_cmd_example] Bash script downloads common application and input files from Azure Storage, enables a Network File System (NFS) share on hello master node, and configures hello other nodes allocated toohello multi-instance task as NFS clients.</span></span>
>
>

## <a name="resource-files"></a><span data-ttu-id="704ff-183">File di risorse</span><span class="sxs-lookup"><span data-stu-id="704ff-183">Resource files</span></span>
<span data-ttu-id="704ff-184">Esistono due set di tooconsider i file di risorse per le attività di multi-istanza: **file di risorse comuni** che *tutti* attività scaricare (principali e sottoattività), hello e **ifiledirisorse** specificato per hello multi-istanza dell'attività stessa, che *solo hello primario* attività di download.</span><span class="sxs-lookup"><span data-stu-id="704ff-184">There are two sets of resource files tooconsider for multi-instance tasks: **common resource files** that *all* tasks download (both primary and subtasks), and hello **resource files** specified for hello multi-instance task itself, which *only hello primary* task downloads.</span></span>

<span data-ttu-id="704ff-185">È possibile specificare uno o più **file di risorse comuni** nelle impostazioni di multi-istanza hello per un'attività.</span><span class="sxs-lookup"><span data-stu-id="704ff-185">You can specify one or more **common resource files** in hello multi-instance settings for a task.</span></span> <span data-ttu-id="704ff-186">Questi file di risorse comuni vengono scaricati da [di archiviazione di Azure](../storage/common/storage-introduction.md) in ogni nodo **directory condivisa attività** hello primaria e tutte le sottoattività.</span><span class="sxs-lookup"><span data-stu-id="704ff-186">These common resource files are downloaded from [Azure Storage](../storage/common/storage-introduction.md) into each node's **task shared directory** by hello primary and all subtasks.</span></span> <span data-ttu-id="704ff-187">È possibile accedere directory condivisa di hello attività dalle righe di comando dell'applicazione e coordinamento tramite hello `AZ_BATCH_TASK_SHARED_DIR` variabile di ambiente.</span><span class="sxs-lookup"><span data-stu-id="704ff-187">You can access hello task shared directory from application and coordination command lines by using hello `AZ_BATCH_TASK_SHARED_DIR` environment variable.</span></span> <span data-ttu-id="704ff-188">Hello `AZ_BATCH_TASK_SHARED_DIR` percorso è identico in ogni attività di multi-istanza nodo toohello allocato, pertanto è possibile condividere un comando singolo coordinamento tra hello primaria e tutte le attività.</span><span class="sxs-lookup"><span data-stu-id="704ff-188">hello `AZ_BATCH_TASK_SHARED_DIR` path is identical on every node allocated toohello multi-instance task, thus you can share a single coordination command between hello primary and all subtasks.</span></span> <span data-ttu-id="704ff-189">Batch "condividono" hello directory in senso di accesso remoto, ma è possibile utilizzarlo come un montaggio o punto come indicato in precedenza in suggerimento hello sulle variabili di ambiente di condivisione.</span><span class="sxs-lookup"><span data-stu-id="704ff-189">Batch does not "share" hello directory in a remote access sense, but you can use it as a mount or share point as mentioned earlier in hello tip on environment variables.</span></span>

<span data-ttu-id="704ff-190">File di risorse che specificano per hello attività multi-istanza stessa directory di lavoro dell'attività toohello scaricato, `AZ_BATCH_TASK_WORKING_DIR`, per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="704ff-190">Resource files that you specify for hello multi-instance task itself are downloaded toohello task's working directory, `AZ_BATCH_TASK_WORKING_DIR`, by default.</span></span> <span data-ttu-id="704ff-191">Come accennato, invece toocommon file di risorse, unica attività primaria hello Scarica i file di risorse specificati per l'attività di hello multi-istanza stessa.</span><span class="sxs-lookup"><span data-stu-id="704ff-191">As mentioned, in contrast toocommon resource files, only hello primary task downloads resource files specified for hello  multi-instance task itself.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="704ff-192">Utilizzare sempre le variabili di ambiente hello `AZ_BATCH_TASK_SHARED_DIR` e `AZ_BATCH_TASK_WORKING_DIR` directory toothese toorefer le righe di comando.</span><span class="sxs-lookup"><span data-stu-id="704ff-192">Always use hello environment variables `AZ_BATCH_TASK_SHARED_DIR` and `AZ_BATCH_TASK_WORKING_DIR` toorefer toothese directories in your command lines.</span></span> <span data-ttu-id="704ff-193">Non tentare percorsi hello tooconstruct manualmente.</span><span class="sxs-lookup"><span data-stu-id="704ff-193">Do not attempt tooconstruct hello paths manually.</span></span>
>
>

## <a name="task-lifetime"></a><span data-ttu-id="704ff-194">Durata dell'attività</span><span class="sxs-lookup"><span data-stu-id="704ff-194">Task lifetime</span></span>
<span data-ttu-id="704ff-195">durata Hello di hello attività principale controlli hello intera durata di hello multi-istanza intera attività.</span><span class="sxs-lookup"><span data-stu-id="704ff-195">hello lifetime of hello primary task controls hello lifetime of hello entire multi-instance task.</span></span> <span data-ttu-id="704ff-196">Quando si chiude hello primario, vengono terminate tutte hello sottoattività.</span><span class="sxs-lookup"><span data-stu-id="704ff-196">When hello primary exits, all of hello subtasks are terminated.</span></span> <span data-ttu-id="704ff-197">codice di uscita Hello di hello primario è il codice di uscita hello dell'attività hello, pertanto riuscita di hello toodetermine utilizzato o meno delle attività hello per scopi di tentativi.</span><span class="sxs-lookup"><span data-stu-id="704ff-197">hello exit code of hello primary is hello exit code of hello task, and is therefore used toodetermine hello success or failure of hello task for retry purposes.</span></span>

<span data-ttu-id="704ff-198">Se una delle sottoattività hello hanno esito negativo, chiusura con codice restituito diverso da zero, ad esempio, hello multi-istanza intera attività ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="704ff-198">If any of hello subtasks fail, exiting with a non-zero return code, for example, hello entire multi-instance task fails.</span></span> <span data-ttu-id="704ff-199">attività di multi-istanza Hello viene quindi terminata e ritentata, backup tooits limite di tentativi.</span><span class="sxs-lookup"><span data-stu-id="704ff-199">hello multi-instance task is then terminated and retried, up tooits retry limit.</span></span>

<span data-ttu-id="704ff-200">Quando si elimina un'attività a più istanze, hello primaria e tutte le attività vengono eliminate anche dal servizio Batch hello.</span><span class="sxs-lookup"><span data-stu-id="704ff-200">When you delete a multi-instance task, hello primary and all subtasks are also deleted by hello Batch service.</span></span> <span data-ttu-id="704ff-201">Tutti sottoattività directory e i relativi file vengono eliminati dai nodi di calcolo hello, come per un'attività standard.</span><span class="sxs-lookup"><span data-stu-id="704ff-201">All subtask directories and their files are deleted from hello compute nodes, just as for a standard task.</span></span>

<span data-ttu-id="704ff-202">[TaskConstraints] [ net_taskconstraints] per un'attività di multi-istanza, ad esempio hello [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime] [ net_taskconstraint_maxwallclock], e [RetentionTime] [ net_taskconstraint_retention] vengono rispettate le proprietà, in quanto sono per un'attività standard e applicare toohello primario e tutte le sottoattività.</span><span class="sxs-lookup"><span data-stu-id="704ff-202">[TaskConstraints][net_taskconstraints] for a multi-instance task, such as hello [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime][net_taskconstraint_maxwallclock], and [RetentionTime][net_taskconstraint_retention] properties, are honored as they are for a standard task, and apply toohello primary and all subtasks.</span></span> <span data-ttu-id="704ff-203">Tuttavia, se si modifica hello [RetentionTime] [ net_taskconstraint_retention] proprietà dopo l'aggiunta di hello multi-istanza attività toohello processo, questa modifica è l'attività principale toohello solo applicato.</span><span class="sxs-lookup"><span data-stu-id="704ff-203">However, if you change hello [RetentionTime][net_taskconstraint_retention] property after adding hello multi-instance task toohello job, this change is applied only toohello primary task.</span></span> <span data-ttu-id="704ff-204">Tutte le sottoattività hello continuare toouse hello originale [RetentionTime][net_taskconstraint_retention].</span><span class="sxs-lookup"><span data-stu-id="704ff-204">All of hello subtasks continue toouse hello original [RetentionTime][net_taskconstraint_retention].</span></span>

<span data-ttu-id="704ff-205">Elenco attività recenti del nodo di calcolo riflette id hello di una sottoattività se attività recente hello faceva parte di un'attività di multi-istanza.</span><span class="sxs-lookup"><span data-stu-id="704ff-205">A compute node's recent task list reflects hello id of a subtask if hello recent task was part of a multi-instance task.</span></span>

## <a name="obtain-information-about-subtasks"></a><span data-ttu-id="704ff-206">Ottenere informazioni sulle sottoattività</span><span class="sxs-lookup"><span data-stu-id="704ff-206">Obtain information about subtasks</span></span>
<span data-ttu-id="704ff-207">informazioni tooobtain su sottoattività tramite la libreria .NET di Batch di hello, chiamata hello [CloudTask.ListSubtasks] [ net_task_listsubtasks] metodo.</span><span class="sxs-lookup"><span data-stu-id="704ff-207">tooobtain information on subtasks by using hello Batch .NET library, call hello [CloudTask.ListSubtasks][net_task_listsubtasks] method.</span></span> <span data-ttu-id="704ff-208">Questo metodo restituisce informazioni su tutte le attività e informazioni su hello calcolo nodo hello attività eseguite.</span><span class="sxs-lookup"><span data-stu-id="704ff-208">This method returns information on all subtasks, and information about hello compute node that executed hello tasks.</span></span> <span data-ttu-id="704ff-209">Tali informazioni, è possibile determinare directory radice del ciascuna sottoattività id del pool di hello, lo stato corrente, codice di uscita e più.</span><span class="sxs-lookup"><span data-stu-id="704ff-209">From this information, you can determine each subtask's root directory, hello pool id, its current state, exit code, and more.</span></span> <span data-ttu-id="704ff-210">È possibile utilizzare queste informazioni in combinazione con hello [PoolOperations.GetNodeFile] [ poolops_getnodefile] i file della sottoattività di metodo tooobtain hello.</span><span class="sxs-lookup"><span data-stu-id="704ff-210">You can use this information in combination with hello [PoolOperations.GetNodeFile][poolops_getnodefile] method tooobtain hello subtask's files.</span></span> <span data-ttu-id="704ff-211">Si noti che questo metodo non restituisce informazioni per l'attività principale hello (id 0).</span><span class="sxs-lookup"><span data-stu-id="704ff-211">Note that this method does not return information for hello primary task (id 0).</span></span>

> [!NOTE]
> <span data-ttu-id="704ff-212">Se non diversamente specificato, i metodi .NET per Batch che operano su hello multi-istanza [CloudTask] [ net_task] stesso applicare *solo* toohello di attività principale.</span><span class="sxs-lookup"><span data-stu-id="704ff-212">Unless otherwise stated, Batch .NET methods that operate on hello multi-instance [CloudTask][net_task] itself apply *only* toohello primary task.</span></span> <span data-ttu-id="704ff-213">Ad esempio, quando si chiama hello [CloudTask.ListNodeFiles] [ net_task_listnodefiles] metodo su un'attività a più istanze, vengono restituiti solo i file dell'attività di hello primario.</span><span class="sxs-lookup"><span data-stu-id="704ff-213">For example, when you call hello [CloudTask.ListNodeFiles][net_task_listnodefiles] method on a multi-instance task, only hello primary task's files are returned.</span></span>
>
>

<span data-ttu-id="704ff-214">Hello frammento di codice seguente viene illustrato come tooobtain sottoattività informazioni e come richiedere il contenuto del file da nodi hello in cui è stato eseguito.</span><span class="sxs-lookup"><span data-stu-id="704ff-214">hello following code snippet shows how tooobtain subtask information, as well as request file contents from hello nodes on which they executed.</span></span>

```csharp
// Obtain hello job and hello multi-instance task from hello Batch service
CloudJob boundJob = batchClient.JobOperations.GetJob("mybatchjob");
CloudTask myMultiInstanceTask = boundJob.GetTask("mymultiinstancetask");

// Now obtain hello list of subtasks for hello task
IPagedEnumerable<SubtaskInformation> subtasks = myMultiInstanceTask.ListSubtasks();

// Asynchronously iterate over hello subtasks and print their stdout and stderr
// output if hello subtask has completed
await subtasks.ForEachAsync(async (subtask) =>
{
    Console.WriteLine("subtask: {0}", subtask.Id);
    Console.WriteLine("exit code: {0}", subtask.ExitCode);

    if (subtask.State == SubtaskState.Completed)
    {
        ComputeNode node =
            await batchClient.PoolOperations.GetComputeNodeAsync(subtask.ComputeNodeInformation.PoolId,
                                                                 subtask.ComputeNodeInformation.ComputeNodeId);

        NodeFile stdOutFile = await node.GetNodeFileAsync(subtask.ComputeNodeInformation.TaskRootDirectory + "\\" + Constants.StandardOutFileName);
        NodeFile stdErrFile = await node.GetNodeFileAsync(subtask.ComputeNodeInformation.TaskRootDirectory + "\\" + Constants.StandardErrorFileName);
        stdOut = await stdOutFile.ReadAsStringAsync();
        stdErr = await stdErrFile.ReadAsStringAsync();

        Console.WriteLine("node: {0}:", node.Id);
        Console.WriteLine("stdout.txt: {0}", stdOut);
        Console.WriteLine("stderr.txt: {0}", stdErr);
    }
    else
    {
        Console.WriteLine("\tSubtask {0} is in state {1}", subtask.Id, subtask.State);
    }
});
```

## <a name="code-sample"></a><span data-ttu-id="704ff-215">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="704ff-215">Code sample</span></span>
<span data-ttu-id="704ff-216">Hello [MultiInstanceTasks] [ github_mpi] nell'esempio di codice su GitHub viene illustrato come una multi-istanza toouse attività toorun un [MS-MPI] [ msmpi_msdn] applicazione sui nodi di calcolo di Batch.</span><span class="sxs-lookup"><span data-stu-id="704ff-216">hello [MultiInstanceTasks][github_mpi] code sample on GitHub demonstrates how toouse a multi-instance task toorun an [MS-MPI][msmpi_msdn] application on Batch compute nodes.</span></span> <span data-ttu-id="704ff-217">Seguire i passaggi di hello in [preparazione](#preparation) e [esecuzione](#execution) toorun: esempio hello.</span><span class="sxs-lookup"><span data-stu-id="704ff-217">Follow hello steps in [Preparation](#preparation) and [Execution](#execution) toorun hello sample.</span></span>

### <a name="preparation"></a><span data-ttu-id="704ff-218">Operazioni preliminari</span><span class="sxs-lookup"><span data-stu-id="704ff-218">Preparation</span></span>
1. <span data-ttu-id="704ff-219">Seguire i primi due passaggi di hello in [come toocompile ed eseguire un semplice programma MS-MPI][msmpi_howto].</span><span class="sxs-lookup"><span data-stu-id="704ff-219">Follow hello first two steps in [How toocompile and run a simple MS-MPI program][msmpi_howto].</span></span> <span data-ttu-id="704ff-220">Questo soddisfa prerequesites hello per hello seguente passaggio.</span><span class="sxs-lookup"><span data-stu-id="704ff-220">This satisfies hello prerequesites for hello following step.</span></span>
2. <span data-ttu-id="704ff-221">Compilare un *versione* versione di hello [MPIHelloWorld] [ helloworld_proj] programma di esempio MPI.</span><span class="sxs-lookup"><span data-stu-id="704ff-221">Build a *Release* version of hello [MPIHelloWorld][helloworld_proj] sample MPI program.</span></span> <span data-ttu-id="704ff-222">Si tratta di programma hello che verrà eseguita dall'attività di multi-istanza hello sui nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="704ff-222">This is hello program that will be run on compute nodes by hello multi-instance task.</span></span>
3. <span data-ttu-id="704ff-223">Creare un file zip contenente `MPIHelloWorld.exe` (compilato per il passaggio 2) e `MSMpiSetup.exe` (scaricato al passaggio 1).</span><span class="sxs-lookup"><span data-stu-id="704ff-223">Create a zip file containing `MPIHelloWorld.exe` (which you built step 2) and `MSMpiSetup.exe` (which you downloaded step 1).</span></span> <span data-ttu-id="704ff-224">Carica il file zip come un pacchetto di applicazione nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="704ff-224">You'll upload this zip file as an application package in hello next step.</span></span>
4. <span data-ttu-id="704ff-225">Hello utilizzare [portale di Azure] [ portal] toocreate un Batch [applicazione](batch-application-packages.md) chiamato "MPIHelloWorld" e specificare i file zip hello creato nel passaggio precedente hello come la versione "1.0" pacchetto di applicazione Hello.</span><span class="sxs-lookup"><span data-stu-id="704ff-225">Use hello [Azure portal][portal] toocreate a Batch [application](batch-application-packages.md) called "MPIHelloWorld", and specify hello zip file you created in hello previous step as version "1.0" of hello application package.</span></span> <span data-ttu-id="704ff-226">Vedere [Caricare e gestire le applicazioni](batch-application-packages.md#upload-and-manage-applications) per maggiori informazioni.</span><span class="sxs-lookup"><span data-stu-id="704ff-226">See [Upload and manage applications](batch-application-packages.md#upload-and-manage-applications) for more information.</span></span>

> [!TIP]
> <span data-ttu-id="704ff-227">Compilare un *versione* versione `MPIHelloWorld.exe` in modo che non è tooinclude eventuali dipendenze aggiuntive (ad esempio, `msvcp140d.dll` o `vcruntime140d.dll`) nel pacchetto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="704ff-227">Build a *Release* version of `MPIHelloWorld.exe` so that you don't have tooinclude any additional dependencies (for example, `msvcp140d.dll` or `vcruntime140d.dll`) in your application package.</span></span>
>
>

### <a name="execution"></a><span data-ttu-id="704ff-228">Esecuzione</span><span class="sxs-lookup"><span data-stu-id="704ff-228">Execution</span></span>
1. <span data-ttu-id="704ff-229">Scaricare hello [esempi di azure batch] [ github_samples_zip] da GitHub.</span><span class="sxs-lookup"><span data-stu-id="704ff-229">Download hello [azure-batch-samples][github_samples_zip] from GitHub.</span></span>
2. <span data-ttu-id="704ff-230">Aprire hello MultiInstanceTasks **soluzione** in Visual Studio 2015 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="704ff-230">Open hello MultiInstanceTasks **solution** in Visual Studio 2015 or newer.</span></span> <span data-ttu-id="704ff-231">Hello `MultiInstanceTasks.sln` file della soluzione si trova:</span><span class="sxs-lookup"><span data-stu-id="704ff-231">hello `MultiInstanceTasks.sln` solution file is located in:</span></span>

    `azure-batch-samples\CSharp\ArticleProjects\MultiInstanceTasks\`
3. <span data-ttu-id="704ff-232">Immettere le credenziali dell'account Batch e l'archiviazione in `AccountSettings.settings` in hello **Microsoft.Azure.Batch.Samples.Common** progetto.</span><span class="sxs-lookup"><span data-stu-id="704ff-232">Enter your Batch and Storage account credentials in `AccountSettings.settings` in hello **Microsoft.Azure.Batch.Samples.Common** project.</span></span>
4. <span data-ttu-id="704ff-233">**Compilare ed eseguire** hello MultiInstanceTasks soluzione tooexecute hello esempio applicazione MPI in nodi di calcolo in un pool di Batch.</span><span class="sxs-lookup"><span data-stu-id="704ff-233">**Build and run** hello MultiInstanceTasks solution tooexecute hello MPI sample application on compute nodes in a Batch pool.</span></span>
5. <span data-ttu-id="704ff-234">*Facoltativo*: hello utilizzare [portale di Azure] [ portal] o hello [Explorer Batch] [ batch_explorer] tooexamine pool esempio hello, processi, e attività ("MultiInstanceSamplePool", "MultiInstanceSampleJob", "MultiInstanceSampleTask") prima di eliminare le risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="704ff-234">*Optional*: Use hello [Azure portal][portal] or hello [Batch Explorer][batch_explorer] tooexamine hello sample pool, job, and task ("MultiInstanceSamplePool", "MultiInstanceSampleJob", "MultiInstanceSampleTask") before you delete hello resources.</span></span>

> [!TIP]
> <span data-ttu-id="704ff-235">È possibile scaricare [Visual Studio Community][visual_studio] gratuitamente se non si dispone di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="704ff-235">You can download [Visual Studio Community][visual_studio] for free if you do not have Visual Studio.</span></span>
>
>

<span data-ttu-id="704ff-236">L'output di `MultiInstanceTasks.exe` è simile toohello seguente:</span><span class="sxs-lookup"><span data-stu-id="704ff-236">Output from `MultiInstanceTasks.exe` is similar toohello following:</span></span>

```
Creating pool [MultiInstanceSamplePool]...
Creating job [MultiInstanceSampleJob]...
Adding task [MultiInstanceSampleTask] toojob [MultiInstanceSampleJob]...
Awaiting task completion, timeout in 00:30:00...

Main task [MultiInstanceSampleTask] is in state [Completed] and ran on compute node [tvm-1219235766_1-20161017t162002z]:
---- stdout.txt ----
Rank 2 received string "Hello world" from Rank 0
Rank 1 received string "Hello world" from Rank 0

---- stderr.txt ----

Main task completed, waiting 00:00:10 for subtasks toocomplete...

---- Subtask information ----
subtask: 1
        exit code: 0
        node: tvm-1219235766_3-20161017t162002z
        stdout.txt:
        stderr.txt:
subtask: 2
        exit code: 0
        node: tvm-1219235766_2-20161017t162002z
        stdout.txt:
        stderr.txt:

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER tooexit...
```

## <a name="next-steps"></a><span data-ttu-id="704ff-237">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="704ff-237">Next steps</span></span>
* <span data-ttu-id="704ff-238">blog del Team di Batch di Azure e Microsoft HPC Hello illustra [MPI il supporto per Linux su Azure Batch][blog_mpi_linux]e include informazioni sull'uso [OpenFOAM] [ openfoam] con Batch.</span><span class="sxs-lookup"><span data-stu-id="704ff-238">hello Microsoft HPC & Azure Batch Team blog discusses [MPI support for Linux on Azure Batch][blog_mpi_linux], and includes information on using [OpenFOAM][openfoam] with Batch.</span></span> <span data-ttu-id="704ff-239">È possibile trovare esempi di codice Python per hello [esempio OpenFOAM su GitHub][github_mpi].</span><span class="sxs-lookup"><span data-stu-id="704ff-239">You can find Python code samples for hello [OpenFOAM example on GitHub][github_mpi].</span></span>
* <span data-ttu-id="704ff-240">Informazioni su come troppo[creare pool di nodi di calcolo Linux](batch-linux-nodes.md) per utilizzare nelle soluzioni di Azure Batch MPI.</span><span class="sxs-lookup"><span data-stu-id="704ff-240">Learn how too[create pools of Linux compute nodes](batch-linux-nodes.md) for use in your Azure Batch MPI solutions.</span></span>

[helloworld_proj]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/MultiInstanceTasks/MPIHelloWorld

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[blog_mpi_linux]: https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/
[cmd_start]: https://technet.microsoft.com/library/cc770297.aspx
[coord_cmd_example]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/article_samples/mpi/data/linux/openfoam/coordination-cmd
[github_mpi]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/MultiInstanceTasks
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[msdn_env_var]: https://msdn.microsoft.com/library/azure/mt743623.aspx
[msmpi_msdn]: https://msdn.microsoft.com/library/bb524831.aspx
[msmpi_sdk]: http://go.microsoft.com/FWLink/p/?LinkID=389556
[msmpi_howto]: http://blogs.technet.com/b/windowshpc/archive/2015/02/02/how-to-compile-and-run-a-simple-ms-mpi-program.aspx
[openfoam]: http://www.openfoam.com/
[visual_studio]: https://www.visualstudio.com/vs/community/

[net_jobprep]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.aspx
[net_multiinstance_class]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.aspx
[net_multiinstance_prop]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.multiinstancesettings.aspx
[net_multiinsance_commonresfiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.commonresourcefiles.aspx
[net_multiinstance_coordcmdline]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.coordinationcommandline.aspx
[net_multiinstance_numinstances]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.numberofinstances.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_pool_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[net_pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_resourcefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.aspx
[net_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.aspx
[net_starttask_cmdline]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.commandline.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_taskconstraints]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.aspx
[net_taskconstraint_maxretry]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.maxtaskretrycount.aspx
[net_taskconstraint_maxwallclock]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.maxwallclocktime.aspx
[net_taskconstraint_retention]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.retentiontime.aspx
[net_task_listsubtasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listsubtasks.aspx
[net_task_listnodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[poolops_getnodefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getnodefile.aspx

[portal]: https://portal.azure.com
[rest_multiinstance]: https://msdn.microsoft.com/library/azure/mt637905.aspx

[1]: ./media/batch-mpi/batch_mpi_01.png "Panoramica sulle istanze multiple"
