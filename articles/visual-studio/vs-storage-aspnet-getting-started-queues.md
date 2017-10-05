---
title: Introduzione all'archiviazione code di Azure e ai servizi connessi di Visual Studio (ASP.NET) | Documentazione Microsoft
description: Informazioni su come iniziare a usare l'archiviazione code di Azure in un progetto ASP.NET in Visual Studio dopo aver eseguito la connessione a un account di archiviazione con i servizi connessi di Visual Studio
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 94ca3413-5497-433f-abbe-836f83a9de72
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/23/2016
ms.author: kraigb
ms.openlocfilehash: 4687e5dfce72583728068c176d86d100313badf6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-queue-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="72604-103">Introduzione all'archiviazione code di Azure e ai servizi connessi di Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="72604-103">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="72604-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="72604-104">Overview</span></span>

<span data-ttu-id="72604-105">L'archivio code di Azure fornisce la messaggistica cloud tra i componenti dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="72604-105">Azure queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="72604-106">Durante la progettazione di applicazioni scalabili, i componenti dell'applicazione vengono spesso separati, per poter essere scalati in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="72604-106">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="72604-107">L'archivio code fornisce la messaggistica asincrona per la comunicazione tra i componenti dell'applicazione, che possono essere eseguiti nel cloud, in un desktop, in un server locale o in un dispositivo mobile.</span><span class="sxs-lookup"><span data-stu-id="72604-107">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in the cloud, on the desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="72604-108">Archiviazione code supporta anche la gestione di attività asincrone e la creazione di flussi di lavoro dei processi.</span><span class="sxs-lookup"><span data-stu-id="72604-108">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

<span data-ttu-id="72604-109">Questa esercitazione illustra come scrivere codice ASP.NET per alcuni scenari comuni usando le entità di archiviazione code di Azure.</span><span class="sxs-lookup"><span data-stu-id="72604-109">This tutorial shows how to write ASP.NET code for some common scenarios using Azure queue storage entities.</span></span> <span data-ttu-id="72604-110">Tali scenari includono attività comuni, ad esempio la creazione di una coda di Azure e l'aggiunta, modifica, lettura e rimozione dei messaggi in coda.</span><span class="sxs-lookup"><span data-stu-id="72604-110">These scenarios include common tasks such as creating an Azure queue, and adding, modifying, reading, and removing queue messages.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="72604-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="72604-111">Prerequisites</span></span>

* [<span data-ttu-id="72604-112">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="72604-112">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="72604-113">Account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="72604-113">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="72604-114">Creare un controller MVC</span><span class="sxs-lookup"><span data-stu-id="72604-114">Create an MVC controller</span></span> 

1. <span data-ttu-id="72604-115">In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Controller** e selezionare **Aggiungi > Controller** dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="72604-115">In the **Solution Explorer**, right-click **Controllers**, and, from the context menu, select **Add->Controller**.</span></span>

    ![Aggiungere un controller a un'app MVC ASP.NET](./media/vs-storage-aspnet-getting-started-queues/add-controller-menu.png)

1. <span data-ttu-id="72604-117">Nella finestra di dialogo **Aggiungi scaffolding** fare clic su **Controller MVC 5 - Vuoto** e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="72604-117">On the **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Specificare il tipo di controller MVC](./media/vs-storage-aspnet-getting-started-queues/add-controller.png)

1. <span data-ttu-id="72604-119">Nella finestra di dialogo **Aggiungi controller** assegnare il nome *QueuesController* al controller e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="72604-119">On the **Add Controller** dialog, name the controller *QueuesController*, and select **Add**.</span></span>

    ![Assegnare un nome al controller MVC](./media/vs-storage-aspnet-getting-started-queues/add-controller-name.png)

1. <span data-ttu-id="72604-121">Aggiungere le direttive *using* seguenti al file `QueuesController.cs`:</span><span class="sxs-lookup"><span data-stu-id="72604-121">Add the following *using* directives to the `QueuesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Queue;
    ```
## <a name="create-a-queue"></a><span data-ttu-id="72604-122">Creare una coda</span><span class="sxs-lookup"><span data-stu-id="72604-122">Create a queue</span></span>

<span data-ttu-id="72604-123">I passaggi seguenti illustrano come creare una coda:</span><span class="sxs-lookup"><span data-stu-id="72604-123">The following steps illustrate how to create a queue:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="72604-124">Questa sezione presuppone che siano stati completati i passaggi descritti in [Configurare l'ambiente di sviluppo](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="72604-124">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="72604-125">Aprire il file `QueuesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="72604-125">Open the `QueuesController.cs` file.</span></span> 

1. <span data-ttu-id="72604-126">Aggiungere un metodo denominato **CreateQueue** che restituisce un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="72604-126">Add a method called **CreateQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateQueue()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="72604-127">Nel metodo **CreateQueue** recuperare un oggetto **CloudStorageAccount** che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="72604-127">Within the **CreateQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="72604-128">Usare il codice seguente per ottenere la stringa di connessione di archiviazione e le informazioni sull'account di archiviazione dalla configurazione del servizio di Azure: sostituire *&lt;storage-account-name>* con il nome dell'account di archiviazione Azure a cui si sta accedendo.</span><span class="sxs-lookup"><span data-stu-id="72604-128">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="72604-129">Ottenere un oggetto **CloudQueueClient** che rappresenta un client del servizio di accodamento.</span><span class="sxs-lookup"><span data-stu-id="72604-129">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```
1. <span data-ttu-id="72604-130">Ottenere un oggetto **CloudQueue** che rappresenta un riferimento al nome della coda desiderata.</span><span class="sxs-lookup"><span data-stu-id="72604-130">Get a **CloudQueue** object that represents a reference to the desired queue name.</span></span> <span data-ttu-id="72604-131">Il metodo **CloudQueueClient.GetQueueReference** non esegue una richiesta all'archiviazione code.</span><span class="sxs-lookup"><span data-stu-id="72604-131">The **CloudQueueClient.GetQueueReference** method does not make a request against queue storage.</span></span> <span data-ttu-id="72604-132">Il riferimento viene restituito indipendentemente dall'esistenza della coda.</span><span class="sxs-lookup"><span data-stu-id="72604-132">The reference is returned whether or not the queue exists.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="72604-133">Chiamare il metodo **CloudQueue.CreateIfNotExists** per creare la coda se non esiste.</span><span class="sxs-lookup"><span data-stu-id="72604-133">Call the **CloudQueue.CreateIfNotExists** method to create the queue if it does not yet exist.</span></span> <span data-ttu-id="72604-134">Il metodo **CloudQueue.CreateIfNotExists** restituisce **true** se la coda non esiste e viene creata correttamente.</span><span class="sxs-lookup"><span data-stu-id="72604-134">The **CloudQueue.CreateIfNotExists** method returns **true** if the queue does not exist, and is successfully created.</span></span> <span data-ttu-id="72604-135">In caso contrario, viene restituito **false**.</span><span class="sxs-lookup"><span data-stu-id="72604-135">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = queue.CreateIfNotExists();
    ```

1. <span data-ttu-id="72604-136">Aggiornare **ViewBag** con il nome della coda.</span><span class="sxs-lookup"><span data-stu-id="72604-136">Update the **ViewBag** with the name of the queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```

1. <span data-ttu-id="72604-137">In **Esplora soluzioni** espandere la cartella **Views**, fare clic con il pulsante destro del mouse su **Code** e dal menu di scelta rapida selezionare **Aggiungi->Visualizzazione**.</span><span class="sxs-lookup"><span data-stu-id="72604-137">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="72604-138">Nella finestra di dialogo **Aggiungi visualizzazione** immettere **CreateQueue** per il nome della visualizzazione e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="72604-138">On the **Add View** dialog, enter **CreateQueue** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="72604-139">Aprire `CreateQueue.cshtml` e modificarlo in modo che l'aspetto sia simile al frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="72604-139">Open `CreateQueue.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Queue";
    }
    
    <h2>Create Queue results</h2>

    Creation of @ViewBag.QueueName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="72604-140">In **Esplora soluzioni** espandere la cartella **Views->Shared** e aprire `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="72604-140">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="72604-141">Dopo l'ultimo **Html.ActionLink**, aggiungere il seguente **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="72604-141">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create queue", "CreateQueue", "Queues")</li>
    ```

1. <span data-ttu-id="72604-142">Eseguire l'applicazione e selezionare **Crea coda** per visualizzare risultati simili allo screenshot seguente:</span><span class="sxs-lookup"><span data-stu-id="72604-142">Run the application, and select **Create queue** to see results similar to the following screen shot:</span></span>
  
    ![Crea coda](./media/vs-storage-aspnet-getting-started-queues/create-queue-results.png)

    <span data-ttu-id="72604-144">Come accennato in precedenza, il metodo **CloudQueue.CreateIfNotExists** restituisce **true** solo quando la coda non esiste e viene creata.</span><span class="sxs-lookup"><span data-stu-id="72604-144">As mentioned previously, the **CloudQueue.CreateIfNotExists** method returns **true** only when the queue doesn't exist and is created.</span></span> <span data-ttu-id="72604-145">Se quindi si esegue l'app quando la coda esiste, il metodo restituisce **false**.</span><span class="sxs-lookup"><span data-stu-id="72604-145">Therefore, if you run the app when the queue exists, the method returns **false**.</span></span> <span data-ttu-id="72604-146">Per eseguire l'app più volte, è necessario eliminare la coda prima di eseguire di nuovo l'app.</span><span class="sxs-lookup"><span data-stu-id="72604-146">To run the app multiple times, you must delete the queue before running the app again.</span></span> <span data-ttu-id="72604-147">L'eliminazione della coda può essere eseguita tramite il metodo **CloudQueue.Delete**.</span><span class="sxs-lookup"><span data-stu-id="72604-147">Deleting the queue can be done via the **CloudQueue.Delete** method.</span></span> <span data-ttu-id="72604-148">È possibile anche eliminare la coda usando il [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) o [Esplora archivi di Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="72604-148">You can also delete the queue using the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="72604-149">Aggiungere un messaggio a una coda</span><span class="sxs-lookup"><span data-stu-id="72604-149">Add a message to a queue</span></span>

<span data-ttu-id="72604-150">Dopo aver [creato una coda](#create-a-queue) è possibile aggiungervi dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="72604-150">Once you've [created a queue](#create-a-queue), you can add messages to that queue.</span></span> <span data-ttu-id="72604-151">Questa sezione illustra i passaggi per aggiungere un messaggio alla coda *test-queue*.</span><span class="sxs-lookup"><span data-stu-id="72604-151">This section walks you through adding a message to a queue *test-queue*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="72604-152">Questa sezione presuppone che siano stati completati i passaggi descritti in [Configurare l'ambiente di sviluppo](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="72604-152">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="72604-153">Aprire il file `QueuesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="72604-153">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="72604-154">Aggiungere un metodo denominato **AddMessage** che restituisce un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="72604-154">Add a method called **AddMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddMessage()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="72604-155">Nel metodo **AddMessage** recuperare un oggetto **CloudStorageAccount** che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="72604-155">Within the **AddMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="72604-156">Usare il codice seguente per ottenere la stringa di connessione di archiviazione e le informazioni sull'account di archiviazione dalla configurazione del servizio di Azure: sostituire *&lt;storage-account-name>* con il nome dell'account di archiviazione Azure a cui si sta accedendo.</span><span class="sxs-lookup"><span data-stu-id="72604-156">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="72604-157">Ottenere un oggetto **CloudQueueClient** che rappresenta un client del servizio di accodamento.</span><span class="sxs-lookup"><span data-stu-id="72604-157">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="72604-158">Ottenere un oggetto **CloudQueueContainer** che rappresenta un riferimento alla coda.</span><span class="sxs-lookup"><span data-stu-id="72604-158">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="72604-159">Creare l'oggetto **CloudQueueMessage** che rappresenta il messaggio da aggiungere alla coda.</span><span class="sxs-lookup"><span data-stu-id="72604-159">Create the **CloudQueueMessage** object representing the message you want to add to the queue.</span></span> <span data-ttu-id="72604-160">È possibile creare un oggetto **CloudQueueMessage** da una stringa in formato UTF-8 o da una matrice di byte.</span><span class="sxs-lookup"><span data-stu-id="72604-160">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

    ```csharp
    CloudQueueMessage message = new CloudQueueMessage("Hello, Azure Queue Storage");
    ```

1. <span data-ttu-id="72604-161">Chiamare il metodo **CloudQueue.AddMessage** per aggiungere il messaggio alla coda.</span><span class="sxs-lookup"><span data-stu-id="72604-161">Call the **CloudQueue.AddMessage** method to add the messaged to the queue.</span></span>

    ```csharp
    queue.AddMessage(message);
    ```

1. <span data-ttu-id="72604-162">Creare e impostare un paio di proprietà **ViewBag** per la visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="72604-162">Create and set a couple of **ViewBag** properties for display in the view.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```

1. <span data-ttu-id="72604-163">In **Esplora soluzioni** espandere la cartella **Views**, fare clic con il pulsante destro del mouse su **Code** e dal menu di scelta rapida selezionare **Aggiungi->Visualizzazione**.</span><span class="sxs-lookup"><span data-stu-id="72604-163">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="72604-164">Nella finestra di dialogo **Aggiungi visualizzazione** immettere **AddMessage** per il nome della visualizzazione e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="72604-164">On the **Add View** dialog, enter **AddMessage** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="72604-165">Aprire `AddMessage.cshtml` e modificarlo in modo che l'aspetto sia simile al frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="72604-165">Open `AddMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add Message";
    }
    
    <h2>Add Message results</h2>
    
    The message '@ViewBag.Message' was added to the queue '@ViewBag.QueueName'.
    ```

1. <span data-ttu-id="72604-166">In **Esplora soluzioni** espandere la cartella **Views->Shared** e aprire `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="72604-166">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="72604-167">Dopo l'ultimo **Html.ActionLink**, aggiungere il seguente **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="72604-167">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add message", "AddMessage", "Queues")</li>
    ```

1. <span data-ttu-id="72604-168">Eseguire l'applicazione e selezionare **Aggiungi messaggio** per visualizzare risultati simili allo screenshot seguente:</span><span class="sxs-lookup"><span data-stu-id="72604-168">Run the application, and select **Add message** to see results similar to the following screen shot:</span></span>
  
    ![Aggiungi messaggio](./media/vs-storage-aspnet-getting-started-queues/add-message-results.png)

<span data-ttu-id="72604-170">Le sezioni [Leggere un messaggio da una coda senza rimuoverlo](#read-a-message-from-a-queue-without-removing-it) e [Leggere e rimuovere un messaggio da una coda](#read-and-remove-a-message-from-a-queue) illustrano come leggere i messaggi da una coda.</span><span class="sxs-lookup"><span data-stu-id="72604-170">The two sections - [Read a message from a queue without removing it](#read-a-message-from-a-queue-without-removing-it) and [Read and remove a message from a queue](#read-and-remove-a-message-from-a-queue) - illustrate how to read messages from a queue.</span></span>    

## <a name="read-a-message-from-a-queue-without-removing-it"></a><span data-ttu-id="72604-171">Leggere un messaggio da una coda senza rimuoverlo</span><span class="sxs-lookup"><span data-stu-id="72604-171">Read a message from a queue without removing it</span></span>

<span data-ttu-id="72604-172">Questa sezione illustra come visualizzare un messaggio in coda (leggere il primo messaggio senza rimuoverlo).</span><span class="sxs-lookup"><span data-stu-id="72604-172">This section illustrates how to peek at a queued message (read the first message without removing it).</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="72604-173">Questa sezione presuppone che siano stati completati i passaggi descritti in [Configurare l'ambiente di sviluppo](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="72604-173">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="72604-174">Aprire il file `QueuesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="72604-174">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="72604-175">Aggiungere un metodo denominato **PeekMessage** che restituisce un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="72604-175">Add a method called **PeekMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult PeekMessage()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="72604-176">Nel metodo **PeekMessage** recuperare un oggetto **CloudStorageAccount** che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="72604-176">Within the **PeekMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="72604-177">Usare il codice seguente per ottenere la stringa di connessione di archiviazione e le informazioni sull'account di archiviazione dalla configurazione del servizio di Azure: sostituire *&lt;storage-account-name>* con il nome dell'account di archiviazione Azure a cui si sta accedendo.</span><span class="sxs-lookup"><span data-stu-id="72604-177">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="72604-178">Ottenere un oggetto **CloudQueueClient** che rappresenta un client del servizio di accodamento.</span><span class="sxs-lookup"><span data-stu-id="72604-178">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="72604-179">Ottenere un oggetto **CloudQueueContainer** che rappresenta un riferimento alla coda.</span><span class="sxs-lookup"><span data-stu-id="72604-179">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="72604-180">Chiamare il metodo **CloudQueue.PeekMessage** per leggere il primo messaggio di una coda senza rimuoverlo dalla coda.</span><span class="sxs-lookup"><span data-stu-id="72604-180">Call the **CloudQueue.PeekMessage** method to read the first message in the queue without removing it from the queue.</span></span> 

    ```csharp
    CloudQueueMessage message = queue.PeekMessage();
    ```

1. <span data-ttu-id="72604-181">Aggiornare **ViewBag** con due valori: il nome della coda e il messaggio letto.</span><span class="sxs-lookup"><span data-stu-id="72604-181">Update the **ViewBag** with two values: the queue name and the message that was read.</span></span> <span data-ttu-id="72604-182">L'oggetto **CloudQueueMessage** espone due proprietà per ottenerne il valore: **CloudQueueMessage.AsBytes** e **CloudQueueMessage.AsString**.</span><span class="sxs-lookup"><span data-stu-id="72604-182">The **CloudQueueMessage** object exposes two properties for getting the object's value: **CloudQueueMessage.AsBytes** and **CloudQueueMessage.AsString**.</span></span> <span data-ttu-id="72604-183">**AsString** (usata in questo esempio) restituisce una stringa, mentre **AsBytes** restituisce una matrice di byte.</span><span class="sxs-lookup"><span data-stu-id="72604-183">**AsString** (used in this example) returns a string, while **AsBytes** returns a byte array.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name; 
    ViewBag.Message = (message != null ? message.AsString : "");
    ```

1. <span data-ttu-id="72604-184">In **Esplora soluzioni** espandere la cartella **Views**, fare clic con il pulsante destro del mouse su **Code** e dal menu di scelta rapida selezionare **Aggiungi->Visualizzazione**.</span><span class="sxs-lookup"><span data-stu-id="72604-184">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="72604-185">Nella finestra di dialogo **Aggiungi visualizzazione** immettere **PeekMessage** per il nome della visualizzazione e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="72604-185">On the **Add View** dialog, enter **PeekMessage** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="72604-186">Aprire `PeekMessage.cshtml` e modificarlo in modo che l'aspetto sia simile al frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="72604-186">Open `PeekMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "PeekMessage";
    }
    
    <h2>Peek Message results</h2>
    
    <table border="1">
        <tr><th>Queue</th><th>Peeked Message</th></tr>
        <tr><td>@ViewBag.QueueName</td><td>@ViewBag.Message</td></tr>
    </table>    
    ```

1. <span data-ttu-id="72604-187">In **Esplora soluzioni** espandere la cartella **Views->Shared** e aprire `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="72604-187">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="72604-188">Dopo l'ultimo **Html.ActionLink**, aggiungere il seguente **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="72604-188">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Peek message", "PeekMessage", "Queues")</li>
    ```

1. <span data-ttu-id="72604-189">Eseguire l'applicazione e selezionare **Visualizza il messaggio** per visualizzare risultati simili allo screenshot seguente:</span><span class="sxs-lookup"><span data-stu-id="72604-189">Run the application, and select **Peek message** to see results similar to the following screen shot:</span></span>
  
    ![Visualizza il messaggio](./media/vs-storage-aspnet-getting-started-queues/peek-message-results.png)

## <a name="read-and-remove-a-message-from-a-queue"></a><span data-ttu-id="72604-191">Leggere e rimuovere un messaggio da una coda</span><span class="sxs-lookup"><span data-stu-id="72604-191">Read and remove a message from a queue</span></span>

<span data-ttu-id="72604-192">In questa sezione viene illustrato come leggere e rimuovere un messaggio da una coda.</span><span class="sxs-lookup"><span data-stu-id="72604-192">In this section, you learn how to read and remove a message from a queue.</span></span>   

> [!NOTE]
> 
> <span data-ttu-id="72604-193">Questa sezione presuppone che siano stati completati i passaggi descritti in [Configurare l'ambiente di sviluppo](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="72604-193">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="72604-194">Aprire il file `QueuesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="72604-194">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="72604-195">Aggiungere un metodo denominato **ReadMessage** che restituisce un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="72604-195">Add a method called **ReadMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ReadMessage()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="72604-196">Nel metodo **ReadMessage** recuperare un oggetto **CloudStorageAccount** che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="72604-196">Within the **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="72604-197">Usare il codice seguente per ottenere la stringa di connessione di archiviazione e le informazioni sull'account di archiviazione dalla configurazione del servizio di Azure: sostituire *&lt;storage-account-name>* con il nome dell'account di archiviazione Azure a cui si sta accedendo.</span><span class="sxs-lookup"><span data-stu-id="72604-197">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="72604-198">Ottenere un oggetto **CloudQueueClient** che rappresenta un client del servizio di accodamento.</span><span class="sxs-lookup"><span data-stu-id="72604-198">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="72604-199">Ottenere un oggetto **CloudQueueContainer** che rappresenta un riferimento alla coda.</span><span class="sxs-lookup"><span data-stu-id="72604-199">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="72604-200">Chiamare il metodo **CloudQueue.GetMessage** per leggere il primo messaggio nella coda.</span><span class="sxs-lookup"><span data-stu-id="72604-200">Call the **CloudQueue.GetMessage** method to read the first message in the queue.</span></span> <span data-ttu-id="72604-201">Il metodo **CloudQueue.GetMessage** rende invisibile il messaggio per 30 secondi (impostazione predefinita) per qualsiasi altro codice che legge i messaggi, in modo che nessun altro codice possa modificare o eliminare il messaggio mentre lo si sta elaborando.</span><span class="sxs-lookup"><span data-stu-id="72604-201">The **CloudQueue.GetMessage** method makes the message invisible for 30 seconds (by default) to any other code reading messages so that no other code can modify or delete the message while your processing it.</span></span> <span data-ttu-id="72604-202">Per modificare l'intervallo di tempo per cui il messaggio rimane invisibile, modificare il parametro **visibilityTimeout** passato al metodo **CloudQueue.GetMessage**.</span><span class="sxs-lookup"><span data-stu-id="72604-202">To change the amount of time the message is invisible, modify the **visibilityTimeout** parameter being passed to the **CloudQueue.GetMessage** method.</span></span>

    ```csharp
    // This message will be invisible to other code for 30 seconds.
    CloudQueueMessage message = queue.GetMessage();     
    ```

1. <span data-ttu-id="72604-203">Chiamare il metodo **CloudQueueMessage.Delete** per eliminare il messaggio dalla coda.</span><span class="sxs-lookup"><span data-stu-id="72604-203">Call the **CloudQueueMessage.Delete** method to delete the message from the queue.</span></span>

    ```csharp
    queue.DeleteMessage(message);
    ```

1. <span data-ttu-id="72604-204">Aggiornare **ViewBag** con il messaggio eliminato e il nome della coda.</span><span class="sxs-lookup"><span data-stu-id="72604-204">Update the **ViewBag** with the message deleted, and the name of the queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```
 
1. <span data-ttu-id="72604-205">In **Esplora soluzioni** espandere la cartella **Views**, fare clic con il pulsante destro del mouse su **Code** e dal menu di scelta rapida selezionare **Aggiungi->Visualizzazione**.</span><span class="sxs-lookup"><span data-stu-id="72604-205">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="72604-206">Nella finestra di dialogo **Aggiungi visualizzazione** immettere **ReadMessage** per il nome della visualizzazione e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="72604-206">On the **Add View** dialog, enter **ReadMessage** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="72604-207">Aprire `ReadMessage.cshtml` e modificarlo in modo che l'aspetto sia simile al frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="72604-207">Open `ReadMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "ReadMessage";
    }
    
    <h2>Read Message results</h2>
    
    <table border="1">
        <tr><th>Queue</th><th>Read (and Deleted) Message</th></tr>
        <tr><td>@ViewBag.QueueName</td><td>@ViewBag.Message</td></tr>
    </table>
    ```

1. <span data-ttu-id="72604-208">In **Esplora soluzioni** espandere la cartella **Views->Shared** e aprire `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="72604-208">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="72604-209">Dopo l'ultimo **Html.ActionLink**, aggiungere il seguente **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="72604-209">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Read/Delete message", "ReadMessage", "Queues")</li>
    ```

1. <span data-ttu-id="72604-210">Eseguire l'applicazione e selezionare **Read/Delete message** (Leggi/Elimina messaggio) per visualizzare risultati simili allo screenshot seguente:</span><span class="sxs-lookup"><span data-stu-id="72604-210">Run the application, and select **Read/Delete message** to see results similar to the following screen shot:</span></span>
  
    ![Read/Delete message (Leggi/Elimina messaggio)](./media/vs-storage-aspnet-getting-started-queues/read-message-results.png)

## <a name="get-the-queue-length"></a><span data-ttu-id="72604-212">Recuperare la lunghezza della coda</span><span class="sxs-lookup"><span data-stu-id="72604-212">Get the queue length</span></span>

<span data-ttu-id="72604-213">In questa sezione viene illustrato come ottenere la lunghezza della coda (numero di messaggi).</span><span class="sxs-lookup"><span data-stu-id="72604-213">This section illustrates how to get the queue length (number of messages).</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="72604-214">Questa sezione presuppone che siano stati completati i passaggi descritti in [Configurare l'ambiente di sviluppo](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="72604-214">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="72604-215">Aprire il file `QueuesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="72604-215">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="72604-216">Aggiungere un metodo denominato **GetQueueLength** che restituisce un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="72604-216">Add a method called **GetQueueLength** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetQueueLength()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="72604-217">Nel metodo **ReadMessage** recuperare un oggetto **CloudStorageAccount** che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="72604-217">Within the **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="72604-218">Usare il codice seguente per ottenere la stringa di connessione di archiviazione e le informazioni sull'account di archiviazione dalla configurazione del servizio di Azure: sostituire *&lt;storage-account-name>* con il nome dell'account di archiviazione Azure a cui si sta accedendo.</span><span class="sxs-lookup"><span data-stu-id="72604-218">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="72604-219">Ottenere un oggetto **CloudQueueClient** che rappresenta un client del servizio di accodamento.</span><span class="sxs-lookup"><span data-stu-id="72604-219">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="72604-220">Ottenere un oggetto **CloudQueueContainer** che rappresenta un riferimento alla coda.</span><span class="sxs-lookup"><span data-stu-id="72604-220">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="72604-221">Chiamare il metodo **CloudQueue.FetchAttributes** per recuperare gli attributi della coda, che includono anche la lunghezza.</span><span class="sxs-lookup"><span data-stu-id="72604-221">Call the **CloudQueue.FetchAttributes** method to retrieve the queue's attributes (including its length).</span></span> 

    ```csharp
    queue.FetchAttributes();
    ```

6. <span data-ttu-id="72604-222">Accedere alla proprietà **CloudQueue.ApproximateMessageCount** per ottenere la lunghezza della coda.</span><span class="sxs-lookup"><span data-stu-id="72604-222">Access the **CloudQueue.ApproximateMessageCount** property to get the queue's length.</span></span>
 
    ```csharp
    int? nMessages = queue.ApproximateMessageCount;
    ```

1. <span data-ttu-id="72604-223">Aggiornare **ViewBag** con il nome e la lunghezza della coda.</span><span class="sxs-lookup"><span data-stu-id="72604-223">Update the **ViewBag** with the name of the queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Length = nMessages;
    ```
 
1. <span data-ttu-id="72604-224">In **Esplora soluzioni** espandere la cartella **Views**, fare clic con il pulsante destro del mouse su **Code** e dal menu di scelta rapida selezionare **Aggiungi->Visualizzazione**.</span><span class="sxs-lookup"><span data-stu-id="72604-224">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="72604-225">Nella finestra di dialogo **Aggiungi visualizzazione** immettere **GetQueueLength** per il nome della visualizzazione e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="72604-225">On the **Add View** dialog, enter **GetQueueLength** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="72604-226">Aprire `GetQueueLengthMessage.cshtml` e modificarlo in modo che l'aspetto sia simile al frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="72604-226">Open `GetQueueLengthMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "GetQueueLength";
    }
    
    <h2>Get Queue Length results</h2>
    
    The queue '@ViewBag.QueueName' has a length of (number of messages): @ViewBag.Length
    ```

1. <span data-ttu-id="72604-227">In **Esplora soluzioni** espandere la cartella **Views->Shared** e aprire `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="72604-227">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="72604-228">Dopo l'ultimo **Html.ActionLink**, aggiungere il seguente **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="72604-228">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get queue length", "GetQueueLength", "Queues")</li>
    ```

1. <span data-ttu-id="72604-229">Eseguire l'applicazione e selezionare **Get queue length** (Ottieni lunghezza coda) per visualizzare risultati simili allo screenshot seguente:</span><span class="sxs-lookup"><span data-stu-id="72604-229">Run the application, and select **Get queue length** to see results similar to the following screen shot:</span></span>
  
    ![Recuperare la lunghezza della coda](./media/vs-storage-aspnet-getting-started-queues/get-queue-length-results.png)


## <a name="delete-a-queue"></a><span data-ttu-id="72604-231">Eliminare una coda</span><span class="sxs-lookup"><span data-stu-id="72604-231">Delete a queue</span></span>
<span data-ttu-id="72604-232">Questa sezione illustra come eliminare una coda.</span><span class="sxs-lookup"><span data-stu-id="72604-232">This section illustrates how to delete a queue.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="72604-233">Questa sezione presuppone che siano stati completati i passaggi descritti in [Configurare l'ambiente di sviluppo](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="72604-233">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="72604-234">Aprire il file `QueuesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="72604-234">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="72604-235">Aggiungere un metodo denominato **DeleteQueue** che restituisce un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="72604-235">Add a method called **DeleteQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteQueue()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="72604-236">Nel metodo **DeleteQueue** recuperare un oggetto **CloudStorageAccount** che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="72604-236">Within the **DeleteQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="72604-237">Usare il codice seguente per ottenere la stringa di connessione di archiviazione e le informazioni sull'account di archiviazione dalla configurazione del servizio di Azure: sostituire *&lt;storage-account-name>* con il nome dell'account di archiviazione Azure a cui si sta accedendo.</span><span class="sxs-lookup"><span data-stu-id="72604-237">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="72604-238">Ottenere un oggetto **CloudQueueClient** che rappresenta un client del servizio di accodamento.</span><span class="sxs-lookup"><span data-stu-id="72604-238">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="72604-239">Ottenere un oggetto **CloudQueueContainer** che rappresenta un riferimento alla coda.</span><span class="sxs-lookup"><span data-stu-id="72604-239">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="72604-240">Chiamare il metodo **CloudQueue.Delete** per eliminare la coda rappresentata dall'oggetto **CloudQueue**.</span><span class="sxs-lookup"><span data-stu-id="72604-240">Call the **CloudQueue.Delete** method to delete the queue represented by the **CloudQueue** object.</span></span>

    ```csharp
    queue.Delete();
    ```

1. <span data-ttu-id="72604-241">Aggiornare **ViewBag** con il nome e la lunghezza della coda.</span><span class="sxs-lookup"><span data-stu-id="72604-241">Update the **ViewBag** with the name of the queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```
 
1. <span data-ttu-id="72604-242">In **Esplora soluzioni** espandere la cartella **Views**, fare clic con il pulsante destro del mouse su **Code** e dal menu di scelta rapida selezionare **Aggiungi->Visualizzazione**.</span><span class="sxs-lookup"><span data-stu-id="72604-242">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="72604-243">Nella finestra di dialogo **Aggiungi visualizzazione** immettere **DeleteQueue** per il nome della visualizzazione e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="72604-243">On the **Add View** dialog, enter **DeleteQueue** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="72604-244">Aprire `DeleteQueue.cshtml` e modificarlo in modo che l'aspetto sia simile al frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="72604-244">Open `DeleteQueue.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "DeleteQueue";
    }
    
    <h2>Delete Queue results</h2>
    
    @ViewBag.QueueName deleted.
    ```

1. <span data-ttu-id="72604-245">In **Esplora soluzioni** espandere la cartella **Views->Shared** e aprire `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="72604-245">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="72604-246">Dopo l'ultimo **Html.ActionLink**, aggiungere il seguente **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="72604-246">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete queue", "DeleteQueue", "Queues")</li>
    ```

1. <span data-ttu-id="72604-247">Eseguire l'applicazione e selezionare **Get queue length** (Ottieni lunghezza coda) per visualizzare risultati simili allo screenshot seguente:</span><span class="sxs-lookup"><span data-stu-id="72604-247">Run the application, and select **Get queue length** to see results similar to the following screen shot:</span></span>
  
    ![Elimina coda](./media/vs-storage-aspnet-getting-started-queues/delete-queue-results.png)

## <a name="next-steps"></a><span data-ttu-id="72604-249">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="72604-249">Next steps</span></span>
<span data-ttu-id="72604-250">Per ulteriori opzioni di archiviazione dei dati in Azure, consultare altre guide alle funzionalità.</span><span class="sxs-lookup"><span data-stu-id="72604-250">View more feature guides to learn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="72604-251">Introduzione all'Archiviazione BLOB di Azure e ai Servizi connessi di Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="72604-251">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](../storage/vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="72604-252">Introduzione all'archiviazione tabelle di Azure e ai Servizi connessi di Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="72604-252">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](vs-storage-aspnet-getting-started-tables.md)
