---
title: "Creare attività per preparare e completare i processi nei nodi di calcolo - Azure Batch | Documentazione Microsoft"
description: "Usare le attività di preparazione a livello di processo per ridurre al minimo il trasferimento dei dati ai nodi di calcolo di Azure Batch e le attività di rilascio per la pulizia del nodo al completamento del processo."
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
ms.openlocfilehash: 6a2525c02ce7bd3969469d2e28a5fccc948f89b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="run-job-preparation-and-job-release-tasks-on-batch-compute-nodes"></a><span data-ttu-id="612f0-103">Eseguire attività di preparazione e rilascio del processo in nodi di calcolo di Batch</span><span class="sxs-lookup"><span data-stu-id="612f0-103">Run job preparation and job release tasks on Batch compute nodes</span></span>

 <span data-ttu-id="612f0-104">Un processo di Azure Batch richiede spesso alcune operazioni di configurazione prima dell'esecuzione delle attività e di manutenzione post-processo dopo il completamento delle attività.</span><span class="sxs-lookup"><span data-stu-id="612f0-104">An Azure Batch job often requires some form of setup before its tasks are executed, and post-job maintenance when its tasks are completed.</span></span> <span data-ttu-id="612f0-105">Potrebbe essere necessario scaricare i dati di input delle attività comuni nei nodi di calcolo o caricare i dati di output delle attività in Archiviazione di Azure al termine del processo.</span><span class="sxs-lookup"><span data-stu-id="612f0-105">You might need to download common task input data to your compute nodes, or upload task output data to Azure Storage after the job completes.</span></span> <span data-ttu-id="612f0-106">Per eseguire queste operazioni, è possibile usare le attività di **preparazione del processo** e di **rilascio del processo**.</span><span class="sxs-lookup"><span data-stu-id="612f0-106">You can use **job preparation** and **job release** tasks to perform these operations.</span></span>

## <a name="what-are-job-preparation-and-release-tasks"></a><span data-ttu-id="612f0-107">Quali sono le attività di preparazione e rilascio dei processi</span><span class="sxs-lookup"><span data-stu-id="612f0-107">What are job preparation and release tasks?</span></span>
<span data-ttu-id="612f0-108">Prima dell'esecuzione delle attività di un processo, viene eseguita l'attività di preparazione del processo su tutti i nodi di calcolo pianificati per l'esecuzione di almeno un'attività.</span><span class="sxs-lookup"><span data-stu-id="612f0-108">Before a job's tasks run, the job preparation task runs on all compute nodes scheduled to run at least one task.</span></span> <span data-ttu-id="612f0-109">Dopo aver completato il processo, viene eseguita l'attività di rilascio del processo in ogni nodo del pool che ha eseguito almeno un'attività.</span><span class="sxs-lookup"><span data-stu-id="612f0-109">Once the job is completed, the job release task runs on each node in the pool that executed at least one task.</span></span> <span data-ttu-id="612f0-110">Come con le normali attività di Batch, è possibile specificare una riga di comando da richiamare quando viene eseguita un'attività di preparazione o rilascio del processo.</span><span class="sxs-lookup"><span data-stu-id="612f0-110">As with normal Batch tasks, you can specify a command line to be invoked when a job preparation or release task is run.</span></span>

<span data-ttu-id="612f0-111">Le attività di preparazione e rilascio del processo offrono funzionalità familiari per le attività di Batch, quali download di file ([file di risorse][net_job_prep_resourcefiles]), esecuzione con privilegi elevati, variabili di ambiente personalizzate, durata massima di esecuzione, numero di tentativi e periodo di conservazione dei file.</span><span class="sxs-lookup"><span data-stu-id="612f0-111">Job preparation and release tasks offer familiar Batch task features such as file download ([resource files][net_job_prep_resourcefiles]), elevated execution, custom environment variables, maximum execution duration, retry count, and file retention time.</span></span>

<span data-ttu-id="612f0-112">Nelle sezioni seguenti viene descritto come usare le classi [JobPreparationTask][net_job_prep] e [JobReleaseTask][net_job_release] disponibili nella libreria [Batch .NET][api_net].</span><span class="sxs-lookup"><span data-stu-id="612f0-112">In the following sections, you'll learn how to use the [JobPreparationTask][net_job_prep] and [JobReleaseTask][net_job_release] classes found in the [Batch .NET][api_net] library.</span></span>

> [!TIP]
> <span data-ttu-id="612f0-113">Le attività di preparazione e rilascio del processo sono particolarmente utili in ambienti con "pool condivisi", in cui un pool di nodi di calcolo viene mantenuto durante l'esecuzione di un processo e viene usato da più processi.</span><span class="sxs-lookup"><span data-stu-id="612f0-113">Job preparation and release tasks are especially helpful in "shared pool" environments, in which a pool of compute nodes persists between job runs and is used by many jobs.</span></span>
> 
> 

## <a name="when-to-use-job-preparation-and-release-tasks"></a><span data-ttu-id="612f0-114">Quando usare le attività di preparazione e rilascio dei processi</span><span class="sxs-lookup"><span data-stu-id="612f0-114">When to use job preparation and release tasks</span></span>
<span data-ttu-id="612f0-115">Le attività di preparazione del processo e di rilascio del processo sono ideali per le situazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="612f0-115">Job preparation and job release tasks are a good fit for the following situations:</span></span>

<span data-ttu-id="612f0-116">**Download dei dati delle attività comuni**</span><span class="sxs-lookup"><span data-stu-id="612f0-116">**Download common task data**</span></span>

<span data-ttu-id="612f0-117">I processi di Batch spesso richiedono un set comune di dati come input per le attività del processo.</span><span class="sxs-lookup"><span data-stu-id="612f0-117">Batch jobs often require a common set of data as input for the job's tasks.</span></span> <span data-ttu-id="612f0-118">Ad esempio, nei calcoli di analisi dei rischi giornalieri, i dati di mercato sono specifici del processo, ma comuni a tutte le attività del processo.</span><span class="sxs-lookup"><span data-stu-id="612f0-118">For example, in daily risk analysis calculations, market data is job-specific, yet common to all tasks in the job.</span></span> <span data-ttu-id="612f0-119">Tali dati di mercato, spesso di grandi dimensioni, devono essere scaricati una sola volta da ogni nodo di calcolo in modo che qualsiasi attività eseguita sul nodo possa usarli.</span><span class="sxs-lookup"><span data-stu-id="612f0-119">This market data, often several gigabytes in size, should be downloaded to each compute node only once so that any task that runs on the node can use it.</span></span> <span data-ttu-id="612f0-120">Usare un' **attività di preparazione del processo** per scaricare questi dati in ogni nodo prima dell'esecuzione di altre attività del processo.</span><span class="sxs-lookup"><span data-stu-id="612f0-120">Use a **job preparation task** to download this data to each node before the execution of the job's other tasks.</span></span>

<span data-ttu-id="612f0-121">**Eliminazione dell'output di processi e attività**</span><span class="sxs-lookup"><span data-stu-id="612f0-121">**Delete job and task output**</span></span>

<span data-ttu-id="612f0-122">In un ambiente con "pool condivisi", in cui i nodi di calcolo di un pool non sono autorizzati tra i processi, potrebbe essere necessario eliminare i dati dei processi tra un'esecuzione e l'altra.</span><span class="sxs-lookup"><span data-stu-id="612f0-122">In a "shared pool" environment, where a pool's compute nodes are not decommissioned between jobs, you may need to delete job data between runs.</span></span> <span data-ttu-id="612f0-123">Potrebbe essere necessario conservare lo spazio su disco nei nodi o rispettare i criteri di sicurezza dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="612f0-123">You might need to conserve disk space on the nodes, or satisfy your organization's security policies.</span></span> <span data-ttu-id="612f0-124">Usare un' **attività di rilascio del processo** per eliminare i dati scaricati da un'attività di preparazione del processo o generati durante l'esecuzione dell'attività.</span><span class="sxs-lookup"><span data-stu-id="612f0-124">Use a **job release task** to delete data that was downloaded by a job preparation task, or generated during task execution.</span></span>

<span data-ttu-id="612f0-125">**Conservazione dei log**</span><span class="sxs-lookup"><span data-stu-id="612f0-125">**Log retention**</span></span>

<span data-ttu-id="612f0-126">È possibile conservare una copia dei file di log generati dalle attività o dei file dump di arresto anomalo generati da errori nelle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="612f0-126">You might want to keep a copy of log files that your tasks generate, or perhaps crash dump files that can be generated by failed applications.</span></span> <span data-ttu-id="612f0-127">In questi casi, usare un'**attività di rilascio del processo** per comprimere e caricare dati in un account di [Archiviazione di Azure][azure_storage].</span><span class="sxs-lookup"><span data-stu-id="612f0-127">Use a **job release task** in such cases to compress and upload this data to an [Azure Storage][azure_storage] account.</span></span>

> [!TIP]
> <span data-ttu-id="612f0-128">Per rendere persistenti i log e gli altri dati di output del processo e delle attività, è anche possibile usare la libreria [Azure Batch File Conventions](batch-task-output.md) .</span><span class="sxs-lookup"><span data-stu-id="612f0-128">Another way to persist logs and other job and task output data is to use the [Azure Batch File Conventions](batch-task-output.md) library.</span></span>
> 
> 

## <a name="job-preparation-task"></a><span data-ttu-id="612f0-129">attività di preparazione del processo</span><span class="sxs-lookup"><span data-stu-id="612f0-129">Job preparation task</span></span>
<span data-ttu-id="612f0-130">Prima dell'esecuzione delle attività di un processo, Batch esegue l'attività di preparazione del processo su ogni nodo di calcolo pianificato per l'esecuzione di un'attività.</span><span class="sxs-lookup"><span data-stu-id="612f0-130">Before execution of a job's tasks, Batch executes the job preparation task on each compute node that is scheduled to run a task.</span></span> <span data-ttu-id="612f0-131">Per impostazione predefinita, il servizio Batch attende il completamento dell'attività di preparazione del processo prima di eseguire le attività pianificate per l'esecuzione nel nodo,</span><span class="sxs-lookup"><span data-stu-id="612f0-131">By default, the Batch service waits for the job preparation task to be completed before running the tasks scheduled to execute on the node.</span></span> <span data-ttu-id="612f0-132">ma è possibile configurare il servizio affinché venga annullata la fase di attesa.</span><span class="sxs-lookup"><span data-stu-id="612f0-132">However, you can configure the service not to wait.</span></span> <span data-ttu-id="612f0-133">Se il nodo viene riavviato, l'attività di preparazione del processo viene eseguita nuovamente, ma è anche possibile disabilitare questo comportamento.</span><span class="sxs-lookup"><span data-stu-id="612f0-133">If the node restarts, the job preparation task runs again, but you can also disable this behavior.</span></span>

<span data-ttu-id="612f0-134">L'attività di preparazione del processo viene eseguita solo su nodi pianificati per l'esecuzione di un'attività.</span><span class="sxs-lookup"><span data-stu-id="612f0-134">The job preparation task is executed only on nodes that are scheduled to run a task.</span></span> <span data-ttu-id="612f0-135">Ciò impedisce l'esecuzione di un'attività di preparazione non necessaria nel caso in cui a un nodo non venga assegnata un'attività.</span><span class="sxs-lookup"><span data-stu-id="612f0-135">This prevents the unnecessary execution of a preparation task in case a node is not assigned a task.</span></span> <span data-ttu-id="612f0-136">Questa situazione può verificarsi quando il numero di attività per un processo è inferiore al numero di nodi in un pool</span><span class="sxs-lookup"><span data-stu-id="612f0-136">This can occur when the number of tasks for a job is less than the number of nodes in a pool.</span></span> <span data-ttu-id="612f0-137">o quando è abilitata l'[esecuzione di attività simultanee](batch-parallel-node-tasks.md). In quest'ultimo caso, alcuni nodi rimangono inattivi se il numero delle attività è inferiore a quello totale delle attività simultanee possibili.</span><span class="sxs-lookup"><span data-stu-id="612f0-137">It also applies when [concurrent task execution](batch-parallel-node-tasks.md) is enabled, which leaves some nodes idle if the task count is lower than the total possible concurrent tasks.</span></span> <span data-ttu-id="612f0-138">Se non si esegue l'attività di preparazione dei processi sui inattivi nodi, è possibile risparmiare sui costi di trasferimento dati.</span><span class="sxs-lookup"><span data-stu-id="612f0-138">By not running the job preparation task on idle nodes, you can spend less money on data transfer charges.</span></span>

> [!NOTE]
> <span data-ttu-id="612f0-139">[JobPreparationTask][net_job_prep_cloudjob] differisce dalla proprietà [CloudPool.StartTask][pool_starttask] perché JobPreparationTask viene eseguita all'avvio di ogni processo, mentre StartTask viene eseguita solo quando un nodo di calcolo viene aggiunto per la prima volta a un pool o viene riavviato.</span><span class="sxs-lookup"><span data-stu-id="612f0-139">[JobPreparationTask][net_job_prep_cloudjob] differs from [CloudPool.StartTask][pool_starttask] in that JobPreparationTask executes at the start of each job, whereas StartTask executes only when a compute node first joins a pool or restarts.</span></span>
> 
> 

## <a name="job-release-task"></a><span data-ttu-id="612f0-140">attività di rilascio del processo</span><span class="sxs-lookup"><span data-stu-id="612f0-140">Job release task</span></span>
<span data-ttu-id="612f0-141">Dopo aver contrassegnato un processo come completato , viene eseguita l'attività di rilascio del processo in ogni nodo del pool che ha eseguito almeno un'attività.</span><span class="sxs-lookup"><span data-stu-id="612f0-141">Once a job is marked as completed, the job release task is executed on each node in the pool that executed at least one task.</span></span> <span data-ttu-id="612f0-142">Un processo viene contrassegnato come completato generando una richiesta di interruzione.</span><span class="sxs-lookup"><span data-stu-id="612f0-142">You mark a job as completed by issuing a terminate request.</span></span> <span data-ttu-id="612f0-143">Il servizio Batch imposta quindi lo stato del processo su *Arresto in corso*, termina le attività attive o in esecuzione associate al processo ed esegue l'attività di rilascio del processo.</span><span class="sxs-lookup"><span data-stu-id="612f0-143">The Batch service then sets the job state to *terminating*, terminates any active or running tasks associated with the job, and runs the job release task.</span></span> <span data-ttu-id="612f0-144">Il processo passa quindi allo stato *completato* .</span><span class="sxs-lookup"><span data-stu-id="612f0-144">The job then moves to the *completed* state.</span></span>

> [!NOTE]
> <span data-ttu-id="612f0-145">Anche l'eliminazione del processo esegue l'attività di rilascio del processo.</span><span class="sxs-lookup"><span data-stu-id="612f0-145">Job deletion also executes the job release task.</span></span> <span data-ttu-id="612f0-146">Tuttavia, se un processo è già stato terminato, l'attività di rilascio non viene eseguita una seconda volta se il processo viene eliminato in seguito.</span><span class="sxs-lookup"><span data-stu-id="612f0-146">However, if a job has already been terminated, the release task is not run a second time if the job is later deleted.</span></span>
> 
> 

## <a name="job-prep-and-release-tasks-with-batch-net"></a><span data-ttu-id="612f0-147">Attività di preparazione e di rilascio del processo con Batch .NET</span><span class="sxs-lookup"><span data-stu-id="612f0-147">Job prep and release tasks with Batch .NET</span></span>
<span data-ttu-id="612f0-148">Per usare un'attività di preparazione del processo, assegnare un oggetto [JobPreparationTask][net_job_prep] alla proprietà [CloudJob.JobPreparationTask][net_job_prep_cloudjob] del processo.</span><span class="sxs-lookup"><span data-stu-id="612f0-148">To use a job preparation task, assign a [JobPreparationTask][net_job_prep] object to your job's [CloudJob.JobPreparationTask][net_job_prep_cloudjob] property.</span></span> <span data-ttu-id="612f0-149">In modo analogo, inizializzare una classe [JobReleaseTask][net_job_release] e assegnarla alla proprietà [CloudJob.JobReleaseTask][net_job_prep_cloudjob] del processo per impostare l'attività di rilascio del processo.</span><span class="sxs-lookup"><span data-stu-id="612f0-149">Similarly, initialize a [JobReleaseTask][net_job_release] and assign it to your job's [CloudJob.JobReleaseTask][net_job_prep_cloudjob] property to set the job's release task.</span></span>

<span data-ttu-id="612f0-150">In questo frammento di codice `myBatchClient` è un'istanza di [BatchClient][net_batch_client] e `myPool` è un pool esistente nell'account Batch.</span><span class="sxs-lookup"><span data-stu-id="612f0-150">In this code snippet, `myBatchClient` is an instance of [BatchClient][net_batch_client], and `myPool` is an existing pool within the Batch account.</span></span>

```csharp
// Create the CloudJob for CloudPool "myPool"
CloudJob myJob =
    myBatchClient.JobOperations.CreateJob(
        "JobPrepReleaseSampleJob",
        new PoolInformation() { PoolId = "myPool" });

// Specify the command lines for the job preparation and release tasks
string jobPrepCmdLine =
    "cmd /c echo %AZ_BATCH_NODE_ID% > %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";
string jobReleaseCmdLine =
    "cmd /c del %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";

// Assign the job preparation task to the job
myJob.JobPreparationTask =
    new JobPreparationTask { CommandLine = jobPrepCmdLine };

// Assign the job release task to the job
myJob.JobReleaseTask =
    new JobPreparationTask { CommandLine = jobReleaseCmdLine };

await myJob.CommitAsync();
```

<span data-ttu-id="612f0-151">Come indicato prima, l'attività di rilascio viene eseguita quando un processo viene concluso o eliminato.</span><span class="sxs-lookup"><span data-stu-id="612f0-151">As mentioned earlier, the release task is executed when a job is terminated or deleted.</span></span> <span data-ttu-id="612f0-152">Terminare un processo con [JobOperations.TerminateJobAsync][net_job_terminate].</span><span class="sxs-lookup"><span data-stu-id="612f0-152">Terminate a job with [JobOperations.TerminateJobAsync][net_job_terminate].</span></span> <span data-ttu-id="612f0-153">Eliminare un processo con [JobOperations.DeleteJobAsync][net_job_delete].</span><span class="sxs-lookup"><span data-stu-id="612f0-153">Delete a job with [JobOperations.DeleteJobAsync][net_job_delete].</span></span> <span data-ttu-id="612f0-154">In genere si termina o si elimina un processo quando le attività vengono completate o quando si raggiunge un timeout definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="612f0-154">You typically terminate or delete a job when its tasks are completed, or when a timeout that you've defined has been reached.</span></span>

```csharp
// Terminate the job to mark it as Completed; this will initiate the
// Job Release Task on any node that executed job tasks. Note that the
// Job Release Task is also executed when a job is deleted, thus you
// need not call Terminate if you typically delete jobs after task completion.
await myBatchClient.JobOperations.TerminateJobAsy("JobPrepReleaseSampleJob");
```

## <a name="code-sample-on-github"></a><span data-ttu-id="612f0-155">Esempio di codice in GitHub</span><span class="sxs-lookup"><span data-stu-id="612f0-155">Code sample on GitHub</span></span>
<span data-ttu-id="612f0-156">Per vedere il funzionamento delle attività di preparazione e rilascio dei processi, esaminare il progetto di esempio [JobPrepRelease][job_prep_release_sample] in GitHub.</span><span class="sxs-lookup"><span data-stu-id="612f0-156">To see job preparation and release tasks in action, check out the [JobPrepRelease][job_prep_release_sample] sample project on GitHub.</span></span> <span data-ttu-id="612f0-157">Questa applicazione console esegue le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="612f0-157">This console application does the following:</span></span>

1. <span data-ttu-id="612f0-158">Crea un pool con due nodi "small".</span><span class="sxs-lookup"><span data-stu-id="612f0-158">Creates a pool with two "small" nodes.</span></span>
2. <span data-ttu-id="612f0-159">Crea un processo con attività di preparazione e rilascio di processi e attività standard.</span><span class="sxs-lookup"><span data-stu-id="612f0-159">Creates a job with job preparation, release, and standard tasks.</span></span>
3. <span data-ttu-id="612f0-160">Esegue un'attività di preparazione del processo che scrive innanzitutto l'ID del nodo in un file di testo in una directory "condivisa" del nodo.</span><span class="sxs-lookup"><span data-stu-id="612f0-160">Runs the job preparation task, which first writes the node ID to a text file in a node's "shared" directory.</span></span>
4. <span data-ttu-id="612f0-161">Esegue un'attività in ogni nodo che scrive il relativo ID attività nello stesso file di testo.</span><span class="sxs-lookup"><span data-stu-id="612f0-161">Runs a task on each node that writes its task ID to the same text file.</span></span>
5. <span data-ttu-id="612f0-162">Dopo aver completato tutte le attività (o aver raggiunto il timeout), stampa i contenuti del file di testo di ogni nodo nella console.</span><span class="sxs-lookup"><span data-stu-id="612f0-162">Once all tasks are completed (or the timeout is reached), prints the contents of each node's text file to the console.</span></span>
6. <span data-ttu-id="612f0-163">Dopo aver completato il processo, esegue l'attività di rilascio del processo per eliminare il file dal nodo.</span><span class="sxs-lookup"><span data-stu-id="612f0-163">When the job is completed, runs the job release task to delete the file from the node.</span></span>
7. <span data-ttu-id="612f0-164">Stampa i codici di uscita delle attività di preparazione e rilascio dei processi per ogni nodo in cui vengono eseguiti.</span><span class="sxs-lookup"><span data-stu-id="612f0-164">Prints the exit codes of the job preparation and release tasks for each node on which they executed.</span></span>
8. <span data-ttu-id="612f0-165">Sospende l'esecuzione per consentire la conferma dell'eliminazione dei processi e/o del pool.</span><span class="sxs-lookup"><span data-stu-id="612f0-165">Pauses execution to allow confirmation of job and/or pool deletion.</span></span>

<span data-ttu-id="612f0-166">L'output dell'applicazione di esempio è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="612f0-166">Output from the sample application is similar to the following:</span></span>

```
Attempting to create pool: JobPrepReleaseSamplePool
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

Waiting for job JobPrepReleaseSampleJob to reach state Completed
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

Sample complete, hit ENTER to exit...
```

> [!NOTE]
> <span data-ttu-id="612f0-167">A causa degli orari variabili di creazione e di inizio per i nodi in un nuovo pool, poiché alcuni nodi sono pronti per le attività prima di altri, è possibile che l'output visualizzato sia diverso.</span><span class="sxs-lookup"><span data-stu-id="612f0-167">Due to the variable creation and start time of nodes in a new pool (some nodes are ready for tasks before others), you may see different output.</span></span> <span data-ttu-id="612f0-168">Poiché le attività vengono completate rapidamente, in particolare, è possibile che uno dei nodi del pool esegua tutte le attività del processo.</span><span class="sxs-lookup"><span data-stu-id="612f0-168">Specifically, because the tasks complete quickly, one of the pool's nodes may execute all of the job's tasks.</span></span> <span data-ttu-id="612f0-169">In questo caso, si potrà notare che le attività di preparazione e di rilascio dei processi non esistono per il nodo che non ha eseguito alcuna attività.</span><span class="sxs-lookup"><span data-stu-id="612f0-169">If this occurs, you will notice that the job prep and release tasks do not exist for the node that executed no tasks.</span></span>
> 
> 

### <a name="inspect-job-preparation-and-release-tasks-in-the-azure-portal"></a><span data-ttu-id="612f0-170">Controllare le attività di preparazione e rilascio del processo nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="612f0-170">Inspect job preparation and release tasks in the Azure portal</span></span>
<span data-ttu-id="612f0-171">Quando si esegue l'applicazione di esempio, è possibile usare il [portale di Azure][portal] per visualizzare le proprietà del processo e le rispettive attività oppure per scaricare il file di testo condiviso modificato dalle attività del processo.</span><span class="sxs-lookup"><span data-stu-id="612f0-171">When you run the sample application, you can use the [Azure portal][portal] to view the properties of the job and its tasks, or even download the shared text file that is modified by the job's tasks.</span></span>

<span data-ttu-id="612f0-172">Lo screenshot seguente mostra il pannello **Attività di preparazione** nel portale di Azure dopo un'esecuzione dell'applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="612f0-172">The screenshot below shows the **Preparation tasks blade** in the Azure portal after a run of the sample application.</span></span> <span data-ttu-id="612f0-173">Passare alle proprietà *JobPrepReleaseSampleJob* dopo il completamento delle attività, ma prima dell'eliminazione del processo e del pool, quindi fare clic su **Attività di preparazione** o **Attività di rilascio** per visualizzare le rispettive proprietà.</span><span class="sxs-lookup"><span data-stu-id="612f0-173">Navigate to the *JobPrepReleaseSampleJob* properties after your tasks have completed (but before deleting your job and pool) and click **Preparation tasks** or **Release tasks** to view their properties.</span></span>

![Proprietà di preparazione del processo nel portale di Azure][1]

## <a name="next-steps"></a><span data-ttu-id="612f0-175">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="612f0-175">Next steps</span></span>
### <a name="application-packages"></a><span data-ttu-id="612f0-176">Pacchetti dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="612f0-176">Application packages</span></span>
<span data-ttu-id="612f0-177">Oltre all'attività di preparazione del processo, è possibile usare anche la funzionalità [Pacchetti dell'applicazione](batch-application-packages.md) di Batch per preparare i nodi di calcolo per l'esecuzione dell'attività.</span><span class="sxs-lookup"><span data-stu-id="612f0-177">In addition to the job preparation task, you can also use the [application packages](batch-application-packages.md) feature of Batch to prepare compute nodes for task execution.</span></span> <span data-ttu-id="612f0-178">Questa funzionalità è particolarmente utile per la distribuzione di applicazioni che non richiedono l'esecuzione di un programma di installazione, applicazioni che contengono molti file (100+) o applicazioni che richiedono un controllo delle versioni rigoroso.</span><span class="sxs-lookup"><span data-stu-id="612f0-178">This feature is especially useful for deploying applications that do not require running an installer, applications that contain many (100+) files, or applications that require strict version control.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="612f0-179">Installazione delle applicazioni e staging dei dati</span><span class="sxs-lookup"><span data-stu-id="612f0-179">Installing applications and staging data</span></span>
<span data-ttu-id="612f0-180">Questo post del forum MSDN offre una panoramica di diversi metodi di preparazione dei nodi per l'esecuzione di attività:</span><span class="sxs-lookup"><span data-stu-id="612f0-180">This MSDN forum post provides an overview of several methods of preparing your nodes for running tasks:</span></span>

<span data-ttu-id="612f0-181">[Installing applications and staging data on Batch compute nodes][forum_post] (Installazione delle applicazioni e staging dei dati nei nodi di calcolo di Batch)</span><span class="sxs-lookup"><span data-stu-id="612f0-181">[Installing applications and staging data on Batch compute nodes][forum_post]</span></span>

<span data-ttu-id="612f0-182">L'autore, uno dei membri del team di Azure Batch, illustra diverse tecniche che è possibile usare per distribuire applicazioni e dati nei nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="612f0-182">Written by one of the Azure Batch team members, it discusses several techniques that you can use to deploy applications and data to compute nodes.</span></span>

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
