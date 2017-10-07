---
title: "aaaCreate attività tooprepare processi e completa sui nodi di calcolo - Azure Batch | Documenti Microsoft"
description: "Dati di utilizzo a livello di processo di preparazione attività toominimize trasferire tooAzure nodi di calcolo di Batch e rilasciare l'attività per la pulizia del nodo al completamento del processo."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 63d9d4f1-8521-4bbb-b95a-c4cad73692d3
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fd5fb47ae6700281e63048c49a1241f4e935baba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-job-preparation-and-job-release-tasks-on-batch-compute-nodes"></a><span data-ttu-id="6c882-103">Eseguire attività di preparazione e rilascio del processo in nodi di calcolo di Batch</span><span class="sxs-lookup"><span data-stu-id="6c882-103">Run job preparation and job release tasks on Batch compute nodes</span></span>

 <span data-ttu-id="6c882-104">Un processo di Azure Batch richiede spesso alcune operazioni di configurazione prima dell'esecuzione delle attività e di manutenzione post-processo dopo il completamento delle attività.</span><span class="sxs-lookup"><span data-stu-id="6c882-104">An Azure Batch job often requires some form of setup before its tasks are executed, and post-job maintenance when its tasks are completed.</span></span> <span data-ttu-id="6c882-105">È possibile necessario toodownload comuni attività dati di input tooyour calcolo nodi o caricare attività output dati tooAzure archiviazione dopo completamento del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="6c882-105">You might need toodownload common task input data tooyour compute nodes, or upload task output data tooAzure Storage after hello job completes.</span></span> <span data-ttu-id="6c882-106">È possibile utilizzare **processo preparazione** e **processo versione** attività tooperform queste operazioni.</span><span class="sxs-lookup"><span data-stu-id="6c882-106">You can use **job preparation** and **job release** tasks tooperform these operations.</span></span>

## <a name="what-are-job-preparation-and-release-tasks"></a><span data-ttu-id="6c882-107">Quali sono le attività di preparazione e rilascio dei processi</span><span class="sxs-lookup"><span data-stu-id="6c882-107">What are job preparation and release tasks?</span></span>
<span data-ttu-id="6c882-108">Prima di eseguire attività di un processo, l'attività di preparazione processo hello viene eseguito su tutti toorun di pianificata di nodi di calcolo almeno un'attività.</span><span class="sxs-lookup"><span data-stu-id="6c882-108">Before a job's tasks run, hello job preparation task runs on all compute nodes scheduled toorun at least one task.</span></span> <span data-ttu-id="6c882-109">Una volta completato il processo di hello, attività di rilascio di hello processo viene eseguito su ogni nodo nel pool di hello eseguita almeno un'attività.</span><span class="sxs-lookup"><span data-stu-id="6c882-109">Once hello job is completed, hello job release task runs on each node in hello pool that executed at least one task.</span></span> <span data-ttu-id="6c882-110">Come con le normale attività di Batch, è possibile specificare toobe una riga di comando viene richiamato ogni volta una preparazione del processo o attività di rilascio viene eseguito.</span><span class="sxs-lookup"><span data-stu-id="6c882-110">As with normal Batch tasks, you can specify a command line toobe invoked when a job preparation or release task is run.</span></span>

<span data-ttu-id="6c882-111">Le attività di preparazione e rilascio del processo offrono funzionalità familiari per le attività di Batch, quali download di file ([file di risorse][net_job_prep_resourcefiles]), esecuzione con privilegi elevati, variabili di ambiente personalizzate, durata massima di esecuzione, numero di tentativi e periodo di conservazione dei file.</span><span class="sxs-lookup"><span data-stu-id="6c882-111">Job preparation and release tasks offer familiar Batch task features such as file download ([resource files][net_job_prep_resourcefiles]), elevated execution, custom environment variables, maximum execution duration, retry count, and file retention time.</span></span>

<span data-ttu-id="6c882-112">Nella seguenti sezioni di hello, si apprenderà come hello toouse [JobPreparationTask] [ net_job_prep] e [JobReleaseTask] [ net_job_release] classi contenute nello hello [.NET per batch] [ api_net] libreria.</span><span class="sxs-lookup"><span data-stu-id="6c882-112">In hello following sections, you'll learn how toouse hello [JobPreparationTask][net_job_prep] and [JobReleaseTask][net_job_release] classes found in hello [Batch .NET][api_net] library.</span></span>

> [!TIP]
> <span data-ttu-id="6c882-113">Le attività di preparazione e rilascio del processo sono particolarmente utili in ambienti con "pool condivisi", in cui un pool di nodi di calcolo viene mantenuto durante l'esecuzione di un processo e viene usato da più processi.</span><span class="sxs-lookup"><span data-stu-id="6c882-113">Job preparation and release tasks are especially helpful in "shared pool" environments, in which a pool of compute nodes persists between job runs and is used by many jobs.</span></span>
> 
> 

## <a name="when-toouse-job-preparation-and-release-tasks"></a><span data-ttu-id="6c882-114">Quando toouse preparazione del processo e rilasciare l'attività</span><span class="sxs-lookup"><span data-stu-id="6c882-114">When toouse job preparation and release tasks</span></span>
<span data-ttu-id="6c882-115">Preparazione del processo e le attività di rilascio di processo sono ideali per hello seguenti situazioni:</span><span class="sxs-lookup"><span data-stu-id="6c882-115">Job preparation and job release tasks are a good fit for hello following situations:</span></span>

<span data-ttu-id="6c882-116">**Download dei dati delle attività comuni**</span><span class="sxs-lookup"><span data-stu-id="6c882-116">**Download common task data**</span></span>

<span data-ttu-id="6c882-117">I processi batch richiedono spesso un set comune di dati come input per l'attività del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="6c882-117">Batch jobs often require a common set of data as input for hello job's tasks.</span></span> <span data-ttu-id="6c882-118">Ad esempio, nei calcoli di analisi dei rischi giornaliera, dati di mercato sono specifici ancora comuni attività tooall hello processo.</span><span class="sxs-lookup"><span data-stu-id="6c882-118">For example, in daily risk analysis calculations, market data is job-specific, yet common tooall tasks in hello job.</span></span> <span data-ttu-id="6c882-119">Questi dati di mercato, dimensioni, spesso diversi gigabyte devono essere solo una volta scaricato tooeach del nodo di calcolo in modo che qualsiasi attività che viene eseguita nel nodo hello possibile utilizzarlo.</span><span class="sxs-lookup"><span data-stu-id="6c882-119">This market data, often several gigabytes in size, should be downloaded tooeach compute node only once so that any task that runs on hello node can use it.</span></span> <span data-ttu-id="6c882-120">Utilizzare un **attività di preparazione del processo** toodownload questo nodo tooeach dati prima che esecuzione hello del processo di hello altre attività.</span><span class="sxs-lookup"><span data-stu-id="6c882-120">Use a **job preparation task** toodownload this data tooeach node before hello execution of hello job's other tasks.</span></span>

<span data-ttu-id="6c882-121">**Eliminazione dell'output di processi e attività**</span><span class="sxs-lookup"><span data-stu-id="6c882-121">**Delete job and task output**</span></span>

<span data-ttu-id="6c882-122">In un ambiente "shared pool", in cui i nodi di calcolo di un pool non sono rimossi tra processi, potrebbe essere dati del processo toodelete tra le esecuzioni.</span><span class="sxs-lookup"><span data-stu-id="6c882-122">In a "shared pool" environment, where a pool's compute nodes are not decommissioned between jobs, you may need toodelete job data between runs.</span></span> <span data-ttu-id="6c882-123">Potrebbe essere necessario tooconserve spazio sui nodi hello, o che soddisfano i criteri di sicurezza dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="6c882-123">You might need tooconserve disk space on hello nodes, or satisfy your organization's security policies.</span></span> <span data-ttu-id="6c882-124">Utilizzare un **versione mansione** toodelete dati che è stati scaricati da un'attività di preparazione del processo o generati durante l'esecuzione dell'attività.</span><span class="sxs-lookup"><span data-stu-id="6c882-124">Use a **job release task** toodelete data that was downloaded by a job preparation task, or generated during task execution.</span></span>

<span data-ttu-id="6c882-125">**Conservazione dei log**</span><span class="sxs-lookup"><span data-stu-id="6c882-125">**Log retention**</span></span>

<span data-ttu-id="6c882-126">È possibile tookeep una copia del file di log che generano le attività, o forse i file di dump di arresto anomalo del sistema possono essere generati da errori nelle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="6c882-126">You might want tookeep a copy of log files that your tasks generate, or perhaps crash dump files that can be generated by failed applications.</span></span> <span data-ttu-id="6c882-127">Utilizzare un **versione mansione** in tali casi di toocompress e caricare questo tooan dati [di archiviazione di Azure] [ azure_storage] account.</span><span class="sxs-lookup"><span data-stu-id="6c882-127">Use a **job release task** in such cases toocompress and upload this data tooan [Azure Storage][azure_storage] account.</span></span>

> [!TIP]
> <span data-ttu-id="6c882-128">Un altro modo toopersist log, l'attività e altri processi di output dei dati sono hello toouse [convenzioni File Batch di Azure](batch-task-output.md) libreria.</span><span class="sxs-lookup"><span data-stu-id="6c882-128">Another way toopersist logs and other job and task output data is toouse hello [Azure Batch File Conventions](batch-task-output.md) library.</span></span>
> 
> 

## <a name="job-preparation-task"></a><span data-ttu-id="6c882-129">attività di preparazione del processo</span><span class="sxs-lookup"><span data-stu-id="6c882-129">Job preparation task</span></span>
<span data-ttu-id="6c882-130">Prima dell'esecuzione di attività di un processo, Batch esegue l'attività di preparazione processo hello in ogni nodo di calcolo è toorun pianificata un'attività.</span><span class="sxs-lookup"><span data-stu-id="6c882-130">Before execution of a job's tasks, Batch executes hello job preparation task on each compute node that is scheduled toorun a task.</span></span> <span data-ttu-id="6c882-131">Per impostazione predefinita, il servizio Batch hello attende hello processo preparazione attività toobe completato prima di eseguire hello attività pianificate tooexecute nel nodo hello.</span><span class="sxs-lookup"><span data-stu-id="6c882-131">By default, hello Batch service waits for hello job preparation task toobe completed before running hello tasks scheduled tooexecute on hello node.</span></span> <span data-ttu-id="6c882-132">Tuttavia, è possibile configurare il servizio di hello non toowait.</span><span class="sxs-lookup"><span data-stu-id="6c882-132">However, you can configure hello service not toowait.</span></span> <span data-ttu-id="6c882-133">Se si riavvia il nodo di hello, viene eseguito di nuovo l'attività di preparazione processo hello, ma è anche possibile disabilitare questo comportamento.</span><span class="sxs-lookup"><span data-stu-id="6c882-133">If hello node restarts, hello job preparation task runs again, but you can also disable this behavior.</span></span>

<span data-ttu-id="6c882-134">l'attività di preparazione processo Hello viene eseguita solo per i nodi che vengono pianificati toorun un'attività.</span><span class="sxs-lookup"><span data-stu-id="6c882-134">hello job preparation task is executed only on nodes that are scheduled toorun a task.</span></span> <span data-ttu-id="6c882-135">Ciò impedisce l'esecuzione non necessari di hello di un'attività di preparazione nel caso in cui un nodo non viene assegnata un'attività.</span><span class="sxs-lookup"><span data-stu-id="6c882-135">This prevents hello unnecessary execution of a preparation task in case a node is not assigned a task.</span></span> <span data-ttu-id="6c882-136">Ciò può verificarsi quando il numero di hello di attività per un processo è minore di numero hello di nodi in un pool.</span><span class="sxs-lookup"><span data-stu-id="6c882-136">This can occur when hello number of tasks for a job is less than hello number of nodes in a pool.</span></span> <span data-ttu-id="6c882-137">Si applica anche quando [esecuzione di attività simultanee](batch-parallel-node-tasks.md) è abilitato, che lascia alcuni nodi inattiva se il numero di attività hello è inferiore a hello totale possibili le attività simultanee.</span><span class="sxs-lookup"><span data-stu-id="6c882-137">It also applies when [concurrent task execution](batch-parallel-node-tasks.md) is enabled, which leaves some nodes idle if hello task count is lower than hello total possible concurrent tasks.</span></span> <span data-ttu-id="6c882-138">Da non in esecuzione l'attività di preparazione processo hello nei nodi di inattività, è possibile spesa sugli addebiti di trasferimento dati.</span><span class="sxs-lookup"><span data-stu-id="6c882-138">By not running hello job preparation task on idle nodes, you can spend less money on data transfer charges.</span></span>

> [!NOTE]
> <span data-ttu-id="6c882-139">[JobPreparationTask] [ net_job_prep_cloudjob] è diverso da [CloudPool.StartTask] [ pool_starttask] in JobPreparationTask viene eseguita all'avvio di hello di ogni processo, mentre StartTask viene eseguita solo quando un nodo di calcolo prima viene aggiunto a un pool o riavvio.</span><span class="sxs-lookup"><span data-stu-id="6c882-139">[JobPreparationTask][net_job_prep_cloudjob] differs from [CloudPool.StartTask][pool_starttask] in that JobPreparationTask executes at hello start of each job, whereas StartTask executes only when a compute node first joins a pool or restarts.</span></span>
> 
> 

## <a name="job-release-task"></a><span data-ttu-id="6c882-140">attività di rilascio del processo</span><span class="sxs-lookup"><span data-stu-id="6c882-140">Job release task</span></span>
<span data-ttu-id="6c882-141">Quando un processo è stato contrassegnato come completato, attività di rilascio di hello processo viene eseguito su ogni nodo nel pool di hello eseguita almeno un'attività.</span><span class="sxs-lookup"><span data-stu-id="6c882-141">Once a job is marked as completed, hello job release task is executed on each node in hello pool that executed at least one task.</span></span> <span data-ttu-id="6c882-142">Un processo viene contrassegnato come completato generando una richiesta di interruzione.</span><span class="sxs-lookup"><span data-stu-id="6c882-142">You mark a job as completed by issuing a terminate request.</span></span> <span data-ttu-id="6c882-143">Hello servizio Batch, quindi imposta hello lo stato del processo troppo*terminazione*, interrompe tutte le attività attive o in esecuzione associate al processo hello ed esegue attività di rilascio processo hello.</span><span class="sxs-lookup"><span data-stu-id="6c882-143">hello Batch service then sets hello job state too*terminating*, terminates any active or running tasks associated with hello job, and runs hello job release task.</span></span> <span data-ttu-id="6c882-144">il processo di Hello passa quindi toohello *completato* stato.</span><span class="sxs-lookup"><span data-stu-id="6c882-144">hello job then moves toohello *completed* state.</span></span>

> [!NOTE]
> <span data-ttu-id="6c882-145">L'eliminazione di processo anche l'esecuzione di attività di rilascio processo hello.</span><span class="sxs-lookup"><span data-stu-id="6c882-145">Job deletion also executes hello job release task.</span></span> <span data-ttu-id="6c882-146">Tuttavia, se un processo è già stato terminato, attività di rilascio hello non viene eseguito una seconda volta se il processo di hello viene eliminato in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="6c882-146">However, if a job has already been terminated, hello release task is not run a second time if hello job is later deleted.</span></span>
> 
> 

## <a name="job-prep-and-release-tasks-with-batch-net"></a><span data-ttu-id="6c882-147">Attività di preparazione e di rilascio del processo con Batch .NET</span><span class="sxs-lookup"><span data-stu-id="6c882-147">Job prep and release tasks with Batch .NET</span></span>
<span data-ttu-id="6c882-148">toouse un'attività di preparazione del processo, assegnare un [JobPreparationTask] [ net_job_prep] processo tooyour oggetti [CloudJob.JobPreparationTask] [ net_job_prep_cloudjob] proprietà .</span><span class="sxs-lookup"><span data-stu-id="6c882-148">toouse a job preparation task, assign a [JobPreparationTask][net_job_prep] object tooyour job's [CloudJob.JobPreparationTask][net_job_prep_cloudjob] property.</span></span> <span data-ttu-id="6c882-149">Analogamente, inizializzare un [JobReleaseTask] [ net_job_release] e assegnarlo del processo tooyour [CloudJob.JobReleaseTask] [ net_job_prep_cloudjob] hello tooset proprietà attività di rilascio del processo.</span><span class="sxs-lookup"><span data-stu-id="6c882-149">Similarly, initialize a [JobReleaseTask][net_job_release] and assign it tooyour job's [CloudJob.JobReleaseTask][net_job_prep_cloudjob] property tooset hello job's release task.</span></span>

<span data-ttu-id="6c882-150">In questo frammento di codice, `myBatchClient` è un'istanza di [BatchClient][net_batch_client], e `myPool` è un pool esistente all'interno di hello account Batch.</span><span class="sxs-lookup"><span data-stu-id="6c882-150">In this code snippet, `myBatchClient` is an instance of [BatchClient][net_batch_client], and `myPool` is an existing pool within hello Batch account.</span></span>

```csharp
// Create hello CloudJob for CloudPool "myPool"
CloudJob myJob =
    myBatchClient.JobOperations.CreateJob(
        "JobPrepReleaseSampleJob",
        new PoolInformation() { PoolId = "myPool" });

// Specify hello command lines for hello job preparation and release tasks
string jobPrepCmdLine =
    "cmd /c echo %AZ_BATCH_NODE_ID% > %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";
string jobReleaseCmdLine =
    "cmd /c del %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";

// Assign hello job preparation task toohello job
myJob.JobPreparationTask =
    new JobPreparationTask { CommandLine = jobPrepCmdLine };

// Assign hello job release task toohello job
myJob.JobReleaseTask =
    new JobPreparationTask { CommandLine = jobReleaseCmdLine };

await myJob.CommitAsync();
```

<span data-ttu-id="6c882-151">Come accennato in precedenza, attività di rilascio hello viene eseguito quando un processo viene terminato o eliminato.</span><span class="sxs-lookup"><span data-stu-id="6c882-151">As mentioned earlier, hello release task is executed when a job is terminated or deleted.</span></span> <span data-ttu-id="6c882-152">Terminare un processo con [JobOperations.TerminateJobAsync][net_job_terminate].</span><span class="sxs-lookup"><span data-stu-id="6c882-152">Terminate a job with [JobOperations.TerminateJobAsync][net_job_terminate].</span></span> <span data-ttu-id="6c882-153">Eliminare un processo con [JobOperations.DeleteJobAsync][net_job_delete].</span><span class="sxs-lookup"><span data-stu-id="6c882-153">Delete a job with [JobOperations.DeleteJobAsync][net_job_delete].</span></span> <span data-ttu-id="6c882-154">In genere si termina o si elimina un processo quando le attività vengono completate o quando si raggiunge un timeout definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="6c882-154">You typically terminate or delete a job when its tasks are completed, or when a timeout that you've defined has been reached.</span></span>

```csharp
// Terminate hello job toomark it as Completed; this will initiate the
// Job Release Task on any node that executed job tasks. Note that the
// Job Release Task is also executed when a job is deleted, thus you
// need not call Terminate if you typically delete jobs after task completion.
await myBatchClient.JobOperations.TerminateJobAsy("JobPrepReleaseSampleJob");
```

## <a name="code-sample-on-github"></a><span data-ttu-id="6c882-155">Esempio di codice in GitHub</span><span class="sxs-lookup"><span data-stu-id="6c882-155">Code sample on GitHub</span></span>
<span data-ttu-id="6c882-156">attività toosee processo di preparazione e rilascio in azione, estrarre hello [JobPrepRelease] [ job_prep_release_sample] progetto di esempio su GitHub.</span><span class="sxs-lookup"><span data-stu-id="6c882-156">toosee job preparation and release tasks in action, check out hello [JobPrepRelease][job_prep_release_sample] sample project on GitHub.</span></span> <span data-ttu-id="6c882-157">Questa applicazione console hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="6c882-157">This console application does hello following:</span></span>

1. <span data-ttu-id="6c882-158">Crea un pool con due nodi "small".</span><span class="sxs-lookup"><span data-stu-id="6c882-158">Creates a pool with two "small" nodes.</span></span>
2. <span data-ttu-id="6c882-159">Crea un processo con attività di preparazione e rilascio di processi e attività standard.</span><span class="sxs-lookup"><span data-stu-id="6c882-159">Creates a job with job preparation, release, and standard tasks.</span></span>
3. <span data-ttu-id="6c882-160">Esecuzioni hello attività di preparazione processo, che scrive i file di testo tooa ID nodo hello innanzitutto nella directory "condiviso" un nodo.</span><span class="sxs-lookup"><span data-stu-id="6c882-160">Runs hello job preparation task, which first writes hello node ID tooa text file in a node's "shared" directory.</span></span>
4. <span data-ttu-id="6c882-161">Esegue un'attività in ogni nodo che scrive il toohello ID attività file di testo stesso.</span><span class="sxs-lookup"><span data-stu-id="6c882-161">Runs a task on each node that writes its task ID toohello same text file.</span></span>
5. <span data-ttu-id="6c882-162">Una volta che vengono completate tutte le attività (o viene raggiunto il timeout di hello), stampa il contenuto di hello della console toohello file testo di ciascun nodo.</span><span class="sxs-lookup"><span data-stu-id="6c882-162">Once all tasks are completed (or hello timeout is reached), prints hello contents of each node's text file toohello console.</span></span>
6. <span data-ttu-id="6c882-163">Al termine dell'esecuzione processo hello, per eseguire hello processo versione attività toodelete hello file dal nodo hello.</span><span class="sxs-lookup"><span data-stu-id="6c882-163">When hello job is completed, runs hello job release task toodelete hello file from hello node.</span></span>
7. <span data-ttu-id="6c882-164">Hello stampe codici di preparazione del processo hello di uscita e rilasciare le attività per ogni nodo in cui è stato eseguito.</span><span class="sxs-lookup"><span data-stu-id="6c882-164">Prints hello exit codes of hello job preparation and release tasks for each node on which they executed.</span></span>
8. <span data-ttu-id="6c882-165">Mette in pausa esecuzione tooallow conferma dell'eliminazione di processo e/o pool.</span><span class="sxs-lookup"><span data-stu-id="6c882-165">Pauses execution tooallow confirmation of job and/or pool deletion.</span></span>

<span data-ttu-id="6c882-166">Output di applicazione di esempio hello è simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="6c882-166">Output from hello sample application is similar toohello following:</span></span>

```
Attempting toocreate pool: JobPrepReleaseSamplePool
Created pool JobPrepReleaseSamplePool with 2 small nodes
Checking for existing job JobPrepReleaseSampleJob...
Job JobPrepReleaseSampleJob not found, creating...
Submitting tasks and awaiting completion...
All tasks completed.

Contents of shared\job_prep_and_release.txt on tvm-2434664350_1-20160623t173951z:
-------------------------------------------
tvm-2434664350_1-20160623t173951z tasks:
  task001
  task004
  task005
  task006

Contents of shared\job_prep_and_release.txt on tvm-2434664350_2-20160623t173951z:
-------------------------------------------
tvm-2434664350_2-20160623t173951z tasks:
  task008
  task002
  task003
  task007

Waiting for job JobPrepReleaseSampleJob tooreach state Completed
...

tvm-2434664350_1-20160623t173951z:
  Prep task exit code:    0
  Release task exit code: 0

tvm-2434664350_2-20160623t173951z:
  Prep task exit code:    0
  Release task exit code: 0

Delete job? [yes] no
yes
Delete pool? [yes] no
yes

Sample complete, hit ENTER tooexit...
```

> [!NOTE]
> <span data-ttu-id="6c882-167">A causa di toohello variabile creazione e ora di inizio nodi in un nuovo pool (alcuni nodi sono pronti per l'attività prima degli altri), verrà visualizzato un output diverso.</span><span class="sxs-lookup"><span data-stu-id="6c882-167">Due toohello variable creation and start time of nodes in a new pool (some nodes are ready for tasks before others), you may see different output.</span></span> <span data-ttu-id="6c882-168">In particolare, in quanto attività hello completato rapidamente, uno dei nodi del pool di hello può eseguire tutte le attività del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="6c882-168">Specifically, because hello tasks complete quickly, one of hello pool's nodes may execute all of hello job's tasks.</span></span> <span data-ttu-id="6c882-169">In questo caso, si noterà che hello preparazione del processo e rilasciare l'attività non esistono per il nodo hello non eseguita alcuna attività.</span><span class="sxs-lookup"><span data-stu-id="6c882-169">If this occurs, you will notice that hello job prep and release tasks do not exist for hello node that executed no tasks.</span></span>
> 
> 

### <a name="inspect-job-preparation-and-release-tasks-in-hello-azure-portal"></a><span data-ttu-id="6c882-170">Controllare l'attività di rilascio nel portale di Azure hello e preparazione del processo</span><span class="sxs-lookup"><span data-stu-id="6c882-170">Inspect job preparation and release tasks in hello Azure portal</span></span>
<span data-ttu-id="6c882-171">Quando si esegue l'applicazione di esempio hello, è possibile utilizzare hello [portale di Azure] [ portal] tooview hello proprietà del processo di hello e le relative attività, o anche scaricare i file di testo condivisa hello modificata dall'attività del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="6c882-171">When you run hello sample application, you can use hello [Azure portal][portal] tooview hello properties of hello job and its tasks, or even download hello shared text file that is modified by hello job's tasks.</span></span>

<span data-ttu-id="6c882-172">schermata di Hello riportata di seguito viene illustrato hello **Pannello attività di preparazione** nel portale di Azure dopo l'esecuzione dell'applicazione di esempio hello hello.</span><span class="sxs-lookup"><span data-stu-id="6c882-172">hello screenshot below shows hello **Preparation tasks blade** in hello Azure portal after a run of hello sample application.</span></span> <span data-ttu-id="6c882-173">Passare toohello *JobPrepReleaseSampleJob* proprietà dopo aver completato le attività, ma prima di eliminare il processo e il pool, fare clic su **attività di preparazione** o **leattivitàdirilascio** tooview le relative proprietà.</span><span class="sxs-lookup"><span data-stu-id="6c882-173">Navigate toohello *JobPrepReleaseSampleJob* properties after your tasks have completed (but before deleting your job and pool) and click **Preparation tasks** or **Release tasks** tooview their properties.</span></span>

![Proprietà di preparazione del processo nel portale di Azure][1]

## <a name="next-steps"></a><span data-ttu-id="6c882-175">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6c882-175">Next steps</span></span>
### <a name="application-packages"></a><span data-ttu-id="6c882-176">Pacchetti dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="6c882-176">Application packages</span></span>
<span data-ttu-id="6c882-177">Nell'attività di preparazione processo toohello aggiunta, è inoltre possibile utilizzare hello [pacchetti di applicazioni](batch-application-packages.md) funzionalità di Batch tooprepare nodi per l'esecuzione dell'attività di calcolo.</span><span class="sxs-lookup"><span data-stu-id="6c882-177">In addition toohello job preparation task, you can also use hello [application packages](batch-application-packages.md) feature of Batch tooprepare compute nodes for task execution.</span></span> <span data-ttu-id="6c882-178">Questa funzionalità è particolarmente utile per la distribuzione di applicazioni che non richiedono l'esecuzione di un programma di installazione, applicazioni che contengono molti file (100+) o applicazioni che richiedono un controllo delle versioni rigoroso.</span><span class="sxs-lookup"><span data-stu-id="6c882-178">This feature is especially useful for deploying applications that do not require running an installer, applications that contain many (100+) files, or applications that require strict version control.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="6c882-179">Installazione delle applicazioni e staging dei dati</span><span class="sxs-lookup"><span data-stu-id="6c882-179">Installing applications and staging data</span></span>
<span data-ttu-id="6c882-180">Questo post del forum MSDN offre una panoramica di diversi metodi di preparazione dei nodi per l'esecuzione di attività:</span><span class="sxs-lookup"><span data-stu-id="6c882-180">This MSDN forum post provides an overview of several methods of preparing your nodes for running tasks:</span></span>

<span data-ttu-id="6c882-181">[Installing applications and staging data on Batch compute nodes][forum_post] (Installazione delle applicazioni e staging dei dati nei nodi di calcolo di Batch)</span><span class="sxs-lookup"><span data-stu-id="6c882-181">[Installing applications and staging data on Batch compute nodes][forum_post]</span></span>

<span data-ttu-id="6c882-182">Scritti da uno dei membri del team di Azure Batch hello, vengono illustrate diverse tecniche che è possibile utilizzare i nodi di toocompute toodeploy applicazioni e dati.</span><span class="sxs-lookup"><span data-stu-id="6c882-182">Written by one of hello Azure Batch team members, it discusses several techniques that you can use toodeploy applications and data toocompute nodes.</span></span>

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_listjobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[azure_storage]: https://azure.microsoft.com/services/storage/
[portal]: https://portal.azure.com
[job_prep_release_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/JobPrepRelease
[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[net_batch_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]:https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_job_prep]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.aspx
[net_job_prep_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobpreparationtask.aspx
[net_job_prep_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.resourcefiles.aspx
[net_job_delete]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.deletejobasync.aspx
[net_job_terminate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.terminatejobasync.aspx
[net_job_release]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobreleasetask.aspx
[net_job_release_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobreleasetask.aspx
[pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx

[net_list_certs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificateoperations.listcertificates.aspx
[net_list_compute_nodes]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listcomputenodes.aspx
[net_list_job_schedules]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobschedules.aspx
[net_list_jobprep_status]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobpreparationandreleasetaskstatus.aspx
[net_list_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[net_list_nodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listnodefiles.aspx
[net_list_pools]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listpools.aspx
[net_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobs.aspx
[net_list_task_files]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[net_list_tasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listtasks.aspx

[1]: ./media/batch-job-prep-release/portal-jobprep-01.png
