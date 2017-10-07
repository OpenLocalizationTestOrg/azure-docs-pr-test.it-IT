---
title: aaaTransfer dati con hello libreria lo spostamento dei dati di archiviazione di Microsoft Azure | Documenti Microsoft
description: Utilizzare hello raccolta lo spostamento dei dati toomove o copia dati tooor dal contenuto di blob e file. Copiare i dati tooAzure archiviazione da file locali, o copiare dati in o tra gli account di archiviazione. Migrare facilmente l'archiviazione di tooAzure di dati.
services: storage
documentationcenter: 
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/22/2017
ms.author: seguler
ms.openlocfilehash: 9aec6cb171f794cc6ca432938ce499079e7dfdec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-hello-microsoft-azure-storage-data-movement-library"></a>Trasferimento dati con hello libreria lo spostamento dei dati di archiviazione di Microsoft Azure

## <a name="overview"></a>Panoramica
Hello libreria lo spostamento dei dati di archiviazione di Microsoft Azure è una libreria di multipiattaforma open source che è progettata per prestazioni elevate di caricamento, download e la copia di BLOB di archiviazione di Azure e i file. Questa libreria è hello dati lo spostamento dei framework di base che alimenta [AzCopy](../storage-use-azcopy.md). Hello raccolta lo spostamento dei dati fornisce pratici metodi che non sono disponibili i tradizionali [.NET Azure Storage Client Library](../blobs/storage-dotnet-how-to-use-blobs.md). Ciò include hello possibilità tooset hello numero di operazioni parallele, tenere traccia dell'avanzamento di trasferimento, riprendere facilmente un trasferimento annullato e molto altro ancora.  

La libreria usa inoltre .NET Core, utile quando si creano app .NET per Windows, Linux e macOS. toolearn ulteriori informazioni su .NET Core, vedere toohello [documentazione di .NET Core](https://dotnet.github.io/). La libreria è compatibile anche con le app .NET Framework tradizionali per Windows. 

Questo documento viene illustrato come un .NET Core toocreate console applicazione che viene eseguito in Windows, Linux e macOS che esegue hello seguenti scenari:

- Caricare file e directory tooBlob archiviazione.
- Definire il numero di hello di operazioni parallele durante il trasferimento dei dati.
- Monitorare lo stato del trasferimento dati.
- Riprendere un trasferimento dati annullato. 
- Copia del file da URL tooBlob archiviazione. 
- Copiare da archiviazione Blob tooBlob archiviazione.

**Che cosa occorre:**

* [Visual Studio Code](https://code.visualstudio.com/)
* Un [account di archiviazione di Azure](storage-create-storage-account.md#create-a-storage-account)

> [!NOTE]
> Questa guida presuppone che si abbia già familiarità con [Archiviazione di Azure](https://azure.microsoft.com/services/storage/). Se durante la lettura, non hello [tooAzure introduzione archiviazione](storage-introduction.md) documentazione è utile. In particolare, è necessario troppo[creare un account di archiviazione](storage-create-storage-account.md#create-a-storage-account) toostart utilizzando hello raccolta lo spostamento dei dati.
> 
> 

## <a name="setup"></a>Configurazione  

1. Visitare hello [Guida all'installazione di .NET Core](https://www.microsoft.com/net/core) tooinstall .NET Core. Quando si seleziona l'ambiente, scegliere l'opzione della riga di comando hello. 
2. Dalla riga di comando hello, creare una directory per il progetto. Spostarsi in questa directory, quindi digitare `dotnet new` progetto console c# toocreate.
3. Aprire la directory in Visual Studio Code. Questo passaggio può essere completato rapidamente tramite la riga di comando hello digitando `code .`.  
4. Installare hello [c# estensione](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) da Visual Studio Marketplace di codice hello. Riavviare Visual Studio Code. 
5. A questo punto compariranno due prompt. Uno viene utilizzata per aggiungere "toobuild asset necessari e debug". Fare clic su "Sì". L'altro prompt consente di ripristinare le dipendenze non risolte. Fare clic su "Ripristina".
6. L'applicazione dovrebbe contenere un `launch.json` file hello `.vscode` directory. In questo file, modificare hello `externalConsole` valore troppo`true`.
7. Codice di Visual Studio consente di applicazioni .NET Core toodebug. Riscontri `F5` toorun l'applicazione e verificare il funzionamento del programma di installazione. Dovrebbe essere visualizzato "Hello World!" console toohello stampato. 

## <a name="add-data-movement-library-tooyour-project"></a>Aggiungi progetto tooyour raccolta lo spostamento dei dati

1. Aggiungere hello la versione più recente di hello raccolta lo spostamento dei dati toohello `dependencies` sezione il `project.json` file. Al momento della scrittura hello sarebbe questa versione`"Microsoft.Azure.Storage.DataMovement": "0.5.0"` 
2. Aggiungere `"portable-net45+win8"` toohello `imports` sezione. 
3. Una richiesta deve essere visualizzato toorestore il progetto. Fare clic su pulsante "Ripristina" hello. È inoltre possibile ripristinare il progetto dalla riga di comando hello digitando il comando hello `dotnet restore` in hello directory radice del progetto.

Modificare `project.json`:

    {
      "version": "1.0.0-*",
      "buildOptions": {
        "debugType": "portable",
        "emitEntryPoint": true
      },
      "dependencies": {
        "Microsoft.Azure.Storage.DataMovement": "0.5.0"
      },
      "frameworks": {
        "netcoreapp1.1": {
          "dependencies": {
            "Microsoft.NETCore.App": {
              "type": "platform",
              "version": "1.1.0"
            }
          },
          "imports": [
            "dnxcore50",
            "portable-net45+win8"
          ]
        }
      }
    }

## <a name="set-up-hello-skeleton-of-your-application"></a>Impostare scheletro hello dell'applicazione
Innanzitutto, è necessario Hello è impostato il codice di "scheletro" hello dell'applicazione. Questo codice richiede la chiave account e nome di un account di archiviazione e utilizza tali toocreate credenziali un `CloudStorageAccount` oggetto. Questo oggetto è toointeract utilizzato con l'account di archiviazione in tutti gli scenari di trasferimento. codice Hello richiede inoltre ci tipo hello toochoose dell'operazione di trasferimento desideriamo tooexecute. 

Modificare `Program.cs`:

```csharp
using System;
using System.Threading;
using System.Diagnostics;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.WindowsAzure.Storage.DataMovement;

namespace DMLibSample
{
    public class Program
    {
        public static void Main()
        {
            Console.WriteLine("Enter Storage account name:");           
            string accountName = Console.ReadLine();

            Console.WriteLine("\nEnter Storage account key:");           
            string accountKey = Console.ReadLine();

            string storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=" + accountName + ";AccountKey=" + accountKey;
            CloudStorageAccount account = CloudStorageAccount.Parse(storageConnectionString);

            ExecuteChoice(account);
        }

        public static void ExecuteChoice(CloudStorageAccount account)
        {
            Console.WriteLine("\nWhat type of transfer would you like tooexecute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
            int choice = int.Parse(Console.ReadLine());

            if(choice == 1)
            {
                TransferLocalFileToAzureBlob(account).Wait();
            }
            else if(choice == 2)
            {
                TransferLocalDirectoryToAzureBlobDirectory(account).Wait();
            }
            else if(choice == 3)
            {
                TransferUrlToAzureBlob(account).Wait();
            }
            else if(choice == 4)
            {
                TransferAzureBlobToAzureBlob(account).Wait();
            }
        }

        public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
        { 
            
        }

        public static async Task TransferLocalDirectoryToAzureBlobDirectory(CloudStorageAccount account)
        { 
            
        }

        public static async Task TransferUrlToAzureBlob(CloudStorageAccount account)
        {

        }

        public static async Task TransferAzureBlobToAzureBlob(CloudStorageAccount account)
        {

        }
    }
}
```

## <a name="transfer-local-file-tooazure-blob"></a>Trasferimento file locale tooAzure Blob
Aggiungere metodi hello `GetSourcePath` e `GetBlob` troppo`Program.cs`:

```csharp
public static string GetSourcePath()
{
    Console.WriteLine("\nProvide path for source:");
    string sourcePath = Console.ReadLine();

    return sourcePath;
}

public static CloudBlockBlob GetBlob(CloudStorageAccount account)
{
    CloudBlobClient blobClient = account.CreateCloudBlobClient();

    Console.WriteLine("\nProvide name of Blob container:");
    string containerName = Console.ReadLine();
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);
    container.CreateIfNotExistsAsync().Wait();

    Console.WriteLine("\nProvide name of new Blob:");
    string blobName = Console.ReadLine();
    CloudBlockBlob blob = container.GetBlockBlobReference(blobName);

    return blob;
}
```

Modificare hello `TransferLocalFileToAzureBlob` metodo:

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    Console.WriteLine("\nTransfer started...");
    await TransferManager.UploadAsync(localFilePath, blob);
    Console.WriteLine("\nTransfer operation complete.");
    ExecuteChoice(account);
}
```

Questo codice richiede ci hello percorso tooa locale file, nome hello di un contenitore di nuovo o esistente e il nome di hello di un nuovo blob. Hello `TransferManager.UploadAsync` metodo esegue il caricamento di hello utilizzando le informazioni. 

Riscontri `F5` toorun l'applicazione. Per verificare se si è verificato durante il caricamento di hello visualizzando l'account di archiviazione con hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).

## <a name="set-number-of-parallel-operations"></a>Impostare il numero di operazioni parallele
Un'ottima funzionalità offerte da hello che raccolta lo spostamento dei dati sono hello possibilità tooset hello di velocità effettiva di trasferimento dei dati di operazioni parallele tooincrease hello. Per impostazione predefinita, hello raccolta lo spostamento dei dati imposta il numero di hello di operazioni parallele too8 * hello numero di core nel computer. 

Tenere presente che molte operazioni parallele in un ambiente di larghezza di banda bassa possono sovraccaricare la connessione di rete hello ed effettivamente impedire completamente il completamento delle operazioni. È necessario tooexperiment con questa impostazione di toodetermine ciò che funziona meglio in base la larghezza di banda di rete disponibile. 

Aggiungere codice che consente di elaborare il numero hello tooset delle operazioni parallele. Aggiungere anche il codice che verifica il tempo necessario per toocomplete trasferimento hello.

Aggiungere un `SetNumberOfParallelOperations` metodo troppo`Program.cs`:

```csharp
public static void SetNumberOfParallelOperations()
{
    Console.WriteLine("\nHow many parallel operations would you like toouse?");
    string parallelOperations = Console.ReadLine();
    TransferManager.Configurations.ParallelOperations = int.Parse(parallelOperations);
}
```

Modificare hello `ExecuteChoice` toouse metodo `SetNumberOfParallelOperations`:

```csharp
public static void ExecuteChoice(CloudStorageAccount account)
{
    Console.WriteLine("\nWhat type of transfer would you like tooexecute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
    int choice = int.Parse(Console.ReadLine());

    SetNumberOfParallelOperations();

    if(choice == 1)
    {
        TransferLocalFileToAzureBlob(account).Wait();
    }
    else if(choice == 2)
    {
        TransferLocalDirectoryToAzureBlobDirectory(account).Wait();
    }
    else if(choice == 3)
    {
        TransferUrlToAzureBlob(account).Wait();
    }
    else if(choice == 4)
    {
        TransferAzureBlobToAzureBlob(account).Wait();
    }
}
```

Modificare hello `TransferLocalFileToAzureBlob` toouse metodo timer:

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    Console.WriteLine("\nTransfer started...");
    Stopwatch stopWatch = Stopwatch.StartNew();
    await TransferManager.UploadAsync(localFilePath, blob);
    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

## <a name="track-transfer-progress"></a>Monitorare lo stato del trasferimento dati
Conoscere il tempo impiegato per il nostro tootransfer dati è molto utile. Tuttavia, in corso hello toosee in grado del trasferimento *durante* operazione di trasferimento hello sarebbe ancora migliore. tooachieve questo scenario, è necessario toocreate un `TransferContext` oggetto. Hello `TransferContext` oggetto sono disponibili in due forme: `SingleTransferContext` e `DirectoryTransferContext`. Hello precedente è per il trasferimento di un singolo file (ovvero stiamo ora) e hello quest'ultimo è per il trasferimento di una directory di file (che si aggiungono più avanti).

Aggiungere metodi hello `GetSingleTransferContext` e `GetDirectoryTransferContext` troppo`Program.cs`: 

```csharp
public static SingleTransferContext GetSingleTransferContext(TransferCheckpoint checkpoint)
{
    SingleTransferContext context = new SingleTransferContext(checkpoint);

    context.ProgressHandler = new Progress<TransferStatus>((progress) =>
    {
        Console.Write("\rBytes transferred: {0}", progress.BytesTransferred );
    });
    
    return context;
}

public static DirectoryTransferContext GetDirectoryTransferContext(TransferCheckpoint checkpoint)
{
    DirectoryTransferContext context = new DirectoryTransferContext(checkpoint);

    context.ProgressHandler = new Progress<TransferStatus>((progress) =>
    {
        Console.Write("\rBytes transferred: {0}", progress.BytesTransferred );
    });
    
    return context;
}
```

Modificare hello `TransferLocalFileToAzureBlob` toouse metodo `GetSingleTransferContext`:

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint);
    Console.WriteLine("\nTransfer started...\n");
    Stopwatch stopWatch = Stopwatch.StartNew();
    await TransferManager.UploadAsync(localFilePath, blob, null, context);
    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

## <a name="resume-a-canceled-transfer"></a>Riprendere un trasferimento annullato
Un'altra caratteristica interessante offerta hello raccolta lo spostamento dei dati è hello possibilità tooresume un trasferimento annullato. Aggiungere codice che consente il trasferimento di hello Annulla tootemporarily digitando `c`e quindi riprendere il trasferimento di hello 3 secondi in un secondo momento.

Modificare `TransferLocalFileToAzureBlob`:

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.UploadAsync(localFilePath, blob, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.UploadAsync(localFilePath, blob, null, context);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

Fino a questo punto, il nostro `checkpoint` valore è sempre stato impostato troppo`null`. A questo punto, se si annulla il trasferimento di hello, è recuperare l'ultimo checkpoint di hello del nostro trasferimento, quindi utilizzare questo nuovo checkpoint in questo contesto di trasferimento. 

## <a name="transfer-local-directory-tooazure-blob-directory"></a>Trasferimento della directory Blob tooAzure directory locale
Sarebbe deludente se hello raccolta lo spostamento dei dati può trasferire un solo file alla volta. Fortunatamente, non è in questo caso hello. Hello raccolta lo spostamento dei dati fornisce hello possibilità tootransfer una directory di file e tutte le relative sottodirectory. Aggiungere codice che consente di elaborare toodo proprio questo.

Innanzitutto, aggiungere il metodo hello `GetBlobDirectory` troppo`Program.cs`:

```csharp
public static CloudBlobDirectory GetBlobDirectory(CloudStorageAccount account)
{
    CloudBlobClient blobClient = account.CreateCloudBlobClient();

    Console.WriteLine("\nProvide name of Blob container. This can be a new or existing Blob container:");
    string containerName = Console.ReadLine();
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);
    container.CreateIfNotExistsAsync().Wait();

    CloudBlobDirectory blobDirectory = container.GetDirectoryReference("");

    return blobDirectory;
}
```

Poi modificare `TransferLocalDirectoryToAzureBlobDirectory`:

```csharp
public static async Task TransferLocalDirectoryToAzureBlobDirectory(CloudStorageAccount account)
{ 
    string localDirectoryPath = GetSourcePath();
    CloudBlobDirectory blobDirectory = GetBlobDirectory(account); 
    TransferCheckpoint checkpoint = null;
    DirectoryTransferContext context = GetDirectoryTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    UploadDirectoryOptions options = new UploadDirectoryOptions()
    {
        Recursive = true
    };

    try
    {
        task = TransferManager.UploadDirectoryAsync(localDirectoryPath, blobDirectory, options, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetDirectoryTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.UploadDirectoryAsync(localDirectoryPath, blobDirectory, options, context);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

Esistono alcune differenze tra questo metodo e il metodo hello per il caricamento di un singolo file. Ora utilizziamo `TransferManager.UploadDirectoryAsync` hello e `getDirectoryTransferContext` metodo creato in precedenza. Inoltre, sono disponibili un `options` valore tooour operazione di caricamento, che consente tooindicate che si vuole che le sottodirectory tooinclude nella funzione di caricamento. 

## <a name="copy-file-from-url-tooazure-blob"></a>Copia del file da tooAzure URL Blob
A questo punto, aggiungere codice che consente di elaborare un file da un Blob di Azure di tooan URL toocopy. 

Modificare `TransferUrlToAzureBlob`:

```csharp
public static async Task TransferUrlToAzureBlob(CloudStorageAccount account)
{
    Uri uri = new Uri(GetSourcePath());
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.CopyAsync(uri, blob, true, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.CopyAsync(uri, blob, true, null, context, cancellationSource.Token);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

Un importante questa funzionalità viene usata quando è necessario toomove dati da un altro cloud service (ad esempio AWS) tooAzure. Se si dispone di un URL che fornisce l'accesso toohello risorse, è possibile spostare facilmente tale risorsa nel BLOB di Azure tramite hello `TransferManager.CopyAsync` metodo. Questo metodo introduce anche un nuovo parametro booleano. Impostando questo parametro troppo`true` indica che si desidera copia toodo un ambiente asincrono sul lato server. Impostando questo parametro troppo`false` indica una copia sincrona, vale a dire risorse hello sono computer locale tooour scaricati in primo luogo, quindi caricato tooAzure Blob. Tuttavia, la copia sincrona è attualmente disponibile solo per la copia da un tooanother di risorse di archiviazione di Azure. 

## <a name="transfer-azure-blob-tooazure-blob"></a>Trasferimento Blob di Azure tooAzure Blob
Un'altra funzionalità fornita in modo univoco da hello raccolta lo spostamento dei dati è hello possibilità toocopy da uno tooanother di risorse di archiviazione di Azure. 

Modificare `TransferAzureBlobToAzureBlob`:

```csharp
public static async Task TransferAzureBlobToAzureBlob(CloudStorageAccount account)
{
    CloudBlockBlob sourceBlob = GetBlob(account);
    CloudBlockBlob destinationBlob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.CopyAsync(sourceBlob, destinationBlob, true, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.CopyAsync(sourceBlob, destinationBlob, false, null, context, cancellationSource.Token);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

In questo esempio viene impostato parametro booleano hello in `TransferManager.CopyAsync` troppo`false` tooindicate che toodo una copia sincrona. Ciò significa che risorse hello sono computer locale tooour scaricato, quindi caricato tooAzure Blob. l'opzione copia sincrono Hello è tooensure un ottimo modo che l'operazione di copia ha una velocità coerenza. Al contrario, la velocità di hello di una copia lato server asincrona è dipendente da hello disponibile larghezza di banda sul server hello, che possono variare. Tuttavia, copia sincrona può generare uscita ulteriori costi rispetto tooasynchronous copia. Hello approccio migliore consiste toouse copia sincrona in una macchina virtuale di Azure in hello stessa area del costo di uscita origine tooavoid account di archiviazione.

## <a name="conclusion"></a>Conclusioni
L'applicazione per lo spostamento dei dati ora è completa. [Nell'esempio di codice completo Hello è disponibile in GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app). 

## <a name="next-steps"></a>Passaggi successivi
In questa guida introduttiva è stata creata un'applicazione in grado di interagire con Archiviazione di Azure e che può essere eseguita su Windows, Linux e macOS. Questa guida introduttiva ha trattato principalmente dell'archivio BLOB. Tuttavia, questa conoscenza stesso può essere applicato tooFile archiviazione. toolearn, estrarre [la documentazione di riferimento libreria lo spostamento dei dati di archiviazione Azure](https://azure.github.io/azure-storage-net-data-movement).

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]




