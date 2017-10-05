---
title: Introduzione all'archiviazione BLOB e ai Servizi connessi di Visual Studio (servizi cloud) | Documentazione Microsoft
description: Informazioni su come iniziare a usare il servizio di archiviazione BLOB in un progetto di servizio di cloud in Visual Studio dopo aver eseguito la connessione a un account di archiviazione con i servizi connessi di Visual Studio.
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 1144a958-f75a-4466-bb21-320b7ae8f304
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: e154c81ef3765a3c006b3c27a979be881f14d0ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="d2b4c-103">Introduzione all’archiviazione BLOB di Azure e ai servizi connessi di Visual Studio (progetti servizi cloud)</span><span class="sxs-lookup"><span data-stu-id="d2b4c-103">Get started with Azure Blob Storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="d2b4c-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="d2b4c-104">Overview</span></span>
<span data-ttu-id="d2b4c-105">Questo articolo descrive come iniziare a usare l'archiviazione BLOB di Azure dopo aver creato o fatto riferimento a un account di archiviazione di Azure usando la finestra di dialogo di Visual Studio per l' **aggiunta dei servizi connessi** in un progetto di servizi cloud di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-105">This article describes how to get started with Azure Blob Storage after you created or referenced an Azure Storage account by using the Visual Studio **Add Connected Services** dialog in a Visual Studio cloud services project.</span></span> <span data-ttu-id="d2b4c-106">Vi mostreremo come accedere e creare contenitori di BLOB e come eseguire attività comuni quali caricare, elencare e scaricare BLOB.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-106">We'll show you how to access and create blob containers, and how to perform common tasks like uploading, listing, and downloading blobs.</span></span> <span data-ttu-id="d2b4c-107">Negli esempi, scritti in C\#, viene usata la [libreria client di Archiviazione di Microsoft Azure per .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="d2b4c-107">The samples are written in C\# and use the [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="d2b4c-108">L'archiviazione BLOB di Azure è un servizio per l'archiviazione di quantità elevate di dati non strutturati a cui è possibile accedere da qualsiasi parte del mondo tramite HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-108">Azure Blob Storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="d2b4c-109">Un singolo BLOB può avere qualsiasi dimensione.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-109">A single blob can be any size.</span></span> <span data-ttu-id="d2b4c-110">I BLOB possono essere costituiti da immagini, file audio e video, dati non elaborati e file di documento.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-110">Blobs can be things like images, audio and video files, raw data, and document files.</span></span>

<span data-ttu-id="d2b4c-111">I BLOB di archiviazione si trovano nei contenitori esattamente come i file si trovano nelle cartelle.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-111">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="d2b4c-112">Dopo aver creato una risorsa di archiviazione, è possibile creare uno o più contenitori nello spazio di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-112">After you have created a storage, you create one or more containers in the storage.</span></span> <span data-ttu-id="d2b4c-113">Ad esempio, in una risorsa di archiviazione denominata "Raccoglitore" è possibile creare contenitori denominati "immagini" per archiviare immagini e un altro contenitore denominato "audio" per archiviare file audio.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-113">For example, in a storage called "Scrapbook," you can create containers in the storage called "images" to store pictures and another called "audio" to store audio files.</span></span> <span data-ttu-id="d2b4c-114">Dopo la creazione dei contenitori, sarà possibile caricarvi singoli file BLOB.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-114">After you create the containers, you can upload individual blob files to them.</span></span>

* <span data-ttu-id="d2b4c-115">Per altre informazioni sulla modifica dei BLOB a livello di codice, vedere [Introduzione all'archiviazione BLOB di Azure con .NET](storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="d2b4c-115">For more information on programmatically manipulating blobs, see [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md).</span></span>
* <span data-ttu-id="d2b4c-116">Per informazioni generali sull'Archiviazione di Azure, vedere [la documentazione relativa all'archiviazione](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="d2b4c-116">For general information about Azure Storage, see [Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>
* <span data-ttu-id="d2b4c-117">Per informazioni generali sui servizi cloud di Azure, vedere [la documentazione sui servizi cloud](https://azure.microsoft.com/documentation/services/cloud-services/).</span><span class="sxs-lookup"><span data-stu-id="d2b4c-117">For general information about Azure Cloud Services, see [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/).</span></span>
* <span data-ttu-id="d2b4c-118">Per altre informazioni sulla programmazione delle applicazioni ASP.NET, vedere [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="d2b4c-118">For more information about programming ASP.NET applications, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="d2b4c-119">Accesso ai contenitori BLOB nel codice</span><span class="sxs-lookup"><span data-stu-id="d2b4c-119">Access blob containers in code</span></span>
<span data-ttu-id="d2b4c-120">Per accedere ai BLOB a livello di codice nei progetti di servizio cloud, è necessario aggiungere gli elementi seguenti, se non sono già presenti.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-120">To programmatically access blobs in cloud service projects, you need to add the following items, if they're not already present.</span></span>

1. <span data-ttu-id="d2b4c-121">Aggiungere le seguenti dichiarazioni dello spazio dei nomi del codice all'inizio del file C# in cui si vuole accedere ad Archiviazione di Azure a livello di codice:</span><span class="sxs-lookup"><span data-stu-id="d2b4c-121">Add the following code namespace declarations to the top of any C# file in which you wish to programmatically access Azure Storage.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="d2b4c-122">Ottenere un oggetto **CloudStorageAccount** che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-122">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="d2b4c-123">Utilizzare il codice seguente per ottenere la stringa di connessione di archiviazione e le informazioni sull'account di archiviazione dalla configurazione del servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-123">Use the following code to get the your storage connection string and storage account information from the Azure service configuration.</span></span>
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        CloudConfigurationManager.GetSetting("<storage account name>_AzureStorageConnectionString"));
3. <span data-ttu-id="d2b4c-124">Ottenere un oggetto **CloudBlobClient** per fare riferimento a un contenitore esistente nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-124">Get a **CloudBlobClient** object to reference an existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
4. <span data-ttu-id="d2b4c-125">Ottenere un oggetto **CloudBlobContainer** per fare riferimento a un contenitore BLOB specifico.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-125">Get a **CloudBlobContainer** object to reference a specific blob container.</span></span>
   
        // Get a reference to a container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

> [!NOTE]
> <span data-ttu-id="d2b4c-126">Usare tutto il codice illustrato nella procedura precedente prima del codice illustrato nelle sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-126">Use all of the code shown in the previous procedure in front of the code shown in the following sections.</span></span>
> 
> 

## <a name="create-a-container-in-code"></a><span data-ttu-id="d2b4c-127">Creazione di un contenitore nel codice</span><span class="sxs-lookup"><span data-stu-id="d2b4c-127">Create a container in code</span></span>
> [!NOTE]
> <span data-ttu-id="d2b4c-128">Alcune API che eseguono chiamate ad Archiviazione di Azure in ASP.NET sono asincrone.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-128">Some APIs that perform calls out to Azure Storage in ASP.NET are asynchronous.</span></span> <span data-ttu-id="d2b4c-129">Per altre informazioni, vedere [Programmazione asincrona con Async e Await](http://msdn.microsoft.com/library/hh191443.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d2b4c-129">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="d2b4c-130">Il codice nell'esempio seguente presuppone che si stiano usando metodi di programmazione asincroni.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-130">The code in the following example assumes that you are using async programming methods.</span></span>
> 
> 

<span data-ttu-id="d2b4c-131">Per creare un contenitore nell'account di archiviazione, è sufficiente eseguire una chiamata a **CreateIfNotExistsAsync** come nel codice seguente:</span><span class="sxs-lookup"><span data-stu-id="d2b4c-131">To create a container in your storage account, all you need to do is add a call to **CreateIfNotExistsAsync** as in the following code:</span></span>

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="d2b4c-132">Per rendere i file all'interno del contenitore disponibili a tutti, è possibile impostare il contenitore come pubblico utilizzando il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-132">To make the files within the container available to everyone, you can set the container to be public by using the following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });


<span data-ttu-id="d2b4c-133">I BLOB in un contenitore pubblico sono visibili a tutti gli utenti di Internet, tuttavia è possibile modificarli o eliminarli solo se si dispone della chiave di accesso appropriata.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-133">Anyone on the Internet can see blobs in a public container, but you can modify or delete them only if you have the appropriate access key.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="d2b4c-134">Caricare un BLOB in un contenitore</span><span class="sxs-lookup"><span data-stu-id="d2b4c-134">Upload a blob into a container</span></span>
<span data-ttu-id="d2b4c-135">Archiviazione di Azure supporta BLOB in blocchi e BLOB di pagine.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-135">Azure Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="d2b4c-136">Nella maggior parte dei casi è consigliabile utilizzare il tipo di BLOB in blocchi.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-136">In the majority of cases, block blob is the recommended type to use.</span></span>

<span data-ttu-id="d2b4c-137">Per caricare un file in un BLOB in blocchi, ottenere un riferimento a un contenitore e utilizzarlo per ottenere un riferimento a un BLOB in blocchi.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-137">To upload a file to a block blob, get a container reference and use it to get a block blob reference.</span></span> <span data-ttu-id="d2b4c-138">Dopo aver ottenuto un riferimento al BLOB, sarà possibile caricarvi qualsiasi flusso di dati chiamando il metodo **UploadFromStream** .</span><span class="sxs-lookup"><span data-stu-id="d2b4c-138">Once you have a blob reference, you can upload any stream of data to it by calling the **UploadFromStream** method.</span></span> <span data-ttu-id="d2b4c-139">Questa operazione crea il BLOB, se non già esistente, o lo sovrascrive, se già esistente.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-139">This operation creates the blob if it didn't previously exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="d2b4c-140">Nell'esempio seguente viene illustrato come caricare un BLOB in un contenitore e si presuppone che il contenitore sia già stato creato.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-140">The following example shows how to upload a blob into a container and assumes that the container was already created.</span></span>

    // Retrieve a reference to a blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite the "myblob" blob with contents from a local file.
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        blockBlob.UploadFromStream(fileStream);
    }

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="d2b4c-141">Elencare i BLOB in un contenitore</span><span class="sxs-lookup"><span data-stu-id="d2b4c-141">List the blobs in a container</span></span>
<span data-ttu-id="d2b4c-142">Per elencare i BLOB in un contenitore, ottenere prima un riferimento al contenitore.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-142">To list the blobs in a container, first get a container reference.</span></span> <span data-ttu-id="d2b4c-143">Sarà quindi possibile utilizzare il metodo **ListBlobs** del contenitore per recuperare i BLOB e/o le directory in esso contenuti.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-143">You can then use the container's **ListBlobs** method to retrieve the blobs and/or directories within it.</span></span> <span data-ttu-id="d2b4c-144">Per accedere all'insieme avanzato di proprietà e metodi per un oggetto **IListBlobItem** restituito, è necessario eseguirne il cast in un oggetto **CloudBlockBlob**, **CloudPageBlob** o **CloudBlobDirectory**.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-144">To access the rich set of properties and methods for a  returned **IListBlobItem**, you must cast it to a **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="d2b4c-145">Se il tipo è sconosciuto, è possibile usare un controllo del tipo per determinare quello in cui viene eseguito il cast.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-145">If the type is unknown, you can use a type check to determine which to cast it to.</span></span> <span data-ttu-id="d2b4c-146">Nel codice seguente viene illustrato come recuperare e visualizzare l'URI di ogni elemento nel contenitore **photos** :</span><span class="sxs-lookup"><span data-stu-id="d2b4c-146">The following code demonstrates how to retrieve and output the URI of each item in the **photos** container:</span></span>

    // Loop over items within the container and output the length and URI.
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

<span data-ttu-id="d2b4c-147">Come illustrato nell'esempio di codice precedente, il servizio BLOB include anche il concetto di directory all'interno di contenitori.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-147">As shown in the previous code sample, the blob service has the concept of directories within containers, as well.</span></span> <span data-ttu-id="d2b4c-148">È quindi possibile organizzare i BLOB in una struttura più simile a quella delle cartelle.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-148">This is so that you can organize your blobs in a more folder-like structure.</span></span> <span data-ttu-id="d2b4c-149">Si consideri, ad esempio, il seguente set di BLOB in blocchi in un contenitore denominato **photos**:</span><span class="sxs-lookup"><span data-stu-id="d2b4c-149">For example, consider the following set of block blobs in a container named **photos**:</span></span>

    photo1.jpg
    2010/architecture/description.txt
    2010/architecture/photo3.jpg
    2010/architecture/photo4.jpg
    2011/architecture/photo5.jpg
    2011/architecture/photo6.jpg
    2011/architecture/description.txt
    2011/photo7.jpg

<span data-ttu-id="d2b4c-150">Quando si chiama **ListBlobs** sul contenitore (come nell'esempio precedente), la raccolta restituita conterrà gli oggetti **CloudBlobDirectory** e **CloudBlockBlob** che rappresentano le directory e i BLOB contenuti al primo livello.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-150">When you call **ListBlobs** on the container (as in the previous sample), the collection returned contains **CloudBlobDirectory** and **CloudBlockBlob** objects representing the directories and blobs contained at the top level.</span></span> <span data-ttu-id="d2b4c-151">Ecco l'output restituito:</span><span class="sxs-lookup"><span data-stu-id="d2b4c-151">Here is the resulting output:</span></span>

    Directory: https://<accountname>.blob.core.windows.net/photos/2010/
    Directory: https://<accountname>.blob.core.windows.net/photos/2011/
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg


<span data-ttu-id="d2b4c-152">Facoltativamente, è possibile impostare su **true** il parametro **UseFlatBlobListing** del metodo **ListBlobs**.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-152">Optionally, you can set the **UseFlatBlobListing** parameter of of the **ListBlobs** method to **true**.</span></span> <span data-ttu-id="d2b4c-153">In questo modo tutti i BLOB verranno restituiti come **CloudBlockBlob**, indipendentemente dalla directory.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-153">This results in every blob being returned as a **CloudBlockBlob**, regardless of directory.</span></span> <span data-ttu-id="d2b4c-154">Ecco la chiamata a **ListBlobs**:</span><span class="sxs-lookup"><span data-stu-id="d2b4c-154">Here is the call to **ListBlobs**:</span></span>

    // Loop over items within the container and output the length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, true))
    {
       ...
    }

<span data-ttu-id="d2b4c-155">e i relativi risultati:</span><span class="sxs-lookup"><span data-stu-id="d2b4c-155">and here are the results:</span></span>

    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
    Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
    Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
    Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
    Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
    Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg

<span data-ttu-id="d2b4c-156">Per altre informazioni, vedere [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).</span><span class="sxs-lookup"><span data-stu-id="d2b4c-156">For more information, see [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).</span></span>

## <a name="download-blobs"></a><span data-ttu-id="d2b4c-157">Scaricare BLOB</span><span class="sxs-lookup"><span data-stu-id="d2b4c-157">Download blobs</span></span>
<span data-ttu-id="d2b4c-158">Per scaricare BLOB, recuperare prima un riferimento al BLOB e quindi chiamare il metodo **DownloadToStream** .</span><span class="sxs-lookup"><span data-stu-id="d2b4c-158">To download blobs, first retrieve a blob reference and then call the **DownloadToStream** method.</span></span> <span data-ttu-id="d2b4c-159">Nell'esempio seguente il metodo **DownloadToStream** viene utilizzato per trasferire il contenuto del BLOB a un oggetto stream che è quindi possibile rendere persistente in un file locale.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-159">The following example uses the **DownloadToStream** method to transfer the blob contents to a stream object that you can then persist to a local file.</span></span>

    // Get a reference to a blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save blob contents to a file.
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        blockBlob.DownloadToStream(fileStream);
    }

<span data-ttu-id="d2b4c-160">È anche possibile utilizzare il metodo **DownloadToStream** per scaricare il contenuto di un BLOB come stringa di testo.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-160">You can also use the **DownloadToStream** method to download the contents of a blob as a text string.</span></span>

    // Get a reference to a blob named "myblob.txt"
    CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

    string text;
    using (var memoryStream = new MemoryStream())
    {
        blockBlob2.DownloadToStream(memoryStream);
        text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
    }

## <a name="delete-blobs"></a><span data-ttu-id="d2b4c-161">Eliminare BLOB</span><span class="sxs-lookup"><span data-stu-id="d2b4c-161">Delete blobs</span></span>
<span data-ttu-id="d2b4c-162">Per eliminare un BLOB, ottenere prima un riferimento al BLOB, poi chiamare il metodo **Delete** .</span><span class="sxs-lookup"><span data-stu-id="d2b4c-162">To delete a blob, first get a blob reference and then call the **Delete** method.</span></span>

    // Get a reference to a blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete the blob.
    blockBlob.Delete();


## <a name="list-blobs-in-pages-asynchronously"></a><span data-ttu-id="d2b4c-163">Elencare BLOB nelle pagine in modalità asincrona</span><span class="sxs-lookup"><span data-stu-id="d2b4c-163">List blobs in pages asynchronously</span></span>
<span data-ttu-id="d2b4c-164">Se si sta elencando un numero elevato di BLOB oppure si vuole controllare il numero di risultati restituiti in un'operazione di elenco, è possibile elencare i BLOB nelle pagine dei risultati.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-164">If you are listing a large number of blobs, or you want to control the number of results you return in one listing operation, you can list blobs in pages of results.</span></span> <span data-ttu-id="d2b4c-165">Questo esempio spiega come restituire i risultati nelle pagine in modalità asincrona, in modo che l'esecuzione non venga bloccata durante l'attesa della restituzione di un set di risultati di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-165">This example shows how to return results in pages asynchronously, so that execution is not blocked while waiting to return a large set of results.</span></span>

<span data-ttu-id="d2b4c-166">Questo esempio illustra un elenco di BLOB lineare, ma è anche possibile eseguire un elenco gerarchico semplicemente impostando il parametro **useFlatBlobListing** del metodo **ListBlobsSegmentedAsync** su **false**.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-166">This example shows a flat blob listing, but you can also perform a hierarchical listing, by setting the **useFlatBlobListing** parameter of the **ListBlobsSegmentedAsync** method to **false**.</span></span>

<span data-ttu-id="d2b4c-167">Poiché il metodo di esempio chiama un metodo asincrono, deve essere prefissato con la parola chiave **async** e restituire un oggetto **Attività**.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-167">Because the sample method calls an asynchronous method, it must be prefaced with the **async** keyword, and it must return a **Task** object.</span></span> <span data-ttu-id="d2b4c-168">La parola chiave di attesa specificata per il metodo **ListBlobsSegmentedAsync** sospende l'esecuzione del metodo di esempio fino al completamento dell'attività di elenco.</span><span class="sxs-lookup"><span data-stu-id="d2b4c-168">The await keyword specified for the **ListBlobsSegmentedAsync** method suspends execution of the sample method until the listing task completes.</span></span>

    async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
    {
        // List blobs to the console window, with paging.
        Console.WriteLine("List blobs in pages:");

        int i = 0;
        BlobContinuationToken continuationToken = null;
        BlobResultSegment resultSegment = null;

        // Call ListBlobsSegmentedAsync and enumerate the result segment returned, while the continuation token is non-null.
        // When the continuation token is null, the last page has been returned and execution can exit the loop.
        do
        {
            // This overload allows control of the page size. You can return all remaining results by passing null for the maxResults parameter,
            // or by calling a different overload.
            resultSegment = await container.ListBlobsSegmentedAsync("", true, BlobListingDetails.All, 10, continuationToken, null, null);
            if (resultSegment.Results.Count<IListBlobItem>() > 0) { Console.WriteLine("Page {0}:", ++i); }
            foreach (var blobItem in resultSegment.Results)
            {
                Console.WriteLine("\t{0}", blobItem.StorageUri.PrimaryUri);
            }
            Console.WriteLine();

            //Get the continuation token.
            continuationToken = resultSegment.ContinuationToken;
        }
        while (continuationToken != null);
    }

## <a name="next-steps"></a><span data-ttu-id="d2b4c-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d2b4c-169">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

