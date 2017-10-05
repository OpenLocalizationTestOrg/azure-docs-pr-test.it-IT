---
title: "Usare attività a istanze multiple per eseguire applicazioni MPI: Azure Batch | Documentazione Microsoft"
description: "Informazioni su come eseguire applicazioni MPI (Message Passing Interface) usando il tipo di attività a istanze multiple in Azure Batch."
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
ms.openlocfilehash: 77d12d6d48b22dfb3e7f09f273dffc11401bb15f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-multi-instance-tasks-to-run-message-passing-interface-mpi-applications-in-batch"></a><span data-ttu-id="f1266-103">Usare le attività a istanze multiple per eseguire applicazioni MPI (Message Passing Interface) in Batch</span><span class="sxs-lookup"><span data-stu-id="f1266-103">Use multi-instance tasks to run Message Passing Interface (MPI) applications in Batch</span></span>

<span data-ttu-id="f1266-104">Le attività a istanze multiple permettono di eseguire un'attività di Azure Batch in più nodi di calcolo contemporaneamente</span><span class="sxs-lookup"><span data-stu-id="f1266-104">Multi-instance tasks allow you to run an Azure Batch task on multiple compute nodes simultaneously.</span></span> <span data-ttu-id="f1266-105">e di abilitare scenari high performance computing, ad esempio le applicazioni MPI (Message Passing Interface) in Batch.</span><span class="sxs-lookup"><span data-stu-id="f1266-105">These tasks enable high performance computing scenarios like Message Passing Interface (MPI) applications in Batch.</span></span> <span data-ttu-id="f1266-106">Questo articolo illustra come eseguire attività a istanze multiple usando la libreria [Batch .NET][api_net].</span><span class="sxs-lookup"><span data-stu-id="f1266-106">In this article, you learn how to execute multi-instance tasks using the [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> <span data-ttu-id="f1266-107">Gli esempi in questo articolo sono incentrati sui nodi di calcolo Batch .NET, MS-MPI e Windows, mentre i concetti relativi alle attività a istanze multiple illustrati di seguito sono applicabili ad altre piattaforme e tecnologie, ad esempio Python e Intel MPI sui nodi Linux.</span><span class="sxs-lookup"><span data-stu-id="f1266-107">While the examples in this article focus on Batch .NET, MS-MPI, and Windows compute nodes, the multi-instance task concepts discussed here are applicable to other platforms and technologies (Python and Intel MPI on Linux nodes, for example).</span></span>
>
>

## <a name="multi-instance-task-overview"></a><span data-ttu-id="f1266-108">Panoramica sulle attività a istanze multiple</span><span class="sxs-lookup"><span data-stu-id="f1266-108">Multi-instance task overview</span></span>
<span data-ttu-id="f1266-109">In Batch ogni attività viene in genere eseguita in un singolo nodo di calcolo, si inviano più attività a un processo e il servizio Batch pianifica l'esecuzione di ogni attività in un nodo.</span><span class="sxs-lookup"><span data-stu-id="f1266-109">In Batch, each task is normally executed on a single compute node--you submit multiple tasks to a job, and the Batch service schedules each task for execution on a node.</span></span> <span data-ttu-id="f1266-110">Tuttavia, configurando le **impostazioni per istanze multiple**, si indica a Batch invece di creare un'attività primaria e svariate sottoattività per che quindi sono eseguite su più nodi.</span><span class="sxs-lookup"><span data-stu-id="f1266-110">However, by configuring a task's **multi-instance settings**, you tell Batch to instead create one primary task and several subtasks that are then executed on multiple nodes.</span></span>

<span data-ttu-id="f1266-111">![Panoramica sulle attività a istanze multiple][1]</span><span class="sxs-lookup"><span data-stu-id="f1266-111">![Multi-instance task overview][1]</span></span>

<span data-ttu-id="f1266-112">Quando si invia a un processo un'attività con impostazioni per istanze multiple, Batch esegue diversi passaggi relativi esclusivamente alle attività a istanze multiple:</span><span class="sxs-lookup"><span data-stu-id="f1266-112">When you submit a task with multi-instance settings to a job, Batch performs several steps unique to multi-instance tasks:</span></span>

1. <span data-ttu-id="f1266-113">Il servizio Batch crea un'attività **primaria** e diverse **sottoattività** in base alle impostazioni multi-istanza.</span><span class="sxs-lookup"><span data-stu-id="f1266-113">The Batch service creates one **primary** and several **subtasks** based on the multi-instance settings.</span></span> <span data-ttu-id="f1266-114">Il numero totale di attività, ovvero quella primaria e tutte le sottoattività, corrisponde al numero di **istanze** (nodi di calcolo) specificato nelle impostazioni per istanze multiple.</span><span class="sxs-lookup"><span data-stu-id="f1266-114">The total number of tasks (primary plus all subtasks) matches the number of **instances** (compute nodes) you specify in the multi-instance settings.</span></span>
2. <span data-ttu-id="f1266-115">Il servizio Batch definisce uno dei nodi di calcolo come **master** e pianifica l'attività primaria da eseguire sul master.</span><span class="sxs-lookup"><span data-stu-id="f1266-115">Batch designates one of the compute nodes as the **master**, and schedules the primary task to execute on the master.</span></span> <span data-ttu-id="f1266-116">Pianifica le sottoattività da eseguire sugli altri nodi di calcolo allocati all'attività a istanze multiple, una sottoattività per ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="f1266-116">It schedules the subtasks to execute on the remainder of the compute nodes allocated to the multi-instance task, one subtask per node.</span></span>
3. <span data-ttu-id="f1266-117">L'attività primaria e tutte le sottoattività scaricano gli eventuali **file di risorse comuni** specificati nelle impostazioni per istanze multiple.</span><span class="sxs-lookup"><span data-stu-id="f1266-117">The primary and all subtasks download any **common resource files** you specify in the multi-instance settings.</span></span>
4. <span data-ttu-id="f1266-118">Dopo aver scaricato i file di risorse comuni, l'attività primaria e le sottoattività eseguono il **comando di coordinamento** specificato nelle impostazioni per istanze multiple.</span><span class="sxs-lookup"><span data-stu-id="f1266-118">After the common resource files have been downloaded, the primary and subtasks execute the **coordination command** you specify in the multi-instance settings.</span></span> <span data-ttu-id="f1266-119">Il comando di coordinamento viene usato in genere per preparare i nodi per l'esecuzione dell'attività.</span><span class="sxs-lookup"><span data-stu-id="f1266-119">The coordination command is typically used to prepare nodes for executing the task.</span></span> <span data-ttu-id="f1266-120">Un esempio è l'avvio di servizi in background, come `smpd.exe` di [Microsoft MPI][msmpi_msdn], e la verifica che i nodi siano pronti per elaborare messaggi tra i nodi.</span><span class="sxs-lookup"><span data-stu-id="f1266-120">This can include starting background services (such as [Microsoft MPI][msmpi_msdn]'s `smpd.exe`) and verifying that the nodes are ready to process inter-node messages.</span></span>
5. <span data-ttu-id="f1266-121">L'attività primaria esegue il **comando applicazione** sul nodo master *dopo* il completamento del comando di coordinamento da parte dell'attività primaria e di tutte le sottoattività.</span><span class="sxs-lookup"><span data-stu-id="f1266-121">The primary task executes the **application command** on the master node *after* the coordination command has been completed successfully by the primary and all subtasks.</span></span> <span data-ttu-id="f1266-122">Il comando applicazione, vale a dire la riga di comando dell'attività a istanze multiple stessa, viene eseguito solo dall'attività primaria.</span><span class="sxs-lookup"><span data-stu-id="f1266-122">The application command is the command line of the multi-instance task itself, and is executed only by the primary task.</span></span> <span data-ttu-id="f1266-123">In una soluzione basata su [MS-MPI][msmpi_msdn], qui viene eseguita l'applicazione abilitata per MPI tramite `mpiexec.exe`.</span><span class="sxs-lookup"><span data-stu-id="f1266-123">In an [MS-MPI][msmpi_msdn]-based solution, this is where you execute your MPI-enabled application using `mpiexec.exe`.</span></span>

> [!NOTE]
> <span data-ttu-id="f1266-124">Anche se distinta a livello funzionale, l'attività a istanze multiple non è un tipo di attività univoco come ad esempio [StartTask][net_starttask] o [JobPreparationTask][net_jobprep].</span><span class="sxs-lookup"><span data-stu-id="f1266-124">Though it is functionally distinct, the "multi-instance task" is not a unique task type like the [StartTask][net_starttask] or [JobPreparationTask][net_jobprep].</span></span> <span data-ttu-id="f1266-125">Si tratta semplicemente di un'attività Batch standard, [CloudTask][net_task] in Batch .NET, per cui sono state configurate le impostazioni per istanze multiple.</span><span class="sxs-lookup"><span data-stu-id="f1266-125">The multi-instance task is simply a standard Batch task ([CloudTask][net_task] in Batch .NET) whose multi-instance settings have been configured.</span></span> <span data-ttu-id="f1266-126">In questo articolo viene definita **attività a istanze multiple**.</span><span class="sxs-lookup"><span data-stu-id="f1266-126">In this article, we refer to this as the **multi-instance task**.</span></span>
>
>

## <a name="requirements-for-multi-instance-tasks"></a><span data-ttu-id="f1266-127">Requisiti delle attività a istanze multiple</span><span class="sxs-lookup"><span data-stu-id="f1266-127">Requirements for multi-instance tasks</span></span>
<span data-ttu-id="f1266-128">Per le attività a istanze multiple è necessario un pool in cui sia **abilitata la comunicazione tra i nodi** e **disabilitata l'esecuzione di attività simultanee**.</span><span class="sxs-lookup"><span data-stu-id="f1266-128">Multi-instance tasks require a pool with **inter-node communication enabled**, and with **concurrent task execution disabled**.</span></span> <span data-ttu-id="f1266-129">Per disabilitare l'esecuzione di attività simultanee, impostare la proprietà [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) su 1.</span><span class="sxs-lookup"><span data-stu-id="f1266-129">To disable concurrent task execution, set the [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) property to 1.</span></span>

<span data-ttu-id="f1266-130">Questo frammento di codice illustra come creare un pool per le attività a istanze multiple usando la libreria Batch .NET.</span><span class="sxs-lookup"><span data-stu-id="f1266-130">This code snippet shows how to create a pool for multi-instance tasks using the Batch .NET library.</span></span>

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
> <span data-ttu-id="f1266-131">Se si prova a eseguire un'attività a istanze multiple in un pool con la comunicazione tra i nodi disabilitata o con un valore *maxTasksPerNode* maggiore di 1, l'attività non viene pianificata e rimane nello stato "attivo" per un periodo illimitato.</span><span class="sxs-lookup"><span data-stu-id="f1266-131">If you try to run a multi-instance task in a pool with internode communication disabled, or with a *maxTasksPerNode* value greater than 1, the task is never scheduled--it remains indefinitely in the "active" state.</span></span> 
>
> <span data-ttu-id="f1266-132">Le attività a istanze multiple possono essere eseguite solo in nodi di pool creati dopo il 14 dicembre 2015.</span><span class="sxs-lookup"><span data-stu-id="f1266-132">Multi-instance tasks can execute only on nodes in pools created after 14 December 2015.</span></span>
>
>

### <a name="use-a-starttask-to-install-mpi"></a><span data-ttu-id="f1266-133">Utilizzare uno StartTask per installare MPI</span><span class="sxs-lookup"><span data-stu-id="f1266-133">Use a StartTask to install MPI</span></span>
<span data-ttu-id="f1266-134">Per eseguire applicazioni MPI con un'attività a più istanze, è necessario innanzitutto installare un'implementazione MPI (MS-MPI o Intel MPI, ad esempio) sui nodi di calcolo nel pool.</span><span class="sxs-lookup"><span data-stu-id="f1266-134">To run MPI applications with a multi-instance task, you first need to install an MPI implementation (MS-MPI or Intel MPI, for example) on the compute nodes in the pool.</span></span> <span data-ttu-id="f1266-135">Questo è il momento giusto per usare un oggetto [StartTask][net_starttask], che viene eseguito ogni volta che un nodo viene aggiunto a un pool o viene riavviato.</span><span class="sxs-lookup"><span data-stu-id="f1266-135">This is a good time to use a [StartTask][net_starttask], which executes whenever a node joins a pool, or is restarted.</span></span> <span data-ttu-id="f1266-136">Questo frammento di codice crea un oggetto StartTask che specifica il pacchetto di installazione di MS-MPI come [file di risorse][net_resourcefile].</span><span class="sxs-lookup"><span data-stu-id="f1266-136">This code snippet creates a StartTask that specifies the MS-MPI setup package as a [resource file][net_resourcefile].</span></span> <span data-ttu-id="f1266-137">La riga di comando dell'attività di avvio viene eseguita dopo avere scaricato il file di risorse sul nodo.</span><span class="sxs-lookup"><span data-stu-id="f1266-137">The start task's command line is executed after the resource file is downloaded to the node.</span></span> <span data-ttu-id="f1266-138">In questo caso, la riga di comando esegue un'installazione automatica di MS-MPI.</span><span class="sxs-lookup"><span data-stu-id="f1266-138">In this case, the command line performs an unattended install of MS-MPI.</span></span>

```csharp
// Create a StartTask for the pool which we use for installing MS-MPI on
// the nodes as they join the pool (or when they are restarted).
StartTask startTask = new StartTask
{
    CommandLine = "cmd /c MSMpiSetup.exe -unattend -force",
    ResourceFiles = new List<ResourceFile> { new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MSMpiSetup.exe", "MSMpiSetup.exe") },
    UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin)),
    WaitForSuccess = true
};
myCloudPool.StartTask = startTask;

// Commit the fully configured pool to the Batch service to actually create
// the pool and its compute nodes.
await myCloudPool.CommitAsync();
```

### <a name="remote-direct-memory-access-rdma"></a><span data-ttu-id="f1266-139">Accesso diretto a memoria remota (RDMA)</span><span class="sxs-lookup"><span data-stu-id="f1266-139">Remote direct memory access (RDMA)</span></span>
<span data-ttu-id="f1266-140">Quando si sceglie [una dimensione che supporta RDMA](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) come ad esempio A9 per i nodi di calcolo nel pool Batch, l'applicazione MPI può sfruttare i vantaggi legati alle prestazioni elevate e alla latenza ridotta della rete con Accesso diretto a memoria remota (RDMA) di Azure.</span><span class="sxs-lookup"><span data-stu-id="f1266-140">When you choose an [RDMA-capable size](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) such as A9 for the compute nodes in your Batch pool, your MPI application can take advantage of Azure's high-performance, low-latency remote direct memory access (RDMA) network.</span></span>

<span data-ttu-id="f1266-141">Cercare le dimensioni specificate come "Co supporto di RDMA" nei seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="f1266-141">Look for the sizes specified as "RDMA capable" in the following articles:</span></span>

* <span data-ttu-id="f1266-142">Pool **CloudServiceConfiguration**</span><span class="sxs-lookup"><span data-stu-id="f1266-142">**CloudServiceConfiguration** pools</span></span>

  * <span data-ttu-id="f1266-143">[Dimensioni dei servizi cloud](../cloud-services/cloud-services-sizes-specs.md) (solo Windows)</span><span class="sxs-lookup"><span data-stu-id="f1266-143">[Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md) (Windows only)</span></span>
* <span data-ttu-id="f1266-144">Pool **VirtualMachineConfiguration**</span><span class="sxs-lookup"><span data-stu-id="f1266-144">**VirtualMachineConfiguration** pools</span></span>

  * <span data-ttu-id="f1266-145">[Dimensioni delle macchine virtuali in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)</span><span class="sxs-lookup"><span data-stu-id="f1266-145">[Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)</span></span>
  * <span data-ttu-id="f1266-146">[Dimensioni delle macchine virtuali in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)</span><span class="sxs-lookup"><span data-stu-id="f1266-146">[Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)</span></span>

> [!NOTE]
> <span data-ttu-id="f1266-147">Per sfruttare i RDMA in [nodi di calcolo Linux](batch-linux-nodes.md), è necessario utilizzare **Intel MPI** sui nodi.</span><span class="sxs-lookup"><span data-stu-id="f1266-147">To take advantage of RDMA on [Linux compute nodes](batch-linux-nodes.md), you must use **Intel MPI** on the nodes.</span></span> <span data-ttu-id="f1266-148">Per ulteriori informazioni sui pool CloudServiceConfiguration e VirtualMachineConfiguration, vedere la sezione Pool di [Cenni preliminari sulla funzionalità di Batch](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="f1266-148">For more information on CloudServiceConfiguration and VirtualMachineConfiguration pools, see the Pool section of the [Batch feature overview](batch-api-basics.md).</span></span>
>
>

## <a name="create-a-multi-instance-task-with-batch-net"></a><span data-ttu-id="f1266-149">Creare un'attività a istanze multiple con Batch .NET</span><span class="sxs-lookup"><span data-stu-id="f1266-149">Create a multi-instance task with Batch .NET</span></span>
<span data-ttu-id="f1266-150">Ora che sono stati illustrati i requisiti del pool e l'installazione del pacchetto MPI, è possibile passare alla creazione dell'attività a istanze multiple.</span><span class="sxs-lookup"><span data-stu-id="f1266-150">Now that we've covered the pool requirements and MPI package installation, let's create the multi-instance task.</span></span> <span data-ttu-id="f1266-151">In questo frammento di codice viene creato un oggetto [CloudTask][net_task] standard e viene quindi configurata la relativa proprietà [MultiInstanceSettings][net_multiinstance_prop].</span><span class="sxs-lookup"><span data-stu-id="f1266-151">In this snippet, we create a standard [CloudTask][net_task], then configure its [MultiInstanceSettings][net_multiinstance_prop] property.</span></span> <span data-ttu-id="f1266-152">Come specificato in precedenza, l'attività a istanze multiple non è un tipo di attività distinto ma un'attività Batch Standard configurata con impostazioni per istanze multiple.</span><span class="sxs-lookup"><span data-stu-id="f1266-152">As mentioned earlier, the multi-instance task is not a distinct task type, but a standard Batch task configured with multi-instance settings.</span></span>

```csharp
// Create the multi-instance task. Its command line is the "application command"
// and will be executed *only* by the primary, and only after the primary and
// subtasks execute the CoordinationCommandLine.
CloudTask myMultiInstanceTask = new CloudTask(id: "mymultiinstancetask",
    commandline: "cmd /c mpiexec.exe -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe");

// Configure the task's MultiInstanceSettings. The CoordinationCommandLine will be executed by
// the primary and all subtasks.
myMultiInstanceTask.MultiInstanceSettings =
    new MultiInstanceSettings(numberOfNodes) {
    CoordinationCommandLine = @"cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d",
    CommonResourceFiles = new List<ResourceFile> {
    new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MyMPIApplication.exe",
                     "MyMPIApplication.exe")
    }
};

// Submit the task to the job. Batch will take care of splitting it into subtasks and
// scheduling them for execution on the nodes.
await myBatchClient.JobOperations.AddTaskAsync("mybatchjob", myMultiInstanceTask);
```

## <a name="primary-task-and-subtasks"></a><span data-ttu-id="f1266-153">Attività primaria e sottoattività</span><span class="sxs-lookup"><span data-stu-id="f1266-153">Primary task and subtasks</span></span>
<span data-ttu-id="f1266-154">Quando si creano le impostazioni per istanze multiple per un'attività, è necessario specificare il numero di nodi di calcolo che devono eseguire l'attività.</span><span class="sxs-lookup"><span data-stu-id="f1266-154">When you create the multi-instance settings for a task, you specify the number of compute nodes that are to execute the task.</span></span> <span data-ttu-id="f1266-155">Quando si invia l'attività a un processo, il servizio Batch crea un'attività **primaria** e un numero sufficiente di **sottoattività** che, insieme, corrispondono al numero di nodi specificato.</span><span class="sxs-lookup"><span data-stu-id="f1266-155">When you submit the task to a job, the Batch service creates one **primary** task and enough **subtasks** that together match the number of nodes you specified.</span></span>

<span data-ttu-id="f1266-156">Alle attività viene assegnato un ID intero compreso tra 0 e *numberOfInstances* -1.</span><span class="sxs-lookup"><span data-stu-id="f1266-156">These tasks are assigned an integer id in the range of 0 to *numberOfInstances* - 1.</span></span> <span data-ttu-id="f1266-157">L'attività con ID 0 è quella primaria, tutti gli altri ID corrispondono a sottoattività.</span><span class="sxs-lookup"><span data-stu-id="f1266-157">The task with id 0 is the primary task, and all other ids are subtasks.</span></span> <span data-ttu-id="f1266-158">Ad esempio, se si creano le impostazioni per istanze multiple seguenti per un'attività, l'attività primaria avrà l'ID 0 e le sottoattività avranno un ID compreso tra 1 e 9.</span><span class="sxs-lookup"><span data-stu-id="f1266-158">For example, if you create the following multi-instance settings for a task, the primary task would have an id of 0, and the subtasks would have ids 1 through 9.</span></span>

```csharp
int numberOfNodes = 10;
myMultiInstanceTask.MultiInstanceSettings = new MultiInstanceSettings(numberOfNodes);
```

### <a name="master-node"></a><span data-ttu-id="f1266-159">Nodo master</span><span class="sxs-lookup"><span data-stu-id="f1266-159">Master node</span></span>
<span data-ttu-id="f1266-160">Quando si invia un'attività a istanze multiple, il servizio Batch definisce uno dei nodi di calcolo come nodo "master" e pianifica l'attività primaria da eseguire sul nodo master.</span><span class="sxs-lookup"><span data-stu-id="f1266-160">When you submit a multi-instance task, the Batch service designates one of the compute nodes as the "master" node, and schedules the primary task to execute on the master node.</span></span> <span data-ttu-id="f1266-161">Le sottoattività vengono pianificate da eseguire sugli altri nodi allocati all'attività a istanze multiple.</span><span class="sxs-lookup"><span data-stu-id="f1266-161">The subtasks are scheduled to execute on the remainder of the nodes allocated to the multi-instance task.</span></span>

## <a name="coordination-command"></a><span data-ttu-id="f1266-162">comando di coordinamento</span><span class="sxs-lookup"><span data-stu-id="f1266-162">Coordination command</span></span>
<span data-ttu-id="f1266-163">Il **comando di coordinamento** viene eseguita sia dall'attività primaria che dalle sottoattività.</span><span class="sxs-lookup"><span data-stu-id="f1266-163">The **coordination command** is executed by both the primary and subtasks.</span></span>

<span data-ttu-id="f1266-164">La chiamata del comando di coordinamento blocca l'esecuzione del comando applicazione da parte del servizio Batch fino a quando il comando di coordinamento non viene restituito per tutte le sottoattività.</span><span class="sxs-lookup"><span data-stu-id="f1266-164">The invocation of the coordination command is blocking--Batch does not execute the application command until the coordination command has returned successfully for all subtasks.</span></span> <span data-ttu-id="f1266-165">Il comando di coordinamento deve quindi avviare eventuali servizi in background necessari, verificare che siano pronti per l'uso e chiudersi.</span><span class="sxs-lookup"><span data-stu-id="f1266-165">The coordination command should therefore start any required background services, verify that they are ready for use, and then exit.</span></span> <span data-ttu-id="f1266-166">Ad esempio, questo comando di coordinamento per una soluzione con MS-MPI versione 7 avvia il servizio SMPD nel nodo e quindi viene chiuso:</span><span class="sxs-lookup"><span data-stu-id="f1266-166">For example, this coordination command for a solution using MS-MPI version 7 starts the SMPD service on the node, then exits:</span></span>

```
cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d
```

<span data-ttu-id="f1266-167">Si noti che l'uso di `start` in questo comando di coordinamento</span><span class="sxs-lookup"><span data-stu-id="f1266-167">Note the use of `start` in this coordination command.</span></span> <span data-ttu-id="f1266-168">è necessario perché l'applicazione `smpd.exe` non viene restituita immediatamente dopo l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="f1266-168">This is required because the `smpd.exe` application does not return immediately after execution.</span></span> <span data-ttu-id="f1266-169">Senza l'uso del comando [start][cmd_start], questo comando di coordinamento non verrebbe restituito e bloccherebbe l'esecuzione del comando applicazione.</span><span class="sxs-lookup"><span data-stu-id="f1266-169">Without the use of the [start][cmd_start] command, this coordination command would not return, and would therefore block the application command from running.</span></span>

## <a name="application-command"></a><span data-ttu-id="f1266-170">Comando applicazione</span><span class="sxs-lookup"><span data-stu-id="f1266-170">Application command</span></span>
<span data-ttu-id="f1266-171">Al termine dell'esecuzione del comando di coordinamento da parte dell'attività primaria e di tutte le sottoattività, la riga di comando dell'attività a istanze multiple viene eseguita *solo*dall'attività primaria.</span><span class="sxs-lookup"><span data-stu-id="f1266-171">Once the primary task and all subtasks have finished executing the coordination command, the multi-instance task's command line is executed by the primary task *only*.</span></span> <span data-ttu-id="f1266-172">La riga di comando viene definita **comando applicazione** per distinguerla dal comando di coordinamento.</span><span class="sxs-lookup"><span data-stu-id="f1266-172">We call this the **application command** to distinguish it from the coordination command.</span></span>

<span data-ttu-id="f1266-173">Per le applicazioni di MS-MPI, usare il comando applicazione per eseguire l'applicazione abilitata per MPI con `mpiexec.exe`.</span><span class="sxs-lookup"><span data-stu-id="f1266-173">For MS-MPI applications, use the application command to execute your MPI-enabled application with `mpiexec.exe`.</span></span> <span data-ttu-id="f1266-174">Di seguito è riportato, a titolo di esempio, il comando applicazione per una soluzione con MS-MPI versione 7:</span><span class="sxs-lookup"><span data-stu-id="f1266-174">For example, here is an application command for a solution using MS-MPI version 7:</span></span>

```
cmd /c ""%MSMPI_BIN%\mpiexec.exe"" -c 1 -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe
```

> [!NOTE]
> <span data-ttu-id="f1266-175">Dato che `mpiexec.exe` in MS-MPI usa la variabile `CCP_NODES` per impostazione predefinita, come illustrato nella sezione [Variabili di ambiente](#environment-variables), questa viene esclusa dalla riga di comando del comando applicazione di esempio precedente.</span><span class="sxs-lookup"><span data-stu-id="f1266-175">Because MS-MPI's `mpiexec.exe` uses the `CCP_NODES` variable by default (see [Environment variables](#environment-variables)) the example application command line above excludes it.</span></span>
>
>

## <a name="environment-variables"></a><span data-ttu-id="f1266-176">Variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="f1266-176">Environment variables</span></span>
<span data-ttu-id="f1266-177">Batch crea più [variabili di ambiente][msdn_env_var] specifiche delle attività a istanze multiple sui nodi di calcolo allocati a un'attività a istanze multiple.</span><span class="sxs-lookup"><span data-stu-id="f1266-177">Batch creates several [environment variables][msdn_env_var] specific to multi-instance tasks on the compute nodes allocated to a multi-instance task.</span></span> <span data-ttu-id="f1266-178">Le righe dei comandi applicazione e di coordinamento possono fare riferimento a queste variabili di ambiente, come agli script e ai programmi che eseguono.</span><span class="sxs-lookup"><span data-stu-id="f1266-178">Your coordination and application command lines can reference these environment variables, as can the scripts and programs they execute.</span></span>

<span data-ttu-id="f1266-179">Le variabili di ambiente seguenti vengono create dal servizio Batch per l'uso da parte di attività a istanze multiple:</span><span class="sxs-lookup"><span data-stu-id="f1266-179">The following environment variables are created by the Batch service for use by multi-instance tasks:</span></span>

* `CCP_NODES`
* `AZ_BATCH_NODE_LIST`
* `AZ_BATCH_HOST_LIST`
* `AZ_BATCH_MASTER_NODE`
* `AZ_BATCH_TASK_SHARED_DIR`
* `AZ_BATCH_IS_CURRENT_NODE_MASTER`

<span data-ttu-id="f1266-180">Per informazioni dettagliate su queste e altre variabili di ambiente dei nodi di calcolo, inclusi i contenuti e la visibilità, vedere l'argomento relativo alle [variabili di ambiente dei nodi di calcolo][msdn_env_var].</span><span class="sxs-lookup"><span data-stu-id="f1266-180">For full details on these and the other Batch compute node environment variables, including their contents and visibility, see [Compute node environment variables][msdn_env_var].</span></span>

> [!TIP]
> <span data-ttu-id="f1266-181">L'esempio di codice MPI per Linux su Batch contiene un esempio d'uso di alcune di queste variabili di ambiente.</span><span class="sxs-lookup"><span data-stu-id="f1266-181">The Batch Linux MPI code sample contains an example of how several of these environment variables can be used.</span></span> <span data-ttu-id="f1266-182">Lo script Bash [coordination-cmd][coord_cmd_example] scarica l'applicazione comune e i file di input da Archiviazione di Azure, consente una condivisione Network File System (NFS) sul nodo master e configura gli altri nodi allocati all'attività a istanze multiple come client NFS.</span><span class="sxs-lookup"><span data-stu-id="f1266-182">The [coordination-cmd][coord_cmd_example] Bash script downloads common application and input files from Azure Storage, enables a Network File System (NFS) share on the master node, and configures the other nodes allocated to the multi-instance task as NFS clients.</span></span>
>
>

## <a name="resource-files"></a><span data-ttu-id="f1266-183">File di risorse</span><span class="sxs-lookup"><span data-stu-id="f1266-183">Resource files</span></span>
<span data-ttu-id="f1266-184">Sono disponibili due set di file di risorse da prendere in considerazione per le attività a istanze multiple: **file di risorse comuni**, scaricati da *tutte* le attività, sia da quella primaria che dalle sottoattività, e **file di risorse** specifici per la stessa attività a istanze multiple, scaricati *solo dall'attività primaria*.</span><span class="sxs-lookup"><span data-stu-id="f1266-184">There are two sets of resource files to consider for multi-instance tasks: **common resource files** that *all* tasks download (both primary and subtasks), and the **resource files** specified for the multi-instance task itself, which *only the primary* task downloads.</span></span>

<span data-ttu-id="f1266-185">È possibile specificare uno o più **file di risorse comuni** nelle impostazioni per istanze multiple relative a un'attività.</span><span class="sxs-lookup"><span data-stu-id="f1266-185">You can specify one or more **common resource files** in the multi-instance settings for a task.</span></span> <span data-ttu-id="f1266-186">Questi file di risorse comuni vengono scaricati da [Archiviazione di Azure](../storage/common/storage-introduction.md) dall'attività primaria e da tutte le sottoattività nella **directory condivisa dell'attività** di ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="f1266-186">These common resource files are downloaded from [Azure Storage](../storage/common/storage-introduction.md) into each node's **task shared directory** by the primary and all subtasks.</span></span> <span data-ttu-id="f1266-187">È possibile accedere alla directory condivisa dell'attività dalle righe del comando applicazione e del comando di coordinamento usando la variabile di ambiente `AZ_BATCH_TASK_SHARED_DIR` .</span><span class="sxs-lookup"><span data-stu-id="f1266-187">You can access the task shared directory from application and coordination command lines by using the `AZ_BATCH_TASK_SHARED_DIR` environment variable.</span></span> <span data-ttu-id="f1266-188">Il percorso `AZ_BATCH_TASK_SHARED_DIR` è identico in ogni nodo allocato all'attività a istanze multiple ed è quindi possibile condividere un singolo comando di coordinamento tra l'attività primaria e tutte le sottoattività.</span><span class="sxs-lookup"><span data-stu-id="f1266-188">The `AZ_BATCH_TASK_SHARED_DIR` path is identical on every node allocated to the multi-instance task, thus you can share a single coordination command between the primary and all subtasks.</span></span> <span data-ttu-id="f1266-189">Il servizio Batch non "condivide" la directory nel senso di consentire un accesso remoto, ma è possibile usarla come punto di montaggio o condivisione, come indicato in precedenza nel suggerimento sulle variabili di ambiente.</span><span class="sxs-lookup"><span data-stu-id="f1266-189">Batch does not "share" the directory in a remote access sense, but you can use it as a mount or share point as mentioned earlier in the tip on environment variables.</span></span>

<span data-ttu-id="f1266-190">I file di risorse specificati per l'attività a istanze multiple stessa vengono scaricati nella directory di lavoro dell'attività, `AZ_BATCH_TASK_WORKING_DIR`, per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="f1266-190">Resource files that you specify for the multi-instance task itself are downloaded to the task's working directory, `AZ_BATCH_TASK_WORKING_DIR`, by default.</span></span> <span data-ttu-id="f1266-191">Come accennato, a differenza dei file di risorse comuni, solo l'attività primaria scarica i file di risorse specificati per l'attività a istanze multiple stessa.</span><span class="sxs-lookup"><span data-stu-id="f1266-191">As mentioned, in contrast to common resource files, only the primary task downloads resource files specified for the  multi-instance task itself.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f1266-192">Usare sempre le variabili di ambiente `AZ_BATCH_TASK_SHARED_DIR` e `AZ_BATCH_TASK_WORKING_DIR` per fare riferimento a tali directory nelle righe di comando.</span><span class="sxs-lookup"><span data-stu-id="f1266-192">Always use the environment variables `AZ_BATCH_TASK_SHARED_DIR` and `AZ_BATCH_TASK_WORKING_DIR` to refer to these directories in your command lines.</span></span> <span data-ttu-id="f1266-193">Evitare di provare a costruire i percorsi manualmente.</span><span class="sxs-lookup"><span data-stu-id="f1266-193">Do not attempt to construct the paths manually.</span></span>
>
>

## <a name="task-lifetime"></a><span data-ttu-id="f1266-194">Durata dell'attività</span><span class="sxs-lookup"><span data-stu-id="f1266-194">Task lifetime</span></span>
<span data-ttu-id="f1266-195">Dalla durata dell'attività principale dipende la durata dell'intera attività a istanze multiple.</span><span class="sxs-lookup"><span data-stu-id="f1266-195">The lifetime of the primary task controls the lifetime of the entire multi-instance task.</span></span> <span data-ttu-id="f1266-196">Quando viene chiusa l'attività primaria, vengono terminate tutte le sottoattività.</span><span class="sxs-lookup"><span data-stu-id="f1266-196">When the primary exits, all of the subtasks are terminated.</span></span> <span data-ttu-id="f1266-197">Il codice di uscita dell'attività primaria è il codice di uscita dell'attività e viene quindi usato per determinare l'esito positivo o negativo dell'attività per la ripetizione dei tentativi.</span><span class="sxs-lookup"><span data-stu-id="f1266-197">The exit code of the primary is the exit code of the task, and is therefore used to determine the success or failure of the task for retry purposes.</span></span>

<span data-ttu-id="f1266-198">Se una delle sottoattività ha esito negativo e viene chiusa con un codice restituito diverso da zero, ad esempio, l'intera attività a istanze multiple ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="f1266-198">If any of the subtasks fail, exiting with a non-zero return code, for example, the entire multi-instance task fails.</span></span> <span data-ttu-id="f1266-199">L'attività a istanze multiple viene quindi terminata e la sua esecuzione verrà ripetuta fino a raggiungere il limite di tentativi.</span><span class="sxs-lookup"><span data-stu-id="f1266-199">The multi-instance task is then terminated and retried, up to its retry limit.</span></span>

<span data-ttu-id="f1266-200">Quando si elimina un'attività a istanze multiple, il servizio Batch elimina anche l'attività primaria e tutte le sottoattività.</span><span class="sxs-lookup"><span data-stu-id="f1266-200">When you delete a multi-instance task, the primary and all subtasks are also deleted by the Batch service.</span></span> <span data-ttu-id="f1266-201">Dai nodi di calcolo vengono eliminate tutte le directory delle sottoattività e i relativi file, come avviene per un'attività standard.</span><span class="sxs-lookup"><span data-stu-id="f1266-201">All subtask directories and their files are deleted from the compute nodes, just as for a standard task.</span></span>

<span data-ttu-id="f1266-202">Le proprietà [TaskConstraints][net_taskconstraints] per un'attività a istanze multiple, ad esempio [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime][net_taskconstraint_maxwallclock] e [RetentionTime][net_taskconstraint_retention], vengono rispettate come avviene per un'attività standard e si applicano all'attività primaria e a tutte le sottoattività.</span><span class="sxs-lookup"><span data-stu-id="f1266-202">[TaskConstraints][net_taskconstraints] for a multi-instance task, such as the [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime][net_taskconstraint_maxwallclock], and [RetentionTime][net_taskconstraint_retention] properties, are honored as they are for a standard task, and apply to the primary and all subtasks.</span></span> <span data-ttu-id="f1266-203">Tuttavia, se si modifica la proprietà [RetentionTime][net_taskconstraint_retention] dopo aver aggiunto l'attività a istanze multiple al processo, la modifica viene applicata solo all'attività primaria.</span><span class="sxs-lookup"><span data-stu-id="f1266-203">However, if you change the [RetentionTime][net_taskconstraint_retention] property after adding the multi-instance task to the job, this change is applied only to the primary task.</span></span> <span data-ttu-id="f1266-204">Tutte le sottoattività continuano a usare la proprietà [RetentionTime][net_taskconstraint_retention] originale.</span><span class="sxs-lookup"><span data-stu-id="f1266-204">All of the subtasks continue to use the original [RetentionTime][net_taskconstraint_retention].</span></span>

<span data-ttu-id="f1266-205">Se l'attività recente faceva parte di un'attività a istanze multiple, nell'elenco delle attività recenti di un nodo di calcolo è incluso l'ID di una sottoattività.</span><span class="sxs-lookup"><span data-stu-id="f1266-205">A compute node's recent task list reflects the id of a subtask if the recent task was part of a multi-instance task.</span></span>

## <a name="obtain-information-about-subtasks"></a><span data-ttu-id="f1266-206">Ottenere informazioni sulle sottoattività</span><span class="sxs-lookup"><span data-stu-id="f1266-206">Obtain information about subtasks</span></span>
<span data-ttu-id="f1266-207">Per ottenere informazioni sulle sottoattività usando la libreria Batch .NET, chiamare il metodo [CloudTask.ListSubtasks][net_task_listsubtasks].</span><span class="sxs-lookup"><span data-stu-id="f1266-207">To obtain information on subtasks by using the Batch .NET library, call the [CloudTask.ListSubtasks][net_task_listsubtasks] method.</span></span> <span data-ttu-id="f1266-208">Questo metodo restituisce informazioni su tutte le sottoattività e sul nodo di calcolo che ha eseguito le attività.</span><span class="sxs-lookup"><span data-stu-id="f1266-208">This method returns information on all subtasks, and information about the compute node that executed the tasks.</span></span> <span data-ttu-id="f1266-209">Queste informazioni permettono di determinare la directory radice di ogni sottoattività, l'ID del pool, lo stato corrente, il codice di uscita e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="f1266-209">From this information, you can determine each subtask's root directory, the pool id, its current state, exit code, and more.</span></span> <span data-ttu-id="f1266-210">È possibile usare queste informazioni in combinazione con il metodo [PoolOperations.GetNodeFile][poolops_getnodefile] per ottenere i file della sottoattività.</span><span class="sxs-lookup"><span data-stu-id="f1266-210">You can use this information in combination with the [PoolOperations.GetNodeFile][poolops_getnodefile] method to obtain the subtask's files.</span></span> <span data-ttu-id="f1266-211">Si noti che questo metodo non restituisce informazioni per l'attività primaria, con ID 0.</span><span class="sxs-lookup"><span data-stu-id="f1266-211">Note that this method does not return information for the primary task (id 0).</span></span>

> [!NOTE]
> <span data-ttu-id="f1266-212">Se non diversamente specificato, i metodi Batch .NET che operano sull'attività a istanze multiple [CloudTask][net_task] stessa si applicano *solo* all'attività primaria.</span><span class="sxs-lookup"><span data-stu-id="f1266-212">Unless otherwise stated, Batch .NET methods that operate on the multi-instance [CloudTask][net_task] itself apply *only* to the primary task.</span></span> <span data-ttu-id="f1266-213">Ad esempio, quando si chiama il metodo [CloudTask.ListNodeFiles][net_task_listnodefiles] in un'attività a istanze multiple, vengono restituiti solo i file dell'attività primaria.</span><span class="sxs-lookup"><span data-stu-id="f1266-213">For example, when you call the [CloudTask.ListNodeFiles][net_task_listnodefiles] method on a multi-instance task, only the primary task's files are returned.</span></span>
>
>

<span data-ttu-id="f1266-214">Il frammento di codice seguente illustra come ottenere informazioni sulle sottoattività e come richiedere il contenuto dei file dai nodi in cui vengono eseguiti.</span><span class="sxs-lookup"><span data-stu-id="f1266-214">The following code snippet shows how to obtain subtask information, as well as request file contents from the nodes on which they executed.</span></span>

```csharp
// Obtain the job and the multi-instance task from the Batch service
CloudJob boundJob = batchClient.JobOperations.GetJob("mybatchjob");
CloudTask myMultiInstanceTask = boundJob.GetTask("mymultiinstancetask");

// Now obtain the list of subtasks for the task
IPagedEnumerable<SubtaskInformation> subtasks = myMultiInstanceTask.ListSubtasks();

// Asynchronously iterate over the subtasks and print their stdout and stderr
// output if the subtask has completed
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

## <a name="code-sample"></a><span data-ttu-id="f1266-215">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="f1266-215">Code sample</span></span>
<span data-ttu-id="f1266-216">Il codice di esempio [MultiInstanceTasks][github_mpi] su GitHub illustra come usare un'attività a più istanze per eseguire un'applicazione [MS-MPI][msmpi_msdn] nei nodi di calcolo di Batch.</span><span class="sxs-lookup"><span data-stu-id="f1266-216">The [MultiInstanceTasks][github_mpi] code sample on GitHub demonstrates how to use a multi-instance task to run an [MS-MPI][msmpi_msdn] application on Batch compute nodes.</span></span> <span data-ttu-id="f1266-217">Seguire i passaggi in [Preparazione](#preparation) e [esecuzione](#execution) per eseguire l'esempio.</span><span class="sxs-lookup"><span data-stu-id="f1266-217">Follow the steps in [Preparation](#preparation) and [Execution](#execution) to run the sample.</span></span>

### <a name="preparation"></a><span data-ttu-id="f1266-218">Operazioni preliminari</span><span class="sxs-lookup"><span data-stu-id="f1266-218">Preparation</span></span>
1. <span data-ttu-id="f1266-219">Seguire i primi due passaggi in [How to compile and run a simple MS-MPI program][msmpi_howto] (Come compilare ed eseguire un semplice programma MS-MPI).</span><span class="sxs-lookup"><span data-stu-id="f1266-219">Follow the first two steps in [How to compile and run a simple MS-MPI program][msmpi_howto].</span></span> <span data-ttu-id="f1266-220">In tal modo sono soddisfatti i prerequisiti per il passaggio seguente.</span><span class="sxs-lookup"><span data-stu-id="f1266-220">This satisfies the prerequesites for the following step.</span></span>
2. <span data-ttu-id="f1266-221">Compilare una versione *Release* del programma MPI di esempio [MPIHelloWorld][helloworld_proj].</span><span class="sxs-lookup"><span data-stu-id="f1266-221">Build a *Release* version of the [MPIHelloWorld][helloworld_proj] sample MPI program.</span></span> <span data-ttu-id="f1266-222">Questo è il programma che verrà eseguito sui nodi di calcolo dall'attività a più istanze.</span><span class="sxs-lookup"><span data-stu-id="f1266-222">This is the program that will be run on compute nodes by the multi-instance task.</span></span>
3. <span data-ttu-id="f1266-223">Creare un file zip contenente `MPIHelloWorld.exe` (compilato per il passaggio 2) e `MSMpiSetup.exe` (scaricato al passaggio 1).</span><span class="sxs-lookup"><span data-stu-id="f1266-223">Create a zip file containing `MPIHelloWorld.exe` (which you built step 2) and `MSMpiSetup.exe` (which you downloaded step 1).</span></span> <span data-ttu-id="f1266-224">Il file zip verrà caricato come un pacchetto dell'applicazione nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="f1266-224">You'll upload this zip file as an application package in the next step.</span></span>
4. <span data-ttu-id="f1266-225">Usare il [portale di Azure][portal] per creare un'[applicazione](batch-application-packages.md) Batch chiamata "MPIHelloWorld" e specificare il file zip creato nel passaggio precedente come versione "1.0" del pacchetto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f1266-225">Use the [Azure portal][portal] to create a Batch [application](batch-application-packages.md) called "MPIHelloWorld", and specify the zip file you created in the previous step as version "1.0" of the application package.</span></span> <span data-ttu-id="f1266-226">Vedere [Caricare e gestire le applicazioni](batch-application-packages.md#upload-and-manage-applications) per maggiori informazioni.</span><span class="sxs-lookup"><span data-stu-id="f1266-226">See [Upload and manage applications](batch-application-packages.md#upload-and-manage-applications) for more information.</span></span>

> [!TIP]
> <span data-ttu-id="f1266-227">Compilare una versione *Release* di `MPIHelloWorld.exe` in modo che non sia necessario includere dipendenze aggiuntive (ad esempio, `msvcp140d.dll` o `vcruntime140d.dll`) nel pacchetto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f1266-227">Build a *Release* version of `MPIHelloWorld.exe` so that you don't have to include any additional dependencies (for example, `msvcp140d.dll` or `vcruntime140d.dll`) in your application package.</span></span>
>
>

### <a name="execution"></a><span data-ttu-id="f1266-228">Esecuzione</span><span class="sxs-lookup"><span data-stu-id="f1266-228">Execution</span></span>
1. <span data-ttu-id="f1266-229">Scaricare [azure-batch-samples][github_samples_zip] da GitHub.</span><span class="sxs-lookup"><span data-stu-id="f1266-229">Download the [azure-batch-samples][github_samples_zip] from GitHub.</span></span>
2. <span data-ttu-id="f1266-230">Aprire la **soluzione** MultiInstanceTasks in Visual Studio 2015 o versione più recente.</span><span class="sxs-lookup"><span data-stu-id="f1266-230">Open the MultiInstanceTasks **solution** in Visual Studio 2015 or newer.</span></span> <span data-ttu-id="f1266-231">Il `MultiInstanceTasks.sln` file della soluzione si trova:</span><span class="sxs-lookup"><span data-stu-id="f1266-231">The `MultiInstanceTasks.sln` solution file is located in:</span></span>

    `azure-batch-samples\CSharp\ArticleProjects\MultiInstanceTasks\`
3. <span data-ttu-id="f1266-232">Immettere le credenziali dell'account di archiviazione e Batch in `AccountSettings.settings` nel progetto **Microsoft.Azure.Batch.Samples.Common**.</span><span class="sxs-lookup"><span data-stu-id="f1266-232">Enter your Batch and Storage account credentials in `AccountSettings.settings` in the **Microsoft.Azure.Batch.Samples.Common** project.</span></span>
4. <span data-ttu-id="f1266-233">**Compilare ed eseguire** la soluzione MultiInstanceTasks per eseguire l'applicazione di esempio MPI sui nodi di calcolo in un pool di Batch.</span><span class="sxs-lookup"><span data-stu-id="f1266-233">**Build and run** the MultiInstanceTasks solution to execute the MPI sample application on compute nodes in a Batch pool.</span></span>
5. <span data-ttu-id="f1266-234">*Facoltativo*: usare il [portale di Azure][portal] o [Batch Explorer][batch_explorer] per esaminare il pool di esempio, il processo e l'attività ("MultiInstanceSamplePool", "MultiInstanceSampleJob", "MultiInstanceSampleTask") prima di eliminare le risorse.</span><span class="sxs-lookup"><span data-stu-id="f1266-234">*Optional*: Use the [Azure portal][portal] or the [Batch Explorer][batch_explorer] to examine the sample pool, job, and task ("MultiInstanceSamplePool", "MultiInstanceSampleJob", "MultiInstanceSampleTask") before you delete the resources.</span></span>

> [!TIP]
> <span data-ttu-id="f1266-235">È possibile scaricare [Visual Studio Community][visual_studio] gratuitamente se non si dispone di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f1266-235">You can download [Visual Studio Community][visual_studio] for free if you do not have Visual Studio.</span></span>
>
>

<span data-ttu-id="f1266-236">L'output di `MultiInstanceTasks.exe`è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="f1266-236">Output from `MultiInstanceTasks.exe` is similar to the following:</span></span>

```
Creating pool [MultiInstanceSamplePool]...
Creating job [MultiInstanceSampleJob]...
Adding task [MultiInstanceSampleTask] to job [MultiInstanceSampleJob]...
Awaiting task completion, timeout in 00:30:00...

Main task [MultiInstanceSampleTask] is in state [Completed] and ran on compute node [tvm-1219235766_1-20161017t162002z]:
---- stdout.txt ----
Rank 2 received string "Hello world" from Rank 0
Rank 1 received string "Hello world" from Rank 0

---- stderr.txt ----

Main task completed, waiting 00:00:10 for subtasks to complete...

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

Sample complete, hit ENTER to exit...
```

## <a name="next-steps"></a><span data-ttu-id="f1266-237">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f1266-237">Next steps</span></span>
* <span data-ttu-id="f1266-238">Il blog del Team di Batch di Azure e Microsoft HPC descrive il [supporto MPI per Linux in Azure Batch][blog_mpi_linux] e include informazioni sull'uso di [OpenFOAM][openfoam] con Batch.</span><span class="sxs-lookup"><span data-stu-id="f1266-238">The Microsoft HPC & Azure Batch Team blog discusses [MPI support for Linux on Azure Batch][blog_mpi_linux], and includes information on using [OpenFOAM][openfoam] with Batch.</span></span> <span data-ttu-id="f1266-239">È possibile trovare esempi di codice Python per l'[esempio OpenFOAM su GitHub][github_mpi].</span><span class="sxs-lookup"><span data-stu-id="f1266-239">You can find Python code samples for the [OpenFOAM example on GitHub][github_mpi].</span></span>
* <span data-ttu-id="f1266-240">Leggere le informazioni su come [creare pool di nodi di calcolo Linux](batch-linux-nodes.md) per utilizzarle con le soluzioni Azure Batch MPI.</span><span class="sxs-lookup"><span data-stu-id="f1266-240">Learn how to [create pools of Linux compute nodes](batch-linux-nodes.md) for use in your Azure Batch MPI solutions.</span></span>

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
