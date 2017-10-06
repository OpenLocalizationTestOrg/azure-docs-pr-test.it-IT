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
# <a name="persist-job-and-task-data-tooazure-storage-with-hello-batch-file-conventions-library-for-net-toopersist"></a>Processo di persistenza e dati tooAzure archiviazione con libreria di hello convenzioni dei File Batch per .NET toopersist di attività 

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

Dati dell'attività toopersist unidirezionale sono hello toouse [libreria convenzioni File Batch di Azure per .NET][nuget_package]. libreria convenzioni File Hello semplifica il processo di hello di output dell'attività di archiviazione dati tooAzure, archiviazione e del suo recupero. È possibile utilizzare hello convenzioni File libreria nel codice di attività sia client &mdash; nel codice dell'attività per salvare in modo permanente i file e nel client toolist del codice e recuperarli. Il codice di attività può usare anche output di hello libreria tooretrieve hello di attività upstream, ad esempio un [le relazioni tra attività](batch-task-dependencies.md) scenario. 

tooretrieve file alla libreria di hello convenzioni dei File di output, è possibile individuare il file hello per un determinato processo o un'attività elencandoli dall'ID e lo scopo. Non è necessario tooknow hello nomi o percorsi di file hello. Ad esempio, utilizzare toolist libreria di hello convenzioni dei File di tutti i file intermedi per una determinata attività oppure ottenere un file di anteprima per un determinato processo.

> [!TIP]
> A partire dalla versione 2017-05-01, hello API del servizio Batch supporta persistenti output dati tooAzure archiviazione per le attività e le attività di gestione processo eseguite sul pool creati con la configurazione della macchina virtuale hello. API del servizio Batch Hello fornisce toopersist un modo semplice l'output di codice che crea un'attività e funge da una libreria di convenzioni di File alternativo toohello hello. È possibile modificare l'output di toopersist Batch applicazioni client senza la necessità di un'applicazione hello tooupdate che l'attività è in esecuzione. Per ulteriori informazioni, vedere [mantenere i dati di attività tooAzure archiviazione con l'API del servizio Batch hello](batch-task-output-files.md).
> 
> 

## <a name="when-do-i-use-hello-file-conventions-library-toopersist-task-output"></a>Utilizzo di output di hello convenzioni dei File della libreria toopersist attività

Azure Batch offre più di un metodo toopersist l'output dell'attività. Hello convenzioni dei File è migliori scenari toothese appropriato:

- È possibile modificare facilmente codice hello per un'applicazione hello che l'attività è in esecuzione file toopersist utilizzando libreria convenzioni File hello.
- Si desidera toostream dati tooAzure archiviazione mentre l'attività hello è ancora in esecuzione.
- Si desidera toopersist dati dal pool creati con la configurazione di macchina virtuale hello o della configurazione del servizio cloud hello.
- L'applicazione client o altre attività in hello processi toolocate esigenze e scaricare i file di output di attività per ID o in base allo scopo. 
- Desideri che l'output dell'attività tooview in hello portale di Azure.

Se lo scenario è diverso da quelli elencati in precedenza, potrebbe essere tooconsider un approccio diverso. Per ulteriori informazioni sulle altre opzioni per salvare in modo permanente l'output dell'attività, vedere [Persist processi e delle attività di output tooAzure archiviazione](batch-task-output.md). 

## <a name="what-is-hello-batch-file-conventions-standard"></a>Che cos'è hello convenzioni dei File Batch standard?

Hello [standard convenzioni dei File Batch](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) fornisce uno schema di denominazione per i contenitori di destinazione hello e toowhich percorsi blob vengono scritti i file di output. File persistente tooAzure archiviazione conformi toohello convenzioni dei File standard sono automaticamente disponibili per la visualizzazione in hello portale di Azure. portale di Hello è a conoscenza di convenzione di denominazione hello e pertanto possa visualizzare i file che rispettano tooit.

libreria di convenzioni per i File Hello per .NET denomina automaticamente i contenitori di archiviazione e i file di output di attività in base toohello convenzioni dei File standard. libreria convenzioni File Hello fornisce anche metodi tooquery di file di output in archiviazione di Azure in base toojob ID, ID attività o scopo.   

Se si sviluppa con un linguaggio diverso da .NET, è possibile implementare manualmente il standard convenzioni File hello nell'applicazione. Per ulteriori informazioni, vedere [sullo standard di convenzioni per i File Batch hello](batch-task-output.md#about-the-batch-file-conventions-standard).

## <a name="link-an-azure-storage-account-tooyour-batch-account"></a>Collegare un tooyour di account di archiviazione di Azure account Batch

toopersist dati di output tooAzure archiviazione utilizzando hello convenzioni File libreria, è innanzitutto necessario collegare un tooyour di account di archiviazione di Azure account Batch. Se non è già fatto, è possibile collegare un tooyour di account di archiviazione account Batch utilizzando hello [portale di Azure](https://portal.azure.com):

1. Passare l'account Batch tooyour in hello portale di Azure. 
2. In **Impostazioni** selezionare **Account di archiviazione**.
3. Se non è già disponibile un account di archiviazione associato all'account Batch, fare clic su **Account di archiviazione (nessuno)**.
4. Selezionare un account di archiviazione dall'elenco di hello per la sottoscrizione. Per prestazioni ottimali, utilizzare un account di archiviazione di Azure in hello stessa area hello account Batch in cui si eseguono le attività.

## <a name="persist-output-data"></a>Rendere persistenti i dati di output

attività e processi toopersist dati con libreria di hello convenzioni dei File di output, creare un contenitore di archiviazione di Azure, quindi salvare contenitore toohello output di hello. Hello utilizzare [libreria client di archiviazione di Azure per .NET](https://www.nuget.org/packages/WindowsAzure.Storage) nel contenitore di attività codice tooupload hello attività output toohello. 

Per altre informazioni sull'uso di contenitori e BLOB in Archiviazione di Azure, vedere [Introduzione all'archiviazione BLOB di Azure con .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).

> [!WARNING]
> Tutti gli output di attività e processi persistenti con hello convenzioni relative ai File archiviati nella libreria hello stesso contenitore. Se un numero elevato di attività Cerca toopersist file hello stesso tempo, [archiviazione limitazioni](../storage/common/storage-performance-checklist.md#blobs) può essere applicata.
> 
> 

### <a name="create-storage-container"></a>Creare un contenitore di archiviazione

toopersist attività output tooAzure archiviazione, prima di creare un contenitore chiamando [CloudJob][net_cloudjob].[ PrepareOutputStorageAsync][net_prepareoutputasync]. Questo metodo di estensione accetta un oggetto [CloudStorageAccount] [ net_cloudstorageaccount] come parametro. Viene creato un contenitore denominato in base toohello File convenzioni standard, in modo che il suo contenuto possono essere individuato dagli hello Azure portal e hello i metodi di recupero descritti più avanti in articolo hello.

È in genere inserire toocreate codice hello un contenitore nell'applicazione client &mdash; hello applicazione che crea il pool di processi e attività.

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

### <a name="store-task-outputs"></a>Archiviare gli output delle attività

Ora che è stata preparata un contenitore di archiviazione di Azure, le attività è possono salvare toohello contenitore dell'output usando hello [TaskOutputStorage] [ net_taskoutputstorage] trovare la classe nella libreria convenzioni File hello.

Nel codice di attività, creare innanzitutto un [TaskOutputStorage] [ net_taskoutputstorage] dell'oggetto, quindi quando l'attività hello del completamento dell'operazione, chiamare hello [TaskOutputStorage] [ net_taskoutputstorage]. [SaveAsync] [ net_saveasync] toosave metodo relativo tooAzure output archiviazione.

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

Hello `kind` parametro di hello [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[ SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) metodo classifica hello file persistente. Esistono quattro tipi [TaskOutputKind][net_taskoutputkind] predefiniti: `TaskOutput`, `TaskPreview`, `TaskLog` e `TaskIntermediate.` È anche possibile definire categorie personalizzate di output.

Questi tipi di output consentono toospecify quale tipo di output toolist quando si eseguono query in un secondo momento Batch per hello persistenti gli output di un'attività specifica. In altre parole, quando si elencano gli output di hello per un'attività, è possibile filtrare l'elenco di hello in uno dei tipi di output di hello. Ad esempio, "trarne vantaggio hello *anteprima* per attività di output *109*." Altre informazioni sulla visualizzazione e recupero di output viene visualizzato [recuperare l'output](#retrieve-output) successive dell'articolo hello.

> [!TIP]
> Hello il tipo di output determina inoltre in hello Azure in cui viene visualizzato un determinato file portale: *TaskOutput*-suddiviso in categorie i file vengono visualizzati in **i file di output dell'attività**, e *TaskLog*i file vengono visualizzati in **attività registri**.
> 
> 

### <a name="store-job-outputs"></a>Archiviare gli output del processo

Inoltre genera toostoring attività, è possibile archiviare gli output di hello associati a un intero processo. Nell'attività di unione hello di un processo di rendering del filmato, ad esempio, si potrebbe persistere film hello completamente il rendering come output un processo. Al termine dell'esecuzione del processo, l'applicazione client è possibile elencare e recuperare l'output di hello per processo hello e non necessario tooquery hello singole attività.

Archiviare l'output del processo dalla chiamata hello [JobOutputStorage][net_joboutputstorage].[ SaveAsync] [ net_joboutputstorage_saveasync] (metodo) e specificare hello [JobOutputKind] [ net_joboutputkind] e il nome file:

```csharp
CloudJob job = new JobOutputStorage(acct, jobId);
JobOutputStorage jobOutputStorage = job.OutputStorage(linkedStorageAccount);

await jobOutputStorage.SaveAsync(JobOutputKind.JobOutput, "mymovie.mp4");
await jobOutputStorage.SaveAsync(JobOutputKind.JobPreview, "mymovie_preview.mp4");
```

Come con hello **TaskOutputKind** tipo per l'output di un'attività, utilizzare hello [JobOutputKind] [ net_joboutputkind] toocategorize tipo un processo del persistenti i file. Questo parametro consente query toolater per un tipo specifico di output (elenco). Hello **JobOutputKind** tipo include categorie output e di anteprima e supporta la creazione di categorie personalizzate.

### <a name="store-task-logs"></a>Archiviare i log delle attività

Inoltre toopersisting un'archiviazione toodurable file quando un'attività o un processo viene completato, potrebbe essere necessario toopersist file aggiornati durante l'esecuzione di un'attività di hello &mdash; i file di log o `stdout.txt` e `stderr.txt`, ad esempio. A tale scopo, la libreria di Azure Batch File convenzioni hello fornisce hello [TaskOutputStorage][net_taskoutputstorage].[ SaveTrackedAsync] [ net_savetrackedasync] metodo. Con [SaveTrackedAsync][net_savetrackedasync], è possibile tenere traccia di file tooa degli aggiornamenti nel nodo hello (in un intervallo specificato) e rendere persistenti tali tooAzure aggiornamenti archiviazione.

Nel seguente frammento di codice di hello, utilizziamo [SaveTrackedAsync] [ net_savetrackedasync] tooupdate `stdout.txt` in archiviazione di Azure ogni 15 secondi, durante l'esecuzione di hello dell'attività hello:

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

Hello commentato sezione `Code tooprocess data and produce output file(s)` è un segnaposto per il codice hello eseguirebbe in genere l'attività. Ad esempio, potrebbe essere disponibile codice che scarica i dati da Archiviazione di Azure ed esegue un calcolo o una trasformazione dei dati. aspetto importante di questo frammento di codice Hello è illustrare come è possibile eseguire il wrapping tale codice in un `using` tooperiodically blocco aggiornare un file con [SaveTrackedAsync][net_savetrackedasync].

agente nodo Hello è un programma che viene eseguito in ogni nodo nel pool di hello e fornisce l'interfaccia di comando e controllo hello tra nodo hello e il servizio Batch hello. Hello `Task.Delay` è necessaria alla fine di hello di questa chiamata `using` tooensure di blocco che hello agente nodo dispone di contenuto di hello tooflush ora dello standard toohello stdout.txt file nel nodo hello. Senza questo ritardo, è possibile toomiss hello ultimi secondi dell'output. Questo ritardo potrebbe non essere necessario per tutti i file.

> [!NOTE]
> Quando si abilita il file di rilevamento con **SaveTrackedAsync**, solo *aggiunge* toohello rilevati file sono persistenti tooAzure archiviazione. Utilizzare questo metodo solo per la registrazione non rotazione dei file di log o altri file che vengono scritti toowith aggiungere fine toohello operazioni del file hello.
> 
> 

## <a name="retrieve-output-data"></a>Recuperare i dati di output

Quando si recupera l'output persistente utilizzando hello Azure convenzioni dei File Batch libreria, non in modo basato su attività e a processo. È possibile richiedere hello di output per attività o il processo senza la necessità di tooknow il relativo percorso di archiviazione di Azure o anche il nome del file. In alternativa, è possibile richiedere i file di output in base all'ID dell'attività o del processo.

Hello frammento di codice seguente scorre le attività di un processo, stampa alcune informazioni sui file di output di hello per attività hello e quindi scarica i file dall'archiviazione.

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

## <a name="view-output-files-in-hello-azure-portal"></a>Visualizzare i file di output in hello portale di Azure

Hello portale di Azure consente di visualizzare i file di output di attività e i log dei tooa persistente collegati account di archiviazione di Azure utilizzando hello [standard convenzioni dei File Batch](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). È possibile implementare queste convenzioni in un linguaggio di propria scelta hello oppure è possibile utilizzare raccolta convenzioni File hello nelle applicazioni .NET.

visualizzazione di hello tooenable dei file di output nel portale di hello, è necessario soddisfare hello seguenti requisiti:

1. [Collegare un account di archiviazione di Azure](#requirement-linked-storage-account) tooyour account Batch.
2. Rispettare le convenzioni di denominazione toohello predefinito per i contenitori di archiviazione e i file durante il salvataggio di output. È possibile trovare la definizione di hello di queste convenzioni nella libreria convenzioni File hello [Leggimi][github_file_conventions_readme]. Se si utilizza hello [convenzioni File Batch di Azure] [ nuget_package] libreria toopersist l'output, i file sono persistenti in base toohello convenzioni dei File standard.

l'output dell'attività tooview file e viene registrato in hello portale di Azure, passare toohello attività il cui output si è interessati, quindi fare clic su **i file di output salvato** o **registri salvati**. La seguente immagine illustra hello **i file di output salvato** per attività hello con ID "007":

![Nel portale di Azure hello pannello risultati delle attività][2]

## <a name="code-sample"></a>Esempio di codice

Hello [PersistOutputs] [ github_persistoutputs] progetto di esempio è uno dei hello [esempi di codice di Azure Batch] [ github_samples] su GitHub. Questa soluzione di Visual Studio viene illustrato come dell'output dell'archiviazione toodurable toouse hello Azure convenzioni dei File Batch libreria toopersist attività. hello toorun di esempio, seguire questi passaggi:

1. Progetto aperto hello in **Visual Studio 2015 o versione successiva**.
2. Aggiungere il Batch e l'archiviazione **delle credenziali dell'account** troppo**AccountSettings.settings** nel progetto Microsoft.Azure.Batch.Samples.Common hello.
3. **Compilare** (ma non le eseguono) hello soluzione. Se richiesto, ripristinare tutti i pacchetti NuGet.
4. Hello utilizzare tooupload portale Azure un [pacchetto di applicazione](batch-application-packages.md) per **PersistOutputsTask**. Includere hello `PersistOutputsTask.exe` e i relativi assembly dipendenti nel pacchetto ZIP hello, set di ID dell'applicazione hello troppo "PersistOutputsTask" e un'applicazione hello pacchetto versione troppo "1.0".
5. **Avviare** hello (esecuzione) **PersistOutputs** progetto.
6. Quando richiesto toochoose hello persistenza tecnologia toouse per esempio hello in esecuzione, immettere **1** : esempio hello toorun utilizzando l'output dell'attività toopersist libreria convenzioni File hello. 

## <a name="next-steps"></a>Passaggi successivi

### <a name="get-hello-batch-file-conventions-library-for-net"></a>Ottenere libreria di hello convenzioni dei File Batch per .NET

libreria di Hello convenzioni dei File Batch per .NET è disponibile sul [NuGet][nuget_package]. libreria Hello estende hello [CloudJob] [ net_cloudjob] e [CloudTask] [ net_cloudtask] classi con nuovi metodi. Vedere anche hello [documentazione di riferimento](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) per la libreria di convenzioni per i File hello.

Hello [codice sorgente] [ github_file_conventions] per hello convenzioni di File di libreria è disponibile su GitHub in hello Microsoft Azure SDK per il repository di .NET. 

### <a name="explore-other-approaches-for-persisting-output-data"></a>Esplorare altri approcci per rendere persistenti i dati di output

- Vedere [Persist processi e delle attività di output tooAzure archiviazione](batch-task-output.md) per una panoramica di rendere persistenti i dati di attività e processi.
- Vedere [mantenere i dati di attività tooAzure archiviazione con l'API del servizio Batch hello](batch-task-output-files.md) toolearn come toouse hello API del servizio Batch toopersist dati di output.

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
