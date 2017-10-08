---
title: aaaGet avviato con l'archiviazione Blob di Azure (archiviazione di oggetti) utilizzando .NET | Documenti Microsoft
description: Archiviare dati non strutturati nel cloud hello con archiviazione Blob di Azure (archiviazione di oggetti).
services: storage
documentationcenter: .net
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: d18a8fc8-97cb-4d37-a408-a6f8107ea8b3
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: marsma
ms.openlocfilehash: 3df0cf14b69d85cdc2f62cc3c8b901be102fa026
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-using-net"></a>Introduzione all'archivio BLOB di Azure con .NET

[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

Archiviazione Blob di Azure è un servizio che archivia i dati non strutturati nel cloud hello come oggetti/BLOB. Archivio BLOB può archiviare qualsiasi tipo di dati di testo o binari, ad esempio un documento, un file multimediale o un programma di installazione di un'applicazione. Archiviazione BLOB è anche archiviazione di oggetti di cui viene fatto riferimento tooas.

### <a name="about-this-tutorial"></a>Informazioni sull'esercitazione
Questa esercitazione viene illustrato come toowrite .NET codice in alcuni scenari comuni di utilizzo dell'archiviazione Blob di Azure. Gli scenari presentati includono caricamento, visualizzazione dell'elenco, download ed eliminazione di BLOB.

**Prerequisiti:**

* [Microsoft Visual Studio](https://www.visualstudio.com/)
* [Libreria client di archiviazione di Azure per .NET](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [Gestione configurazione di Azure per .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* Un [account di archiviazione di Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a>Altri esempi
Per altri esempi di uso dell'archivio BLOB, vedere [Getting Started with Azure Blob Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)(Introduzione all'archiviazione BLOB di Azure in .NET). È possibile scaricare l'applicazione di esempio hello ed eseguirlo o esaminare il codice hello su GitHub.

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a>Aggiungere le direttive using
Aggiungere il seguente hello **utilizzando** hello cima toohello direttive `Program.cs` file:

```csharp
using Microsoft.WindowsAzure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Blob storage types
```

### <a name="parse-hello-connection-string"></a>Analizzare la stringa di connessione hello
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-blob-service-client"></a>Creare hello client del servizio Blob
Hello **CloudBlobClient** classe consente tooretrieve contenitori e BLOB archiviati nell'archiviazione Blob. Ecco un modo toocreate client del servizio hello:

```csharp
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```
Si è ora pronto toowrite codice che legge i dati da e scrive tooBlob archiviazione dei dati.

## <a name="create-a-container"></a>Creare un contenitore
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

Questo esempio viene illustrato come toocreate un contenitore, se non esiste già:

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create hello container if it doesn't already exist.
container.CreateIfNotExists();
```

Per impostazione predefinita, il nuovo contenitore di hello è privato, vale a dire che è necessario specificare i BLOB toodownload chiave di accesso di archiviazione da questo contenitore. Se si desidera toomake hello file all'interno di hello contenitore disponibili tooeveryone, è possibile impostare hello contenitore toobe pubblico utilizzando hello seguente codice:

```csharp
container.SetPermissions(
    new BlobContainerPermissions { PublicAccess = BlobContainerPublicAccessType.Blob });
```

Chiunque in Internet hello può visualizzare i BLOB in un contenitore pubblico. Tuttavia, è possibile modificare o eliminarli solo se si dispone di una firma di accesso condiviso o di chiave di accesso account appropriato hello.

## <a name="upload-a-blob-into-a-container"></a>Caricare un BLOB in un contenitore
In Archiviazione BLOB di Azure sono supportati BLOB in blocchi e BLOB di pagine.  Nella maggior parte dei casi, blob in blocchi è consigliata toouse tipo hello.

tooupload un blob in blocchi file tooa, ottenere un riferimento a un contenitore e usarlo tooget un riferimento di blob di blocco. Dopo aver creato un riferimento di blob, è possibile caricare qualsiasi flusso di dati tooit dal chiamante hello **UploadFromStream** metodo. Questa operazione crea blob hello se non esiste in precedenza o sovrascritto se esiste.

Hello seguente esempio viene illustrato come tooupload un blob in un contenitore e si presuppone che il contenitore hello è già stato creato.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

// Create or overwrite hello "myblob" blob with contents from a local file.
using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
{
    blockBlob.UploadFromStream(fileStream);
}
```

## <a name="list-hello-blobs-in-a-container"></a>Elenco di BLOB hello in un contenitore
BLOB di hello toolist in un contenitore, prima di ottenere un riferimento di contenitore. È quindi possibile utilizzare del contenitore hello **ListBlobs** BLOB hello tooretrieve di metodo e/o directory all'interno di esso. set completo di proprietà e metodi per un tipo restituito di hello tooaccess **IListBlobItem**, è necessario eseguirne il cast tooa **CloudBlockBlob**, **CloudPageBlob**, o  **CloudBlobDirectory** oggetto. Se il tipo di hello è sconosciuto, è possibile utilizzare un toodetermine di controllo di tipo quali toocast a. Hello codice seguente viene illustrato come tooretrieve e output di hello URI di ogni elemento nel hello _foto_ contenitore:

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("photos");

// Loop over items within hello container and output hello length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, false))
{
    if (item.GetType() == typeof(CloudBlockBlob))
    {
        CloudBlockBlob blob = (CloudBlockBlob)item;

        Console.WriteLine("Block blob of length {0}: {1}", blob.Properties.Length, blob.Uri);

    }
    else if (item.GetType() == typeof(CloudPageBlob))
    {
        CloudPageBlob pageBlob = (CloudPageBlob)item;

        Console.WriteLine("Page blob of length {0}: {1}", pageBlob.Properties.Length, pageBlob.Uri);

    }
    else if (item.GetType() == typeof(CloudBlobDirectory))
    {
        CloudBlobDirectory directory = (CloudBlobDirectory)item;

        Console.WriteLine("Directory: {0}", directory.Uri);
    }
}
```

Includendo le informazioni sul percorso nei nomi di BLOB, è possibile creare una struttura di directory virtuale che è possibile organizzare e attraversare come un file system tradizionale. struttura di directory Hello è virtuale solo - hello solo le risorse disponibili nell'archiviazione Blob sono contenitori e BLOB. Libreria client di archiviazione hello offre tuttavia un **CloudBlobDirectory** oggetto directory virtuale di toorefer tooa e semplificare il processo di hello dell'utilizzo di BLOB sono organizzati in questo modo.

Si consideri ad esempio hello seguente set di BLOB in blocchi in un contenitore denominato *foto*:

```
photo1.jpg
2010/architecture/description.txt
2010/architecture/photo3.jpg
2010/architecture/photo4.jpg
2011/architecture/photo5.jpg
2011/architecture/photo6.jpg
2011/architecture/description.txt
2011/photo7.jpg
```

Quando si chiama **ListBlobs** su hello *foto* contenitore (ad esempio hello frammento di codice precedente), viene restituito un elenco gerarchico. Il nome contiene i **CloudBlobDirectory** e **CloudBlockBlob** oggetti che rappresentano directory hello e i BLOB nel contenitore di hello, rispettivamente. output di Hello risultante è simile:

```
Directory: https://<accountname>.blob.core.windows.net/photos/2010/
Directory: https://<accountname>.blob.core.windows.net/photos/2011/
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

Facoltativamente, è possibile impostare hello **UseFlatBlobListing** parametro di hello **ListBlobs** metodo **true**. In questo caso, ogni blob nel contenitore hello viene restituito come un **CloudBlockBlob** oggetto. Hello chiamata troppo**ListBlobs** tooreturn un elenco semplice è simile al seguente:

```csharp
// Loop over items within hello container and output hello length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, true))
{
    ...
}
```

e i risultati di hello è simile al seguente:

```
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

## <a name="download-blobs"></a>Scaricare BLOB
BLOB toodownload, recuperare innanzitutto un riferimento di blob e quindi chiamare hello **metodi DownloadToStream** metodo. esempio Hello utilizza hello **metodi DownloadToStream** metodo tootransfer hello blob contenuto tooa oggetto flusso che può quindi rendere persistente tooa file locale.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "photo1.jpg".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

// Save blob contents tooa file.
using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
{
    blockBlob.DownloadToStream(fileStream);
}
```

È inoltre possibile utilizzare hello **metodi DownloadToStream** contenuto hello toodownload di metodo di un blob come una stringa di testo.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob.txt"
CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

string text;
using (var memoryStream = new MemoryStream())
{
    blockBlob2.DownloadToStream(memoryStream);
    text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
}
```

## <a name="delete-blobs"></a>Eliminare BLOB
un blob, toodelete innanzitutto ottenere un riferimento di blob e quindi chiamare il **eliminare** metodo su di esso.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob.txt".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

// Delete hello blob.
blockBlob.Delete();
```

## <a name="list-blobs-in-pages-asynchronously"></a>Elencare BLOB nelle pagine in modalità asincrona
Elencare un numero elevato di BLOB, se si desidera toocontrol hello numero di risultati che restituito in un'unica operazione di elenco, è possibile elencare i BLOB di pagine di risultati. Questo esempio mostra la vista tooreturn dei risultati nelle pagine in modo asincrono, in modo che non l'esecuzione viene bloccata durante l'attesa tooreturn un ampio set di risultati.

Questo esempio viene illustrato un semplice elenco di blob, ma è anche possibile eseguire un elenco gerarchico, impostazione hello _useFlatBlobListing_ parametro di hello **ListBlobsSegmentedAsync** too_false_ metodo.

Poiché l'esempio hello chiama un metodo asincrono, devono essere preceduto da hello _async_ (parola chiave) e deve restituire un **attività** oggetto. Hello await (parola chiave) specificato per hello **ListBlobsSegmentedAsync** metodo sospende l'esecuzione del metodo di esempio hello fino al completamento hello elenco attività.

```csharp
async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
{
    //List blobs toohello console window, with paging.
    Console.WriteLine("List blobs in pages:");

    int i = 0;
    BlobContinuationToken continuationToken = null;
    BlobResultSegment resultSegment = null;

    //Call ListBlobsSegmentedAsync and enumerate hello result segment returned, while hello continuation token is non-null.
    //When hello continuation token is null, hello last page has been returned and execution can exit hello loop.
    do
    {
        //This overload allows control of hello page size. You can return all remaining results by passing null for hello maxResults parameter,
        //or by calling a different overload.
        resultSegment = await container.ListBlobsSegmentedAsync("", true, BlobListingDetails.All, 10, continuationToken, null, null);
        if (resultSegment.Results.Count<IListBlobItem>() > 0) { Console.WriteLine("Page {0}:", ++i); }
        foreach (var blobItem in resultSegment.Results)
        {
            Console.WriteLine("\t{0}", blobItem.StorageUri.PrimaryUri);
        }
        Console.WriteLine();

        //Get hello continuation token.
        continuationToken = resultSegment.ContinuationToken;
    }
    while (continuationToken != null);
}
```

## <a name="writing-tooan-append-blob"></a>Scrittura tooan aggiungere blob
Un blob di accodamento è ottimizzato per le operazioni di accodamento, ad esempio la registrazione. Come un blob in blocchi, un blob di aggiunta è costituito da blocchi, ma quando si aggiunge un nuovo blob in blocchi tooan accodamento, è sempre aggiunte toohello fine del blob hello. È possibile aggiornare o eliminare un blocco esistente in un blob di Accodamento. ID blocco Hello per un blob di aggiunta non vengono esposte come se fossero per un blob in blocchi.

Ogni blocco di un blob di aggiunta può avere dimensioni diverse, backup tooa massimo 4 MB, e un blob di aggiunta può includere un massimo di 50.000 blocchi. dimensione massima di Hello di un blob di aggiunta è pertanto leggermente superiore a 195 GB (4 MB X 50.000 blocchi).

esempio Hello seguente crea un nuovo blob di aggiunta e accoda tooit alcuni dati, simulazione di un'operazione di registrazione semplice.

```csharp
//Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

//Create service client for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("my-append-blobs");

//Create hello container if it does not already exist.
container.CreateIfNotExists();

//Get a reference tooan append blob.
CloudAppendBlob appendBlob = container.GetAppendBlobReference("append-blob.log");

//Create hello append blob. Note that if hello blob already exists, hello CreateOrReplace() method will overwrite it.
//You can check whether hello blob exists tooavoid overwriting it by using CloudAppendBlob.Exists().
appendBlob.CreateOrReplace();

int numBlocks = 10;

//Generate an array of random bytes.
Random rnd = new Random();
byte[] bytes = new byte[numBlocks];
rnd.NextBytes(bytes);

//Simulate a logging operation by writing text data and byte data toohello end of hello append blob.
for (int i = 0; i < numBlocks; i++)
{
    appendBlob.AppendText(String.Format("Timestamp: {0:u} \tLog Entry: {1}{2}",
        DateTime.UtcNow, bytes[i], Environment.NewLine));
}

//Read hello append blob toohello console window.
Console.WriteLine(appendBlob.DownloadText());
```

Vedere [informazioni sui BLOB in blocchi, BLOB di pagine e BLOB, accodare](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) per ulteriori informazioni sulle differenze di hello tra hello tre tipi di BLOB.

## <a name="managing-security-for-blobs"></a>Gestione della sicurezza dei BLOB
Per impostazione predefinita, archiviazione di Azure i dati rimangono al sicuro limitando l'accesso toohello account proprietario, ovvero in possesso delle chiavi di accesso account hello. Quando è necessario tooshare i dati blob nell'account di archiviazione, è importante toodo così senza compromettere la sicurezza hello di chiavi di accesso account. Inoltre, è possibile crittografare tooensure dati blob che è sicuro passare rete hello e archiviazione di Azure.

[!INCLUDE [storage-account-key-note-include](../../../includes/storage-account-key-note-include.md)]

### <a name="controlling-access-tooblob-data"></a>Controllo dell'accesso ai dati tooblob
Per impostazione predefinita, i dati blob hello nell'account di archiviazione sono accessibile solo proprietario dell'account toostorage. Autenticazione delle richieste nel servizio di archiviazione Blob richiede una chiave di accesso account hello per impostazione predefinita. Tuttavia, è preferibile toomake determinati utenti tooother disponibili dati di blob. Sono disponibili due opzioni:

* **Accesso anonimo** : è possibile rendere disponibili pubblicamente per l'accesso anonimo un contenitore o i BLOB in esso inclusi. Vedere [gestire BLOB e accesso in lettura anonimo toocontainers](storage-manage-access-to-resources.md) per ulteriori informazioni.
* **Firme di accesso condiviso:** è possibile fornire ai client con una firma di accesso condiviso (SAS), che fornisce l'accesso delegato tooa risorse nell'account di archiviazione, con le autorizzazioni specificate e in un intervallo di tempo specificato. Vedere [Using Shared Access Signatures (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) (Uso di firme di accesso condiviso) per altre informazioni.

### <a name="encrypting-blob-data"></a>Crittografia dei dati BLOB
Archiviazione di Azure supporta la crittografia dei dati blob sia nel client hello hello server:

* **Crittografia client-side:** hello libreria Client di archiviazione per .NET supporta la crittografia dei dati all'interno delle applicazioni client prima di caricare tooAzure Storage e la decrittografia dei dati durante il download toohello client. libreria Hello supporta inoltre l'integrazione con l'insieme di credenziali chiave di Azure per la gestione di chiave account di archiviazione. Per altre informazioni, vedere [Crittografia lato client con .NET per Archiviazione di Microsoft Azure](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) . Vedere anche [Esercitazione: Crittografare e decrittografare i BLOB in Archiviazione di Microsoft Azure tramite l'insieme di credenziali delle chiavi di Azure](storage-encrypt-decrypt-blobs-key-vault.md).
* **Crittografia lato server**: Archiviazione di Azure supporta ora la crittografia lato server. Vedere [Crittografia del servizio di archiviazione di Azure per dati inattivi (anteprima)](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

## <a name="next-steps"></a>Passaggi successivi
Ora che si è appreso i concetti di base di hello dell'archiviazione Blob, seguire questi ulteriori toolearn di collegamenti.

### <a name="microsoft-azure-storage-explorer"></a>Microsoft Azure Storage Explorer
* [Microsoft Azure Storage Explorer (MASE)](../../vs-azure-tools-storage-manage-with-storage-explorer.md) è un'app autonoma, disponibile da Microsoft che consente di toowork visivamente i dati di archiviazione di Azure in Windows, macOS e Linux.

### <a name="blob-storage-samples"></a>Esempi di archiviazione BLOB
* [Getting Started with Azure Blob Storage in .NET (Introduzione all'archiviazione BLOB di Azure in .NET)](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)

### <a name="blob-storage-reference"></a>Informazioni di riferimento sull'archiviazione BLOB
* [Informazioni di riferimento sulla libreria client di archiviazione per .NET](https://msdn.microsoft.com/library/azure/mt347887.aspx)
* [Informazioni di riferimento sulle API REST](/rest/api/storageservices/azure-storage-services-rest-api-reference)

### <a name="conceptual-guides"></a>Guide concettuali
* [Trasferimento dati con hello utilità della riga di comando AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [Come usare l'archiviazione file di Azure](../files/storage-dotnet-how-to-use-files.md)
* [La modalità di archiviazione con blob di Azure toouse hello WebJobs SDK](../../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
