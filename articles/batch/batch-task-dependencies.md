---
title: "Usare le relazioni tra attività per eseguire attività basate sul completamento di altre attività: Azure Batch | Microsoft Docs"
description: "Creare attività che dipendono dal completamento di altre attività per l'elaborazione di carichi di lavoro di tipo MapReduce e carichi di lavoro Big Data simili in Azure Batch."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: b8d12db5-ca30-4c7d-993a-a05af9257210
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 465306d2de8d1dbe6ba1f0cd74be720b78a50de3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-task-dependencies-to-run-tasks-that-depend-on-other-tasks"></a><span data-ttu-id="96e3b-103">Creare relazioni tra attività per eseguire attività che dipendono da altre attività</span><span class="sxs-lookup"><span data-stu-id="96e3b-103">Create task dependencies to run tasks that depend on other tasks</span></span>

<span data-ttu-id="96e3b-104">È possibile definire dipendenze delle attività per eseguire un'attività o un set di attività solo dopo il completamento di un'attività padre.</span><span class="sxs-lookup"><span data-stu-id="96e3b-104">You can define task dependencies to run a task or set of tasks only after a parent task has completed.</span></span> <span data-ttu-id="96e3b-105">Ecco alcuni degli scenari in cui le dipendenze delle attività sono utili:</span><span class="sxs-lookup"><span data-stu-id="96e3b-105">Some scenarios where task dependencies are useful include:</span></span>

* <span data-ttu-id="96e3b-106">Carichi di lavoro di tipo MapReduce nel cloud.</span><span class="sxs-lookup"><span data-stu-id="96e3b-106">MapReduce-style workloads in the cloud.</span></span>
* <span data-ttu-id="96e3b-107">Processi le cui attività di elaborazione dati può essere espressa come grafo aciclico diretto (DAG).</span><span class="sxs-lookup"><span data-stu-id="96e3b-107">Jobs whose data processing tasks can be expressed as a directed acyclic graph (DAG).</span></span>
* <span data-ttu-id="96e3b-108">Processi di pre-rendering e post-rendering, in cui ogni attività deve essere completata prima di poter avviare quella successiva.</span><span class="sxs-lookup"><span data-stu-id="96e3b-108">Pre-rendering and post-rendering processes, where each task must complete before the next task can begin.</span></span>
* <span data-ttu-id="96e3b-109">Qualsiasi altro processo in cui le attività downstream dipendono l'output delle attività upstream.</span><span class="sxs-lookup"><span data-stu-id="96e3b-109">Any other job in which downstream tasks depend on the output of upstream tasks.</span></span>

<span data-ttu-id="96e3b-110">Tramite le dipendenze delle attività di Batch è possibile creare attività di cui pianificare l'esecuzione nei nodi di calcolo dopo il completamento di una o più attività padre.</span><span class="sxs-lookup"><span data-stu-id="96e3b-110">With Batch task dependencies, you can create tasks that are scheduled for execution on compute nodes after the completion of one or more parent tasks.</span></span> <span data-ttu-id="96e3b-111">Ad esempio, è possibile creare un processo che esegue il rendering di ogni fotogramma di un film 3D con le attività parallele separate.</span><span class="sxs-lookup"><span data-stu-id="96e3b-111">For example, you can create a job that renders each frame of a 3D movie with separate, parallel tasks.</span></span> <span data-ttu-id="96e3b-112">L'attività finale, ovvero "attività di unione", unisce i fotogrammi sottoposti a rendering in un filmato completo solo dopo che è stato eseguito il rendering di tutti i fotogrammi.</span><span class="sxs-lookup"><span data-stu-id="96e3b-112">The final task--the "merge task"--merges the rendered frames into the complete movie only after all frames have been successfully rendered.</span></span>

<span data-ttu-id="96e3b-113">Per impostazione predefinita, l'esecuzione delle attività dipendenti è pianificata solo dopo il corretto completamento dell'attività padre.</span><span class="sxs-lookup"><span data-stu-id="96e3b-113">By default, dependent tasks are scheduled for execution only after the parent task has completed successfully.</span></span> <span data-ttu-id="96e3b-114">È possibile specificare un'azione di dipendenza per sostituire il comportamento predefinito ed eseguire attività quando l'attività padre non riesce.</span><span class="sxs-lookup"><span data-stu-id="96e3b-114">You can specify a dependency action to override the default behavior and run tasks when the parent task fails.</span></span> <span data-ttu-id="96e3b-115">Per informazioni dettagliate, vedere la sezione [Azioni di dipendenza](#dependency-actions).</span><span class="sxs-lookup"><span data-stu-id="96e3b-115">See the [Dependency actions](#dependency-actions) section for details.</span></span>  

<span data-ttu-id="96e3b-116">È possibile creare attività che dipendono da altre attività in una relazione uno-a-uno o uno-a-molti.</span><span class="sxs-lookup"><span data-stu-id="96e3b-116">You can create tasks that depend on other tasks in a one-to-one or one-to-many relationship.</span></span> <span data-ttu-id="96e3b-117">È anche possibile creare una dipendenza da un intervallo, in cui un'attività dipende dal completamento di un gruppo di attività all'interno di un intervallo di ID attività specifico.</span><span class="sxs-lookup"><span data-stu-id="96e3b-117">You can also create a range dependency where a task depends on the completion of a group of tasks within a specified range of task IDs.</span></span> <span data-ttu-id="96e3b-118">È possibile combinare questi tre scenari di base per creare relazioni molti-a-molti.</span><span class="sxs-lookup"><span data-stu-id="96e3b-118">You can combine these three basic scenarios to create many-to-many relationships.</span></span>

## <a name="task-dependencies-with-batch-net"></a><span data-ttu-id="96e3b-119">Relazioni tra attività con Batch .NET</span><span class="sxs-lookup"><span data-stu-id="96e3b-119">Task dependencies with Batch .NET</span></span>
<span data-ttu-id="96e3b-120">Questo articolo illustra la configurazione di relazioni tra attività tramite la libreria [Batch .NET][net_msdn].</span><span class="sxs-lookup"><span data-stu-id="96e3b-120">In this article, we discuss how to configure task dependencies by using the [Batch .NET][net_msdn] library.</span></span> <span data-ttu-id="96e3b-121">Viene illustrato prima come [abilitare le dipendenze tra attività](#enable-task-dependencies) nei processi, quindi viene spiegato come [configurare un'attività con dipendenze](#create-dependent-tasks).</span><span class="sxs-lookup"><span data-stu-id="96e3b-121">We first show you how to [enable task dependency](#enable-task-dependencies) on your jobs, and then demonstrate how to [configure a task with dependencies](#create-dependent-tasks).</span></span> <span data-ttu-id="96e3b-122">Viene inoltre descritto come specificare un'azione di dipendenza per l'esecuzione di attività dipendenti se l'attività padre non riesce.</span><span class="sxs-lookup"><span data-stu-id="96e3b-122">We also describe how to specify a dependency action to run dependent tasks if the parent fails.</span></span> <span data-ttu-id="96e3b-123">Vengono infine illustrati gli [scenari delle relazione](#dependency-scenarios) supportate da Batch.</span><span class="sxs-lookup"><span data-stu-id="96e3b-123">Finally, we discuss the [dependency scenarios](#dependency-scenarios) that Batch supports.</span></span>

## <a name="enable-task-dependencies"></a><span data-ttu-id="96e3b-124">Abilitare le relazioni tra attività</span><span class="sxs-lookup"><span data-stu-id="96e3b-124">Enable task dependencies</span></span>
<span data-ttu-id="96e3b-125">Per usare le dipendenze delle attività nell'applicazione Batch, è innanzitutto necessario configurare il processo per l'uso delle dipendenze.</span><span class="sxs-lookup"><span data-stu-id="96e3b-125">To use task dependencies in your Batch application, you must first configure the job to use task dependencies.</span></span> <span data-ttu-id="96e3b-126">In Batch .NET abilitare la funzionalità in [CloudJob][net_cloudjob] impostando la rispettiva proprietà [UsesTaskDependencies][net_usestaskdependencies] su `true`:</span><span class="sxs-lookup"><span data-stu-id="96e3b-126">In Batch .NET, enable it on your [CloudJob][net_cloudjob] by setting its [UsesTaskDependencies][net_usestaskdependencies] property to `true`:</span></span>

```csharp
CloudJob unboundJob = batchClient.JobOperations.CreateJob( "job001",
    new PoolInformation { PoolId = "pool001" });

// IMPORTANT: This is REQUIRED for using task dependencies.
unboundJob.UsesTaskDependencies = true;
```

<span data-ttu-id="96e3b-127">Nel frammento di codice precedente "batchClient" è un'istanza della classe [BatchClient][net_batchclient].</span><span class="sxs-lookup"><span data-stu-id="96e3b-127">In the preceding code snippet, "batchClient" is an instance of the [BatchClient][net_batchclient] class.</span></span>

## <a name="create-dependent-tasks"></a><span data-ttu-id="96e3b-128">Creare attività dipendenti</span><span class="sxs-lookup"><span data-stu-id="96e3b-128">Create dependent tasks</span></span>
<span data-ttu-id="96e3b-129">Per creare un'attività che dipende dal completamento di una o più attività padre, è possibile specificare che l'attività "dipende" dalle altre attività.</span><span class="sxs-lookup"><span data-stu-id="96e3b-129">To create a task that depends on the completion of one or more parent tasks, you can specify that the task "depends on" the other tasks.</span></span> <span data-ttu-id="96e3b-130">In Batch .NET configurare la proprietà [CloudTask][net_cloudtask].[DependsOn][net_dependson] con un'istanza della classe [TaskDependencies][net_taskdependencies]:</span><span class="sxs-lookup"><span data-stu-id="96e3b-130">In Batch .NET, configure the [CloudTask][net_cloudtask].[DependsOn][net_dependson] property with an instance of the [TaskDependencies][net_taskdependencies] class:</span></span>

```csharp
// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
```

<span data-ttu-id="96e3b-131">Questo frammento di codice crea un'attività dipendente con ID attività "Flowers".</span><span class="sxs-lookup"><span data-stu-id="96e3b-131">This code snippet creates a dependent task with task ID "Flowers".</span></span> <span data-ttu-id="96e3b-132">L'attività "Flowers" dipende dalle attività "Rain" e "Sun".</span><span class="sxs-lookup"><span data-stu-id="96e3b-132">The "Flowers" task depends on tasks "Rain" and "Sun".</span></span> <span data-ttu-id="96e3b-133">L'esecuzione dell'attività "Flowers" in un nodo di calcolo verrà pianificata solo dopo il corretto completamento delle attività "Rain" e "Sun".</span><span class="sxs-lookup"><span data-stu-id="96e3b-133">Task "Flowers" will be scheduled to run on a compute node only after tasks "Rain" and "Sun" have completed successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="96e3b-134">Un'attività viene considerata correttamente completata quando l'attività è in **stato completato** e il **codice di uscita** è `0`.</span><span class="sxs-lookup"><span data-stu-id="96e3b-134">A task is considered to be completed successfully when it is in the **completed** state and its **exit code** is `0`.</span></span> <span data-ttu-id="96e3b-135">In Batch .NET ciò corrisponde a un valore della proprietà [CloudTask][net_cloudtask].[State][net_taskstate] pari a `Completed` e il valore della proprietà [TaskExecutionInformation][net_taskexecutioninformation].[ExitCode][net_exitcode] è `0`.</span><span class="sxs-lookup"><span data-stu-id="96e3b-135">In Batch .NET, this means a [CloudTask][net_cloudtask].[State][net_taskstate] property value of `Completed` and the CloudTask's [TaskExecutionInformation][net_taskexecutioninformation].[ExitCode][net_exitcode] property value is `0`.</span></span>
> 
> 

## <a name="dependency-scenarios"></a><span data-ttu-id="96e3b-136">scenari delle relazione</span><span class="sxs-lookup"><span data-stu-id="96e3b-136">Dependency scenarios</span></span>
<span data-ttu-id="96e3b-137">In Azure Batch è possibile usare tre scenari di relazioni tra attività di base, ovvero uno-a-uno, uno-a-molti e la relazione tra intervalli di ID.</span><span class="sxs-lookup"><span data-stu-id="96e3b-137">There are three basic task dependency scenarios that you can use in Azure Batch: one-to-one, one-to-many, and task ID range dependency.</span></span> <span data-ttu-id="96e3b-138">Questi scenari possono essere combinati per ottenere un quarto scenario, ovvero molti-a-molti.</span><span class="sxs-lookup"><span data-stu-id="96e3b-138">These can be combined to provide a fourth scenario, many-to-many.</span></span>

| <span data-ttu-id="96e3b-139">Scenario&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="96e3b-139">Scenario&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="96e3b-140">Esempio</span><span class="sxs-lookup"><span data-stu-id="96e3b-140">Example</span></span> |  |
|:---:| --- | --- |
|  [<span data-ttu-id="96e3b-141">Uno-a-uno</span><span class="sxs-lookup"><span data-stu-id="96e3b-141">One-to-one</span></span>](#one-to-one) |<span data-ttu-id="96e3b-142">L'*attivitàB* dipende dall'*attivitàA*</span><span class="sxs-lookup"><span data-stu-id="96e3b-142">*taskB* depends on *taskA*</span></span> <p/> <span data-ttu-id="96e3b-143">L'*attivitàB* sarà pianificata per l'esecuzione solo dopo il completamento corretto dell'*attivitàA*</span><span class="sxs-lookup"><span data-stu-id="96e3b-143">*taskB* will not be scheduled for execution until *taskA* has completed successfully</span></span> |<span data-ttu-id="96e3b-144">![Diagramma: relazione uno-a-uno tra attività][1]</span><span class="sxs-lookup"><span data-stu-id="96e3b-144">![Diagram: one-to-one task dependency][1]</span></span> |
|  [<span data-ttu-id="96e3b-145">Uno-a-molti</span><span class="sxs-lookup"><span data-stu-id="96e3b-145">One-to-many</span></span>](#one-to-many) |<span data-ttu-id="96e3b-146">L'*attivitàC* dipende sia dall'*attivitàA* che dall'*attivitàB*.</span><span class="sxs-lookup"><span data-stu-id="96e3b-146">*taskC* depends on both *taskA* and *taskB*</span></span> <p/> <span data-ttu-id="96e3b-147">L'*attivitàC* sarà pianificata per l'esecuzione solo dopo il completamento corretto dell'*attivitàA* e dell'*attivitàB*</span><span class="sxs-lookup"><span data-stu-id="96e3b-147">*taskC* will not be scheduled for execution until both *taskA* and *taskB* have completed successfully</span></span> |<span data-ttu-id="96e3b-148">![Diagramma: relazione uno-a-molti tra attività][2]</span><span class="sxs-lookup"><span data-stu-id="96e3b-148">![Diagram: one-to-many task dependency][2]</span></span> |
|  [<span data-ttu-id="96e3b-149">Intervallo di ID attività</span><span class="sxs-lookup"><span data-stu-id="96e3b-149">Task ID range</span></span>](#task-id-range) |<span data-ttu-id="96e3b-150">L'*attivitàD* dipende da un intervallo di attività</span><span class="sxs-lookup"><span data-stu-id="96e3b-150">*taskD* depends on a range of tasks</span></span> <p/> <span data-ttu-id="96e3b-151">L'*attivitàD* sarà pianificata per l'esecuzione solo dopo il completamento corretto delle attività con ID compresi tra *1* e *10*</span><span class="sxs-lookup"><span data-stu-id="96e3b-151">*taskD* will not be scheduled for execution until the tasks with IDs *1* through *10* have completed successfully</span></span> |<span data-ttu-id="96e3b-152">![Diagramma: relazione tra intervalli di ID attività][3]</span><span class="sxs-lookup"><span data-stu-id="96e3b-152">![Diagram: Task id range dependency][3]</span></span> |

> [!TIP]
> <span data-ttu-id="96e3b-153">È possibile creare relazioni **molti-a-molti**, ad esempio relazioni in cui le attività C, D, E e F dipendono dalle attività A e B. Questo tipo di relazione risulta utile, ad esempio, negli scenari di pre-elaborazione parallelizzata, in cui le attività downstream dipendono dall'output di più attività upstream.</span><span class="sxs-lookup"><span data-stu-id="96e3b-153">You can create **many-to-many** relationships, such as where tasks C, D, E, and F each depend on tasks A and B. This is useful, for example, in parallelized preprocessing scenarios where your downstream tasks depend on the output of multiple upstream tasks.</span></span>
> 
> <span data-ttu-id="96e3b-154">Negli esempi di questa sezione un'attività dipendente viene eseguita solo dopo che le attività padre vengono completate correttamente.</span><span class="sxs-lookup"><span data-stu-id="96e3b-154">In the examples in this section, a dependent task runs only after the parent tasks complete successfully.</span></span> <span data-ttu-id="96e3b-155">Questo comportamento è quello predefinito per un'attività dipendente.</span><span class="sxs-lookup"><span data-stu-id="96e3b-155">This behavior is the default behavior for a dependent task.</span></span> <span data-ttu-id="96e3b-156">È possibile eseguire un'attività dipendente dopo che un'attività padre non riesce specificando un'azione di dipendenza per sostituire il comportamento predefinito.</span><span class="sxs-lookup"><span data-stu-id="96e3b-156">You can run a dependent task after a parent task fails by specifying a dependency action to override the default behavior.</span></span> <span data-ttu-id="96e3b-157">Per informazioni dettagliate, vedere la sezione [Azioni di dipendenza](#dependency-actions).</span><span class="sxs-lookup"><span data-stu-id="96e3b-157">See the [Dependency actions](#dependency-actions) section for details.</span></span>

### <a name="one-to-one"></a><span data-ttu-id="96e3b-158">Uno-a-uno</span><span class="sxs-lookup"><span data-stu-id="96e3b-158">One-to-one</span></span>
<span data-ttu-id="96e3b-159">In una relazione uno-a-uno un'attività dipende dal corretto completamento di una sola attività padre.</span><span class="sxs-lookup"><span data-stu-id="96e3b-159">In a one-to-one relationship, a task depends on the successful completion of one parent task.</span></span> <span data-ttu-id="96e3b-160">Per creare la dipendenza, specificare un solo ID attività nel metodo statico [TaskDependencies][net_taskdependencies].[OnId][net_onid] quando si popola la proprietà [DependsOn][net_dependson] di [CloudTask][net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="96e3b-160">To create the dependency, provide a single task ID to the [TaskDependencies][net_taskdependencies].[OnId][net_onid] static method when you populate the [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

```csharp
// Task 'taskA' doesn't depend on any other tasks
new CloudTask("taskA", "cmd.exe /c echo taskA"),

// Task 'taskB' depends on completion of task 'taskA'
new CloudTask("taskB", "cmd.exe /c echo taskB")
{
    DependsOn = TaskDependencies.OnId("taskA")
},
```

### <a name="one-to-many"></a><span data-ttu-id="96e3b-161">Uno-a-molti</span><span class="sxs-lookup"><span data-stu-id="96e3b-161">One-to-many</span></span>
<span data-ttu-id="96e3b-162">In una relazione uno-a-molti un'attività dipende dal completamento di più attività padre.</span><span class="sxs-lookup"><span data-stu-id="96e3b-162">In a one-to-many relationship, a task depends on the completion of multiple parent tasks.</span></span> <span data-ttu-id="96e3b-163">Per creare la dipendenza, specificare una raccolta di ID attività nel metodo statico [TaskDependencies][net_taskdependencies].[OnId][net_onids] quando si popola la proprietà [DependsOn][net_dependson] di [CloudTask][net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="96e3b-163">To create the dependency, provide a collection of task IDs to the [TaskDependencies][net_taskdependencies].[OnIds][net_onids] static method when you populate the [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

```csharp
// 'Rain' and 'Sun' don't depend on any other tasks
new CloudTask("Rain", "cmd.exe /c echo Rain"),
new CloudTask("Sun", "cmd.exe /c echo Sun"),

// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
``` 

### <a name="task-id-range"></a><span data-ttu-id="96e3b-164">Intervallo di ID attività</span><span class="sxs-lookup"><span data-stu-id="96e3b-164">Task ID range</span></span>
<span data-ttu-id="96e3b-165">In una dipendenza da un intervallo di attività padre un'attività dipende dal completamento delle attività il cui ID è compreso all'interno di un intervallo.</span><span class="sxs-lookup"><span data-stu-id="96e3b-165">In a dependency on a range of parent tasks, a task depends on the the completion of tasks whose IDs lie within a range.</span></span>
<span data-ttu-id="96e3b-166">Per creare la dipendenza, specificare il primo e l'ultimo ID attività dell'intervallo nel metodo statico [TaskDependencies][net_taskdependencies].[OnIdRange][net_onidrange] quando si popola la proprietà [DependsOn][net_dependson] di [CloudTask][net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="96e3b-166">To create the dependency, provide the first and last task IDs in the range to the [TaskDependencies][net_taskdependencies].[OnIdRange][net_onidrange] static method when you populate the [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="96e3b-167">Quando si usano intervalli di ID attività per le relazioni, gli ID attività inclusi nell'intervallo *devono* essere rappresentazioni di stringa di valori interi.</span><span class="sxs-lookup"><span data-stu-id="96e3b-167">When you use task ID ranges for your dependencies, the task IDs in the range *must* be string representations of integer values.</span></span>
> 
> <span data-ttu-id="96e3b-168">Ogni attività compresa nell'intervallo deve soddisfare la dipendenza attraverso il corretto completamento o il completamento con un errore associato a un'azione di dipendenza impostata su **Satisfy**.</span><span class="sxs-lookup"><span data-stu-id="96e3b-168">Every task in the range must satisfy the dependency, either by completing successfully or by completing with a failure that’s mapped to a dependency action set to **Satisfy**.</span></span> <span data-ttu-id="96e3b-169">Per informazioni dettagliate, vedere la sezione [Azioni di dipendenza](#dependency-actions).</span><span class="sxs-lookup"><span data-stu-id="96e3b-169">See the [Dependency actions](#dependency-actions) section for details.</span></span>
>
>

```csharp
// Tasks 1, 2, and 3 don't depend on any other tasks. Because
// we will be using them for a task range dependency, we must
// specify string representations of integers as their ids.
new CloudTask("1", "cmd.exe /c echo 1"),
new CloudTask("2", "cmd.exe /c echo 2"),
new CloudTask("3", "cmd.exe /c echo 3"),

// Task 4 depends on a range of tasks, 1 through 3
new CloudTask("4", "cmd.exe /c echo 4")
{
    // To use a range of tasks, their ids must be integer values.
    // Note that we pass integers as parameters to TaskIdRange,
    // but their ids (above) are string representations of the ids.
    DependsOn = TaskDependencies.OnIdRange(1, 3)
},
```

## <a name="dependency-actions"></a><span data-ttu-id="96e3b-170">Azioni di dipendenza</span><span class="sxs-lookup"><span data-stu-id="96e3b-170">Dependency actions</span></span>

<span data-ttu-id="96e3b-171">Per impostazione predefinita, un'attività o un set di attività dipendenti vengono eseguite solo dopo il corretto completamento di un'attività padre.</span><span class="sxs-lookup"><span data-stu-id="96e3b-171">By default, a dependent task or set of tasks runs only after a parent task has completed successfully.</span></span> <span data-ttu-id="96e3b-172">In alcuni scenari potrebbe essere necessario eseguire attività dipendenti anche se l'attività padre non riesce.</span><span class="sxs-lookup"><span data-stu-id="96e3b-172">In some scenarios, you may want to run dependent tasks even if the parent task fails.</span></span> <span data-ttu-id="96e3b-173">È possibile sostituire il comportamento predefinito specificando un'azione di dipendenza.</span><span class="sxs-lookup"><span data-stu-id="96e3b-173">You can override the default behavior by specifying a dependency action.</span></span> <span data-ttu-id="96e3b-174">Un'azione di dipendenza specifica se un'attività dipendente è idonea per l'esecuzione in base alla riuscita o meno dell'attività padre.</span><span class="sxs-lookup"><span data-stu-id="96e3b-174">A dependency action specifies whether a dependent task is eligible to run, based on the success or failure of the parent task.</span></span> 

<span data-ttu-id="96e3b-175">Si supponga, ad esempio, un'attività dipendente in attesa di dati dal completamento dell'attività upstream.</span><span class="sxs-lookup"><span data-stu-id="96e3b-175">For example, suppose that a dependent task is awaiting data from the completion of the upstream task.</span></span> <span data-ttu-id="96e3b-176">Se l'attività upstream non riesce, l'attività dipendente potrebbe comunque essere eseguita usando dati meno recenti.</span><span class="sxs-lookup"><span data-stu-id="96e3b-176">If the upstream task fails, the dependent task may still be able to run using older data.</span></span> <span data-ttu-id="96e3b-177">In questo caso, un'azione di dipendenza può specificare che l'attività dipendente è idonea per l'esecuzione nonostante l'errore dell'attività padre.</span><span class="sxs-lookup"><span data-stu-id="96e3b-177">In this case, a dependency action can specify that the dependent task is eligible to run despite the failure of the parent task.</span></span>

<span data-ttu-id="96e3b-178">Un'azione di dipendenza è basata su una condizione di uscita per l'attività padre.</span><span class="sxs-lookup"><span data-stu-id="96e3b-178">A dependency action is based on an exit condition for the parent task.</span></span> <span data-ttu-id="96e3b-179">È possibile specificare un'azione di dipendenza per una qualsiasi delle condizioni di uscita seguenti. Per .NET, vedere la classe [ExitConditions][net_exitconditions] per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="96e3b-179">You can specify a dependency action for any of the following exit conditions; for .NET, see the [ExitConditions][net_exitconditions] class for details:</span></span>

- <span data-ttu-id="96e3b-180">Quando si verifica un errore di pre-elaborazione.</span><span class="sxs-lookup"><span data-stu-id="96e3b-180">When a pre-processing error occurs.</span></span>
- <span data-ttu-id="96e3b-181">Quando si verifica un errore di caricamento dei file.</span><span class="sxs-lookup"><span data-stu-id="96e3b-181">When a file upload error occurs.</span></span> <span data-ttu-id="96e3b-182">Se l'attività si chiude con un codice di uscita specificato tramite **exitCodes** o **exitCodeRanges** e quindi si verifica un errore di caricamento dei file, l'azione specificata dal codice di uscita ha la precedenza.</span><span class="sxs-lookup"><span data-stu-id="96e3b-182">If the task exits with an exit code that was specified via **exitCodes** or **exitCodeRanges**, and then encounters a file upload error, the action specified by the exit code takes precedence.</span></span>
- <span data-ttu-id="96e3b-183">Quando l'attività termina con un codice di uscita definito dalla proprietà **ExitCodes**.</span><span class="sxs-lookup"><span data-stu-id="96e3b-183">When the task exits with an exit code defined by the **ExitCodes** property.</span></span>
- <span data-ttu-id="96e3b-184">Quando l'attività termina con un codice di uscita compreso in un intervallo specificato dalla proprietà **ExitCodeRanges**.</span><span class="sxs-lookup"><span data-stu-id="96e3b-184">When the task exits with an exit code that falls within a range specified by the **ExitCodeRanges** property.</span></span>
- <span data-ttu-id="96e3b-185">Il caso predefinito, ovvero se l'attività si chiude con un codice di uscita non definito da **ExitCodes** o **ExitCodeRanges** oppure se l'attività si chiude con un errore di pre-elaborazione e la proprietà **PreProcessingError** non è stata configurata o se l'attività ha esito negativo con un errore di caricamento dei file e la proprietà **FileUploadError** non è stata configurata.</span><span class="sxs-lookup"><span data-stu-id="96e3b-185">The default case, if the task exits with an exit code not defined by **ExitCodes** or **ExitCodeRanges**, or if the task exits with a pre-processing error and the **PreProcessingError** property is not set, or if the task fails with a file upload error and the **FileUploadError** property is not set.</span></span> 

<span data-ttu-id="96e3b-186">Per specificare un'azione di dipendenza in .NET, impostare la proprietà [ExitOptions][net_exitoptions].[DependencyAction][net_dependencyaction] per la condizione di uscita.</span><span class="sxs-lookup"><span data-stu-id="96e3b-186">To specify a dependency action in .NET, set the [ExitOptions][net_exitoptions].[DependencyAction][net_dependencyaction] property for the exit condition.</span></span> <span data-ttu-id="96e3b-187">La proprietà **DependencyAction** accetta uno di questi due valori:</span><span class="sxs-lookup"><span data-stu-id="96e3b-187">The **DependencyAction** property takes one of two values:</span></span>

- <span data-ttu-id="96e3b-188">L'impostazione della proprietà **DependencyAction** su **Satisfy** indica che le attività dipendenti sono idonee per l'esecuzione se l'attività padre termina con un errore specificato.</span><span class="sxs-lookup"><span data-stu-id="96e3b-188">Setting the **DependencyAction** property to **Satisfy** indicates that dependent tasks are eligible to run if the parent task exits with a specified error.</span></span>
- <span data-ttu-id="96e3b-189">L'impostazione della proprietà **DependencyAction** su **Block** indica che le attività dipendenti non sono idonee per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="96e3b-189">Setting the **DependencyAction** property to **Block** indicates that dependent tasks are not eligible to run.</span></span>

<span data-ttu-id="96e3b-190">L'impostazione predefinita per la proprietà **DependencyAction** è **Satisfy** per il codice di uscita 0 e **Block** per tutte le altre condizioni di uscita.</span><span class="sxs-lookup"><span data-stu-id="96e3b-190">The default setting for the **DependencyAction** property is **Satisfy** for exit code 0, and **Block** for all other exit conditions.</span></span>

<span data-ttu-id="96e3b-191">Il frammento di codice seguente imposta la proprietà **DependencyAction** per un'attività padre.</span><span class="sxs-lookup"><span data-stu-id="96e3b-191">The following code snippet sets the **DependencyAction** property for a parent task.</span></span> <span data-ttu-id="96e3b-192">Se l'attività padre termina con un errore di pre-elaborazione o con i codici di errore specificati, l'attività dipendente viene bloccata.</span><span class="sxs-lookup"><span data-stu-id="96e3b-192">If the parent task exits with a pre-processing error, or with the specified error codes, the dependent task is blocked.</span></span> <span data-ttu-id="96e3b-193">Se l'attività padre termina con qualsiasi altro errore diverso da zero, l'attività dipendente è idonea per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="96e3b-193">If the parent task exits with any other non-zero error, the dependent task is eligible to run.</span></span>

```csharp
// Task A is the parent task.
new CloudTask("A", "cmd.exe /c echo A")
{
    // Specify exit conditions for task A and their dependency actions.
    ExitConditions = new ExitConditions
    {
        // If task A exits with a pre-processing error, block any downstream tasks (in this example, task B).
        PreProcessingError = new ExitOptions
        {
            DependencyAction = DependencyAction.Block
        },
        // If task A exits with the specified error codes, block any downstream tasks (in this example, task B).
        ExitCodes = new List<ExitCodeMapping>
        {
            new ExitCodeMapping(10, new ExitOptions() { DependencyAction = DependencyAction.Block }),
            new ExitCodeMapping(20, new ExitOptions() { DependencyAction = DependencyAction.Block })
        },
        // If task A succeeds or fails with any other error, any downstream tasks become eligible to run 
        // (in this example, task B).
        Default = new ExitOptions
        {
            DependencyAction = DependencyAction.Satisfy
        }
    }
},
// Task B depends on task A. Whether it becomes eligible to run depends on how task A exits.
new CloudTask("B", "cmd.exe /c echo B")
{
    DependsOn = TaskDependencies.OnId("A")
},
```

## <a name="code-sample"></a><span data-ttu-id="96e3b-194">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="96e3b-194">Code sample</span></span>
<span data-ttu-id="96e3b-195">Il progetto di esempio [TaskDependencies][github_taskdependencies] è uno degli [esempi di codice di Azure Batch][github_samples] disponibili in GitHub.</span><span class="sxs-lookup"><span data-stu-id="96e3b-195">The [TaskDependencies][github_taskdependencies] sample project is one of the [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="96e3b-196">Questa soluzione di Visual Studio mostra:</span><span class="sxs-lookup"><span data-stu-id="96e3b-196">This Visual Studio solution demonstrates:</span></span>

- <span data-ttu-id="96e3b-197">Come abilitare la dipendenza delle attività in un processo</span><span class="sxs-lookup"><span data-stu-id="96e3b-197">How to enable task dependency on a job</span></span>
- <span data-ttu-id="96e3b-198">Come creare attività che dipendono da altre attività</span><span class="sxs-lookup"><span data-stu-id="96e3b-198">How to create tasks that depend on other tasks</span></span>
- <span data-ttu-id="96e3b-199">Come eseguire queste attività in un pool di nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="96e3b-199">How to execute those tasks on a pool of compute nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="96e3b-200">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="96e3b-200">Next steps</span></span>
### <a name="application-deployment"></a><span data-ttu-id="96e3b-201">Distribuzione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="96e3b-201">Application deployment</span></span>
<span data-ttu-id="96e3b-202">La funzionalità [Pacchetti dell'applicazione](batch-application-packages.md) di Batch offre un modo semplice per distribuire e controllare le versioni delle applicazioni eseguite dalle attività nei nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="96e3b-202">The [application packages](batch-application-packages.md) feature of Batch provides an easy way to both deploy and version the applications that your tasks execute on compute nodes.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="96e3b-203">Installazione delle applicazioni e staging dei dati</span><span class="sxs-lookup"><span data-stu-id="96e3b-203">Installing applications and staging data</span></span>
<span data-ttu-id="96e3b-204">Per una panoramica dei metodi di preparazione dei nodi per l'esecuzione di attività, vedere [Installing applications and staging data on Batch compute nodes][forum_post] (Installazione di applicazioni e staging dei dati nei nodi di calcolo di Batch) nel forum di Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="96e3b-204">See [Installing applications and staging data on Batch compute nodes][forum_post] in the Azure Batch forum for an overview of methods for preparing your nodes to run tasks.</span></span> <span data-ttu-id="96e3b-205">Scritto da uno dei membri del team di Azure Batch, questo post è una panoramica utile dei diversi modi disponibili per copiare applicazioni, dati di input di attività e altri file nei nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="96e3b-205">Written by one of the Azure Batch team members, this post is a good primer on the different ways to copy applications, task input data, and other files to your compute nodes.</span></span>

[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[github_taskdependencies]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/TaskDependencies
[github_samples]: https://github.com/Azure/azure-batch-samples
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_dependson]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.dependson.aspx
[net_exitcode]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskexecutioninformation.exitcode.aspx
[net_exitconditions]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitconditions
[net_exitoptions]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitoptions
[net_dependencyaction]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitoptions#Microsoft_Azure_Batch_ExitOptions_DependencyAction
[net_msdn]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[net_onid]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onid.aspx
[net_onids]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onids.aspx
[net_onidrange]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onidrange.aspx
[net_taskexecutioninformation]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskexecutioninformation.aspx
[net_taskstate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.taskstate.aspx
[net_usestaskdependencies]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.usestaskdependencies.aspx
[net_taskdependencies]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskdependencies.aspx

<span data-ttu-id="96e3b-206">[1]: ./media/batch-task-dependency/01_one_to_one.png "Diagramma: relazione uno-a-uno"</span><span class="sxs-lookup"><span data-stu-id="96e3b-206">[1]: ./media/batch-task-dependency/01_one_to_one.png "Diagram: one-to-one dependency"</span></span>
<span data-ttu-id="96e3b-207">[2]: ./media/batch-task-dependency/02_one_to_many.png "Diagramma: relazione uno-a-molti"</span><span class="sxs-lookup"><span data-stu-id="96e3b-207">[2]: ./media/batch-task-dependency/02_one_to_many.png "Diagram: one-to-many dependency"</span></span>
<span data-ttu-id="96e3b-208">[3]: ./media/batch-task-dependency/03_task_id_range.png "Diagramma: relazione tra intervalli di ID attività"</span><span class="sxs-lookup"><span data-stu-id="96e3b-208">[3]: ./media/batch-task-dependency/03_task_id_range.png "Diagram: task id range dependency"</span></span>
