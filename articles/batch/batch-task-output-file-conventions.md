---
title: "Rendere persistente l'output di processi e attività in Archiviazione di Azure con la libreria File Conventions per .NET - Azure Batch | Microsoft Docs"
description: "Informazioni su come usare la libreria Azure Batch File Conventions per .NET per rendere persistente l'output di attività e processi di Batch in Archiviazione di Azure e visualizzare l'output reso persistente nel portale di Azure."
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
ms.openlocfilehash: a9de327c20463469bc91d9720aa17333a36f919e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="persist-job-and-task-data-to-azure-storage-with-the-batch-file-conventions-library-for-net-to-persist"></a><span data-ttu-id="7d29c-103">Rendere persistenti i dati di attività e processi in Archiviazione di Azure con la libreria Batch File Conventions per .NET</span><span class="sxs-lookup"><span data-stu-id="7d29c-103">Persist job and task data to Azure Storage with the Batch File Conventions library for .NET to persist</span></span> 

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

<span data-ttu-id="7d29c-104">Un modo per rendere persistenti i dati consiste nell'usare la [libreria Azure Batch File Conventions per .NET][nuget_package].</span><span class="sxs-lookup"><span data-stu-id="7d29c-104">One way to persist task data is to use the [Azure Batch File Conventions library for .NET][nuget_package].</span></span> <span data-ttu-id="7d29c-105">La libreria File Conventions semplifica il processo di archiviazione dei dati di output delle attività in Archiviazione di Azure e il relativo recupero.</span><span class="sxs-lookup"><span data-stu-id="7d29c-105">The File Conventions library simplifies the process of storing task output data to Azure Storage and retrieving it.</span></span> <span data-ttu-id="7d29c-106">È possibile usare la libreria File Conventions sia nel codice di attività che nel codice client: nel codice di attività per rendere persistenti i file e nel codice client per elencarli e recuperarli.</span><span class="sxs-lookup"><span data-stu-id="7d29c-106">You can use the File Conventions library in both task and client code &mdash; in task code for persisting files, and in client code to list and retrieve them.</span></span> <span data-ttu-id="7d29c-107">È anche possibile usare la libreria nel codice di attività per recuperare l'output delle attività upstream, ad esempio in uno scenario di [dipendenze tra attività](batch-task-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="7d29c-107">Your task code can also use the library to retrieve the output of upstream tasks, such as in a [task dependencies](batch-task-dependencies.md) scenario.</span></span> 

<span data-ttu-id="7d29c-108">Per recuperare i file di output con la libreria File Conventions, è possibile individuare i file per un determinato processo o un'attività elencandoli in base a ID e scopo.</span><span class="sxs-lookup"><span data-stu-id="7d29c-108">To retrieve output files with the File Conventions library, you can locate the files for a given job or task by listing them by ID and purpose.</span></span> <span data-ttu-id="7d29c-109">Non è necessario conoscere i nomi o i percorsi dei file.</span><span class="sxs-lookup"><span data-stu-id="7d29c-109">You don't need to know the names or locations of the files.</span></span> <span data-ttu-id="7d29c-110">Ad esempio, è possibile usare la libreria File Conventions per elencare tutti i file intermedi per una determinata attività o per ottenere un file di anteprima per un determinato processo.</span><span class="sxs-lookup"><span data-stu-id="7d29c-110">For example, you can use the File Conventions library to list all intermediate files for a given task, or get a preview file for a given job.</span></span>

> [!TIP]
> <span data-ttu-id="7d29c-111">A partire dalla versione 2017-05-01, l'API del servizio Batch supporta la persistenza dei dati di output in Archiviazione di Azure per le attività e le attività di gestione processo eseguite sui pool creati con la configurazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7d29c-111">Starting with version 2017-05-01, the Batch service API supports persisting output data to Azure Storage for tasks and job manager tasks that run on pools created with the virtual machine configuration.</span></span> <span data-ttu-id="7d29c-112">L'API del servizio Batch mette a disposizione un modo semplice per rendere persistente l'output dall'interno del codice che crea un'attività e rappresenta un'alternativa alla libreria File Conventions.</span><span class="sxs-lookup"><span data-stu-id="7d29c-112">The Batch service API provides a simple way to persist output from within the code that creates a task and serves as an alternative to the File Conventions library.</span></span> <span data-ttu-id="7d29c-113">È possibile modificare le applicazioni client del servizio Batch in modo che rendano persistente l'output senza dover aggiornare l'applicazione eseguita dall'attività.</span><span class="sxs-lookup"><span data-stu-id="7d29c-113">You can modify your Batch client applications to persist output without needing to update the application that your task is running.</span></span> <span data-ttu-id="7d29c-114">Per altre informazioni, vedere [Rendere persistenti i dati di attività in Archiviazione di Azure con l'API del servizio Batch](batch-task-output-files.md).</span><span class="sxs-lookup"><span data-stu-id="7d29c-114">For more information, see [Persist task data to Azure Storage with the Batch service API](batch-task-output-files.md).</span></span>
> 
> 

## <a name="when-do-i-use-the-file-conventions-library-to-persist-task-output"></a><span data-ttu-id="7d29c-115">Quando è appropriato usare la libreria File Conventions per rendere persistente l'output delle attività?</span><span class="sxs-lookup"><span data-stu-id="7d29c-115">When do I use the File Conventions library to persist task output?</span></span>

<span data-ttu-id="7d29c-116">Il servizio Azure Batch offre diversi modi per rendere persistente l'output delle attività.</span><span class="sxs-lookup"><span data-stu-id="7d29c-116">Azure Batch provides more than one way to persist task output.</span></span> <span data-ttu-id="7d29c-117">La libreria File Conventions è la scelta ottimale per questi scenari:</span><span class="sxs-lookup"><span data-stu-id="7d29c-117">The File Conventions is best suited to these scenarios:</span></span>

- <span data-ttu-id="7d29c-118">È possibile modificare facilmente il codice per l'applicazione eseguita dall'attività per rendere persistenti i file usando la libreria File Conventions.</span><span class="sxs-lookup"><span data-stu-id="7d29c-118">You can easily modify the code for the application that your task is running to persist files using the File Conventions library.</span></span>
- <span data-ttu-id="7d29c-119">Si vogliono inviare flussi di dati in Archiviazione di Azure mentre l'attività è ancora in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="7d29c-119">You want to stream data to Azure Storage while the task is still running.</span></span>
- <span data-ttu-id="7d29c-120">Si vogliono rendere persistenti i dati dai pool creati con la configurazione del servizio cloud o con la configurazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7d29c-120">You want to persist data from pools created with either the cloud service configuration or the virtual machine configuration.</span></span>
- <span data-ttu-id="7d29c-121">L'applicazione client o altre attività nel processo devono individuare e scaricare i file di output delle attività in base all'ID o allo scopo.</span><span class="sxs-lookup"><span data-stu-id="7d29c-121">Your client application or other tasks in the job needs to locate and download task output files by ID or by purpose.</span></span> 
- <span data-ttu-id="7d29c-122">Si vuole visualizzare l'output delle attività nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7d29c-122">You want to view task output in the Azure portal.</span></span>

<span data-ttu-id="7d29c-123">Se lo scenario è diverso da quelli sopra elencati, potrebbe essere necessario prendere in considerazione un approccio diverso.</span><span class="sxs-lookup"><span data-stu-id="7d29c-123">If your scenario differs from those listed above, you may need to consider a different approach.</span></span> <span data-ttu-id="7d29c-124">Per altre informazioni sulle opzioni per rendere persistente l'output delle attività, vedere [Rendere persistente l'output di processi e attività](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="7d29c-124">For more information on other options for persisting task output, see [Persist job and task output to Azure Storage](batch-task-output.md).</span></span> 

## <a name="what-is-the-batch-file-conventions-standard"></a><span data-ttu-id="7d29c-125">Che cos'è lo standard Batch File Conventions?</span><span class="sxs-lookup"><span data-stu-id="7d29c-125">What is the Batch File Conventions standard?</span></span>

<span data-ttu-id="7d29c-126">Lo [standard Batch File Conventions](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) fornisce uno schema di denominazione per i percorsi di contenitori e BLOB di destinazione in cui vengono scritti i file di output.</span><span class="sxs-lookup"><span data-stu-id="7d29c-126">The [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) provides a naming scheme for the destination containers and blob paths to which your output files are written.</span></span> <span data-ttu-id="7d29c-127">I file resi persistenti in Archiviazione di Azure e conformi allo standard File Conventions sono automaticamente disponibili per la visualizzazione nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7d29c-127">Files persisted to Azure Storage that adhere to the File Conventions standard are automatically available for viewing in the Azure portal.</span></span> <span data-ttu-id="7d29c-128">Il portale riconosce la convenzione di denominazione e pertanto può visualizzare i file che rispettano tale convenzione.</span><span class="sxs-lookup"><span data-stu-id="7d29c-128">The portal is aware of the naming convention and so can display files that adhere to it.</span></span>

<span data-ttu-id="7d29c-129">La libreria File Conventions per .NET assegna automaticamente i nomi ai contenitori di archiviazione e ai file di output delle attività in base allo standard File Conventions.</span><span class="sxs-lookup"><span data-stu-id="7d29c-129">The File Conventions library for .NET automatically names your storage containers and task output files according to the File Conventions standard.</span></span> <span data-ttu-id="7d29c-130">La libreria File Conventions fornisce anche metodi per eseguire query sui file di output in Archiviazione di Azure in base all'ID del processo, all'ID dell'attività o allo scopo.</span><span class="sxs-lookup"><span data-stu-id="7d29c-130">The File Conventions library also provides methods to query output files in Azure Storage according to job ID, task ID, or purpose.</span></span>   

<span data-ttu-id="7d29c-131">Se si sviluppa con un linguaggio diverso da .NET, è possibile implementare autonomamente lo standard File Conventions nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7d29c-131">If you are developing with a language other than .NET, you can implement the File Conventions standard yourself in your application.</span></span> <span data-ttu-id="7d29c-132">Per altre informazioni, vedere [Informazioni sullo standard Batch File Conventions](batch-task-output.md#about-the-batch-file-conventions-standard).</span><span class="sxs-lookup"><span data-stu-id="7d29c-132">For more information, see [About the Batch File Conventions standard](batch-task-output.md#about-the-batch-file-conventions-standard).</span></span>

## <a name="link-an-azure-storage-account-to-your-batch-account"></a><span data-ttu-id="7d29c-133">Collegare un account di archiviazione di Azure all'account Batch</span><span class="sxs-lookup"><span data-stu-id="7d29c-133">Link an Azure Storage account to your Batch account</span></span>

<span data-ttu-id="7d29c-134">Per rendere persistenti i dati di output in Archiviazione di Azure usando la libreria File Conventions, è prima necessario collegare un account di Archiviazione di Azure all'account Batch.</span><span class="sxs-lookup"><span data-stu-id="7d29c-134">To persist output data to Azure Storage using the File Conventions library, you must first link an Azure Storage account to your Batch account.</span></span> <span data-ttu-id="7d29c-135">Se non è già stato fatto, collegare un account di archiviazione all'account Batch tramite il [portale di Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="7d29c-135">If you haven't done so already, link a Storage account to your Batch account by using the [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="7d29c-136">Passare all'account Batch nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7d29c-136">Navigate to your Batch account in the Azure portal.</span></span> 
2. <span data-ttu-id="7d29c-137">In **Impostazioni** selezionare **Account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="7d29c-137">Under **Settings**, select **Storage Account**.</span></span>
3. <span data-ttu-id="7d29c-138">Se non è già disponibile un account di archiviazione associato all'account Batch, fare clic su **Account di archiviazione (nessuno)**.</span><span class="sxs-lookup"><span data-stu-id="7d29c-138">If you do not already have a Storage account associated with your Batch account, click **Storage Account (None)**.</span></span>
4. <span data-ttu-id="7d29c-139">Selezionare un account di archiviazione nell'elenco per la sottoscrizione corrente.</span><span class="sxs-lookup"><span data-stu-id="7d29c-139">Select a Storage account from the list for your subscription.</span></span> <span data-ttu-id="7d29c-140">Per prestazioni ottimali, usare un account di Archiviazione di Azure nella stessa area dell'account Batch in cui si eseguono le attività.</span><span class="sxs-lookup"><span data-stu-id="7d29c-140">For best performance, use an Azure Storage account that is in the same region as the Batch account where your tasks are running.</span></span>

## <a name="persist-output-data"></a><span data-ttu-id="7d29c-141">Rendere persistenti i dati di output</span><span class="sxs-lookup"><span data-stu-id="7d29c-141">Persist output data</span></span>

<span data-ttu-id="7d29c-142">Per rendere persistenti i dati di output di processi e attività con la libreria File Conventions, creare un contenitore in Archiviazione di Azure e quindi salvare l'output nel contenitore.</span><span class="sxs-lookup"><span data-stu-id="7d29c-142">To persist job and task output data with the File Conventions library, create a container in Azure Storage, then save the output to the container.</span></span> <span data-ttu-id="7d29c-143">Usare la [libreria client di Archiviazione di Azure per .NET](https://www.nuget.org/packages/WindowsAzure.Storage) nel codice dell'attività per caricare l'output dell'attività nel contenitore.</span><span class="sxs-lookup"><span data-stu-id="7d29c-143">Use the [Azure Storage client library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage) in your task code to upload the task output to the container.</span></span> 

<span data-ttu-id="7d29c-144">Per altre informazioni sull'uso di contenitori e BLOB in Archiviazione di Azure, vedere [Introduzione all'archiviazione BLOB di Azure con .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="7d29c-144">For more information about working with containers and blobs in Azure Storage, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span>

> [!WARNING]
> <span data-ttu-id="7d29c-145">Tutti gli output di processi e attività resi persistenti con la libreria File Conventions vengono archiviati nello stesso contenitore.</span><span class="sxs-lookup"><span data-stu-id="7d29c-145">All job and task outputs persisted with the File Conventions library are stored in the same container.</span></span> <span data-ttu-id="7d29c-146">Se un numero elevato di attività tenta di rendere persistenti i file nello stesso momento, potrebbero essere applicate [limitazioni dell'archiviazione](../storage/common/storage-performance-checklist.md#blobs).</span><span class="sxs-lookup"><span data-stu-id="7d29c-146">If a large number of tasks try to persist files at the same time, [storage throttling limits](../storage/common/storage-performance-checklist.md#blobs) may be enforced.</span></span>
> 
> 

### <a name="create-storage-container"></a><span data-ttu-id="7d29c-147">Creare un contenitore di archiviazione</span><span class="sxs-lookup"><span data-stu-id="7d29c-147">Create storage container</span></span>

<span data-ttu-id="7d29c-148">Per rendere persistente l'output delle attività in Archiviazione di Azure, creare innanzitutto un contenitore chiamando [CloudJob][net_cloudjob].[PrepareOutputStorageAsync][net_prepareoutputasync].</span><span class="sxs-lookup"><span data-stu-id="7d29c-148">To persist task output to Azure Storage, first create a container by calling [CloudJob][net_cloudjob].[PrepareOutputStorageAsync][net_prepareoutputasync].</span></span> <span data-ttu-id="7d29c-149">Questo metodo di estensione accetta un oggetto [CloudStorageAccount] [ net_cloudstorageaccount] come parametro.</span><span class="sxs-lookup"><span data-stu-id="7d29c-149">This extension method takes a [CloudStorageAccount][net_cloudstorageaccount] object as a parameter.</span></span> <span data-ttu-id="7d29c-150">Crea un contenitore denominato in base allo standard File Conventions, in modo che il relativo contenuto sia individuabile dal portale di Azure e dai metodi di recupero descritti più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="7d29c-150">It creates a container named according to the File Conventions standard,so that its contents are discoverable by the Azure portal and the retrieval methods discussed later in the article.</span></span>

<span data-ttu-id="7d29c-151">In genere si inserisce il codice per creare un contenitore nell'applicazione client, ovvero l'applicazione che crea i pool, i processi e le attività.</span><span class="sxs-lookup"><span data-stu-id="7d29c-151">You typically place the code to create a container in your client application &mdash; the application that creates your pools, jobs, and tasks.</span></span>

```csharp
CloudJob job = batchClient.JobOperations.CreateJob(
    "myJob",
    new PoolInformation { PoolId = "myPool" });

// Create reference to the linked Azure Storage account
CloudStorageAccount linkedStorageAccount =
    new CloudStorageAccount(myCredentials, true);

// Create the blob storage container for the outputs
await job.PrepareOutputStorageAsync(linkedStorageAccount);
```

### <a name="store-task-outputs"></a><span data-ttu-id="7d29c-152">Archiviare gli output delle attività</span><span class="sxs-lookup"><span data-stu-id="7d29c-152">Store task outputs</span></span>

<span data-ttu-id="7d29c-153">Dopo avere preparato un contenitore in Archiviazione di Azure, le attività possono salvare l'output nel contenitore usando la classe [TaskOutputStorage][net_taskoutputstorage] disponibile nella libreria File Conventions.</span><span class="sxs-lookup"><span data-stu-id="7d29c-153">Now that you've prepared a container in Azure Storage, tasks can save output to the container by using the [TaskOutputStorage][net_taskoutputstorage] class found in the File Conventions library.</span></span>

<span data-ttu-id="7d29c-154">Nel codice dell'attività creare un oggetto [TaskOutputStorage][net_taskoutputstorage] e quindi, dopo che l'attività ha completato tutte le relative operazioni, chiamare il metodo [TaskOutputStorage][net_taskoutputstorage].[SaveAsync][net_saveasync] per salvarne l'output in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7d29c-154">In your task code, first create a [TaskOutputStorage][net_taskoutputstorage] object, then when the task has completed its work, call the [TaskOutputStorage][net_taskoutputstorage].[SaveAsync][net_saveasync] method to save its output to Azure Storage.</span></span>

```csharp
CloudStorageAccount linkedStorageAccount = new CloudStorageAccount(myCredentials);
string jobId = Environment.GetEnvironmentVariable("AZ_BATCH_JOB_ID");
string taskId = Environment.GetEnvironmentVariable("AZ_BATCH_TASK_ID");

TaskOutputStorage taskOutputStorage = new TaskOutputStorage(
    linkedStorageAccount, jobId, taskId);

/* Code to process data and produce output file(s) */

await taskOutputStorage.SaveAsync(TaskOutputKind.TaskOutput, "frame_full_res.jpg");
await taskOutputStorage.SaveAsync(TaskOutputKind.TaskPreview, "frame_low_res.jpg");
```

<span data-ttu-id="7d29c-155">Il parametro `kind` del metodo [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) consente di categorizzare i file persistenti.</span><span class="sxs-lookup"><span data-stu-id="7d29c-155">The `kind` parameter of the [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) method categorizes the persisted files.</span></span> <span data-ttu-id="7d29c-156">Esistono quattro tipi [TaskOutputKind][net_taskoutputkind] predefiniti: `TaskOutput`, `TaskPreview`, `TaskLog` e `TaskIntermediate.` È anche possibile definire categorie personalizzate di output.</span><span class="sxs-lookup"><span data-stu-id="7d29c-156">There are four predefined [TaskOutputKind][net_taskoutputkind] types: `TaskOutput`, `TaskPreview`, `TaskLog`, and `TaskIntermediate.` You can also define custom categories of output.</span></span>

<span data-ttu-id="7d29c-157">Questi tipi di output consentono di specificare il tipo di output da elencare, quando in seguito si eseguono query su Batch per visualizzare gli output salvati in modo permanente per una determinata attività.</span><span class="sxs-lookup"><span data-stu-id="7d29c-157">These output types allow you to specify which type of outputs to list when you later query Batch for the persisted outputs of a given task.</span></span> <span data-ttu-id="7d29c-158">In altre parole, quando si elencano gli output per un'attività, è possibile filtrare l'elenco in base a uno dei tipi di output.</span><span class="sxs-lookup"><span data-stu-id="7d29c-158">In other words, when you list the outputs for a task, you can filter the list on one of the output types.</span></span> <span data-ttu-id="7d29c-159">Ad esempio, "Scaricare l'output di *anteprima* per l'attività *109*."</span><span class="sxs-lookup"><span data-stu-id="7d29c-159">For example, "Give me the *preview* output for task *109*."</span></span> <span data-ttu-id="7d29c-160">Altre informazioni su come elencare e recuperare gli output sono disponibili in [Recuperare l'output](#retrieve-output) più avanti nell'articolo.</span><span class="sxs-lookup"><span data-stu-id="7d29c-160">More on listing and retrieving outputs appears in [Retrieve output](#retrieve-output) later in the article.</span></span>

> [!TIP]
> <span data-ttu-id="7d29c-161">Il tipo di output determina anche dove viene visualizzato un file specifico nel portale di Azure. *TaskOutput*: i file categorizzati vengono visualizzati in **File di output delle attività** e i file di *TaskLog* vengono visualizzati in **Task logs** (Log delle attività).</span><span class="sxs-lookup"><span data-stu-id="7d29c-161">The output kind also determines where in the Azure portal a particular file appears: *TaskOutput*-categorized files appear under **Task output files**, and *TaskLog* files appear under **Task logs**.</span></span>
> 
> 

### <a name="store-job-outputs"></a><span data-ttu-id="7d29c-162">Archiviare gli output del processo</span><span class="sxs-lookup"><span data-stu-id="7d29c-162">Store job outputs</span></span>

<span data-ttu-id="7d29c-163">Oltre ad archiviare gli output di un'attività, è possibile archiviare gli output associato a un intero processo.</span><span class="sxs-lookup"><span data-stu-id="7d29c-163">In addition to storing task outputs, you can store the outputs associated with an entire job.</span></span> <span data-ttu-id="7d29c-164">Ad esempio, nell'attività di unione di un processo di rendering di un filmato, è possibile salvare in modo permanente l'intero filmato sottoposto a rendering come output del processo.</span><span class="sxs-lookup"><span data-stu-id="7d29c-164">For example, in the merge task of a movie rendering job, you could persist the fully rendered movie as a job output.</span></span> <span data-ttu-id="7d29c-165">Una volta completato il processo, l'applicazione client può elencare e recuperare gli output del processo senza dover eseguire query sulle singole attività.</span><span class="sxs-lookup"><span data-stu-id="7d29c-165">When your job is completed, your client application can list and retrieve the outputs for the job, and does not need to query the individual tasks.</span></span>

<span data-ttu-id="7d29c-166">Per archiviare l'output del processo, chiamare il metodo [JobOutputStorage][net_joboutputstorage].[SaveAsync][net_joboutputstorage_saveasync] e specificare [JobOutputKind][net_joboutputkind] e il nome file:</span><span class="sxs-lookup"><span data-stu-id="7d29c-166">Store job output by calling the [JobOutputStorage][net_joboutputstorage].[SaveAsync][net_joboutputstorage_saveasync] method, and specify the [JobOutputKind][net_joboutputkind] and filename:</span></span>

```csharp
CloudJob job = new JobOutputStorage(acct, jobId);
JobOutputStorage jobOutputStorage = job.OutputStorage(linkedStorageAccount);

await jobOutputStorage.SaveAsync(JobOutputKind.JobOutput, "mymovie.mp4");
await jobOutputStorage.SaveAsync(JobOutputKind.JobPreview, "mymovie_preview.mp4");
```

<span data-ttu-id="7d29c-167">Come con il tipo **TaskOutputKind** per gli output di un'attività, usare il tipo [JobOutputKind][net_joboutputkind] per categorizzare i file persistenti di un processo.</span><span class="sxs-lookup"><span data-stu-id="7d29c-167">As with the **TaskOutputKind** type for task outputs, you use the [JobOutputKind][net_joboutputkind] type to categorize a job's persisted files.</span></span> <span data-ttu-id="7d29c-168">Questo parametro consente di eseguire query in seguito, per ottenere l'elenco di un tipo specifico di output.</span><span class="sxs-lookup"><span data-stu-id="7d29c-168">This parameter allows you to later query for (list) a specific type of output.</span></span> <span data-ttu-id="7d29c-169">Il tipo **JobOutputKind** include sia categorie di output che di anteprima e supporta la creazione di categorie personalizzate.</span><span class="sxs-lookup"><span data-stu-id="7d29c-169">The **JobOutputKind** type includes both output and preview categories, and supports creating custom categories.</span></span>

### <a name="store-task-logs"></a><span data-ttu-id="7d29c-170">Archiviare i log delle attività</span><span class="sxs-lookup"><span data-stu-id="7d29c-170">Store task logs</span></span>

<span data-ttu-id="7d29c-171">Oltre a rendere persistente un file in una risorsa di archiviazione permanente quando un'attività o un processo viene completato, può essere necessario rendere persistenti i file aggiornati durante l'esecuzione di un'attività, ad esempio i file di log o `stdout.txt` e `stderr.txt`.</span><span class="sxs-lookup"><span data-stu-id="7d29c-171">In addition to persisting a file to durable storage when a task or job completes, you may need to persist files that are updated during the execution of a task &mdash; log files or `stdout.txt` and `stderr.txt`, for example.</span></span> <span data-ttu-id="7d29c-172">A questo scopo, nella libreria Azure Batch File Conventions è disponibile il metodo [TaskOutputStorage][net_taskoutputstorage].[SaveTrackedAsync][net_savetrackedasync].</span><span class="sxs-lookup"><span data-stu-id="7d29c-172">For this purpose, the Azure Batch File Conventions library provides the [TaskOutputStorage][net_taskoutputstorage].[SaveTrackedAsync][net_savetrackedasync] method.</span></span> <span data-ttu-id="7d29c-173">Con [SaveTrackedAsync][net_savetrackedasync] è possibile tenere traccia degli aggiornamenti a un file nel nodo (in base a un intervallo specificato) e salvare in modo permanente gli aggiornamenti in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7d29c-173">With [SaveTrackedAsync][net_savetrackedasync], you can track updates to a file on the node (at an interval that you specify) and persist those updates to Azure Storage.</span></span>

<span data-ttu-id="7d29c-174">Nel frammento di codice seguente viene usato [SaveTrackedAsync][net_savetrackedasync] per aggiornare `stdout.txt` in Archiviazione di Azure ogni 15 secondi durante l'esecuzione dell'attività:</span><span class="sxs-lookup"><span data-stu-id="7d29c-174">In the following code snippet, we use [SaveTrackedAsync][net_savetrackedasync] to update `stdout.txt` in Azure Storage every 15 seconds during the execution of the task:</span></span>

```csharp
TimeSpan stdoutFlushDelay = TimeSpan.FromSeconds(3);
string logFilePath = Path.Combine(
    Environment.GetEnvironmentVariable("AZ_BATCH_TASK_DIR"), "stdout.txt");

// The primary task logic is wrapped in a using statement that sends updates to
// the stdout.txt blob in Storage every 15 seconds while the task code runs.
using (ITrackedSaveOperation stdout =
        await taskStorage.SaveTrackedAsync(
        TaskOutputKind.TaskLog,
        logFilePath,
        "stdout.txt",
        TimeSpan.FromSeconds(15)))
{
    /* Code to process data and produce output file(s) */

    // We are tracking the disk file to save our standard output, but the
    // node agent may take up to 3 seconds to flush the stdout stream to
    // disk. So give the file a moment to catch up.
     await Task.Delay(stdoutFlushDelay);
}
```

<span data-ttu-id="7d29c-175">La sezione impostata come commento `Code to process data and produce output file(s)` è un segnaposto per il codice eseguito normalmente da un'attività.</span><span class="sxs-lookup"><span data-stu-id="7d29c-175">The commented section `Code to process data and produce output file(s)` is a placeholder for the code that your task would normally perform.</span></span> <span data-ttu-id="7d29c-176">Ad esempio, potrebbe essere disponibile codice che scarica i dati da Archiviazione di Azure ed esegue un calcolo o una trasformazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="7d29c-176">For example, you might have code that downloads data from Azure Storage and performs transformation or calculation on it.</span></span> <span data-ttu-id="7d29c-177">Questo frammento di codice è importante perché dimostra come è possibile eseguire il wrapping di tale codice in un blocco `using` per aggiornare periodicamente un file con [SaveTrackedAsync][net_savetrackedasync].</span><span class="sxs-lookup"><span data-stu-id="7d29c-177">The important part of this snippet is demonstrating how you can wrap such code in a `using` block to periodically update a file with [SaveTrackedAsync][net_savetrackedasync].</span></span>

<span data-ttu-id="7d29c-178">L'agente del nodo è un programma in esecuzione in ogni nodo del pool e fornisce l'interfaccia di comando e controllo tra il nodo e il servizio Batch.</span><span class="sxs-lookup"><span data-stu-id="7d29c-178">The node agent is a program that runs on each node in the pool and provides the command-and-control interface between the node and the Batch service.</span></span> <span data-ttu-id="7d29c-179">La chiamata `Task.Delay` è necessaria alla fine di questo blocco `using` per garantire che l'agente del nodo abbia tempo sufficiente per scaricare il contenuto dell'output standard nel file stdout.txt nel nodo.</span><span class="sxs-lookup"><span data-stu-id="7d29c-179">The `Task.Delay` call is required at the end of this `using` block to ensure that the node agent has time to flush the contents of standard out to the stdout.txt file on the node.</span></span> <span data-ttu-id="7d29c-180">Senza questo ritardo, è possibile perdere gli ultimi secondi dell'output.</span><span class="sxs-lookup"><span data-stu-id="7d29c-180">Without this delay, it is possible to miss the last few seconds of output.</span></span> <span data-ttu-id="7d29c-181">Questo ritardo potrebbe non essere necessario per tutti i file.</span><span class="sxs-lookup"><span data-stu-id="7d29c-181">This delay may not be required for all files.</span></span>

> [!NOTE]
> <span data-ttu-id="7d29c-182">Quando si abilita il rilevamento file con **SaveTrackedAsync**, solo le *aggiunte* al file rilevato vengono rese persistenti in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7d29c-182">When you enable file tracking with **SaveTrackedAsync**, only *appends* to the tracked file are persisted to Azure Storage.</span></span> <span data-ttu-id="7d29c-183">Usare questo metodo solo per il rilevamento dei file di log non a rotazione o altri file in cui le scritture vengono eseguite con operazioni di aggiunta alla fine del file.</span><span class="sxs-lookup"><span data-stu-id="7d29c-183">Use this method only for tracking non-rotating log files or other files that are written to with append operations to the end of the file.</span></span>
> 
> 

## <a name="retrieve-output-data"></a><span data-ttu-id="7d29c-184">Recuperare i dati di output</span><span class="sxs-lookup"><span data-stu-id="7d29c-184">Retrieve output data</span></span>

<span data-ttu-id="7d29c-185">Quando si recupera l'output salvato in modo permanente con la libreria Azure Batch File Conventions, si esegue questa operazione con un approccio incentrato su attività e processo.</span><span class="sxs-lookup"><span data-stu-id="7d29c-185">When you retrieve your persisted output using the Azure Batch File Conventions library, you do so in a task- and job-centric manner.</span></span> <span data-ttu-id="7d29c-186">È possibile richiedere l'output per un'attività o un processo specifico senza dover conoscere il percorso in Archiviazione di Azure, né il nome di file.</span><span class="sxs-lookup"><span data-stu-id="7d29c-186">You can request the output for given task or job without needing to know its path in Azure Storage, or even its file name.</span></span> <span data-ttu-id="7d29c-187">In alternativa, è possibile richiedere i file di output in base all'ID dell'attività o del processo.</span><span class="sxs-lookup"><span data-stu-id="7d29c-187">Instead, you can request output files by task or job ID.</span></span>

<span data-ttu-id="7d29c-188">Il frammento di codice seguente esegue l'iterazione delle attività di un processo, stampa alcune informazioni sui file di output per l'attività e quindi scarica i file dalla risorsa di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7d29c-188">The following code snippet iterates through a job's tasks, prints some information about the output files for the task, and then downloads its files from Storage.</span></span>

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

## <a name="view-output-files-in-the-azure-portal"></a><span data-ttu-id="7d29c-189">Visualizzare i file di output nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="7d29c-189">View output files in the Azure portal</span></span>

<span data-ttu-id="7d29c-190">Il portale di Azure visualizza gli output e i log di un'attività resi persistenti in un account di archiviazione di Azure collegato usando lo [standard Batch File Conventions](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span><span class="sxs-lookup"><span data-stu-id="7d29c-190">The Azure portal displays task output files and logs that are persisted to a linked Azure Storage account using the [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span></span> <span data-ttu-id="7d29c-191">È possibile implementare queste convenzioni nel linguaggio preferito o usare la libreria File Conventions nelle applicazioni .NET.</span><span class="sxs-lookup"><span data-stu-id="7d29c-191">You can implement these conventions yourself in the a language of your choice, or you can use the File Conventions library in your .NET applications.</span></span>

<span data-ttu-id="7d29c-192">Per abilitare la visualizzazione dei file di output nel portale, è necessario soddisfare i requisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="7d29c-192">To enable the display of your output files in the portal, you must satisfy the following requirements:</span></span>

1. <span data-ttu-id="7d29c-193">[Collegare un account di archiviazione di Azure](#requirement-linked-storage-account) all'account Batch.</span><span class="sxs-lookup"><span data-stu-id="7d29c-193">[Link an Azure Storage account](#requirement-linked-storage-account) to your Batch account.</span></span>
2. <span data-ttu-id="7d29c-194">Rispettare le convenzioni di denominazione predefinite per i contenitori di archiviazione e i file durante il salvataggio in modo permanente degli output.</span><span class="sxs-lookup"><span data-stu-id="7d29c-194">Adhere to the predefined naming conventions for Storage containers and files when persisting outputs.</span></span> <span data-ttu-id="7d29c-195">È possibile trovare la definizione di queste convenzioni nel file [LEGGIMI][github_file_conventions_readme] della libreria File Conventions.</span><span class="sxs-lookup"><span data-stu-id="7d29c-195">You can find the definition of these conventions in the File Conventions library [README][github_file_conventions_readme].</span></span> <span data-ttu-id="7d29c-196">Se si usa la libreria [Azure Batch File Conventions][nuget_package] per rendere persistente l'output, i file vengono resi persistenti in base allo standard File Conventions.</span><span class="sxs-lookup"><span data-stu-id="7d29c-196">If you use the [Azure Batch File Conventions][nuget_package] library to persist your output, your files are persisted according to the File Conventions standard.</span></span>

<span data-ttu-id="7d29c-197">Per visualizzare i file di output delle attività e i log nel portale di Azure, passare all'attività di cui si vuole visualizzare l'output, quindi fare clic su **File di output salvati** o **Log salvati**.</span><span class="sxs-lookup"><span data-stu-id="7d29c-197">To view task output files and logs in the Azure portal, navigate to the task whose output you are interested in, then click either **Saved output files** or **Saved logs**.</span></span> <span data-ttu-id="7d29c-198">L'immagine illustra l'opzione **ile di output salvato** per l'attività con ID "007":</span><span class="sxs-lookup"><span data-stu-id="7d29c-198">This image shows the **Saved output files** for the task with ID "007":</span></span>

<span data-ttu-id="7d29c-199">![Pannello dei file di output delle attività nel portale di Azure][2]</span><span class="sxs-lookup"><span data-stu-id="7d29c-199">![Task outputs blade in the Azure portal][2]</span></span>

## <a name="code-sample"></a><span data-ttu-id="7d29c-200">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="7d29c-200">Code sample</span></span>

<span data-ttu-id="7d29c-201">Il progetto di esempio [PersistOutputs][github_persistoutputs] è uno degli [esempi di codice di Azure Batch][github_samples] disponibili in GitHub.</span><span class="sxs-lookup"><span data-stu-id="7d29c-201">The [PersistOutputs][github_persistoutputs] sample project is one of the [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="7d29c-202">Questa soluzione di Visual Studio descrive come usare la libreria Azure Batch File Conventions per salvare in modo permanente l'output dell'attività in una risorsa di archiviazione permanente.</span><span class="sxs-lookup"><span data-stu-id="7d29c-202">This Visual Studio solution demonstrates how to use the Azure Batch File Conventions library to persist task output to durable storage.</span></span> <span data-ttu-id="7d29c-203">Per eseguire l'esempio, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="7d29c-203">To run the sample, follow these steps:</span></span>

1. <span data-ttu-id="7d29c-204">Aprire il progetto in **Visual Studio 2015 o in una versione più recente**.</span><span class="sxs-lookup"><span data-stu-id="7d29c-204">Open the project in **Visual Studio 2015 or newer**.</span></span>
2. <span data-ttu-id="7d29c-205">Aggiungere **le credenziali dell'account** di archiviazione e Batch a **AccountSettings.settings** nel progetto Microsoft.Azure.Batch.Samples.Common.</span><span class="sxs-lookup"><span data-stu-id="7d29c-205">Add your Batch and Storage **account credentials** to **AccountSettings.settings** in the Microsoft.Azure.Batch.Samples.Common project.</span></span>
3. <span data-ttu-id="7d29c-206">**Compilare** , ma non eseguire, la soluzione.</span><span class="sxs-lookup"><span data-stu-id="7d29c-206">**Build** (but do not run) the solution.</span></span> <span data-ttu-id="7d29c-207">Se richiesto, ripristinare tutti i pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="7d29c-207">Restore any NuGet packages if prompted.</span></span>
4. <span data-ttu-id="7d29c-208">Usare il portale di Azure per caricare un [pacchetto dell'applicazione](batch-application-packages.md) per **PersistOutputsTask**.</span><span class="sxs-lookup"><span data-stu-id="7d29c-208">Use the Azure portal to upload an [application package](batch-application-packages.md) for **PersistOutputsTask**.</span></span> <span data-ttu-id="7d29c-209">Includere `PersistOutputsTask.exe` e relativi assembly dipendenti nel pacchetto ZIP, impostare l'ID applicazione su "PersistOutputsTask" e la versione del pacchetto dell'applicazione su "1.0".</span><span class="sxs-lookup"><span data-stu-id="7d29c-209">Include the `PersistOutputsTask.exe` and its dependent assemblies in the .zip package, set the application ID to "PersistOutputsTask", and the application package version to "1.0".</span></span>
5. <span data-ttu-id="7d29c-210">**Avviare**, ovvero eseguire, il progetto **PersistOutputs**.</span><span class="sxs-lookup"><span data-stu-id="7d29c-210">**Start** (run) the **PersistOutputs** project.</span></span>
6. <span data-ttu-id="7d29c-211">Quando viene richiesto di scegliere la tecnologia di persistenza da usare per l'esecuzione dell'esempio, immettere **1** per eseguire l'esempio con la libreria File Conventions per rendere persistente l'output dell'attività.</span><span class="sxs-lookup"><span data-stu-id="7d29c-211">When prompted to choose the persistence technology to use for running the sample, enter **1** to run the sample using the File Conventions library to persist task output.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="7d29c-212">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7d29c-212">Next steps</span></span>

### <a name="get-the-batch-file-conventions-library-for-net"></a><span data-ttu-id="7d29c-213">Ottenere la libreria Batch File Conventions per .NET</span><span class="sxs-lookup"><span data-stu-id="7d29c-213">Get the Batch File Conventions library for .NET</span></span>

<span data-ttu-id="7d29c-214">La libreria Batch File Conventions per .NET è disponibile in [NuGet][nuget_package].</span><span class="sxs-lookup"><span data-stu-id="7d29c-214">The Batch File Conventions library for .NET is available on [NuGet][nuget_package].</span></span> <span data-ttu-id="7d29c-215">La libreria estende le classi [CloudJob][net_cloudjob] e [CloudTask][net_cloudtask] con nuovi metodi.</span><span class="sxs-lookup"><span data-stu-id="7d29c-215">The library extends the [CloudJob][net_cloudjob] and [CloudTask][net_cloudtask] classes with new methods.</span></span> <span data-ttu-id="7d29c-216">Vedere anche la [documentazione di riferimento](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) per la libreria File Conventions.</span><span class="sxs-lookup"><span data-stu-id="7d29c-216">Also see the [reference documentation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) for the File Conventions library.</span></span>

<span data-ttu-id="7d29c-217">Il [codice sorgente][github_file_conventions] per la libreria File Conventions è disponibile in GitHub nel repository Microsoft Azure SDK per .NET.</span><span class="sxs-lookup"><span data-stu-id="7d29c-217">The [source code][github_file_conventions] for the File Conventions library is available on GitHub in the Microsoft Azure SDK for .NET repository.</span></span> 

### <a name="explore-other-approaches-for-persisting-output-data"></a><span data-ttu-id="7d29c-218">Esplorare altri approcci per rendere persistenti i dati di output</span><span class="sxs-lookup"><span data-stu-id="7d29c-218">Explore other approaches for persisting output data</span></span>

- <span data-ttu-id="7d29c-219">Per una panoramica delle opzioni per rendere persistenti i dati di processi e attività, vedere [Rendere persistente l'output di processi e attività](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="7d29c-219">See [Persist job and task output to Azure Storage](batch-task-output.md) for an overview of persisting task and job data.</span></span>
- <span data-ttu-id="7d29c-220">Vedere [Rendere persistenti i dati di attività in Archiviazione di Azure con l'API del servizio Batch](batch-task-output-files.md) per scoprire come usare l'API del servizio Batch per rendere persistenti i dati di output.</span><span class="sxs-lookup"><span data-stu-id="7d29c-220">See [Persist task data to Azure Storage with the Batch service API](batch-task-output-files.md) to learn how to use the Batch service API to persist output data.</span></span>

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
[2]: ./media/batch-task-output/task-output-02.png "Pannello dei file di output delle attività nel portale di Azure"
