---
title: "attività e processi aaaPersist output tooAzure archiviazione con hello API del servizio Azure Batch | Documenti Microsoft"
description: "Informazioni su come processo e attività di Batch toopersist toouse API del servizio Batch output tooAzure archiviazione."
services: batch
author: tamram
manager: timlt
editor: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: tamram
ms.openlocfilehash: 71b3f7c0dda2d2a9d8eb3eef83229873c70ca22c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="persist-task-data-tooazure-storage-with-hello-batch-service-api"></a>Mantenere i dati di attività tooAzure archiviazione con hello API del servizio Batch

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

A partire dalla versione 2017-05-01, hello API del servizio Batch supporta persistenti output dati tooAzure archiviazione per le attività e attività di processo di gestione eseguite in pool con la configurazione della macchina virtuale hello. Quando si aggiunge un'attività, è possibile specificare un contenitore di archiviazione di Azure come destinazione di hello per l'output dell'attività hello. servizio Batch Hello scrive quindi qualsiasi contenitore toothat dati di output quando hello attività è stata completata.

Un hello toousing vantaggio Batch output attività toopersist API del servizio è che non è necessaria un'applicazione hello toomodify che hello attività è in esecuzione. Al contrario, con alcune semplici modifiche tooyour applicazione client è possibile mantenere l'output dell'attività hello all'interno del codice hello Crea attività hello.   

## <a name="when-do-i-use-hello-batch-service-api-toopersist-task-output"></a>Utilizzo di output dell'attività toopersist hello API del servizio Batch

Azure Batch offre più di un metodo toopersist l'output dell'attività. Utilizzo di hello API del servizio Batch è un approccio pratico scenari adatti toothese migliori:

- Si desidera toowrite codice toopersist attività output all'interno dell'applicazione client, senza modificare l'applicazione hello che l'attività è in esecuzione.
- Si desidera toopersist output dalle attività di Batch e attività di processo di gestione nel pool creati con la configurazione della macchina virtuale hello.
- Si desidera toopersist contenitore di archiviazione di Azure tooan dell'output con un nome arbitrario.
- Che si desidera toopersist output tooan di archiviazione di Azure contenitore denominato in base toohello [standard convenzioni dei File Batch](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). 

Se lo scenario è diverso da quelli elencati in precedenza, potrebbe essere tooconsider un approccio diverso. Ad esempio, API del servizio Batch hello non attualmente supporta streaming output tooAzure archiviazione durante l'esecuzione di attività hello. toostream output, utilizzare la libreria hello convenzioni dei File Batch, disponibile per .NET. Per altre lingue, è necessario tooimplement la propria soluzione. Per ulteriori informazioni sulle altre opzioni per salvare in modo permanente l'output dell'attività, vedere [Persist processi e delle attività di output tooAzure archiviazione](batch-task-output.md). 

## <a name="create-a-container-in-azure-storage"></a>Creare un contenitore in Archiviazione di Azure

output dell'attività di toopersist tooAzure archiviazione, sarà necessario toocreate un contenitore che funge da destinazione hello per i file di output. Creare il contenitore di hello prima di eseguire l'attività, preferibilmente prima di inviare il processo. contenitore hello toocreate o utilizzare hello appropriata libreria client di archiviazione di Azure SDK. Per ulteriori informazioni sulle API di archiviazione di Azure, vedere hello [documentazione di archiviazione di Azure](https://docs.microsoft.com/azure/storage/).

Ad esempio, se si scrive l'applicazione in c#, utilizzare hello [libreria client di archiviazione di Azure per .NET](https://www.nuget.org/packages/WindowsAzure.Storage/). Hello seguente esempio viene illustrato come un contenitore toocreate:

```csharp
CloudBlobContainer container = storageAccount.CreateCloudBlobClient().GetContainerReference(containerName);
await conainer.CreateIfNotExists();
```

## <a name="get-a-shared-access-signature-for-hello-container"></a>Ottenere una firma di accesso condiviso per il contenitore di hello

Dopo aver creato il contenitore di hello, ottenere una firma di accesso condiviso (SAS) con accesso in scrittura toohello contenitore. Una firma di accesso condiviso fornisce contenitore toohello accesso delegato. Hello firma di accesso condiviso concede l'accesso con un set specificato di autorizzazioni e in un intervallo di tempo specificato. Hello servizio Batch deve una firma di accesso condiviso con il contenitore toohello output attività di scrittura autorizzazioni toowrite. Per altre informazioni sulle firme di accesso condiviso, vedere [Uso delle firme di \(accesso condiviso\) in Archiviazione di Azure](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

Quando si otterrà una firma di accesso condiviso utilizzando le API di archiviazione di Azure hello, hello API restituisce una stringa di token di firma di accesso condiviso. Questa stringa di token include tutti i parametri di hello SAS, tra cui autorizzazioni hello e intervallo di hello in cui hello firma di accesso condiviso è valida. toouse hello SAS tooaccess un contenitore di archiviazione di Azure, è necessario tooappend hello SAS stringa token toohello URI della risorsa. Hello URI risorsa, insieme a hello aggiunto token SAS, fornisce l'accesso autenticato tooAzure archiviazione.

Hello esempio seguente viene illustrato come la stringa per il contenitore di hello del token tooget una SAS di sola scrittura, quindi aggiunge l'URI del contenitore toohello hello SAS:

```csharp
string containerSasToken = container.GetSharedAccessSignature(new SharedAccessBlobPolicy()
{
    SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddDays(1),
    Permissions = SharedAccessBlobPermissions.Write
});

string containerSasUrl = container.Uri.AbsoluteUri + containerSasToken; 
```

## <a name="specify-output-files-for-task-output"></a>Specificare i file di output per l'output dell'attività

file di output toospecify per un'attività, creare una raccolta di [OutputFile](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfile) oggetti e assegnarla toohello [CloudTask.OutputFiles](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudtask.outputfiles#Microsoft_Azure_Batch_CloudTask_OutputFiles) proprietà quando si crea l'attività hello. 

esempio di codice .NET Hello crea un'attività che scrive file di numeri casuali tooa denominato `output.txt`. esempio Hello crea un file di output per `output.txt` toobe scritto toohello contenitore. esempio Hello crea anche i file di output per tutti i file di log che corrispondono a criterio file hello `std*.txt` (_ad esempio_, `stdout.txt` e `stderr.txt`). URL del contenitore Hello richiede hello associazioni di sicurezza che è stato creato in precedenza per il contenitore di hello. Hello servizio Batch Usa contenitore toohello di hello SAS tooauthenticate accesso: 

```csharp
new CloudTask(taskId, "cmd /v:ON /c \"echo off && set && (FOR /L %i IN (1,1,100000) DO (ECHO !RANDOM!)) > output.txt\"")
{
    OutputFiles = new List<OutputFile>
    {
        new OutputFile(
            filePattern: @"..\std*.txt",
            destination: new OutputFileDestination(
         new OutputFileBlobContainerDestination(
                    containerUrl: containerSasUrl,
                    path: taskId)),
            uploadOptions: new OutputFileUploadOptions(
            uploadCondition: OutputFileUploadCondition.TaskCompletion)),
        new OutputFile(
            filePattern: @"output.txt",
            destination: 
         new OutputFileDestination(new OutputFileBlobContainerDestination(
                    containerUrl: containerSasUrl,
                    path: taskId + @"\output.txt")),
            uploadOptions: new OutputFileUploadOptions(
            uploadCondition: OutputFileUploadCondition.TaskCompletion)),
}
```

### <a name="specify-a-file-pattern-for-matching"></a>Specificare un modello di file per la corrispondenza

Quando si specifica un file di output, è possibile utilizzare hello [OutputFile.FilePattern](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfile.filepattern#Microsoft_Azure_Batch_OutputFile_FilePattern) toospecify proprietà un modello di file per la corrispondenza. modello di file Hello potrebbe corrispondere a zero file, un singolo file o un set di file creati da attività hello.

Hello **FilePattern** proprietà supporta i caratteri jolly standard del file System, ad esempio `*` (per non ricorsivo corrisponde) e `**` (per ricorsiva corrisponde). Ad esempio, nell'esempio di codice hello precedente specifica hello file modello toomatch `std*.txt` non in modo ricorsivo: 

`filePattern: @"..\std*.txt"`

tooupload un singolo file, specificare un modello di file senza caratteri jolly. Ad esempio, nell'esempio di codice hello precedente specifica hello file modello toomatch `output.txt`:

`filePattern: @"output.txt"`

### <a name="specify-an-upload-condition"></a>Specificare una condizione di caricamento

Hello [OutputFileUploadOptions.UploadCondition](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileuploadoptions.uploadcondition#Microsoft_Azure_Batch_OutputFileUploadOptions_UploadCondition) proprietà consente di caricare condizionale dei file di output. Uno scenario comune è tooupload un insieme di file se hello attività ha esito positivo e un set di file diverso, in caso di errore. È consigliabile, ad esempio, il file di log dettagliati tooupload solo quando l'attività hello non riesce e viene terminato con un codice di uscita diverso da zero. Analogamente, è opportuno file dei risultati tooupload solo se l'attività hello ha esito positivo, come tali file potrebbero essere mancanti o incomplete se hello attività ha esito negativo.

Nell'esempio di codice sopra Hello imposta hello **UploadCondition** proprietà troppo**TaskCompletion**. Questa impostazione specifica che se il file hello è toobe caricati dopo aver completato le attività di hello, indipendentemente dal valore hello hello codice di uscita. 

`uploadCondition: OutputFileUploadCondition.TaskCompletion`

Per altre impostazioni, vedere hello [OutputFileUploadCondition](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.common.outputfileuploadcondition) enum.

### <a name="disambiguate-files-with-hello-same-name"></a>Risolvere le ambiguità nei file con hello stesso nome

attività Hello in un processo può produrre file hello con stesso nome. Ad esempio, i file `stdout.txt` e `stderr.txt` vengono creati per ogni attività eseguita in un processo. Poiché ogni attività viene eseguita in un contesto specifico, questi file non siano in conflitto nel file system di hello nodo. Tuttavia, quando si caricano file dal contenitore di condivisi di più attività tooa, è necessario il file toodisambiguate con hello stesso nome.

Hello [OutputFileBlobContainerDestination.Path](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileblobcontainerdestination.path#Microsoft_Azure_Batch_OutputFileBlobContainerDestination_Path) proprietà specifica il blob di destinazione hello o la directory virtuale per file di output. È possibile utilizzare hello **percorso** blob hello tooname di proprietà o la directory virtuale in modo che i file di output con hello stesso nome sono denominati in modo univoco in archiviazione di Azure. Usando un ID di attività hello in percorso hello è un nome univoco di tooensure efficace e identificare facilmente i file.

Se hello **FilePattern** tooa espressione con caratteri jolly è impostata, quindi tutti i file che corrispondono a hello criterio sono caricati toohello directory virtuale specificata da hello **percorso** proprietà. Ad esempio, se hello contenitore è `mycontainer`, attività hello ID `mytask`, e il modello di file hello è `..\std*.txt`, quindi hello assoluto URI toohello di file di output in archiviazione di Azure sarà simile a:

```
https://myaccount.blob.core.windows.net/mycontainer/mytask/stderr.txt
https://myaccount.blob.core.windows.net/mycontainer/mytask/stdout.txt
```

Se hello **FilePattern** proprietà set toomatch un singolo nome file, quindi non contiene caratteri jolly, ovvero hello valore hello **percorso** proprietà specifica il nome di blob completo hello . Se si prevede di conflitto con un singolo file da più attività, quindi includere hello nome della directory virtuale hello come parte di toodisambiguate di nome file hello tali file. Ad esempio, set hello **percorso** ID attività hello tooinclude di proprietà, il carattere delimitatore hello (in genere una barra rovesciata) e nome del file hello:

`path: taskId + @"/output.txt"`

Hello assoluto URI toohello i file di output per un set di attività sarà simili a:

```
https://myaccount.blob.core.windows.net/mycontainer/task1/output.txt
https://myaccount.blob.core.windows.net/mycontainer/task2/output.txt
```

Per ulteriori informazioni sulle directory virtuali in archiviazione di Azure, vedere [elencare i BLOB hello in un contenitore](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container).


## <a name="diagnose-file-upload-errors"></a>Diagnosticare gli errori di caricamento file

Se l'output di caricamento file ha esito negativo archiviazione tooAzure, quindi attività hello Sposta toohello **completato** lo stato e hello [TaskExecutionInformation.FailureInformation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.taskexecutioninformation.failureinformation#Microsoft_Azure_Batch_TaskExecutionInformation_FailureInformation) proprietà è impostata. Esaminare hello **FailureInformation** toodetermine proprietà sul tipo di errore. Di seguito è ad esempio, un errore che si verifica al momento del caricamento di file non è possibile trovare il contenitore di hello: 

```
Category: UserError
Code: FileUploadContainerNotFound
Message: One of hello specified Azure container(s) was not found while attempting tooupload an output file
```

In ogni caricamento di file, scrive due log del nodo di calcolo toohello file, Batch `fileuploadout.txt` e `fileuploaderr.txt`. È possibile esaminare questi toolearn i file di log altre informazioni sull'errore specifico. Nei casi in cui il caricamento di file hello mai tentativo, ad esempio perché non è stato possibile eseguire l'attività hello stessa, quindi questi file di log non esiste.

## <a name="diagnose-file-upload-performance"></a>Diagnosticare le prestazioni di caricamento file

Hello `fileuploadout.txt` file registra lo stato di caricamento. È possibile esaminare questo toolearn file richiede ulteriori informazioni su quanto tempo consente di caricare il file. Tenere presente che esistono molti fattori delle prestazioni tooupload, comprese le dimensioni di hello del nodo di hello, altre attività nel nodo hello in fase di hello di caricamento di hello, se un contenitore di destinazione hello in hello pool Batch hello stessa area, il numero di nodi è caricamento account di archiviazione toohello in hello stesso tempo e così via.

## <a name="use-hello-batch-service-api-with-hello-batch-file-conventions-standard"></a>Utilizzare l'API del servizio Batch hello con hello convenzioni dei File Batch standard

Quando si mantiene fissa l'output dell'attività con hello API del servizio Batch, è possibile assegnare un nome del contenitore di destinazione e tuttavia si desidera che i BLOB. È anche possibile scegliere tooname loro in base toohello [standard convenzioni dei File Batch](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). standard convenzioni File Hello determina i nomi di hello del contenitore di destinazione hello e blob in archiviazione di Azure per un file di output specificata in base ai nomi di hello del processo di hello e attività. Se si utilizza hello convenzioni dei File standard per la denominazione dei file di output, quindi i file di output sono disponibili per la visualizzazione in hello [portale di Azure](https://portal.azure.com).

Se si sviluppa in c#, è possibile utilizzare i metodi di hello incorporati hello [libreria convenzioni dei File Batch per .NET](https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files). Questa libreria crea hello denominate in modo corretto i contenitori e percorsi blob per l'utente. Ad esempio, è possibile chiamare API hello tooget hello il nome corretto per il contenitore di hello, in base al nome di processo hello:

```csharp
string containerName = job.OutputStorageContainerName();
```

È possibile utilizzare hello [CloudJobExtensions.GetOutputStorageContainerUrl](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files.cloudjobextensions.getoutputstoragecontainerurl) metodo tooreturn un URL di accesso condiviso (firma) utilizzati toowrite toohello contenitore. È quindi possibile passare questo toohello SAS [OutputFileBlobContainerDestination](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileblobcontainerdestination) costruttore.

Se si sviluppa in un linguaggio diverso da c#, si sarà necessario standard di tooimplement hello convenzioni dei File.

## <a name="code-sample"></a>Esempio di codice

Hello [PersistOutputs] [ github_persistoutputs] progetto di esempio è uno dei hello [esempi di codice di Azure Batch] [ github_samples] su GitHub. Questa soluzione di Visual Studio viene illustrato come libreria client di toouse hello Batch per attività toopersist .NET output toodurable archiviazione. hello toorun di esempio, seguire questi passaggi:

1. Progetto aperto hello in **Visual Studio 2015 o versione successiva**.
2. Aggiungere il Batch e l'archiviazione **delle credenziali dell'account** troppo**AccountSettings.settings** nel progetto Microsoft.Azure.Batch.Samples.Common hello.
3. **Compilare** (ma non le eseguono) hello soluzione. Se richiesto, ripristinare tutti i pacchetti NuGet.
4. Hello utilizzare tooupload portale Azure un [pacchetto di applicazione](batch-application-packages.md) per **PersistOutputsTask**. Includere hello `PersistOutputsTask.exe` e i relativi assembly dipendenti nel pacchetto ZIP hello, set di ID dell'applicazione hello troppo "PersistOutputsTask" e un'applicazione hello pacchetto versione troppo "1.0".
5. **Avviare** hello (esecuzione) **PersistOutputs** progetto.
6. Quando richiesto toochoose hello persistenza tecnologia toouse per esempio hello in esecuzione, immettere **2** toorun: esempio hello usando l'output dell'attività toopersist hello API del servizio Batch.
7. Se si desidera, eseguire: esempio hello nuovamente, immettendo **3** toopersist output con l'API del servizio Batch hello e tooname hello blob e contenitore percorso di destinazione in base toohello convenzioni dei File standard.

## <a name="next-steps"></a>Passaggi successivi

- Per ulteriori informazioni sul salvataggio in modo permanente l'output dell'attività con libreria convenzioni File hello per .NET, vedere [mantenere job e task tooAzure archiviazione dati con libreria di hello convenzioni dei File Batch per .NET toopersist ](batch-task-output-file-conventions.md).
- Per informazioni su altri approcci per rendere persistenti i dati di output in Batch di Azure, vedere [Persist processi e delle attività di output tooAzure archiviazione](batch-task-output.md).

[github_persistoutputs]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/PersistOutputs
[github_samples]: https://github.com/Azure/azure-batch-samples
