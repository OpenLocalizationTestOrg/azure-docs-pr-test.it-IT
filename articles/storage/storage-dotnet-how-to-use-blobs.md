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
ms.openlocfilehash: 9b675ac073e7e901fe1afe54f7bfea12eefbf3ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-using-net"></a><span data-ttu-id="7bd86-103">Introduzione all'archivio BLOB di Azure con .NET</span><span class="sxs-lookup"><span data-stu-id="7bd86-103">Get started with Azure Blob storage using .NET</span></span>

[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

<span data-ttu-id="7bd86-104">Archiviazione Blob di Azure è un servizio che archivia i dati non strutturati nel cloud hello come oggetti/BLOB.</span><span class="sxs-lookup"><span data-stu-id="7bd86-104">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="7bd86-105">Archivio BLOB può archiviare qualsiasi tipo di dati di testo o binari, ad esempio un documento, un file multimediale o un programma di installazione di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7bd86-105">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="7bd86-106">Archiviazione BLOB è anche archiviazione di oggetti di cui viene fatto riferimento tooas.</span><span class="sxs-lookup"><span data-stu-id="7bd86-106">Blob storage is also referred tooas object storage.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="7bd86-107">Informazioni sull'esercitazione</span><span class="sxs-lookup"><span data-stu-id="7bd86-107">About this tutorial</span></span>
<span data-ttu-id="7bd86-108">Questa esercitazione viene illustrato come toowrite .NET codice in alcuni scenari comuni di utilizzo dell'archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="7bd86-108">This tutorial shows how toowrite .NET code for some common scenarios using Azure Blob storage.</span></span> <span data-ttu-id="7bd86-109">Gli scenari presentati includono caricamento, visualizzazione dell'elenco, download ed eliminazione di BLOB.</span><span class="sxs-lookup"><span data-stu-id="7bd86-109">Scenarios covered include uploading, listing, downloading, and deleting blobs.</span></span>

<span data-ttu-id="7bd86-110">**Prerequisiti:**</span><span class="sxs-lookup"><span data-stu-id="7bd86-110">**Prerequisites:**</span></span>

* [<span data-ttu-id="7bd86-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7bd86-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/)
* [<span data-ttu-id="7bd86-112">Libreria client di archiviazione di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="7bd86-112">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="7bd86-113">Gestione configurazione di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="7bd86-113">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* <span data-ttu-id="7bd86-114">Un [account di archiviazione di Azure](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="7bd86-114">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a><span data-ttu-id="7bd86-115">Altri esempi</span><span class="sxs-lookup"><span data-stu-id="7bd86-115">More samples</span></span>
<span data-ttu-id="7bd86-116">Per altri esempi di uso dell'archivio BLOB, vedere [Getting Started with Azure Blob Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)(Introduzione all'archiviazione BLOB di Azure in .NET).</span><span class="sxs-lookup"><span data-stu-id="7bd86-116">For additional examples using Blob storage, see [Getting Started with Azure Blob Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span></span> <span data-ttu-id="7bd86-117">È possibile scaricare l'applicazione di esempio hello ed eseguirlo o esaminare il codice hello su GitHub.</span><span class="sxs-lookup"><span data-stu-id="7bd86-117">You can download hello sample application and run it, or browse hello code on GitHub.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="7bd86-118">Aggiungere le direttive using</span><span class="sxs-lookup"><span data-stu-id="7bd86-118">Add using directives</span></span>
<span data-ttu-id="7bd86-119">Aggiungere il seguente hello **utilizzando** hello cima toohello direttive `Program.cs` file:</span><span class="sxs-lookup"><span data-stu-id="7bd86-119">Add hello following **using** directives toohello top of hello `Program.cs` file:</span></span>

```csharp
using Microsoft.WindowsAzure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Blob storage types
```

### <a name="parse-hello-connection-string"></a><span data-ttu-id="7bd86-120">Analizzare la stringa di connessione hello</span><span class="sxs-lookup"><span data-stu-id="7bd86-120">Parse hello connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-blob-service-client"></a><span data-ttu-id="7bd86-121">Creare hello client del servizio Blob</span><span class="sxs-lookup"><span data-stu-id="7bd86-121">Create hello Blob service client</span></span>
<span data-ttu-id="7bd86-122">Hello **CloudBlobClient** classe consente tooretrieve contenitori e BLOB archiviati nell'archiviazione Blob.</span><span class="sxs-lookup"><span data-stu-id="7bd86-122">hello **CloudBlobClient** class enables you tooretrieve containers and blobs stored in Blob storage.</span></span> <span data-ttu-id="7bd86-123">Ecco un modo toocreate client del servizio hello:</span><span class="sxs-lookup"><span data-stu-id="7bd86-123">Here's one way toocreate hello service client:</span></span>

```csharp
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```
<span data-ttu-id="7bd86-124">Si è ora pronto toowrite codice che legge i dati da e scrive tooBlob archiviazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="7bd86-124">Now you are ready toowrite code that reads data from and writes data tooBlob storage.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="7bd86-125">Creare un contenitore</span><span class="sxs-lookup"><span data-stu-id="7bd86-125">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="7bd86-126">Questo esempio viene illustrato come toocreate un contenitore, se non esiste già:</span><span class="sxs-lookup"><span data-stu-id="7bd86-126">This example shows how toocreate a container if it does not already exist:</span></span>

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

<span data-ttu-id="7bd86-127">Per impostazione predefinita, il nuovo contenitore di hello è privato, vale a dire che è necessario specificare i BLOB toodownload chiave di accesso di archiviazione da questo contenitore.</span><span class="sxs-lookup"><span data-stu-id="7bd86-127">By default, hello new container is private, meaning that you must specify your storage access key toodownload blobs from this container.</span></span> <span data-ttu-id="7bd86-128">Se si desidera toomake hello file all'interno di hello contenitore disponibili tooeveryone, è possibile impostare hello contenitore toobe pubblico utilizzando hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="7bd86-128">If you want toomake hello files within hello container available tooeveryone, you can set hello container toobe public using hello following code:</span></span>

```csharp
container.SetPermissions(
    new BlobContainerPermissions { PublicAccess = BlobContainerPublicAccessType.Blob });
```

<span data-ttu-id="7bd86-129">Chiunque in Internet hello può visualizzare i BLOB in un contenitore pubblico.</span><span class="sxs-lookup"><span data-stu-id="7bd86-129">Anyone on hello Internet can see blobs in a public container.</span></span> <span data-ttu-id="7bd86-130">Tuttavia, è possibile modificare o eliminarli solo se si dispone di una firma di accesso condiviso o di chiave di accesso account appropriato hello.</span><span class="sxs-lookup"><span data-stu-id="7bd86-130">However, you can modify or delete them only if you have hello appropriate account access key or a shared access signature.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="7bd86-131">Caricare un BLOB in un contenitore</span><span class="sxs-lookup"><span data-stu-id="7bd86-131">Upload a blob into a container</span></span>
<span data-ttu-id="7bd86-132">In Archiviazione BLOB di Azure sono supportati BLOB in blocchi e BLOB di pagine.</span><span class="sxs-lookup"><span data-stu-id="7bd86-132">Azure Blob Storage supports block blobs and page blobs.</span></span>  <span data-ttu-id="7bd86-133">Nella maggior parte dei casi, blob in blocchi è consigliata toouse tipo hello.</span><span class="sxs-lookup"><span data-stu-id="7bd86-133">In most cases, block blob is hello recommended type toouse.</span></span>

<span data-ttu-id="7bd86-134">tooupload un blob in blocchi file tooa, ottenere un riferimento a un contenitore e usarlo tooget un riferimento di blob di blocco.</span><span class="sxs-lookup"><span data-stu-id="7bd86-134">tooupload a file tooa block blob, get a container reference and use it tooget a block blob reference.</span></span> <span data-ttu-id="7bd86-135">Dopo aver creato un riferimento di blob, è possibile caricare qualsiasi flusso di dati tooit dal chiamante hello **UploadFromStream** metodo.</span><span class="sxs-lookup"><span data-stu-id="7bd86-135">Once you have a blob reference, you can upload any stream of data tooit by calling hello **UploadFromStream** method.</span></span> <span data-ttu-id="7bd86-136">Questa operazione crea blob hello se non esiste in precedenza o sovrascritto se esiste.</span><span class="sxs-lookup"><span data-stu-id="7bd86-136">This operation creates hello blob if it didn't previously exist, or overwrites it if it does exist.</span></span>

<span data-ttu-id="7bd86-137">Hello seguente esempio viene illustrato come tooupload un blob in un contenitore e si presuppone che il contenitore hello è già stato creato.</span><span class="sxs-lookup"><span data-stu-id="7bd86-137">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>

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

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="7bd86-138">Elenco di BLOB hello in un contenitore</span><span class="sxs-lookup"><span data-stu-id="7bd86-138">List hello blobs in a container</span></span>
<span data-ttu-id="7bd86-139">BLOB di hello toolist in un contenitore, prima di ottenere un riferimento di contenitore.</span><span class="sxs-lookup"><span data-stu-id="7bd86-139">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="7bd86-140">È quindi possibile utilizzare del contenitore hello **ListBlobs** BLOB hello tooretrieve di metodo e/o directory all'interno di esso.</span><span class="sxs-lookup"><span data-stu-id="7bd86-140">You can then use hello container's **ListBlobs** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="7bd86-141">set completo di proprietà e metodi per un tipo restituito di hello tooaccess **IListBlobItem**, è necessario eseguirne il cast tooa **CloudBlockBlob**, **CloudPageBlob**, o  **CloudBlobDirectory** oggetto.</span><span class="sxs-lookup"><span data-stu-id="7bd86-141">tooaccess hello  rich set of properties and methods for a returned **IListBlobItem**, you must cast it tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="7bd86-142">Se il tipo di hello è sconosciuto, è possibile utilizzare un toodetermine di controllo di tipo quali toocast a.</span><span class="sxs-lookup"><span data-stu-id="7bd86-142">If hello type is unknown, you can use a type check toodetermine which toocast it to.</span></span> <span data-ttu-id="7bd86-143">Hello codice seguente viene illustrato come tooretrieve e output di hello URI di ogni elemento nel hello _foto_ contenitore:</span><span class="sxs-lookup"><span data-stu-id="7bd86-143">hello following code demonstrates how tooretrieve and output hello URI of each item in hello _photos_ container:</span></span>

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

<span data-ttu-id="7bd86-144">Includendo le informazioni sul percorso nei nomi di BLOB, è possibile creare una struttura di directory virtuale che è possibile organizzare e attraversare come un file system tradizionale.</span><span class="sxs-lookup"><span data-stu-id="7bd86-144">By including path information in blob names, you can create a virtual directory structure you can organize and traverse as you would a traditional file system.</span></span> <span data-ttu-id="7bd86-145">struttura di directory Hello è virtuale solo - hello solo le risorse disponibili nell'archiviazione Blob sono contenitori e BLOB.</span><span class="sxs-lookup"><span data-stu-id="7bd86-145">hello directory structure is virtual only--hello only resources available in Blob storage are containers and blobs.</span></span> <span data-ttu-id="7bd86-146">Libreria client di archiviazione hello offre tuttavia un **CloudBlobDirectory** oggetto directory virtuale di toorefer tooa e semplificare il processo di hello dell'utilizzo di BLOB sono organizzati in questo modo.</span><span class="sxs-lookup"><span data-stu-id="7bd86-146">However, hello storage client library offers a **CloudBlobDirectory** object toorefer tooa virtual directory and simplify hello process of working with blobs that are organized in this way.</span></span>

<span data-ttu-id="7bd86-147">Si consideri ad esempio hello seguente set di BLOB in blocchi in un contenitore denominato *foto*:</span><span class="sxs-lookup"><span data-stu-id="7bd86-147">For example, consider hello following set of block blobs in a container named *photos*:</span></span>

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

<span data-ttu-id="7bd86-148">Quando si chiama **ListBlobs** su hello *foto* contenitore (ad esempio hello frammento di codice precedente), viene restituito un elenco gerarchico.</span><span class="sxs-lookup"><span data-stu-id="7bd86-148">When you call **ListBlobs** on hello *photos* container (as in hello preceding code snippet), a hierarchical listing is returned.</span></span> <span data-ttu-id="7bd86-149">Il nome contiene i **CloudBlobDirectory** e **CloudBlockBlob** oggetti che rappresentano directory hello e i BLOB nel contenitore di hello, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="7bd86-149">It contains both **CloudBlobDirectory** and **CloudBlockBlob** objects, representing hello directories and blobs in hello container, respectively.</span></span> <span data-ttu-id="7bd86-150">output di Hello risultante è simile:</span><span class="sxs-lookup"><span data-stu-id="7bd86-150">hello resulting output looks like:</span></span>

```
Directory: https://<accountname>.blob.core.windows.net/photos/2010/
Directory: https://<accountname>.blob.core.windows.net/photos/2011/
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

<span data-ttu-id="7bd86-151">Facoltativamente, è possibile impostare hello **UseFlatBlobListing** parametro di hello **ListBlobs** metodo **true**.</span><span class="sxs-lookup"><span data-stu-id="7bd86-151">Optionally, you can set hello **UseFlatBlobListing** parameter of hello **ListBlobs** method to **true**.</span></span> <span data-ttu-id="7bd86-152">In questo caso, ogni blob nel contenitore hello viene restituito come un **CloudBlockBlob** oggetto.</span><span class="sxs-lookup"><span data-stu-id="7bd86-152">In this case, every blob in hello container is returned as a **CloudBlockBlob** object.</span></span> <span data-ttu-id="7bd86-153">Hello chiamata troppo**ListBlobs** tooreturn un elenco semplice è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="7bd86-153">hello call too**ListBlobs** tooreturn a flat listing looks like this:</span></span>

```csharp
// Loop over items within hello container and output hello length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, true))
{
    ...
}
```

<span data-ttu-id="7bd86-154">e i risultati di hello è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="7bd86-154">and hello results look like this:</span></span>

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

## <a name="download-blobs"></a><span data-ttu-id="7bd86-155">Scaricare BLOB</span><span class="sxs-lookup"><span data-stu-id="7bd86-155">Download blobs</span></span>
<span data-ttu-id="7bd86-156">BLOB toodownload, recuperare innanzitutto un riferimento di blob e quindi chiamare hello **metodi DownloadToStream** metodo.</span><span class="sxs-lookup"><span data-stu-id="7bd86-156">toodownload blobs, first retrieve a blob reference and then call hello **DownloadToStream** method.</span></span> <span data-ttu-id="7bd86-157">esempio Hello utilizza hello **metodi DownloadToStream** metodo tootransfer hello blob contenuto tooa oggetto flusso che può quindi rendere persistente tooa file locale.</span><span class="sxs-lookup"><span data-stu-id="7bd86-157">hello following example uses hello **DownloadToStream** method tootransfer hello blob contents tooa stream object that you can then persist tooa local file.</span></span>

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

<span data-ttu-id="7bd86-158">È inoltre possibile utilizzare hello **metodi DownloadToStream** contenuto hello toodownload di metodo di un blob come una stringa di testo.</span><span class="sxs-lookup"><span data-stu-id="7bd86-158">You can also use hello **DownloadToStream** method toodownload hello contents of a blob as a text string.</span></span>

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

## <a name="delete-blobs"></a><span data-ttu-id="7bd86-159">Eliminare BLOB</span><span class="sxs-lookup"><span data-stu-id="7bd86-159">Delete blobs</span></span>
<span data-ttu-id="7bd86-160">un blob, toodelete innanzitutto ottenere un riferimento di blob e quindi chiamare il **eliminare** metodo su di esso.</span><span class="sxs-lookup"><span data-stu-id="7bd86-160">toodelete a blob, first get a blob reference and then call the **Delete** method on it.</span></span>

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

## <a name="list-blobs-in-pages-asynchronously"></a><span data-ttu-id="7bd86-161">Elencare BLOB nelle pagine in modalità asincrona</span><span class="sxs-lookup"><span data-stu-id="7bd86-161">List blobs in pages asynchronously</span></span>
<span data-ttu-id="7bd86-162">Elencare un numero elevato di BLOB, se si desidera toocontrol hello numero di risultati che restituito in un'unica operazione di elenco, è possibile elencare i BLOB di pagine di risultati.</span><span class="sxs-lookup"><span data-stu-id="7bd86-162">If you are listing a large number of blobs, or you want toocontrol hello number of results you return in one listing operation, you can list blobs in pages of results.</span></span> <span data-ttu-id="7bd86-163">Questo esempio mostra la vista tooreturn dei risultati nelle pagine in modo asincrono, in modo che non l'esecuzione viene bloccata durante l'attesa tooreturn un ampio set di risultati.</span><span class="sxs-lookup"><span data-stu-id="7bd86-163">This example shows how tooreturn results in pages asynchronously, so that execution is not blocked while waiting tooreturn a large set of results.</span></span>

<span data-ttu-id="7bd86-164">Questo esempio viene illustrato un semplice elenco di blob, ma è anche possibile eseguire un elenco gerarchico, impostazione hello _useFlatBlobListing_ parametro di hello **ListBlobsSegmentedAsync** too_false_ metodo.</span><span class="sxs-lookup"><span data-stu-id="7bd86-164">This example shows a flat blob listing, but you can also perform a hierarchical listing, by setting hello _useFlatBlobListing_ parameter of hello **ListBlobsSegmentedAsync** method too_false_.</span></span>

<span data-ttu-id="7bd86-165">Poiché l'esempio hello chiama un metodo asincrono, devono essere preceduto da hello _async_ (parola chiave) e deve restituire un **attività** oggetto.</span><span class="sxs-lookup"><span data-stu-id="7bd86-165">Because hello sample method calls an asynchronous method, it must be prefaced with hello _async_ keyword, and it must return a **Task** object.</span></span> <span data-ttu-id="7bd86-166">Hello await (parola chiave) specificato per hello **ListBlobsSegmentedAsync** metodo sospende l'esecuzione del metodo di esempio hello fino al completamento hello elenco attività.</span><span class="sxs-lookup"><span data-stu-id="7bd86-166">hello await keyword specified for hello **ListBlobsSegmentedAsync** method suspends execution of hello sample method until hello listing task completes.</span></span>

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

## <a name="writing-tooan-append-blob"></a><span data-ttu-id="7bd86-167">Scrittura tooan aggiungere blob</span><span class="sxs-lookup"><span data-stu-id="7bd86-167">Writing tooan append blob</span></span>
<span data-ttu-id="7bd86-168">Un blob di accodamento è ottimizzato per le operazioni di accodamento, ad esempio la registrazione.</span><span class="sxs-lookup"><span data-stu-id="7bd86-168">An append blob is optimized for append operations, such as logging.</span></span> <span data-ttu-id="7bd86-169">Come un blob in blocchi, un blob di aggiunta è costituito da blocchi, ma quando si aggiunge un nuovo blob in blocchi tooan accodamento, è sempre aggiunte toohello fine del blob hello.</span><span class="sxs-lookup"><span data-stu-id="7bd86-169">Like a block blob, an append blob is comprised of blocks, but when you add a new block tooan append blob, it is always appended toohello end of hello blob.</span></span> <span data-ttu-id="7bd86-170">È possibile aggiornare o eliminare un blocco esistente in un blob di Accodamento.</span><span class="sxs-lookup"><span data-stu-id="7bd86-170">You cannot update or delete an existing block in an append blob.</span></span> <span data-ttu-id="7bd86-171">ID blocco Hello per un blob di aggiunta non vengono esposte come se fossero per un blob in blocchi.</span><span class="sxs-lookup"><span data-stu-id="7bd86-171">hello block IDs for an append blob are not exposed as they are for a block blob.</span></span>

<span data-ttu-id="7bd86-172">Ogni blocco di un blob di aggiunta può avere dimensioni diverse, backup tooa massimo 4 MB, e un blob di aggiunta può includere un massimo di 50.000 blocchi.</span><span class="sxs-lookup"><span data-stu-id="7bd86-172">Each block in an append blob can be a different size, up tooa maximum of 4 MB, and an append blob can include a maximum of 50,000 blocks.</span></span> <span data-ttu-id="7bd86-173">dimensione massima di Hello di un blob di aggiunta è pertanto leggermente superiore a 195 GB (4 MB X 50.000 blocchi).</span><span class="sxs-lookup"><span data-stu-id="7bd86-173">hello maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).</span></span>

<span data-ttu-id="7bd86-174">esempio Hello seguente crea un nuovo blob di aggiunta e accoda tooit alcuni dati, simulazione di un'operazione di registrazione semplice.</span><span class="sxs-lookup"><span data-stu-id="7bd86-174">hello example below creates a new append blob and appends some data tooit, simulating a simple logging operation.</span></span>

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

<span data-ttu-id="7bd86-175">Vedere [informazioni sui BLOB in blocchi, BLOB di pagine e BLOB, accodare](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) per ulteriori informazioni sulle differenze di hello tra hello tre tipi di BLOB.</span><span class="sxs-lookup"><span data-stu-id="7bd86-175">See [Understanding Block Blobs, Page Blobs, and Append Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) for more information about hello differences between hello three types of blobs.</span></span>

## <a name="managing-security-for-blobs"></a><span data-ttu-id="7bd86-176">Gestione della sicurezza dei BLOB</span><span class="sxs-lookup"><span data-stu-id="7bd86-176">Managing security for blobs</span></span>
<span data-ttu-id="7bd86-177">Per impostazione predefinita, archiviazione di Azure i dati rimangono al sicuro limitando l'accesso toohello account proprietario, ovvero in possesso delle chiavi di accesso account hello.</span><span class="sxs-lookup"><span data-stu-id="7bd86-177">By default, Azure Storage keeps your data secure by limiting access toohello account owner, who is in possession of hello account access keys.</span></span> <span data-ttu-id="7bd86-178">Quando è necessario tooshare i dati blob nell'account di archiviazione, è importante toodo così senza compromettere la sicurezza hello di chiavi di accesso account.</span><span class="sxs-lookup"><span data-stu-id="7bd86-178">When you need tooshare blob data in your storage account, it is important toodo so without compromising hello security of your account access keys.</span></span> <span data-ttu-id="7bd86-179">Inoltre, è possibile crittografare tooensure dati blob che è sicuro passare rete hello e archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7bd86-179">Additionally, you can encrypt blob data tooensure that it is secure going over hello wire and in Azure Storage.</span></span>

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

### <a name="controlling-access-tooblob-data"></a><span data-ttu-id="7bd86-180">Controllo dell'accesso ai dati tooblob</span><span class="sxs-lookup"><span data-stu-id="7bd86-180">Controlling access tooblob data</span></span>
<span data-ttu-id="7bd86-181">Per impostazione predefinita, i dati blob hello nell'account di archiviazione sono accessibile solo proprietario dell'account toostorage.</span><span class="sxs-lookup"><span data-stu-id="7bd86-181">By default, hello blob data in your storage account is accessible only toostorage account owner.</span></span> <span data-ttu-id="7bd86-182">Autenticazione delle richieste nel servizio di archiviazione Blob richiede una chiave di accesso account hello per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="7bd86-182">Authenticating requests against Blob storage requires hello account access key by default.</span></span> <span data-ttu-id="7bd86-183">Tuttavia, è preferibile toomake determinati utenti tooother disponibili dati di blob.</span><span class="sxs-lookup"><span data-stu-id="7bd86-183">However, you may wish toomake certain blob data available tooother users.</span></span> <span data-ttu-id="7bd86-184">Sono disponibili due opzioni:</span><span class="sxs-lookup"><span data-stu-id="7bd86-184">You have two options:</span></span>

* <span data-ttu-id="7bd86-185">**Accesso anonimo** : è possibile rendere disponibili pubblicamente per l'accesso anonimo un contenitore o i BLOB in esso inclusi.</span><span class="sxs-lookup"><span data-stu-id="7bd86-185">**Anonymous access:** You can make a container or its blobs publicly available for anonymous access.</span></span> <span data-ttu-id="7bd86-186">Vedere [gestire BLOB e accesso in lettura anonimo toocontainers](storage-manage-access-to-resources.md) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="7bd86-186">See [Manage anonymous read access toocontainers and blobs](storage-manage-access-to-resources.md) for more information.</span></span>
* <span data-ttu-id="7bd86-187">**Firme di accesso condiviso:** è possibile fornire ai client con una firma di accesso condiviso (SAS), che fornisce l'accesso delegato tooa risorse nell'account di archiviazione, con le autorizzazioni specificate e in un intervallo di tempo specificato.</span><span class="sxs-lookup"><span data-stu-id="7bd86-187">**Shared access signatures:** You can provide clients with a shared access signature (SAS), which provides delegated access tooa resource in your storage account, with permissions that you specify and over an interval that you specify.</span></span> <span data-ttu-id="7bd86-188">Vedere [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) (Uso di firme di accesso condiviso) per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="7bd86-188">See [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) for more information.</span></span>

### <a name="encrypting-blob-data"></a><span data-ttu-id="7bd86-189">Crittografia dei dati BLOB</span><span class="sxs-lookup"><span data-stu-id="7bd86-189">Encrypting blob data</span></span>
<span data-ttu-id="7bd86-190">Archiviazione di Azure supporta la crittografia dei dati blob sia nel client hello hello server:</span><span class="sxs-lookup"><span data-stu-id="7bd86-190">Azure Storage supports encrypting blob data both at hello client and on hello server:</span></span>

* <span data-ttu-id="7bd86-191">**Crittografia client-side:** hello libreria Client di archiviazione per .NET supporta la crittografia dei dati all'interno delle applicazioni client prima di caricare tooAzure Storage e la decrittografia dei dati durante il download toohello client.</span><span class="sxs-lookup"><span data-stu-id="7bd86-191">**Client-side encryption:** hello Storage Client Library for .NET supports encrypting data within client applications before uploading tooAzure Storage, and decrypting data while downloading toohello client.</span></span> <span data-ttu-id="7bd86-192">libreria Hello supporta inoltre l'integrazione con l'insieme di credenziali chiave di Azure per la gestione di chiave account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7bd86-192">hello library also supports integration with Azure Key Vault for storage account key management.</span></span> <span data-ttu-id="7bd86-193">Per altre informazioni, vedere [Crittografia lato client con .NET per Archiviazione di Microsoft Azure](storage-client-side-encryption.md) .</span><span class="sxs-lookup"><span data-stu-id="7bd86-193">See [Client-Side Encryption with .NET for Microsoft Azure Storage](storage-client-side-encryption.md) for more information.</span></span> <span data-ttu-id="7bd86-194">Vedere anche [Esercitazione: Crittografare e decrittografare i BLOB in Archiviazione di Microsoft Azure tramite l'insieme di credenziali delle chiavi di Azure](storage-encrypt-decrypt-blobs-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="7bd86-194">Also see [Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault](storage-encrypt-decrypt-blobs-key-vault.md).</span></span>
* <span data-ttu-id="7bd86-195">**Crittografia lato server**: Archiviazione di Azure supporta ora la crittografia lato server.</span><span class="sxs-lookup"><span data-stu-id="7bd86-195">**Server-side encryption**: Azure Storage now supports server-side encryption.</span></span> <span data-ttu-id="7bd86-196">Vedere [Crittografia del servizio di archiviazione di Azure per dati inattivi (anteprima)](storage-service-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="7bd86-196">See [Azure Storage Service Encryption for Data at Rest (Preview)](storage-service-encryption.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7bd86-197">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7bd86-197">Next steps</span></span>
<span data-ttu-id="7bd86-198">Ora che si è appreso i concetti di base di hello dell'archiviazione Blob, seguire questi ulteriori toolearn di collegamenti.</span><span class="sxs-lookup"><span data-stu-id="7bd86-198">Now that you've learned hello basics of Blob storage, follow these links toolearn more.</span></span>

### <a name="microsoft-azure-storage-explorer"></a><span data-ttu-id="7bd86-199">Microsoft Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="7bd86-199">Microsoft Azure Storage Explorer</span></span>
* <span data-ttu-id="7bd86-200">[Microsoft Azure Storage Explorer (MASE)](../vs-azure-tools-storage-manage-with-storage-explorer.md) è un'app autonoma, disponibile da Microsoft che consente di toowork visivamente i dati di archiviazione di Azure in Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="7bd86-200">[Microsoft Azure Storage Explorer (MASE)](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

### <a name="blob-storage-samples"></a><span data-ttu-id="7bd86-201">Esempi di archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="7bd86-201">Blob storage samples</span></span>
* [<span data-ttu-id="7bd86-202">Getting Started with Azure Blob Storage in .NET (Introduzione all'archiviazione BLOB di Azure in .NET)</span><span class="sxs-lookup"><span data-stu-id="7bd86-202">Getting Started with Azure Blob Storage in .NET</span></span>](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)

### <a name="blob-storage-reference"></a><span data-ttu-id="7bd86-203">Informazioni di riferimento sull'archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="7bd86-203">Blob storage reference</span></span>
* [<span data-ttu-id="7bd86-204">Informazioni di riferimento sulla libreria client di archiviazione per .NET</span><span class="sxs-lookup"><span data-stu-id="7bd86-204">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/mt347887.aspx)
* [<span data-ttu-id="7bd86-205">Informazioni di riferimento sulle API REST</span><span class="sxs-lookup"><span data-stu-id="7bd86-205">REST API reference</span></span>](/rest/api/storageservices/azure-storage-services-rest-api-reference)

### <a name="conceptual-guides"></a><span data-ttu-id="7bd86-206">Guide concettuali</span><span class="sxs-lookup"><span data-stu-id="7bd86-206">Conceptual guides</span></span>
* [<span data-ttu-id="7bd86-207">Trasferimento dati con hello utilità della riga di comando AzCopy</span><span class="sxs-lookup"><span data-stu-id="7bd86-207">Transfer data with hello AzCopy command-line utility</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="7bd86-208">Come usare l'archiviazione file di Azure</span><span class="sxs-lookup"><span data-stu-id="7bd86-208">Get started with File storage for .NET</span></span>](storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="7bd86-209">La modalità di archiviazione con blob di Azure toouse hello WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="7bd86-209">How toouse Azure blob storage with hello WebJobs SDK</span></span>](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
