---
title: aaaGet avviato con l'archiviazione delle code di Azure e Visual Studio connesso servizi (ASP.NET) | Documenti Microsoft
description: "La modalità di avvio utilizzando l'archiviazione delle code di Azure in un progetto ASP.NET in Visual Studio dopo la connessione di account di archiviazione tooa con Visual Studio connesso Services tooget"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 94ca3413-5497-433f-abbe-836f83a9de72
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/23/2016
ms.author: tarcher
ms.openlocfilehash: a9d6ecb1e8d61d75f59658d0ea3fa63d26fd7354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-queue-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="2a9f2-103">Introduzione all'archiviazione code di Azure e ai servizi connessi di Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="2a9f2-103">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="2a9f2-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="2a9f2-104">Overview</span></span>

<span data-ttu-id="2a9f2-105">L'archivio code di Azure fornisce la messaggistica cloud tra i componenti dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-105">Azure queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="2a9f2-106">Durante la progettazione di applicazioni scalabili, i componenti dell'applicazione vengono spesso separati, per poter essere scalati in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-106">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="2a9f2-107">L'archiviazione delle code recapita la messaggistica asincrona per la comunicazione tra i componenti dell'applicazione, se sono in esecuzione nel cloud hello, sul desktop di hello, in un server locale o in un dispositivo mobile.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-107">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in hello cloud, on hello desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="2a9f2-108">Archiviazione code supporta anche la gestione di attività asincrone e la creazione di flussi di lavoro dei processi.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-108">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

<span data-ttu-id="2a9f2-109">Questa esercitazione viene illustrato come toowrite ASP.NET codice in alcuni scenari comuni con le entità di archiviazione delle code di Azure.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-109">This tutorial shows how toowrite ASP.NET code for some common scenarios using Azure queue storage entities.</span></span> <span data-ttu-id="2a9f2-110">Tali scenari includono attività comuni, ad esempio la creazione di una coda di Azure e l'aggiunta, modifica, lettura e rimozione dei messaggi in coda.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-110">These scenarios include common tasks such as creating an Azure queue, and adding, modifying, reading, and removing queue messages.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="2a9f2-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2a9f2-111">Prerequisites</span></span>

* [<span data-ttu-id="2a9f2-112">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2a9f2-112">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="2a9f2-113">Account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="2a9f2-113">Azure storage account</span></span>](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="2a9f2-114">Creare un controller MVC</span><span class="sxs-lookup"><span data-stu-id="2a9f2-114">Create an MVC controller</span></span> 

1. <span data-ttu-id="2a9f2-115">In hello **Esplora soluzioni**, fare doppio clic su **controller**, selezionare il menu di scelta rapida hello **Aggiungi -> Controller**.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-115">In hello **Solution Explorer**, right-click **Controllers**, and, from hello context menu, select **Add->Controller**.</span></span>

    ![Aggiungere un tooan controller app ASP.NET MVC](./media/vs-storage-aspnet-getting-started-queues/add-controller-menu.png)

1. <span data-ttu-id="2a9f2-117">In hello **aggiungere lo scaffolding** finestra di dialogo Seleziona **Controller MVC 5 - vuoto**e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-117">On hello **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Specificare il tipo di controller MVC](./media/vs-storage-aspnet-getting-started-queues/add-controller.png)

1. <span data-ttu-id="2a9f2-119">In hello **Aggiungi Controller** finestra di dialogo, nome del controller hello *QueuesController*e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-119">On hello **Add Controller** dialog, name hello controller *QueuesController*, and select **Add**.</span></span>

    ![Controller MVC hello di nome](./media/vs-storage-aspnet-getting-started-queues/add-controller-name.png)

1. <span data-ttu-id="2a9f2-121">Aggiungere il seguente hello *utilizzando* toohello direttive `QueuesController.cs` file:</span><span class="sxs-lookup"><span data-stu-id="2a9f2-121">Add hello following *using* directives toohello `QueuesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Queue;
    ```
## <a name="create-a-queue"></a><span data-ttu-id="2a9f2-122">Creare una coda</span><span class="sxs-lookup"><span data-stu-id="2a9f2-122">Create a queue</span></span>

<span data-ttu-id="2a9f2-123">Hello passaggi seguenti viene illustrato come toocreate una coda:</span><span class="sxs-lookup"><span data-stu-id="2a9f2-123">hello following steps illustrate how toocreate a queue:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="2a9f2-124">Questa sezione si presuppone di aver completato i passaggi di hello [configurare un ambiente di sviluppo hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="2a9f2-124">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="2a9f2-125">Aprire hello `QueuesController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-125">Open hello `QueuesController.cs` file.</span></span> 

1. <span data-ttu-id="2a9f2-126">Aggiungere un metodo denominato **CreateQueue** che restituisce un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-126">Add a method called **CreateQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="2a9f2-127">All'interno di hello **CreateQueue** (metodo), ottenere un **CloudStorageAccount** oggetto che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-127">Within hello **CreateQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="2a9f2-128">Esempio di codice seguente di hello utilizzare tooget hello archiviazione stringa e l'archiviazione account informazioni di connessione di configurazione del servizio Azure hello: (modifica  *&lt;storage-account-name >* toohello nome hello archiviazione di Azure account che si accede.)</span><span class="sxs-lookup"><span data-stu-id="2a9f2-128">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="2a9f2-129">Ottenere un oggetto **CloudQueueClient** che rappresenta un client del servizio di accodamento.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-129">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```
1. <span data-ttu-id="2a9f2-130">Ottenere un **CloudQueue** oggetto che rappresenta un nome di riferimento toohello coda desiderata.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-130">Get a **CloudQueue** object that represents a reference toohello desired queue name.</span></span> <span data-ttu-id="2a9f2-131">Hello **CloudQueueClient.GetQueueReference** metodo non apporta una richiesta per l'archiviazione delle code.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-131">hello **CloudQueueClient.GetQueueReference** method does not make a request against queue storage.</span></span> <span data-ttu-id="2a9f2-132">coda hello esista o meno, viene restituito il riferimento di Hello.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-132">hello reference is returned whether or not hello queue exists.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="2a9f2-133">Chiamare hello **CloudQueue.CreateIfNotExists** coda di hello toocreate metodo se non esiste ancora.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-133">Call hello **CloudQueue.CreateIfNotExists** method toocreate hello queue if it does not yet exist.</span></span> <span data-ttu-id="2a9f2-134">Hello **CloudQueue.CreateIfNotExists** restituisce **true** coda hello non esiste, se è stata creata correttamente.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-134">hello **CloudQueue.CreateIfNotExists** method returns **true** if hello queue does not exist, and is successfully created.</span></span> <span data-ttu-id="2a9f2-135">In caso contrario, viene restituito **false**.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-135">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = queue.CreateIfNotExists();
    ```

1. <span data-ttu-id="2a9f2-136">Hello aggiornamento **ViewBag** con nome hello della coda di hello.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-136">Update hello **ViewBag** with hello name of hello queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```

1. <span data-ttu-id="2a9f2-137">In hello **Esplora**, espandere hello **viste** cartella, fare doppio clic su **code**e quindi scegliere il menu di scelta rapida hello **Aggiungi -> Vista**.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-137">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="2a9f2-138">In hello **Aggiungi visualizzazione** finestra di dialogo immettere **CreateQueue** per nome della visualizzazione hello e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-138">On hello **Add View** dialog, enter **CreateQueue** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="2a9f2-139">Aprire `CreateQueue.cshtml`e modificarlo in modo che risulti simile hello frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="2a9f2-139">Open `CreateQueue.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Queue";
    }
    
    <h2>Create Queue results</h2>

    Creation of @ViewBag.QueueName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="2a9f2-140">In hello **Esplora**, espandere hello **viste -> Shared** cartella e aprire `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-140">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="2a9f2-141">Dopo aver hello ultimo **HTML. ActionLink**, aggiungere il seguente hello **HTML. ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="2a9f2-141">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create queue", "CreateQueue", "Queues")</li>
    ```

1. <span data-ttu-id="2a9f2-142">Eseguire un'applicazione hello e selezionare **Create queue** toosee risultati simile toohello cattura di schermata seguente:</span><span class="sxs-lookup"><span data-stu-id="2a9f2-142">Run hello application, and select **Create queue** toosee results similar toohello following screen shot:</span></span>
  
    ![Crea coda](./media/vs-storage-aspnet-getting-started-queues/create-queue-results.png)

    <span data-ttu-id="2a9f2-144">Come accennato in precedenza, hello **CloudQueue.CreateIfNotExists** restituisce **true** solo quando la coda hello non esiste e viene creata.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-144">As mentioned previously, hello **CloudQueue.CreateIfNotExists** method returns **true** only when hello queue doesn't exist and is created.</span></span> <span data-ttu-id="2a9f2-145">Pertanto, se si esegue l'applicazione hello quando hello coda esiste, il metodo di hello restituisce **false**.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-145">Therefore, if you run hello app when hello queue exists, hello method returns **false**.</span></span> <span data-ttu-id="2a9f2-146">app hello toorun più volte, è necessario eliminare hello coda prima di eseguire nuovamente l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-146">toorun hello app multiple times, you must delete hello queue before running hello app again.</span></span> <span data-ttu-id="2a9f2-147">L'eliminazione della coda di hello può essere eseguita tramite hello **CloudQueue.Delete** metodo.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-147">Deleting hello queue can be done via hello **CloudQueue.Delete** method.</span></span> <span data-ttu-id="2a9f2-148">È anche possibile eliminare coda hello utilizzando hello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) o hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="2a9f2-148">You can also delete hello queue using hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="2a9f2-149">Aggiungere una coda di messaggi tooa</span><span class="sxs-lookup"><span data-stu-id="2a9f2-149">Add a message tooa queue</span></span>

<span data-ttu-id="2a9f2-150">Dopo aver [creazione di una coda](#create-a-queue), è possibile aggiungere messaggi toothat coda.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-150">Once you've [created a queue](#create-a-queue), you can add messages toothat queue.</span></span> <span data-ttu-id="2a9f2-151">In questa sezione viene illustrata l'aggiunta di una coda di messaggi tooa *test coda*.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-151">This section walks you through adding a message tooa queue *test-queue*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="2a9f2-152">Questa sezione si presuppone di aver completato i passaggi di hello [configurare un ambiente di sviluppo hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="2a9f2-152">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="2a9f2-153">Aprire hello `QueuesController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-153">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="2a9f2-154">Aggiungere un metodo denominato **AddMessage** che restituisce un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-154">Add a method called **AddMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="2a9f2-155">All'interno di hello **AddMessage** (metodo), ottenere un **CloudStorageAccount** oggetto che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-155">Within hello **AddMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="2a9f2-156">Esempio di codice seguente di hello utilizzare tooget hello archiviazione stringa e l'archiviazione account informazioni di connessione di configurazione del servizio Azure hello: (modifica  *&lt;storage-account-name >* toohello nome hello archiviazione di Azure account che si accede.)</span><span class="sxs-lookup"><span data-stu-id="2a9f2-156">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="2a9f2-157">Ottenere un oggetto **CloudQueueClient** che rappresenta un client del servizio di accodamento.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-157">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="2a9f2-158">Ottenere un **CloudQueueContainer** oggetto che rappresenta una coda di toohello di riferimento.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-158">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="2a9f2-159">Creare hello **CloudQueueMessage** oggetto che rappresenta il messaggio hello da tooadd toohello coda.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-159">Create hello **CloudQueueMessage** object representing hello message you want tooadd toohello queue.</span></span> <span data-ttu-id="2a9f2-160">È possibile creare un oggetto **CloudQueueMessage** da una stringa in formato UTF-8 o da una matrice di byte.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-160">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

    ```csharp
    CloudQueueMessage message = new CloudQueueMessage("Hello, Azure Queue Storage");
    ```

1. <span data-ttu-id="2a9f2-161">Chiamare hello **CloudQueue.AddMessage** coda di messaggi toohello hello tooadd metodo.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-161">Call hello **CloudQueue.AddMessage** method tooadd hello messaged toohello queue.</span></span>

    ```csharp
    queue.AddMessage(message);
    ```

1. <span data-ttu-id="2a9f2-162">Creare e impostare un paio di **ViewBag** le proprietà per la visualizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-162">Create and set a couple of **ViewBag** properties for display in hello view.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```

1. <span data-ttu-id="2a9f2-163">In hello **Esplora**, espandere hello **viste** cartella, fare doppio clic su **code**e quindi scegliere il menu di scelta rapida hello **Aggiungi -> Vista**.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-163">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="2a9f2-164">In hello **Aggiungi visualizzazione** finestra di dialogo immettere **AddMessage** per nome della visualizzazione hello e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-164">On hello **Add View** dialog, enter **AddMessage** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="2a9f2-165">Aprire `AddMessage.cshtml`e modificarlo in modo che risulti simile hello frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="2a9f2-165">Open `AddMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add Message";
    }
    
    <h2>Add Message results</h2>
    
    hello message '@ViewBag.Message' was added toohello queue '@ViewBag.QueueName'.
    ```

1. <span data-ttu-id="2a9f2-166">In hello **Esplora**, espandere hello **viste -> Shared** cartella e aprire `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-166">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="2a9f2-167">Dopo aver hello ultimo **HTML. ActionLink**, aggiungere il seguente hello **HTML. ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="2a9f2-167">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add message", "AddMessage", "Queues")</li>
    ```

1. <span data-ttu-id="2a9f2-168">Eseguire un'applicazione hello e selezionare **Aggiungi messaggio** toosee risultati simile toohello cattura di schermata seguente:</span><span class="sxs-lookup"><span data-stu-id="2a9f2-168">Run hello application, and select **Add message** toosee results similar toohello following screen shot:</span></span>
  
    ![Aggiungi messaggio](./media/vs-storage-aspnet-getting-started-queues/add-message-results.png)

<span data-ttu-id="2a9f2-170">Hello due sezioni - [leggere un messaggio da una coda senza rimuoverlo](#read-a-message-from-a-queue-without-removing-it) e [lettura e rimuovere un messaggio da una coda](#read-and-remove-a-message-from-a-queue) -illustrare la modalità tooread dei messaggi da una coda.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-170">hello two sections - [Read a message from a queue without removing it](#read-a-message-from-a-queue-without-removing-it) and [Read and remove a message from a queue](#read-and-remove-a-message-from-a-queue) - illustrate how tooread messages from a queue.</span></span>  

## <a name="read-a-message-from-a-queue-without-removing-it"></a><span data-ttu-id="2a9f2-171">Leggere un messaggio da una coda senza rimuoverlo</span><span class="sxs-lookup"><span data-stu-id="2a9f2-171">Read a message from a queue without removing it</span></span>

<span data-ttu-id="2a9f2-172">In questa sezione viene illustrato come toopeek un messaggio in coda (messaggio senza rimuoverlo prima di hello lettura).</span><span class="sxs-lookup"><span data-stu-id="2a9f2-172">This section illustrates how toopeek at a queued message (read hello first message without removing it).</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="2a9f2-173">Questa sezione si presuppone di aver completato i passaggi di hello [configurare un ambiente di sviluppo hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="2a9f2-173">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="2a9f2-174">Aprire hello `QueuesController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-174">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="2a9f2-175">Aggiungere un metodo denominato **PeekMessage** che restituisce un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-175">Add a method called **PeekMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult PeekMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="2a9f2-176">All'interno di hello **PeekMessage** (metodo), ottenere un **CloudStorageAccount** oggetto che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-176">Within hello **PeekMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="2a9f2-177">Esempio di codice seguente di hello utilizzare tooget hello archiviazione stringa e l'archiviazione account informazioni di connessione di configurazione del servizio Azure hello: (modifica  *&lt;storage-account-name >* toohello nome hello archiviazione di Azure account che si accede.)</span><span class="sxs-lookup"><span data-stu-id="2a9f2-177">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="2a9f2-178">Ottenere un oggetto **CloudQueueClient** che rappresenta un client del servizio di accodamento.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-178">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="2a9f2-179">Ottenere un **CloudQueueContainer** oggetto che rappresenta una coda di toohello di riferimento.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-179">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="2a9f2-180">Chiamare hello **CloudQueue.PeekMessage** metodo tooread hello primo messaggio hello coda senza rimuoverlo dalla coda hello.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-180">Call hello **CloudQueue.PeekMessage** method tooread hello first message in hello queue without removing it from hello queue.</span></span> 

    ```csharp
    CloudQueueMessage message = queue.PeekMessage();
    ```

1. <span data-ttu-id="2a9f2-181">Hello aggiornamento **ViewBag** con due valori: nome della coda hello e un messaggio hello che è stato letto.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-181">Update hello **ViewBag** with two values: hello queue name and hello message that was read.</span></span> <span data-ttu-id="2a9f2-182">Hello **CloudQueueMessage** oggetto espone due proprietà per ottenere il valore dell'oggetto hello: **CloudQueueMessage.AsBytes** e **CloudQueueMessage.AsString**.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-182">hello **CloudQueueMessage** object exposes two properties for getting hello object's value: **CloudQueueMessage.AsBytes** and **CloudQueueMessage.AsString**.</span></span> <span data-ttu-id="2a9f2-183">**AsString** (usata in questo esempio) restituisce una stringa, mentre **AsBytes** restituisce una matrice di byte.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-183">**AsString** (used in this example) returns a string, while **AsBytes** returns a byte array.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name; 
    ViewBag.Message = (message != null ? message.AsString : "");
    ```

1. <span data-ttu-id="2a9f2-184">In hello **Esplora**, espandere hello **viste** cartella, fare doppio clic su **code**e quindi scegliere il menu di scelta rapida hello **Aggiungi -> Vista**.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-184">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="2a9f2-185">In hello **Aggiungi visualizzazione** finestra di dialogo immettere **PeekMessage** per nome della visualizzazione hello e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-185">On hello **Add View** dialog, enter **PeekMessage** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="2a9f2-186">Aprire `PeekMessage.cshtml`e modificarlo in modo che risulti simile hello frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="2a9f2-186">Open `PeekMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

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

1. <span data-ttu-id="2a9f2-187">In hello **Esplora**, espandere hello **viste -> Shared** cartella e aprire `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-187">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="2a9f2-188">Dopo aver hello ultimo **HTML. ActionLink**, aggiungere il seguente hello **HTML. ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="2a9f2-188">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Peek message", "PeekMessage", "Queues")</li>
    ```

1. <span data-ttu-id="2a9f2-189">Eseguire un'applicazione hello e selezionare **messaggio Peek** toosee risultati simile toohello cattura di schermata seguente:</span><span class="sxs-lookup"><span data-stu-id="2a9f2-189">Run hello application, and select **Peek message** toosee results similar toohello following screen shot:</span></span>
  
    ![Visualizza il messaggio](./media/vs-storage-aspnet-getting-started-queues/peek-message-results.png)

## <a name="read-and-remove-a-message-from-a-queue"></a><span data-ttu-id="2a9f2-191">Leggere e rimuovere un messaggio da una coda</span><span class="sxs-lookup"><span data-stu-id="2a9f2-191">Read and remove a message from a queue</span></span>

<span data-ttu-id="2a9f2-192">In questa sezione viene illustrato come tooread e rimuovere un messaggio da una coda.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-192">In this section, you learn how tooread and remove a message from a queue.</span></span>   

> [!NOTE]
> 
> <span data-ttu-id="2a9f2-193">Questa sezione si presuppone di aver completato i passaggi di hello [configurare un ambiente di sviluppo hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="2a9f2-193">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="2a9f2-194">Aprire hello `QueuesController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-194">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="2a9f2-195">Aggiungere un metodo denominato **ReadMessage** che restituisce un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-195">Add a method called **ReadMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ReadMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="2a9f2-196">All'interno di hello **ReadMessage** (metodo), ottenere un **CloudStorageAccount** oggetto che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-196">Within hello **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="2a9f2-197">Esempio di codice seguente di hello utilizzare tooget hello archiviazione stringa e l'archiviazione account informazioni di connessione di configurazione del servizio Azure hello: (modifica  *&lt;storage-account-name >* toohello nome hello archiviazione di Azure account che si accede.)</span><span class="sxs-lookup"><span data-stu-id="2a9f2-197">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="2a9f2-198">Ottenere un oggetto **CloudQueueClient** che rappresenta un client del servizio di accodamento.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-198">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="2a9f2-199">Ottenere un **CloudQueueContainer** oggetto che rappresenta una coda di toohello di riferimento.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-199">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="2a9f2-200">Chiamare hello **CloudQueue.GetMessage** metodo tooread hello primo messaggio nella coda di hello.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-200">Call hello **CloudQueue.GetMessage** method tooread hello first message in hello queue.</span></span> <span data-ttu-id="2a9f2-201">Hello **CloudQueue.GetMessage** metodo rende hello altro codice la lettura dei messaggi in modo che nessun altro codice è possibile modificare o eliminare il messaggio hello durante l'elaborazione di messaggi invisibili per tooany 30 secondi (per impostazione predefinita).</span><span class="sxs-lookup"><span data-stu-id="2a9f2-201">hello **CloudQueue.GetMessage** method makes hello message invisible for 30 seconds (by default) tooany other code reading messages so that no other code can modify or delete hello message while your processing it.</span></span> <span data-ttu-id="2a9f2-202">quantità di hello toochange di messaggio hello ora non è visibile, modificare hello **visibilityTimeout** parametro passato toohello **CloudQueue.GetMessage** metodo.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-202">toochange hello amount of time hello message is invisible, modify hello **visibilityTimeout** parameter being passed toohello **CloudQueue.GetMessage** method.</span></span>

    ```csharp
    // This message will be invisible tooother code for 30 seconds.
    CloudQueueMessage message = queue.GetMessage();     
    ```

1. <span data-ttu-id="2a9f2-203">Chiamare hello **CloudQueueMessage.Delete** messaggio dalla coda hello hello toodelete del metodo.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-203">Call hello **CloudQueueMessage.Delete** method toodelete hello message from hello queue.</span></span>

    ```csharp
    queue.DeleteMessage(message);
    ```

1. <span data-ttu-id="2a9f2-204">Hello aggiornamento **ViewBag** con hello messaggio eliminato e nome della coda di hello hello.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-204">Update hello **ViewBag** with hello message deleted, and hello name of hello queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```
 
1. <span data-ttu-id="2a9f2-205">In hello **Esplora**, espandere hello **viste** cartella, fare doppio clic su **code**e quindi scegliere il menu di scelta rapida hello **Aggiungi -> Vista**.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-205">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="2a9f2-206">In hello **Aggiungi visualizzazione** finestra di dialogo immettere **ReadMessage** per nome della visualizzazione hello e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-206">On hello **Add View** dialog, enter **ReadMessage** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="2a9f2-207">Aprire `ReadMessage.cshtml`e modificarlo in modo che risulti simile hello frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="2a9f2-207">Open `ReadMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

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

1. <span data-ttu-id="2a9f2-208">In hello **Esplora**, espandere hello **viste -> Shared** cartella e aprire `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-208">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="2a9f2-209">Dopo aver hello ultimo **HTML. ActionLink**, aggiungere il seguente hello **HTML. ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="2a9f2-209">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Read/Delete message", "ReadMessage", "Queues")</li>
    ```

1. <span data-ttu-id="2a9f2-210">Eseguire un'applicazione hello e selezionare **messaggio di lettura/eliminazione** toosee risultati simile toohello cattura di schermata seguente:</span><span class="sxs-lookup"><span data-stu-id="2a9f2-210">Run hello application, and select **Read/Delete message** toosee results similar toohello following screen shot:</span></span>
  
    ![Read/Delete message (Leggi/Elimina messaggio)](./media/vs-storage-aspnet-getting-started-queues/read-message-results.png)

## <a name="get-hello-queue-length"></a><span data-ttu-id="2a9f2-212">Ottiene la lunghezza della coda hello</span><span class="sxs-lookup"><span data-stu-id="2a9f2-212">Get hello queue length</span></span>

<span data-ttu-id="2a9f2-213">In questa sezione viene illustrato come tooget hello lunghezza della coda (numero di messaggi).</span><span class="sxs-lookup"><span data-stu-id="2a9f2-213">This section illustrates how tooget hello queue length (number of messages).</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="2a9f2-214">Questa sezione si presuppone di aver completato i passaggi di hello [configurare un ambiente di sviluppo hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="2a9f2-214">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="2a9f2-215">Aprire hello `QueuesController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-215">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="2a9f2-216">Aggiungere un metodo denominato **GetQueueLength** che restituisce un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-216">Add a method called **GetQueueLength** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetQueueLength()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="2a9f2-217">All'interno di hello **ReadMessage** (metodo), ottenere un **CloudStorageAccount** oggetto che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-217">Within hello **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="2a9f2-218">Esempio di codice seguente di hello utilizzare tooget hello archiviazione stringa e l'archiviazione account informazioni di connessione di configurazione del servizio Azure hello: (modifica  *&lt;storage-account-name >* toohello nome hello archiviazione di Azure account che si accede.)</span><span class="sxs-lookup"><span data-stu-id="2a9f2-218">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="2a9f2-219">Ottenere un oggetto **CloudQueueClient** che rappresenta un client del servizio di accodamento.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-219">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="2a9f2-220">Ottenere un **CloudQueueContainer** oggetto che rappresenta una coda di toohello di riferimento.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-220">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="2a9f2-221">Chiamare hello **CloudQueue.FetchAttributes** attributi della coda di metodo tooretrieve hello (inclusa la relativa lunghezza).</span><span class="sxs-lookup"><span data-stu-id="2a9f2-221">Call hello **CloudQueue.FetchAttributes** method tooretrieve hello queue's attributes (including its length).</span></span> 

    ```csharp
    queue.FetchAttributes();
    ```

6. <span data-ttu-id="2a9f2-222">Hello accesso **CloudQueue.ApproximateMessageCount** lunghezza della coda di proprietà tooget hello.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-222">Access hello **CloudQueue.ApproximateMessageCount** property tooget hello queue's length.</span></span>
 
    ```csharp
    int? nMessages = queue.ApproximateMessageCount;
    ```

1. <span data-ttu-id="2a9f2-223">Hello aggiornamento **ViewBag** con nome hello della coda di hello e la relativa lunghezza.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-223">Update hello **ViewBag** with hello name of hello queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Length = nMessages;
    ```
 
1. <span data-ttu-id="2a9f2-224">In hello **Esplora**, espandere hello **viste** cartella, fare doppio clic su **code**e quindi scegliere il menu di scelta rapida hello **Aggiungi -> Vista**.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-224">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="2a9f2-225">In hello **Aggiungi visualizzazione** finestra di dialogo immettere **GetQueueLength** per nome della visualizzazione hello e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-225">On hello **Add View** dialog, enter **GetQueueLength** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="2a9f2-226">Aprire `GetQueueLengthMessage.cshtml`e modificarlo in modo che risulti simile hello frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="2a9f2-226">Open `GetQueueLengthMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "GetQueueLength";
    }
    
    <h2>Get Queue Length results</h2>
    
    hello queue '@ViewBag.QueueName' has a length of (number of messages): @ViewBag.Length
    ```

1. <span data-ttu-id="2a9f2-227">In hello **Esplora**, espandere hello **viste -> Shared** cartella e aprire `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-227">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="2a9f2-228">Dopo aver hello ultimo **HTML. ActionLink**, aggiungere il seguente hello **HTML. ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="2a9f2-228">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get queue length", "GetQueueLength", "Queues")</li>
    ```

1. <span data-ttu-id="2a9f2-229">Eseguire un'applicazione hello e selezionare **ottenere lunghezza coda** toosee risultati simile toohello cattura di schermata seguente:</span><span class="sxs-lookup"><span data-stu-id="2a9f2-229">Run hello application, and select **Get queue length** toosee results similar toohello following screen shot:</span></span>
  
    ![Recuperare la lunghezza della coda](./media/vs-storage-aspnet-getting-started-queues/get-queue-length-results.png)


## <a name="delete-a-queue"></a><span data-ttu-id="2a9f2-231">Eliminare una coda</span><span class="sxs-lookup"><span data-stu-id="2a9f2-231">Delete a queue</span></span>
<span data-ttu-id="2a9f2-232">In questa sezione viene illustrato come toodelete una coda.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-232">This section illustrates how toodelete a queue.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="2a9f2-233">Questa sezione si presuppone di aver completato i passaggi di hello [configurare un ambiente di sviluppo hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="2a9f2-233">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="2a9f2-234">Aprire hello `QueuesController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-234">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="2a9f2-235">Aggiungere un metodo denominato **DeleteQueue** che restituisce un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-235">Add a method called **DeleteQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="2a9f2-236">All'interno di hello **DeleteQueue** (metodo), ottenere un **CloudStorageAccount** oggetto che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-236">Within hello **DeleteQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="2a9f2-237">Esempio di codice seguente di hello utilizzare tooget hello archiviazione stringa e l'archiviazione account informazioni di connessione di configurazione del servizio Azure hello: (modifica  *&lt;storage-account-name >* toohello nome hello archiviazione di Azure account che si accede.)</span><span class="sxs-lookup"><span data-stu-id="2a9f2-237">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="2a9f2-238">Ottenere un oggetto **CloudQueueClient** che rappresenta un client del servizio di accodamento.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-238">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="2a9f2-239">Ottenere un **CloudQueueContainer** oggetto che rappresenta una coda di toohello di riferimento.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-239">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="2a9f2-240">Chiamare hello **CloudQueue.Delete** coda di hello toodelete metodo rappresentata da hello **CloudQueue** oggetto.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-240">Call hello **CloudQueue.Delete** method toodelete hello queue represented by hello **CloudQueue** object.</span></span>

    ```csharp
    queue.Delete();
    ```

1. <span data-ttu-id="2a9f2-241">Hello aggiornamento **ViewBag** con nome hello della coda di hello e la relativa lunghezza.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-241">Update hello **ViewBag** with hello name of hello queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```
 
1. <span data-ttu-id="2a9f2-242">In hello **Esplora**, espandere hello **viste** cartella, fare doppio clic su **code**e quindi scegliere il menu di scelta rapida hello **Aggiungi -> Vista**.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-242">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="2a9f2-243">In hello **Aggiungi visualizzazione** finestra di dialogo immettere **DeleteQueue** per nome della visualizzazione hello e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-243">On hello **Add View** dialog, enter **DeleteQueue** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="2a9f2-244">Aprire `DeleteQueue.cshtml`e modificarlo in modo che risulti simile hello frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="2a9f2-244">Open `DeleteQueue.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "DeleteQueue";
    }
    
    <h2>Delete Queue results</h2>
    
    @ViewBag.QueueName deleted.
    ```

1. <span data-ttu-id="2a9f2-245">In hello **Esplora**, espandere hello **viste -> Shared** cartella e aprire `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-245">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="2a9f2-246">Dopo aver hello ultimo **HTML. ActionLink**, aggiungere il seguente hello **HTML. ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="2a9f2-246">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete queue", "DeleteQueue", "Queues")</li>
    ```

1. <span data-ttu-id="2a9f2-247">Eseguire un'applicazione hello e selezionare **ottenere lunghezza coda** toosee risultati simile toohello cattura di schermata seguente:</span><span class="sxs-lookup"><span data-stu-id="2a9f2-247">Run hello application, and select **Get queue length** toosee results similar toohello following screen shot:</span></span>
  
    ![Elimina coda](./media/vs-storage-aspnet-getting-started-queues/delete-queue-results.png)

## <a name="next-steps"></a><span data-ttu-id="2a9f2-249">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2a9f2-249">Next steps</span></span>
<span data-ttu-id="2a9f2-250">Consente di visualizzare altre toolearn di guide di funzionalità sulle opzioni aggiuntive per l'archiviazione dei dati in Azure.</span><span class="sxs-lookup"><span data-stu-id="2a9f2-250">View more feature guides toolearn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="2a9f2-251">Introduzione all'Archiviazione BLOB di Azure e ai Servizi connessi di Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="2a9f2-251">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="2a9f2-252">Introduzione all'archiviazione tabelle di Azure e ai Servizi connessi di Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="2a9f2-252">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-tables.md)
