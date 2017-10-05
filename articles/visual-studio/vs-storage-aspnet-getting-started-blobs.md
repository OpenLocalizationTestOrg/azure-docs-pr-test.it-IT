---
title: Introduzione all'Archiviazione BLOB di Azure e ai Servizi connessi di Visual Studio (ASP.NET) | Documentazione Microsoft
description: Informazioni su come iniziare a usare l'Archiviazione BLOB di Azure in un progetto ASP.NET in Visual Studio dopo la connessione a un account di archiviazione con Servizi connessi di Visual Studio
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: b3497055-bef8-4c95-8567-181556b50d95
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: kraig
ms.openlocfilehash: e953c7978705379a28581213e8f1c665473ddd60
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="43db8-103">Introduzione all'Archiviazione BLOB di Azure e ai Servizi connessi di Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="43db8-103">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="43db8-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="43db8-104">Overview</span></span>

<span data-ttu-id="43db8-105">L'Archiviazione BLOB di Azure è un servizio che archivia i dati non strutturati nel cloud come oggetti/BLOB.</span><span class="sxs-lookup"><span data-stu-id="43db8-105">Azure blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="43db8-106">Archivio BLOB può archiviare qualsiasi tipo di dati di testo o binari, ad esempio un documento, un file multimediale o un programma di installazione di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="43db8-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="43db8-107">L'archivio BLOB è anche denominato archivio di oggetti.</span><span class="sxs-lookup"><span data-stu-id="43db8-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="43db8-108">Questa esercitazione illustra come scrivere codice ASP.NET per alcuni scenari comuni usando l'Archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="43db8-108">This tutorial shows how to write ASP.NET code for some common scenarios using Azure blob storage.</span></span> <span data-ttu-id="43db8-109">Gli scenari includono la creazione di un contenitore BLOB e il caricamento, la creazione di elenchi, il download e l'eliminazione di BLOB.</span><span class="sxs-lookup"><span data-stu-id="43db8-109">Scenarios include creating a blob container, and uploading, listing, downloading, and deleting blobs.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="43db8-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="43db8-110">Prerequisites</span></span>

* [<span data-ttu-id="43db8-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="43db8-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="43db8-112">Account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="43db8-112">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="43db8-113">Creare un controller MVC</span><span class="sxs-lookup"><span data-stu-id="43db8-113">Create an MVC controller</span></span> 

1. <span data-ttu-id="43db8-114">In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Controller** e selezionare **Aggiungi > Controller** dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="43db8-114">In the **Solution Explorer**, right-click **Controllers**, and, from the context menu, select **Add->Controller**.</span></span>

    ![Aggiungere un controller a un'app MVC ASP.NET](./media/vs-storage-aspnet-getting-started-blobs/add-controller-menu.png)

1. <span data-ttu-id="43db8-116">Nella finestra di dialogo **Aggiungi scaffolding** fare clic su **Controller MVC 5 - Vuoto** e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="43db8-116">On the **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Specificare il tipo di controller MVC](./media/vs-storage-aspnet-getting-started-blobs/add-controller.png)

1. <span data-ttu-id="43db8-118">Nella finestra di dialogo **Aggiungi controller** assegnare un nome al controller *BlobsController*e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="43db8-118">On the **Add Controller** dialog, name the controller *BlobsController*, and select **Add**.</span></span>

    ![Assegnare un nome al controller MVC](./media/vs-storage-aspnet-getting-started-blobs/add-controller-name.png)

1. <span data-ttu-id="43db8-120">Aggiungere le direttive *using* seguenti al file `BlobsController.cs`:</span><span class="sxs-lookup"><span data-stu-id="43db8-120">Add the following *using* directives to the `BlobsController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

## <a name="create-a-blob-container"></a><span data-ttu-id="43db8-121">Creare un contenitore BLOB</span><span class="sxs-lookup"><span data-stu-id="43db8-121">Create a blob container</span></span>

<span data-ttu-id="43db8-122">Un contenitore BLOB è una gerarchia nidificata di BLOB e cartelle.</span><span class="sxs-lookup"><span data-stu-id="43db8-122">A blob container is a nested hierarchy of blobs and folders.</span></span> <span data-ttu-id="43db8-123">I passaggi seguenti illustrano come creare un contenitore BLOB:</span><span class="sxs-lookup"><span data-stu-id="43db8-123">The following steps illustrate how to create a blob container:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="43db8-124">Il codice in questa sezione presuppone che siano stati completati i passaggi descritti nella sezione [Configurare l'ambiente di sviluppo](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="43db8-124">The code in this section assumes that you have completed the steps in the section, [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="43db8-125">Aprire il file `BlobsController.cs` .</span><span class="sxs-lookup"><span data-stu-id="43db8-125">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="43db8-126">Aggiungere un metodo denominato **CreateBlobContainer** che restituisce un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="43db8-126">Add a method called **CreateBlobContainer** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateBlobContainer()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="43db8-127">Nel metodo **CreateBlobContainer** recuperare un oggetto **CloudStorageAccount** che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="43db8-127">Within the **CreateBlobContainer** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="43db8-128">Utilizzare il codice seguente per ottenere la stringa di connessione di archiviazione e le informazioni sull'account di archiviazione dalla configurazione del servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="43db8-128">Use the following code to get the storage connection string and storage account information from the Azure service configuration.</span></span> <span data-ttu-id="43db8-129">Cambiare *&lt;storage-account-name>* con il nome dell'account di archiviazione di Azure a cui si sta eseguendo l'accesso.</span><span class="sxs-lookup"><span data-stu-id="43db8-129">(Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="43db8-130">Recuperare un oggetto **CloudBlobClient** che rappresenta un client del servizio BLOB.</span><span class="sxs-lookup"><span data-stu-id="43db8-130">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="43db8-131">Recuperare un oggetto **CloudBlobContainer** che rappresenta un riferimento al nome del contenitore BLOB desiderato.</span><span class="sxs-lookup"><span data-stu-id="43db8-131">Get a **CloudBlobContainer** object that represents a reference to the desired blob container name.</span></span> <span data-ttu-id="43db8-132">Il metodo **CloudBlobClient.GetContainerReference** non esegue una richiesta all'archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="43db8-132">The **CloudBlobClient.GetContainerReference** method does not make a request against blob storage.</span></span> <span data-ttu-id="43db8-133">Il riferimento viene restituito indipendentemente dall'esistenza del contenitore BLOB.</span><span class="sxs-lookup"><span data-stu-id="43db8-133">The reference is returned whether or not the blob container exists.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="43db8-134">Chiamare il metodo **CloudBlobContainer.CreateIfNotExists** per creare il contenitore, se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="43db8-134">Call the **CloudBlobContainer.CreateIfNotExists** method to create the container if it does not yet exist.</span></span> <span data-ttu-id="43db8-135">Il metodo **CloudBlobContainer.CreateIfNotExists** restituisce **true** se il contenitore non esiste e il contenitore viene creato.</span><span class="sxs-lookup"><span data-stu-id="43db8-135">The **CloudBlobContainer.CreateIfNotExists** method returns **true** if the container does not exist, and is successfully created.</span></span> <span data-ttu-id="43db8-136">In caso contrario, viene restituito **false**.</span><span class="sxs-lookup"><span data-stu-id="43db8-136">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = container.CreateIfNotExists();
    ```

1. <span data-ttu-id="43db8-137">Aggiornare **ViewBag** con il nome del contenitore BLOB.</span><span class="sxs-lookup"><span data-stu-id="43db8-137">Update the **ViewBag** with the name of the blob container.</span></span>

    ```csharp
    ViewBag.BlobContainerName = container.Name;
    ```

1. <span data-ttu-id="43db8-138">In **Esplora soluzioni** espandere la cartella **Views**, fare clic con il pulsante destro del mouse su **BLOB** e dal menu di scelta rapida selezionare **Aggiungi->Visualizzazione**.</span><span class="sxs-lookup"><span data-stu-id="43db8-138">In the **Solution Explorer**, expand the **Views** folder, right-click **Blobs**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="43db8-139">Nella finestra di dialogo **Aggiungi visualizzazione** immettere **CreateBlobContainer** per il nome della visualizzazione e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="43db8-139">On the **Add View** dialog, enter **CreateBlobContainer** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="43db8-140">Aprire `CreateBlobContainer.cshtml` e modificarlo in modo che l'aspetto sia simile al frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="43db8-140">Open `CreateBlobContainer.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Blob Container";
    }
    
    <h2>Create Blob Container results</h2>

    Creation of @ViewBag.BlobContainerName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="43db8-141">In **Esplora soluzioni** espandere la cartella **Views->Shared** e aprire `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="43db8-141">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="43db8-142">Dopo l'ultimo **Html.ActionLink**, aggiungere il seguente **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="43db8-142">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create blob container", "CreateBlobContainer", "Blobs")</li>
    ```

1. <span data-ttu-id="43db8-143">Eseguire l'applicazione e selezionare **Crea contenitore BLOB** per visualizzare risultati simili allo screenshot seguente:</span><span class="sxs-lookup"><span data-stu-id="43db8-143">Run the application, and select **Create Blob Container** to see results similar to the following screen shot:</span></span>
  
    ![Creare un contenitore BLOB](./media/vs-storage-aspnet-getting-started-blobs/create-blob-container-results.png)

    <span data-ttu-id="43db8-145">Come accennato in precedenza, il metodo **CloudBlobContainer.CreateIfNotExists** restituisce **true** solo quando il contenitore non esiste e viene creato.</span><span class="sxs-lookup"><span data-stu-id="43db8-145">As mentioned previously, the **CloudBlobContainer.CreateIfNotExists** method returns **true** only when the container doesn't exist and is created.</span></span> <span data-ttu-id="43db8-146">Se quindi si esegue l'app quando il contenitore esiste, il metodo restituisce **false**.</span><span class="sxs-lookup"><span data-stu-id="43db8-146">Therefore, if you run the app when the container exists, the method returns **false**.</span></span> <span data-ttu-id="43db8-147">Per eseguire l'app più volte, è necessario eliminare il contenitore prima di eseguire di nuovo l'app.</span><span class="sxs-lookup"><span data-stu-id="43db8-147">To run the app multiple times, you must delete the container before running the app again.</span></span> <span data-ttu-id="43db8-148">È possibile eliminare il contenitore usando il metodo **CloudBlobContainer.Delete**.</span><span class="sxs-lookup"><span data-stu-id="43db8-148">Deleting the container can be done via the **CloudBlobContainer.Delete** method.</span></span> <span data-ttu-id="43db8-149">È possibile anche eliminare il contenitore usando il [portale Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) o [Esplora archivi di Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="43db8-149">You can also delete the container using the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="upload-a-blob-into-a-blob-container"></a><span data-ttu-id="43db8-150">Caricare un BLOB in un contenitore BLOB</span><span class="sxs-lookup"><span data-stu-id="43db8-150">Upload a blob into a blob container</span></span>

<span data-ttu-id="43db8-151">Dopo avere [creato un contenitore BLOB](#create-a-blob-container), è possibile caricare file in questo contenitore.</span><span class="sxs-lookup"><span data-stu-id="43db8-151">Once you've [created a blob container](#create-a-blob-container), you can upload files into that container.</span></span> <span data-ttu-id="43db8-152">Questa sezione illustra come caricare un file locale in un contenitore BLOB.</span><span class="sxs-lookup"><span data-stu-id="43db8-152">This section walks you through uploading a local file to a blob container.</span></span> <span data-ttu-id="43db8-153">Nei passaggi si presuppone che sia stato creato un contenitore BLOB denominato *test-blob-container*.</span><span class="sxs-lookup"><span data-stu-id="43db8-153">The steps assume you've created a blob container named *test-blob-container*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="43db8-154">Il codice in questa sezione presuppone che siano stati completati i passaggi descritti nella sezione [Configurare l'ambiente di sviluppo](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="43db8-154">The code in this section assumes that you have completed the steps in the section, [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="43db8-155">Aprire il file `BlobsController.cs` .</span><span class="sxs-lookup"><span data-stu-id="43db8-155">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="43db8-156">Aggiungere un metodo denominato **UploadBlob** che restituisce un **EmptyResult**.</span><span class="sxs-lookup"><span data-stu-id="43db8-156">Add a method called **UploadBlob** that returns an **EmptyResult**.</span></span>

    ```csharp
    public EmptyResult UploadBlob()
    {
        // The code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="43db8-157">Nel metodo **UploadBlob** recuperare un oggetto **CloudStorageAccount** che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="43db8-157">Within the **UploadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="43db8-158">Usare il codice seguente per ottenere la stringa di connessione di archiviazione e le informazioni sull'account di archiviazione dalla configurazione del servizio di Azure: sostituire *&lt;storage-account-name>* con il nome dell'account di archiviazione Azure a cui si sta accedendo.</span><span class="sxs-lookup"><span data-stu-id="43db8-158">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="43db8-159">Recuperare un oggetto **CloudBlobClient** che rappresenta un client del servizio BLOB.</span><span class="sxs-lookup"><span data-stu-id="43db8-159">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="43db8-160">Recuperare un oggetto **CloudBlobContainer** che rappresenta un riferimento al nome del contenitore BLOB.</span><span class="sxs-lookup"><span data-stu-id="43db8-160">Get a **CloudBlobContainer** object that represents a reference to the blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="43db8-161">Come illustrato in precedenza, l'Archiviazione di Azure supporta tipi di BLOB diversi.</span><span class="sxs-lookup"><span data-stu-id="43db8-161">As explained earlier, Azure storage supports different blob types.</span></span> <span data-ttu-id="43db8-162">Per recuperare un riferimento a un BLOB di pagine, chiamare il metodo **CloudBlobContainer.GetPageBlobReference**.</span><span class="sxs-lookup"><span data-stu-id="43db8-162">To retrieve a reference to a page blob, call the **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="43db8-163">Per recuperare un riferimento a un BLOB in blocchi, chiamare il metodo **CloudBlobContainer.GetBlockBlobReference**.</span><span class="sxs-lookup"><span data-stu-id="43db8-163">To retrieve a reference to a block blob, call the **CloudBlobContainer.GetBlockBlobReference** method.</span></span> <span data-ttu-id="43db8-164">Nella maggior parte dei casi è consigliabile usare il tipo di BLOB in blocchi.</span><span class="sxs-lookup"><span data-stu-id="43db8-164">Usually, block blob is the recommended type to use.</span></span> <span data-ttu-id="43db8-165">Cambiare <blob-name>* nel nome da assegnare al BLOB una volta caricato.</span><span class="sxs-lookup"><span data-stu-id="43db8-165">(Change <blob-name>* to the name you want to give the blob once uploaded.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="43db8-166">Dopo avere ottenuto un riferimento al BLOB, è possibile caricarvi qualsiasi flusso di dati chiamando il metodo **UploadFromStream** dell'oggetto di riferimento al BLOB.</span><span class="sxs-lookup"><span data-stu-id="43db8-166">Once you have a blob reference, you can upload any data stream to it by calling the blob reference object's **UploadFromStream** method.</span></span> <span data-ttu-id="43db8-167">Il metodo **UploadFromStream** crea il BLOB, se non esiste, o lo sovrascrive, se esiste.</span><span class="sxs-lookup"><span data-stu-id="43db8-167">The **UploadFromStream** method creates the blob if it doesn't exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="43db8-168">Cambiare *&lt;file-to-upload>* in un percorso completo del file da caricare.</span><span class="sxs-lookup"><span data-stu-id="43db8-168">(Change *&lt;file-to-upload>* to a fully qualified path to the file you want to upload.)</span></span>

    ```csharp
    using (var fileStream = System.IO.File.OpenRead(<file-to-upload>))
    {
        blob.UploadFromStream(fileStream);
    }
    ```

1. <span data-ttu-id="43db8-169">In **Esplora soluzioni** espandere la cartella **Views**, fare clic con il pulsante destro del mouse su **BLOB** e dal menu di scelta rapida selezionare **Aggiungi->Visualizzazione**.</span><span class="sxs-lookup"><span data-stu-id="43db8-169">In the **Solution Explorer**, expand the **Views** folder, right-click **Blobs**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="43db8-170">In **Esplora soluzioni** espandere la cartella **Views->Shared** e aprire `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="43db8-170">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="43db8-171">Dopo l'ultimo **Html.ActionLink**, aggiungere il seguente **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="43db8-171">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Upload blob", "UploadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="43db8-172">Eseguire l'applicazione e selezionare **Carica BLOB**.</span><span class="sxs-lookup"><span data-stu-id="43db8-172">Run the application, and select **Upload blob**.</span></span>  
  
<span data-ttu-id="43db8-173">La sezione [Elencare i BLOB in un contenitore BLOB](#list-the-blobs-in-a-blob-container) illustra come elencare i BLOB in un contenitore BLOB.</span><span class="sxs-lookup"><span data-stu-id="43db8-173">The section - [List the blobs in a blob container](#list-the-blobs-in-a-blob-container) - illustrates how to list the blobs in a blob container.</span></span>    

## <a name="list-the-blobs-in-a-blob-container"></a><span data-ttu-id="43db8-174">Elencare i BLOB in un contenitore BLOB</span><span class="sxs-lookup"><span data-stu-id="43db8-174">List the blobs in a blob container</span></span>

<span data-ttu-id="43db8-175">Questa sezione illustra come elencare i BLOB in un contenitore BLOB.</span><span class="sxs-lookup"><span data-stu-id="43db8-175">This section illustrates how to list the blobs in a blob container.</span></span> <span data-ttu-id="43db8-176">Il codice di esempio fa riferimento al *test-blob-container* creato nella sezione [Creare un contenitore BLOB](#create-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="43db8-176">The sample code references the *test-blob-container* created in the section, [Create a blob container](#create-a-blob-container).</span></span>

> [!NOTE]
> 
> <span data-ttu-id="43db8-177">Il codice in questa sezione presuppone che siano stati completati i passaggi descritti nella sezione [Configurare l'ambiente di sviluppo](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="43db8-177">The code in this section assumes that you have completed the steps in the section, [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="43db8-178">Aprire il file `BlobsController.cs` .</span><span class="sxs-lookup"><span data-stu-id="43db8-178">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="43db8-179">Aggiungere un metodo denominato **ListBlobs** che restituisce un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="43db8-179">Add a method called **ListBlobs** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ListBlobs()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="43db8-180">Nel metodo **ListBlobs** recuperare un oggetto **CloudStorageAccount** che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="43db8-180">Within the **ListBlobs** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="43db8-181">Usare il codice seguente per ottenere la stringa di connessione di archiviazione e le informazioni sull'account di archiviazione dalla configurazione del servizio di Azure: sostituire *&lt;storage-account-name>* con il nome dell'account di archiviazione Azure a cui si sta accedendo.</span><span class="sxs-lookup"><span data-stu-id="43db8-181">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="43db8-182">Recuperare un oggetto **CloudBlobClient** che rappresenta un client del servizio BLOB.</span><span class="sxs-lookup"><span data-stu-id="43db8-182">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="43db8-183">Recuperare un oggetto **CloudBlobContainer** che rappresenta un riferimento al nome del contenitore BLOB.</span><span class="sxs-lookup"><span data-stu-id="43db8-183">Get a **CloudBlobContainer** object that represents a reference to the blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="43db8-184">Per elencare i BLOB in un contenitore BLOB, usare il metodo **CloudBlobContainer.ListBlobs**.</span><span class="sxs-lookup"><span data-stu-id="43db8-184">To list the blobs in a blob container, use the **CloudBlobContainer.ListBlobs** method.</span></span> <span data-ttu-id="43db8-185">Il metodo **CloudBlobContainer.ListBlobs** restituisce un oggetto **IListBlobItem** che viene trasmesso a un oggetto **CloudBlockBlob**, **CloudPageBlob** o **CloudBlobDirectory**.</span><span class="sxs-lookup"><span data-stu-id="43db8-185">The **CloudBlobContainer.ListBlobs** method returns an **IListBlobItem** object that you cast to a **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="43db8-186">Il seguente frammento di codice enumera tutti i BLOB in un contenitore BLOB.</span><span class="sxs-lookup"><span data-stu-id="43db8-186">The following code snippet enumerates all the blobs in a blob container.</span></span> <span data-ttu-id="43db8-187">Ogni BLOB trasmesso all'oggetto appropriato in base al tipo e il suo nome (o URI nel caso di una **CloudBlobDirectory**) viene aggiunto a un elenco.</span><span class="sxs-lookup"><span data-stu-id="43db8-187">Each blob is cast to the appropriate object based on its type, and its name (or URI in the case of a **CloudBlobDirectory**) is added to a list.</span></span>

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

    <span data-ttu-id="43db8-188">I contenitori BLOB possono contenere directory, oltre ai BLOB.</span><span class="sxs-lookup"><span data-stu-id="43db8-188">In addition to blobs, blob containers can contain directories.</span></span> <span data-ttu-id="43db8-189">Se ad esempio si esamina un contenitore BLOB denominato *test-blob-container* con la gerarchia seguente:</span><span class="sxs-lookup"><span data-stu-id="43db8-189">Let's suppose you have a blob container called *test-blob-container* with the following hierarchy:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

    <span data-ttu-id="43db8-190">Con l'esempio di codice precedente, l'elenco di stringhe **blobs** contiene valori simili ai seguenti:</span><span class="sxs-lookup"><span data-stu-id="43db8-190">Using the preceding code example, the **blobs** string list contains values similar to the following:</span></span>

        foo.png
        <storage-account-url>/test-blob-container/dir1
        <storage-account-url>/test-blob-container/dir2

    <span data-ttu-id="43db8-191">Come può notare, l'elenco include solo le entità di livello superiore, non quelle annidate (*bar.png* e *baz.png*).</span><span class="sxs-lookup"><span data-stu-id="43db8-191">As you can see, the list includes only the top-level entities; not the nested ones (*bar.png* and *baz.png*).</span></span> <span data-ttu-id="43db8-192">Per elencare tutte le entità all'interno di un contenitore BLOB, è necessario chiamare il metodo **CloudBlobContainer.ListBlobs** e passare **true** per il parametro **useFlatBlobListing**.</span><span class="sxs-lookup"><span data-stu-id="43db8-192">To list all the entities within a blob container, you must call the **CloudBlobContainer.ListBlobs** method and pass **true** for the **useFlatBlobListing** parameter.</span></span>    

    ```csharp
    ...
    foreach (IListBlobItem item in container.ListBlobs(useFlatBlobListing:true))
    ...
    ```

    <span data-ttu-id="43db8-193">L'impostazione del parametro **useFlatBlobListing** su **true** restituisce un elenco semplice di tutte le entità nel contenitore BLOB e genera i risultati seguenti:</span><span class="sxs-lookup"><span data-stu-id="43db8-193">Setting the **useFlatBlobListing** parameter to **true** returns a flat listing of all entities in the blob container, and yields the following results:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

1. <span data-ttu-id="43db8-194">In **Esplora soluzioni** espandere la cartella **Views**, fare clic con il pulsante destro del mouse su **BLOB** e dal menu di scelta rapida selezionare **Aggiungi->Visualizzazione**.</span><span class="sxs-lookup"><span data-stu-id="43db8-194">In the **Solution Explorer**, expand the **Views** folder, right-click **Blobs**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="43db8-195">Nella finestra di dialogo **Aggiungi visualizzazione** immettere **ListBlobs** per il nome della visualizzazione e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="43db8-195">On the **Add View** dialog, enter **ListBlobs** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="43db8-196">Aprire `ListBlobs.cshtml` e modificarlo in modo che l'aspetto sia simile al frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="43db8-196">Open `ListBlobs.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

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

1. <span data-ttu-id="43db8-197">In **Esplora soluzioni** espandere la cartella **Views->Shared** e aprire `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="43db8-197">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="43db8-198">Dopo l'ultimo **Html.ActionLink**, aggiungere il seguente **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="43db8-198">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("List blobs", "ListBlobs", "Blobs")</li>
    ```

1. <span data-ttu-id="43db8-199">Eseguire l'applicazione e selezionare **List blobs** (Elenca BLOB) per visualizzare risultati simili allo screenshot seguente:</span><span class="sxs-lookup"><span data-stu-id="43db8-199">Run the application, and select **List blobs** to see results similar to the following screen shot:</span></span>
  
    ![Elenco di BLOB](./media/vs-storage-aspnet-getting-started-blobs/listblobs.png)

## <a name="download-blobs"></a><span data-ttu-id="43db8-201">Scaricare BLOB</span><span class="sxs-lookup"><span data-stu-id="43db8-201">Download blobs</span></span>

<span data-ttu-id="43db8-202">Questa sezione illustra come scaricare un BLOB e salvarlo in modo permanente nell'archiviazione locale o leggere il contenuto in una stringa.</span><span class="sxs-lookup"><span data-stu-id="43db8-202">This section illustrates how to download a blob and either persist it to local storage or read the contents into a string.</span></span> <span data-ttu-id="43db8-203">Il codice di esempio fa riferimento al *test-blob-container* creato nella sezione [Creare un contenitore BLOB](#create-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="43db8-203">The sample code references the *test-blob-container* created in the section, [Create a blob container](#create-a-blob-container).</span></span>

1. <span data-ttu-id="43db8-204">Aprire il file `BlobsController.cs` .</span><span class="sxs-lookup"><span data-stu-id="43db8-204">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="43db8-205">Aggiungere un metodo denominato **DownloadBlob** che restituisce un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="43db8-205">Add a method called **DownloadBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DownloadBlob()
    {
        // The code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="43db8-206">Nel metodo **DownloadBlob** recuperare un oggetto **CloudStorageAccount** che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="43db8-206">Within the **DownloadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="43db8-207">Usare il codice seguente per ottenere la stringa di connessione di archiviazione e le informazioni sull'account di archiviazione dalla configurazione del servizio di Azure: sostituire *&lt;storage-account-name>* con il nome dell'account di archiviazione Azure a cui si sta accedendo.</span><span class="sxs-lookup"><span data-stu-id="43db8-207">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="43db8-208">Recuperare un oggetto **CloudBlobClient** che rappresenta un client del servizio BLOB.</span><span class="sxs-lookup"><span data-stu-id="43db8-208">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="43db8-209">Recuperare un oggetto **CloudBlobContainer** che rappresenta un riferimento al nome del contenitore BLOB.</span><span class="sxs-lookup"><span data-stu-id="43db8-209">Get a **CloudBlobContainer** object that represents a reference to the blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="43db8-210">Recuperare un oggetto di riferimento al BLOB chiamando il metodo **CloudBlobContainer.GetBlockBlobReference** o **CloudBlobContainer.GetPageBlobReference**.</span><span class="sxs-lookup"><span data-stu-id="43db8-210">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="43db8-211">Cambiare *&lt;blob-name>* nel nome del BLOB che si sta scaricando.</span><span class="sxs-lookup"><span data-stu-id="43db8-211">(Change *&lt;blob-name>* to the name of the blob you are downloading.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="43db8-212">Per scaricare un BLOB, usare il metodo **CloudBlockBlob.DownloadToStream** o **CloudPageBlob.DownloadToStream**, a seconda del tipo di BLOB.</span><span class="sxs-lookup"><span data-stu-id="43db8-212">To download a blob, use the **CloudBlockBlob.DownloadToStream** or **CloudPageBlob.DownloadToStream** method, depending on the blob type.</span></span> <span data-ttu-id="43db8-213">Il frammento di codice seguente usa il metodo **CloudBlockBlob.DownloadToStream** per trasferire il contenuto di un BLOB a un oggetto flusso che viene salvato in modo permanente in un file locale: modificare *&lt;local-file-name>* nel nome del file completo che rappresenta il percorso in cui scaricare il BLOB.</span><span class="sxs-lookup"><span data-stu-id="43db8-213">The following code snippet uses the **CloudBlockBlob.DownloadToStream** method to transfer a blob's contents to a stream object that is then persisted to a local file: (Change *&lt;local-file-name>* to the fully qualified file name representing where you want the blob downloaded.)</span></span> 

    ```csharp
    using (var fileStream = System.IO.File.OpenWrite(<local-file-name>))
    {
        blob.DownloadToStream(fileStream);
    }
    ```

1. <span data-ttu-id="43db8-214">In **Esplora soluzioni** espandere la cartella **Views->Shared** e aprire `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="43db8-214">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="43db8-215">Dopo l'ultimo **Html.ActionLink**, aggiungere il seguente **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="43db8-215">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Download blob", "DownloadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="43db8-216">Eseguire l'applicazione e selezionare **Scarica BLOB** per scaricare il BLOB.</span><span class="sxs-lookup"><span data-stu-id="43db8-216">Run the application, and select **Download blob** to download the blob.</span></span> <span data-ttu-id="43db8-217">Il BLOB specificato nella chiamata al metodo **CloudBlobContainer.GetBlockBlobReference** viene scaricato nel percorso specificato nella chiamata al metodo **File.OpenWrite**.</span><span class="sxs-lookup"><span data-stu-id="43db8-217">The blob specified in the **CloudBlobContainer.GetBlockBlobReference** method call downloads to the location you specify in the **File.OpenWrite** method call.</span></span> 

## <a name="delete-blobs"></a><span data-ttu-id="43db8-218">Eliminare BLOB</span><span class="sxs-lookup"><span data-stu-id="43db8-218">Delete blobs</span></span>

<span data-ttu-id="43db8-219">I passaggi seguenti illustrano come eliminare un BLOB:</span><span class="sxs-lookup"><span data-stu-id="43db8-219">The following steps illustrate how to delete a blob:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="43db8-220">Il codice in questa sezione presuppone che siano stati completati i passaggi descritti nella sezione [Configurare l'ambiente di sviluppo](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="43db8-220">The code in this section assumes that you have completed the steps in the section, [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="43db8-221">Aprire il file `BlobsController.cs` .</span><span class="sxs-lookup"><span data-stu-id="43db8-221">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="43db8-222">Aggiungere un metodo denominato **DeleteBlob** che restituisce un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="43db8-222">Add a method called **DeleteBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DeleteBlob()
    {
        // The code in this section goes here.

        return new EmptyResult();
    }
    ```

1. <span data-ttu-id="43db8-223">Ottenere un oggetto **CloudStorageAccount** che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="43db8-223">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="43db8-224">Usare il codice seguente per ottenere la stringa di connessione di archiviazione e le informazioni sull'account di archiviazione dalla configurazione del servizio di Azure: sostituire *&lt;storage-account-name>* con il nome dell'account di archiviazione Azure a cui si sta accedendo.</span><span class="sxs-lookup"><span data-stu-id="43db8-224">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="43db8-225">Recuperare un oggetto **CloudBlobClient** che rappresenta un client del servizio BLOB.</span><span class="sxs-lookup"><span data-stu-id="43db8-225">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="43db8-226">Recuperare un oggetto **CloudBlobContainer** che rappresenta un riferimento al nome del contenitore BLOB.</span><span class="sxs-lookup"><span data-stu-id="43db8-226">Get a **CloudBlobContainer** object that represents a reference to the blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="43db8-227">Recuperare un oggetto di riferimento al BLOB chiamando il metodo **CloudBlobContainer.GetBlockBlobReference** o **CloudBlobContainer.GetPageBlobReference**.</span><span class="sxs-lookup"><span data-stu-id="43db8-227">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="43db8-228">Cambiare *&lt;blob-name>* nel nome del BLOB che si sta eliminando.</span><span class="sxs-lookup"><span data-stu-id="43db8-228">(Change *&lt;blob-name>* to the name of the blob you are deleting.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
        ```

1. To delete a blob, use the **Delete** method.

    ```csharp
    blob.Delete();
    ```

1. <span data-ttu-id="43db8-229">In **Esplora soluzioni** espandere la cartella **Views->Shared** e aprire `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="43db8-229">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="43db8-230">Dopo l'ultimo **Html.ActionLink**, aggiungere il seguente **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="43db8-230">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete blob", "DeleteBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="43db8-231">Eseguire l'applicazione e selezionare **Elimina BLOB** per eliminare il BLOB specificato nella chiamata al metodo **CloudBlobContainer.GetBlockBlobReference**.</span><span class="sxs-lookup"><span data-stu-id="43db8-231">Run the application, and select **Delete blob** to delete the blob specified in the **CloudBlobContainer.GetBlockBlobReference** method call.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="43db8-232">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="43db8-232">Next steps</span></span>
<span data-ttu-id="43db8-233">Per ulteriori opzioni di archiviazione dei dati in Azure, consultare altre guide alle funzionalità.</span><span class="sxs-lookup"><span data-stu-id="43db8-233">View more feature guides to learn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="43db8-234">Introduzione all'archiviazione tabelle di Azure e ai Servizi connessi di Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="43db8-234">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](vs-storage-aspnet-getting-started-tables.md)
  * [<span data-ttu-id="43db8-235">Introduzione all'archiviazione code di Azure e ai Servizi connessi di Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="43db8-235">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>](vs-storage-aspnet-getting-started-queues.md)
