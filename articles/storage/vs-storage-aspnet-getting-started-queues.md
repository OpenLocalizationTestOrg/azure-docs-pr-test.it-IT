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
# <a name="get-started-with-azure-queue-storage-and-visual-studio-connected-services-aspnet"></a>Introduzione all'archiviazione code di Azure e ai servizi connessi di Visual Studio (ASP.NET)
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Panoramica

L'archivio code di Azure fornisce la messaggistica cloud tra i componenti dell'applicazione. Durante la progettazione di applicazioni scalabili, i componenti dell'applicazione vengono spesso separati, per poter essere scalati in modo indipendente. L'archiviazione delle code recapita la messaggistica asincrona per la comunicazione tra i componenti dell'applicazione, se sono in esecuzione nel cloud hello, sul desktop di hello, in un server locale o in un dispositivo mobile. Archiviazione code supporta anche la gestione di attività asincrone e la creazione di flussi di lavoro dei processi.

Questa esercitazione viene illustrato come toowrite ASP.NET codice in alcuni scenari comuni con le entità di archiviazione delle code di Azure. Tali scenari includono attività comuni, ad esempio la creazione di una coda di Azure e l'aggiunta, modifica, lettura e rimozione dei messaggi in coda.

##<a name="prerequisites"></a>Prerequisiti

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Account di archiviazione di Azure](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a>Creare un controller MVC 

1. In hello **Esplora soluzioni**, fare doppio clic su **controller**, selezionare il menu di scelta rapida hello **Aggiungi -> Controller**.

    ![Aggiungere un tooan controller app ASP.NET MVC](./media/vs-storage-aspnet-getting-started-queues/add-controller-menu.png)

1. In hello **aggiungere lo scaffolding** finestra di dialogo Seleziona **Controller MVC 5 - vuoto**e selezionare **Aggiungi**.

    ![Specificare il tipo di controller MVC](./media/vs-storage-aspnet-getting-started-queues/add-controller.png)

1. In hello **Aggiungi Controller** finestra di dialogo, nome del controller hello *QueuesController*e selezionare **Aggiungi**.

    ![Controller MVC hello di nome](./media/vs-storage-aspnet-getting-started-queues/add-controller-name.png)

1. Aggiungere il seguente hello *utilizzando* toohello direttive `QueuesController.cs` file:

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Queue;
    ```
## <a name="create-a-queue"></a>Creare una coda

Hello passaggi seguenti viene illustrato come toocreate una coda:

> [!NOTE]
> 
> Questa sezione si presuppone di aver completato i passaggi di hello [configurare un ambiente di sviluppo hello](#set-up-the-development-environment). 

1. Aprire hello `QueuesController.cs` file. 

1. Aggiungere un metodo denominato **CreateQueue** che restituisce un **ActionResult**.

    ```csharp
    public ActionResult CreateQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. All'interno di hello **CreateQueue** (metodo), ottenere un **CloudStorageAccount** oggetto che rappresenta le informazioni sull'account di archiviazione. Esempio di codice seguente di hello utilizzare tooget hello archiviazione stringa e l'archiviazione account informazioni di connessione di configurazione del servizio Azure hello: (modifica  *&lt;storage-account-name >* toohello nome hello archiviazione di Azure account che si accede.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Ottenere un oggetto **CloudQueueClient** che rappresenta un client del servizio di accodamento.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```
1. Ottenere un **CloudQueue** oggetto che rappresenta un nome di riferimento toohello coda desiderata. Hello **CloudQueueClient.GetQueueReference** metodo non apporta una richiesta per l'archiviazione delle code. coda hello esista o meno, viene restituito il riferimento di Hello. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Chiamare hello **CloudQueue.CreateIfNotExists** coda di hello toocreate metodo se non esiste ancora. Hello **CloudQueue.CreateIfNotExists** restituisce **true** coda hello non esiste, se è stata creata correttamente. In caso contrario, viene restituito **false**.    

    ```csharp
    ViewBag.Success = queue.CreateIfNotExists();
    ```

1. Hello aggiornamento **ViewBag** con nome hello della coda di hello.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```

1. In hello **Esplora**, espandere hello **viste** cartella, fare doppio clic su **code**e quindi scegliere il menu di scelta rapida hello **Aggiungi -> Vista**.

1. In hello **Aggiungi visualizzazione** finestra di dialogo immettere **CreateQueue** per nome della visualizzazione hello e selezionare **Aggiungi**.

1. Aprire `CreateQueue.cshtml`e modificarlo in modo che risulti simile hello frammento di codice seguente:

    ```csharp
    @{
        ViewBag.Title = "Create Queue";
    }
    
    <h2>Create Queue results</h2>

    Creation of @ViewBag.QueueName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. In hello **Esplora**, espandere hello **viste -> Shared** cartella e aprire `_Layout.cshtml`.

1. Dopo aver hello ultimo **HTML. ActionLink**, aggiungere il seguente hello **HTML. ActionLink**:

    ```html
    <li>@Html.ActionLink("Create queue", "CreateQueue", "Queues")</li>
    ```

1. Eseguire un'applicazione hello e selezionare **Create queue** toosee risultati simile toohello cattura di schermata seguente:
  
    ![Crea coda](./media/vs-storage-aspnet-getting-started-queues/create-queue-results.png)

    Come accennato in precedenza, hello **CloudQueue.CreateIfNotExists** restituisce **true** solo quando la coda hello non esiste e viene creata. Pertanto, se si esegue l'applicazione hello quando hello coda esiste, il metodo di hello restituisce **false**. app hello toorun più volte, è necessario eliminare hello coda prima di eseguire nuovamente l'applicazione hello. L'eliminazione della coda di hello può essere eseguita tramite hello **CloudQueue.Delete** metodo. È anche possibile eliminare coda hello utilizzando hello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) o hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).  

## <a name="add-a-message-tooa-queue"></a>Aggiungere una coda di messaggi tooa

Dopo aver [creazione di una coda](#create-a-queue), è possibile aggiungere messaggi toothat coda. In questa sezione viene illustrata l'aggiunta di una coda di messaggi tooa *test coda*. 

> [!NOTE]
> 
> Questa sezione si presuppone di aver completato i passaggi di hello [configurare un ambiente di sviluppo hello](#set-up-the-development-environment). 

1. Aprire hello `QueuesController.cs` file.

1. Aggiungere un metodo denominato **AddMessage** che restituisce un **ActionResult**.

    ```csharp
    public ActionResult AddMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. All'interno di hello **AddMessage** (metodo), ottenere un **CloudStorageAccount** oggetto che rappresenta le informazioni sull'account di archiviazione. Esempio di codice seguente di hello utilizzare tooget hello archiviazione stringa e l'archiviazione account informazioni di connessione di configurazione del servizio Azure hello: (modifica  *&lt;storage-account-name >* toohello nome hello archiviazione di Azure account che si accede.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Ottenere un oggetto **CloudQueueClient** che rappresenta un client del servizio di accodamento.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Ottenere un **CloudQueueContainer** oggetto che rappresenta una coda di toohello di riferimento. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Creare hello **CloudQueueMessage** oggetto che rappresenta il messaggio hello da tooadd toohello coda. È possibile creare un oggetto **CloudQueueMessage** da una stringa in formato UTF-8 o da una matrice di byte.

    ```csharp
    CloudQueueMessage message = new CloudQueueMessage("Hello, Azure Queue Storage");
    ```

1. Chiamare hello **CloudQueue.AddMessage** coda di messaggi toohello hello tooadd metodo.

    ```csharp
    queue.AddMessage(message);
    ```

1. Creare e impostare un paio di **ViewBag** le proprietà per la visualizzazione hello.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```

1. In hello **Esplora**, espandere hello **viste** cartella, fare doppio clic su **code**e quindi scegliere il menu di scelta rapida hello **Aggiungi -> Vista**.

1. In hello **Aggiungi visualizzazione** finestra di dialogo immettere **AddMessage** per nome della visualizzazione hello e selezionare **Aggiungi**.

1. Aprire `AddMessage.cshtml`e modificarlo in modo che risulti simile hello frammento di codice seguente:

    ```csharp
    @{
        ViewBag.Title = "Add Message";
    }
    
    <h2>Add Message results</h2>
    
    hello message '@ViewBag.Message' was added toohello queue '@ViewBag.QueueName'.
    ```

1. In hello **Esplora**, espandere hello **viste -> Shared** cartella e aprire `_Layout.cshtml`.

1. Dopo aver hello ultimo **HTML. ActionLink**, aggiungere il seguente hello **HTML. ActionLink**:

    ```html
    <li>@Html.ActionLink("Add message", "AddMessage", "Queues")</li>
    ```

1. Eseguire un'applicazione hello e selezionare **Aggiungi messaggio** toosee risultati simile toohello cattura di schermata seguente:
  
    ![Aggiungi messaggio](./media/vs-storage-aspnet-getting-started-queues/add-message-results.png)

Hello due sezioni - [leggere un messaggio da una coda senza rimuoverlo](#read-a-message-from-a-queue-without-removing-it) e [lettura e rimuovere un messaggio da una coda](#read-and-remove-a-message-from-a-queue) -illustrare la modalità tooread dei messaggi da una coda.  

## <a name="read-a-message-from-a-queue-without-removing-it"></a>Leggere un messaggio da una coda senza rimuoverlo

In questa sezione viene illustrato come toopeek un messaggio in coda (messaggio senza rimuoverlo prima di hello lettura).  

> [!NOTE]
> 
> Questa sezione si presuppone di aver completato i passaggi di hello [configurare un ambiente di sviluppo hello](#set-up-the-development-environment). 

1. Aprire hello `QueuesController.cs` file.

1. Aggiungere un metodo denominato **PeekMessage** che restituisce un **ActionResult**.

    ```csharp
    public ActionResult PeekMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. All'interno di hello **PeekMessage** (metodo), ottenere un **CloudStorageAccount** oggetto che rappresenta le informazioni sull'account di archiviazione. Esempio di codice seguente di hello utilizzare tooget hello archiviazione stringa e l'archiviazione account informazioni di connessione di configurazione del servizio Azure hello: (modifica  *&lt;storage-account-name >* toohello nome hello archiviazione di Azure account che si accede.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Ottenere un oggetto **CloudQueueClient** che rappresenta un client del servizio di accodamento.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Ottenere un **CloudQueueContainer** oggetto che rappresenta una coda di toohello di riferimento. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Chiamare hello **CloudQueue.PeekMessage** metodo tooread hello primo messaggio hello coda senza rimuoverlo dalla coda hello. 

    ```csharp
    CloudQueueMessage message = queue.PeekMessage();
    ```

1. Hello aggiornamento **ViewBag** con due valori: nome della coda hello e un messaggio hello che è stato letto. Hello **CloudQueueMessage** oggetto espone due proprietà per ottenere il valore dell'oggetto hello: **CloudQueueMessage.AsBytes** e **CloudQueueMessage.AsString**. **AsString** (usata in questo esempio) restituisce una stringa, mentre **AsBytes** restituisce una matrice di byte.

    ```csharp
    ViewBag.QueueName = queue.Name; 
    ViewBag.Message = (message != null ? message.AsString : "");
    ```

1. In hello **Esplora**, espandere hello **viste** cartella, fare doppio clic su **code**e quindi scegliere il menu di scelta rapida hello **Aggiungi -> Vista**.

1. In hello **Aggiungi visualizzazione** finestra di dialogo immettere **PeekMessage** per nome della visualizzazione hello e selezionare **Aggiungi**.

1. Aprire `PeekMessage.cshtml`e modificarlo in modo che risulti simile hello frammento di codice seguente:

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

1. In hello **Esplora**, espandere hello **viste -> Shared** cartella e aprire `_Layout.cshtml`.

1. Dopo aver hello ultimo **HTML. ActionLink**, aggiungere il seguente hello **HTML. ActionLink**:

    ```html
    <li>@Html.ActionLink("Peek message", "PeekMessage", "Queues")</li>
    ```

1. Eseguire un'applicazione hello e selezionare **messaggio Peek** toosee risultati simile toohello cattura di schermata seguente:
  
    ![Visualizza il messaggio](./media/vs-storage-aspnet-getting-started-queues/peek-message-results.png)

## <a name="read-and-remove-a-message-from-a-queue"></a>Leggere e rimuovere un messaggio da una coda

In questa sezione viene illustrato come tooread e rimuovere un messaggio da una coda.   

> [!NOTE]
> 
> Questa sezione si presuppone di aver completato i passaggi di hello [configurare un ambiente di sviluppo hello](#set-up-the-development-environment). 

1. Aprire hello `QueuesController.cs` file.

1. Aggiungere un metodo denominato **ReadMessage** che restituisce un **ActionResult**.

    ```csharp
    public ActionResult ReadMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. All'interno di hello **ReadMessage** (metodo), ottenere un **CloudStorageAccount** oggetto che rappresenta le informazioni sull'account di archiviazione. Esempio di codice seguente di hello utilizzare tooget hello archiviazione stringa e l'archiviazione account informazioni di connessione di configurazione del servizio Azure hello: (modifica  *&lt;storage-account-name >* toohello nome hello archiviazione di Azure account che si accede.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Ottenere un oggetto **CloudQueueClient** che rappresenta un client del servizio di accodamento.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Ottenere un **CloudQueueContainer** oggetto che rappresenta una coda di toohello di riferimento. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Chiamare hello **CloudQueue.GetMessage** metodo tooread hello primo messaggio nella coda di hello. Hello **CloudQueue.GetMessage** metodo rende hello altro codice la lettura dei messaggi in modo che nessun altro codice è possibile modificare o eliminare il messaggio hello durante l'elaborazione di messaggi invisibili per tooany 30 secondi (per impostazione predefinita). quantità di hello toochange di messaggio hello ora non è visibile, modificare hello **visibilityTimeout** parametro passato toohello **CloudQueue.GetMessage** metodo.

    ```csharp
    // This message will be invisible tooother code for 30 seconds.
    CloudQueueMessage message = queue.GetMessage();     
    ```

1. Chiamare hello **CloudQueueMessage.Delete** messaggio dalla coda hello hello toodelete del metodo.

    ```csharp
    queue.DeleteMessage(message);
    ```

1. Hello aggiornamento **ViewBag** con hello messaggio eliminato e nome della coda di hello hello.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```
 
1. In hello **Esplora**, espandere hello **viste** cartella, fare doppio clic su **code**e quindi scegliere il menu di scelta rapida hello **Aggiungi -> Vista**.

1. In hello **Aggiungi visualizzazione** finestra di dialogo immettere **ReadMessage** per nome della visualizzazione hello e selezionare **Aggiungi**.

1. Aprire `ReadMessage.cshtml`e modificarlo in modo che risulti simile hello frammento di codice seguente:

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

1. In hello **Esplora**, espandere hello **viste -> Shared** cartella e aprire `_Layout.cshtml`.

1. Dopo aver hello ultimo **HTML. ActionLink**, aggiungere il seguente hello **HTML. ActionLink**:

    ```html
    <li>@Html.ActionLink("Read/Delete message", "ReadMessage", "Queues")</li>
    ```

1. Eseguire un'applicazione hello e selezionare **messaggio di lettura/eliminazione** toosee risultati simile toohello cattura di schermata seguente:
  
    ![Read/Delete message (Leggi/Elimina messaggio)](./media/vs-storage-aspnet-getting-started-queues/read-message-results.png)

## <a name="get-hello-queue-length"></a>Ottiene la lunghezza della coda hello

In questa sezione viene illustrato come tooget hello lunghezza della coda (numero di messaggi). 

> [!NOTE]
> 
> Questa sezione si presuppone di aver completato i passaggi di hello [configurare un ambiente di sviluppo hello](#set-up-the-development-environment). 

1. Aprire hello `QueuesController.cs` file.

1. Aggiungere un metodo denominato **GetQueueLength** che restituisce un **ActionResult**.

    ```csharp
    public ActionResult GetQueueLength()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. All'interno di hello **ReadMessage** (metodo), ottenere un **CloudStorageAccount** oggetto che rappresenta le informazioni sull'account di archiviazione. Esempio di codice seguente di hello utilizzare tooget hello archiviazione stringa e l'archiviazione account informazioni di connessione di configurazione del servizio Azure hello: (modifica  *&lt;storage-account-name >* toohello nome hello archiviazione di Azure account che si accede.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Ottenere un oggetto **CloudQueueClient** che rappresenta un client del servizio di accodamento.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Ottenere un **CloudQueueContainer** oggetto che rappresenta una coda di toohello di riferimento. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Chiamare hello **CloudQueue.FetchAttributes** attributi della coda di metodo tooretrieve hello (inclusa la relativa lunghezza). 

    ```csharp
    queue.FetchAttributes();
    ```

6. Hello accesso **CloudQueue.ApproximateMessageCount** lunghezza della coda di proprietà tooget hello.
 
    ```csharp
    int? nMessages = queue.ApproximateMessageCount;
    ```

1. Hello aggiornamento **ViewBag** con nome hello della coda di hello e la relativa lunghezza.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Length = nMessages;
    ```
 
1. In hello **Esplora**, espandere hello **viste** cartella, fare doppio clic su **code**e quindi scegliere il menu di scelta rapida hello **Aggiungi -> Vista**.

1. In hello **Aggiungi visualizzazione** finestra di dialogo immettere **GetQueueLength** per nome della visualizzazione hello e selezionare **Aggiungi**.

1. Aprire `GetQueueLengthMessage.cshtml`e modificarlo in modo che risulti simile hello frammento di codice seguente:

    ```csharp
    @{
        ViewBag.Title = "GetQueueLength";
    }
    
    <h2>Get Queue Length results</h2>
    
    hello queue '@ViewBag.QueueName' has a length of (number of messages): @ViewBag.Length
    ```

1. In hello **Esplora**, espandere hello **viste -> Shared** cartella e aprire `_Layout.cshtml`.

1. Dopo aver hello ultimo **HTML. ActionLink**, aggiungere il seguente hello **HTML. ActionLink**:

    ```html
    <li>@Html.ActionLink("Get queue length", "GetQueueLength", "Queues")</li>
    ```

1. Eseguire un'applicazione hello e selezionare **ottenere lunghezza coda** toosee risultati simile toohello cattura di schermata seguente:
  
    ![Recuperare la lunghezza della coda](./media/vs-storage-aspnet-getting-started-queues/get-queue-length-results.png)


## <a name="delete-a-queue"></a>Eliminare una coda
In questa sezione viene illustrato come toodelete una coda. 

> [!NOTE]
> 
> Questa sezione si presuppone di aver completato i passaggi di hello [configurare un ambiente di sviluppo hello](#set-up-the-development-environment). 

1. Aprire hello `QueuesController.cs` file.

1. Aggiungere un metodo denominato **DeleteQueue** che restituisce un **ActionResult**.

    ```csharp
    public ActionResult DeleteQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. All'interno di hello **DeleteQueue** (metodo), ottenere un **CloudStorageAccount** oggetto che rappresenta le informazioni sull'account di archiviazione. Esempio di codice seguente di hello utilizzare tooget hello archiviazione stringa e l'archiviazione account informazioni di connessione di configurazione del servizio Azure hello: (modifica  *&lt;storage-account-name >* toohello nome hello archiviazione di Azure account che si accede.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Ottenere un oggetto **CloudQueueClient** che rappresenta un client del servizio di accodamento.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Ottenere un **CloudQueueContainer** oggetto che rappresenta una coda di toohello di riferimento. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Chiamare hello **CloudQueue.Delete** coda di hello toodelete metodo rappresentata da hello **CloudQueue** oggetto.

    ```csharp
    queue.Delete();
    ```

1. Hello aggiornamento **ViewBag** con nome hello della coda di hello e la relativa lunghezza.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```
 
1. In hello **Esplora**, espandere hello **viste** cartella, fare doppio clic su **code**e quindi scegliere il menu di scelta rapida hello **Aggiungi -> Vista**.

1. In hello **Aggiungi visualizzazione** finestra di dialogo immettere **DeleteQueue** per nome della visualizzazione hello e selezionare **Aggiungi**.

1. Aprire `DeleteQueue.cshtml`e modificarlo in modo che risulti simile hello frammento di codice seguente:

    ```csharp
    @{
        ViewBag.Title = "DeleteQueue";
    }
    
    <h2>Delete Queue results</h2>
    
    @ViewBag.QueueName deleted.
    ```

1. In hello **Esplora**, espandere hello **viste -> Shared** cartella e aprire `_Layout.cshtml`.

1. Dopo aver hello ultimo **HTML. ActionLink**, aggiungere il seguente hello **HTML. ActionLink**:

    ```html
    <li>@Html.ActionLink("Delete queue", "DeleteQueue", "Queues")</li>
    ```

1. Eseguire un'applicazione hello e selezionare **ottenere lunghezza coda** toosee risultati simile toohello cattura di schermata seguente:
  
    ![Elimina coda](./media/vs-storage-aspnet-getting-started-queues/delete-queue-results.png)

## <a name="next-steps"></a>Passaggi successivi
Consente di visualizzare altre toolearn di guide di funzionalità sulle opzioni aggiuntive per l'archiviazione dei dati in Azure.

  * [Introduzione all'Archiviazione BLOB di Azure e ai Servizi connessi di Visual Studio (ASP.NET)](./vs-storage-aspnet-getting-started-blobs.md)
  * [Introduzione all'archiviazione tabelle di Azure e ai Servizi connessi di Visual Studio (ASP.NET)](./vs-storage-aspnet-getting-started-tables.md)
