---
title: "attività di aaaUse toorun di dipendenze in base hello completamento di altre attività - Azure Batch | Documenti Microsoft"
description: "Creare le attività che dipendono dal completamento hello di altre attività per l'elaborazione di stile MapReduce e i dati di grandi dimensioni simili carichi di lavoro nel Batch di Azure."
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
ms.openlocfilehash: faf08ec38cb30b1f66acd51e256c31aea6215c62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-task-dependencies-toorun-tasks-that-depend-on-other-tasks"></a><span data-ttu-id="41462-103">Creare relazioni tra attività attività toorun che dipendono da altre attività</span><span class="sxs-lookup"><span data-stu-id="41462-103">Create task dependencies toorun tasks that depend on other tasks</span></span>

<span data-ttu-id="41462-104">È possibile definire attività dipendenze toorun un'attività o un set di attività solo dopo che un'attività padre è stata completata.</span><span class="sxs-lookup"><span data-stu-id="41462-104">You can define task dependencies toorun a task or set of tasks only after a parent task has completed.</span></span> <span data-ttu-id="41462-105">Ecco alcuni degli scenari in cui le dipendenze delle attività sono utili:</span><span class="sxs-lookup"><span data-stu-id="41462-105">Some scenarios where task dependencies are useful include:</span></span>

* <span data-ttu-id="41462-106">Stile MapReduce i carichi di lavoro nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="41462-106">MapReduce-style workloads in hello cloud.</span></span>
* <span data-ttu-id="41462-107">Processi le cui attività di elaborazione dati può essere espressa come grafo aciclico diretto (DAG).</span><span class="sxs-lookup"><span data-stu-id="41462-107">Jobs whose data processing tasks can be expressed as a directed acyclic graph (DAG).</span></span>
* <span data-ttu-id="41462-108">Dopo il rendering e il pre-rendering di elabora, in cui ogni attività è necessario completare prima di poter iniziare l'attività successiva hello.</span><span class="sxs-lookup"><span data-stu-id="41462-108">Pre-rendering and post-rendering processes, where each task must complete before hello next task can begin.</span></span>
* <span data-ttu-id="41462-109">Qualsiasi altro processo in cui attività downstream dipendono dall'output di hello delle attività a monte.</span><span class="sxs-lookup"><span data-stu-id="41462-109">Any other job in which downstream tasks depend on hello output of upstream tasks.</span></span>

<span data-ttu-id="41462-110">Con le relazioni tra attività Batch, è possibile creare attività pianificate per l'esecuzione in nodi di calcolo dopo il completamento di hello di uno o più attività padre.</span><span class="sxs-lookup"><span data-stu-id="41462-110">With Batch task dependencies, you can create tasks that are scheduled for execution on compute nodes after hello completion of one or more parent tasks.</span></span> <span data-ttu-id="41462-111">Ad esempio, è possibile creare un processo che esegue il rendering di ogni fotogramma di un film 3D con le attività parallele separate.</span><span class="sxs-lookup"><span data-stu-id="41462-111">For example, you can create a job that renders each frame of a 3D movie with separate, parallel tasks.</span></span> <span data-ttu-id="41462-112">attività finale Hello - hello "attività merge" - unioni hello fotogrammi sottoposti a rendering in film completo di hello solo dopo che tutti i frame è stato correttamente eseguito il rendering.</span><span class="sxs-lookup"><span data-stu-id="41462-112">hello final task--hello "merge task"--merges hello rendered frames into hello complete movie only after all frames have been successfully rendered.</span></span>

<span data-ttu-id="41462-113">Per impostazione predefinita, le attività dipendenti pianificate per l'esecuzione solo dopo che l'attività padre hello è stata completata.</span><span class="sxs-lookup"><span data-stu-id="41462-113">By default, dependent tasks are scheduled for execution only after hello parent task has completed successfully.</span></span> <span data-ttu-id="41462-114">È possibile specificare un dipendenza azione toooverride hello il comportamento predefinito ed eseguire attività quando l'attività padre hello ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="41462-114">You can specify a dependency action toooverride hello default behavior and run tasks when hello parent task fails.</span></span> <span data-ttu-id="41462-115">Vedere hello [azioni dipendenza](#dependency-actions) sezione per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="41462-115">See hello [Dependency actions](#dependency-actions) section for details.</span></span>  

<span data-ttu-id="41462-116">È possibile creare attività che dipendono da altre attività in una relazione uno-a-uno o uno-a-molti.</span><span class="sxs-lookup"><span data-stu-id="41462-116">You can create tasks that depend on other tasks in a one-to-one or one-to-many relationship.</span></span> <span data-ttu-id="41462-117">È inoltre possibile creare una dipendenza di intervallo in cui un'attività dipende dal completamento di hello di un gruppo di attività all'interno di un intervallo di ID attività specificato.</span><span class="sxs-lookup"><span data-stu-id="41462-117">You can also create a range dependency where a task depends on hello completion of a group of tasks within a specified range of task IDs.</span></span> <span data-ttu-id="41462-118">È possibile combinare queste tre relazioni molti-a-molti toocreate di scenari di base.</span><span class="sxs-lookup"><span data-stu-id="41462-118">You can combine these three basic scenarios toocreate many-to-many relationships.</span></span>

## <a name="task-dependencies-with-batch-net"></a><span data-ttu-id="41462-119">Relazioni tra attività con Batch .NET</span><span class="sxs-lookup"><span data-stu-id="41462-119">Task dependencies with Batch .NET</span></span>
<span data-ttu-id="41462-120">In questo articolo viene illustrato come dipendenze di attività tooconfigure utilizzando hello [.NET per Batch] [ net_msdn] libreria.</span><span class="sxs-lookup"><span data-stu-id="41462-120">In this article, we discuss how tooconfigure task dependencies by using hello [Batch .NET][net_msdn] library.</span></span> <span data-ttu-id="41462-121">Viene innanzitutto illustrata la modalità è troppo[abilitare la relazione tra attività](#enable-task-dependencies) nei processi e quindi illustra come troppo[configurare un'attività con le dipendenze](#create-dependent-tasks).</span><span class="sxs-lookup"><span data-stu-id="41462-121">We first show you how too[enable task dependency](#enable-task-dependencies) on your jobs, and then demonstrate how too[configure a task with dependencies](#create-dependent-tasks).</span></span> <span data-ttu-id="41462-122">È anche descrivere come toospecify un dipendenza azione toorun attività dipendente se padre hello ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="41462-122">We also describe how toospecify a dependency action toorun dependent tasks if hello parent fails.</span></span> <span data-ttu-id="41462-123">Infine, approfondiremo hello [scenari dipendenza](#dependency-scenarios) che supporta Batch.</span><span class="sxs-lookup"><span data-stu-id="41462-123">Finally, we discuss hello [dependency scenarios](#dependency-scenarios) that Batch supports.</span></span>

## <a name="enable-task-dependencies"></a><span data-ttu-id="41462-124">Abilitare le relazioni tra attività</span><span class="sxs-lookup"><span data-stu-id="41462-124">Enable task dependencies</span></span>
<span data-ttu-id="41462-125">dipendenze di attività toouse Batch nell'applicazione in uso, è necessario configurare le dipendenze di attività toouse di hello del processo.</span><span class="sxs-lookup"><span data-stu-id="41462-125">toouse task dependencies in your Batch application, you must first configure hello job toouse task dependencies.</span></span> <span data-ttu-id="41462-126">In .NET per Batch, abilitarlo nel [CloudJob] [ net_cloudjob] impostando il relativo [UsesTaskDependencies] [ net_usestaskdependencies] proprietà troppo`true`:</span><span class="sxs-lookup"><span data-stu-id="41462-126">In Batch .NET, enable it on your [CloudJob][net_cloudjob] by setting its [UsesTaskDependencies][net_usestaskdependencies] property too`true`:</span></span>

```csharp
CloudJob unboundJob = batchClient.JobOperations.CreateJob( "job001",
    new PoolInformation { PoolId = "pool001" });

// IMPORTANT: This is REQUIRED for using task dependencies.
unboundJob.UsesTaskDependencies = true;
```

<span data-ttu-id="41462-127">Nel precedente frammento di codice di hello, "batchClient" è un'istanza di hello [BatchClient] [ net_batchclient] classe.</span><span class="sxs-lookup"><span data-stu-id="41462-127">In hello preceding code snippet, "batchClient" is an instance of hello [BatchClient][net_batchclient] class.</span></span>

## <a name="create-dependent-tasks"></a><span data-ttu-id="41462-128">Creare attività dipendenti</span><span class="sxs-lookup"><span data-stu-id="41462-128">Create dependent tasks</span></span>
<span data-ttu-id="41462-129">toocreate un'attività che dipende dal completamento hello di uno o più attività padre, è possibile specificare l'attività "dipende" hello che hello altre attività.</span><span class="sxs-lookup"><span data-stu-id="41462-129">toocreate a task that depends on hello completion of one or more parent tasks, you can specify that hello task "depends on" hello other tasks.</span></span> <span data-ttu-id="41462-130">In .NET per Batch, configurare hello [CloudTask][net_cloudtask].[ DependsOn] [ net_dependson] proprietà con un'istanza di hello [TaskDependencies] [ net_taskdependencies] classe:</span><span class="sxs-lookup"><span data-stu-id="41462-130">In Batch .NET, configure hello [CloudTask][net_cloudtask].[DependsOn][net_dependson] property with an instance of hello [TaskDependencies][net_taskdependencies] class:</span></span>

```csharp
// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
```

<span data-ttu-id="41462-131">Questo frammento di codice crea un'attività dipendente con ID attività "Flowers".</span><span class="sxs-lookup"><span data-stu-id="41462-131">This code snippet creates a dependent task with task ID "Flowers".</span></span> <span data-ttu-id="41462-132">Hello "Fiori" attività dipende dalle attività "Ora" e "Sun".</span><span class="sxs-lookup"><span data-stu-id="41462-132">hello "Flowers" task depends on tasks "Rain" and "Sun".</span></span> <span data-ttu-id="41462-133">L'attività "Fiori" sarà toorun pianificato su un nodo di calcolo solo dopo l'attività "Ora" e "Sun" sono stati completati correttamente.</span><span class="sxs-lookup"><span data-stu-id="41462-133">Task "Flowers" will be scheduled toorun on a compute node only after tasks "Rain" and "Sun" have completed successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="41462-134">Un'attività viene considerata toobe completata correttamente quando è in hello **completato** stato e il relativo **codice di uscita** è `0`.</span><span class="sxs-lookup"><span data-stu-id="41462-134">A task is considered toobe completed successfully when it is in hello **completed** state and its **exit code** is `0`.</span></span> <span data-ttu-id="41462-135">In .NET per Batch, ciò significa un [CloudTask][net_cloudtask].[ Stato] [ net_taskstate] valore della proprietà `Completed` e hello del CloudTask [TaskExecutionInformation][net_taskexecutioninformation].[ Codice di uscita] [ net_exitcode] valore della proprietà è `0`.</span><span class="sxs-lookup"><span data-stu-id="41462-135">In Batch .NET, this means a [CloudTask][net_cloudtask].[State][net_taskstate] property value of `Completed` and hello CloudTask's [TaskExecutionInformation][net_taskexecutioninformation].[ExitCode][net_exitcode] property value is `0`.</span></span>
> 
> 

## <a name="dependency-scenarios"></a><span data-ttu-id="41462-136">scenari delle relazione</span><span class="sxs-lookup"><span data-stu-id="41462-136">Dependency scenarios</span></span>
<span data-ttu-id="41462-137">In Azure Batch è possibile usare tre scenari di relazioni tra attività di base, ovvero uno-a-uno, uno-a-molti e la relazione tra intervalli di ID.</span><span class="sxs-lookup"><span data-stu-id="41462-137">There are three basic task dependency scenarios that you can use in Azure Batch: one-to-one, one-to-many, and task ID range dependency.</span></span> <span data-ttu-id="41462-138">Possono essere combinati tooprovide un quarto scenario, molti-a-molti.</span><span class="sxs-lookup"><span data-stu-id="41462-138">These can be combined tooprovide a fourth scenario, many-to-many.</span></span>

| <span data-ttu-id="41462-139">Scenario&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="41462-139">Scenario&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="41462-140">Esempio</span><span class="sxs-lookup"><span data-stu-id="41462-140">Example</span></span> |  |
|:---:| --- | --- |
|  [<span data-ttu-id="41462-141">Uno-a-uno</span><span class="sxs-lookup"><span data-stu-id="41462-141">One-to-one</span></span>](#one-to-one) |<span data-ttu-id="41462-142">L'*attivitàB* dipende dall'*attivitàA*</span><span class="sxs-lookup"><span data-stu-id="41462-142">*taskB* depends on *taskA*</span></span> <p/> <span data-ttu-id="41462-143">L'*attivitàB* sarà pianificata per l'esecuzione solo dopo il completamento corretto dell'*attivitàA*</span><span class="sxs-lookup"><span data-stu-id="41462-143">*taskB* will not be scheduled for execution until *taskA* has completed successfully</span></span> |<span data-ttu-id="41462-144">![Diagramma: relazione uno-a-uno tra attività][1]</span><span class="sxs-lookup"><span data-stu-id="41462-144">![Diagram: one-to-one task dependency][1]</span></span> |
|  [<span data-ttu-id="41462-145">Uno-a-molti</span><span class="sxs-lookup"><span data-stu-id="41462-145">One-to-many</span></span>](#one-to-many) |<span data-ttu-id="41462-146">L'*attivitàC* dipende sia dall'*attivitàA* che dall'*attivitàB*.</span><span class="sxs-lookup"><span data-stu-id="41462-146">*taskC* depends on both *taskA* and *taskB*</span></span> <p/> <span data-ttu-id="41462-147">L'*attivitàC* sarà pianificata per l'esecuzione solo dopo il completamento corretto dell'*attivitàA* e dell'*attivitàB*</span><span class="sxs-lookup"><span data-stu-id="41462-147">*taskC* will not be scheduled for execution until both *taskA* and *taskB* have completed successfully</span></span> |<span data-ttu-id="41462-148">![Diagramma: relazione uno-a-molti tra attività][2]</span><span class="sxs-lookup"><span data-stu-id="41462-148">![Diagram: one-to-many task dependency][2]</span></span> |
|  [<span data-ttu-id="41462-149">Intervallo di ID attività</span><span class="sxs-lookup"><span data-stu-id="41462-149">Task ID range</span></span>](#task-id-range) |<span data-ttu-id="41462-150">L'*attivitàD* dipende da un intervallo di attività</span><span class="sxs-lookup"><span data-stu-id="41462-150">*taskD* depends on a range of tasks</span></span> <p/> <span data-ttu-id="41462-151">*taskD* non verrà pianificato per l'esecuzione fino a quando le attività con ID hello *1* tramite *10* sono stati completati correttamente</span><span class="sxs-lookup"><span data-stu-id="41462-151">*taskD* will not be scheduled for execution until hello tasks with IDs *1* through *10* have completed successfully</span></span> |<span data-ttu-id="41462-152">![Diagramma: relazione tra intervalli di ID attività][3]</span><span class="sxs-lookup"><span data-stu-id="41462-152">![Diagram: Task id range dependency][3]</span></span> |

> [!TIP]
> <span data-ttu-id="41462-153">È possibile creare **molti-a-molti** relazioni, ad esempio in cui attività C, D, E e F ogni dipende da attività A e B. Ciò è utile, ad esempio, negli scenari di pre-elaborazione parallelizzati in cui le attività downstream dipendono dall'output di hello di più attività upstream.</span><span class="sxs-lookup"><span data-stu-id="41462-153">You can create **many-to-many** relationships, such as where tasks C, D, E, and F each depend on tasks A and B. This is useful, for example, in parallelized preprocessing scenarios where your downstream tasks depend on hello output of multiple upstream tasks.</span></span>
> 
> <span data-ttu-id="41462-154">Negli esempi di hello in questa sezione, un'attività dipendente viene eseguito solo dopo che l'attività padre hello completata correttamente.</span><span class="sxs-lookup"><span data-stu-id="41462-154">In hello examples in this section, a dependent task runs only after hello parent tasks complete successfully.</span></span> <span data-ttu-id="41462-155">Questo comportamento è hello predefinito per un'attività dipendente.</span><span class="sxs-lookup"><span data-stu-id="41462-155">This behavior is hello default behavior for a dependent task.</span></span> <span data-ttu-id="41462-156">Dopo che un'attività padre non riesce, specificando un comportamento predefinito di hello toooverride di azione di dipendenza, è possibile eseguire un'attività dipendente.</span><span class="sxs-lookup"><span data-stu-id="41462-156">You can run a dependent task after a parent task fails by specifying a dependency action toooverride hello default behavior.</span></span> <span data-ttu-id="41462-157">Vedere hello [azioni dipendenza](#dependency-actions) sezione per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="41462-157">See hello [Dependency actions](#dependency-actions) section for details.</span></span>

### <a name="one-to-one"></a><span data-ttu-id="41462-158">Uno-a-uno</span><span class="sxs-lookup"><span data-stu-id="41462-158">One-to-one</span></span>
<span data-ttu-id="41462-159">In una relazione uno-a un'attività dipende dal completamento hello dell'attività padre.</span><span class="sxs-lookup"><span data-stu-id="41462-159">In a one-to-one relationship, a task depends on hello successful completion of one parent task.</span></span> <span data-ttu-id="41462-160">toocreate hello dipendenza, fornire un toohello ID singola attività [TaskDependencies][net_taskdependencies].[ OnId] [ net_onid] metodo statico quando si popola hello [DependsOn] [ net_dependson] proprietà di [CloudTask] [ net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="41462-160">toocreate hello dependency, provide a single task ID toohello [TaskDependencies][net_taskdependencies].[OnId][net_onid] static method when you populate hello [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

```csharp
// Task 'taskA' doesn't depend on any other tasks
new CloudTask("taskA", "cmd.exe /c echo taskA"),

// Task 'taskB' depends on completion of task 'taskA'
new CloudTask("taskB", "cmd.exe /c echo taskB")
{
    DependsOn = TaskDependencies.OnId("taskA")
},
```

### <a name="one-to-many"></a><span data-ttu-id="41462-161">Uno-a-molti</span><span class="sxs-lookup"><span data-stu-id="41462-161">One-to-many</span></span>
<span data-ttu-id="41462-162">In una relazione uno-a-molti, un'attività dipende dal completamento di hello di più attività padre.</span><span class="sxs-lookup"><span data-stu-id="41462-162">In a one-to-many relationship, a task depends on hello completion of multiple parent tasks.</span></span> <span data-ttu-id="41462-163">toocreate hello dipendenza, offrono un insieme di attività ID toohello [TaskDependencies][net_taskdependencies].[ OnIds] [ net_onids] metodo statico quando si popola hello [DependsOn] [ net_dependson] proprietà di [CloudTask] [ net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="41462-163">toocreate hello dependency, provide a collection of task IDs toohello [TaskDependencies][net_taskdependencies].[OnIds][net_onids] static method when you populate hello [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

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

### <a name="task-id-range"></a><span data-ttu-id="41462-164">Intervallo di ID attività</span><span class="sxs-lookup"><span data-stu-id="41462-164">Task ID range</span></span>
<span data-ttu-id="41462-165">Una dipendenza su un intervallo di attività padre, un'attività dipende dal completamento di hello hello delle attività i cui ID sono situati all'interno di un intervallo.</span><span class="sxs-lookup"><span data-stu-id="41462-165">In a dependency on a range of parent tasks, a task depends on hello hello completion of tasks whose IDs lie within a range.</span></span>
<span data-ttu-id="41462-166">dipendenza hello toocreate, fornire hello prima e ultima attività ID in hello intervallo toohello [TaskDependencies][net_taskdependencies].[ OnIdRange] [ net_onidrange] metodo statico quando si popola hello [DependsOn] [ net_dependson] proprietà di [CloudTask] [net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="41462-166">toocreate hello dependency, provide hello first and last task IDs in hello range toohello [TaskDependencies][net_taskdependencies].[OnIdRange][net_onidrange] static method when you populate hello [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="41462-167">Quando si usano gli intervalli di ID attività per le dipendenze, hello ID attività nell'intervallo di hello *deve* da rappresentazioni di stringa di valori integer.</span><span class="sxs-lookup"><span data-stu-id="41462-167">When you use task ID ranges for your dependencies, hello task IDs in hello range *must* be string representations of integer values.</span></span>
> 
> <span data-ttu-id="41462-168">Ogni attività nell'intervallo di hello devono soddisfare dipendenza hello, completamento o completando con un errore che è mappata tooa dipendenza azione impostare troppo**Satisfies**.</span><span class="sxs-lookup"><span data-stu-id="41462-168">Every task in hello range must satisfy hello dependency, either by completing successfully or by completing with a failure that’s mapped tooa dependency action set too**Satisfy**.</span></span> <span data-ttu-id="41462-169">Vedere hello [azioni dipendenza](#dependency-actions) sezione per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="41462-169">See hello [Dependency actions](#dependency-actions) section for details.</span></span>
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
    // toouse a range of tasks, their ids must be integer values.
    // Note that we pass integers as parameters tooTaskIdRange,
    // but their ids (above) are string representations of hello ids.
    DependsOn = TaskDependencies.OnIdRange(1, 3)
},
```

## <a name="dependency-actions"></a><span data-ttu-id="41462-170">Azioni di dipendenza</span><span class="sxs-lookup"><span data-stu-id="41462-170">Dependency actions</span></span>

<span data-ttu-id="41462-171">Per impostazione predefinita, un'attività o un set di attività dipendenti vengono eseguite solo dopo il corretto completamento di un'attività padre.</span><span class="sxs-lookup"><span data-stu-id="41462-171">By default, a dependent task or set of tasks runs only after a parent task has completed successfully.</span></span> <span data-ttu-id="41462-172">In alcuni scenari, è consigliabile attività dipendenti toorun anche se l'attività padre hello ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="41462-172">In some scenarios, you may want toorun dependent tasks even if hello parent task fails.</span></span> <span data-ttu-id="41462-173">È possibile eseguire l'override di comportamento predefinito di hello specificando un'azione di dipendenza.</span><span class="sxs-lookup"><span data-stu-id="41462-173">You can override hello default behavior by specifying a dependency action.</span></span> <span data-ttu-id="41462-174">Un'azione di dipendenza specifica se un'attività dipendente è idoneo toorun, in base a hello riuscita o meno delle attività padre hello.</span><span class="sxs-lookup"><span data-stu-id="41462-174">A dependency action specifies whether a dependent task is eligible toorun, based on hello success or failure of hello parent task.</span></span> 

<span data-ttu-id="41462-175">Ad esempio, si supponga che un'attività dipendente è in attesa di dati dal completamento hello dell'attività upstream hello.</span><span class="sxs-lookup"><span data-stu-id="41462-175">For example, suppose that a dependent task is awaiting data from hello completion of hello upstream task.</span></span> <span data-ttu-id="41462-176">Se attività upstream hello non riesce, l'attività dipendente hello potrebbe essere ancora in grado di toorun i dati obsoleti.</span><span class="sxs-lookup"><span data-stu-id="41462-176">If hello upstream task fails, hello dependent task may still be able toorun using older data.</span></span> <span data-ttu-id="41462-177">In questo caso, un'azione di dipendenza è possibile specificare che tale attività dipendente hello è idoneo toorun nonostante l'errore hello dell'attività padre hello.</span><span class="sxs-lookup"><span data-stu-id="41462-177">In this case, a dependency action can specify that hello dependent task is eligible toorun despite hello failure of hello parent task.</span></span>

<span data-ttu-id="41462-178">Un'azione di dipendenza si basa su una condizione di uscita per l'attività padre hello.</span><span class="sxs-lookup"><span data-stu-id="41462-178">A dependency action is based on an exit condition for hello parent task.</span></span> <span data-ttu-id="41462-179">È possibile specificare un'azione di dipendenza per una delle seguenti condizioni di uscita; hello per .NET, vedere hello [ExitConditions] [ net_exitconditions] classe per informazioni dettagliate:</span><span class="sxs-lookup"><span data-stu-id="41462-179">You can specify a dependency action for any of hello following exit conditions; for .NET, see hello [ExitConditions][net_exitconditions] class for details:</span></span>

- <span data-ttu-id="41462-180">Quando si verifica un errore di pre-elaborazione.</span><span class="sxs-lookup"><span data-stu-id="41462-180">When a pre-processing error occurs.</span></span>
- <span data-ttu-id="41462-181">Quando si verifica un errore di caricamento dei file.</span><span class="sxs-lookup"><span data-stu-id="41462-181">When a file upload error occurs.</span></span> <span data-ttu-id="41462-182">Se l'attività hello viene terminata con un codice di uscita specificato tramite **exitCodes** o **exitCodeRanges**e quindi si verifica un errore di caricamento di file, l'azione hello specificata da hello uscita codice avrà la precedenza.</span><span class="sxs-lookup"><span data-stu-id="41462-182">If hello task exits with an exit code that was specified via **exitCodes** or **exitCodeRanges**, and then encounters a file upload error, hello action specified by hello exit code takes precedence.</span></span>
- <span data-ttu-id="41462-183">Quando attività hello termina con un codice di uscita definito da hello **ExitCodes** proprietà.</span><span class="sxs-lookup"><span data-stu-id="41462-183">When hello task exits with an exit code defined by hello **ExitCodes** property.</span></span>
- <span data-ttu-id="41462-184">Quando attività hello termina con un codice di uscita che rientra in un intervallo specificato da hello **ExitCodeRanges** proprietà.</span><span class="sxs-lookup"><span data-stu-id="41462-184">When hello task exits with an exit code that falls within a range specified by hello **ExitCodeRanges** property.</span></span>
- <span data-ttu-id="41462-185">Hello caso predefinito, se l'attività hello termina con un codice di uscita non è definito da **ExitCodes** o **ExitCodeRanges**, o se l'attività hello termina con un errore di pre-elaborazione e hello **PreProcessingError**  non è impostata, o se hello attività non riesce e genera un file di caricamento di errore e hello **FileUploadError** non è impostata.</span><span class="sxs-lookup"><span data-stu-id="41462-185">hello default case, if hello task exits with an exit code not defined by **ExitCodes** or **ExitCodeRanges**, or if hello task exits with a pre-processing error and hello **PreProcessingError** property is not set, or if hello task fails with a file upload error and hello **FileUploadError** property is not set.</span></span> 

<span data-ttu-id="41462-186">un'azione di dipendenza in .NET, hello set toospecify [ExitOptions][net_exitoptions].[ DependencyAction] [ net_dependencyaction] proprietà per la condizione di uscita hello.</span><span class="sxs-lookup"><span data-stu-id="41462-186">toospecify a dependency action in .NET, set hello [ExitOptions][net_exitoptions].[DependencyAction][net_dependencyaction] property for hello exit condition.</span></span> <span data-ttu-id="41462-187">Hello **DependencyAction** proprietà prende uno dei due valori:</span><span class="sxs-lookup"><span data-stu-id="41462-187">hello **DependencyAction** property takes one of two values:</span></span>

- <span data-ttu-id="41462-188">Hello impostazione **DependencyAction** proprietà troppo**Satisfies** indica che le attività dipendenti sono idonei toorun se l'attività padre hello termina con un errore specificato.</span><span class="sxs-lookup"><span data-stu-id="41462-188">Setting hello **DependencyAction** property too**Satisfy** indicates that dependent tasks are eligible toorun if hello parent task exits with a specified error.</span></span>
- <span data-ttu-id="41462-189">Hello impostazione **DependencyAction** proprietà troppo**blocco** indica che le attività dipendenti non sono idonee toorun.</span><span class="sxs-lookup"><span data-stu-id="41462-189">Setting hello **DependencyAction** property too**Block** indicates that dependent tasks are not eligible toorun.</span></span>

<span data-ttu-id="41462-190">impostazione predefinita per hello Hello **DependencyAction** proprietà **Satisfies** per il codice di uscita 0, e **blocco** per tutte le altre condizioni di uscita.</span><span class="sxs-lookup"><span data-stu-id="41462-190">hello default setting for hello **DependencyAction** property is **Satisfy** for exit code 0, and **Block** for all other exit conditions.</span></span>

<span data-ttu-id="41462-191">frammento di codice seguente Hello imposta hello **DependencyAction** proprietà per un'attività padre.</span><span class="sxs-lookup"><span data-stu-id="41462-191">hello following code snippet sets hello **DependencyAction** property for a parent task.</span></span> <span data-ttu-id="41462-192">Se l'attività padre hello termina con un errore di pre-elaborazione o con hello hello dipendenti codici di errore specificato, l'attività è bloccata.</span><span class="sxs-lookup"><span data-stu-id="41462-192">If hello parent task exits with a pre-processing error, or with hello specified error codes, hello dependent task is blocked.</span></span> <span data-ttu-id="41462-193">Se l'attività padre hello viene terminato con un altro errore diverso da zero, l'attività dipendente hello è toorun idonei.</span><span class="sxs-lookup"><span data-stu-id="41462-193">If hello parent task exits with any other non-zero error, hello dependent task is eligible toorun.</span></span>

```csharp
// Task A is hello parent task.
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
        // If task A exits with hello specified error codes, block any downstream tasks (in this example, task B).
        ExitCodes = new List<ExitCodeMapping>
        {
            new ExitCodeMapping(10, new ExitOptions() { DependencyAction = DependencyAction.Block }),
            new ExitCodeMapping(20, new ExitOptions() { DependencyAction = DependencyAction.Block })
        },
        // If task A succeeds or fails with any other error, any downstream tasks become eligible toorun 
        // (in this example, task B).
        Default = new ExitOptions
        {
            DependencyAction = DependencyAction.Satisfy
        }
    }
},
// Task B depends on task A. Whether it becomes eligible toorun depends on how task A exits.
new CloudTask("B", "cmd.exe /c echo B")
{
    DependsOn = TaskDependencies.OnId("A")
},
```

## <a name="code-sample"></a><span data-ttu-id="41462-194">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="41462-194">Code sample</span></span>
<span data-ttu-id="41462-195">Hello [TaskDependencies] [ github_taskdependencies] progetto di esempio è uno dei hello [esempi di codice di Azure Batch] [ github_samples] su GitHub.</span><span class="sxs-lookup"><span data-stu-id="41462-195">hello [TaskDependencies][github_taskdependencies] sample project is one of hello [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="41462-196">Questa soluzione di Visual Studio mostra:</span><span class="sxs-lookup"><span data-stu-id="41462-196">This Visual Studio solution demonstrates:</span></span>

- <span data-ttu-id="41462-197">Come tooenable attività dipendenza su un processo</span><span class="sxs-lookup"><span data-stu-id="41462-197">How tooenable task dependency on a job</span></span>
- <span data-ttu-id="41462-198">Modalità toocreate attività da cui dipendono altre attività</span><span class="sxs-lookup"><span data-stu-id="41462-198">How toocreate tasks that depend on other tasks</span></span>
- <span data-ttu-id="41462-199">Modalità tooexecute quelli delle attività in un pool di nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="41462-199">How tooexecute those tasks on a pool of compute nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="41462-200">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="41462-200">Next steps</span></span>
### <a name="application-deployment"></a><span data-ttu-id="41462-201">Distribuzione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="41462-201">Application deployment</span></span>
<span data-ttu-id="41462-202">Hello [pacchetti di applicazioni](batch-application-packages.md) funzionalità di Batch fornisce un modo semplice distribuire tooboth e la versione applicazioni hello le attività eseguite in nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="41462-202">hello [application packages](batch-application-packages.md) feature of Batch provides an easy way tooboth deploy and version hello applications that your tasks execute on compute nodes.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="41462-203">Installazione delle applicazioni e staging dei dati</span><span class="sxs-lookup"><span data-stu-id="41462-203">Installing applications and staging data</span></span>
<span data-ttu-id="41462-204">Vedere [l'installazione di applicazioni e dati in Batch di gestione temporanea di nodi di calcolo] [ forum_post] nel forum di Azure Batch hello per una panoramica dei metodi per la preparazione dei nodi toorun attività.</span><span class="sxs-lookup"><span data-stu-id="41462-204">See [Installing applications and staging data on Batch compute nodes][forum_post] in hello Azure Batch forum for an overview of methods for preparing your nodes toorun tasks.</span></span> <span data-ttu-id="41462-205">Scritti da uno dei membri del team hello Azure Batch, che questo post di è una buona panoramica sulle applicazioni di toocopy hello modi diversi, i dati di input attività e altri tooyour file nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="41462-205">Written by one of hello Azure Batch team members, this post is a good primer on hello different ways toocopy applications, task input data, and other files tooyour compute nodes.</span></span>

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

[1]: ./media/batch-task-dependency/01_one_to_one.png "Diagramma: relazione uno-a-uno"
[2]: ./media/batch-task-dependency/02_one_to_many.png "Diagramma: relazione uno-a-molti"
[3]: ./media/batch-task-dependency/03_task_id_range.png "Diagramma: relazione tra intervalli di ID attività"
