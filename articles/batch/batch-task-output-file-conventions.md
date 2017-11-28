---
title: aaaPersist job e task tooAzure archiviazione con libreria di hello convenzioni dei File di output per .NET - Azure Batch | Documenti Microsoft
description: "Informazioni su come toouse convenzioni File Batch di Azure library per .NET toopersist attività Batch e processo output tooAzure archiviazione e hello visualizzazione persistente output di hello portale di Azure."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 16e12d0e-958c-46c2-a6b8-7843835d830e
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cf2ac8632a13d32438c1bdcf11b4b9649de1e2b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="persist-job-and-task-data-tooazure-storage-with-hello-batch-file-conventions-library-for-net-toopersist"></a><span data-ttu-id="17954-103">Processo di persistenza e dati tooAzure archiviazione con libreria di hello convenzioni dei File Batch per .NET toopersist di attività</span><span class="sxs-lookup"><span data-stu-id="17954-103">Persist job and task data tooAzure Storage with hello Batch File Conventions library for .NET toopersist</span></span> 

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

<span data-ttu-id="17954-104">Dati dell'attività toopersist unidirezionale sono hello toouse [libreria convenzioni File Batch di Azure per .NET][nuget_package].</span><span class="sxs-lookup"><span data-stu-id="17954-104">One way toopersist task data is toouse hello [Azure Batch File Conventions library for .NET][nuget_package].</span></span> <span data-ttu-id="17954-105">libreria convenzioni File Hello semplifica il processo di hello di output dell'attività di archiviazione dati tooAzure, archiviazione e del suo recupero.</span><span class="sxs-lookup"><span data-stu-id="17954-105">hello File Conventions library simplifies hello process of storing task output data tooAzure Storage and retrieving it.</span></span> <span data-ttu-id="17954-106">È possibile utilizzare hello convenzioni File libreria nel codice di attività sia client &mdash; nel codice dell'attività per salvare in modo permanente i file e nel client toolist del codice e recuperarli.</span><span class="sxs-lookup"><span data-stu-id="17954-106">You can use hello File Conventions library in both task and client code &mdash; in task code for persisting files, and in client code toolist and retrieve them.</span></span> <span data-ttu-id="17954-107">Il codice di attività può usare anche output di hello libreria tooretrieve hello di attività upstream, ad esempio un [le relazioni tra attività](batch-task-dependencies.md) scenario.</span><span class="sxs-lookup"><span data-stu-id="17954-107">Your task code can also use hello library tooretrieve hello output of upstream tasks, such as in a [task dependencies](batch-task-dependencies.md) scenario.</span></span> 

<span data-ttu-id="17954-108">tooretrieve file alla libreria di hello convenzioni dei File di output, è possibile individuare il file hello per un determinato processo o un'attività elencandoli dall'ID e lo scopo.</span><span class="sxs-lookup"><span data-stu-id="17954-108">tooretrieve output files with hello File Conventions library, you can locate hello files for a given job or task by listing them by ID and purpose.</span></span> <span data-ttu-id="17954-109">Non è necessario tooknow hello nomi o percorsi di file hello.</span><span class="sxs-lookup"><span data-stu-id="17954-109">You don't need tooknow hello names or locations of hello files.</span></span> <span data-ttu-id="17954-110">Ad esempio, utilizzare toolist libreria di hello convenzioni dei File di tutti i file intermedi per una determinata attività oppure ottenere un file di anteprima per un determinato processo.</span><span class="sxs-lookup"><span data-stu-id="17954-110">For example, you can use hello File Conventions library toolist all intermediate files for a given task, or get a preview file for a given job.</span></span>

> [!TIP]
> <span data-ttu-id="17954-111">A partire dalla versione 2017-05-01, hello API del servizio Batch supporta persistenti output dati tooAzure archiviazione per le attività e le attività di gestione processo eseguite sul pool creati con la configurazione della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="17954-111">Starting with version 2017-05-01, hello Batch service API supports persisting output data tooAzure Storage for tasks and job manager tasks that run on pools created with hello virtual machine configuration.</span></span> <span data-ttu-id="17954-112">API del servizio Batch Hello fornisce toopersist un modo semplice l'output di codice che crea un'attività e funge da una libreria di convenzioni di File alternativo toohello hello.</span><span class="sxs-lookup"><span data-stu-id="17954-112">hello Batch service API provides a simple way toopersist output from within hello code that creates a task and serves as an alternative toohello File Conventions library.</span></span> <span data-ttu-id="17954-113">È possibile modificare l'output di toopersist Batch applicazioni client senza la necessità di un'applicazione hello tooupdate che l'attività è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="17954-113">You can modify your Batch client applications toopersist output without needing tooupdate hello application that your task is running.</span></span> <span data-ttu-id="17954-114">Per ulteriori informazioni, vedere [mantenere i dati di attività tooAzure archiviazione con l'API del servizio Batch hello](batch-task-output-files.md).</span><span class="sxs-lookup"><span data-stu-id="17954-114">For more information, see [Persist task data tooAzure Storage with hello Batch service API](batch-task-output-files.md).</span></span>
> 
> 

## <a name="when-do-i-use-hello-file-conventions-library-toopersist-task-output"></a><span data-ttu-id="17954-115">Utilizzo di output di hello convenzioni dei File della libreria toopersist attività</span><span class="sxs-lookup"><span data-stu-id="17954-115">When do I use hello File Conventions library toopersist task output?</span></span>

<span data-ttu-id="17954-116">Azure Batch offre più di un metodo toopersist l'output dell'attività.</span><span class="sxs-lookup"><span data-stu-id="17954-116">Azure Batch provides more than one way toopersist task output.</span></span> <span data-ttu-id="17954-117">Hello convenzioni dei File è migliori scenari toothese appropriato:</span><span class="sxs-lookup"><span data-stu-id="17954-117">hello File Conventions is best suited toothese scenarios:</span></span>

- <span data-ttu-id="17954-118">È possibile modificare facilmente codice hello per un'applicazione hello che l'attività è in esecuzione file toopersist utilizzando libreria convenzioni File hello.</span><span class="sxs-lookup"><span data-stu-id="17954-118">You can easily modify hello code for hello application that your task is running toopersist files using hello File Conventions library.</span></span>
- <span data-ttu-id="17954-119">Si desidera toostream dati tooAzure archiviazione mentre l'attività hello è ancora in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="17954-119">You want toostream data tooAzure Storage while hello task is still running.</span></span>
- <span data-ttu-id="17954-120">Si desidera toopersist dati dal pool creati con la configurazione di macchina virtuale hello o della configurazione del servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="17954-120">You want toopersist data from pools created with either hello cloud service configuration or hello virtual machine configuration.</span></span>
- <span data-ttu-id="17954-121">L'applicazione client o altre attività in hello processi toolocate esigenze e scaricare i file di output di attività per ID o in base allo scopo.</span><span class="sxs-lookup"><span data-stu-id="17954-121">Your client application or other tasks in hello job needs toolocate and download task output files by ID or by purpose.</span></span> 
- <span data-ttu-id="17954-122">Desideri che l'output dell'attività tooview in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="17954-122">You want tooview task output in hello Azure portal.</span></span>

<span data-ttu-id="17954-123">Se lo scenario è diverso da quelli elencati in precedenza, potrebbe essere tooconsider un approccio diverso.</span><span class="sxs-lookup"><span data-stu-id="17954-123">If your scenario differs from those listed above, you may need tooconsider a different approach.</span></span> <span data-ttu-id="17954-124">Per ulteriori informazioni sulle altre opzioni per salvare in modo permanente l'output dell'attività, vedere [Persist processi e delle attività di output tooAzure archiviazione](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="17954-124">For more information on other options for persisting task output, see [Persist job and task output tooAzure Storage](batch-task-output.md).</span></span> 

## <a name="what-is-hello-batch-file-conventions-standard"></a><span data-ttu-id="17954-125">Che cos'è hello convenzioni dei File Batch standard?</span><span class="sxs-lookup"><span data-stu-id="17954-125">What is hello Batch File Conventions standard?</span></span>

<span data-ttu-id="17954-126">Hello [standard convenzioni dei File Batch](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) fornisce uno schema di denominazione per i contenitori di destinazione hello e toowhich percorsi blob vengono scritti i file di output.</span><span class="sxs-lookup"><span data-stu-id="17954-126">hello [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) provides a naming scheme for hello destination containers and blob paths toowhich your output files are written.</span></span> <span data-ttu-id="17954-127">File persistente tooAzure archiviazione conformi toohello convenzioni dei File standard sono automaticamente disponibili per la visualizzazione in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="17954-127">Files persisted tooAzure Storage that adhere toohello File Conventions standard are automatically available for viewing in hello Azure portal.</span></span> <span data-ttu-id="17954-128">portale di Hello è a conoscenza di convenzione di denominazione hello e pertanto possa visualizzare i file che rispettano tooit.</span><span class="sxs-lookup"><span data-stu-id="17954-128">hello portal is aware of hello naming convention and so can display files that adhere tooit.</span></span>

<span data-ttu-id="17954-129">libreria di convenzioni per i File Hello per .NET denomina automaticamente i contenitori di archiviazione e i file di output di attività in base toohello convenzioni dei File standard.</span><span class="sxs-lookup"><span data-stu-id="17954-129">hello File Conventions library for .NET automatically names your storage containers and task output files according toohello File Conventions standard.</span></span> <span data-ttu-id="17954-130">libreria convenzioni File Hello fornisce anche metodi tooquery di file di output in archiviazione di Azure in base toojob ID, ID attività o scopo.</span><span class="sxs-lookup"><span data-stu-id="17954-130">hello File Conventions library also provides methods tooquery output files in Azure Storage according toojob ID, task ID, or purpose.</span></span>   

<span data-ttu-id="17954-131">Se si sviluppa con un linguaggio diverso da .NET, è possibile implementare manualmente il standard convenzioni File hello nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="17954-131">If you are developing with a language other than .NET, you can implement hello File Conventions standard yourself in your application.</span></span> <span data-ttu-id="17954-132">Per ulteriori informazioni, vedere [sullo standard di convenzioni per i File Batch hello](batch-task-output.md#about-the-batch-file-conventions-standard).</span><span class="sxs-lookup"><span data-stu-id="17954-132">For more information, see [About hello Batch File Conventions standard](batch-task-output.md#about-the-batch-file-conventions-standard).</span></span>

## <a name="link-an-azure-storage-account-tooyour-batch-account"></a><span data-ttu-id="17954-133">Collegare un tooyour di account di archiviazione di Azure account Batch</span><span class="sxs-lookup"><span data-stu-id="17954-133">Link an Azure Storage account tooyour Batch account</span></span>

<span data-ttu-id="17954-134">toopersist dati di output tooAzure archiviazione utilizzando hello convenzioni File libreria, è innanzitutto necessario collegare un tooyour di account di archiviazione di Azure account Batch.</span><span class="sxs-lookup"><span data-stu-id="17954-134">toopersist output data tooAzure Storage using hello File Conventions library, you must first link an Azure Storage account tooyour Batch account.</span></span> <span data-ttu-id="17954-135">Se non è già fatto, è possibile collegare un tooyour di account di archiviazione account Batch utilizzando hello [portale di Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="17954-135">If you haven't done so already, link a Storage account tooyour Batch account by using hello [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="17954-136">Passare l'account Batch tooyour in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="17954-136">Navigate tooyour Batch account in hello Azure portal.</span></span> 
2. <span data-ttu-id="17954-137">In **Impostazioni** selezionare **Account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="17954-137">Under **Settings**, select **Storage Account**.</span></span>
3. <span data-ttu-id="17954-138">Se non è già disponibile un account di archiviazione associato all'account Batch, fare clic su **Account di archiviazione (nessuno)**.</span><span class="sxs-lookup"><span data-stu-id="17954-138">If you do not already have a Storage account associated with your Batch account, click **Storage Account (None)**.</span></span>
4. <span data-ttu-id="17954-139">Selezionare un account di archiviazione dall'elenco di hello per la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="17954-139">Select a Storage account from hello list for your subscription.</span></span> <span data-ttu-id="17954-140">Per prestazioni ottimali, utilizzare un account di archiviazione di Azure in hello stessa area hello account Batch in cui si eseguono le attività.</span><span class="sxs-lookup"><span data-stu-id="17954-140">For best performance, use an Azure Storage account that is in hello same region as hello Batch account where your tasks are running.</span></span>

## <a name="persist-output-data"></a><span data-ttu-id="17954-141">Rendere persistenti i dati di output</span><span class="sxs-lookup"><span data-stu-id="17954-141">Persist output data</span></span>

<span data-ttu-id="17954-142">attività e processi toopersist dati con libreria di hello convenzioni dei File di output, creare un contenitore di archiviazione di Azure, quindi salvare contenitore toohello output di hello.</span><span class="sxs-lookup"><span data-stu-id="17954-142">toopersist job and task output data with hello File Conventions library, create a container in Azure Storage, then save hello output toohello container.</span></span> <span data-ttu-id="17954-143">Hello utilizzare [libreria client di archiviazione di Azure per .NET](https://www.nuget.org/packages/WindowsAzure.Storage) nel contenitore di attività codice tooupload hello attività output toohello.</span><span class="sxs-lookup"><span data-stu-id="17954-143">Use hello [Azure Storage client library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage) in your task code tooupload hello task output toohello container.</span></span> 

<span data-ttu-id="17954-144">Per altre informazioni sull'uso di contenitori e BLOB in Archiviazione di Azure, vedere [Introduzione all'archiviazione BLOB di Azure con .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="17954-144">For more information about working with containers and blobs in Azure Storage, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span>

> [!WARNING]
> <span data-ttu-id="17954-145">Tutti gli output di attività e processi persistenti con hello convenzioni relative ai File archiviati nella libreria hello stesso contenitore.</span><span class="sxs-lookup"><span data-stu-id="17954-145">All job and task outputs persisted with hello File Conventions library are stored in hello same container.</span></span> <span data-ttu-id="17954-146">Se un numero elevato di attività Cerca toopersist file hello stesso tempo, [archiviazione limitazioni](../storage/common/storage-performance-checklist.md#blobs) può essere applicata.</span><span class="sxs-lookup"><span data-stu-id="17954-146">If a large number of tasks try toopersist files at hello same time, [storage throttling limits](../storage/common/storage-performance-checklist.md#blobs) may be enforced.</span></span>
> 
> 

### <a name="create-storage-container"></a><span data-ttu-id="17954-147">Creare un contenitore di archiviazione</span><span class="sxs-lookup"><span data-stu-id="17954-147">Create storage container</span></span>

<span data-ttu-id="17954-148">toopersist attività output tooAzure archiviazione, prima di creare un contenitore chiamando [CloudJob][net_cloudjob].[ PrepareOutputStorageAsync][net_prepareoutputasync].</span><span class="sxs-lookup"><span data-stu-id="17954-148">toopersist task output tooAzure Storage, first create a container by calling [CloudJob][net_cloudjob].[PrepareOutputStorageAsync][net_prepareoutputasync].</span></span> <span data-ttu-id="17954-149">Questo metodo di estensione accetta un oggetto [CloudStorageAccount] [ net_cloudstorageaccount] come parametro.</span><span class="sxs-lookup"><span data-stu-id="17954-149">This extension method takes a [CloudStorageAccount][net_cloudstorageaccount] object as a parameter.</span></span> <span data-ttu-id="17954-150">Viene creato un contenitore denominato in base toohello File convenzioni standard, in modo che il suo contenuto possono essere individuato dagli hello Azure portal e hello i metodi di recupero descritti più avanti in articolo hello.</span><span class="sxs-lookup"><span data-stu-id="17954-150">It creates a container named according toohello File Conventions standard,so that its contents are discoverable by hello Azure portal and hello retrieval methods discussed later in hello article.</span></span>

<span data-ttu-id="17954-151">È in genere inserire toocreate codice hello un contenitore nell'applicazione client &mdash; hello applicazione che crea il pool di processi e attività.</span><span class="sxs-lookup"><span data-stu-id="17954-151">You typically place hello code toocreate a container in your client application &mdash; hello application that creates your pools, jobs, and tasks.</span></span>

```csharp
CloudJob job = batchClient.JobOperations.CreateJob(
    "myJob",
    new PoolInformation { PoolId = "myPool" });

// Create reference toohello linked Azure Storage account
CloudStorageAccount linkedStorageAccount =
    new CloudStorageAccount(myCredentials, true);

// Create hello blob storage container for hello outputs
await job.PrepareOutputStorageAsync(linkedStorageAccount);
```

### <a name="store-task-outputs"></a><span data-ttu-id="17954-152">Archiviare gli output delle attività</span><span class="sxs-lookup"><span data-stu-id="17954-152">Store task outputs</span></span>

<span data-ttu-id="17954-153">Ora che è stata preparata un contenitore di archiviazione di Azure, le attività è possono salvare toohello contenitore dell'output usando hello [TaskOutputStorage] [ net_taskoutputstorage] trovare la classe nella libreria convenzioni File hello.</span><span class="sxs-lookup"><span data-stu-id="17954-153">Now that you've prepared a container in Azure Storage, tasks can save output toohello container by using hello [TaskOutputStorage][net_taskoutputstorage] class found in hello File Conventions library.</span></span>

<span data-ttu-id="17954-154">Nel codice di attività, creare innanzitutto un [TaskOutputStorage] [ net_taskoutputstorage] dell'oggetto, quindi quando l'attività hello del completamento dell'operazione, chiamare hello [TaskOutputStorage] [ net_taskoutputstorage]. [SaveAsync] [ net_saveasync] toosave metodo relativo tooAzure output archiviazione.</span><span class="sxs-lookup"><span data-stu-id="17954-154">In your task code, first create a [TaskOutputStorage][net_taskoutputstorage] object, then when hello task has completed its work, call hello [TaskOutputStorage][net_taskoutputstorage].[SaveAsync][net_saveasync] method toosave its output tooAzure Storage.</span></span>

```csharp
CloudStorageAccount linkedStorageAccount = new CloudStorageAccount(myCredentials);
string jobId = Environment.GetEnvironmentVariable("AZ_BATCH_JOB_ID");
string taskId = Environment.GetEnvironmentVariable("AZ_BATCH_TASK_ID");

TaskOutputStorage taskOutputStorage = new TaskOutputStorage(
    linkedStorageAccount, jobId, taskId);

/* Code tooprocess data and produce output file(s) */

await taskOutputStorage.SaveAsync(TaskOutputKind.TaskOutput, "frame_full_res.jpg");
await taskOutputStorage.SaveAsync(TaskOutputKind.TaskPreview, "frame_low_res.jpg");
```

<span data-ttu-id="17954-155">Hello `kind` parametro di hello [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[ SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) metodo classifica hello file persistente.</span><span class="sxs-lookup"><span data-stu-id="17954-155">hello `kind` parameter of hello [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) method categorizes hello persisted files.</span></span> <span data-ttu-id="17954-156">Esistono quattro tipi [TaskOutputKind][net_taskoutputkind] predefiniti: `TaskOutput`, `TaskPreview`, `TaskLog` e `TaskIntermediate.` È anche possibile definire categorie personalizzate di output.</span><span class="sxs-lookup"><span data-stu-id="17954-156">There are four predefined [TaskOutputKind][net_taskoutputkind] types: `TaskOutput`, `TaskPreview`, `TaskLog`, and `TaskIntermediate.` You can also define custom categories of output.</span></span>

<span data-ttu-id="17954-157">Questi tipi di output consentono toospecify quale tipo di output toolist quando si eseguono query in un secondo momento Batch per hello persistenti gli output di un'attività specifica.</span><span class="sxs-lookup"><span data-stu-id="17954-157">These output types allow you toospecify which type of outputs toolist when you later query Batch for hello persisted outputs of a given task.</span></span> <span data-ttu-id="17954-158">In altre parole, quando si elencano gli output di hello per un'attività, è possibile filtrare l'elenco di hello in uno dei tipi di output di hello.</span><span class="sxs-lookup"><span data-stu-id="17954-158">In other words, when you list hello outputs for a task, you can filter hello list on one of hello output types.</span></span> <span data-ttu-id="17954-159">Ad esempio, "trarne vantaggio hello *anteprima* per attività di output *109*."</span><span class="sxs-lookup"><span data-stu-id="17954-159">For example, "Give me hello *preview* output for task *109*."</span></span> <span data-ttu-id="17954-160">Altre informazioni sulla visualizzazione e recupero di output viene visualizzato [recuperare l'output](#retrieve-output) successive dell'articolo hello.</span><span class="sxs-lookup"><span data-stu-id="17954-160">More on listing and retrieving outputs appears in [Retrieve output](#retrieve-output) later in hello article.</span></span>

> [!TIP]
> <span data-ttu-id="17954-161">Hello il tipo di output determina inoltre in hello Azure in cui viene visualizzato un determinato file portale: *TaskOutput*-suddiviso in categorie i file vengono visualizzati in **i file di output dell'attività**, e *TaskLog*i file vengono visualizzati in **attività registri**.</span><span class="sxs-lookup"><span data-stu-id="17954-161">hello output kind also determines where in hello Azure portal a particular file appears: *TaskOutput*-categorized files appear under **Task output files**, and *TaskLog* files appear under **Task logs**.</span></span>
> 
> 

### <a name="store-job-outputs"></a><span data-ttu-id="17954-162">Archiviare gli output del processo</span><span class="sxs-lookup"><span data-stu-id="17954-162">Store job outputs</span></span>

<span data-ttu-id="17954-163">Inoltre genera toostoring attività, è possibile archiviare gli output di hello associati a un intero processo.</span><span class="sxs-lookup"><span data-stu-id="17954-163">In addition toostoring task outputs, you can store hello outputs associated with an entire job.</span></span> <span data-ttu-id="17954-164">Nell'attività di unione hello di un processo di rendering del filmato, ad esempio, si potrebbe persistere film hello completamente il rendering come output un processo.</span><span class="sxs-lookup"><span data-stu-id="17954-164">For example, in hello merge task of a movie rendering job, you could persist hello fully rendered movie as a job output.</span></span> <span data-ttu-id="17954-165">Al termine dell'esecuzione del processo, l'applicazione client è possibile elencare e recuperare l'output di hello per processo hello e non necessario tooquery hello singole attività.</span><span class="sxs-lookup"><span data-stu-id="17954-165">When your job is completed, your client application can list and retrieve hello outputs for hello job, and does not need tooquery hello individual tasks.</span></span>

<span data-ttu-id="17954-166">Archiviare l'output del processo dalla chiamata hello [JobOutputStorage][net_joboutputstorage].[ SaveAsync] [ net_joboutputstorage_saveasync] (metodo) e specificare hello [JobOutputKind] [ net_joboutputkind] e il nome file:</span><span class="sxs-lookup"><span data-stu-id="17954-166">Store job output by calling hello [JobOutputStorage][net_joboutputstorage].[SaveAsync][net_joboutputstorage_saveasync] method, and specify hello [JobOutputKind][net_joboutputkind] and filename:</span></span>

```csharp
CloudJob job = new JobOutputStorage(acct, jobId);
JobOutputStorage jobOutputStorage = job.OutputStorage(linkedStorageAccount);

await jobOutputStorage.SaveAsync(JobOutputKind.JobOutput, "mymovie.mp4");
await jobOutputStorage.SaveAsync(JobOutputKind.JobPreview, "mymovie_preview.mp4");
```

<span data-ttu-id="17954-167">Come con hello **TaskOutputKind** tipo per l'output di un'attività, utilizzare hello [JobOutputKind] [ net_joboutputkind] toocategorize tipo un processo del persistenti i file.</span><span class="sxs-lookup"><span data-stu-id="17954-167">As with hello **TaskOutputKind** type for task outputs, you use hello [JobOutputKind][net_joboutputkind] type toocategorize a job's persisted files.</span></span> <span data-ttu-id="17954-168">Questo parametro consente query toolater per un tipo specifico di output (elenco).</span><span class="sxs-lookup"><span data-stu-id="17954-168">This parameter allows you toolater query for (list) a specific type of output.</span></span> <span data-ttu-id="17954-169">Hello **JobOutputKind** tipo include categorie output e di anteprima e supporta la creazione di categorie personalizzate.</span><span class="sxs-lookup"><span data-stu-id="17954-169">hello **JobOutputKind** type includes both output and preview categories, and supports creating custom categories.</span></span>

### <a name="store-task-logs"></a><span data-ttu-id="17954-170">Archiviare i log delle attività</span><span class="sxs-lookup"><span data-stu-id="17954-170">Store task logs</span></span>

<span data-ttu-id="17954-171">Inoltre toopersisting un'archiviazione toodurable file quando un'attività o un processo viene completato, potrebbe essere necessario toopersist file aggiornati durante l'esecuzione di un'attività di hello &mdash; i file di log o `stdout.txt` e `stderr.txt`, ad esempio.</span><span class="sxs-lookup"><span data-stu-id="17954-171">In addition toopersisting a file toodurable storage when a task or job completes, you may need toopersist files that are updated during hello execution of a task &mdash; log files or `stdout.txt` and `stderr.txt`, for example.</span></span> <span data-ttu-id="17954-172">A tale scopo, la libreria di Azure Batch File convenzioni hello fornisce hello [TaskOutputStorage][net_taskoutputstorage].[ SaveTrackedAsync] [ net_savetrackedasync] metodo.</span><span class="sxs-lookup"><span data-stu-id="17954-172">For this purpose, hello Azure Batch File Conventions library provides hello [TaskOutputStorage][net_taskoutputstorage].[SaveTrackedAsync][net_savetrackedasync] method.</span></span> <span data-ttu-id="17954-173">Con [SaveTrackedAsync][net_savetrackedasync], è possibile tenere traccia di file tooa degli aggiornamenti nel nodo hello (in un intervallo specificato) e rendere persistenti tali tooAzure aggiornamenti archiviazione.</span><span class="sxs-lookup"><span data-stu-id="17954-173">With [SaveTrackedAsync][net_savetrackedasync], you can track updates tooa file on hello node (at an interval that you specify) and persist those updates tooAzure Storage.</span></span>

<span data-ttu-id="17954-174">Nel seguente frammento di codice di hello, utilizziamo [SaveTrackedAsync] [ net_savetrackedasync] tooupdate `stdout.txt` in archiviazione di Azure ogni 15 secondi, durante l'esecuzione di hello dell'attività hello:</span><span class="sxs-lookup"><span data-stu-id="17954-174">In hello following code snippet, we use [SaveTrackedAsync][net_savetrackedasync] tooupdate `stdout.txt` in Azure Storage every 15 seconds during hello execution of hello task:</span></span>

```csharp
TimeSpan stdoutFlushDelay = TimeSpan.FromSeconds(3);
string logFilePath = Path.Combine(
    Environment.GetEnvironmentVariable("AZ_BATCH_TASK_DIR"), "stdout.txt");

// hello primary task logic is wrapped in a using statement that sends updates to
// hello stdout.txt blob in Storage every 15 seconds while hello task code runs.
using (ITrackedSaveOperation stdout =
        await taskStorage.SaveTrackedAsync(
        TaskOutputKind.TaskLog,
        logFilePath,
        "stdout.txt",
        TimeSpan.FromSeconds(15)))
{
    /* Code tooprocess data and produce output file(s) */

    // We are tracking hello disk file toosave our standard output, but the
    // node agent may take up too3 seconds tooflush hello stdout stream to
    // disk. So give hello file a moment toocatch up.
     await Task.Delay(stdoutFlushDelay);
}
```

<span data-ttu-id="17954-175">Hello commentato sezione `Code tooprocess data and produce output file(s)` è un segnaposto per il codice hello eseguirebbe in genere l'attività.</span><span class="sxs-lookup"><span data-stu-id="17954-175">hello commented section `Code tooprocess data and produce output file(s)` is a placeholder for hello code that your task would normally perform.</span></span> <span data-ttu-id="17954-176">Ad esempio, potrebbe essere disponibile codice che scarica i dati da Archiviazione di Azure ed esegue un calcolo o una trasformazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="17954-176">For example, you might have code that downloads data from Azure Storage and performs transformation or calculation on it.</span></span> <span data-ttu-id="17954-177">aspetto importante di questo frammento di codice Hello è illustrare come è possibile eseguire il wrapping tale codice in un `using` tooperiodically blocco aggiornare un file con [SaveTrackedAsync][net_savetrackedasync].</span><span class="sxs-lookup"><span data-stu-id="17954-177">hello important part of this snippet is demonstrating how you can wrap such code in a `using` block tooperiodically update a file with [SaveTrackedAsync][net_savetrackedasync].</span></span>

<span data-ttu-id="17954-178">agente nodo Hello è un programma che viene eseguito in ogni nodo nel pool di hello e fornisce l'interfaccia di comando e controllo hello tra nodo hello e il servizio Batch hello.</span><span class="sxs-lookup"><span data-stu-id="17954-178">hello node agent is a program that runs on each node in hello pool and provides hello command-and-control interface between hello node and hello Batch service.</span></span> <span data-ttu-id="17954-179">Hello `Task.Delay` è necessaria alla fine di hello di questa chiamata `using` tooensure di blocco che hello agente nodo dispone di contenuto di hello tooflush ora dello standard toohello stdout.txt file nel nodo hello.</span><span class="sxs-lookup"><span data-stu-id="17954-179">hello `Task.Delay` call is required at hello end of this `using` block tooensure that hello node agent has time tooflush hello contents of standard out toohello stdout.txt file on hello node.</span></span> <span data-ttu-id="17954-180">Senza questo ritardo, è possibile toomiss hello ultimi secondi dell'output.</span><span class="sxs-lookup"><span data-stu-id="17954-180">Without this delay, it is possible toomiss hello last few seconds of output.</span></span> <span data-ttu-id="17954-181">Questo ritardo potrebbe non essere necessario per tutti i file.</span><span class="sxs-lookup"><span data-stu-id="17954-181">This delay may not be required for all files.</span></span>

> [!NOTE]
> <span data-ttu-id="17954-182">Quando si abilita il file di rilevamento con **SaveTrackedAsync**, solo *aggiunge* toohello rilevati file sono persistenti tooAzure archiviazione.</span><span class="sxs-lookup"><span data-stu-id="17954-182">When you enable file tracking with **SaveTrackedAsync**, only *appends* toohello tracked file are persisted tooAzure Storage.</span></span> <span data-ttu-id="17954-183">Utilizzare questo metodo solo per la registrazione non rotazione dei file di log o altri file che vengono scritti toowith aggiungere fine toohello operazioni del file hello.</span><span class="sxs-lookup"><span data-stu-id="17954-183">Use this method only for tracking non-rotating log files or other files that are written toowith append operations toohello end of hello file.</span></span>
> 
> 

## <a name="retrieve-output-data"></a><span data-ttu-id="17954-184">Recuperare i dati di output</span><span class="sxs-lookup"><span data-stu-id="17954-184">Retrieve output data</span></span>

<span data-ttu-id="17954-185">Quando si recupera l'output persistente utilizzando hello Azure convenzioni dei File Batch libreria, non in modo basato su attività e a processo.</span><span class="sxs-lookup"><span data-stu-id="17954-185">When you retrieve your persisted output using hello Azure Batch File Conventions library, you do so in a task- and job-centric manner.</span></span> <span data-ttu-id="17954-186">È possibile richiedere hello di output per attività o il processo senza la necessità di tooknow il relativo percorso di archiviazione di Azure o anche il nome del file.</span><span class="sxs-lookup"><span data-stu-id="17954-186">You can request hello output for given task or job without needing tooknow its path in Azure Storage, or even its file name.</span></span> <span data-ttu-id="17954-187">In alternativa, è possibile richiedere i file di output in base all'ID dell'attività o del processo.</span><span class="sxs-lookup"><span data-stu-id="17954-187">Instead, you can request output files by task or job ID.</span></span>

<span data-ttu-id="17954-188">Hello frammento di codice seguente scorre le attività di un processo, stampa alcune informazioni sui file di output di hello per attività hello e quindi scarica i file dall'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="17954-188">hello following code snippet iterates through a job's tasks, prints some information about hello output files for hello task, and then downloads its files from Storage.</span></span>

```csharp
foreach (CloudTask task in myJob.ListTasks())
{
    foreach (OutputFileReference output in
        task.OutputStorage(storageAccount).ListOutputs(
            TaskOutputKind.TaskOutput))
    {
        Console.WriteLine($"output file: {output.FilePath}");

        output.DownloadToFileAsync(
            $"{jobId}-{output.FilePath}",
            System.IO.FileMode.Create).Wait();
    }
}
```

## <a name="view-output-files-in-hello-azure-portal"></a><span data-ttu-id="17954-189">Visualizzare i file di output in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="17954-189">View output files in hello Azure portal</span></span>

<span data-ttu-id="17954-190">Hello portale di Azure consente di visualizzare i file di output di attività e i log dei tooa persistente collegati account di archiviazione di Azure utilizzando hello [standard convenzioni dei File Batch](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span><span class="sxs-lookup"><span data-stu-id="17954-190">hello Azure portal displays task output files and logs that are persisted tooa linked Azure Storage account using hello [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span></span> <span data-ttu-id="17954-191">È possibile implementare queste convenzioni in un linguaggio di propria scelta hello oppure è possibile utilizzare raccolta convenzioni File hello nelle applicazioni .NET.</span><span class="sxs-lookup"><span data-stu-id="17954-191">You can implement these conventions yourself in hello a language of your choice, or you can use hello File Conventions library in your .NET applications.</span></span>

<span data-ttu-id="17954-192">visualizzazione di hello tooenable dei file di output nel portale di hello, è necessario soddisfare hello seguenti requisiti:</span><span class="sxs-lookup"><span data-stu-id="17954-192">tooenable hello display of your output files in hello portal, you must satisfy hello following requirements:</span></span>

1. <span data-ttu-id="17954-193">[Collegare un account di archiviazione di Azure](#requirement-linked-storage-account) tooyour account Batch.</span><span class="sxs-lookup"><span data-stu-id="17954-193">[Link an Azure Storage account](#requirement-linked-storage-account) tooyour Batch account.</span></span>
2. <span data-ttu-id="17954-194">Rispettare le convenzioni di denominazione toohello predefinito per i contenitori di archiviazione e i file durante il salvataggio di output.</span><span class="sxs-lookup"><span data-stu-id="17954-194">Adhere toohello predefined naming conventions for Storage containers and files when persisting outputs.</span></span> <span data-ttu-id="17954-195">È possibile trovare la definizione di hello di queste convenzioni nella libreria convenzioni File hello [Leggimi][github_file_conventions_readme].</span><span class="sxs-lookup"><span data-stu-id="17954-195">You can find hello definition of these conventions in hello File Conventions library [README][github_file_conventions_readme].</span></span> <span data-ttu-id="17954-196">Se si utilizza hello [convenzioni File Batch di Azure] [ nuget_package] libreria toopersist l'output, i file sono persistenti in base toohello convenzioni dei File standard.</span><span class="sxs-lookup"><span data-stu-id="17954-196">If you use hello [Azure Batch File Conventions][nuget_package] library toopersist your output, your files are persisted according toohello File Conventions standard.</span></span>

<span data-ttu-id="17954-197">l'output dell'attività tooview file e viene registrato in hello portale di Azure, passare toohello attività il cui output si è interessati, quindi fare clic su **i file di output salvato** o **registri salvati**.</span><span class="sxs-lookup"><span data-stu-id="17954-197">tooview task output files and logs in hello Azure portal, navigate toohello task whose output you are interested in, then click either **Saved output files** or **Saved logs**.</span></span> <span data-ttu-id="17954-198">La seguente immagine illustra hello **i file di output salvato** per attività hello con ID "007":</span><span class="sxs-lookup"><span data-stu-id="17954-198">This image shows hello **Saved output files** for hello task with ID "007":</span></span>

<span data-ttu-id="17954-199">![Nel portale di Azure hello pannello risultati delle attività][2]</span><span class="sxs-lookup"><span data-stu-id="17954-199">![Task outputs blade in hello Azure portal][2]</span></span>

## <a name="code-sample"></a><span data-ttu-id="17954-200">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="17954-200">Code sample</span></span>

<span data-ttu-id="17954-201">Hello [PersistOutputs] [ github_persistoutputs] progetto di esempio è uno dei hello [esempi di codice di Azure Batch] [ github_samples] su GitHub.</span><span class="sxs-lookup"><span data-stu-id="17954-201">hello [PersistOutputs][github_persistoutputs] sample project is one of hello [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="17954-202">Questa soluzione di Visual Studio viene illustrato come dell'output dell'archiviazione toodurable toouse hello Azure convenzioni dei File Batch libreria toopersist attività.</span><span class="sxs-lookup"><span data-stu-id="17954-202">This Visual Studio solution demonstrates how toouse hello Azure Batch File Conventions library toopersist task output toodurable storage.</span></span> <span data-ttu-id="17954-203">hello toorun di esempio, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="17954-203">toorun hello sample, follow these steps:</span></span>

1. <span data-ttu-id="17954-204">Progetto aperto hello in **Visual Studio 2015 o versione successiva**.</span><span class="sxs-lookup"><span data-stu-id="17954-204">Open hello project in **Visual Studio 2015 or newer**.</span></span>
2. <span data-ttu-id="17954-205">Aggiungere il Batch e l'archiviazione **delle credenziali dell'account** troppo**AccountSettings.settings** nel progetto Microsoft.Azure.Batch.Samples.Common hello.</span><span class="sxs-lookup"><span data-stu-id="17954-205">Add your Batch and Storage **account credentials** too**AccountSettings.settings** in hello Microsoft.Azure.Batch.Samples.Common project.</span></span>
3. <span data-ttu-id="17954-206">**Compilare** (ma non le eseguono) hello soluzione.</span><span class="sxs-lookup"><span data-stu-id="17954-206">**Build** (but do not run) hello solution.</span></span> <span data-ttu-id="17954-207">Se richiesto, ripristinare tutti i pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="17954-207">Restore any NuGet packages if prompted.</span></span>
4. <span data-ttu-id="17954-208">Hello utilizzare tooupload portale Azure un [pacchetto di applicazione](batch-application-packages.md) per **PersistOutputsTask**.</span><span class="sxs-lookup"><span data-stu-id="17954-208">Use hello Azure portal tooupload an [application package](batch-application-packages.md) for **PersistOutputsTask**.</span></span> <span data-ttu-id="17954-209">Includere hello `PersistOutputsTask.exe` e i relativi assembly dipendenti nel pacchetto ZIP hello, set di ID dell'applicazione hello troppo "PersistOutputsTask" e un'applicazione hello pacchetto versione troppo "1.0".</span><span class="sxs-lookup"><span data-stu-id="17954-209">Include hello `PersistOutputsTask.exe` and its dependent assemblies in hello .zip package, set hello application ID too"PersistOutputsTask", and hello application package version too"1.0".</span></span>
5. <span data-ttu-id="17954-210">**Avviare** hello (esecuzione) **PersistOutputs** progetto.</span><span class="sxs-lookup"><span data-stu-id="17954-210">**Start** (run) hello **PersistOutputs** project.</span></span>
6. <span data-ttu-id="17954-211">Quando richiesto toochoose hello persistenza tecnologia toouse per esempio hello in esecuzione, immettere **1** : esempio hello toorun utilizzando l'output dell'attività toopersist libreria convenzioni File hello.</span><span class="sxs-lookup"><span data-stu-id="17954-211">When prompted toochoose hello persistence technology toouse for running hello sample, enter **1** toorun hello sample using hello File Conventions library toopersist task output.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="17954-212">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="17954-212">Next steps</span></span>

### <a name="get-hello-batch-file-conventions-library-for-net"></a><span data-ttu-id="17954-213">Ottenere libreria di hello convenzioni dei File Batch per .NET</span><span class="sxs-lookup"><span data-stu-id="17954-213">Get hello Batch File Conventions library for .NET</span></span>

<span data-ttu-id="17954-214">libreria di Hello convenzioni dei File Batch per .NET è disponibile sul [NuGet][nuget_package].</span><span class="sxs-lookup"><span data-stu-id="17954-214">hello Batch File Conventions library for .NET is available on [NuGet][nuget_package].</span></span> <span data-ttu-id="17954-215">libreria Hello estende hello [CloudJob] [ net_cloudjob] e [CloudTask] [ net_cloudtask] classi con nuovi metodi.</span><span class="sxs-lookup"><span data-stu-id="17954-215">hello library extends hello [CloudJob][net_cloudjob] and [CloudTask][net_cloudtask] classes with new methods.</span></span> <span data-ttu-id="17954-216">Vedere anche hello [documentazione di riferimento](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) per la libreria di convenzioni per i File hello.</span><span class="sxs-lookup"><span data-stu-id="17954-216">Also see hello [reference documentation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) for hello File Conventions library.</span></span>

<span data-ttu-id="17954-217">Hello [codice sorgente] [ github_file_conventions] per hello convenzioni di File di libreria è disponibile su GitHub in hello Microsoft Azure SDK per il repository di .NET.</span><span class="sxs-lookup"><span data-stu-id="17954-217">hello [source code][github_file_conventions] for hello File Conventions library is available on GitHub in hello Microsoft Azure SDK for .NET repository.</span></span> 

### <a name="explore-other-approaches-for-persisting-output-data"></a><span data-ttu-id="17954-218">Esplorare altri approcci per rendere persistenti i dati di output</span><span class="sxs-lookup"><span data-stu-id="17954-218">Explore other approaches for persisting output data</span></span>

- <span data-ttu-id="17954-219">Vedere [Persist processi e delle attività di output tooAzure archiviazione](batch-task-output.md) per una panoramica di rendere persistenti i dati di attività e processi.</span><span class="sxs-lookup"><span data-stu-id="17954-219">See [Persist job and task output tooAzure Storage](batch-task-output.md) for an overview of persisting task and job data.</span></span>
- <span data-ttu-id="17954-220">Vedere [mantenere i dati di attività tooAzure archiviazione con l'API del servizio Batch hello](batch-task-output-files.md) toolearn come toouse hello API del servizio Batch toopersist dati di output.</span><span class="sxs-lookup"><span data-stu-id="17954-220">See [Persist task data tooAzure Storage with hello Batch service API](batch-task-output-files.md) toolearn how toouse hello Batch service API toopersist output data.</span></span>

[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[github_file_conventions]: https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Batch/FileConventions
[github_file_conventions_readme]: https://github.com/Azure/azure-sdk-for-net/blob/AutoRest/src/Batch/FileConventions/README.md
[github_persistoutputs]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/PersistOutputs
[github_samples]: https://github.com/Azure/azure-batch-samples
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_cloudstorageaccount]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_fileconventions_readme]: https://github.com/Azure/azure-sdk-for-net/blob/AutoRest/src/Batch/FileConventions/README.md
[net_joboutputkind]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputkind.aspx
[net_joboutputstorage]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputstorage.aspx
[net_joboutputstorage_saveasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputstorage.saveasync.aspx
[net_msdn]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[net_prepareoutputasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.cloudjobextensions.prepareoutputstorageasync.aspx
[net_saveasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx
[net_savetrackedasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.savetrackedasync.aspx
[net_taskoutputkind]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputkind.aspx
[net_taskoutputstorage]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx
[nuget_manager]: https://docs.nuget.org/consume/installing-nuget
[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[portal]: https://portal.azure.com
[storage_explorer]: http://storageexplorer.com/

[1]: ./media/batch-task-output/task-output-01.png "Selettori di file di output salvati e di log salvati nel portale"
[2]: ./media/batch-task-output/task-output-02.png "Nel portale di Azure hello pannello risultati delle attività"
