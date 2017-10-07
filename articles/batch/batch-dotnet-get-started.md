---
title: aaaTutorial - libreria client di utilizzare hello Azure Batch per .NET | Documenti Microsoft
description: Informazioni su concetti di base di Azure Batch hello e compilare una soluzione semplice usando .NET.
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 76cb9807-cbc1-405a-8136-d1e53e66e82b
ms.service: batch
ms.devlang: dotnet
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 06062b3886a8081bd9a831824a981503ef55f9b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-building-solutions-with-hello-batch-client-library-for-net"></a>Iniziare a creare soluzioni alla libreria client di hello Batch per .NET

> [!div class="op_single_selector"]
> * [.NET](batch-dotnet-get-started.md)
> * [Python](batch-python-tutorial.md)
> * [Node.js](batch-nodejs-get-started.md)
>
>

Nozioni di base hello di [Azure Batch] [ azure_batch] hello e [.NET per Batch] [ net_api] libreria in questo articolo come illustrato un passaggio dell'applicazione di esempio in c# da passaggio. Si esamina come applicazione di esempio hello sfrutta hello Batch servizio tooprocess un carico di lavoro parallelo in cloud hello e come essa interagisce con [di archiviazione di Azure](../storage/common/storage-introduction.md) per gestione temporanea di file e il recupero. Si illustra Batch applicazione flusso di lavoro comune e acquisire una comprensione di base dei componenti principali hello del Batch, ad esempio i processi, attività, i pool e nodi di calcolo.

![Flusso di lavoro della soluzione Batch (di base)][11]<br/>

## <a name="prerequisites"></a>Prerequisiti
Questo articolo presuppone che si sia in grado di usare C# e Visual Studio Si presuppone inoltre che si è in grado di toosatisfy hello creazione requisiti dell'account specificate di seguito per Azure e hello Batch e servizi di archiviazione.

### <a name="accounts"></a>Account
* **Account Azure**: se non si ha già una sottoscrizione di Azure, [creare un account Azure gratuito][azure_free_account].
* **Account Batch**: dopo aver creato una sottoscrizione di Azure, [creare un account Azure Batch](batch-account-create-portal.md).
* **Account di archiviazione**: vedere [Creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [Informazioni sugli account di archiviazione di Azure](../storage/common/storage-create-storage-account.md).

> [!IMPORTANT]
> Batch attualmente supporta *solo* hello **generica** tipo di account di archiviazione, come descritto nel passaggio &#5; [creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [su Azure gli account di archiviazione](../storage/common/storage-create-storage-account.md).
>
>

### <a name="visual-studio"></a>Visual Studio
È necessario disporre di **Visual Studio 2015 o versione successiva** toobuild progetto di esempio hello. È possibile trovare versioni gratuite e di valutazione di Visual Studio in hello [panoramica dei prodotti Visual Studio][visual_studio].

### <a name="dotnettutorial-code-sample"></a>*DotNetTutorial*
Hello [DotNetTutorial] [ github_dotnettutorial] esempio è uno dei molti esempi di codice di Batch, vedere hello hello [esempi di azure batch] [ github_samples] repository in GitHub. È possibile scaricare tutti gli esempi di hello facendo **Clone o download > Download ZIP** nella home page del repository hello o facendo clic su hello [azure-batch-esempi-master.zip] [ github_samples_zip]collegamento diretto. Dopo aver estratto il contenuto di hello del file ZIP hello, è possibile trovare la soluzione hello in hello seguente cartella:

`\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial`

### <a name="azure-batch-explorer-optional"></a>Azure Batch Explorer (facoltativo)
Hello [Azure Batch Explorer] [ github_batchexplorer] è un'utilità gratuita che è incluso in hello [esempi di azure batch] [ github_samples] repository in GitHub. Mentre toocomplete non necessari in questa esercitazione, può essere utile durante lo sviluppo e debug delle soluzioni di Batch.

## <a name="dotnettutorial-sample-project-overview"></a>Panoramica del progetto di esempio DotNetTutorial
Hello *DotNetTutorial* nell'esempio di codice è una soluzione di Visual Studio che è costituito da due progetti: **DotNetTutorial** e **TaskApplication**.

* **DotNetTutorial** è un'applicazione hello client che interagisce con tooexecute di servizi di archiviazione e Batch hello un carico di lavoro parallelo in nodi di calcolo (macchine virtuali). L'esempio DotNetTutorial viene eseguito nella workstation locale.
* **TaskApplication** programma hello che viene eseguito in nodi di calcolo di Azure tooperform il lavoro effettivo hello. Nell'esempio hello `TaskApplication.exe` analizza hello testo in un file scaricato dall'archiviazione di Azure (file di input di hello). Quindi, produce un file di testo (file di output di hello) che contiene un elenco di hello prime tre parole che vengono visualizzati nel file di input hello. Dopo la creazione di file di output di hello TaskApplication carica tooAzure file hello archiviazione. Questo rende l'applicazione client toohello disponibili per il download. TaskApplication viene eseguito in parallelo in più nodi di calcolo di hello servizio Batch.

Hello diagramma seguente è illustrata hello primaria le operazioni eseguite dall'applicazione client hello, *DotNetTutorial*, un'applicazione che viene eseguita dalle attività hello, hello e *TaskApplication*. Questo flusso di lavoro di base è tipico di molte soluzioni di calcolo create con Batch. Mentre non vengono visualizzati tutte le funzionalità disponibili nel servizio Batch hello, quasi ogni scenario di Batch include parti del flusso di lavoro.

![Flusso di lavoro dell'esempio di Batch][8]<br/>

[**Passaggio 1.**](#step-1-create-storage-containers) Creare **contenitori** nell'archivio BLOB di Azure.<br/>
[**Passaggio 2.**](#step-2-upload-task-application-and-data-files) Caricare i file dell'applicazione di attività e i file di input toocontainers.<br/>
[**Passaggio 3.**](#step-3-create-batch-pool) Creare un **pool** di Batch.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**3a.** Hello pool **StartTask** download hello toonodes (TaskApplication) i file binari di attività che si connettono pool hello.<br/>
[**Passaggio 4.**](#step-4-create-batch-job) Creare un **processo** di Batch.<br/>
[**Passaggio 5.**](#step-5-add-tasks-to-job) Aggiungere **attività** toohello processo.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**5a.** attività di Hello sono tooexecute pianificati sui nodi.<br/>
    &nbsp;&nbsp;&nbsp;&nbsp;**5b.** Ogni attività scarica i rispettivi dati di input da Archiviazione di Azure e quindi avvia l'esecuzione.<br/>
[**Passaggio 6.**](#step-6-monitor-tasks) Monitorare le attività.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**6a.** Come vengono completate, caricamento del loro tooAzure di dati di output archiviazione.<br/>
[**Passaggio 7.**](#step-7-download-task-output) Scaricare l'output delle attività dal servizio di archiviazione.

Come indicato, non tutte le soluzioni di Batch consente di eseguire questi passaggi esatti e possono includere molte altre ancora, ma hello *DotNetTutorial* applicazione di esempio illustra i processi comuni in una soluzione di Batch.

## <a name="build-hello-dotnettutorial-sample-project"></a>Compilare hello *DotNetTutorial* progetto di esempio
Prima di eseguire correttamente l'esempio hello, è necessario specificare le credenziali dell'account Batch e l'archiviazione sia in hello *DotNetTutorial* del progetto `Program.cs` file. Se non è già stato fatto, aprire la soluzione hello in Visual Studio facendo doppio clic su hello `DotNetTutorial.sln` file della soluzione. O aprirlo da Visual Studio utilizzando hello **File > Apri > progetto/soluzione** menu.

Aprire `Program.cs` all'interno di hello *DotNetTutorial* progetto. Quindi aggiungere le credenziali specificate superiore hello del file hello:

```csharp
// Update hello Batch and Storage account credential strings below with hello values
// unique tooyour accounts. These are used when constructing connection strings
// for hello Batch and Storage client objects.

// Batch account credentials
private const string BatchAccountName = "";
private const string BatchAccountKey  = "";
private const string BatchAccountUrl  = "";

// Storage account credentials
private const string StorageAccountName = "";
private const string StorageAccountKey  = "";
```

> [!IMPORTANT]
> Come indicato in precedenza, attualmente non è necessario specificare le credenziali di hello per un **generica** account di archiviazione in archiviazione di Azure. Le applicazioni di Batch utilizzano spazio di archiviazione blob hello **generica** account di archiviazione. Non specificare le credenziali di hello per un account di archiviazione che è stata creata tramite la selezione hello *nell'archiviazione Blob* tipo di account.
>
>

È possibile trovare le credenziali dell'account Batch e l'archiviazione all'interno di blade account hello di ogni servizio in hello [portale di Azure][azure_portal]:

![Batch credenziali nel portale di hello][9]
![le credenziali di archiviazione nel portale di hello][10]<br/>

Ora che è stato aggiornato il progetto di hello con le credenziali, fare doppio clic hello soluzione in Esplora soluzioni e fare clic su **Compila soluzione**. Confermare l'operazione di ripristino di hello di tutti i pacchetti NuGet, se richiesto.

> [!TIP]
> Se non vengono ripristinati automaticamente i pacchetti di NuGet hello o se vengono visualizzati errori sui pacchetti di hello toorestore errore, assicurarsi di aver hello [Gestione pacchetti NuGet] [ nuget_packagemgr] installato. Quindi, abilitare il download di hello di pacchetti mancanti. Vedere [abilitazione pacchetto ripristinare durante la compilazione] [ nuget_restore] tooenable download del pacchetto.
>
>

Hello le sezioni seguenti, è suddividere l'applicazione di esempio hello in passaggi hello tooprocess viene eseguito un carico di lavoro nel servizio Batch hello e discutere i passaggi descritti in dettaglio. Si consiglia di toorefer toohello Apri soluzione in Visual Studio mentre si lavora in modo tramite rest hello di questo articolo, poiché non ogni riga di codice nell'esempio hello è descritto.

Passare toohello cima hello `MainAsync` metodo hello *DotNetTutorial* del progetto `Program.cs` file toostart con il passaggio 1. Ogni passaggio seguito quindi approssimativamente segue hello progressione del metodo viene chiamato `MainAsync`.

## <a name="step-1-create-storage-containers"></a>Passaggio 1: Creare contenitori di archiviazione
![Creare contenitori in Archiviazione di Azure][1]
<br/>

Batch include il supporto predefinito per l'interazione con Archiviazione di Azure. I contenitori nell'account di archiviazione offrono file hello necessari per le attività di hello eseguite nell'account di Batch. i contenitori di Hello offrono anche un posizionamento toostore hello output di dati che producono attività hello. in primo luogo Hello hello *DotNetTutorial* applicazione client è creare tre contenitori in [archiviazione Blob di Azure](../storage/common/storage-introduction.md):

* **applicazione**: questo contenitore verranno archiviati applicazione hello eseguita dall'attività hello, nonché le relative dipendenze, ad esempio le DLL.
* **input**: attività scaricherà tooprocess i file di dati hello dal hello *input* contenitore.
* **output**: al termine dell'elaborazione del file di input di attività, verrà caricato hello risultati toohello *output* contenitore.

In ordine toointeract con uno spazio di archiviazione account e creare contenitori, utilizziamo hello [Azure Storage Client Library per .NET][net_api_storage]. Si crea un account toohello di riferimento con [CloudStorageAccount][net_cloudstorageaccount]e da cui creare un [CloudBlobClient][net_cloudblobclient]:

```csharp
// Construct hello Storage account connection string
string storageConnectionString = String.Format(
    "DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}",
    StorageAccountName,
    StorageAccountKey);

// Retrieve hello storage account
CloudStorageAccount storageAccount =
    CloudStorageAccount.Parse(storageConnectionString);

// Create hello blob client, for use in obtaining references to
// blob storage containers
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```

Utilizziamo hello `blobClient` fare riferimento in un'applicazione hello e passarlo come parametro tooseveral metodi. Un esempio è nel blocco di codice hello che segue immediatamente hello precedente, in cui è stato chiamato `CreateContainerIfNotExistAsync` tooactually creare contenitori di hello.

```csharp
// Use hello blob client toocreate hello containers in Azure Storage if they don't
// yet exist
const string appContainerName    = "application";
const string inputContainerName  = "input";
const string outputContainerName = "output";
await CreateContainerIfNotExistAsync(blobClient, appContainerName);
await CreateContainerIfNotExistAsync(blobClient, inputContainerName);
await CreateContainerIfNotExistAsync(blobClient, outputContainerName);
```

```csharp
private static async Task CreateContainerIfNotExistAsync(
    CloudBlobClient blobClient,
    string containerName)
{
        CloudBlobContainer container =
            blobClient.GetContainerReference(containerName);

        if (await container.CreateIfNotExistsAsync())
        {
                Console.WriteLine("Container [{0}] created.", containerName);
        }
        else
        {
                Console.WriteLine("Container [{0}] exists, skipping creation.",
                    containerName);
        }
}
```

Dopo avere creati i contenitori di hello, un'applicazione hello ora possibile caricare file hello che verranno utilizzati dalle attività hello.

> [!TIP]
> [Come archiviazione di Blob da .NET toouse](../storage/blobs/storage-dotnet-how-to-use-blobs.md) fornisce una buona panoramica dell'utilizzo di BLOB e contenitori di archiviazione di Azure. Quando si inizia a batch deve essere superiore hello dell'elenco di lettura.
>
>

## <a name="step-2-upload-task-application-and-data-files"></a>Passaggio 2: Caricare l'applicazione dell'attività e i file di dati
![Attività di caricamento dell'applicazione e di input (dati) file toocontainers][2]
<br/>

Nel file hello caricare operazione *DotNetTutorial* prima definisce le raccolte di **applicazione** e **input** percorsi di file in cui si trovano sul computer locale hello. Carica quindi questi contenitori toohello file creato nel passaggio precedente hello.

```csharp
// Paths toohello executable and its dependencies that will be executed by hello tasks
List<string> applicationFilePaths = new List<string>
{
    // hello DotNetTutorial project includes a project reference tooTaskApplication,
    // allowing us toodetermine hello path of hello task application binary dynamically
    typeof(TaskApplication.Program).Assembly.Location,
    "Microsoft.WindowsAzure.Storage.dll"
};

// hello collection of data files that are toobe processed by hello tasks
List<string> inputFilePaths = new List<string>
{
    @"..\..\taskdata1.txt",
    @"..\..\taskdata2.txt",
    @"..\..\taskdata3.txt"
};

// Upload hello application and its dependencies tooAzure Storage. This is the
// application that will process hello data files, and will be executed by each
// of hello tasks on hello compute nodes.
List<ResourceFile> applicationFiles = await UploadFilesToContainerAsync(
    blobClient,
    appContainerName,
    applicationFilePaths);

// Upload hello data files. This is hello data that will be processed by each of
// hello tasks that are executed on hello compute nodes within hello pool.
List<ResourceFile> inputFiles = await UploadFilesToContainerAsync(
    blobClient,
    inputContainerName,
    inputFilePaths);
```

Esistono due metodi in `Program.cs` che sono coinvolti nel processo di caricamento hello:

* `UploadFilesToContainerAsync`: Questo metodo restituisce una raccolta di [ResourceFile] [ net_resourcefile] oggetti (come descritti di seguito) e internamente chiamate `UploadFileToContainerAsync` tooupload ogni file che è passato in hello *filePaths* parametro.
* `UploadFileToContainerAsync`: Questo è il metodo hello che effettivamente esegue il caricamento di file hello e crea hello [ResourceFile] [ net_resourcefile] oggetti. Dopo aver caricato il file hello, ottiene una firma di accesso condiviso (SAS) per il file hello e restituisce un oggetto ResourceFile che lo rappresenta. Più avanti vengono illustrate anche le firme di accesso condiviso.

```csharp
private static async Task<ResourceFile> UploadFileToContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string filePath)
{
        Console.WriteLine(
            "Uploading file {0} toocontainer [{1}]...", filePath, containerName);

        string blobName = Path.GetFileName(filePath);

        CloudBlobContainer container = blobClient.GetContainerReference(containerName);
        CloudBlockBlob blobData = container.GetBlockBlobReference(blobName);
        await blobData.UploadFromFileAsync(filePath);

        // Set hello expiry time and permissions for hello blob shared access signature.
        // In this case, no start time is specified, so hello shared access signature
        // becomes valid immediately
        SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy
        {
                SharedAccessExpiryTime = DateTime.UtcNow.AddHours(2),
                Permissions = SharedAccessBlobPermissions.Read
        };

        // Construct hello SAS URL for blob
        string sasBlobToken = blobData.GetSharedAccessSignature(sasConstraints);
        string blobSasUri = String.Format("{0}{1}", blobData.Uri, sasBlobToken);

        return new ResourceFile(blobSasUri, blobName);
}
```

### <a name="resourcefiles"></a>ResourceFiles
Oggetto [ResourceFile] [ net_resourcefile] fornisce operazioni in Batch con file di tooa URL hello in archiviazione di Azure che viene scaricato tooa nodo di calcolo prima di tale attività è in esecuzione. Hello [ResourceFile.BlobSource] [ net_resourcefile_blobsource] proprietà specifica hello URL completo del file hello presenti in archiviazione di Azure. Hello URL può includere una firma di accesso condiviso (SAS) che fornisce l'accesso sicuro toohello file. Una proprietà *ResourceFiles* è inclusa nella maggior parte dei tipi di attività in Batch .NET, ad esempio:

* [CloudTask][net_task]
* [StartTask][net_pool_starttask]
* [JobPreparationTask][net_jobpreptask]
* [JobReleaseTask][net_jobreltask]

Hello DotNetTutorial l'applicazione di esempio non utilizza hello JobPreparationTask o JobReleaseTask tipi di attività, ma è possibile leggere informazioni su di essi in [attività Esegui processo di preparazione e completamento del Batch di Azure i nodi di calcolo](batch-job-prep-release.md).

### <a name="shared-access-signature-sas"></a>Firma di accesso condiviso
Accesso condiviso, le firme sono stringhe che, quando incluse come parte di un URL, fornire accesso sicuro toocontainers e BLOB in archiviazione di Azure. Hello DotNetTutorial applicazione vengono utilizzati entrambi blob e contenitore gli URL di firma di accesso condiviso, viene illustrato come accedere stringhe firma tooobtain questi condiviso dal servizio di archiviazione hello.

* **Firme di accesso condiviso di BLOB**: StartTask del pool di hello in DotNetTutorial utilizza le firme di accesso condiviso di blob durante il download dei file binari dell'applicazione hello e i file di dati di input dall'archivio (vedere il # passaggio 3 riportato di seguito). Hello `UploadFileToContainerAsync` del DotNetTutorial metodo `Program.cs` contiene codice hello che ottiene la firma di accesso condiviso del blob ogni. L'operazione viene eseguita chiamando [CloudBlob.GetSharedAccessSignature][net_sas_blob].
* **Firme di accesso condiviso contenitore**: come le operazioni sul nodo di calcolo hello al termine di ogni attività, viene caricato il toohello di file di output *output* contenitore di archiviazione di Azure. toodo in tal caso, TaskApplication utilizza una firma di accesso condiviso di contenitore che fornisce l'accesso in scrittura toohello contenitore come parte del percorso di hello quando viene caricato il file hello. Firma di accesso condiviso di ottenere hello contenitore viene eseguita in modo simile come quando i blob hello ottenere firma di accesso condiviso. DotNetTutorial, si noterà che hello `GetContainerSasUrl` chiamate al metodo helper [Cloudblobcontainer] [ net_sas_container] toodo in modo. È possibile leggere informazioni sull'utilizzo di contenitore hello TaskApplication condiviso di firma di accesso in "passaggio 6: attività di monitoraggio."

> [!TIP]
> Check-out di serie in due parti hello sulle firme di accesso condiviso, [parte 1: hello comprensione condiviso il modello di firma di accesso](../storage/common/storage-dotnet-shared-access-signature-part-1.md) e [parte 2: creare e usare una firma di accesso condiviso (SAS) con archiviazione Blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn ulteriori informazioni su come fornire accesso sicuro toodata nell'account di archiviazione.
>
>

## <a name="step-3-create-batch-pool"></a>Passaggio 3: Creare un pool di Batch
![Creare un pool di Batch][3]
<br/>

Un **pool** di Batch è una raccolta di nodi di calcolo (macchine virtuali) in cui Batch esegue le attività di un processo.

Dopo il caricamento di un'applicazione hello e i file di dati toohello account di archiviazione con le API di archiviazione di Azure, *DotNetTutorial* inizia effettua chiamate toohello Batch servizio con le API fornite dalla libreria .NET di Batch hello. Hello codice crea prima una [BatchClient][net_batchclient]:

```csharp
BatchSharedKeyCredentials cred = new BatchSharedKeyCredentials(
    BatchAccountUrl,
    BatchAccountName,
    BatchAccountKey);

using (BatchClient batchClient = BatchClient.Open(cred))
{
    ...
```

Successivamente, esempio hello crea un pool di nodi di calcolo nell'account di Batch hello con una chiamata troppo`CreatePoolIfNotExistsAsync`. `CreatePoolIfNotExistsAsync`Usa hello [BatchClient.PoolOperations.CreatePool] [ net_pool_create] metodo toocreate un nuovo pool di hello servizio Batch:

```csharp
private static async Task CreatePoolIfNotExistAsync(BatchClient batchClient, string poolId, IList<ResourceFile> resourceFiles)
{
    CloudPool pool = null;
    try
    {
        Console.WriteLine("Creating pool [{0}]...", poolId);

        // Create hello unbound pool. Until we call CloudPool.Commit() or CommitAsync(), no pool is actually created in the
        // Batch service. This CloudPool instance is therefore considered "unbound," and we can modify its properties.
        pool = batchClient.PoolOperations.CreatePool(
            poolId: poolId,
            targetDedicatedComputeNodes: 3,                                             // 3 compute nodes
            virtualMachineSize: "small",                                                // single-core, 1.75 GB memory, 225 GB disk
            cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));   // Windows Server 2012 R2

        // Create and assign hello StartTask that will be executed when compute nodes join hello pool.
        // In this case, we copy hello StartTask's resource files (that will be automatically downloaded
        // toohello node by hello StartTask) into hello shared directory that all tasks will have access to.
        pool.StartTask = new StartTask
        {
            // Specify a command line for hello StartTask that copies hello task application files toothe
            // node's shared directory. Every compute node in a Batch pool is configured with a number
            // of pre-defined environment variables that can be referenced by commands or applications
            // run by tasks.

            // Since a successful execution of robocopy can return a non-zero exit code (e.g. 1 when one or
            // more files were successfully copied) we need toomanually exit with a 0 for Batch toorecognize
            // StartTask execution success.
            CommandLine = "cmd /c (robocopy %AZ_BATCH_TASK_WORKING_DIR% %AZ_BATCH_NODE_SHARED_DIR%) ^& IF %ERRORLEVEL% LEQ 1 exit 0",
            ResourceFiles = resourceFiles,
            WaitForSuccess = true
        };

        await pool.CommitAsync();
    }
    catch (BatchException be)
    {
        // Swallow hello specific error code PoolExists since that is expected if hello pool already exists
        if (be.RequestInformation?.BatchError != null && be.RequestInformation.BatchError.Code == BatchErrorCodeStrings.PoolExists)
        {
            Console.WriteLine("hello pool {0} already existed when we tried toocreate it", poolId);
        }
        else
        {
            throw; // Any other exception is unexpected
        }
    }
}
```

Quando si crea un pool con [CreatePool][net_pool_create], specificare diversi parametri, ad esempio il numero di hello di nodi di calcolo, hello [dimensioni dei nodi hello](../cloud-services/cloud-services-sizes-specs.md), e hello operativo dei nodi System. In *DotNetTutorial*, utilizziamo [CloudServiceConfiguration] [ net_cloudserviceconfiguration] toospecify Windows Server 2012 R2 da [servizi Cloud](../cloud-services/cloud-services-guestos-update-matrix.md). 

È anche possibile creare pool di nodi di calcolo che sono macchine virtuali di Azure (VM) specificando hello [VirtualMachineConfiguration] [ net_virtualmachineconfiguration] per il pool. È possibile creare un pool di nodi di calcolo di tipo VM da immagini Windows o [Linux](batch-linux-nodes.md). origine Hello per le immagini di macchina virtuale possono essere:

- Hello [macchine virtuali di Azure Marketplace][vm_marketplace], che fornisce le immagini di Windows e Linux che sono pronti all'uso. 
- Un'immagine personalizzata preparata e fornita dall'utente. Per informazioni dettagliate sulle immagini personalizzate, vedere [Sviluppare soluzioni di calcolo parallele su larga scala con Batch](batch-api-basics.md#pool).

> [!IMPORTANT]
> Vengono effettuati addebiti per le risorse di calcolo in Batch. toominimize costi, è possibile abbassare `targetDedicatedComputeNodes` too1 prima di eseguire l'esempio hello.
>
>

Con queste proprietà del nodo fisico, è inoltre possibile specificare un [StartTask] [ net_pool_starttask] per pool hello. Hello StartTask viene eseguito in ogni nodo come nodo aggiunto pool hello e ogni volta che un nodo viene riavviato. Hello StartTask è particolarmente utile per l'installazione di applicazioni in esecuzione precedente toohello nodi di calcolo delle attività. Se, ad esempio, le attività di elaborano i dati utilizzando gli script Python, è possibile utilizzare un tooinstall StartTask Python sui nodi di calcolo hello.

In questa applicazione di esempio, hello StartTask copia i file hello scaricati dall'archiviazione (che vengono specificati usando hello [StartTask][net_starttask].[ ResourceFiles] [ net_starttask_resourcefiles] proprietà) dalla cartella condivisa di hello StartTask lavoro directory toohello che *tutti* accessibili alle attività in esecuzione nel nodo hello. In pratica, questa copia `TaskApplication.exe` e relativo toohello dipendenze directory condivise su ciascun nodo come nodo hello join pool hello, in modo che qualsiasi attività che vengono eseguite sul nodo hello può accedervi.

> [!TIP]
> Hello **pacchetti di applicazioni** funzionalità di Batch di Azure fornisce un altro modo tooget l'applicazione nei nodi di calcolo hello in un pool. Vedere [distribuire applicazioni toocompute nodi con i pacchetti di applicazione di Batch](batch-application-packages.md) per informazioni dettagliate.
>
>

Inoltre rilevanti nel frammento di codice hello sopra sono utilizzare hello due variabili di ambiente nell'hello *CommandLine* proprietà di hello StartTask: `%AZ_BATCH_TASK_WORKING_DIR%` e `%AZ_BATCH_NODE_SHARED_DIR%`. Ogni nodo di calcolo all'interno di un Batch viene configurato automaticamente con alcune variabili di ambiente sono tooBatch specifico. Qualsiasi processo che viene eseguita da un'attività con le variabili di ambiente toothese di accesso.

> [!TIP]
> toofind ulteriori informazioni sulle variabili di ambiente hello sono disponibili nei nodi di calcolo in un pool di Batch e informazioni sulla directory di lavoro attività, vedere hello [impostazioni di ambiente per l'attività](batch-api-basics.md#environment-settings-for-tasks) e [file e directory ](batch-api-basics.md#files-and-directories) sezioni hello [Cenni preliminari sulla funzionalità di Batch per gli sviluppatori](batch-api-basics.md).
>
>

## <a name="step-4-create-batch-job"></a>Passaggio 4: Creare un processo di Batch
![Creare un processo di Batch][4]<br/>

Un **processo** di Batch è una raccolta di attività ed è associato a un pool di nodi di calcolo. attività Hello in un processo eseguito sui nodi di calcolo del pool di hello associata.

È possibile utilizzare un processo non solo per l'organizzazione e il rilevamento di attività nei carichi di lavoro correlati, ma anche per l'imposizione di determinati vincoli, ad esempio hello di esecuzione massimo per il processo di hello (e, di conseguenza, le relative attività) nonché la priorità del processo nei processi tooother relazione in hello Batch account. In questo esempio, tuttavia, viene associato solo a pool hello creato nel passaggio &#3; processo hello. Non vengono configurate proprietà aggiuntive.

Tutti i processi di Batch sono associati a un pool specifico. Questa associazione indica i nodi che eseguirà l'attività del processo di hello in. Specificare tramite hello [CloudJob.PoolInformation] [ net_job_poolinfo] proprietà, come illustrato nel frammento di codice hello riportato di seguito.

```csharp
private static async Task CreateJobAsync(
    BatchClient batchClient,
    string jobId,
    string poolId)
{
    Console.WriteLine("Creating job [{0}]...", jobId);

    CloudJob job = batchClient.JobOperations.CreateJob();
    job.Id = jobId;
    job.PoolInformation = new PoolInformation { PoolId = poolId };

    await job.CommitAsync();
}
```

Ora che è stato creato un processo, le attività vengono aggiunti lavoro hello tooperform.

## <a name="step-5-add-tasks-toojob"></a>Passaggio 5: Aggiungere attività toojob
![Aggiungere attività toojob][5]<br/>
*(1) processo toohello sono state aggiunte le attività, le attività di hello (2) sono pianificati toorun nei nodi e attività hello (3) scaricare tooprocess i file di dati hello*

Batch **attività** sono nodi di calcolo hello singole unità di lavoro che vengono eseguite sullo hello. Un'attività dispone di una riga di comando ed esegue gli script hello o file eseguibili specificati in questa riga di comando.

tooactually eseguire lavoro, è necessario aggiungere attività tooa processo. Ogni [CloudTask] [ net_task] viene configurata con una proprietà della riga di comando e [ResourceFiles] [ net_task_resourcefiles] (come StartTask del pool di hello) che attività Hello Scarica nodo toohello prima che la riga di comando viene eseguita automaticamente. In hello *DotNetTutorial* progetto di esempio, ogni attività elabora un solo file. Di conseguenza, la rispettiva raccolta ResourceFiles contiene un singolo elemento.

```csharp
private static async Task<List<CloudTask>> AddTasksAsync(
    BatchClient batchClient,
    string jobId,
    List<ResourceFile> inputFiles,
    string outputContainerSasUrl)
{
    Console.WriteLine("Adding {0} tasks toojob [{1}]...", inputFiles.Count, jobId);

    // Create a collection toohold hello tasks that we'll be adding toohello job
    List<CloudTask> tasks = new List<CloudTask>();

    // Create each of hello tasks. Because we copied hello task application toothe
    // node's shared directory with hello pool's StartTask, we can access it via
    // hello shared directory on hello node that hello task runs on.
    foreach (ResourceFile inputFile in inputFiles)
    {
        string taskId = "topNtask" + inputFiles.IndexOf(inputFile);
        string taskCommandLine = String.Format(
            "cmd /c %AZ_BATCH_NODE_SHARED_DIR%\\TaskApplication.exe {0} 3 \"{1}\"",
            inputFile.FilePath,
            outputContainerSasUrl);

        CloudTask task = new CloudTask(taskId, taskCommandLine);
        task.ResourceFiles = new List<ResourceFile> { inputFile };
        tasks.Add(task);
    }

    // Add hello tasks as a collection, as opposed tooissuing a separate AddTask call
    // for each. Bulk task submission helps tooensure efficient underlying API calls
    // toohello Batch service.
    await batchClient.JobOperations.AddTaskAsync(jobId, tasks);

    return tasks;
}
```

> [!IMPORTANT]
> Quando accedono a variabili di ambiente, ad esempio `%AZ_BATCH_NODE_SHARED_DIR%` o eseguire un'applicazione non trovata nel nodo di hello `PATH`, righe di comando dell'attività devono essere precedute dai `cmd /c`. In modo esplicito verrà eseguire interprete dei comandi hello e fare in modo che tooterminate dopo aver eseguito il comando. Questo requisito non è necessario se un'applicazione di esecuzione delle attività nel nodo di hello `PATH` (ad esempio *robocopy.exe* o *powershell.exe*) e non le variabili di ambiente vengono utilizzate.
>
>

All'interno di hello `foreach` ciclo nel frammento di codice hello precedente, è possibile vedere che la riga di comando hello per attività hello viene costruita in modo che i tre argomenti della riga di comando vengono passati troppo*TaskApplication.exe*:

1. Hello **primo argomento** percorso hello di tooprocess file hello. Si tratta di file toohello percorso locale di hello quanto sia presente nel nodo hello. Quando hello oggetto ResourceFile `UploadFileToContainerAsync` creazione sopra, nome del file hello è stato utilizzato per questa proprietà (come costruttore ResourceFile toohello parametro). Ciò indica che file hello è reperibile in hello stessa directory come *TaskApplication.exe*.
2. Hello **secondo argomento** specifica che la parte superiore di hello *N* parole devono essere scritti i file di output toohello. Nell'esempio hello, questo livello di codice in modo che i tre parole hello superiore vengono scritti i file di output toohello.
3. Hello **terzo argomento** firma di accesso condiviso hello (SAS) che fornisce l'accesso in scrittura toohello **output** contenitore di archiviazione di Azure. *TaskApplication.exe* vengono usati il condiviso accesso URL della firma quando carica hello output file tooAzure archiviazione. È disponibile codice hello per questo hello `UploadFileToContainer` metodo nel hello TaskApplication progetto `Program.cs` file:

```csharp
// NOTE: From project TaskApplication Program.cs

private static void UploadFileToContainer(string filePath, string containerSas)
{
        string blobName = Path.GetFileName(filePath);

        // Obtain a reference toohello container using hello SAS URI.
        CloudBlobContainer container = new CloudBlobContainer(new Uri(containerSas));

        // Upload hello file (as a new blob) toohello container
        try
        {
                CloudBlockBlob blob = container.GetBlockBlobReference(blobName);
                blob.UploadFromFile(filePath);

                Console.WriteLine("Write operation succeeded for SAS URL " + containerSas);
                Console.WriteLine();
        }
        catch (StorageException e)
        {

                Console.WriteLine("Write operation failed for SAS URL " + containerSas);
                Console.WriteLine("Additional error information: " + e.Message);
                Console.WriteLine();

                // Indicate that a failure has occurred so that when hello Batch service
                // sets hello CloudTask.ExecutionInformation.ExitCode for hello task that
                // executed this application, it properly indicates that there was a
                // problem with hello task.
                Environment.ExitCode = -1;
        }
}
```

## <a name="step-6-monitor-tasks"></a>Passaggio 6: Monitorare le attività
![Monitorare le attività][6]<br/>
*applicazione client di Hello (1) monitoraggi hello attività per il completamento e lo stato di esito positivo e (2) hello attività caricamento risultati dati tooAzure archiviazione*

Quando le attività vengono aggiunte tooa processo, vengono automaticamente in coda e pianificate per l'esecuzione nei nodi di calcolo nel pool di hello associata al processo hello. In base alle impostazioni di hello specificate, Batch gestisce tutte le attività di accodamento, la pianificazione, nuovo tentativo in corso e altre funzioni di amministrazione di attività per l'utente.

Esistono molti approcci toomonitoring l'esecuzione dell'attività. DotNetTutorial illustra un semplice esempio che segnala solo gli stati di completamento ed esito positivo o negativo dell'attività. All'interno di hello `MonitorTasks` del DotNetTutorial metodo `Program.cs`, sono disponibili tre concetti .NET per Batch che garantisca la discussione. I concetti sono elencati di seguito nell'ordine in cui appaiono:

1. **ODATADetailLevel**: specificare [ODATADetailLevel][net_odatadetaillevel] nelle operazioni di tipo elenco, come ad esempio il recupero di un elenco delle attività di un processo, è essenziale per assicurare prestazioni ottimali per l'applicazione Batch. Aggiungere [Query in modo efficiente il servizio di Azure Batch hello](batch-efficient-list-queries.md) tooyour lettura dell'elenco se prevede di eseguire una sorta di monitoraggio dello stato all'interno delle applicazioni di Batch.
2. **TaskStateMonitor**: [TaskStateMonitor][net_taskstatemonitor] fornisce alle applicazioni Batch .NET le utilità helper per monitorare gli stati delle attività. In `MonitorTasks`, *DotNetTutorial* è in attesa di tutte le attività tooreach [TaskState.Completed] [ net_taskstate] entro un limite di tempo. Quindi termina il processo di hello.
3. **TerminateJobAsync**: terminare un processo con [JobOperations.TerminateJobAsync] [ net_joboperations_terminatejob] (o hello blocco JobOperations.TerminateJob) contrassegna tale processo come completato. È essenziale toodo pertanto se la soluzione Batch utilizza un [JobReleaseTask][net_jobreltask]. un tipo speciale di attività descritto in [Attività di preparazione e completamento di processi](batch-job-prep-release.md).

Hello `MonitorTasks` metodo *DotNetTutorial*del `Program.cs` viene visualizzato sotto:

```csharp
private static async Task<bool> MonitorTasks(
    BatchClient batchClient,
    string jobId,
    TimeSpan timeout)
{
    bool allTasksSuccessful = true;
    const string successMessage = "All tasks reached state Completed.";
    const string failureMessage = "One or more tasks failed tooreach hello Completed state within hello timeout period.";

    // Obtain hello collection of tasks currently managed by hello job. Note that we use
    // a detail level too specify that only hello "id" property of each task should be
    // populated. Using a detail level for all list operations helps toolower
    // response time from hello Batch service.
    ODATADetailLevel detail = new ODATADetailLevel(selectClause: "id");
    List<CloudTask> tasks =
        await batchClient.JobOperations.ListTasks(JobId, detail).ToListAsync();

    Console.WriteLine("Awaiting task completion, timeout in {0}...",
        timeout.ToString());

    // We use a TaskStateMonitor toomonitor hello state of our tasks. In this case, we
    // will wait for all tasks tooreach hello Completed state.
    TaskStateMonitor taskStateMonitor
        = batchClient.Utilities.CreateTaskStateMonitor();

    try
    {
        await taskStateMonitor.WhenAll(tasks, TaskState.Completed, timeout);
    }
    catch (TimeoutException)
    {
        await batchClient.JobOperations.TerminateJobAsync(jobId, failureMessage);
        Console.WriteLine(failureMessage);
        return false;
    }

    await batchClient.JobOperations.TerminateJobAsync(jobId, successMessage);

    // All tasks have reached hello "Completed" state, however, this does not
    // guarantee all tasks completed successfully. Here we further check each task's
    // ExecutionInfo property tooensure that it did not encounter a failure
    // or return a non-zero exit code.

    // Update hello detail level toopopulate only hello task id and executionInfo
    // properties. We refresh hello tasks below, and need only this information for
    // each task.
    detail.SelectClause = "id, executionInfo";

    foreach (CloudTask task in tasks)
    {
        // Populate hello task's properties with hello latest info from hello Batch service
        await task.RefreshAsync(detail);

        if (task.ExecutionInformation.Result == TaskExecutionResult.Failure)
        {
            // A task with failure information set indicates there was a problem with hello task. It is important toonote that
            // hello task's state can be "Completed," yet still have encountered a failure.

            allTasksSuccessful = false;

            Console.WriteLine("WARNING: Task [{0}] encountered a failure: {1}", task.Id, task.ExecutionInformation.FailureInformation.Message);
            if (task.ExecutionInformation.ExitCode != 0)
            {
                // A non-zero exit code may indicate that hello application executed by hello task encountered an error
                // during execution. As not every application returns non-zero on failure by default (e.g. robocopy),
                // your implementation of error checking may differ from this example.

                Console.WriteLine("WARNING: Task [{0}] returned a non-zero exit code - this may indicate task execution or completion failure.", task.Id);
            }
        }
    }

    if (allTasksSuccessful)
    {
        Console.WriteLine("Success! All tasks completed successfully within hello specified timeout period.");
    }

    return allTasksSuccessful;
}
```

## <a name="step-7-download-task-output"></a>Passaggio 7: Scaricare l'output dell'attività
![Scaricare l'output delle attività dal servizio di archiviazione][7]<br/>

Hello processo una volta completato, l'output di hello di hello attività può essere scaricato dall'archiviazione di Azure. Questa operazione viene eseguita con una chiamata troppo`DownloadBlobsFromContainerAsync` in *DotNetTutorial*del `Program.cs`:

```csharp
private static async Task DownloadBlobsFromContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string directoryPath)
{
        Console.WriteLine("Downloading all files from container [{0}]...", containerName);

        // Retrieve a reference tooa previously created container
        CloudBlobContainer container = blobClient.GetContainerReference(containerName);

        // Get a flat listing of all hello block blobs in hello specified container
        foreach (IListBlobItem item in container.ListBlobs(
                    prefix: null,
                    useFlatBlobListing: true))
        {
                // Retrieve reference toohello current blob
                CloudBlob blob = (CloudBlob)item;

                // Save blob contents tooa file in hello specified folder
                string localOutputFile = Path.Combine(directoryPath, blob.Name);
                await blob.DownloadToFileAsync(localOutputFile, FileMode.Create);
        }

        Console.WriteLine("All files downloaded too{0}", directoryPath);
}
```

> [!NOTE]
> Hello chiamata troppo`DownloadBlobsFromContainerAsync` in hello *DotNetTutorial* applicazione specifica che il file hello devono essere scaricato tooyour `%TEMP%` cartella. Ritiene toomodify disponibile in questo percorso di output.
>
>

## <a name="step-8-delete-containers"></a>Passaggio 8: Eliminare i contenitori
Poiché vengono addebitati i dati che si trovano in archiviazione di Azure, è sempre un BLOB tooremove buona norma che non sono più necessari per i processi Batch. In DotNetTutorial `Program.cs`, questa operazione viene eseguita con metodo di supporto toohello tre chiamate `DeleteContainerAsync`:

```csharp
// Clean up Storage resources
await DeleteContainerAsync(blobClient, appContainerName);
await DeleteContainerAsync(blobClient, inputContainerName);
await DeleteContainerAsync(blobClient, outputContainerName);
```

metodo Hello stesso Ottiene semplicemente un contenitore di toohello di riferimento e quindi chiama [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:

```csharp
private static async Task DeleteContainerAsync(
    CloudBlobClient blobClient,
    string containerName)
{
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);

    if (await container.DeleteIfExistsAsync())
    {
        Console.WriteLine("Container [{0}] deleted.", containerName);
    }
    else
    {
        Console.WriteLine("Container [{0}] does not exist, skipping deletion.",
            containerName);
    }
}
```

## <a name="step-9-delete-hello-job-and-hello-pool"></a>Passaggio 9: Eliminare il processo di hello e pool hello
Nel passaggio finale hello, puoi toodelete richiesta hello hello e processo del pool creati dall'applicazione DotNetTutorial hello. Anche se non vengono addebitati costi per i processi e per le attività, *vengono* invece addebiti costi per i nodi di calcolo. È quindi consigliabile allocare i nodi solo in base alla necessità. L'eliminazione dei pool inutilizzati può fare parte del processo di manutenzione.

BatchClient Hello [JobOperations] [ net_joboperations] e [PoolOperations] [ net_pooloperations] dispongono di metodi di eliminazione corrispondente, ovvero se utente Hello conferma eliminazione:

```csharp
// Clean up hello resources we've created in hello Batch account if hello user so chooses
Console.WriteLine();
Console.WriteLine("Delete job? [yes] no");
string response = Console.ReadLine().ToLower();
if (response != "n" && response != "no")
{
    await batchClient.JobOperations.DeleteJobAsync(JobId);
}

Console.WriteLine("Delete pool? [yes] no");
response = Console.ReadLine();
if (response != "n" && response != "no")
{
    await batchClient.PoolOperations.DeletePoolAsync(PoolId);
}
```

> [!IMPORTANT]
> Occorre ricordare che vengono effettuati addebiti per le risorse di calcolo e che l'eliminazione di pool non usati consente di ridurre al minimo i costi. Inoltre, tenere presente che l'eliminazione di un pool Elimina tutti i nodi di calcolo all'interno di tale pool e che tutti i dati nei nodi hello sarà irreversibili dopo l'eliminazione di pool hello.
>
>

## <a name="run-hello-dotnettutorial-sample"></a>Eseguire hello *DotNetTutorial* esempio
Quando si esegue l'applicazione di esempio hello, l'output di console hello sarà simile toohello seguente. Durante l'esecuzione, si verificherà una pausa in `Awaiting task completion, timeout in 00:30:00...` mentre vengono avviati i nodi di calcolo del pool di hello. Hello utilizzare [portale di Azure] [ azure_portal] toomonitor il pool, nodi di calcolo, processi e attività durante e dopo l'esecuzione. Hello utilizzare [portale di Azure] [ azure_portal] o hello [Azure Storage Explorer] [ storage_explorers] tooview hello le risorse di archiviazione (contenitori e BLOB) che sono creato da un'applicazione hello.

Tempo di esecuzione tipico è **circa 5 minuti** quando si esegue un'applicazione hello nella configurazione predefinita.

```
Sample start: 1/8/2016 09:42:58 AM

Container [application] created.
Container [input] created.
Container [output] created.
Uploading file C:\repos\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial\bin\Debug\TaskApplication.exe toocontainer [application]...
Uploading file Microsoft.WindowsAzure.Storage.dll toocontainer [application]...
Uploading file ..\..\taskdata1.txt toocontainer [input]...
Uploading file ..\..\taskdata2.txt toocontainer [input]...
Uploading file ..\..\taskdata3.txt toocontainer [input]...
Creating pool [DotNetTutorialPool]...
Creating job [DotNetTutorialJob]...
Adding 3 tasks toojob [DotNetTutorialJob]...
Awaiting task completion, timeout in 00:30:00...
Success! All tasks completed successfully within hello specified timeout period.
Downloading all files from container [output]...
All files downloaded tooC:\Users\USERNAME\AppData\Local\Temp
Container [application] deleted.
Container [input] deleted.
Container [output] deleted.

Sample end: 1/8/2016 09:47:47 AM
Elapsed time: 00:04:48.5358142

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER tooexit...
```

## <a name="next-steps"></a>Passaggi successivi
È gratuita toomake modifiche troppo*DotNetTutorial* e *TaskApplication* tooexperiment con diversi scenari di calcolo. Ad esempio, provare ad aggiungere un ritardo di esecuzione troppo*TaskApplication*, ad esempio come con [Sleep][net_thread_sleep], le attività e monitorarli nel portale di hello toosimulate con esecuzione prolungata. Provare aggiungendo più attività o modificando il numero di hello di nodi di calcolo. Aggiungere logica toocheck per e consentire l'utilizzo di hello di un tempo di esecuzione toospeed pool esistenti (*hint*: estrarre `ArticleHelpers.cs` in hello [Microsoft.Azure.Batch.Samples.Common] [ github_samples_common] nel progetto [esempi di azure batch][github_samples]).

Ora che si ha familiarità con hello base del flusso di lavoro di una soluzione di Batch, è ora toodig in toohello funzionalità aggiuntive di hello servizio Batch.

* Hello revisione [funzionalità Panoramica di Azure Batch](batch-api-basics.md) articolo, è consigliabile se si è nuovo servizio toohello.
* Inizio nel hello altri articoli di sviluppo di Batch in **sviluppo approfondito** in hello [il percorso di apprendimento Batch][batch_learning_path].
* Estrarre un'implementazione diversa di elaborazione del carico di lavoro hello "top N parole" tramite Batch in hello [TopNWords] [ github_topnwords] esempio.
* Hello revisione .NET per Batch [note sulla versione](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) per le modifiche più recenti di hello nella libreria hello.

[azure_batch]: https://azure.microsoft.com/services/batch/
[azure_free_account]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[batch_learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[github_batchexplorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[github_dotnettutorial]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/DotNetTutorial
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_common]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/Common
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[github_topnwords]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords
[net_api]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[net_api_storage]: https://msdn.microsoft.com/library/azure/mt347887.aspx
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudblobclient]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobclient.aspx
[net_cloudblobcontainer]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.aspx
[net_cloudstorageaccount]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx
[net_cloudserviceconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudserviceconfiguration.aspx
[net_container_delete]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.deleteifexistsasync.aspx
[net_job]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_job_poolinfo]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.protocol.models.cloudjob.poolinformation.aspx
[net_joboperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.joboperations
[net_joboperations_terminatejob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.terminatejobasync.aspx
[net_jobpreptask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobpreparationtask.aspx
[net_jobreltask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobreleasetask.aspx
[net_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.aspx
[net_odatadetaillevel]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_pool_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[net_pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_pooloperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.pooloperations
[net_resourcefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.aspx
[net_resourcefile_blobsource]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.blobsource.aspx
[net_sas_blob]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblob.getsharedaccesssignature.aspx
[net_sas_container]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblobcontainer.getsharedaccesssignature.aspx
[net_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.aspx
[net_starttask_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.resourcefiles.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_task_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.resourcefiles.aspx
[net_taskstate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.taskstate.aspx
[net_taskstatemonitor]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskstatemonitor.aspx
[net_thread_sleep]: https://msdn.microsoft.com/library/274eh01d(v=vs.110).aspx
[net_virtualmachineconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.virtualmachineconfiguration.aspx
[nuget_packagemgr]: https://docs.nuget.org/consume/installing-nuget
[nuget_restore]: https://docs.nuget.org/consume/package-restore/msbuild-integrated#enabling-package-restore-during-build
[storage_explorers]: http://storageexplorer.com/
[visual_studio]: https://www.visualstudio.com/vs/
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/

[1]: ./media/batch-dotnet-get-started/batch_workflow_01_sm.png "Creare contenitori in Archiviazione di Azure"
[2]: ./media/batch-dotnet-get-started/batch_workflow_02_sm.png "Attività di caricamento dell'applicazione e di input (dati) file toocontainers"
[3]: ./media/batch-dotnet-get-started/batch_workflow_03_sm.png "Creare un pool di Batch"
[4]: ./media/batch-dotnet-get-started/batch_workflow_04_sm.png "Creare un processo di Batch"
[5]: ./media/batch-dotnet-get-started/batch_workflow_05_sm.png "Aggiungere attività toojob"
[6]: ./media/batch-dotnet-get-started/batch_workflow_06_sm.png "Monitorare le attività"
[7]: ./media/batch-dotnet-get-started/batch_workflow_07_sm.png "Scaricare l'output delle attività dal servizio di archiviazione"
[8]: ./media/batch-dotnet-get-started/batch_workflow_sm.png "Flusso di lavoro della soluzione Batch (diagramma completo)"
[9]: ./media/batch-dotnet-get-started/credentials_batch_sm.png "Credenziali di Batch nel portale"
[10]: ./media/batch-dotnet-get-started/credentials_storage_sm.png "Credenziali del servizio di archiviazione nel portale"
[11]: ./media/batch-dotnet-get-started/batch_workflow_minimal_sm.png "Flusso di lavoro della soluzione Batch (diagramma minimo)"
