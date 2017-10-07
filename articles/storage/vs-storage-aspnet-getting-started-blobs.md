---
title: aaaGet generali di archiviazione blob di Azure e Visual Studio connesso servizi (ASP.NET) | Documenti Microsoft
description: "La modalità di avvio tooget utilizzo dell'archiviazione blob di Azure in un progetto ASP.NET in Visual Studio dopo la connessione di account di archiviazione tooa utilizzando servizi connessi di Visual Studio"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: b3497055-bef8-4c95-8567-181556b50d95
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: tarcher
ms.openlocfilehash: eb38889f239a63852d6928e8be10c3d3f1746e9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="dd0a0-103">Introduzione all'Archiviazione BLOB di Azure e ai Servizi connessi di Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="dd0a0-103">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="dd0a0-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="dd0a0-104">Overview</span></span>

<span data-ttu-id="dd0a0-105">Archiviazione blob di Azure è un servizio che archivia i dati non strutturati nel cloud hello come oggetti/BLOB.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-105">Azure blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="dd0a0-106">Archivio BLOB può archiviare qualsiasi tipo di dati di testo o binari, ad esempio un documento, un file multimediale o un programma di installazione di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="dd0a0-107">Archiviazione BLOB è anche archiviazione di oggetti di cui viene fatto riferimento tooas.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="dd0a0-108">Questa esercitazione viene illustrato come toowrite ASP.NET codice in alcuni scenari comuni di utilizzo dell'archiviazione blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-108">This tutorial shows how toowrite ASP.NET code for some common scenarios using Azure blob storage.</span></span> <span data-ttu-id="dd0a0-109">Gli scenari includono la creazione di un contenitore BLOB e il caricamento, la creazione di elenchi, il download e l'eliminazione di BLOB.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-109">Scenarios include creating a blob container, and uploading, listing, downloading, and deleting blobs.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="dd0a0-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="dd0a0-110">Prerequisites</span></span>

* [<span data-ttu-id="dd0a0-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dd0a0-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="dd0a0-112">Account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="dd0a0-112">Azure storage account</span></span>](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="dd0a0-113">Creare un controller MVC</span><span class="sxs-lookup"><span data-stu-id="dd0a0-113">Create an MVC controller</span></span> 

1. <span data-ttu-id="dd0a0-114">In hello **Esplora soluzioni**, fare doppio clic su **controller**, selezionare il menu di scelta rapida hello **Aggiungi -> Controller**.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-114">In hello **Solution Explorer**, right-click **Controllers**, and, from hello context menu, select **Add->Controller**.</span></span>

    ![Aggiungere un tooan controller app ASP.NET MVC](./media/vs-storage-aspnet-getting-started-blobs/add-controller-menu.png)

1. <span data-ttu-id="dd0a0-116">In hello **aggiungere lo scaffolding** finestra di dialogo Seleziona **Controller MVC 5 - vuoto**e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-116">On hello **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Specificare il tipo di controller MVC](./media/vs-storage-aspnet-getting-started-blobs/add-controller.png)

1. <span data-ttu-id="dd0a0-118">In hello **Aggiungi Controller** finestra di dialogo, nome del controller hello *BlobsController*e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-118">On hello **Add Controller** dialog, name hello controller *BlobsController*, and select **Add**.</span></span>

    ![Controller MVC hello di nome](./media/vs-storage-aspnet-getting-started-blobs/add-controller-name.png)

1. <span data-ttu-id="dd0a0-120">Aggiungere il seguente hello *utilizzando* toohello direttive `BlobsController.cs` file:</span><span class="sxs-lookup"><span data-stu-id="dd0a0-120">Add hello following *using* directives toohello `BlobsController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

## <a name="create-a-blob-container"></a><span data-ttu-id="dd0a0-121">Creare un contenitore BLOB</span><span class="sxs-lookup"><span data-stu-id="dd0a0-121">Create a blob container</span></span>

<span data-ttu-id="dd0a0-122">Un contenitore BLOB è una gerarchia nidificata di BLOB e cartelle.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-122">A blob container is a nested hierarchy of blobs and folders.</span></span> <span data-ttu-id="dd0a0-123">Hello passaggi seguenti viene illustrato come un contenitore blob toocreate:</span><span class="sxs-lookup"><span data-stu-id="dd0a0-123">hello following steps illustrate how toocreate a blob container:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="dd0a0-124">Hello codice in questa sezione si presuppone di aver completato i passaggi di hello nella sezione hello [configurare un ambiente di sviluppo hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="dd0a0-124">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="dd0a0-125">Aprire hello `BlobsController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-125">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="dd0a0-126">Aggiungere un metodo denominato **CreateBlobContainer** che restituisce un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-126">Add a method called **CreateBlobContainer** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateBlobContainer()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="dd0a0-127">All'interno di hello **CreateBlobContainer** (metodo), ottenere un **CloudStorageAccount** oggetto che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-127">Within hello **CreateBlobContainer** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="dd0a0-128">Utilizzare hello seguendo codice tooget hello archiviazione stringa e l'archiviazione account informazioni di connessione dalla configurazione del servizio Azure hello.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-128">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration.</span></span> <span data-ttu-id="dd0a0-129">(Modifica  *&lt;storage-account-name >* toohello nome di account di archiviazione di Azure si accede hello.)</span><span class="sxs-lookup"><span data-stu-id="dd0a0-129">(Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="dd0a0-130">Recuperare un oggetto **CloudBlobClient** che rappresenta un client del servizio BLOB.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-130">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="dd0a0-131">Ottenere un **CloudBlobContainer** oggetto che rappresenta un nome di contenitore blob desiderato toohello di riferimento.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-131">Get a **CloudBlobContainer** object that represents a reference toohello desired blob container name.</span></span> <span data-ttu-id="dd0a0-132">Hello **CloudBlobClient.GetContainerReference** metodo non effettuare una richiesta nel servizio di archiviazione blob.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-132">hello **CloudBlobClient.GetContainerReference** method does not make a request against blob storage.</span></span> <span data-ttu-id="dd0a0-133">contenitore blob hello esista o meno, viene restituito il riferimento di Hello.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-133">hello reference is returned whether or not hello blob container exists.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="dd0a0-134">Chiamare hello **CloudBlobContainer.CreateIfNotExists** contenitore di hello toocreate metodo se non esiste ancora.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-134">Call hello **CloudBlobContainer.CreateIfNotExists** method toocreate hello container if it does not yet exist.</span></span> <span data-ttu-id="dd0a0-135">Hello **CloudBlobContainer.CreateIfNotExists** restituisce **true** se hello contenitore non esiste e viene creato correttamente.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-135">hello **CloudBlobContainer.CreateIfNotExists** method returns **true** if hello container does not exist, and is successfully created.</span></span> <span data-ttu-id="dd0a0-136">In caso contrario, viene restituito **false**.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-136">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = container.CreateIfNotExists();
    ```

1. <span data-ttu-id="dd0a0-137">Hello aggiornamento **ViewBag** con nome hello del contenitore blob hello.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-137">Update hello **ViewBag** with hello name of hello blob container.</span></span>

    ```csharp
    ViewBag.BlobContainerName = container.Name;
    ```

1. <span data-ttu-id="dd0a0-138">In hello **Esplora**, espandere hello **viste** cartella, fare doppio clic su **BLOB**e quindi scegliere il menu di scelta rapida hello **Aggiungi -> Vista**.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-138">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Blobs**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="dd0a0-139">In hello **Aggiungi visualizzazione** finestra di dialogo immettere **CreateBlobContainer** per nome della visualizzazione hello e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-139">On hello **Add View** dialog, enter **CreateBlobContainer** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="dd0a0-140">Aprire `CreateBlobContainer.cshtml`e modificarlo in modo che risulti simile hello frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="dd0a0-140">Open `CreateBlobContainer.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Blob Container";
    }
    
    <h2>Create Blob Container results</h2>

    Creation of @ViewBag.BlobContainerName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="dd0a0-141">In hello **Esplora**, espandere hello **viste -> Shared** cartella e aprire `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-141">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="dd0a0-142">Dopo aver hello ultimo **HTML. ActionLink**, aggiungere il seguente hello **HTML. ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="dd0a0-142">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create blob container", "CreateBlobContainer", "Blobs")</li>
    ```

1. <span data-ttu-id="dd0a0-143">Eseguire un'applicazione hello e selezionare **crea contenitore Blob** toosee risultati simile toohello cattura di schermata seguente:</span><span class="sxs-lookup"><span data-stu-id="dd0a0-143">Run hello application, and select **Create Blob Container** toosee results similar toohello following screen shot:</span></span>
  
    ![Creare un contenitore BLOB](./media/vs-storage-aspnet-getting-started-blobs/create-blob-container-results.png)

    <span data-ttu-id="dd0a0-145">Come accennato in precedenza, hello **CloudBlobContainer.CreateIfNotExists** restituisce **true** solo quando il contenitore di hello non esiste e viene creato.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-145">As mentioned previously, hello **CloudBlobContainer.CreateIfNotExists** method returns **true** only when hello container doesn't exist and is created.</span></span> <span data-ttu-id="dd0a0-146">Pertanto, se si esegue l'applicazione hello quando hello contenitore esiste, il metodo di hello restituisce **false**.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-146">Therefore, if you run hello app when hello container exists, hello method returns **false**.</span></span> <span data-ttu-id="dd0a0-147">app hello toorun più volte, è necessario eliminare il contenitore di hello prima di eseguire nuovamente l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-147">toorun hello app multiple times, you must delete hello container before running hello app again.</span></span> <span data-ttu-id="dd0a0-148">Contenitore hello eliminazione può essere eseguite tramite hello **CloudBlobContainer.Delete** metodo.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-148">Deleting hello container can be done via hello **CloudBlobContainer.Delete** method.</span></span> <span data-ttu-id="dd0a0-149">È anche possibile eliminare il contenitore di hello utilizzando hello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) o hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="dd0a0-149">You can also delete hello container using hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="upload-a-blob-into-a-blob-container"></a><span data-ttu-id="dd0a0-150">Caricare un BLOB in un contenitore BLOB</span><span class="sxs-lookup"><span data-stu-id="dd0a0-150">Upload a blob into a blob container</span></span>

<span data-ttu-id="dd0a0-151">Dopo avere [creato un contenitore BLOB](#create-a-blob-container), è possibile caricare file in questo contenitore.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-151">Once you've [created a blob container](#create-a-blob-container), you can upload files into that container.</span></span> <span data-ttu-id="dd0a0-152">In questa sezione viene illustrato il caricamento di un contenitore di blob tooa file locale.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-152">This section walks you through uploading a local file tooa blob container.</span></span> <span data-ttu-id="dd0a0-153">passaggi di Hello presuppongono la creazione di un contenitore blob denominato *contenitore di blob test*.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-153">hello steps assume you've created a blob container named *test-blob-container*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="dd0a0-154">Hello codice in questa sezione si presuppone di aver completato i passaggi di hello nella sezione hello [configurare un ambiente di sviluppo hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="dd0a0-154">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="dd0a0-155">Aprire hello `BlobsController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-155">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="dd0a0-156">Aggiungere un metodo denominato **UploadBlob** che restituisce un **EmptyResult**.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-156">Add a method called **UploadBlob** that returns an **EmptyResult**.</span></span>

    ```csharp
    public EmptyResult UploadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="dd0a0-157">All'interno di hello **UploadBlob** (metodo), ottenere un **CloudStorageAccount** oggetto che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-157">Within hello **UploadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="dd0a0-158">Esempio di codice seguente di hello utilizzare tooget hello archiviazione stringa e l'archiviazione account informazioni di connessione di configurazione del servizio Azure hello: (modifica  *&lt;storage-account-name >* toohello nome hello archiviazione di Azure account che si accede.)</span><span class="sxs-lookup"><span data-stu-id="dd0a0-158">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="dd0a0-159">Recuperare un oggetto **CloudBlobClient** che rappresenta un client del servizio BLOB.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-159">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="dd0a0-160">Ottenere un **CloudBlobContainer** oggetto che rappresenta un nome di contenitore blob toohello di riferimento.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-160">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="dd0a0-161">Come illustrato in precedenza, l'Archiviazione di Azure supporta tipi di BLOB diversi.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-161">As explained earlier, Azure storage supports different blob types.</span></span> <span data-ttu-id="dd0a0-162">tooretrieve un blob di pagine di riferimento tooa, chiamata hello **CloudBlobContainer.GetPageBlobReference** metodo.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-162">tooretrieve a reference tooa page blob, call hello **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="dd0a0-163">tooretrieve un blob in blocchi, tooa riferimento chiamata hello **CloudBlobContainer.GetBlockBlobReference** metodo.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-163">tooretrieve a reference tooa block blob, call hello **CloudBlobContainer.GetBlockBlobReference** method.</span></span> <span data-ttu-id="dd0a0-164">Blob in blocchi in genere, è consigliata toouse tipo hello.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-164">Usually, block blob is hello recommended type toouse.</span></span> <span data-ttu-id="dd0a0-165">(Modifica < nome del blob > * toohello nome blob hello toogive una volta caricato.)</span><span class="sxs-lookup"><span data-stu-id="dd0a0-165">(Change <blob-name>* toohello name you want toogive hello blob once uploaded.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="dd0a0-166">Dopo aver creato un riferimento di blob, è possibile caricare qualsiasi tooit di flusso di dati chiamando hello blob riferimento oggetto **UploadFromStream** metodo.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-166">Once you have a blob reference, you can upload any data stream tooit by calling hello blob reference object's **UploadFromStream** method.</span></span> <span data-ttu-id="dd0a0-167">Hello **UploadFromStream** metodo consente di creare blob hello se non esiste o lo sovrascrive se esiste.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-167">hello **UploadFromStream** method creates hello blob if it doesn't exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="dd0a0-168">(Modifica  *&lt;al caricamento di file >* tooa completo file di toohello percorso desiderato tooupload.)</span><span class="sxs-lookup"><span data-stu-id="dd0a0-168">(Change *&lt;file-to-upload>* tooa fully qualified path toohello file you want tooupload.)</span></span>

    ```csharp
    using (var fileStream = System.IO.File.OpenRead(<file-to-upload>))
    {
        blob.UploadFromStream(fileStream);
    }
    ```

1. <span data-ttu-id="dd0a0-169">In hello **Esplora**, espandere hello **viste** cartella, fare doppio clic su **BLOB**e quindi scegliere il menu di scelta rapida hello **Aggiungi -> Vista**.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-169">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Blobs**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="dd0a0-170">In hello **Esplora**, espandere hello **viste -> Shared** cartella e aprire `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-170">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="dd0a0-171">Dopo aver hello ultimo **HTML. ActionLink**, aggiungere il seguente hello **HTML. ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="dd0a0-171">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Upload blob", "UploadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="dd0a0-172">Eseguire un'applicazione hello e selezionare **caricamento blob**.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-172">Run hello application, and select **Upload blob**.</span></span>  
  
<span data-ttu-id="dd0a0-173">Hello sezione - [elencare i BLOB hello in un contenitore blob](#list-the-blobs-in-a-blob-container) -illustra come hello toolist BLOB in un contenitore blob.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-173">hello section - [List hello blobs in a blob container](#list-the-blobs-in-a-blob-container) - illustrates how toolist hello blobs in a blob container.</span></span>  

## <a name="list-hello-blobs-in-a-blob-container"></a><span data-ttu-id="dd0a0-174">Elencare i BLOB hello in un contenitore blob</span><span class="sxs-lookup"><span data-stu-id="dd0a0-174">List hello blobs in a blob container</span></span>

<span data-ttu-id="dd0a0-175">In questa sezione viene illustrato come hello toolist BLOB in un contenitore blob.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-175">This section illustrates how toolist hello blobs in a blob container.</span></span> <span data-ttu-id="dd0a0-176">codice di esempio Hello fa riferimento a hello *contenitore di blob test* creato nella sezione hello, [creare un contenitore blob](#create-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="dd0a0-176">hello sample code references hello *test-blob-container* created in hello section, [Create a blob container](#create-a-blob-container).</span></span>

> [!NOTE]
> 
> <span data-ttu-id="dd0a0-177">Hello codice in questa sezione si presuppone di aver completato i passaggi di hello nella sezione hello [configurare un ambiente di sviluppo hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="dd0a0-177">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="dd0a0-178">Aprire hello `BlobsController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-178">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="dd0a0-179">Aggiungere un metodo denominato **ListBlobs** che restituisce un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-179">Add a method called **ListBlobs** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ListBlobs()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="dd0a0-180">All'interno di hello **ListBlobs** (metodo), ottenere un **CloudStorageAccount** oggetto che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-180">Within hello **ListBlobs** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="dd0a0-181">Esempio di codice seguente di hello utilizzare tooget hello archiviazione stringa e l'archiviazione account informazioni di connessione di configurazione del servizio Azure hello: (modifica  *&lt;storage-account-name >* toohello nome hello archiviazione di Azure account che si accede.)</span><span class="sxs-lookup"><span data-stu-id="dd0a0-181">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="dd0a0-182">Recuperare un oggetto **CloudBlobClient** che rappresenta un client del servizio BLOB.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-182">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="dd0a0-183">Ottenere un **CloudBlobContainer** oggetto che rappresenta un nome di contenitore blob toohello di riferimento.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-183">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="dd0a0-184">BLOB hello toolist in un contenitore blob, utilizzare hello **cloudblobcontainer. Listblobs** metodo.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-184">toolist hello blobs in a blob container, use hello **CloudBlobContainer.ListBlobs** method.</span></span> <span data-ttu-id="dd0a0-185">Hello **cloudblobcontainer. Listblobs** metodo restituisce un **IListBlobItem** dell'oggetto che si esegue il cast tooa **CloudBlockBlob**, **CloudPageBlob**, o **CloudBlobDirectory** oggetto.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-185">hello **CloudBlobContainer.ListBlobs** method returns an **IListBlobItem** object that you cast tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="dd0a0-186">Hello frammento di codice seguente consente di enumerare tutti i BLOB hello in un contenitore blob.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-186">hello following code snippet enumerates all hello blobs in a blob container.</span></span> <span data-ttu-id="dd0a0-187">Ciascun blob è il cast toohello appropriato di oggetti in base a tipo e il relativo nome (nel caso di hello di URI o un **CloudBlobDirectory**) viene aggiunto l'elenco tooa.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-187">Each blob is cast toohello appropriate object based on its type, and its name (or URI in hello case of a **CloudBlobDirectory**) is added tooa list.</span></span>

    ```csharp
    List<string> blobs = new List<string>();

    foreach (IListBlobItem item in container.ListBlobs(null, false))
    {
        if (item.GetType() == typeof(CloudBlockBlob))
        {
            CloudBlockBlob blob = (CloudBlockBlob)item;
            blobs.Add(blob.Name);
        }
        else if (item.GetType() == typeof(CloudPageBlob))
        {
            CloudPageBlob blob = (CloudPageBlob)item;
            blobs.Add(blob.Name);
        }
        else if (item.GetType() == typeof(CloudBlobDirectory))
        {
            CloudBlobDirectory dir = (CloudBlobDirectory)item;
            blobs.Add(dir.Uri.ToString());
        }
    }

    return View(blobs);
    ```

    <span data-ttu-id="dd0a0-188">In aggiunta tooblobs, contenitori blob possono contenere le directory.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-188">In addition tooblobs, blob containers can contain directories.</span></span> <span data-ttu-id="dd0a0-189">Si supponga di disporre di un contenitore blob denominato *contenitore di blob test* con hello seguente gerarchia:</span><span class="sxs-lookup"><span data-stu-id="dd0a0-189">Let's suppose you have a blob container called *test-blob-container* with hello following hierarchy:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

    <span data-ttu-id="dd0a0-190">Utilizza hello precedente esempio di codice, hello **BLOB** elenco stringa siano contenuti valori simili toohello:</span><span class="sxs-lookup"><span data-stu-id="dd0a0-190">Using hello preceding code example, hello **blobs** string list contains values similar toohello following:</span></span>

        foo.png
        <storage-account-url>/test-blob-container/dir1
        <storage-account-url>/test-blob-container/dir2

    <span data-ttu-id="dd0a0-191">Come si può notare, l'elenco di hello include solo hello livello principale le entità; hello non annidati quelle (*bar.png* e *baz.png*).</span><span class="sxs-lookup"><span data-stu-id="dd0a0-191">As you can see, hello list includes only hello top-level entities; not hello nested ones (*bar.png* and *baz.png*).</span></span> <span data-ttu-id="dd0a0-192">toolist tutti hello entità all'interno di un contenitore blob, è necessario chiamare hello **cloudblobcontainer. Listblobs** (metodo) e passare **true** per hello **useFlatBlobListing** parametro.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-192">toolist all hello entities within a blob container, you must call hello **CloudBlobContainer.ListBlobs** method and pass **true** for hello **useFlatBlobListing** parameter.</span></span>    

    ```csharp
    ...
    foreach (IListBlobItem item in container.ListBlobs(useFlatBlobListing:true))
    ...
    ```

    <span data-ttu-id="dd0a0-193">Hello impostazione **useFlatBlobListing** parametro troppo**true** restituisce un elenco semplice di tutte le entità nel contenitore di blob hello e produce hello seguenti risultati:</span><span class="sxs-lookup"><span data-stu-id="dd0a0-193">Setting hello **useFlatBlobListing** parameter too**true** returns a flat listing of all entities in hello blob container, and yields hello following results:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

1. <span data-ttu-id="dd0a0-194">In hello **Esplora**, espandere hello **viste** cartella, fare doppio clic su **BLOB**e quindi scegliere il menu di scelta rapida hello **Aggiungi -> Vista**.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-194">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Blobs**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="dd0a0-195">In hello **Aggiungi visualizzazione** finestra di dialogo immettere **ListBlobs** per nome della visualizzazione hello e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-195">On hello **Add View** dialog, enter **ListBlobs** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="dd0a0-196">Aprire `ListBlobs.cshtml`e modificarlo in modo che risulti simile hello frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="dd0a0-196">Open `ListBlobs.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```html
    @model List<string>
    @{
        ViewBag.Title = "List blobs";
    }
    
    <h2>List blobs</h2>
    
    <ul>
        @foreach (var item in Model)
        {
        <li>@item</li>
        }
    </ul>
    ```

1. <span data-ttu-id="dd0a0-197">In hello **Esplora**, espandere hello **viste -> Shared** cartella e aprire `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-197">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="dd0a0-198">Dopo aver hello ultimo **HTML. ActionLink**, aggiungere il seguente hello **HTML. ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="dd0a0-198">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("List blobs", "ListBlobs", "Blobs")</li>
    ```

1. <span data-ttu-id="dd0a0-199">Eseguire un'applicazione hello e selezionare **elencare i BLOB** toosee risultati simile toohello cattura di schermata seguente:</span><span class="sxs-lookup"><span data-stu-id="dd0a0-199">Run hello application, and select **List blobs** toosee results similar toohello following screen shot:</span></span>
  
    ![Elenco di BLOB](./media/vs-storage-aspnet-getting-started-blobs/listblobs.png)

## <a name="download-blobs"></a><span data-ttu-id="dd0a0-201">Scaricare BLOB</span><span class="sxs-lookup"><span data-stu-id="dd0a0-201">Download blobs</span></span>

<span data-ttu-id="dd0a0-202">In questa sezione viene illustrato come toodownload un blob e renderlo persistente contenuto di hello toolocal archiviazione o di lettura in una stringa.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-202">This section illustrates how toodownload a blob and either persist it toolocal storage or read hello contents into a string.</span></span> <span data-ttu-id="dd0a0-203">codice di esempio Hello fa riferimento a hello *contenitore di blob test* creato nella sezione hello, [creare un contenitore blob](#create-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="dd0a0-203">hello sample code references hello *test-blob-container* created in hello section, [Create a blob container](#create-a-blob-container).</span></span>

1. <span data-ttu-id="dd0a0-204">Aprire hello `BlobsController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-204">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="dd0a0-205">Aggiungere un metodo denominato **DownloadBlob** che restituisce un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-205">Add a method called **DownloadBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DownloadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="dd0a0-206">All'interno di hello **DownloadBlob** (metodo), ottenere un **CloudStorageAccount** oggetto che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-206">Within hello **DownloadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="dd0a0-207">Esempio di codice seguente di hello utilizzare tooget hello archiviazione stringa e l'archiviazione account informazioni di connessione di configurazione del servizio Azure hello: (modifica  *&lt;storage-account-name >* toohello nome hello archiviazione di Azure account che si accede.)</span><span class="sxs-lookup"><span data-stu-id="dd0a0-207">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="dd0a0-208">Recuperare un oggetto **CloudBlobClient** che rappresenta un client del servizio BLOB.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-208">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="dd0a0-209">Ottenere un **CloudBlobContainer** oggetto che rappresenta un nome di contenitore blob toohello di riferimento.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-209">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="dd0a0-210">Recuperare un oggetto di riferimento al BLOB chiamando il metodo **CloudBlobContainer.GetBlockBlobReference** o **CloudBlobContainer.GetPageBlobReference**.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-210">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="dd0a0-211">(Modifica  *&lt;nome blob >* toohello nome di blob hello si scaricano.)</span><span class="sxs-lookup"><span data-stu-id="dd0a0-211">(Change *&lt;blob-name>* toohello name of hello blob you are downloading.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="dd0a0-212">toodownload un blob, utilizzare hello **CloudBlockBlob.DownloadToStream** o **CloudPageBlob.DownloadToStream** (metodo), in base al tipo di blob hello.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-212">toodownload a blob, use hello **CloudBlockBlob.DownloadToStream** or **CloudPageBlob.DownloadToStream** method, depending on hello blob type.</span></span> <span data-ttu-id="dd0a0-213">frammento di codice seguente Hello utilizza hello **CloudBlockBlob.DownloadToStream** tootransfer metodo flusso tooa di contenuto del blob, un oggetto che è quindi persistente file locale tooa: (modifica  *&lt;nome del file locale >* toohello completo di nome di file, che rappresenta il percorso blob hello scaricati.)</span><span class="sxs-lookup"><span data-stu-id="dd0a0-213">hello following code snippet uses hello **CloudBlockBlob.DownloadToStream** method tootransfer a blob's contents tooa stream object that is then persisted tooa local file: (Change *&lt;local-file-name>* toohello fully qualified file name representing where you want hello blob downloaded.)</span></span> 

    ```csharp
    using (var fileStream = System.IO.File.OpenWrite(<local-file-name>))
    {
        blob.DownloadToStream(fileStream);
    }
    ```

1. <span data-ttu-id="dd0a0-214">In hello **Esplora**, espandere hello **viste -> Shared** cartella e aprire `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-214">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="dd0a0-215">Dopo aver hello ultimo **HTML. ActionLink**, aggiungere il seguente hello **HTML. ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="dd0a0-215">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Download blob", "DownloadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="dd0a0-216">Eseguire un'applicazione hello e selezionare **Download blob** blob hello toodownload.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-216">Run hello application, and select **Download blob** toodownload hello blob.</span></span> <span data-ttu-id="dd0a0-217">blob Hello specificato in hello **CloudBlobContainer.GetBlockBlobReference** chiamata al metodo scarica toohello percorso specificato in hello **file. OpenWrite** chiamata al metodo.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-217">hello blob specified in hello **CloudBlobContainer.GetBlockBlobReference** method call downloads toohello location you specify in hello **File.OpenWrite** method call.</span></span> 

## <a name="delete-blobs"></a><span data-ttu-id="dd0a0-218">Eliminare BLOB</span><span class="sxs-lookup"><span data-stu-id="dd0a0-218">Delete blobs</span></span>

<span data-ttu-id="dd0a0-219">Hello passaggi seguenti viene illustrato come toodelete un blob:</span><span class="sxs-lookup"><span data-stu-id="dd0a0-219">hello following steps illustrate how toodelete a blob:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="dd0a0-220">Hello codice in questa sezione si presuppone di aver completato i passaggi di hello nella sezione hello [configurare un ambiente di sviluppo hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="dd0a0-220">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="dd0a0-221">Aprire hello `BlobsController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-221">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="dd0a0-222">Aggiungere un metodo denominato **DeleteBlob** che restituisce un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-222">Add a method called **DeleteBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DeleteBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```

1. <span data-ttu-id="dd0a0-223">Ottenere un oggetto **CloudStorageAccount** che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-223">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="dd0a0-224">Esempio di codice seguente di hello utilizzare tooget hello archiviazione stringa e l'archiviazione account informazioni di connessione di configurazione del servizio Azure hello: (modifica  *&lt;storage-account-name >* toohello nome hello archiviazione di Azure account che si accede.)</span><span class="sxs-lookup"><span data-stu-id="dd0a0-224">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="dd0a0-225">Recuperare un oggetto **CloudBlobClient** che rappresenta un client del servizio BLOB.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-225">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="dd0a0-226">Ottenere un **CloudBlobContainer** oggetto che rappresenta un nome di contenitore blob toohello di riferimento.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-226">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="dd0a0-227">Recuperare un oggetto di riferimento al BLOB chiamando il metodo **CloudBlobContainer.GetBlockBlobReference** o **CloudBlobContainer.GetPageBlobReference**.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-227">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="dd0a0-228">(Modifica  *&lt;nome blob >* toohello nome di blob hello si sta eliminando.)</span><span class="sxs-lookup"><span data-stu-id="dd0a0-228">(Change *&lt;blob-name>* toohello name of hello blob you are deleting.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
        ```

1. toodelete a blob, use hello **Delete** method.

    ```csharp
    blob.Delete();
    ```

1. <span data-ttu-id="dd0a0-229">In hello **Esplora**, espandere hello **viste -> Shared** cartella e aprire `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-229">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="dd0a0-230">Dopo aver hello ultimo **HTML. ActionLink**, aggiungere il seguente hello **HTML. ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="dd0a0-230">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete blob", "DeleteBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="dd0a0-231">Eseguire un'applicazione hello e selezionare **Delete blob** blob hello toodelete specificato in hello **CloudBlobContainer.GetBlockBlobReference** chiamata al metodo.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-231">Run hello application, and select **Delete blob** toodelete hello blob specified in hello **CloudBlobContainer.GetBlockBlobReference** method call.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="dd0a0-232">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dd0a0-232">Next steps</span></span>
<span data-ttu-id="dd0a0-233">Consente di visualizzare altre toolearn di guide di funzionalità sulle opzioni aggiuntive per l'archiviazione dei dati in Azure.</span><span class="sxs-lookup"><span data-stu-id="dd0a0-233">View more feature guides toolearn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="dd0a0-234">Introduzione all'archiviazione tabelle di Azure e ai Servizi connessi di Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="dd0a0-234">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-tables.md)
  * [<span data-ttu-id="dd0a0-235">Introduzione all'archiviazione code di Azure e ai Servizi connessi di Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="dd0a0-235">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-queues.md)
