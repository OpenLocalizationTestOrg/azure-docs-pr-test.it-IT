---
title: aaaGet generali di archiviazione blob e Visual Studio (ASP.NET Core) di servizi connessi | Documenti Microsoft
description: "La modalità di avvio utilizzando l'archiviazione Blob di Azure in un progetto di Visual Studio ASP.NET Core dopo aver creato un account di archiviazione usando Visual Studio tooget servizi connessi"
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
ms.openlocfilehash: 8eedf331896b21658c7b30a68a4391d8d60cd729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="5f1a8-103">Introduzione all'archiviazione BLOB di Azure e ai relativi servizi di Visual Studio (ASP.NET Core)</span><span class="sxs-lookup"><span data-stu-id="5f1a8-103">Get started with Azure Blob storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="5f1a8-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="5f1a8-104">Overview</span></span>
<span data-ttu-id="5f1a8-105">Questo articolo descrive la modalità di avvio con archiviazione Blob di Azure in Visual Studio dopo aver creato o a cui fa riferimento a un account di archiviazione di Azure in un progetto ASP.NET Core utilizzando la finestra di Visual Studio aggiungere servizi connessi hello tooget.</span><span class="sxs-lookup"><span data-stu-id="5f1a8-105">This article describes how tooget started using Azure Blob storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using hello Visual Studio Add Connected Services dialog.</span></span>

<span data-ttu-id="5f1a8-106">Archiviazione Blob di Azure è un servizio per l'archiviazione di grandi quantità di dati non strutturati che è possibile accedere da qualsiasi in HelloWorld tramite HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="5f1a8-106">Azure Blob storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="5f1a8-107">Un singolo BLOB può avere qualsiasi dimensione.</span><span class="sxs-lookup"><span data-stu-id="5f1a8-107">A single blob can be any size.</span></span> <span data-ttu-id="5f1a8-108">I BLOB possono essere costituiti da immagini, file audio e video, dati non elaborati e file di documento.</span><span class="sxs-lookup"><span data-stu-id="5f1a8-108">Blobs can be things like images, audio and video files, raw data, and document files.</span></span> <span data-ttu-id="5f1a8-109">Questo articolo descrive la modalità di avvio tooget con archiviazione blob dopo aver creato un account di archiviazione di Azure tramite Visual Studio hello **aggiungere servizi connessi** finestra di dialogo in un progetto ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="5f1a8-109">This article describes how tooget started with blob storage after you create an Azure storage account by using hello Visual Studio **Add Connected Services** dialog in an ASP.NET Core project.</span></span>

<span data-ttu-id="5f1a8-110">I BLOB di archiviazione si trovano nei contenitori esattamente come i file si trovano nelle cartelle.</span><span class="sxs-lookup"><span data-stu-id="5f1a8-110">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="5f1a8-111">Dopo aver creato uno spazio di archiviazione, creare uno o più contenitori in archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="5f1a8-111">After you have created a storage, you create one or more containers in hello storage.</span></span> <span data-ttu-id="5f1a8-112">Ad esempio, nell'archiviazione chiamato "Raccoglitore", è possibile creare contenitori nel servizio di archiviazione hello chiamato immagini toostore "immagini" e un altro denominato "audio" toostore file audio.</span><span class="sxs-lookup"><span data-stu-id="5f1a8-112">For example, in a storage called "Scrapbook," you can create containers in hello storage called "images" toostore pictures and another called "audio" toostore audio files.</span></span> <span data-ttu-id="5f1a8-113">Dopo aver creato i contenitori di hello, è possibile caricare blob singoli file toothem.</span><span class="sxs-lookup"><span data-stu-id="5f1a8-113">After you create hello containers, you can upload individual blob files toothem.</span></span> <span data-ttu-id="5f1a8-114">Per altre informazioni sulla modifica dei BLOB a livello di codice, vedere [Introduzione all'archiviazione BLOB di Azure con .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) .</span><span class="sxs-lookup"><span data-stu-id="5f1a8-114">See [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) for more information on programmatically manipulating blobs.</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="5f1a8-115">Accesso ai contenitori BLOB nel codice</span><span class="sxs-lookup"><span data-stu-id="5f1a8-115">Access blob containers in code</span></span>
<span data-ttu-id="5f1a8-116">tooprogrammatically Accedi ai BLOB in progetti ASP.NET Core, è necessario hello tooadd elementi, se non sono già presenti.</span><span class="sxs-lookup"><span data-stu-id="5f1a8-116">tooprogrammatically access blobs in ASP.NET Core projects, you need tooadd hello following items, if they're not already present.</span></span>

1. <span data-ttu-id="5f1a8-117">Aggiungere hello seguente di codice lo spazio dei nomi dichiarazioni toohello superiore di qualsiasi file c# in cui si desidera tooprogrammatically archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5f1a8-117">Add hello following code namespace declarations toohello top of any C# file in which you want tooprogrammatically access Azure storage.</span></span>
   
        using Microsoft.Extensions.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Extensions.Logging.LogLevel;
2. <span data-ttu-id="5f1a8-118">Ottenere un oggetto **CloudStorageAccount** che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5f1a8-118">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="5f1a8-119">Utilizzare hello tooget di codice seguente la stringa di connessione di archiviazione e informazioni sull'account di archiviazione dalla configurazione del servizio Azure hello.</span><span class="sxs-lookup"><span data-stu-id="5f1a8-119">Use hello following code tooget your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = new CloudStorageAccount(
            new Microsoft.WindowsAzure.Storage.Auth.StorageCredentials(
            "<storage-account-name>",
            "<access-key>"), true);
   
    <span data-ttu-id="5f1a8-120">**Nota:** utilizzare tutti hello sopra codice codice hello in hello le sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="5f1a8-120">**NOTE:** Use all of hello above code in front of hello code in hello following sections.</span></span>
3. <span data-ttu-id="5f1a8-121">Utilizzare un **CloudBlobClient** oggetto tooget un **CloudBlobContainer** contenitore esistente tooan di riferimento nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5f1a8-121">Use a **CloudBlobClient** object tooget a **CloudBlobContainer** reference tooan existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

## <a name="create-a-container-in-code"></a><span data-ttu-id="5f1a8-122">Creazione di un contenitore nel codice</span><span class="sxs-lookup"><span data-stu-id="5f1a8-122">Create a container in code</span></span>
<span data-ttu-id="5f1a8-123">È inoltre possibile utilizzare hello **CloudBlobClient** toocreate un contenitore nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5f1a8-123">You can also use hello **CloudBlobClient** toocreate a container in your storage account.</span></span> <span data-ttu-id="5f1a8-124">È sufficiente toodo è una chiamata tooadd troppo**CreateIfNotExistsAsync** come hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="5f1a8-124">All you need toodo is tooadd a call too**CreateIfNotExistsAsync** as in hello following code:</span></span>

    // Create a blob client.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    // Get a reference tooa container named "my-new-container."
    CloudBlobContainer container = blobClient.GetContainerReference("my-new-container");

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="5f1a8-125">**Nota:** hello API che eseguono chiamate tooAzure archiviazione in ASP.NET Core sono asincrone.</span><span class="sxs-lookup"><span data-stu-id="5f1a8-125">**NOTE:** hello APIs that perform calls tooAzure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="5f1a8-126">Per ulteriori informazioni, vedere [Programmazione asincrona con Async e Await](http://msdn.microsoft.com/library/hh191443.aspx) .</span><span class="sxs-lookup"><span data-stu-id="5f1a8-126">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="5f1a8-127">codice Hello riportato di seguito si presuppone che vengono utilizzati i metodi di programmazione asincrono.</span><span class="sxs-lookup"><span data-stu-id="5f1a8-127">hello code below assumes async programming methods are being used.</span></span>

<span data-ttu-id="5f1a8-128">toomake hello i file all'interno hello contenitore disponibili tooeveryone, è possibile impostare hello contenitore toobe pubblica utilizzando hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="5f1a8-128">toomake hello files within hello container available tooeveryone, you can set hello container toobe public by using hello following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="5f1a8-129">Caricare un BLOB in un contenitore</span><span class="sxs-lookup"><span data-stu-id="5f1a8-129">Upload a blob into a container</span></span>
<span data-ttu-id="5f1a8-130">tooupload un file blob in un contenitore, ottenere un riferimento a un contenitore e usarlo tooget un riferimento di blob.</span><span class="sxs-lookup"><span data-stu-id="5f1a8-130">tooupload a blob file into a container, get a container reference and use it tooget a blob reference.</span></span> <span data-ttu-id="5f1a8-131">Dopo aver ottenuto un riferimento di blob, è possibile caricare qualsiasi flusso di dati tooit dal chiamante hello **UploadFromStreamAsync** metodo.</span><span class="sxs-lookup"><span data-stu-id="5f1a8-131">After you have a blob reference, you can upload any stream of data tooit by calling hello **UploadFromStreamAsync** method.</span></span> <span data-ttu-id="5f1a8-132">Questa operazione crea blob hello se è già presente, o lo sovrascrive se esiste.</span><span class="sxs-lookup"><span data-stu-id="5f1a8-132">This operation creates hello blob if it's not already there, or overwrites it if it does exist.</span></span> <span data-ttu-id="5f1a8-133">Hello seguente esempio viene illustrato come tooupload un blob in un contenitore e si presuppone che il contenitore hello è già stato creato.</span><span class="sxs-lookup"><span data-stu-id="5f1a8-133">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>

    // Get a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with hello contents of a local file
    // named "myfile".
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        await blockBlob.UploadFromStreamAsync(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="5f1a8-134">Elenco di BLOB hello in un contenitore</span><span class="sxs-lookup"><span data-stu-id="5f1a8-134">List hello blobs in a container</span></span>
<span data-ttu-id="5f1a8-135">BLOB di hello toolist in un contenitore, prima di ottenere un riferimento di contenitore.</span><span class="sxs-lookup"><span data-stu-id="5f1a8-135">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="5f1a8-136">È quindi possibile chiamare del contenitore hello **ListBlobsSegmentedAsync** BLOB hello tooretrieve di metodo e/o directory all'interno di esso.</span><span class="sxs-lookup"><span data-stu-id="5f1a8-136">You can then call hello container's **ListBlobsSegmentedAsync** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="5f1a8-137">set completo di proprietà e metodi per un tipo restituito di hello tooaccess **IListBlobItem**, è necessario eseguirne il cast tooa **CloudBlockBlob**, **CloudPageBlob**, o  **CloudBlobDirectory** oggetto.</span><span class="sxs-lookup"><span data-stu-id="5f1a8-137">tooaccess hello rich set of properties and methods for a returned **IListBlobItem**, you must cast it tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="5f1a8-138">Se non si conosce blob hello tipo, è possibile utilizzare un toodetermine di controllo di tipo cui toocast in.</span><span class="sxs-lookup"><span data-stu-id="5f1a8-138">If you don't know hello blob type, you can use a type check toodetermine which toocast it to.</span></span> <span data-ttu-id="5f1a8-139">Hello di codice seguente viene illustrato come tooretrieve e output di hello URI di ogni elemento in un contenitore.</span><span class="sxs-lookup"><span data-stu-id="5f1a8-139">hello following code demonstrates how tooretrieve and output hello URI of each item in a container.</span></span>

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

<span data-ttu-id="5f1a8-140">Esistono altri modi toolist hello contenuto un contenitore blob.</span><span class="sxs-lookup"><span data-stu-id="5f1a8-140">There are others ways toolist hello contents of a blob container.</span></span> <span data-ttu-id="5f1a8-141">Per altre informazioni, vedere [Introduzione all'archiviazione BLOB di Azure con .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) .</span><span class="sxs-lookup"><span data-stu-id="5f1a8-141">See [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) for more information.</span></span>

## <a name="download-a-blob"></a><span data-ttu-id="5f1a8-142">Scaricare un BLOB</span><span class="sxs-lookup"><span data-stu-id="5f1a8-142">Download a blob</span></span>
<span data-ttu-id="5f1a8-143">ottenere innanzitutto un blob di riferimento toohello toodownload un blob e quindi chiamare hello **DownloadToStreamAsync** metodo.</span><span class="sxs-lookup"><span data-stu-id="5f1a8-143">toodownload a blob, first get a reference toohello blob, and then call hello **DownloadToStreamAsync** method.</span></span> <span data-ttu-id="5f1a8-144">esempio Hello utilizza hello **DownloadToStreamAsync** metodo tootransfer hello blob contenuto tooa oggetto flusso che è quindi possibile salvare come file locale.</span><span class="sxs-lookup"><span data-stu-id="5f1a8-144">hello following example uses hello **DownloadToStreamAsync** method tootransfer hello blob contents tooa stream object that you can then save as a local file.</span></span>

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save hello blob contents tooa file named "myfile".
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        await blockBlob.DownloadToStreamAsync(fileStream);
    }

<span data-ttu-id="5f1a8-145">Esistono altri modi toosave BLOB come file.</span><span class="sxs-lookup"><span data-stu-id="5f1a8-145">There are other ways toosave blobs as files.</span></span> <span data-ttu-id="5f1a8-146">Per altre informazioni, vedere [Introduzione all'archiviazione BLOB di Azure con .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs) .</span><span class="sxs-lookup"><span data-stu-id="5f1a8-146">See [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs) for more information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="5f1a8-147">Eliminare un BLOB</span><span class="sxs-lookup"><span data-stu-id="5f1a8-147">Delete a blob</span></span>
<span data-ttu-id="5f1a8-148">ottenere innanzitutto un blob di riferimento toohello toodelete un blob e quindi chiamare hello **DeleteAsync** metodo su di esso.</span><span class="sxs-lookup"><span data-stu-id="5f1a8-148">toodelete a blob, first get a reference toohello blob, and then call hello **DeleteAsync** method on it.</span></span>

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    await blockBlob.DeleteAsync();

## <a name="next-steps"></a><span data-ttu-id="5f1a8-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5f1a8-149">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

