---
title: aaaGet avviato con l'archiviazione tabelle di Azure e Visual Studio connesso servizi (ASP.NET) | Documenti Microsoft
description: "La modalità di avvio utilizzando l'archiviazione tabelle di Azure in un progetto ASP.NET in Visual Studio dopo la connessione di account di archiviazione tooa con Visual Studio connesso Services tooget"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: af81a326-18f4-4449-bc0d-e96fba27c1f8
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: tarcher
ms.openlocfilehash: e7ed17098c8742954972dc9e1b50eca77221e327
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-table-storage-and-visual-studio-connected-services-aspnet"></a>Introduzione all'archiviazione tabelle di Azure e a Servizi connessi di Visual Studio (ASP.NET)
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a>Panoramica

Archiviazione tabelle di Azure consente toostore grandi quantità di dati strutturati. servizio Hello è un archivio dati NoSQL che accetta chiamate autenticate dall'interno ed esterno hello cloud di Azure. Le tabelle di Azure sono ideali per l'archiviazione di dati strutturati non relazionali.

Questa esercitazione viene illustrato come toowrite ASP.NET codice in alcuni scenari comuni con le entità di archiviazione tabelle di Azure. Questi scenari includono la creazione di una tabella, l'aggiunta, la creazione di query ed eliminazione di entità di tabella. 

##<a name="prerequisites"></a>Prerequisiti

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Account di archiviazione di Azure](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a>Creare un controller MVC 

1. In hello **Esplora soluzioni**, fare doppio clic su **controller**, selezionare il menu di scelta rapida hello **Aggiungi -> Controller**.

    ![Aggiungere un tooan controller app ASP.NET MVC](./media/vs-storage-aspnet-getting-started-tables/add-controller-menu.png)

1. In hello **aggiungere lo scaffolding** finestra di dialogo Seleziona **Controller MVC 5 - vuoto**e selezionare **Aggiungi**.

    ![Specificare il tipo di controller MVC](./media/vs-storage-aspnet-getting-started-tables/add-controller.png)

1. In hello **Aggiungi Controller** finestra di dialogo, nome del controller hello *TablesController*e selezionare **Aggiungi**.

    ![Controller MVC hello di nome](./media/vs-storage-aspnet-getting-started-tables/add-controller-name.png)

1. Aggiungere il seguente hello *utilizzando* toohello direttive `TablesController.cs` file:

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Table;
    ```

### <a name="create-a-model-class"></a>Creare una classe di modello

Molti degli esempi di hello in questo articolo usa una **TableEntity**-derivata denominata **CustomerEntity**. Hello passaggi consentono di eseguire la dichiarazione di questa classe come classe di modello:

1. In hello **Esplora**, fare doppio clic su **modelli**, selezionare il menu di scelta rapida hello **Aggiungi -> classe**.

1. In hello **Aggiungi nuovo elemento** finestra di dialogo, nome classe hello, **CustomerEntity**.

1. Aprire hello `CustomerEntity.cs` file e aggiungere il seguente hello **utilizzando** direttiva:

    ```csharp
    using Microsoft.WindowsAzure.Storage.Table;
    ```

1. Modificare la classe hello in modo che, al termine, la classe hello è dichiarata come hello seguente codice. classe Hello dichiara una classe di entità denominata **CustomerEntity** che utilizza hello nome del cliente come chiave di riga hello e il cognome come chiave di partizione hello.

    ```csharp
    public class CustomerEntity : TableEntity
    {
        public CustomerEntity(string lastName, string firstName)
        {
            this.PartitionKey = lastName;
            this.RowKey = firstName;
        }

        public CustomerEntity() { }

        public string Email { get; set; }
    }
    ```

## <a name="create-a-table"></a>Creare una tabella

Hello passaggi seguenti viene illustrato come toocreate una tabella:

> [!NOTE]
> 
> Questa sezione si presuppone di aver completato i passaggi di hello in [configurare un ambiente di sviluppo hello](#set-up-the-development-environment). 

1. Aprire hello `TablesController.cs` file.

1. Aggiungere un metodo denominato **CreateTable** che restituisce un **ActionResult**.

    ```csharp
    public ActionResult CreateTable()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. All'interno di hello **CreateTable** (metodo), ottenere un **CloudStorageAccount** oggetto che rappresenta le informazioni sull'account di archiviazione. Esempio di codice seguente di hello utilizzare tooget hello archiviazione stringa e l'archiviazione account informazioni di connessione di configurazione del servizio Azure hello: (modifica  *&lt;storage-account-name >* toohello nome hello archiviazione di Azure account che si accede.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Ottenere un oggetto **CloudTableClient** che rappresenta un client del servizio tabelle.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Ottenere un **CloudTable** oggetto che rappresenta un nome di riferimento toohello tabella desiderata. Hello **CloudTableClient.GetTableReference** metodo non effettuare una richiesta nel servizio di archiviazione tabella. tabella hello esista o meno, viene restituito il riferimento di Hello. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Chiamare hello **CloudTable.CreateIfNotExists** tabella dei metodi toocreate hello se non esiste ancora. Hello **CloudTable.CreateIfNotExists** restituisce **true** se non esiste nella tabella hello e viene creata correttamente. In caso contrario, viene restituito **false**.    

    ```csharp
    ViewBag.Success = table.CreateIfNotExists();
    ```

1. Hello aggiornamento **ViewBag** con nome hello hello table.

    ```csharp
    ViewBag.TableName = table.Name;
    ```

1. In hello **Esplora**, espandere hello **viste** cartella, fare doppio clic su **tabelle**e quindi scegliere il menu di scelta rapida hello **Aggiungi -> Vista**.

1. In hello **Aggiungi visualizzazione** finestra di dialogo immettere **CreateTable** per nome della visualizzazione hello e selezionare **Aggiungi**.

1. Aprire `CreateTable.cshtml`e modificarlo in modo che risulti simile hello frammento di codice seguente:

    ```csharp
    @{
        ViewBag.Title = "Create Table";
    }
    
    <h2>Create Table results</h2>

    Creation of @ViewBag.TableName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. In hello **Esplora**, espandere hello **viste -> Shared** cartella e aprire `_Layout.cshtml`.

1. Dopo aver hello ultimo **HTML. ActionLink**, aggiungere il seguente hello **HTML. ActionLink**:

    ```html
    <li>@Html.ActionLink("Create table", "CreateTable", "Tables")</li>
    ```

1. Eseguire un'applicazione hello e selezionare **crea una tabella** toosee risultati simile toohello cattura di schermata seguente:
  
    ![Crea tabella](./media/vs-storage-aspnet-getting-started-tables/create-table-results.png)

    Come accennato in precedenza, hello **CloudTable.CreateIfNotExists** restituisce **true** solo quando la tabella hello non esiste e viene creata. Pertanto, se si esegue l'applicazione hello quando hello tabella esiste, il metodo di hello restituisce **false**. app hello toorun più volte, è necessario eliminare la tabella hello prima di eseguire nuovamente l'applicazione hello. Eliminazione della tabella hello possono essere eseguita tramite hello **CloudTable.Delete** metodo. È anche possibile eliminare tabella hello utilizzando hello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) o hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).  

## <a name="add-an-entity-tooa-table"></a>Aggiungere una tabella tooa entità

*Entità* mapping tooC\# oggetti usando una classe personalizzata derivata da **TableEntity**. tooadd tabella tooa un'entità, creare una classe che definisce le proprietà di hello dell'entità. In questa sezione, verrà visualizzato come una classe di entità che utilizza toodefine hello nome del cliente come chiave di riga hello e il cognome come chiave di partizione hello. Insieme, di partizione e chiave di riga identificano entità hello nella tabella di hello. Le query su entità con la stessa chiave di partizione vengono eseguite più rapidamente di quelle con chiavi di partizione diverse, tuttavia l'uso di chiavi di partizione diverse assicura una maggiore scalabilità delle operazioni parallele. Per qualsiasi proprietà che devono essere archiviati nel servizio tabelle hello, proprietà hello deve essere una proprietà pubblica di un tipo supportato che espone sia l'impostazione e recupero di valori.
classe di entità Hello *deve* dichiarare un costruttore senza parametri pubblico.

> [!NOTE]
> 
> Questa sezione si presuppone di aver completato i passaggi di hello in [configurare un ambiente di sviluppo hello](#set-up-the-development-environment).

1. Aprire hello `TablesController.cs` file.

1. Aggiungere hello dopo la direttiva in modo che hello codice hello `TablesController.cs` file può accedere hello **CustomerEntity** classe:

    ```csharp
    using StorageAspnet.Models;
    ```

1. Aggiungere un metodo denominato **AddEntity** che restituisce un **ActionResult**.

    ```csharp
    public ActionResult AddEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. All'interno di hello **AddEntity** (metodo), ottenere un **CloudStorageAccount** oggetto che rappresenta le informazioni sull'account di archiviazione. Esempio di codice seguente di hello utilizzare tooget hello archiviazione stringa e l'archiviazione account informazioni di connessione di configurazione del servizio Azure hello: (modifica  *&lt;storage-account-name >* toohello nome hello archiviazione di Azure account che si accede.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Ottenere un oggetto **CloudTableClient** che rappresenta un client del servizio tabelle.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Ottenere un **CloudTable** oggetto che rappresenta un toowhich tabella toohello di riferimento si intende una nuova entità di tooadd hello. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Creare e inizializzare hello **CustomerEntity** classe.

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    ```

1. Creare un **TableOperation** che inserisce l'entità customer hello.

    ```csharp
    TableOperation insertOperation = TableOperation.Insert(customer1);
    ```

1. Eseguire l'operazione di inserimento hello dal chiamante hello **CloudTable.Execute** metodo. È possibile verificare il risultato di hello dell'operazione di hello controllando hello **TableResult.HttpStatusCode** proprietà. Un codice di stato di 2xx indica l'azione di hello richiesta dal client hello è stato elaborato correttamente. Ad esempio, ha esito positivo le operazioni di inserimento della nuova entità risultato in un codice di stato HTTP 204, vale a dire che è stata elaborata correttamente operazione hello e server hello non ha restituito alcun contenuto.

    ```csharp
    TableResult result = table.Execute(insertOperation);
    ```

1. Hello aggiornamento **ViewBag** con il nome di tabella hello e hello risultati dell'operazione di inserimento hello.

    ```csharp
    ViewBag.TableName = table.Name;
    ViewBag.Result = result.HttpStatusCode;
    ```

1. In hello **Esplora**, espandere hello **viste** cartella, fare doppio clic su **tabelle**e quindi scegliere il menu di scelta rapida hello **Aggiungi -> Vista**.

1. In hello **Aggiungi visualizzazione** finestra di dialogo immettere **AddEntity** per nome della visualizzazione hello e selezionare **Aggiungi**.

1. Aprire `AddEntity.cshtml`e modificarlo in modo che risulti simile hello frammento di codice seguente:

    ```csharp
    @{
        ViewBag.Title = "Add entity";
    }
    
    <h2>Add entity results</h2>

    Insert of entity into @ViewBag.TableName @(ViewBag.Result == 204 ? "succeeded" : "failed")
    ```
1. In hello **Esplora**, espandere hello **viste -> Shared** cartella e aprire `_Layout.cshtml`.

1. Dopo aver hello ultimo **HTML. ActionLink**, aggiungere il seguente hello **HTML. ActionLink**:

    ```html
    <li>@Html.ActionLink("Add entity", "AddEntity", "Tables")</li>
    ```

1. Eseguire un'applicazione hello e selezionare **aggiungere entità** toosee risultati simile toohello cattura di schermata seguente:
  
    ![Aggiungi entità](./media/vs-storage-aspnet-getting-started-tables/add-entity-results.png)

    È possibile verificare che sia stato aggiunto entità hello seguendo i passaggi di hello nella sezione hello, [ottenere una singola entità](#get-a-single-entity). È inoltre possibile utilizzare hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview tutti hello entità per le tabelle.

## <a name="add-a-batch-of-entities-tooa-table"></a>Aggiungere un batch di tabella tooa entità

In aggiunta toobeing in grado di troppo[aggiungere una tabella tooa entità uno alla volta](#add-an-entity-to-a-table), è inoltre possibile aggiungere entità nel batch. Aggiunta di entità in batch riduce il numero di hello di round trip tra il codice e hello servizio tabelle di Azure. Hello alla procedura seguente viene illustrato come tooadd tooa di più entità di tabella con un'operazione di inserimento singolo:

> [!NOTE]
> 
> Questa sezione si presuppone di aver completato i passaggi di hello in [configurare un ambiente di sviluppo hello](#set-up-the-development-environment).

1. Aprire hello `TablesController.cs` file.

1. Aggiungere un metodo denominato **AddEntities** che restituisce un **ActionResult**.

    ```csharp
    public ActionResult AddEntities()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. All'interno di hello **AddEntities** (metodo), ottenere un **CloudStorageAccount** oggetto che rappresenta le informazioni sull'account di archiviazione. Esempio di codice seguente di hello utilizzare tooget hello archiviazione stringa e l'archiviazione account informazioni di connessione di configurazione del servizio Azure hello: (modifica  *&lt;storage-account-name >* toohello nome hello archiviazione di Azure account che si accede.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Ottenere un oggetto **CloudTableClient** che rappresenta un client del servizio tabelle.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Ottenere un **CloudTable** oggetto che rappresenta un toowhich tabella toohello di riferimento sono nuove entità corso tooadd hello. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Creare un'istanza di alcuni oggetti di clienti in base a hello **CustomerEntity** classe presentati nella sezione hello modello [aggiungere una tabella tooa entità](#add-an-entity-to-a-table).

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
    customer1.Email = "Jeff@contoso.com";

    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.Email = "Ben@contoso.com";
    ```

1. Ottenere un oggetto **TableBatchOperation**.

    ```csharp
    TableBatchOperation batchOperation = new TableBatchOperation();
    ```

1. Aggiungere l'oggetto dell'operazione di inserimento batch toohello entità.

    ```csharp
    batchOperation.Insert(customer1);
    batchOperation.Insert(customer2);
    ```

1. Eseguire l'operazione di inserimento batch hello dal chiamante hello **CloudTable.ExecuteBatch** metodo.   

    ```csharp
    IList<TableResult> results = table.ExecuteBatch(batchOperation);
    ```

1. Hello **CloudTable.ExecuteBatch** il metodo restituisce un elenco di **TableResult** oggetti in cui ogni **TableResult** oggetto può essere esaminato toodetermine hello riuscita o meno di ogni singola operazione. In questo esempio hello elenco tooa visualizzazione passata e consente di visualizzare i risultati di hello di ogni operazione visualizzazione hello. 
 
    ```csharp
    return View(results);
    ```

1. In hello **Esplora**, espandere hello **viste** cartella, fare doppio clic su **tabelle**e quindi scegliere il menu di scelta rapida hello **Aggiungi -> Vista**.

1. In hello **Aggiungi visualizzazione** finestra di dialogo immettere **AddEntities** per nome della visualizzazione hello e selezionare **Aggiungi**.

1. Aprire `AddEntities.cshtml`e modificarlo in modo che risulti simile hello seguente.

    ```csharp
    @model IEnumerable<Microsoft.WindowsAzure.Storage.Table.TableResult>
    @{
        ViewBag.Title = "AddEntities";
    }
    
    <h2>Add-entities results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>HTTP result</th>
        </tr>
        @foreach (var result in Model)
        {
        <tr>
            <td>@((result.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((result.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@result.HttpStatusCode</td>
        </tr>
        }
    </table>
    ```

1. In hello **Esplora**, espandere hello **viste -> Shared** cartella e aprire `_Layout.cshtml`.

1. Dopo aver hello ultimo **HTML. ActionLink**, aggiungere il seguente hello **HTML. ActionLink**:

    ```html
    <li>@Html.ActionLink("Add entities", "AddEntities", "Tables")</li>
    ```

1. Eseguire un'applicazione hello e selezionare **aggiungere entità** toosee risultati simile toohello cattura di schermata seguente:
  
    ![Aggiungi entità](./media/vs-storage-aspnet-getting-started-tables/add-entities-results.png)

    È possibile verificare che sia stato aggiunto entità hello seguendo i passaggi di hello nella sezione hello, [ottenere una singola entità](#get-a-single-entity). È inoltre possibile utilizzare hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview tutti hello entità per le tabelle.

## <a name="get-a-single-entity"></a>Ottenere una singola entità

In questa sezione viene illustrato come una singola entità da una tabella utilizzando tooget hello chiave di riga e la chiave di partizione dell'entità. 

> [!NOTE]
> 
> Questa sezione si presuppone di aver completato i passaggi di hello in [configurare un ambiente di sviluppo hello](#set-up-the-development-environment)e utilizza i dati di [aggiungere un batch di tabella tooa entità](#add-a-batch-of-entities-to-a-table). 

1. Aprire hello `TablesController.cs` file.

1. Aggiungere un metodo denominato **GetSingle** che restituisce un **ActionResult**.

    ```csharp
    public ActionResult GetSingle()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. All'interno di hello **GetSingle** (metodo), ottenere un **CloudStorageAccount** oggetto che rappresenta le informazioni sull'account di archiviazione. Esempio di codice seguente di hello utilizzare tooget hello archiviazione stringa e l'archiviazione account informazioni di connessione di configurazione del servizio Azure hello: (modifica  *&lt;storage-account-name >* toohello nome hello archiviazione di Azure account che si accede.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Ottenere un oggetto **CloudTableClient** che rappresenta un client del servizio tabelle.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Ottenere un **CloudTable** oggetto che rappresenta una tabella di riferimento toohello da cui si desidera recuperare entità hello. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Creare un oggetto operazione di recupero che accetta un oggetto entità derivato da **TableEntity**. il primo parametro Hello è hello *partitionKey*, e il secondo parametro hello è hello *rowKey*. Utilizzando hello **CustomerEntity** classe e i dati presentati nella sezione hello [aggiungere un batch di tabella tooa entità](#add-a-batch-of-entities-to-a-table), hello seguenti tabella query hello frammento di codice per un **CustomerEntity** entità con un *partitionKey* valore "Smith" e un *rowKey* valore di "Ben":

    ```csharp
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");
    ```

1. Eseguire l'operazione di recupero hello.   

    ```csharp
    TableResult result = table.Execute(retrieveOperation);
    ```

1. Passare a visualizzazione toohello hello dei risultati per la visualizzazione.

    ```csharp
    return View(result);
    ```

1. In hello **Esplora**, espandere hello **viste** cartella, fare doppio clic su **tabelle**e quindi scegliere il menu di scelta rapida hello **Aggiungi -> Vista**.

1. In hello **Aggiungi visualizzazione** finestra di dialogo immettere **GetSingle** per nome della visualizzazione hello e selezionare **Aggiungi**.

1. Aprire `GetSingle.cshtml`e modificarlo in modo che risulti simile hello frammento di codice seguente:

    ```csharp
    @model Microsoft.WindowsAzure.Storage.Table.TableResult
    @{
        ViewBag.Title = "GetSingle";
    }
    
    <h2>Get Single results</h2>
    
    <table border="1">
        <tr>
            <th>HTTP result</th>
            <th>First name</th>
            <th>Last name</th>
            <th>Email</th>
        </tr>
        <tr>
            <td>@Model.HttpStatusCode</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).Email)</td>
        </tr>
    </table>
    ```

1. In hello **Esplora**, espandere hello **viste -> Shared** cartella e aprire `_Layout.cshtml`.

1. Dopo aver hello ultimo **HTML. ActionLink**, aggiungere il seguente hello **HTML. ActionLink**:

    ```html
    <li>@Html.ActionLink("Get single", "GetSingle", "Tables")</li>
    ```

1. Eseguire un'applicazione hello e selezionare **ottenere singolo** toosee risultati simile toohello cattura di schermata seguente:
  
    ![Get single](./media/vs-storage-aspnet-getting-started-tables/get-single-results.png)

## <a name="get-all-entities-in-a-partition"></a>Recuperare tutte le entità di una partizione

Come indicato nella sezione hello [aggiungere una tabella di entità tooa](#add-an-entity-to-a-table), combinazione di hello di una partizione e una chiave di riga identifica in modo univoco un'entità in una tabella. Le query su entità con la stessa chiave di partizione vengono eseguite più rapidamente di quelle con chiavi di partizione diverse. In questa sezione viene illustrato come tooquery una tabella per tutte le entità hello da una partizione specificata.  

> [!NOTE]
> 
> Questa sezione si presuppone di aver completato i passaggi di hello in [configurare un ambiente di sviluppo hello](#set-up-the-development-environment)e utilizza i dati di [aggiungere un batch di tabella tooa entità](#add-a-batch-of-entities-to-a-table). 

1. Aprire hello `TablesController.cs` file.

1. Aggiungere un metodo denominato **GetPartition** che restituisce un **ActionResult**.

    ```csharp
    public ActionResult GetPartition()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. All'interno di hello **GetPartition** (metodo), ottenere un **CloudStorageAccount** oggetto che rappresenta le informazioni sull'account di archiviazione. Esempio di codice seguente di hello utilizzare tooget hello archiviazione stringa e l'archiviazione account informazioni di connessione di configurazione del servizio Azure hello: (modifica  *&lt;storage-account-name >* toohello nome hello archiviazione di Azure account che si accede.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Ottenere un oggetto **CloudTableClient** che rappresenta un client del servizio tabelle.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Ottenere un **CloudTable** oggetto che rappresenta una tabella di riferimento toohello da cui si desidera recuperare entità hello. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Creare un'istanza di un **TableQuery** oggetto che specifica la query hello in hello **dove** clausola. Utilizzando hello **CustomerEntity** classe e i dati presentati nella sezione hello [aggiungere un batch di tabella tooa entità](#add-a-batch-of-entities-to-a-table), tabella di hello frammento query per tutte le entità di codice seguente di hello dove hello  **PartitionKey** (cognome del cliente) ha un valore di "Smith":

    ```csharp
    TableQuery<CustomerEntity> query = 
        new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));
    ```

1. All'interno di un ciclo, chiamare hello **CloudTable.ExecuteQuerySegmented** passando l'oggetto query hello è creata un'istanza nel passaggio precedente hello.  Hello **CloudTable.ExecuteQuerySegmented** metodo restituisce un **TableContinuationToken** - oggetto quando **null** -indica che non sono più alcuna entità tooretrieve. Nel ciclo di hello, utilizzare un altro ciclo tooiterate hello le entità restituita. Nell'esempio di codice seguente di hello, ogni entità restituita viene aggiunta tooa elenco. Una volta hello ciclo termina, elenco hello viene passato tooa visualizzazione per la visualizzazione: 

    ```csharp
    List<CustomerEntity> customers = new List<CustomerEntity>();
    TableContinuationToken token = null;
    do
    {
        TableQuerySegment<CustomerEntity> resultSegment = table.ExecuteQuerySegmented(query, token);
        token = resultSegment.ContinuationToken;

        foreach (CustomerEntity customer in resultSegment.Results)
        {
            customers.Add(customer);
        }
    } while (token != null);

    return View(customers);
    ```

1. In hello **Esplora**, espandere hello **viste** cartella, fare doppio clic su **tabelle**e quindi scegliere il menu di scelta rapida hello **Aggiungi -> Vista**.

1. In hello **Aggiungi visualizzazione** finestra di dialogo immettere **GetPartition** per nome della visualizzazione hello e selezionare **Aggiungi**.

1. Aprire `GetPartition.cshtml`e modificarlo in modo che risulti simile hello frammento di codice seguente:

    ```csharp
    @model IEnumerable<StorageAspnet.Models.CustomerEntity>
    @{
        ViewBag.Title = "GetPartition";
    }
    
    <h2>Get Partition results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>Email</th>
        </tr>
        @foreach (var customer in Model)
        {
        <tr>
            <td>@(customer.RowKey)</td>
            <td>@(customer.PartitionKey)</td>
            <td>@(customer.Email)</td>
        </tr>
        }
    </table>
    ```

1. In hello **Esplora**, espandere hello **viste -> Shared** cartella e aprire `_Layout.cshtml`.

1. Dopo aver hello ultimo **HTML. ActionLink**, aggiungere il seguente hello **HTML. ActionLink**:

    ```html
    <li>@Html.ActionLink("Get partition", "GetPartition", "Tables")</li>
    ```

1. Eseguire un'applicazione hello e selezionare **ottenere partizione** toosee risultati simile toohello cattura di schermata seguente:
  
    ![Get Partition](./media/vs-storage-aspnet-getting-started-tables/get-partition-results.png)

## <a name="delete-an-entity"></a>Eliminare un'entità

In questa sezione viene illustrato come toodelete un'entità da una tabella.

> [!NOTE]
> 
> Questa sezione si presuppone di aver completato i passaggi di hello in [configurare un ambiente di sviluppo hello](#set-up-the-development-environment)e utilizza i dati di [aggiungere un batch di tabella tooa entità](#add-a-batch-of-entities-to-a-table). 

1. Aprire hello `TablesController.cs` file.

1. Aggiungere un metodo denominato **DeleteEntity** che restituisce un **ActionResult**.

    ```csharp
    public ActionResult DeleteEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. All'interno di hello **DeleteEntity** (metodo), ottenere un **CloudStorageAccount** oggetto che rappresenta le informazioni sull'account di archiviazione. Esempio di codice seguente di hello utilizzare tooget hello archiviazione stringa e l'archiviazione account informazioni di connessione di configurazione del servizio Azure hello: (modifica  *&lt;storage-account-name >* toohello nome hello archiviazione di Azure account che si accede.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Ottenere un oggetto **CloudTableClient** che rappresenta un client del servizio tabelle.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Ottenere un **CloudTable** oggetto che rappresenta una tabella di riferimento toohello da cui si sta eliminando entità hello. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Creare un oggetto operazione di eliminazione che accetta un oggetto entità derivato da **TableEntity**. In questo caso, utilizziamo hello **CustomerEntity** classe e i dati presentati nella sezione hello [aggiungere un batch di tabella tooa entità](#add-a-batch-of-entities-to-a-table). Hello dell'entità **ETag** deve essere impostato tooa valido.  

    ```csharp
    TableOperation deleteOperation = 
        TableOperation.Delete(new CustomerEntity("Smith", "Ben") { ETag = "*" } );
    ```

1. Eseguire l'operazione di eliminazione di hello.   

    ```csharp
    TableResult result = table.Execute(deleteOperation);
    ```

1. Passare a visualizzazione toohello hello dei risultati per la visualizzazione.

    ```csharp
    return View(result);
    ```

1. In hello **Esplora**, espandere hello **viste** cartella, fare doppio clic su **tabelle**e quindi scegliere il menu di scelta rapida hello **Aggiungi -> Vista**.

1. In hello **Aggiungi visualizzazione** finestra di dialogo immettere **DeleteEntity** per nome della visualizzazione hello e selezionare **Aggiungi**.

1. Aprire `DeleteEntity.cshtml`e modificarlo in modo che risulti simile hello frammento di codice seguente:

    ```csharp
    @model Microsoft.WindowsAzure.Storage.Table.TableResult
    @{
        ViewBag.Title = "DeleteEntity";
    }
    
    <h2>Delete Entity results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>HTTP result</th>
        </tr>
        <tr>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@Model.HttpStatusCode</td>
        </tr>
    </table>

    ```

1. In hello **Esplora**, espandere hello **viste -> Shared** cartella e aprire `_Layout.cshtml`.

1. Dopo aver hello ultimo **HTML. ActionLink**, aggiungere il seguente hello **HTML. ActionLink**:

    ```html
    <li>@Html.ActionLink("Delete entity", "DeleteEntity", "Tables")</li>
    ```

1. Eseguire un'applicazione hello e selezionare **eliminare entità** toosee risultati simile toohello cattura di schermata seguente:
  
    ![Get single](./media/vs-storage-aspnet-getting-started-tables/delete-entity-results.png)

## <a name="next-steps"></a>Passaggi successivi
Consente di visualizzare altre toolearn di guide di funzionalità sulle opzioni aggiuntive per l'archiviazione dei dati in Azure.

  * [Introduzione all'Archiviazione BLOB di Azure e ai Servizi connessi di Visual Studio (ASP.NET)](./vs-storage-aspnet-getting-started-blobs.md)
  * [Introduzione all'archiviazione code di Azure e ai Servizi connessi di Visual Studio (ASP.NET)](./vs-storage-aspnet-getting-started-queues.md)
