---
title: Introduzione all'archiviazione BLOB e ai servizi connessi di Visual Studio (ASP.NET Core) | Microsoft Docs
description: Informazioni su come iniziare a usare l'archiviazione BLOB di Azure in un progetto ASP.NET Core in Visual Studio dopo aver creato un account di archiviazione con i servizi connessi di Visual Studio
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 094b596a-c92c-40c4-a0f5-86407ae79672
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 2e8060b44c395ad7c24e7778c0ef65148a3a45de
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="6011a-103">Introduzione all'archiviazione BLOB di Azure e ai relativi servizi di Visual Studio (ASP.NET Core)</span><span class="sxs-lookup"><span data-stu-id="6011a-103">Get started with Azure Blob storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="6011a-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="6011a-104">Overview</span></span>
<span data-ttu-id="6011a-105">Questo articolo descrive come iniziare a usare l'archiviazione BLOB di Azure in Visual Studio dopo aver creato o fatto riferimento a un account di archiviazione di Azure in un progetto ASP.NET Core usando la finestra di dialogo Aggiungi servizi connessi di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6011a-105">This article describes how to get started using Azure Blob storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using the Visual Studio Add Connected Services dialog.</span></span>

<span data-ttu-id="6011a-106">L'archiviazione BLOB di Azure è un servizio per l'archiviazione di quantità elevate di dati non strutturati a cui è possibile accedere da qualsiasi parte del mondo tramite HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6011a-106">Azure Blob storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="6011a-107">Un singolo BLOB può avere qualsiasi dimensione.</span><span class="sxs-lookup"><span data-stu-id="6011a-107">A single blob can be any size.</span></span> <span data-ttu-id="6011a-108">I BLOB possono essere costituiti da immagini, file audio e video, dati non elaborati e file di documento.</span><span class="sxs-lookup"><span data-stu-id="6011a-108">Blobs can be things like images, audio and video files, raw data, and document files.</span></span> <span data-ttu-id="6011a-109">Questo articolo descrive come iniziare a usare l'archiviazione BLOB dopo la creazione di un account di archiviazione di Azure usando la finestra di dialogo **Aggiungi servizi connessi** di Visual Studio in un progetto ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="6011a-109">This article describes how to get started with blob storage after you create an Azure storage account by using the Visual Studio **Add Connected Services** dialog in an ASP.NET Core project.</span></span>

<span data-ttu-id="6011a-110">I BLOB di archiviazione si trovano nei contenitori esattamente come i file si trovano nelle cartelle.</span><span class="sxs-lookup"><span data-stu-id="6011a-110">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="6011a-111">Dopo aver creato una risorsa di archiviazione, è possibile creare uno o più contenitori nello spazio di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="6011a-111">After you have created a storage, you create one or more containers in the storage.</span></span> <span data-ttu-id="6011a-112">Ad esempio, in una risorsa di archiviazione denominata "Raccoglitore" è possibile creare contenitori denominati "immagini" per archiviare immagini e un altro contenitore denominato "audio" per archiviare file audio.</span><span class="sxs-lookup"><span data-stu-id="6011a-112">For example, in a storage called "Scrapbook," you can create containers in the storage called "images" to store pictures and another called "audio" to store audio files.</span></span> <span data-ttu-id="6011a-113">Dopo la creazione dei contenitori, sarà possibile caricarvi singoli file BLOB.</span><span class="sxs-lookup"><span data-stu-id="6011a-113">After you create the containers, you can upload individual blob files to them.</span></span> <span data-ttu-id="6011a-114">Per altre informazioni sulla modifica dei BLOB a livello di codice, vedere [Introduzione all'archiviazione BLOB di Azure con .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) .</span><span class="sxs-lookup"><span data-stu-id="6011a-114">See [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) for more information on programmatically manipulating blobs.</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="6011a-115">Accesso ai contenitori BLOB nel codice</span><span class="sxs-lookup"><span data-stu-id="6011a-115">Access blob containers in code</span></span>
<span data-ttu-id="6011a-116">Per accedere ai BLOB a livello di codice nei progetti ASP.NET Core, è necessario aggiungere gli elementi seguenti, se non sono già presenti.</span><span class="sxs-lookup"><span data-stu-id="6011a-116">To programmatically access blobs in ASP.NET Core projects, you need to add the following items, if they're not already present.</span></span>

1. <span data-ttu-id="6011a-117">Aggiungere le dichiarazioni dello spazio dei nomi del codice seguenti all'inizio del file C# in cui si desidera accedere ad Archiviazione di Azure a livello di codice:</span><span class="sxs-lookup"><span data-stu-id="6011a-117">Add the following code namespace declarations to the top of any C# file in which you want to programmatically access Azure storage.</span></span>
   
        using Microsoft.Extensions.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Extensions.Logging.LogLevel;
2. <span data-ttu-id="6011a-118">Ottenere un oggetto **CloudStorageAccount** che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="6011a-118">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="6011a-119">Usare il codice seguente per ottenere la stringa di connessione di archiviazione e le informazioni sull'account di archiviazione dalla configurazione del servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="6011a-119">Use the following code to get your storage connection string and storage account information from the Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = new CloudStorageAccount(
            new Microsoft.WindowsAzure.Storage.Auth.StorageCredentials(
            "<storage-account-name>",
            "<access-key>"), true);
   
    <span data-ttu-id="6011a-120">**NOTA:** utilizzare tutto il codice riportato in precedenza prima del codice indicato nelle sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="6011a-120">**NOTE:** Use all of the above code in front of the code in the following sections.</span></span>
3. <span data-ttu-id="6011a-121">Usare un oggetto **CloudBlobClient** per ottenere un riferimento **CloudBlobContainer** a un contenitore esistente nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="6011a-121">Use a **CloudBlobClient** object to get a **CloudBlobContainer** reference to an existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
   
        // Get a reference to a container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

## <a name="create-a-container-in-code"></a><span data-ttu-id="6011a-122">Creazione di un contenitore nel codice</span><span class="sxs-lookup"><span data-stu-id="6011a-122">Create a container in code</span></span>
<span data-ttu-id="6011a-123">È inoltre possibile utilizzare **CloudBlobClient** per creare un contenitore nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="6011a-123">You can also use the **CloudBlobClient** to create a container in your storage account.</span></span> <span data-ttu-id="6011a-124">È sufficiente aggiungere un richiamo a **CreateIfNotExistsAsync** come nel codice seguente:</span><span class="sxs-lookup"><span data-stu-id="6011a-124">All you need to do is to add a call to **CreateIfNotExistsAsync** as in the following code:</span></span>

    // Create a blob client.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    // Get a reference to a container named "my-new-container."
    CloudBlobContainer container = blobClient.GetContainerReference("my-new-container");

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="6011a-125">**NOTA:** le API che eseguono chiamate ad Archiviazione di Azure in ASP.NET Core sono asincrone.</span><span class="sxs-lookup"><span data-stu-id="6011a-125">**NOTE:** The APIs that perform calls to Azure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="6011a-126">Per ulteriori informazioni, vedere [Programmazione asincrona con Async e Await](http://msdn.microsoft.com/library/hh191443.aspx) .</span><span class="sxs-lookup"><span data-stu-id="6011a-126">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="6011a-127">Nel codice riportato di seguito si presuppone vengano utilizzati i metodi di programmazione asincrona.</span><span class="sxs-lookup"><span data-stu-id="6011a-127">The code below assumes async programming methods are being used.</span></span>

<span data-ttu-id="6011a-128">Per rendere i file all'interno del contenitore disponibili a tutti, è possibile impostare il contenitore come pubblico utilizzando il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="6011a-128">To make the files within the container available to everyone, you can set the container to be public by using the following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="6011a-129">Caricare un BLOB in un contenitore</span><span class="sxs-lookup"><span data-stu-id="6011a-129">Upload a blob into a container</span></span>
<span data-ttu-id="6011a-130">Per caricare un file BLOB in un contenitore, ottenere un riferimento a un contenitore e usarlo per ottenere un riferimento a un BLOB.</span><span class="sxs-lookup"><span data-stu-id="6011a-130">To upload a blob file into a container, get a container reference and use it to get a blob reference.</span></span> <span data-ttu-id="6011a-131">Dopo aver ottenuto un riferimento al BLOB, sarà possibile caricarvi qualsiasi flusso di dati chiamando il metodo **UploadFromStreamAsync** .</span><span class="sxs-lookup"><span data-stu-id="6011a-131">After you have a blob reference, you can upload any stream of data to it by calling the **UploadFromStreamAsync** method.</span></span> <span data-ttu-id="6011a-132">Questa operazione crea il BLOB, se non esiste già, oppure lo sovrascrive se esiste già.</span><span class="sxs-lookup"><span data-stu-id="6011a-132">This operation creates the blob if it's not already there, or overwrites it if it does exist.</span></span> <span data-ttu-id="6011a-133">Nell'esempio seguente viene illustrato come caricare un BLOB in un contenitore e si presuppone che il contenitore sia già stato creato.</span><span class="sxs-lookup"><span data-stu-id="6011a-133">The following example shows how to upload a blob into a container and assumes that the container was already created.</span></span>

    // Get a reference to a blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite the "myblob" blob with the contents of a local file
    // named "myfile".
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        await blockBlob.UploadFromStreamAsync(fileStream);
    }

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="6011a-134">Elencare i BLOB in un contenitore</span><span class="sxs-lookup"><span data-stu-id="6011a-134">List the blobs in a container</span></span>
<span data-ttu-id="6011a-135">Per elencare i BLOB in un contenitore, ottenere prima un riferimento al contenitore.</span><span class="sxs-lookup"><span data-stu-id="6011a-135">To list the blobs in a container, first get a container reference.</span></span> <span data-ttu-id="6011a-136">Sarà quindi possibile chiamare il metodo **ListBlobsSegmentedAsync** del contenitore per recuperare i BLOB e/o le directory disponibili.</span><span class="sxs-lookup"><span data-stu-id="6011a-136">You can then call the container's **ListBlobsSegmentedAsync** method to retrieve the blobs and/or directories within it.</span></span> <span data-ttu-id="6011a-137">Per accedere all'insieme avanzato di proprietà e metodi per un oggetto **IListBlobItem** restituito, è necessario eseguirne il cast in un oggetto **CloudBlockBlob**, **CloudPageBlob** o **CloudBlobDirectory**.</span><span class="sxs-lookup"><span data-stu-id="6011a-137">To access the rich set of properties and methods for a returned **IListBlobItem**, you must cast it to a **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="6011a-138">Se il tipo del BLOB non è noto, è possibile usare un controllo del tipo per determinare quello in cui viene eseguito il cast.</span><span class="sxs-lookup"><span data-stu-id="6011a-138">If you don't know the blob type, you can use a type check to determine which to cast it to.</span></span> <span data-ttu-id="6011a-139">Nel codice seguente viene illustrato come recuperare e visualizzare l'URI di ogni elemento in un contenitore.</span><span class="sxs-lookup"><span data-stu-id="6011a-139">The following code demonstrates how to retrieve and output the URI of each item in a container.</span></span>

    BlobContinuationToken token = null;
    do
    {
        BlobResultSegment resultSegment = await container.ListBlobsSegmentedAsync(token);
        token = resultSegment.ContinuationToken;

        foreach (IListBlobItem item in resultSegment.Results)
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
    } while (token != null);

<span data-ttu-id="6011a-140">È possibile elencare i contenuti di un contenitore BLOB in altri modi.</span><span class="sxs-lookup"><span data-stu-id="6011a-140">There are others ways to list the contents of a blob container.</span></span> <span data-ttu-id="6011a-141">Per altre informazioni, vedere [Introduzione all'archiviazione BLOB di Azure con .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) .</span><span class="sxs-lookup"><span data-stu-id="6011a-141">See [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) for more information.</span></span>

## <a name="download-a-blob"></a><span data-ttu-id="6011a-142">Scaricare un BLOB</span><span class="sxs-lookup"><span data-stu-id="6011a-142">Download a blob</span></span>
<span data-ttu-id="6011a-143">Per scaricare un BLOB, ottenere prima di tutto un riferimento al BLOB, quindi chiamare il metodo **DownloadToStreamAsync** .</span><span class="sxs-lookup"><span data-stu-id="6011a-143">To download a blob, first get a reference to the blob, and then call the **DownloadToStreamAsync** method.</span></span> <span data-ttu-id="6011a-144">Nell'esempio seguente viene utilizzato il metodo **DownloadToStreamAsync** per trasferire i contenuti del BLOB a un oggetto stream che è quindi possibile salvare come file locale.</span><span class="sxs-lookup"><span data-stu-id="6011a-144">The following example uses the **DownloadToStreamAsync** method to transfer the blob contents to a stream object that you can then save as a local file.</span></span>

    // Get a reference to a blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save the blob contents to a file named "myfile".
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        await blockBlob.DownloadToStreamAsync(fileStream);
    }

<span data-ttu-id="6011a-145">È possibile salvare i BLOB come file in altri modi.</span><span class="sxs-lookup"><span data-stu-id="6011a-145">There are other ways to save blobs as files.</span></span> <span data-ttu-id="6011a-146">Per altre informazioni, vedere [Introduzione all'archiviazione BLOB di Azure con .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs) .</span><span class="sxs-lookup"><span data-stu-id="6011a-146">See [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs) for more information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="6011a-147">Eliminare un BLOB</span><span class="sxs-lookup"><span data-stu-id="6011a-147">Delete a blob</span></span>
<span data-ttu-id="6011a-148">Per eliminare un BLOB, ottenere prima di tutto un riferimento al BLOB, quindi chiamare il metodo **DeleteAsync** .</span><span class="sxs-lookup"><span data-stu-id="6011a-148">To delete a blob, first get a reference to the blob, and then call the **DeleteAsync** method on it.</span></span>

    // Get a reference to a blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete the blob.
    await blockBlob.DeleteAsync();

## <a name="next-steps"></a><span data-ttu-id="6011a-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6011a-149">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

