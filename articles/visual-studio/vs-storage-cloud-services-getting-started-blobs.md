---
title: aaaGet avviato con Visual Studio e di archiviazione blob di servizi connessi (servizi cloud) | Documenti Microsoft
description: "La modalità di avvio tooget utilizzo dell'archiviazione Blob di Azure in un progetto di servizio cloud in Visual Studio dopo la connessione di account di archiviazione tooa utilizzando Visual Studio di servizi connessi"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1144a958-f75a-4466-bb21-320b7ae8f304
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 158197a9d49bc4f26841d689405529192c52f529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="50bc7-103">Introduzione all’archiviazione BLOB di Azure e ai servizi connessi di Visual Studio (progetti servizi cloud)</span><span class="sxs-lookup"><span data-stu-id="50bc7-103">Get started with Azure Blob Storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="50bc7-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="50bc7-104">Overview</span></span>
<span data-ttu-id="50bc7-105">Questo articolo descrive la modalità di avvio tooget con archiviazione Blob di Azure dopo aver creato o a cui fa riferimento a un account di archiviazione di Azure tramite Visual Studio hello **aggiungere servizi connessi** progetto di servizi di finestra di dialogo in un cloud di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="50bc7-105">This article describes how tooget started with Azure Blob Storage after you created or referenced an Azure Storage account by using hello Visual Studio **Add Connected Services** dialog in a Visual Studio cloud services project.</span></span> <span data-ttu-id="50bc7-106">Vi mostreremo come tooaccess e creare contenitori blob e come attività comuni tooperform caricamento, visualizzazione e il download di BLOB.</span><span class="sxs-lookup"><span data-stu-id="50bc7-106">We'll show you how tooaccess and create blob containers, and how tooperform common tasks like uploading, listing, and downloading blobs.</span></span> <span data-ttu-id="50bc7-107">Hello esempi sono scritti in C\# e utilizzare hello [Microsoft Azure Storage Client Library per .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="50bc7-107">hello samples are written in C\# and use hello [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="50bc7-108">Archiviazione Blob di Azure è un servizio per l'archiviazione di grandi quantità di dati non strutturati che è possibile accedere da qualsiasi in HelloWorld tramite HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="50bc7-108">Azure Blob Storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="50bc7-109">Un singolo BLOB può avere qualsiasi dimensione.</span><span class="sxs-lookup"><span data-stu-id="50bc7-109">A single blob can be any size.</span></span> <span data-ttu-id="50bc7-110">I BLOB possono essere costituiti da immagini, file audio e video, dati non elaborati e file di documento.</span><span class="sxs-lookup"><span data-stu-id="50bc7-110">Blobs can be things like images, audio and video files, raw data, and document files.</span></span>

<span data-ttu-id="50bc7-111">I BLOB di archiviazione si trovano nei contenitori esattamente come i file si trovano nelle cartelle.</span><span class="sxs-lookup"><span data-stu-id="50bc7-111">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="50bc7-112">Dopo aver creato uno spazio di archiviazione, creare uno o più contenitori in archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="50bc7-112">After you have created a storage, you create one or more containers in hello storage.</span></span> <span data-ttu-id="50bc7-113">Ad esempio, nell'archiviazione chiamato "Raccoglitore", è possibile creare contenitori nel servizio di archiviazione hello chiamato immagini toostore "immagini" e un altro denominato "audio" toostore file audio.</span><span class="sxs-lookup"><span data-stu-id="50bc7-113">For example, in a storage called "Scrapbook," you can create containers in hello storage called "images" toostore pictures and another called "audio" toostore audio files.</span></span> <span data-ttu-id="50bc7-114">Dopo aver creato i contenitori di hello, è possibile caricare blob singoli file toothem.</span><span class="sxs-lookup"><span data-stu-id="50bc7-114">After you create hello containers, you can upload individual blob files toothem.</span></span>

* <span data-ttu-id="50bc7-115">Per altre informazioni sulla modifica dei BLOB a livello di codice, vedere [Introduzione all'archiviazione BLOB di Azure con .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="50bc7-115">For more information on programmatically manipulating blobs, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span>
* <span data-ttu-id="50bc7-116">Per informazioni generali sull'Archiviazione di Azure, vedere [la documentazione relativa all'archiviazione](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="50bc7-116">For general information about Azure Storage, see [Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>
* <span data-ttu-id="50bc7-117">Per informazioni generali sui servizi cloud di Azure, vedere [la documentazione sui servizi cloud](https://azure.microsoft.com/documentation/services/cloud-services/).</span><span class="sxs-lookup"><span data-stu-id="50bc7-117">For general information about Azure Cloud Services, see [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/).</span></span>
* <span data-ttu-id="50bc7-118">Per altre informazioni sulla programmazione delle applicazioni ASP.NET, vedere [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="50bc7-118">For more information about programming ASP.NET applications, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="50bc7-119">Accesso ai contenitori BLOB nel codice</span><span class="sxs-lookup"><span data-stu-id="50bc7-119">Access blob containers in code</span></span>
<span data-ttu-id="50bc7-120">tooprogrammatically Accedi ai BLOB in progetti di servizi cloud, è necessario hello tooadd seguenti elementi, se non sono già presenti.</span><span class="sxs-lookup"><span data-stu-id="50bc7-120">tooprogrammatically access blobs in cloud service projects, you need tooadd hello following items, if they're not already present.</span></span>

1. <span data-ttu-id="50bc7-121">Aggiungere hello seguente di codice lo spazio dei nomi dichiarazioni toohello superiore di qualsiasi file c# in cui si desidera tooprogrammatically accesso di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="50bc7-121">Add hello following code namespace declarations toohello top of any C# file in which you wish tooprogrammatically access Azure Storage.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="50bc7-122">Ottenere un oggetto **CloudStorageAccount** che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="50bc7-122">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="50bc7-123">Hello utilizzare seguente tooget codice hello la stringa di connessione di archiviazione e informazioni sull'account di archiviazione dalla configurazione del servizio Azure hello.</span><span class="sxs-lookup"><span data-stu-id="50bc7-123">Use hello following code tooget hello your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        CloudConfigurationManager.GetSetting("<storage account name>_AzureStorageConnectionString"));
3. <span data-ttu-id="50bc7-124">Ottenere un **CloudBlobClient** tooreference un contenitore esistente nell'account di archiviazione dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="50bc7-124">Get a **CloudBlobClient** object tooreference an existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
4. <span data-ttu-id="50bc7-125">Ottenere un **CloudBlobContainer** tooreference un contenitore di blob specifico dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="50bc7-125">Get a **CloudBlobContainer** object tooreference a specific blob container.</span></span>
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

> [!NOTE]
> <span data-ttu-id="50bc7-126">Utilizzare tutto il codice hello illustrato nella procedura precedente di hello davanti codice hello di hello le sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="50bc7-126">Use all of hello code shown in hello previous procedure in front of hello code shown in hello following sections.</span></span>
> 
> 

## <a name="create-a-container-in-code"></a><span data-ttu-id="50bc7-127">Creazione di un contenitore nel codice</span><span class="sxs-lookup"><span data-stu-id="50bc7-127">Create a container in code</span></span>
> [!NOTE]
> <span data-ttu-id="50bc7-128">Alcune API che eseguono chiamate tooAzure archiviazione in ASP.NET sono asincrone.</span><span class="sxs-lookup"><span data-stu-id="50bc7-128">Some APIs that perform calls out tooAzure Storage in ASP.NET are asynchronous.</span></span> <span data-ttu-id="50bc7-129">Per ulteriori informazioni, vedere [Programmazione asincrona con Async e Await](http://msdn.microsoft.com/library/hh191443.aspx) .</span><span class="sxs-lookup"><span data-stu-id="50bc7-129">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="50bc7-130">codice Hello in hello di esempio seguente si presuppone che si utilizzano i metodi di programmazione asincrono.</span><span class="sxs-lookup"><span data-stu-id="50bc7-130">hello code in hello following example assumes that you are using async programming methods.</span></span>
> 
> 

<span data-ttu-id="50bc7-131">toocreate un contenitore nell'account di archiviazione, è sufficiente toodo è aggiungere una chiamata troppo**CreateIfNotExistsAsync** come hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="50bc7-131">toocreate a container in your storage account, all you need toodo is add a call too**CreateIfNotExistsAsync** as in hello following code:</span></span>

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="50bc7-132">toomake hello i file all'interno hello contenitore disponibili tooeveryone, è possibile impostare hello contenitore toobe pubblica utilizzando hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="50bc7-132">toomake hello files within hello container available tooeveryone, you can set hello container toobe public by using hello following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });


<span data-ttu-id="50bc7-133">Chiunque sia connesso a Internet hello possa vedere i BLOB in un contenitore pubblico, ma è possibile modificarli o eliminarli solo se si dispone di hello chiave di accesso appropriati.</span><span class="sxs-lookup"><span data-stu-id="50bc7-133">Anyone on hello Internet can see blobs in a public container, but you can modify or delete them only if you have hello appropriate access key.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="50bc7-134">Caricare un BLOB in un contenitore</span><span class="sxs-lookup"><span data-stu-id="50bc7-134">Upload a blob into a container</span></span>
<span data-ttu-id="50bc7-135">Archiviazione di Azure supporta BLOB in blocchi e BLOB di pagine.</span><span class="sxs-lookup"><span data-stu-id="50bc7-135">Azure Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="50bc7-136">Nella maggior parte delle hello blob in blocchi è consigliata toouse tipo hello.</span><span class="sxs-lookup"><span data-stu-id="50bc7-136">In hello majority of cases, block blob is hello recommended type toouse.</span></span>

<span data-ttu-id="50bc7-137">tooupload un blob in blocchi file tooa, ottenere un riferimento a un contenitore e usarlo tooget un riferimento di blob di blocco.</span><span class="sxs-lookup"><span data-stu-id="50bc7-137">tooupload a file tooa block blob, get a container reference and use it tooget a block blob reference.</span></span> <span data-ttu-id="50bc7-138">Dopo aver creato un riferimento di blob, è possibile caricare qualsiasi flusso di dati tooit dal chiamante hello **UploadFromStream** metodo.</span><span class="sxs-lookup"><span data-stu-id="50bc7-138">Once you have a blob reference, you can upload any stream of data tooit by calling hello **UploadFromStream** method.</span></span> <span data-ttu-id="50bc7-139">Questa operazione crea blob hello se non esiste in precedenza o sovrascritto se esiste.</span><span class="sxs-lookup"><span data-stu-id="50bc7-139">This operation creates hello blob if it didn't previously exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="50bc7-140">Hello seguente esempio viene illustrato come tooupload un blob in un contenitore e si presuppone che il contenitore hello è già stato creato.</span><span class="sxs-lookup"><span data-stu-id="50bc7-140">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>

    // Retrieve a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with contents from a local file.
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        blockBlob.UploadFromStream(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="50bc7-141">Elenco di BLOB hello in un contenitore</span><span class="sxs-lookup"><span data-stu-id="50bc7-141">List hello blobs in a container</span></span>
<span data-ttu-id="50bc7-142">BLOB di hello toolist in un contenitore, prima di ottenere un riferimento di contenitore.</span><span class="sxs-lookup"><span data-stu-id="50bc7-142">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="50bc7-143">È quindi possibile utilizzare del contenitore hello **ListBlobs** BLOB hello tooretrieve di metodo e/o directory all'interno di esso.</span><span class="sxs-lookup"><span data-stu-id="50bc7-143">You can then use hello container's **ListBlobs** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="50bc7-144">set completo di proprietà e metodi per un tipo restituito di hello tooaccess **IListBlobItem**, è necessario eseguirne il cast tooa **CloudBlockBlob**, **CloudPageBlob**, o  **CloudBlobDirectory** oggetto.</span><span class="sxs-lookup"><span data-stu-id="50bc7-144">tooaccess hello rich set of properties and methods for a  returned **IListBlobItem**, you must cast it tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="50bc7-145">Se il tipo di hello è sconosciuto, è possibile utilizzare un toodetermine di controllo di tipo quali toocast a.</span><span class="sxs-lookup"><span data-stu-id="50bc7-145">If hello type is unknown, you can use a type check toodetermine which toocast it to.</span></span> <span data-ttu-id="50bc7-146">Hello codice seguente viene illustrato come tooretrieve e output di hello URI di ogni elemento nel hello **foto** contenitore:</span><span class="sxs-lookup"><span data-stu-id="50bc7-146">hello following code demonstrates how tooretrieve and output hello URI of each item in hello **photos** container:</span></span>

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

<span data-ttu-id="50bc7-147">Come illustrato nell'esempio di codice hello precedente, il concetto di hello di directory all'interno di contenitori, servizio blob hello.</span><span class="sxs-lookup"><span data-stu-id="50bc7-147">As shown in hello previous code sample, hello blob service has hello concept of directories within containers, as well.</span></span> <span data-ttu-id="50bc7-148">È quindi possibile organizzare i BLOB in una struttura più simile a quella delle cartelle.</span><span class="sxs-lookup"><span data-stu-id="50bc7-148">This is so that you can organize your blobs in a more folder-like structure.</span></span> <span data-ttu-id="50bc7-149">Si consideri ad esempio hello seguente set di BLOB in blocchi in un contenitore denominato **foto**:</span><span class="sxs-lookup"><span data-stu-id="50bc7-149">For example, consider hello following set of block blobs in a container named **photos**:</span></span>

    photo1.jpg
    2010/architecture/description.txt
    2010/architecture/photo3.jpg
    2010/architecture/photo4.jpg
    2011/architecture/photo5.jpg
    2011/architecture/photo6.jpg
    2011/architecture/description.txt
    2011/photo7.jpg

<span data-ttu-id="50bc7-150">Quando si chiama **ListBlobs** nel contenitore di hello (come nell'esempio precedente del hello), raccolta hello restituita contiene **CloudBlobDirectory** e **CloudBlockBlob** oggetti che rappresenta la directory hello e BLOB contenuti al livello superiore di hello.</span><span class="sxs-lookup"><span data-stu-id="50bc7-150">When you call **ListBlobs** on hello container (as in hello previous sample), hello collection returned contains **CloudBlobDirectory** and **CloudBlockBlob** objects representing hello directories and blobs contained at hello top level.</span></span> <span data-ttu-id="50bc7-151">Di seguito è riportato l'output risultante hello:</span><span class="sxs-lookup"><span data-stu-id="50bc7-151">Here is hello resulting output:</span></span>

    Directory: https://<accountname>.blob.core.windows.net/photos/2010/
    Directory: https://<accountname>.blob.core.windows.net/photos/2011/
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg


<span data-ttu-id="50bc7-152">Facoltativamente, è possibile impostare hello **UseFlatBlobListing** parametro di hello **ListBlobs** metodo **true**.</span><span class="sxs-lookup"><span data-stu-id="50bc7-152">Optionally, you can set hello **UseFlatBlobListing** parameter of of hello **ListBlobs** method to **true**.</span></span> <span data-ttu-id="50bc7-153">In questo modo tutti i BLOB verranno restituiti come **CloudBlockBlob**, indipendentemente dalla directory.</span><span class="sxs-lookup"><span data-stu-id="50bc7-153">This results in every blob being returned as a **CloudBlockBlob**, regardless of directory.</span></span> <span data-ttu-id="50bc7-154">Ecco la chiamata di hello troppo**ListBlobs**:</span><span class="sxs-lookup"><span data-stu-id="50bc7-154">Here is hello call too**ListBlobs**:</span></span>

    // Loop over items within hello container and output hello length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, true))
    {
       ...
    }

<span data-ttu-id="50bc7-155">e di seguito sono riportati i risultati di hello:</span><span class="sxs-lookup"><span data-stu-id="50bc7-155">and here are hello results:</span></span>

    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
    Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
    Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
    Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
    Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
    Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg

<span data-ttu-id="50bc7-156">Per altre informazioni, vedere [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).</span><span class="sxs-lookup"><span data-stu-id="50bc7-156">For more information, see [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).</span></span>

## <a name="download-blobs"></a><span data-ttu-id="50bc7-157">Scaricare BLOB</span><span class="sxs-lookup"><span data-stu-id="50bc7-157">Download blobs</span></span>
<span data-ttu-id="50bc7-158">BLOB toodownload, recuperare innanzitutto un riferimento di blob e quindi chiamare hello **metodi DownloadToStream** metodo.</span><span class="sxs-lookup"><span data-stu-id="50bc7-158">toodownload blobs, first retrieve a blob reference and then call hello **DownloadToStream** method.</span></span> <span data-ttu-id="50bc7-159">esempio Hello utilizza hello **metodi DownloadToStream** metodo tootransfer hello blob contenuto tooa oggetto flusso che può quindi rendere persistente tooa file locale.</span><span class="sxs-lookup"><span data-stu-id="50bc7-159">hello following example uses hello **DownloadToStream** method tootransfer hello blob contents tooa stream object that you can then persist tooa local file.</span></span>

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save blob contents tooa file.
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        blockBlob.DownloadToStream(fileStream);
    }

<span data-ttu-id="50bc7-160">È inoltre possibile utilizzare hello **metodi DownloadToStream** contenuto hello toodownload di metodo di un blob come una stringa di testo.</span><span class="sxs-lookup"><span data-stu-id="50bc7-160">You can also use hello **DownloadToStream** method toodownload hello contents of a blob as a text string.</span></span>

    // Get a reference tooa blob named "myblob.txt"
    CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

    string text;
    using (var memoryStream = new MemoryStream())
    {
        blockBlob2.DownloadToStream(memoryStream);
        text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
    }

## <a name="delete-blobs"></a><span data-ttu-id="50bc7-161">Eliminare BLOB</span><span class="sxs-lookup"><span data-stu-id="50bc7-161">Delete blobs</span></span>
<span data-ttu-id="50bc7-162">un blob, toodelete innanzitutto ottenere un riferimento di blob e quindi chiamare il **eliminare** metodo.</span><span class="sxs-lookup"><span data-stu-id="50bc7-162">toodelete a blob, first get a blob reference and then call the **Delete** method.</span></span>

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    blockBlob.Delete();


## <a name="list-blobs-in-pages-asynchronously"></a><span data-ttu-id="50bc7-163">Elencare BLOB nelle pagine in modalità asincrona</span><span class="sxs-lookup"><span data-stu-id="50bc7-163">List blobs in pages asynchronously</span></span>
<span data-ttu-id="50bc7-164">Elencare un numero elevato di BLOB, se si desidera toocontrol hello numero di risultati che restituito in un'unica operazione di elenco, è possibile elencare i BLOB di pagine di risultati.</span><span class="sxs-lookup"><span data-stu-id="50bc7-164">If you are listing a large number of blobs, or you want toocontrol hello number of results you return in one listing operation, you can list blobs in pages of results.</span></span> <span data-ttu-id="50bc7-165">Questo esempio mostra la vista tooreturn dei risultati nelle pagine in modo asincrono, in modo che non l'esecuzione viene bloccata durante l'attesa tooreturn un ampio set di risultati.</span><span class="sxs-lookup"><span data-stu-id="50bc7-165">This example shows how tooreturn results in pages asynchronously, so that execution is not blocked while waiting tooreturn a large set of results.</span></span>

<span data-ttu-id="50bc7-166">Questo esempio viene illustrato un semplice elenco di blob, ma è anche possibile eseguire un elenco gerarchico, impostazione hello **useFlatBlobListing** parametro di hello **ListBlobsSegmentedAsync** metodo troppo **false**.</span><span class="sxs-lookup"><span data-stu-id="50bc7-166">This example shows a flat blob listing, but you can also perform a hierarchical listing, by setting hello **useFlatBlobListing** parameter of hello **ListBlobsSegmentedAsync** method too**false**.</span></span>

<span data-ttu-id="50bc7-167">Poiché l'esempio hello chiama un metodo asincrono, devono essere preceduto da hello **async** (parola chiave) e deve restituire un **attività** oggetto.</span><span class="sxs-lookup"><span data-stu-id="50bc7-167">Because hello sample method calls an asynchronous method, it must be prefaced with hello **async** keyword, and it must return a **Task** object.</span></span> <span data-ttu-id="50bc7-168">Hello await (parola chiave) specificato per hello **ListBlobsSegmentedAsync** metodo sospende l'esecuzione del metodo di esempio hello fino al completamento hello elenco attività.</span><span class="sxs-lookup"><span data-stu-id="50bc7-168">hello await keyword specified for hello **ListBlobsSegmentedAsync** method suspends execution of hello sample method until hello listing task completes.</span></span>

    async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
    {
        // List blobs toohello console window, with paging.
        Console.WriteLine("List blobs in pages:");

        int i = 0;
        BlobContinuationToken continuationToken = null;
        BlobResultSegment resultSegment = null;

        // Call ListBlobsSegmentedAsync and enumerate hello result segment returned, while hello continuation token is non-null.
        // When hello continuation token is null, hello last page has been returned and execution can exit hello loop.
        do
        {
            // This overload allows control of hello page size. You can return all remaining results by passing null for hello maxResults parameter,
            // or by calling a different overload.
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

## <a name="next-steps"></a><span data-ttu-id="50bc7-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="50bc7-169">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

