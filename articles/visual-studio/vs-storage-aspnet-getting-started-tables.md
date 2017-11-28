---
title: aaaGet avviato con l'archiviazione tabelle di Azure e Visual Studio connesso servizi (ASP.NET) | Documenti Microsoft
description: "La modalità di avvio utilizzando l'archiviazione tabelle di Azure in un progetto ASP.NET in Visual Studio dopo la connessione di account di archiviazione tooa con Visual Studio connesso Services tooget"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: af81a326-18f4-4449-bc0d-e96fba27c1f8
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: kraigb
ms.openlocfilehash: 04f79db7aad60ca51c3c866da1f4b01d9e11ac52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-table-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="7bf3f-103">Introduzione all'archiviazione tabelle di Azure e a Servizi connessi di Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="7bf3f-103">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="7bf3f-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="7bf3f-104">Overview</span></span>

<span data-ttu-id="7bf3f-105">Archiviazione tabelle di Azure consente toostore grandi quantità di dati strutturati.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-105">Azure Table storage enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="7bf3f-106">servizio Hello è un archivio dati NoSQL che accetta chiamate autenticate dall'interno ed esterno hello cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-106">hello service is a NoSQL datastore that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="7bf3f-107">Le tabelle di Azure sono ideali per l'archiviazione di dati strutturati non relazionali.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-107">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="7bf3f-108">Questa esercitazione viene illustrato come toowrite ASP.NET codice in alcuni scenari comuni con le entità di archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-108">This tutorial shows how toowrite ASP.NET code for some common scenarios using Azure table storage entities.</span></span> <span data-ttu-id="7bf3f-109">Questi scenari includono la creazione di una tabella, l'aggiunta, la creazione di query ed eliminazione di entità di tabella.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-109">These scenarios include creating a table, and adding, querying, and deleting table entities.</span></span> 

##<a name="prerequisites"></a><span data-ttu-id="7bf3f-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7bf3f-110">Prerequisites</span></span>

* [<span data-ttu-id="7bf3f-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7bf3f-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="7bf3f-112">Account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="7bf3f-112">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="7bf3f-113">Creare un controller MVC</span><span class="sxs-lookup"><span data-stu-id="7bf3f-113">Create an MVC controller</span></span> 

1. <span data-ttu-id="7bf3f-114">In hello **Esplora soluzioni**, fare doppio clic su **controller**, selezionare il menu di scelta rapida hello **Aggiungi -> Controller**.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-114">In hello **Solution Explorer**, right-click **Controllers**, and, from hello context menu, select **Add->Controller**.</span></span>

    ![Aggiungere un tooan controller app ASP.NET MVC](./media/vs-storage-aspnet-getting-started-tables/add-controller-menu.png)

1. <span data-ttu-id="7bf3f-116">In hello **aggiungere lo scaffolding** finestra di dialogo Seleziona **Controller MVC 5 - vuoto**e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-116">On hello **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Specificare il tipo di controller MVC](./media/vs-storage-aspnet-getting-started-tables/add-controller.png)

1. <span data-ttu-id="7bf3f-118">In hello **Aggiungi Controller** finestra di dialogo, nome del controller hello *TablesController*e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-118">On hello **Add Controller** dialog, name hello controller *TablesController*, and select **Add**.</span></span>

    ![Controller MVC hello di nome](./media/vs-storage-aspnet-getting-started-tables/add-controller-name.png)

1. <span data-ttu-id="7bf3f-120">Aggiungere il seguente hello *utilizzando* toohello direttive `TablesController.cs` file:</span><span class="sxs-lookup"><span data-stu-id="7bf3f-120">Add hello following *using* directives toohello `TablesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Table;
    ```

### <a name="create-a-model-class"></a><span data-ttu-id="7bf3f-121">Creare una classe di modello</span><span class="sxs-lookup"><span data-stu-id="7bf3f-121">Create a model class</span></span>

<span data-ttu-id="7bf3f-122">Molti degli esempi di hello in questo articolo usa una **TableEntity**-derivata denominata **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-122">Many of hello examples in this article use a **TableEntity**-derived class called **CustomerEntity**.</span></span> <span data-ttu-id="7bf3f-123">Hello passaggi consentono di eseguire la dichiarazione di questa classe come classe di modello:</span><span class="sxs-lookup"><span data-stu-id="7bf3f-123">hello following steps guide you through declaring this class as a model class:</span></span>

1. <span data-ttu-id="7bf3f-124">In hello **Esplora**, fare doppio clic su **modelli**, selezionare il menu di scelta rapida hello **Aggiungi -> classe**.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-124">In hello **Solution Explorer**, right-click **Models**, and, from hello context menu, select **Add->Class**.</span></span>

1. <span data-ttu-id="7bf3f-125">In hello **Aggiungi nuovo elemento** finestra di dialogo, nome classe hello, **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-125">On hello **Add New Item** dialog, name hello class, **CustomerEntity**.</span></span>

1. <span data-ttu-id="7bf3f-126">Aprire hello `CustomerEntity.cs` file e aggiungere il seguente hello **utilizzando** direttiva:</span><span class="sxs-lookup"><span data-stu-id="7bf3f-126">Open hello `CustomerEntity.cs` file, and add hello following **using** directive:</span></span>

    ```csharp
    using Microsoft.WindowsAzure.Storage.Table;
    ```

1. <span data-ttu-id="7bf3f-127">Modificare la classe hello in modo che, al termine, la classe hello è dichiarata come hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-127">Modify hello class so that, when finished, hello class is declared as in hello following code.</span></span> <span data-ttu-id="7bf3f-128">classe Hello dichiara una classe di entità denominata **CustomerEntity** che utilizza hello nome del cliente come chiave di riga hello e il cognome come chiave di partizione hello.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-128">hello class declares an entity class called **CustomerEntity** that uses hello customer's first name as hello row key and last name as hello partition key.</span></span>

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

## <a name="create-a-table"></a><span data-ttu-id="7bf3f-129">Creare una tabella</span><span class="sxs-lookup"><span data-stu-id="7bf3f-129">Create a table</span></span>

<span data-ttu-id="7bf3f-130">Hello passaggi seguenti viene illustrato come toocreate una tabella:</span><span class="sxs-lookup"><span data-stu-id="7bf3f-130">hello following steps illustrate how toocreate a table:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="7bf3f-131">Questa sezione si presuppone di aver completato i passaggi di hello in [configurare un ambiente di sviluppo hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="7bf3f-131">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="7bf3f-132">Aprire hello `TablesController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-132">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="7bf3f-133">Aggiungere un metodo denominato **CreateTable** che restituisce un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-133">Add a method called **CreateTable** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateTable()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="7bf3f-134">All'interno di hello **CreateTable** (metodo), ottenere un **CloudStorageAccount** oggetto che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-134">Within hello **CreateTable** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="7bf3f-135">Esempio di codice seguente di hello utilizzare tooget hello archiviazione stringa e l'archiviazione account informazioni di connessione di configurazione del servizio Azure hello: (modifica  *&lt;storage-account-name >* toohello nome hello archiviazione di Azure account che si accede.)</span><span class="sxs-lookup"><span data-stu-id="7bf3f-135">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="7bf3f-136">Ottenere un oggetto **CloudTableClient** che rappresenta un client del servizio tabelle.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-136">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="7bf3f-137">Ottenere un **CloudTable** oggetto che rappresenta un nome di riferimento toohello tabella desiderata.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-137">Get a **CloudTable** object that represents a reference toohello desired table name.</span></span> <span data-ttu-id="7bf3f-138">Hello **CloudTableClient.GetTableReference** metodo non effettuare una richiesta nel servizio di archiviazione tabella.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-138">hello **CloudTableClient.GetTableReference** method does not make a request against table storage.</span></span> <span data-ttu-id="7bf3f-139">tabella hello esista o meno, viene restituito il riferimento di Hello.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-139">hello reference is returned whether or not hello table exists.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="7bf3f-140">Chiamare hello **CloudTable.CreateIfNotExists** tabella dei metodi toocreate hello se non esiste ancora.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-140">Call hello **CloudTable.CreateIfNotExists** method toocreate hello table if it does not yet exist.</span></span> <span data-ttu-id="7bf3f-141">Hello **CloudTable.CreateIfNotExists** restituisce **true** se non esiste nella tabella hello e viene creata correttamente.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-141">hello **CloudTable.CreateIfNotExists** method returns **true** if hello table does not exist, and is successfully created.</span></span> <span data-ttu-id="7bf3f-142">In caso contrario, viene restituito **false**.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-142">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = table.CreateIfNotExists();
    ```

1. <span data-ttu-id="7bf3f-143">Hello aggiornamento **ViewBag** con nome hello hello table.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-143">Update hello **ViewBag** with hello name of hello table.</span></span>

    ```csharp
    ViewBag.TableName = table.Name;
    ```

1. <span data-ttu-id="7bf3f-144">In hello **Esplora**, espandere hello **viste** cartella, fare doppio clic su **tabelle**e quindi scegliere il menu di scelta rapida hello **Aggiungi -> Vista**.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-144">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="7bf3f-145">In hello **Aggiungi visualizzazione** finestra di dialogo immettere **CreateTable** per nome della visualizzazione hello e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-145">On hello **Add View** dialog, enter **CreateTable** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="7bf3f-146">Aprire `CreateTable.cshtml`e modificarlo in modo che risulti simile hello frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="7bf3f-146">Open `CreateTable.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Table";
    }
    
    <h2>Create Table results</h2>

    Creation of @ViewBag.TableName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="7bf3f-147">In hello **Esplora**, espandere hello **viste -> Shared** cartella e aprire `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-147">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="7bf3f-148">Dopo aver hello ultimo **HTML. ActionLink**, aggiungere il seguente hello **HTML. ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="7bf3f-148">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create table", "CreateTable", "Tables")</li>
    ```

1. <span data-ttu-id="7bf3f-149">Eseguire un'applicazione hello e selezionare **crea una tabella** toosee risultati simile toohello cattura di schermata seguente:</span><span class="sxs-lookup"><span data-stu-id="7bf3f-149">Run hello application, and select **Create table** toosee results similar toohello following screen shot:</span></span>
  
    ![Crea tabella](./media/vs-storage-aspnet-getting-started-tables/create-table-results.png)

    <span data-ttu-id="7bf3f-151">Come accennato in precedenza, hello **CloudTable.CreateIfNotExists** restituisce **true** solo quando la tabella hello non esiste e viene creata.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-151">As mentioned previously, hello **CloudTable.CreateIfNotExists** method returns **true** only when hello table doesn't exist and is created.</span></span> <span data-ttu-id="7bf3f-152">Pertanto, se si esegue l'applicazione hello quando hello tabella esiste, il metodo di hello restituisce **false**.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-152">Therefore, if you run hello app when hello table exists, hello method returns **false**.</span></span> <span data-ttu-id="7bf3f-153">app hello toorun più volte, è necessario eliminare la tabella hello prima di eseguire nuovamente l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-153">toorun hello app multiple times, you must delete hello table before running hello app again.</span></span> <span data-ttu-id="7bf3f-154">Eliminazione della tabella hello possono essere eseguita tramite hello **CloudTable.Delete** metodo.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-154">Deleting hello table can be done via hello **CloudTable.Delete** method.</span></span> <span data-ttu-id="7bf3f-155">È anche possibile eliminare tabella hello utilizzando hello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) o hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="7bf3f-155">You can also delete hello table using hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="7bf3f-156">Aggiungere una tabella tooa entità</span><span class="sxs-lookup"><span data-stu-id="7bf3f-156">Add an entity tooa table</span></span>

<span data-ttu-id="7bf3f-157">*Entità* mapping tooC\# oggetti usando una classe personalizzata derivata da **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-157">*Entities* map tooC\# objects by using a custom class derived from **TableEntity**.</span></span> <span data-ttu-id="7bf3f-158">tooadd tabella tooa un'entità, creare una classe che definisce le proprietà di hello dell'entità.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-158">tooadd an entity tooa table, create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="7bf3f-159">In questa sezione, verrà visualizzato come una classe di entità che utilizza toodefine hello nome del cliente come chiave di riga hello e il cognome come chiave di partizione hello.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-159">In this section, you'll see how toodefine an entity class that uses hello customer's first name as hello row key and last name as hello partition key.</span></span> <span data-ttu-id="7bf3f-160">Insieme, di partizione e chiave di riga identificano entità hello nella tabella di hello.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-160">Together, an entity's partition and row key uniquely identify hello entity in hello table.</span></span> <span data-ttu-id="7bf3f-161">Le query su entità con la stessa chiave di partizione vengono eseguite più rapidamente di quelle con chiavi di partizione diverse, tuttavia l'uso di chiavi di partizione diverse assicura una maggiore scalabilità delle operazioni parallele.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-161">Entities with the same partition key can be queried faster than entities with different partition keys, but using diverse partition keys allows for greater scalability of parallel operations.</span></span> <span data-ttu-id="7bf3f-162">Per qualsiasi proprietà che devono essere archiviati nel servizio tabelle hello, proprietà hello deve essere una proprietà pubblica di un tipo supportato che espone sia l'impostazione e recupero di valori.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-162">For any property that should be stored in hello table service, hello property must be a public property of a supported type that exposes both setting and retrieving values.</span></span>
<span data-ttu-id="7bf3f-163">classe di entità Hello *deve* dichiarare un costruttore senza parametri pubblico.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-163">hello entity class *must* declare a public parameter-less constructor.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="7bf3f-164">Questa sezione si presuppone di aver completato i passaggi di hello in [configurare un ambiente di sviluppo hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="7bf3f-164">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment).</span></span>

1. <span data-ttu-id="7bf3f-165">Aprire hello `TablesController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-165">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="7bf3f-166">Aggiungere hello dopo la direttiva in modo che hello codice hello `TablesController.cs` file può accedere hello **CustomerEntity** classe:</span><span class="sxs-lookup"><span data-stu-id="7bf3f-166">Add hello following directive so that hello code in hello `TablesController.cs` file can access hello **CustomerEntity** class:</span></span>

    ```csharp
    using StorageAspnet.Models;
    ```

1. <span data-ttu-id="7bf3f-167">Aggiungere un metodo denominato **AddEntity** che restituisce un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-167">Add a method called **AddEntity** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="7bf3f-168">All'interno di hello **AddEntity** (metodo), ottenere un **CloudStorageAccount** oggetto che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-168">Within hello **AddEntity** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="7bf3f-169">Esempio di codice seguente di hello utilizzare tooget hello archiviazione stringa e l'archiviazione account informazioni di connessione di configurazione del servizio Azure hello: (modifica  *&lt;storage-account-name >* toohello nome hello archiviazione di Azure account che si accede.)</span><span class="sxs-lookup"><span data-stu-id="7bf3f-169">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="7bf3f-170">Ottenere un oggetto **CloudTableClient** che rappresenta un client del servizio tabelle.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-170">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="7bf3f-171">Ottenere un **CloudTable** oggetto che rappresenta un toowhich tabella toohello di riferimento si intende una nuova entità di tooadd hello.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-171">Get a **CloudTable** object that represents a reference toohello table toowhich you are going tooadd hello new entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="7bf3f-172">Creare e inizializzare hello **CustomerEntity** classe.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-172">Instantiate and initialize hello **CustomerEntity** class.</span></span>

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    ```

1. <span data-ttu-id="7bf3f-173">Creare un **TableOperation** che inserisce l'entità customer hello.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-173">Create a **TableOperation** object that inserts hello customer entity.</span></span>

    ```csharp
    TableOperation insertOperation = TableOperation.Insert(customer1);
    ```

1. <span data-ttu-id="7bf3f-174">Eseguire l'operazione di inserimento hello dal chiamante hello **CloudTable.Execute** metodo.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-174">Execute hello insert operation by calling hello **CloudTable.Execute** method.</span></span> <span data-ttu-id="7bf3f-175">È possibile verificare il risultato di hello dell'operazione di hello controllando hello **TableResult.HttpStatusCode** proprietà.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-175">You can verify hello result of hello operation by inspecting hello **TableResult.HttpStatusCode** property.</span></span> <span data-ttu-id="7bf3f-176">Un codice di stato di 2xx indica l'azione di hello richiesta dal client hello è stato elaborato correttamente.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-176">A status code of 2xx indicates hello action requested by hello client was processed successfully.</span></span> <span data-ttu-id="7bf3f-177">Ad esempio, ha esito positivo le operazioni di inserimento della nuova entità risultato in un codice di stato HTTP 204, vale a dire che è stata elaborata correttamente operazione hello e server hello non ha restituito alcun contenuto.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-177">For example, successful insertions of new entities results in an HTTP status code of 204, meaning that hello operation was successfully processed and hello server did not return any content.</span></span>

    ```csharp
    TableResult result = table.Execute(insertOperation);
    ```

1. <span data-ttu-id="7bf3f-178">Hello aggiornamento **ViewBag** con il nome di tabella hello e hello risultati dell'operazione di inserimento hello.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-178">Update hello **ViewBag** with hello table name, and hello results of hello insert operation.</span></span>

    ```csharp
    ViewBag.TableName = table.Name;
    ViewBag.Result = result.HttpStatusCode;
    ```

1. <span data-ttu-id="7bf3f-179">In hello **Esplora**, espandere hello **viste** cartella, fare doppio clic su **tabelle**e quindi scegliere il menu di scelta rapida hello **Aggiungi -> Vista**.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-179">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="7bf3f-180">In hello **Aggiungi visualizzazione** finestra di dialogo immettere **AddEntity** per nome della visualizzazione hello e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-180">On hello **Add View** dialog, enter **AddEntity** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="7bf3f-181">Aprire `AddEntity.cshtml`e modificarlo in modo che risulti simile hello frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="7bf3f-181">Open `AddEntity.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add entity";
    }
    
    <h2>Add entity results</h2>

    Insert of entity into @ViewBag.TableName @(ViewBag.Result == 204 ? "succeeded" : "failed")
    ```
1. <span data-ttu-id="7bf3f-182">In hello **Esplora**, espandere hello **viste -> Shared** cartella e aprire `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-182">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="7bf3f-183">Dopo aver hello ultimo **HTML. ActionLink**, aggiungere il seguente hello **HTML. ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="7bf3f-183">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add entity", "AddEntity", "Tables")</li>
    ```

1. <span data-ttu-id="7bf3f-184">Eseguire un'applicazione hello e selezionare **aggiungere entità** toosee risultati simile toohello cattura di schermata seguente:</span><span class="sxs-lookup"><span data-stu-id="7bf3f-184">Run hello application, and select **Add entity** toosee results similar toohello following screen shot:</span></span>
  
    ![Aggiungi entità](./media/vs-storage-aspnet-getting-started-tables/add-entity-results.png)

    <span data-ttu-id="7bf3f-186">È possibile verificare che sia stato aggiunto entità hello seguendo i passaggi di hello nella sezione hello, [ottenere una singola entità](#get-a-single-entity).</span><span class="sxs-lookup"><span data-stu-id="7bf3f-186">You can verify that hello entity was added by following hello steps in hello section, [Get a single entity](#get-a-single-entity).</span></span> <span data-ttu-id="7bf3f-187">È inoltre possibile utilizzare hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview tutti hello entità per le tabelle.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-187">You can also use hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview all hello entities for your tables.</span></span>

## <a name="add-a-batch-of-entities-tooa-table"></a><span data-ttu-id="7bf3f-188">Aggiungere un batch di tabella tooa entità</span><span class="sxs-lookup"><span data-stu-id="7bf3f-188">Add a batch of entities tooa table</span></span>

<span data-ttu-id="7bf3f-189">In aggiunta toobeing in grado di troppo[aggiungere una tabella tooa entità uno alla volta](#add-an-entity-to-a-table), è inoltre possibile aggiungere entità nel batch.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-189">In addition toobeing able too[add an entity tooa table one at a time](#add-an-entity-to-a-table), you can also add entities in batch.</span></span> <span data-ttu-id="7bf3f-190">Aggiunta di entità in batch riduce il numero di hello di round trip tra il codice e hello servizio tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-190">Adding entities in batch reduces hello number of round-trips between your code and hello Azure table service.</span></span> <span data-ttu-id="7bf3f-191">Hello alla procedura seguente viene illustrato come tooadd tooa di più entità di tabella con un'operazione di inserimento singolo:</span><span class="sxs-lookup"><span data-stu-id="7bf3f-191">hello following steps illustrate how tooadd multiple entities tooa table with a single insert operation:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="7bf3f-192">Questa sezione si presuppone di aver completato i passaggi di hello in [configurare un ambiente di sviluppo hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="7bf3f-192">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment).</span></span>

1. <span data-ttu-id="7bf3f-193">Aprire hello `TablesController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-193">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="7bf3f-194">Aggiungere un metodo denominato **AddEntities** che restituisce un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-194">Add a method called **AddEntities** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddEntities()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="7bf3f-195">All'interno di hello **AddEntities** (metodo), ottenere un **CloudStorageAccount** oggetto che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-195">Within hello **AddEntities** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="7bf3f-196">Esempio di codice seguente di hello utilizzare tooget hello archiviazione stringa e l'archiviazione account informazioni di connessione di configurazione del servizio Azure hello: (modifica  *&lt;storage-account-name >* toohello nome hello archiviazione di Azure account che si accede.)</span><span class="sxs-lookup"><span data-stu-id="7bf3f-196">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="7bf3f-197">Ottenere un oggetto **CloudTableClient** che rappresenta un client del servizio tabelle.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-197">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="7bf3f-198">Ottenere un **CloudTable** oggetto che rappresenta un toowhich tabella toohello di riferimento sono nuove entità corso tooadd hello.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-198">Get a **CloudTable** object that represents a reference toohello table toowhich you are going tooadd hello new entities.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="7bf3f-199">Creare un'istanza di alcuni oggetti di clienti in base a hello **CustomerEntity** classe presentati nella sezione hello modello [aggiungere una tabella tooa entità](#add-an-entity-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="7bf3f-199">Instantiate some customer objects based on hello **CustomerEntity** model class presented in hello section, [Add an entity tooa table](#add-an-entity-to-a-table).</span></span>

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
    customer1.Email = "Jeff@contoso.com";

    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.Email = "Ben@contoso.com";
    ```

1. <span data-ttu-id="7bf3f-200">Ottenere un oggetto **TableBatchOperation**.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-200">Get a **TableBatchOperation** object.</span></span>

    ```csharp
    TableBatchOperation batchOperation = new TableBatchOperation();
    ```

1. <span data-ttu-id="7bf3f-201">Aggiungere l'oggetto dell'operazione di inserimento batch toohello entità.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-201">Add entities toohello batch insert operation object.</span></span>

    ```csharp
    batchOperation.Insert(customer1);
    batchOperation.Insert(customer2);
    ```

1. <span data-ttu-id="7bf3f-202">Eseguire l'operazione di inserimento batch hello dal chiamante hello **CloudTable.ExecuteBatch** metodo.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-202">Execute hello batch insert operation by calling hello **CloudTable.ExecuteBatch** method.</span></span>   

    ```csharp
    IList<TableResult> results = table.ExecuteBatch(batchOperation);
    ```

1. <span data-ttu-id="7bf3f-203">Hello **CloudTable.ExecuteBatch** il metodo restituisce un elenco di **TableResult** oggetti in cui ogni **TableResult** oggetto può essere esaminato toodetermine hello riuscita o meno di ogni singola operazione.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-203">hello **CloudTable.ExecuteBatch** method returns a list of **TableResult** objects where each **TableResult** object can be examined toodetermine hello success or failure of each individual operation.</span></span> <span data-ttu-id="7bf3f-204">In questo esempio hello elenco tooa visualizzazione passata e consente di visualizzare i risultati di hello di ogni operazione visualizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-204">For this example, pass hello list tooa view and let hello view display hello results of each operation.</span></span> 
 
    ```csharp
    return View(results);
    ```

1. <span data-ttu-id="7bf3f-205">In hello **Esplora**, espandere hello **viste** cartella, fare doppio clic su **tabelle**e quindi scegliere il menu di scelta rapida hello **Aggiungi -> Vista**.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-205">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="7bf3f-206">In hello **Aggiungi visualizzazione** finestra di dialogo immettere **AddEntities** per nome della visualizzazione hello e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-206">On hello **Add View** dialog, enter **AddEntities** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="7bf3f-207">Aprire `AddEntities.cshtml`e modificarlo in modo che risulti simile hello seguente.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-207">Open `AddEntities.cshtml`, and modify it so that it looks like hello following.</span></span>

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

1. <span data-ttu-id="7bf3f-208">In hello **Esplora**, espandere hello **viste -> Shared** cartella e aprire `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-208">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="7bf3f-209">Dopo aver hello ultimo **HTML. ActionLink**, aggiungere il seguente hello **HTML. ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="7bf3f-209">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add entities", "AddEntities", "Tables")</li>
    ```

1. <span data-ttu-id="7bf3f-210">Eseguire un'applicazione hello e selezionare **aggiungere entità** toosee risultati simile toohello cattura di schermata seguente:</span><span class="sxs-lookup"><span data-stu-id="7bf3f-210">Run hello application, and select **Add entities** toosee results similar toohello following screen shot:</span></span>
  
    ![Aggiungi entità](./media/vs-storage-aspnet-getting-started-tables/add-entities-results.png)

    <span data-ttu-id="7bf3f-212">È possibile verificare che sia stato aggiunto entità hello seguendo i passaggi di hello nella sezione hello, [ottenere una singola entità](#get-a-single-entity).</span><span class="sxs-lookup"><span data-stu-id="7bf3f-212">You can verify that hello entity was added by following hello steps in hello section, [Get a single entity](#get-a-single-entity).</span></span> <span data-ttu-id="7bf3f-213">È inoltre possibile utilizzare hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview tutti hello entità per le tabelle.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-213">You can also use hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview all hello entities for your tables.</span></span>

## <a name="get-a-single-entity"></a><span data-ttu-id="7bf3f-214">Ottenere una singola entità</span><span class="sxs-lookup"><span data-stu-id="7bf3f-214">Get a single entity</span></span>

<span data-ttu-id="7bf3f-215">In questa sezione viene illustrato come una singola entità da una tabella utilizzando tooget hello chiave di riga e la chiave di partizione dell'entità.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-215">This section illustrates how tooget a single entity from a table using hello entity's row key and partition key.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="7bf3f-216">Questa sezione si presuppone di aver completato i passaggi di hello in [configurare un ambiente di sviluppo hello](#set-up-the-development-environment)e utilizza i dati di [aggiungere un batch di tabella tooa entità](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="7bf3f-216">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="7bf3f-217">Aprire hello `TablesController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-217">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="7bf3f-218">Aggiungere un metodo denominato **GetSingle** che restituisce un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-218">Add a method called **GetSingle** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetSingle()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="7bf3f-219">All'interno di hello **GetSingle** (metodo), ottenere un **CloudStorageAccount** oggetto che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-219">Within hello **GetSingle** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="7bf3f-220">Esempio di codice seguente di hello utilizzare tooget hello archiviazione stringa e l'archiviazione account informazioni di connessione di configurazione del servizio Azure hello: (modifica  *&lt;storage-account-name >* toohello nome hello archiviazione di Azure account che si accede.)</span><span class="sxs-lookup"><span data-stu-id="7bf3f-220">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="7bf3f-221">Ottenere un oggetto **CloudTableClient** che rappresenta un client del servizio tabelle.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-221">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="7bf3f-222">Ottenere un **CloudTable** oggetto che rappresenta una tabella di riferimento toohello da cui si desidera recuperare entità hello.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-222">Get a **CloudTable** object that represents a reference toohello table from which you are retrieving hello entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="7bf3f-223">Creare un oggetto operazione di recupero che accetta un oggetto entità derivato da **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-223">Create a retrieve operation object that takes an entity object derived from **TableEntity**.</span></span> <span data-ttu-id="7bf3f-224">il primo parametro Hello è hello *partitionKey*, e il secondo parametro hello è hello *rowKey*.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-224">hello first parameter is hello *partitionKey*, and hello second parameter is hello *rowKey*.</span></span> <span data-ttu-id="7bf3f-225">Utilizzando hello **CustomerEntity** classe e i dati presentati nella sezione hello [aggiungere un batch di tabella tooa entità](#add-a-batch-of-entities-to-a-table), hello seguenti tabella query hello frammento di codice per un **CustomerEntity** entità con un *partitionKey* valore "Smith" e un *rowKey* valore di "Ben":</span><span class="sxs-lookup"><span data-stu-id="7bf3f-225">Using hello **CustomerEntity** class and data presented in hello section [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table), hello following code snippet queries hello table for a **CustomerEntity** entity with a *partitionKey* value of "Smith" and a *rowKey* value of "Ben":</span></span>

    ```csharp
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");
    ```

1. <span data-ttu-id="7bf3f-226">Eseguire l'operazione di recupero hello.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-226">Execute hello retrieve operation.</span></span>   

    ```csharp
    TableResult result = table.Execute(retrieveOperation);
    ```

1. <span data-ttu-id="7bf3f-227">Passare a visualizzazione toohello hello dei risultati per la visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-227">Pass hello result toohello view for display.</span></span>

    ```csharp
    return View(result);
    ```

1. <span data-ttu-id="7bf3f-228">In hello **Esplora**, espandere hello **viste** cartella, fare doppio clic su **tabelle**e quindi scegliere il menu di scelta rapida hello **Aggiungi -> Vista**.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-228">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="7bf3f-229">In hello **Aggiungi visualizzazione** finestra di dialogo immettere **GetSingle** per nome della visualizzazione hello e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-229">On hello **Add View** dialog, enter **GetSingle** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="7bf3f-230">Aprire `GetSingle.cshtml`e modificarlo in modo che risulti simile hello frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="7bf3f-230">Open `GetSingle.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

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

1. <span data-ttu-id="7bf3f-231">In hello **Esplora**, espandere hello **viste -> Shared** cartella e aprire `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-231">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="7bf3f-232">Dopo aver hello ultimo **HTML. ActionLink**, aggiungere il seguente hello **HTML. ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="7bf3f-232">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get single", "GetSingle", "Tables")</li>
    ```

1. <span data-ttu-id="7bf3f-233">Eseguire un'applicazione hello e selezionare **ottenere singolo** toosee risultati simile toohello cattura di schermata seguente:</span><span class="sxs-lookup"><span data-stu-id="7bf3f-233">Run hello application, and select **Get Single** toosee results similar toohello following screen shot:</span></span>
  
    ![Get single](./media/vs-storage-aspnet-getting-started-tables/get-single-results.png)

## <a name="get-all-entities-in-a-partition"></a><span data-ttu-id="7bf3f-235">Recuperare tutte le entità di una partizione</span><span class="sxs-lookup"><span data-stu-id="7bf3f-235">Get all entities in a partition</span></span>

<span data-ttu-id="7bf3f-236">Come indicato nella sezione hello [aggiungere una tabella di entità tooa](#add-an-entity-to-a-table), combinazione di hello di una partizione e una chiave di riga identifica in modo univoco un'entità in una tabella.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-236">As mentioned in hello section, [Add an entity tooa table](#add-an-entity-to-a-table), hello combination of a partition and a row key uniquely identify an entity in a table.</span></span> <span data-ttu-id="7bf3f-237">Le query su entità con la stessa chiave di partizione vengono eseguite più rapidamente di quelle con chiavi di partizione diverse.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-237">Entities with the same partition key can be queried faster than entities with different partition keys.</span></span> <span data-ttu-id="7bf3f-238">In questa sezione viene illustrato come tooquery una tabella per tutte le entità hello da una partizione specificata.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-238">This section illustrates how tooquery a table for all hello entities from a specified partition.</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="7bf3f-239">Questa sezione si presuppone di aver completato i passaggi di hello in [configurare un ambiente di sviluppo hello](#set-up-the-development-environment)e utilizza i dati di [aggiungere un batch di tabella tooa entità](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="7bf3f-239">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="7bf3f-240">Aprire hello `TablesController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-240">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="7bf3f-241">Aggiungere un metodo denominato **GetPartition** che restituisce un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-241">Add a method called **GetPartition** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetPartition()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="7bf3f-242">All'interno di hello **GetPartition** (metodo), ottenere un **CloudStorageAccount** oggetto che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-242">Within hello **GetPartition** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="7bf3f-243">Esempio di codice seguente di hello utilizzare tooget hello archiviazione stringa e l'archiviazione account informazioni di connessione di configurazione del servizio Azure hello: (modifica  *&lt;storage-account-name >* toohello nome hello archiviazione di Azure account che si accede.)</span><span class="sxs-lookup"><span data-stu-id="7bf3f-243">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="7bf3f-244">Ottenere un oggetto **CloudTableClient** che rappresenta un client del servizio tabelle.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-244">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="7bf3f-245">Ottenere un **CloudTable** oggetto che rappresenta una tabella di riferimento toohello da cui si desidera recuperare entità hello.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-245">Get a **CloudTable** object that represents a reference toohello table from which you are retrieving hello entities.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="7bf3f-246">Creare un'istanza di un **TableQuery** oggetto che specifica la query hello in hello **dove** clausola.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-246">Instantiate a **TableQuery** object specifying hello query in hello **Where** clause.</span></span> <span data-ttu-id="7bf3f-247">Utilizzando hello **CustomerEntity** classe e i dati presentati nella sezione hello [aggiungere un batch di tabella tooa entità](#add-a-batch-of-entities-to-a-table), tabella di hello frammento query per tutte le entità di codice seguente di hello dove hello  **PartitionKey** (cognome del cliente) ha un valore di "Smith":</span><span class="sxs-lookup"><span data-stu-id="7bf3f-247">Using hello **CustomerEntity** class and data presented in hello section [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table), hello following code snippet queries hello table for a all entities where hello **PartitionKey** (customer's last name) has a value of "Smith":</span></span>

    ```csharp
    TableQuery<CustomerEntity> query = 
        new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));
    ```

1. <span data-ttu-id="7bf3f-248">All'interno di un ciclo, chiamare hello **CloudTable.ExecuteQuerySegmented** passando l'oggetto query hello è creata un'istanza nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-248">Within a loop, call hello **CloudTable.ExecuteQuerySegmented** method passing hello query object you instantiated in hello previous step.</span></span>  <span data-ttu-id="7bf3f-249">Hello **CloudTable.ExecuteQuerySegmented** metodo restituisce un **TableContinuationToken** - oggetto quando **null** -indica che non sono più alcuna entità tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-249">hello **CloudTable.ExecuteQuerySegmented** method returns a **TableContinuationToken** object that - when **null** - indicates that there are no more entities tooretrieve.</span></span> <span data-ttu-id="7bf3f-250">Nel ciclo di hello, utilizzare un altro ciclo tooiterate hello le entità restituita.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-250">Within hello loop, use another loop tooiterate over hello returned entities.</span></span> <span data-ttu-id="7bf3f-251">Nell'esempio di codice seguente di hello, ogni entità restituita viene aggiunta tooa elenco.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-251">In hello following code example, each returned entity is added tooa list.</span></span> <span data-ttu-id="7bf3f-252">Una volta hello ciclo termina, elenco hello viene passato tooa visualizzazione per la visualizzazione:</span><span class="sxs-lookup"><span data-stu-id="7bf3f-252">Once hello loop ends, hello list is passed tooa view for display:</span></span> 

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

1. <span data-ttu-id="7bf3f-253">In hello **Esplora**, espandere hello **viste** cartella, fare doppio clic su **tabelle**e quindi scegliere il menu di scelta rapida hello **Aggiungi -> Vista**.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-253">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="7bf3f-254">In hello **Aggiungi visualizzazione** finestra di dialogo immettere **GetPartition** per nome della visualizzazione hello e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-254">On hello **Add View** dialog, enter **GetPartition** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="7bf3f-255">Aprire `GetPartition.cshtml`e modificarlo in modo che risulti simile hello frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="7bf3f-255">Open `GetPartition.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

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

1. <span data-ttu-id="7bf3f-256">In hello **Esplora**, espandere hello **viste -> Shared** cartella e aprire `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-256">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="7bf3f-257">Dopo aver hello ultimo **HTML. ActionLink**, aggiungere il seguente hello **HTML. ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="7bf3f-257">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get partition", "GetPartition", "Tables")</li>
    ```

1. <span data-ttu-id="7bf3f-258">Eseguire un'applicazione hello e selezionare **ottenere partizione** toosee risultati simile toohello cattura di schermata seguente:</span><span class="sxs-lookup"><span data-stu-id="7bf3f-258">Run hello application, and select **Get Partition** toosee results similar toohello following screen shot:</span></span>
  
    ![Get Partition](./media/vs-storage-aspnet-getting-started-tables/get-partition-results.png)

## <a name="delete-an-entity"></a><span data-ttu-id="7bf3f-260">Eliminare un'entità</span><span class="sxs-lookup"><span data-stu-id="7bf3f-260">Delete an entity</span></span>

<span data-ttu-id="7bf3f-261">In questa sezione viene illustrato come toodelete un'entità da una tabella.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-261">This section illustrates how toodelete an entity from a table.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="7bf3f-262">Questa sezione si presuppone di aver completato i passaggi di hello in [configurare un ambiente di sviluppo hello](#set-up-the-development-environment)e utilizza i dati di [aggiungere un batch di tabella tooa entità](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="7bf3f-262">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="7bf3f-263">Aprire hello `TablesController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-263">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="7bf3f-264">Aggiungere un metodo denominato **DeleteEntity** che restituisce un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-264">Add a method called **DeleteEntity** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="7bf3f-265">All'interno di hello **DeleteEntity** (metodo), ottenere un **CloudStorageAccount** oggetto che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-265">Within hello **DeleteEntity** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="7bf3f-266">Esempio di codice seguente di hello utilizzare tooget hello archiviazione stringa e l'archiviazione account informazioni di connessione di configurazione del servizio Azure hello: (modifica  *&lt;storage-account-name >* toohello nome hello archiviazione di Azure account che si accede.)</span><span class="sxs-lookup"><span data-stu-id="7bf3f-266">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="7bf3f-267">Ottenere un oggetto **CloudTableClient** che rappresenta un client del servizio tabelle.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-267">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="7bf3f-268">Ottenere un **CloudTable** oggetto che rappresenta una tabella di riferimento toohello da cui si sta eliminando entità hello.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-268">Get a **CloudTable** object that represents a reference toohello table from which you are deleting hello entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="7bf3f-269">Creare un oggetto operazione di eliminazione che accetta un oggetto entità derivato da **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-269">Create a delete operation object that takes an entity object derived from **TableEntity**.</span></span> <span data-ttu-id="7bf3f-270">In questo caso, utilizziamo hello **CustomerEntity** classe e i dati presentati nella sezione hello [aggiungere un batch di tabella tooa entità](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="7bf3f-270">In this case, we use hello **CustomerEntity** class and data presented in hello section [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> <span data-ttu-id="7bf3f-271">Hello dell'entità **ETag** deve essere impostato tooa valido.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-271">hello entity's **ETag** must be set tooa valid value.</span></span>  

    ```csharp
    TableOperation deleteOperation = 
        TableOperation.Delete(new CustomerEntity("Smith", "Ben") { ETag = "*" } );
    ```

1. <span data-ttu-id="7bf3f-272">Eseguire l'operazione di eliminazione di hello.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-272">Execute hello delete operation.</span></span>   

    ```csharp
    TableResult result = table.Execute(deleteOperation);
    ```

1. <span data-ttu-id="7bf3f-273">Passare a visualizzazione toohello hello dei risultati per la visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-273">Pass hello result toohello view for display.</span></span>

    ```csharp
    return View(result);
    ```

1. <span data-ttu-id="7bf3f-274">In hello **Esplora**, espandere hello **viste** cartella, fare doppio clic su **tabelle**e quindi scegliere il menu di scelta rapida hello **Aggiungi -> Vista**.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-274">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="7bf3f-275">In hello **Aggiungi visualizzazione** finestra di dialogo immettere **DeleteEntity** per nome della visualizzazione hello e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-275">On hello **Add View** dialog, enter **DeleteEntity** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="7bf3f-276">Aprire `DeleteEntity.cshtml`e modificarlo in modo che risulti simile hello frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="7bf3f-276">Open `DeleteEntity.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

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

1. <span data-ttu-id="7bf3f-277">In hello **Esplora**, espandere hello **viste -> Shared** cartella e aprire `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-277">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="7bf3f-278">Dopo aver hello ultimo **HTML. ActionLink**, aggiungere il seguente hello **HTML. ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="7bf3f-278">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete entity", "DeleteEntity", "Tables")</li>
    ```

1. <span data-ttu-id="7bf3f-279">Eseguire un'applicazione hello e selezionare **eliminare entità** toosee risultati simile toohello cattura di schermata seguente:</span><span class="sxs-lookup"><span data-stu-id="7bf3f-279">Run hello application, and select **Delete entity** toosee results similar toohello following screen shot:</span></span>
  
    ![Get single](./media/vs-storage-aspnet-getting-started-tables/delete-entity-results.png)

## <a name="next-steps"></a><span data-ttu-id="7bf3f-281">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7bf3f-281">Next steps</span></span>
<span data-ttu-id="7bf3f-282">Consente di visualizzare altre toolearn di guide di funzionalità sulle opzioni aggiuntive per l'archiviazione dei dati in Azure.</span><span class="sxs-lookup"><span data-stu-id="7bf3f-282">View more feature guides toolearn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="7bf3f-283">Introduzione all'Archiviazione BLOB di Azure e ai Servizi connessi di Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="7bf3f-283">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](../storage/vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="7bf3f-284">Introduzione all'archiviazione code di Azure e ai Servizi connessi di Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="7bf3f-284">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>](../storage/vs-storage-aspnet-getting-started-queues.md)
