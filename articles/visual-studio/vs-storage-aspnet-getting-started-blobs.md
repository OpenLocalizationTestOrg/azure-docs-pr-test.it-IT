---
title: aaaGet generali di archiviazione blob di Azure e Visual Studio connesso servizi (ASP.NET) | Documenti Microsoft
description: "La modalità di avvio tooget utilizzo dell'archiviazione blob di Azure in un progetto ASP.NET in Visual Studio dopo la connessione di account di archiviazione tooa utilizzando servizi connessi di Visual Studio"
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
ms.openlocfilehash: 7b3e160da5bb95967ca4650b124afb8e867c03d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet"></a>Introduzione all'Archiviazione BLOB di Azure e ai Servizi connessi di Visual Studio (ASP.NET)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Panoramica

Archiviazione blob di Azure è un servizio che archivia i dati non strutturati nel cloud hello come oggetti/BLOB. Archivio BLOB può archiviare qualsiasi tipo di dati di testo o binari, ad esempio un documento, un file multimediale o un programma di installazione di un'applicazione. Archiviazione BLOB è anche archiviazione di oggetti di cui viene fatto riferimento tooas.

Questa esercitazione viene illustrato come toowrite ASP.NET codice in alcuni scenari comuni di utilizzo dell'archiviazione blob di Azure. Gli scenari includono la creazione di un contenitore BLOB e il caricamento, la creazione di elenchi, il download e l'eliminazione di BLOB.

##<a name="prerequisites"></a>Prerequisiti

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Account di archiviazione di Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a>Creare un controller MVC 

1. In hello **Esplora soluzioni**, fare doppio clic su **controller**, selezionare il menu di scelta rapida hello **Aggiungi -> Controller**.

    ![Aggiungere un tooan controller app ASP.NET MVC](./media/vs-storage-aspnet-getting-started-blobs/add-controller-menu.png)

1. In hello **aggiungere lo scaffolding** finestra di dialogo Seleziona **Controller MVC 5 - vuoto**e selezionare **Aggiungi**.

    ![Specificare il tipo di controller MVC](./media/vs-storage-aspnet-getting-started-blobs/add-controller.png)

1. In hello **Aggiungi Controller** finestra di dialogo, nome del controller hello *BlobsController*e selezionare **Aggiungi**.

    ![Controller MVC hello di nome](./media/vs-storage-aspnet-getting-started-blobs/add-controller-name.png)

1. Aggiungere il seguente hello *utilizzando* toohello direttive `BlobsController.cs` file:

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

## <a name="create-a-blob-container"></a>Creare un contenitore BLOB

Un contenitore BLOB è una gerarchia nidificata di BLOB e cartelle. Hello passaggi seguenti viene illustrato come un contenitore blob toocreate:

> [!NOTE]
> 
> Hello codice in questa sezione si presuppone di aver completato i passaggi di hello nella sezione hello [configurare un ambiente di sviluppo hello](#set-up-the-development-environment). 

1. Aprire hello `BlobsController.cs` file.

1. Aggiungere un metodo denominato **CreateBlobContainer** che restituisce un **ActionResult**.

    ```csharp
    public ActionResult CreateBlobContainer()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. All'interno di hello **CreateBlobContainer** (metodo), ottenere un **CloudStorageAccount** oggetto che rappresenta le informazioni sull'account di archiviazione. Utilizzare hello seguendo codice tooget hello archiviazione stringa e l'archiviazione account informazioni di connessione dalla configurazione del servizio Azure hello. (Modifica  *&lt;storage-account-name >* toohello nome di account di archiviazione di Azure si accede hello.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Recuperare un oggetto **CloudBlobClient** che rappresenta un client del servizio BLOB.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Ottenere un **CloudBlobContainer** oggetto che rappresenta un nome di contenitore blob desiderato toohello di riferimento. Hello **CloudBlobClient.GetContainerReference** metodo non effettuare una richiesta nel servizio di archiviazione blob. contenitore blob hello esista o meno, viene restituito il riferimento di Hello. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. Chiamare hello **CloudBlobContainer.CreateIfNotExists** contenitore di hello toocreate metodo se non esiste ancora. Hello **CloudBlobContainer.CreateIfNotExists** restituisce **true** se hello contenitore non esiste e viene creato correttamente. In caso contrario, viene restituito **false**.    

    ```csharp
    ViewBag.Success = container.CreateIfNotExists();
    ```

1. Hello aggiornamento **ViewBag** con nome hello del contenitore blob hello.

    ```csharp
    ViewBag.BlobContainerName = container.Name;
    ```

1. In hello **Esplora**, espandere hello **viste** cartella, fare doppio clic su **BLOB**e quindi scegliere il menu di scelta rapida hello **Aggiungi -> Vista**.

1. In hello **Aggiungi visualizzazione** finestra di dialogo immettere **CreateBlobContainer** per nome della visualizzazione hello e selezionare **Aggiungi**.

1. Aprire `CreateBlobContainer.cshtml`e modificarlo in modo che risulti simile hello frammento di codice seguente:

    ```csharp
    @{
        ViewBag.Title = "Create Blob Container";
    }
    
    <h2>Create Blob Container results</h2>

    Creation of @ViewBag.BlobContainerName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. In hello **Esplora**, espandere hello **viste -> Shared** cartella e aprire `_Layout.cshtml`.

1. Dopo aver hello ultimo **HTML. ActionLink**, aggiungere il seguente hello **HTML. ActionLink**:

    ```html
    <li>@Html.ActionLink("Create blob container", "CreateBlobContainer", "Blobs")</li>
    ```

1. Eseguire un'applicazione hello e selezionare **crea contenitore Blob** toosee risultati simile toohello cattura di schermata seguente:
  
    ![Creare un contenitore BLOB](./media/vs-storage-aspnet-getting-started-blobs/create-blob-container-results.png)

    Come accennato in precedenza, hello **CloudBlobContainer.CreateIfNotExists** restituisce **true** solo quando il contenitore di hello non esiste e viene creato. Pertanto, se si esegue l'applicazione hello quando hello contenitore esiste, il metodo di hello restituisce **false**. app hello toorun più volte, è necessario eliminare il contenitore di hello prima di eseguire nuovamente l'applicazione hello. Contenitore hello eliminazione può essere eseguite tramite hello **CloudBlobContainer.Delete** metodo. È anche possibile eliminare il contenitore di hello utilizzando hello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) o hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).  

## <a name="upload-a-blob-into-a-blob-container"></a>Caricare un BLOB in un contenitore BLOB

Dopo avere [creato un contenitore BLOB](#create-a-blob-container), è possibile caricare file in questo contenitore. In questa sezione viene illustrato il caricamento di un contenitore di blob tooa file locale. passaggi di Hello presuppongono la creazione di un contenitore blob denominato *contenitore di blob test*. 

> [!NOTE]
> 
> Hello codice in questa sezione si presuppone di aver completato i passaggi di hello nella sezione hello [configurare un ambiente di sviluppo hello](#set-up-the-development-environment). 

1. Aprire hello `BlobsController.cs` file.

1. Aggiungere un metodo denominato **UploadBlob** che restituisce un **EmptyResult**.

    ```csharp
    public EmptyResult UploadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. All'interno di hello **UploadBlob** (metodo), ottenere un **CloudStorageAccount** oggetto che rappresenta le informazioni sull'account di archiviazione. Esempio di codice seguente di hello utilizzare tooget hello archiviazione stringa e l'archiviazione account informazioni di connessione di configurazione del servizio Azure hello: (modifica  *&lt;storage-account-name >* toohello nome hello archiviazione di Azure account che si accede.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Recuperare un oggetto **CloudBlobClient** che rappresenta un client del servizio BLOB.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Ottenere un **CloudBlobContainer** oggetto che rappresenta un nome di contenitore blob toohello di riferimento. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. Come illustrato in precedenza, l'Archiviazione di Azure supporta tipi di BLOB diversi. tooretrieve un blob di pagine di riferimento tooa, chiamata hello **CloudBlobContainer.GetPageBlobReference** metodo. tooretrieve un blob in blocchi, tooa riferimento chiamata hello **CloudBlobContainer.GetBlockBlobReference** metodo. Blob in blocchi in genere, è consigliata toouse tipo hello. (Modifica < nome del blob > * toohello nome blob hello toogive una volta caricato.)

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. Dopo aver creato un riferimento di blob, è possibile caricare qualsiasi tooit di flusso di dati chiamando hello blob riferimento oggetto **UploadFromStream** metodo. Hello **UploadFromStream** metodo consente di creare blob hello se non esiste o lo sovrascrive se esiste. (Modifica  *&lt;al caricamento di file >* tooa completo file di toohello percorso desiderato tooupload.)

    ```csharp
    using (var fileStream = System.IO.File.OpenRead(<file-to-upload>))
    {
        blob.UploadFromStream(fileStream);
    }
    ```

1. In hello **Esplora**, espandere hello **viste** cartella, fare doppio clic su **BLOB**e quindi scegliere il menu di scelta rapida hello **Aggiungi -> Vista**.

1. In hello **Esplora**, espandere hello **viste -> Shared** cartella e aprire `_Layout.cshtml`.

1. Dopo aver hello ultimo **HTML. ActionLink**, aggiungere il seguente hello **HTML. ActionLink**:

    ```html
    <li>@Html.ActionLink("Upload blob", "UploadBlob", "Blobs")</li>
    ```

1. Eseguire un'applicazione hello e selezionare **caricamento blob**.  
  
Hello sezione - [elencare i BLOB hello in un contenitore blob](#list-the-blobs-in-a-blob-container) -illustra come hello toolist BLOB in un contenitore blob.  

## <a name="list-hello-blobs-in-a-blob-container"></a>Elencare i BLOB hello in un contenitore blob

In questa sezione viene illustrato come hello toolist BLOB in un contenitore blob. codice di esempio Hello fa riferimento a hello *contenitore di blob test* creato nella sezione hello, [creare un contenitore blob](#create-a-blob-container).

> [!NOTE]
> 
> Hello codice in questa sezione si presuppone di aver completato i passaggi di hello nella sezione hello [configurare un ambiente di sviluppo hello](#set-up-the-development-environment). 

1. Aprire hello `BlobsController.cs` file.

1. Aggiungere un metodo denominato **ListBlobs** che restituisce un **ActionResult**.

    ```csharp
    public ActionResult ListBlobs()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. All'interno di hello **ListBlobs** (metodo), ottenere un **CloudStorageAccount** oggetto che rappresenta le informazioni sull'account di archiviazione. Esempio di codice seguente di hello utilizzare tooget hello archiviazione stringa e l'archiviazione account informazioni di connessione di configurazione del servizio Azure hello: (modifica  *&lt;storage-account-name >* toohello nome hello archiviazione di Azure account che si accede.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Recuperare un oggetto **CloudBlobClient** che rappresenta un client del servizio BLOB.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Ottenere un **CloudBlobContainer** oggetto che rappresenta un nome di contenitore blob toohello di riferimento. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. BLOB hello toolist in un contenitore blob, utilizzare hello **cloudblobcontainer. Listblobs** metodo. Hello **cloudblobcontainer. Listblobs** metodo restituisce un **IListBlobItem** dell'oggetto che si esegue il cast tooa **CloudBlockBlob**, **CloudPageBlob**, o **CloudBlobDirectory** oggetto. Hello frammento di codice seguente consente di enumerare tutti i BLOB hello in un contenitore blob. Ciascun blob è il cast toohello appropriato di oggetti in base a tipo e il relativo nome (nel caso di hello di URI o un **CloudBlobDirectory**) viene aggiunto l'elenco tooa.

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

    In aggiunta tooblobs, contenitori blob possono contenere le directory. Si supponga di disporre di un contenitore blob denominato *contenitore di blob test* con hello seguente gerarchia:

        foo.png
        dir1/bar.png
        dir2/baz.png

    Utilizza hello precedente esempio di codice, hello **BLOB** elenco stringa siano contenuti valori simili toohello:

        foo.png
        <storage-account-url>/test-blob-container/dir1
        <storage-account-url>/test-blob-container/dir2

    Come si può notare, l'elenco di hello include solo hello livello principale le entità; hello non annidati quelle (*bar.png* e *baz.png*). toolist tutti hello entità all'interno di un contenitore blob, è necessario chiamare hello **cloudblobcontainer. Listblobs** (metodo) e passare **true** per hello **useFlatBlobListing** parametro.    

    ```csharp
    ...
    foreach (IListBlobItem item in container.ListBlobs(useFlatBlobListing:true))
    ...
    ```

    Hello impostazione **useFlatBlobListing** parametro troppo**true** restituisce un elenco semplice di tutte le entità nel contenitore di blob hello e produce hello seguenti risultati:

        foo.png
        dir1/bar.png
        dir2/baz.png

1. In hello **Esplora**, espandere hello **viste** cartella, fare doppio clic su **BLOB**e quindi scegliere il menu di scelta rapida hello **Aggiungi -> Vista**.

1. In hello **Aggiungi visualizzazione** finestra di dialogo immettere **ListBlobs** per nome della visualizzazione hello e selezionare **Aggiungi**.

1. Aprire `ListBlobs.cshtml`e modificarlo in modo che risulti simile hello frammento di codice seguente:

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

1. In hello **Esplora**, espandere hello **viste -> Shared** cartella e aprire `_Layout.cshtml`.

1. Dopo aver hello ultimo **HTML. ActionLink**, aggiungere il seguente hello **HTML. ActionLink**:

    ```html
    <li>@Html.ActionLink("List blobs", "ListBlobs", "Blobs")</li>
    ```

1. Eseguire un'applicazione hello e selezionare **elencare i BLOB** toosee risultati simile toohello cattura di schermata seguente:
  
    ![Elenco di BLOB](./media/vs-storage-aspnet-getting-started-blobs/listblobs.png)

## <a name="download-blobs"></a>Scaricare BLOB

In questa sezione viene illustrato come toodownload un blob e renderlo persistente contenuto di hello toolocal archiviazione o di lettura in una stringa. codice di esempio Hello fa riferimento a hello *contenitore di blob test* creato nella sezione hello, [creare un contenitore blob](#create-a-blob-container).

1. Aprire hello `BlobsController.cs` file.

1. Aggiungere un metodo denominato **DownloadBlob** che restituisce un **ActionResult**.

    ```csharp
    public EmptyResult DownloadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. All'interno di hello **DownloadBlob** (metodo), ottenere un **CloudStorageAccount** oggetto che rappresenta le informazioni sull'account di archiviazione. Esempio di codice seguente di hello utilizzare tooget hello archiviazione stringa e l'archiviazione account informazioni di connessione di configurazione del servizio Azure hello: (modifica  *&lt;storage-account-name >* toohello nome hello archiviazione di Azure account che si accede.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Recuperare un oggetto **CloudBlobClient** che rappresenta un client del servizio BLOB.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Ottenere un **CloudBlobContainer** oggetto che rappresenta un nome di contenitore blob toohello di riferimento. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. Recuperare un oggetto di riferimento al BLOB chiamando il metodo **CloudBlobContainer.GetBlockBlobReference** o **CloudBlobContainer.GetPageBlobReference**. (Modifica  *&lt;nome blob >* toohello nome di blob hello si scaricano.)

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. toodownload un blob, utilizzare hello **CloudBlockBlob.DownloadToStream** o **CloudPageBlob.DownloadToStream** (metodo), in base al tipo di blob hello. frammento di codice seguente Hello utilizza hello **CloudBlockBlob.DownloadToStream** tootransfer metodo flusso tooa di contenuto del blob, un oggetto che è quindi persistente file locale tooa: (modifica  *&lt;nome del file locale >* toohello completo di nome di file, che rappresenta il percorso blob hello scaricati.) 

    ```csharp
    using (var fileStream = System.IO.File.OpenWrite(<local-file-name>))
    {
        blob.DownloadToStream(fileStream);
    }
    ```

1. In hello **Esplora**, espandere hello **viste -> Shared** cartella e aprire `_Layout.cshtml`.

1. Dopo aver hello ultimo **HTML. ActionLink**, aggiungere il seguente hello **HTML. ActionLink**:

    ```html
    <li>@Html.ActionLink("Download blob", "DownloadBlob", "Blobs")</li>
    ```

1. Eseguire un'applicazione hello e selezionare **Download blob** blob hello toodownload. blob Hello specificato in hello **CloudBlobContainer.GetBlockBlobReference** chiamata al metodo scarica toohello percorso specificato in hello **file. OpenWrite** chiamata al metodo. 

## <a name="delete-blobs"></a>Eliminare BLOB

Hello passaggi seguenti viene illustrato come toodelete un blob:

> [!NOTE]
> 
> Hello codice in questa sezione si presuppone di aver completato i passaggi di hello nella sezione hello [configurare un ambiente di sviluppo hello](#set-up-the-development-environment). 

1. Aprire hello `BlobsController.cs` file.

1. Aggiungere un metodo denominato **DeleteBlob** che restituisce un **ActionResult**.

    ```csharp
    public EmptyResult DeleteBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```

1. Ottenere un oggetto **CloudStorageAccount** che rappresenta le informazioni sull'account di archiviazione. Esempio di codice seguente di hello utilizzare tooget hello archiviazione stringa e l'archiviazione account informazioni di connessione di configurazione del servizio Azure hello: (modifica  *&lt;storage-account-name >* toohello nome hello archiviazione di Azure account che si accede.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Recuperare un oggetto **CloudBlobClient** che rappresenta un client del servizio BLOB.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Ottenere un **CloudBlobContainer** oggetto che rappresenta un nome di contenitore blob toohello di riferimento. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. Recuperare un oggetto di riferimento al BLOB chiamando il metodo **CloudBlobContainer.GetBlockBlobReference** o **CloudBlobContainer.GetPageBlobReference**. (Modifica  *&lt;nome blob >* toohello nome di blob hello si sta eliminando.)

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
        ```

1. toodelete a blob, use hello **Delete** method.

    ```csharp
    blob.Delete();
    ```

1. In hello **Esplora**, espandere hello **viste -> Shared** cartella e aprire `_Layout.cshtml`.

1. Dopo aver hello ultimo **HTML. ActionLink**, aggiungere il seguente hello **HTML. ActionLink**:

    ```html
    <li>@Html.ActionLink("Delete blob", "DeleteBlob", "Blobs")</li>
    ```

1. Eseguire un'applicazione hello e selezionare **Delete blob** blob hello toodelete specificato in hello **CloudBlobContainer.GetBlockBlobReference** chiamata al metodo. 

## <a name="next-steps"></a>Passaggi successivi
Consente di visualizzare altre toolearn di guide di funzionalità sulle opzioni aggiuntive per l'archiviazione dei dati in Azure.

  * [Introduzione all'archiviazione tabelle di Azure e ai Servizi connessi di Visual Studio (ASP.NET)](vs-storage-aspnet-getting-started-tables.md)
  * [Introduzione all'archiviazione code di Azure e ai Servizi connessi di Visual Studio (ASP.NET)](vs-storage-aspnet-getting-started-queues.md)
