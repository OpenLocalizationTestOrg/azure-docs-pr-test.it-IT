---
title: Introduzione all'archiviazione tabelle di Azure e a Servizi connessi di Visual Studio (ASP.NET) | Documentazione Microsoft
description: Informazioni su come iniziare a usare il servizio di archiviazione tabelle in un progetto ASP.NET in Visual Studio dopo aver eseguito la connessione a un account di archiviazione con Servizi connessi di Visual Studio
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
ms.openlocfilehash: 32a57e77bf6fe3cff88b9d6772ede9e6669ec75f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-table-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="bfb8d-103">Introduzione all'archiviazione tabelle di Azure e a Servizi connessi di Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="bfb8d-103">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="bfb8d-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="bfb8d-104">Overview</span></span>

<span data-ttu-id="bfb8d-105">L’archiviazione tabelle di Azure consente di archiviare grandi quantità di dati strutturati.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-105">Azure Table storage enables you to store large amounts of structured data.</span></span> <span data-ttu-id="bfb8d-106">Il servizio è un datastore NoSQL che accetta chiamate autenticate dall'interno e dall'esterno del cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-106">The service is a NoSQL datastore that accepts authenticated calls from inside and outside the Azure cloud.</span></span> <span data-ttu-id="bfb8d-107">Le tabelle di Azure sono ideali per l'archiviazione di dati strutturati non relazionali.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-107">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="bfb8d-108">Questa esercitazione illustra come scrivere codice ASP.NET per alcuni scenari comuni usando le entità di archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-108">This tutorial shows how to write ASP.NET code for some common scenarios using Azure table storage entities.</span></span> <span data-ttu-id="bfb8d-109">Questi scenari includono la creazione di una tabella, l'aggiunta, la creazione di query ed eliminazione di entità di tabella.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-109">These scenarios include creating a table, and adding, querying, and deleting table entities.</span></span> 

##<a name="prerequisites"></a><span data-ttu-id="bfb8d-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="bfb8d-110">Prerequisites</span></span>

* [<span data-ttu-id="bfb8d-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bfb8d-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="bfb8d-112">Account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="bfb8d-112">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="bfb8d-113">Creare un controller MVC</span><span class="sxs-lookup"><span data-stu-id="bfb8d-113">Create an MVC controller</span></span> 

1. <span data-ttu-id="bfb8d-114">In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Controller** e selezionare **Aggiungi > Controller** dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-114">In the **Solution Explorer**, right-click **Controllers**, and, from the context menu, select **Add->Controller**.</span></span>

    ![Aggiungere un controller a un'app MVC ASP.NET](./media/vs-storage-aspnet-getting-started-tables/add-controller-menu.png)

1. <span data-ttu-id="bfb8d-116">Nella finestra di dialogo **Aggiungi scaffolding** fare clic su **Controller MVC 5 - Vuoto** e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-116">On the **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Specificare il tipo di controller MVC](./media/vs-storage-aspnet-getting-started-tables/add-controller.png)

1. <span data-ttu-id="bfb8d-118">Nella finestra di dialogo **Aggiungi controller** assegnare un nome al controller *TablesController* e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-118">On the **Add Controller** dialog, name the controller *TablesController*, and select **Add**.</span></span>

    ![Assegnare un nome al controller MVC](./media/vs-storage-aspnet-getting-started-tables/add-controller-name.png)

1. <span data-ttu-id="bfb8d-120">Aggiungere le direttive *using* seguenti al file `TablesController.cs`:</span><span class="sxs-lookup"><span data-stu-id="bfb8d-120">Add the following *using* directives to the `TablesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Table;
    ```

### <a name="create-a-model-class"></a><span data-ttu-id="bfb8d-121">Creare una classe di modello</span><span class="sxs-lookup"><span data-stu-id="bfb8d-121">Create a model class</span></span>

<span data-ttu-id="bfb8d-122">Molti esempi in questo articolo usano una classe derivata da **TableEntity**, denominata **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-122">Many of the examples in this article use a **TableEntity**-derived class called **CustomerEntity**.</span></span> <span data-ttu-id="bfb8d-123">La procedura seguente consente di dichiarare questa classe come classe di modello:</span><span class="sxs-lookup"><span data-stu-id="bfb8d-123">The following steps guide you through declaring this class as a model class:</span></span>

1. <span data-ttu-id="bfb8d-124">In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Modelli** e selezionare **Aggiungi > Classe** dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-124">In the **Solution Explorer**, right-click **Models**, and, from the context menu, select **Add->Class**.</span></span>

1. <span data-ttu-id="bfb8d-125">Nella finestra di dialogo **Aggiungi nuovo elemento** assegnare un nome alla classe, **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-125">On the **Add New Item** dialog, name the class, **CustomerEntity**.</span></span>

1. <span data-ttu-id="bfb8d-126">Aprire il file `CustomerEntity.cs` e aggiungere le direttive **using** seguenti:</span><span class="sxs-lookup"><span data-stu-id="bfb8d-126">Open the `CustomerEntity.cs` file, and add the following **using** directive:</span></span>

    ```csharp
    using Microsoft.WindowsAzure.Storage.Table;
    ```

1. <span data-ttu-id="bfb8d-127">Modificare la classe in modo che, al termine, la classe venga dichiarata come illustrato nel codice seguente.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-127">Modify the class so that, when finished, the class is declared as in the following code.</span></span> <span data-ttu-id="bfb8d-128">La classe dichiara una classe di entità denominata **CustomerEntity** che usa il nome e il cognome del cliente rispettivamente come chiave di riga e chiave di partizione.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-128">The class declares an entity class called **CustomerEntity** that uses the customer's first name as the row key and last name as the partition key.</span></span>

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

## <a name="create-a-table"></a><span data-ttu-id="bfb8d-129">Creare una tabella</span><span class="sxs-lookup"><span data-stu-id="bfb8d-129">Create a table</span></span>

<span data-ttu-id="bfb8d-130">I passaggi seguenti illustrano come creare una tabella:</span><span class="sxs-lookup"><span data-stu-id="bfb8d-130">The following steps illustrate how to create a table:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="bfb8d-131">Questa sezione presuppone che siano stati completati i passaggi descritti in [Configurare l'ambiente di sviluppo](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="bfb8d-131">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="bfb8d-132">Aprire il file `TablesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="bfb8d-132">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="bfb8d-133">Aggiungere un metodo denominato **CreateTable** che restituisce un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-133">Add a method called **CreateTable** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateTable()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="bfb8d-134">Nel metodo **CreateTable** recuperare un oggetto **CloudStorageAccount** che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-134">Within the **CreateTable** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="bfb8d-135">Usare il codice seguente per ottenere la stringa di connessione di archiviazione e le informazioni sull'account di archiviazione dalla configurazione del servizio di Azure: sostituire *&lt;nome account di archiviazione>* con il nome dell'account di archiviazione Azure a cui si sta accedendo.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-135">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="bfb8d-136">Ottenere un oggetto **CloudTableClient** che rappresenta un client del servizio tabelle.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-136">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="bfb8d-137">Ottenere un oggetto **CloudTable** che rappresenta un riferimento al nome della tabella desiderata.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-137">Get a **CloudTable** object that represents a reference to the desired table name.</span></span> <span data-ttu-id="bfb8d-138">Il metodo **CloudTableClient.GetTableReference** non esegue una richiesta all'archiviazione tabelle.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-138">The **CloudTableClient.GetTableReference** method does not make a request against table storage.</span></span> <span data-ttu-id="bfb8d-139">Il riferimento viene restituito indipendentemente dall'esistenza della tabella.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-139">The reference is returned whether or not the table exists.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="bfb8d-140">Chiamare il metodo **CloudTable.CreateIfNotExists** per creare la tabella se non esiste.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-140">Call the **CloudTable.CreateIfNotExists** method to create the table if it does not yet exist.</span></span> <span data-ttu-id="bfb8d-141">Il metodo **CloudTable.CreateIfNotExists** restituisce **true** se la tabella non esiste e viene creata correttamente.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-141">The **CloudTable.CreateIfNotExists** method returns **true** if the table does not exist, and is successfully created.</span></span> <span data-ttu-id="bfb8d-142">In caso contrario, viene restituito **false**.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-142">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = table.CreateIfNotExists();
    ```

1. <span data-ttu-id="bfb8d-143">Aggiornare **ViewBag** con il nome della tabella.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-143">Update the **ViewBag** with the name of the table.</span></span>

    ```csharp
    ViewBag.TableName = table.Name;
    ```

1. <span data-ttu-id="bfb8d-144">In **Esplora soluzioni** espandere la cartella **Views**, fare clic con il pulsante destro del mouse su **Tabelle** e dal menu di scelta rapida selezionare **Aggiungi->Visualizzazione**.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-144">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="bfb8d-145">Nella finestra di dialogo **Aggiungi visualizzazione** immettere **CreateTable** per il nome della visualizzazione e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-145">On the **Add View** dialog, enter **CreateTable** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="bfb8d-146">Aprire `CreateTable.cshtml` e modificarlo in modo che l'aspetto sia simile al frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="bfb8d-146">Open `CreateTable.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Table";
    }
    
    <h2>Create Table results</h2>

    Creation of @ViewBag.TableName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="bfb8d-147">In **Esplora soluzioni** espandere la cartella **Views->Shared** e aprire `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-147">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="bfb8d-148">Dopo l'ultimo **Html.ActionLink** aggiungere il seguente **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="bfb8d-148">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create table", "CreateTable", "Tables")</li>
    ```

1. <span data-ttu-id="bfb8d-149">Eseguire l'applicazione e selezionare **Create table** per visualizzare risultati simili allo screenshot seguente:</span><span class="sxs-lookup"><span data-stu-id="bfb8d-149">Run the application, and select **Create table** to see results similar to the following screen shot:</span></span>
  
    ![Crea tabella](./media/vs-storage-aspnet-getting-started-tables/create-table-results.png)

    <span data-ttu-id="bfb8d-151">Come accennato in precedenza, il metodo **CloudTable.CreateIfNotExists** restituisce **true** solo quando la tabella non esiste e viene creata.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-151">As mentioned previously, the **CloudTable.CreateIfNotExists** method returns **true** only when the table doesn't exist and is created.</span></span> <span data-ttu-id="bfb8d-152">Se quindi si esegue l'app quando la tabella esiste, il metodo restituisce **false**.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-152">Therefore, if you run the app when the table exists, the method returns **false**.</span></span> <span data-ttu-id="bfb8d-153">Per eseguire l'app più volte, è necessario eliminare la tabella prima di eseguire di nuovo l'app.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-153">To run the app multiple times, you must delete the table before running the app again.</span></span> <span data-ttu-id="bfb8d-154">L'eliminazione della tabella può essere eseguita tramite il metodo **CloudTable.Delete**.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-154">Deleting the table can be done via the **CloudTable.Delete** method.</span></span> <span data-ttu-id="bfb8d-155">È possibile anche eliminare la tabella usando il [portale Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) o [Esplora archivi di Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="bfb8d-155">You can also delete the table using the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="bfb8d-156">Aggiungere un'entità a una tabella</span><span class="sxs-lookup"><span data-stu-id="bfb8d-156">Add an entity to a table</span></span>

<span data-ttu-id="bfb8d-157">Per eseguire il mapping di *entità* a oggetti C\#, viene usata una classe personalizzata derivata da **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-157">*Entities* map to C\# objects by using a custom class derived from **TableEntity**.</span></span> <span data-ttu-id="bfb8d-158">Per aggiungere un'entità a una classe, creare una classe che definisca le proprietà dell'entità.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-158">To add an entity to a table, create a class that defines the properties of your entity.</span></span> <span data-ttu-id="bfb8d-159">Questa sezione illustra come definire una classe di entità che usa il nome e il cognome del cliente rispettivamente come chiave di riga e chiave di partizione.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-159">In this section, you'll see how to define an entity class that uses the customer's first name as the row key and last name as the partition key.</span></span> <span data-ttu-id="bfb8d-160">La combinazione della chiave di riga e della chiave di partizione di un'entità consentono di identificare in modo univoco l'entità nella tabella.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-160">Together, an entity's partition and row key uniquely identify the entity in the table.</span></span> <span data-ttu-id="bfb8d-161">Le query su entità con la stessa chiave di partizione vengono eseguite più rapidamente di quelle con chiavi di partizione diverse, tuttavia l'uso di chiavi di partizione diverse assicura una maggiore scalabilità delle operazioni parallele.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-161">Entities with the same partition key can be queried faster than entities with different partition keys, but using diverse partition keys allows for greater scalability of parallel operations.</span></span> <span data-ttu-id="bfb8d-162">Tutte le proprietà da archiviare nel servizio tabelle devono essere proprietà pubbliche di un tipo supportato che espone entrambi i valori di impostazione e recupero.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-162">For any property that should be stored in the table service, the property must be a public property of a supported type that exposes both setting and retrieving values.</span></span>
<span data-ttu-id="bfb8d-163">La classe di entità *deve* dichiarare un costruttore pubblico senza parametri.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-163">The entity class *must* declare a public parameter-less constructor.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="bfb8d-164">Questa sezione presuppone che siano stati completati i passaggi descritti in [Configurare l'ambiente di sviluppo](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="bfb8d-164">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment).</span></span>

1. <span data-ttu-id="bfb8d-165">Aprire il file `TablesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="bfb8d-165">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="bfb8d-166">Aggiungere la seguente direttiva in modo che il codice nel file `TablesController.cs` possa accedere alla classe **CustomerEntity**:</span><span class="sxs-lookup"><span data-stu-id="bfb8d-166">Add the following directive so that the code in the `TablesController.cs` file can access the **CustomerEntity** class:</span></span>

    ```csharp
    using StorageAspnet.Models;
    ```

1. <span data-ttu-id="bfb8d-167">Aggiungere un metodo denominato **AddEntity** che restituisce un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-167">Add a method called **AddEntity** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddEntity()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="bfb8d-168">Nel metodo **AddEntity** recuperare un oggetto **CloudStorageAccount** che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-168">Within the **AddEntity** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="bfb8d-169">Usare il codice seguente per ottenere la stringa di connessione di archiviazione e le informazioni sull'account di archiviazione dalla configurazione del servizio di Azure: sostituire *&lt;nome account di archiviazione>* con il nome dell'account di archiviazione Azure a cui si sta accedendo.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-169">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="bfb8d-170">Ottenere un oggetto **CloudTableClient** che rappresenta un client del servizio tabelle.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-170">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="bfb8d-171">Ottenere un oggetto **CloudTable** che rappresenta un riferimento alla tabella in cui si sta aggiungendo la nuova entità.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-171">Get a **CloudTable** object that represents a reference to the table to which you are going to add the new entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="bfb8d-172">Creare un'istanza e inizializzare la classe **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-172">Instantiate and initialize the **CustomerEntity** class.</span></span>

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    ```

1. <span data-ttu-id="bfb8d-173">Creare un oggetto **TableOperation** che inserisce l'entità cliente.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-173">Create a **TableOperation** object that inserts the customer entity.</span></span>

    ```csharp
    TableOperation insertOperation = TableOperation.Insert(customer1);
    ```

1. <span data-ttu-id="bfb8d-174">Eseguire l'operazione di inserimento chiamando il metodo **CloudTable.Execute**.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-174">Execute the insert operation by calling the **CloudTable.Execute** method.</span></span> <span data-ttu-id="bfb8d-175">È possibile verificare il risultato dell'operazione controllando la proprietà **TableResult.HttpStatusCode**.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-175">You can verify the result of the operation by inspecting the **TableResult.HttpStatusCode** property.</span></span> <span data-ttu-id="bfb8d-176">Il codice di stato 2xx indica che l'azione richiesta dal client è stata elaborata correttamente.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-176">A status code of 2xx indicates the action requested by the client was processed successfully.</span></span> <span data-ttu-id="bfb8d-177">Ad esempio, l'inserimento di nuove entità genera il codice di stato HTTP 204 indicante che l'operazione è stata elaborata correttamente e il server non ha restituito alcun contenuto.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-177">For example, successful insertions of new entities results in an HTTP status code of 204, meaning that the operation was successfully processed and the server did not return any content.</span></span>

    ```csharp
    TableResult result = table.Execute(insertOperation);
    ```

1. <span data-ttu-id="bfb8d-178">Aggiornare **ViewBag** con il nome della tabella e i risultati dell'operazione di inserimento.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-178">Update the **ViewBag** with the table name, and the results of the insert operation.</span></span>

    ```csharp
    ViewBag.TableName = table.Name;
    ViewBag.Result = result.HttpStatusCode;
    ```

1. <span data-ttu-id="bfb8d-179">In **Esplora soluzioni** espandere la cartella **Views**, fare clic con il pulsante destro del mouse su **Tabelle** e dal menu di scelta rapida selezionare **Aggiungi->Visualizzazione**.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-179">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="bfb8d-180">Nella finestra di dialogo **Aggiungi visualizzazione** immettere **AddEntity** per il nome della visualizzazione e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-180">On the **Add View** dialog, enter **AddEntity** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="bfb8d-181">Aprire `AddEntity.cshtml` e modificarlo in modo che l'aspetto sia simile al frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="bfb8d-181">Open `AddEntity.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add entity";
    }
    
    <h2>Add entity results</h2>

    Insert of entity into @ViewBag.TableName @(ViewBag.Result == 204 ? "succeeded" : "failed")
    ```
1. <span data-ttu-id="bfb8d-182">In **Esplora soluzioni** espandere la cartella **Views->Shared** e aprire `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-182">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="bfb8d-183">Dopo l'ultimo **Html.ActionLink** aggiungere il seguente **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="bfb8d-183">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add entity", "AddEntity", "Tables")</li>
    ```

1. <span data-ttu-id="bfb8d-184">Eseguire l'applicazione e selezionare **Aggiungi entità** per visualizzare risultati simili allo screenshot seguente:</span><span class="sxs-lookup"><span data-stu-id="bfb8d-184">Run the application, and select **Add entity** to see results similar to the following screen shot:</span></span>
  
    ![Aggiungi entità](./media/vs-storage-aspnet-getting-started-tables/add-entity-results.png)

    <span data-ttu-id="bfb8d-186">È possibile verificare che l'entità sia stata aggiunta seguendo i passaggi nella sezione [Ottenere una singola entità](#get-a-single-entity).</span><span class="sxs-lookup"><span data-stu-id="bfb8d-186">You can verify that the entity was added by following the steps in the section, [Get a single entity](#get-a-single-entity).</span></span> <span data-ttu-id="bfb8d-187">È possibile anche usare [Esplora archivi di Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) per visualizzare tutte le entità per le tabelle.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-187">You can also use the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) to view all the entities for your tables.</span></span>

## <a name="add-a-batch-of-entities-to-a-table"></a><span data-ttu-id="bfb8d-188">Aggiungere un batch di entità a una tabella</span><span class="sxs-lookup"><span data-stu-id="bfb8d-188">Add a batch of entities to a table</span></span>

<span data-ttu-id="bfb8d-189">Oltre ad [aggiungere entità a una tabella una alla volta](#add-an-entity-to-a-table), è possibile aggiungere entità anche in batch.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-189">In addition to being able to [add an entity to a table one at a time](#add-an-entity-to-a-table), you can also add entities in batch.</span></span> <span data-ttu-id="bfb8d-190">L'aggiunta di entità in batch riduce il numero di round trip tra il codice e il servizio tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-190">Adding entities in batch reduces the number of round-trips between your code and the Azure table service.</span></span> <span data-ttu-id="bfb8d-191">I passaggi seguenti illustrano come aggiungere più entità a una tabella con una singola operazione di inserimento:</span><span class="sxs-lookup"><span data-stu-id="bfb8d-191">The following steps illustrate how to add multiple entities to a table with a single insert operation:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="bfb8d-192">Questa sezione presuppone che siano stati completati i passaggi descritti in [Configurare l'ambiente di sviluppo](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="bfb8d-192">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment).</span></span>

1. <span data-ttu-id="bfb8d-193">Aprire il file `TablesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="bfb8d-193">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="bfb8d-194">Aggiungere un metodo denominato **AddEntities** che restituisce un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-194">Add a method called **AddEntities** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddEntities()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="bfb8d-195">Nel metodo **AddEntities** recuperare un oggetto **CloudStorageAccount** che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-195">Within the **AddEntities** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="bfb8d-196">Usare il codice seguente per ottenere la stringa di connessione di archiviazione e le informazioni sull'account di archiviazione dalla configurazione del servizio di Azure: sostituire *&lt;nome account di archiviazione>* con il nome dell'account di archiviazione Azure a cui si sta accedendo.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-196">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="bfb8d-197">Ottenere un oggetto **CloudTableClient** che rappresenta un client del servizio tabelle.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-197">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="bfb8d-198">Ottenere un oggetto **CloudTable** che rappresenta un riferimento alla tabella in cui si sta aggiungendo le nuove entità.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-198">Get a **CloudTable** object that represents a reference to the table to which you are going to add the new entities.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="bfb8d-199">Creare un'istanza di alcuni oggetti cliente basati sulla classe di modello **CustomerEntity** presentati nella sezione [Aggiungere un'entità a una tabella](#add-an-entity-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="bfb8d-199">Instantiate some customer objects based on the **CustomerEntity** model class presented in the section, [Add an entity to a table](#add-an-entity-to-a-table).</span></span>

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
    customer1.Email = "Jeff@contoso.com";

    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.Email = "Ben@contoso.com";
    ```

1. <span data-ttu-id="bfb8d-200">Ottenere un oggetto **TableBatchOperation**.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-200">Get a **TableBatchOperation** object.</span></span>

    ```csharp
    TableBatchOperation batchOperation = new TableBatchOperation();
    ```

1. <span data-ttu-id="bfb8d-201">Aggiungere le entità all'oggetto di operazione di inserimento in batch.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-201">Add entities to the batch insert operation object.</span></span>

    ```csharp
    batchOperation.Insert(customer1);
    batchOperation.Insert(customer2);
    ```

1. <span data-ttu-id="bfb8d-202">Eseguire l'operazione di inserimento in batch chiamando il metodo **CloudTable.ExecuteBatch**.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-202">Execute the batch insert operation by calling the **CloudTable.ExecuteBatch** method.</span></span>   

    ```csharp
    IList<TableResult> results = table.ExecuteBatch(batchOperation);
    ```

1. <span data-ttu-id="bfb8d-203">Il metodo **CloudTable.ExecuteBatch** restituisce un elenco di oggetti **TableResult** in cui ogni oggetto **TableResult** può essere esaminato per determinare l'esito positivo o negativo di ogni singola operazione.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-203">The **CloudTable.ExecuteBatch** method returns a list of **TableResult** objects where each **TableResult** object can be examined to determine the success or failure of each individual operation.</span></span> <span data-ttu-id="bfb8d-204">Per questo esempio, passare l'elenco a una visualizzazione e mostrare i risultati di ogni operazione.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-204">For this example, pass the list to a view and let the view display the results of each operation.</span></span> 
 
    ```csharp
    return View(results);
    ```

1. <span data-ttu-id="bfb8d-205">In **Esplora soluzioni** espandere la cartella **Views**, fare clic con il pulsante destro del mouse su **Tabelle** e dal menu di scelta rapida selezionare **Aggiungi->Visualizzazione**.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-205">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="bfb8d-206">Nella finestra di dialogo **Aggiungi visualizzazione** immettere **AddEntities** per il nome della visualizzazione e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-206">On the **Add View** dialog, enter **AddEntities** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="bfb8d-207">Aprire `AddEntities.cshtml` e modificarlo in modo che l'aspetto sia simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-207">Open `AddEntities.cshtml`, and modify it so that it looks like the following.</span></span>

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

1. <span data-ttu-id="bfb8d-208">In **Esplora soluzioni** espandere la cartella **Views->Shared** e aprire `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-208">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="bfb8d-209">Dopo l'ultimo **Html.ActionLink** aggiungere il seguente **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="bfb8d-209">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add entities", "AddEntities", "Tables")</li>
    ```

1. <span data-ttu-id="bfb8d-210">Eseguire l'applicazione e selezionare **Aggiungi entità** per visualizzare risultati simili allo screenshot seguente:</span><span class="sxs-lookup"><span data-stu-id="bfb8d-210">Run the application, and select **Add entities** to see results similar to the following screen shot:</span></span>
  
    ![Aggiungi entità](./media/vs-storage-aspnet-getting-started-tables/add-entities-results.png)

    <span data-ttu-id="bfb8d-212">È possibile verificare che l'entità sia stata aggiunta seguendo i passaggi nella sezione [Ottenere una singola entità](#get-a-single-entity).</span><span class="sxs-lookup"><span data-stu-id="bfb8d-212">You can verify that the entity was added by following the steps in the section, [Get a single entity](#get-a-single-entity).</span></span> <span data-ttu-id="bfb8d-213">È possibile anche usare [Esplora archivi di Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) per visualizzare tutte le entità per le tabelle.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-213">You can also use the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) to view all the entities for your tables.</span></span>

## <a name="get-a-single-entity"></a><span data-ttu-id="bfb8d-214">Ottenere una singola entità</span><span class="sxs-lookup"><span data-stu-id="bfb8d-214">Get a single entity</span></span>

<span data-ttu-id="bfb8d-215">Questa sezione illustra come ottenere una singola entità da una tabella usando la chiave di riga e la chiave di partizione dell'entità.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-215">This section illustrates how to get a single entity from a table using the entity's row key and partition key.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="bfb8d-216">Questa sezione presuppone che siano stati completati i passaggi descritti in [Configurare l'ambiente di sviluppo](#set-up-the-development-environment) e che siano stati usati i dati in [Aggiungere un batch di entità a una tabella](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="bfb8d-216">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="bfb8d-217">Aprire il file `TablesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="bfb8d-217">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="bfb8d-218">Aggiungere un metodo denominato **GetSingle** che restituisce un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-218">Add a method called **GetSingle** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetSingle()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="bfb8d-219">Nel metodo **ListBlobs** recuperare un oggetto **CloudStorageAccount** che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-219">Within the **GetSingle** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="bfb8d-220">Usare il codice seguente per ottenere la stringa di connessione di archiviazione e le informazioni sull'account di archiviazione dalla configurazione del servizio di Azure: sostituire *&lt;nome account di archiviazione>* con il nome dell'account di archiviazione Azure a cui si sta accedendo.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-220">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="bfb8d-221">Ottenere un oggetto **CloudTableClient** che rappresenta un client del servizio tabelle.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-221">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="bfb8d-222">Ottenere un oggetto **CloudTable** che rappresenta un riferimento alla tabella da cui si stanno recuperando l'entità.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-222">Get a **CloudTable** object that represents a reference to the table from which you are retrieving the entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="bfb8d-223">Creare un oggetto operazione di recupero che accetta un oggetto entità derivato da **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-223">Create a retrieve operation object that takes an entity object derived from **TableEntity**.</span></span> <span data-ttu-id="bfb8d-224">Il primo parametro è il *partitionKey* e il secondo è il *rowKey*.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-224">The first parameter is the *partitionKey*, and the second parameter is the *rowKey*.</span></span> <span data-ttu-id="bfb8d-225">Usando la classe **CustomerEntity** e i dati presentati nella sezione [Aggiungere un batch di entità a una tabella](#add-a-batch-of-entities-to-a-table), il frammento di codice seguente esegue una query sulla tabella per un **CustomerEntity** il cui valore *partitionKey* sia "Smith" e il cui valore *rowKey* sia "Ben":</span><span class="sxs-lookup"><span data-stu-id="bfb8d-225">Using the **CustomerEntity** class and data presented in the section [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table), the following code snippet queries the table for a **CustomerEntity** entity with a *partitionKey* value of "Smith" and a *rowKey* value of "Ben":</span></span>

    ```csharp
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");
    ```

1. <span data-ttu-id="bfb8d-226">Eseguire l'operazione di recupero.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-226">Execute the retrieve operation.</span></span>   

    ```csharp
    TableResult result = table.Execute(retrieveOperation);
    ```

1. <span data-ttu-id="bfb8d-227">Passare il risultato alla visualizzazione per mostrare i dati ottenuti.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-227">Pass the result to the view for display.</span></span>

    ```csharp
    return View(result);
    ```

1. <span data-ttu-id="bfb8d-228">In **Esplora soluzioni** espandere la cartella **Views**, fare clic con il pulsante destro del mouse su **Tabelle** e dal menu di scelta rapida selezionare **Aggiungi->Visualizzazione**.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-228">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="bfb8d-229">Nella finestra di dialogo **Aggiungi visualizzazione** immettere **GetSingle** per il nome della visualizzazione e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-229">On the **Add View** dialog, enter **GetSingle** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="bfb8d-230">Aprire `GetSingle.cshtml` e modificarlo in modo che l'aspetto sia simile al frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="bfb8d-230">Open `GetSingle.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

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

1. <span data-ttu-id="bfb8d-231">In **Esplora soluzioni** espandere la cartella **Views->Shared** e aprire `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-231">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="bfb8d-232">Dopo l'ultimo **Html.ActionLink** aggiungere il seguente **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="bfb8d-232">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get single", "GetSingle", "Tables")</li>
    ```

1. <span data-ttu-id="bfb8d-233">Eseguire l'applicazione e selezionare **Get Single** per visualizzare risultati simili allo screenshot seguente:</span><span class="sxs-lookup"><span data-stu-id="bfb8d-233">Run the application, and select **Get Single** to see results similar to the following screen shot:</span></span>
  
    ![Get single](./media/vs-storage-aspnet-getting-started-tables/get-single-results.png)

## <a name="get-all-entities-in-a-partition"></a><span data-ttu-id="bfb8d-235">Recuperare tutte le entità di una partizione</span><span class="sxs-lookup"><span data-stu-id="bfb8d-235">Get all entities in a partition</span></span>

<span data-ttu-id="bfb8d-236">Come accennato nella sezione [Aggiungere un'entità a una tabella](#add-an-entity-to-a-table), la combinazione di una partizione e una chiave di riga identifica in modo univoco un'entità in una tabella.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-236">As mentioned in the section, [Add an entity to a table](#add-an-entity-to-a-table), the combination of a partition and a row key uniquely identify an entity in a table.</span></span> <span data-ttu-id="bfb8d-237">Le query su entità con la stessa chiave di partizione vengono eseguite più rapidamente di quelle con chiavi di partizione diverse.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-237">Entities with the same partition key can be queried faster than entities with different partition keys.</span></span> <span data-ttu-id="bfb8d-238">Questa sezione illustra come eseguire query su una tabella per tutte le entità da una partizione specificata.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-238">This section illustrates how to query a table for all the entities from a specified partition.</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="bfb8d-239">Questa sezione presuppone che siano stati completati i passaggi descritti in [Configurare l'ambiente di sviluppo](#set-up-the-development-environment) e che siano stati usati i dati in [Aggiungere un batch di entità a una tabella](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="bfb8d-239">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="bfb8d-240">Aprire il file `TablesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="bfb8d-240">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="bfb8d-241">Aggiungere un metodo denominato **GetPartition** che restituisce un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-241">Add a method called **GetPartition** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetPartition()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="bfb8d-242">Nel metodo **GetPartition** recuperare un oggetto **CloudStorageAccount** che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-242">Within the **GetPartition** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="bfb8d-243">Usare il codice seguente per ottenere la stringa di connessione di archiviazione e le informazioni sull'account di archiviazione dalla configurazione del servizio di Azure: sostituire *&lt;nome account di archiviazione>* con il nome dell'account di archiviazione Azure a cui si sta accedendo.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-243">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="bfb8d-244">Ottenere un oggetto **CloudTableClient** che rappresenta un client del servizio tabelle.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-244">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="bfb8d-245">Ottenere un oggetto **CloudTable** che rappresenta un riferimento alla tabella da cui si stanno recuperando le entità.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-245">Get a **CloudTable** object that represents a reference to the table from which you are retrieving the entities.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="bfb8d-246">Creare un'istanza di un oggetto **TableQuery** specificando la query nella clausola **Where**.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-246">Instantiate a **TableQuery** object specifying the query in the **Where** clause.</span></span> <span data-ttu-id="bfb8d-247">Usando la classe **CustomerEntity** e i dati presentati nella sezione [Aggiungere un batch di entità a una tabella](#add-a-batch-of-entities-to-a-table), il frammento di codice seguente esegue una query sulla tabella per tutte le entità in cui il valore **PartitionKey** (cognome del cliente) sia "Smith":</span><span class="sxs-lookup"><span data-stu-id="bfb8d-247">Using the **CustomerEntity** class and data presented in the section [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table), the following code snippet queries the table for a all entities where the **PartitionKey** (customer's last name) has a value of "Smith":</span></span>

    ```csharp
    TableQuery<CustomerEntity> query = 
        new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));
    ```

1. <span data-ttu-id="bfb8d-248">All'interno di un ciclo chiamare il metodo **CloudTable.ExecuteQuerySegmented** passando l'oggetto query istanziato nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-248">Within a loop, call the **CloudTable.ExecuteQuerySegmented** method passing the query object you instantiated in the previous step.</span></span>  <span data-ttu-id="bfb8d-249">Il metodo **CloudTable.ExecuteQuerySegmented** restituisce un oggetto **TableContinuationToken** che, quando è **null**, indica che non ci sono più entità da recuperare.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-249">The **CloudTable.ExecuteQuerySegmented** method returns a **TableContinuationToken** object that - when **null** - indicates that there are no more entities to retrieve.</span></span> <span data-ttu-id="bfb8d-250">All'interno del ciclo usare un altro ciclo per eseguire un'iterazione sulle entità restituite.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-250">Within the loop, use another loop to iterate over the returned entities.</span></span> <span data-ttu-id="bfb8d-251">Nell'esempio di codice seguente ogni entità restituita viene aggiunta a un elenco.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-251">In the following code example, each returned entity is added to a list.</span></span> <span data-ttu-id="bfb8d-252">Al termine del ciclo, l'elenco viene passato a una visualizzazione per mostrare i dati ottenuti:</span><span class="sxs-lookup"><span data-stu-id="bfb8d-252">Once the loop ends, the list is passed to a view for display:</span></span> 

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

1. <span data-ttu-id="bfb8d-253">In **Esplora soluzioni** espandere la cartella **Views**, fare clic con il pulsante destro del mouse su **Tabelle** e dal menu di scelta rapida selezionare **Aggiungi->Visualizzazione**.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-253">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="bfb8d-254">Nella finestra di dialogo **Aggiungi visualizzazione** immettere **GetPartition** per il nome della visualizzazione e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-254">On the **Add View** dialog, enter **GetPartition** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="bfb8d-255">Aprire `GetPartition.cshtml` e modificarlo in modo che l'aspetto sia simile al frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="bfb8d-255">Open `GetPartition.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

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

1. <span data-ttu-id="bfb8d-256">In **Esplora soluzioni** espandere la cartella **Views->Shared** e aprire `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-256">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="bfb8d-257">Dopo l'ultimo **Html.ActionLink** aggiungere il seguente **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="bfb8d-257">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get partition", "GetPartition", "Tables")</li>
    ```

1. <span data-ttu-id="bfb8d-258">Eseguire l'applicazione e selezionare **Get Partition** per visualizzare risultati simili allo screenshot seguente:</span><span class="sxs-lookup"><span data-stu-id="bfb8d-258">Run the application, and select **Get Partition** to see results similar to the following screen shot:</span></span>
  
    ![Get Partition](./media/vs-storage-aspnet-getting-started-tables/get-partition-results.png)

## <a name="delete-an-entity"></a><span data-ttu-id="bfb8d-260">Eliminare un'entità</span><span class="sxs-lookup"><span data-stu-id="bfb8d-260">Delete an entity</span></span>

<span data-ttu-id="bfb8d-261">Questa sezione illustra come eliminare un'entità da una tabella.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-261">This section illustrates how to delete an entity from a table.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="bfb8d-262">Questa sezione presuppone che siano stati completati i passaggi descritti in [Configurare l'ambiente di sviluppo](#set-up-the-development-environment) e che siano stati usati i dati in [Aggiungere un batch di entità a una tabella](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="bfb8d-262">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="bfb8d-263">Aprire il file `TablesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="bfb8d-263">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="bfb8d-264">Aggiungere un metodo denominato **DeleteEntity** che restituisce un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-264">Add a method called **DeleteEntity** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteEntity()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="bfb8d-265">Nel metodo **DeleteEntity** recuperare un oggetto **CloudStorageAccount** che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-265">Within the **DeleteEntity** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="bfb8d-266">Usare il codice seguente per ottenere la stringa di connessione di archiviazione e le informazioni sull'account di archiviazione dalla configurazione del servizio di Azure: sostituire *&lt;nome account di archiviazione>* con il nome dell'account di archiviazione Azure a cui si sta accedendo.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-266">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="bfb8d-267">Ottenere un oggetto **CloudTableClient** che rappresenta un client del servizio tabelle.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-267">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="bfb8d-268">Ottenere un oggetto **CloudTable** che rappresenta un riferimento alla tabella da cui si sta eliminando l'entità.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-268">Get a **CloudTable** object that represents a reference to the table from which you are deleting the entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="bfb8d-269">Creare un oggetto operazione di eliminazione che accetta un oggetto entità derivato da **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-269">Create a delete operation object that takes an entity object derived from **TableEntity**.</span></span> <span data-ttu-id="bfb8d-270">In questo caso si usa la classe **CustomerEntity** e ai dati presentati nella sezione [Aggiungere un batch di entità a una tabella](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="bfb8d-270">In this case, we use the **CustomerEntity** class and data presented in the section [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table).</span></span> <span data-ttu-id="bfb8d-271">Il valore **ETag** dell'entità deve essere impostato su un valore valido.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-271">The entity's **ETag** must be set to a valid value.</span></span>  

    ```csharp
    TableOperation deleteOperation = 
        TableOperation.Delete(new CustomerEntity("Smith", "Ben") { ETag = "*" } );
    ```

1. <span data-ttu-id="bfb8d-272">Eseguire l'operazione di eliminazione.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-272">Execute the delete operation.</span></span>   

    ```csharp
    TableResult result = table.Execute(deleteOperation);
    ```

1. <span data-ttu-id="bfb8d-273">Passare il risultato alla visualizzazione per mostrare i dati ottenuti.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-273">Pass the result to the view for display.</span></span>

    ```csharp
    return View(result);
    ```

1. <span data-ttu-id="bfb8d-274">In **Esplora soluzioni** espandere la cartella **Views**, fare clic con il pulsante destro del mouse su **Tabelle** e dal menu di scelta rapida selezionare **Aggiungi->Visualizzazione**.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-274">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="bfb8d-275">Nella finestra di dialogo **Aggiungi visualizzazione** immettere **DeleteEntity** per il nome della visualizzazione e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-275">On the **Add View** dialog, enter **DeleteEntity** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="bfb8d-276">Aprire `DeleteEntity.cshtml` e modificarlo in modo che l'aspetto sia simile al frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="bfb8d-276">Open `DeleteEntity.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

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

1. <span data-ttu-id="bfb8d-277">In **Esplora soluzioni** espandere la cartella **Views->Shared** e aprire `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-277">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="bfb8d-278">Dopo l'ultimo **Html.ActionLink** aggiungere il seguente **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="bfb8d-278">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete entity", "DeleteEntity", "Tables")</li>
    ```

1. <span data-ttu-id="bfb8d-279">Eseguire l'applicazione e selezionare **Delete entity** per visualizzare risultati simili allo screenshot seguente:</span><span class="sxs-lookup"><span data-stu-id="bfb8d-279">Run the application, and select **Delete entity** to see results similar to the following screen shot:</span></span>
  
    ![Get single](./media/vs-storage-aspnet-getting-started-tables/delete-entity-results.png)

## <a name="next-steps"></a><span data-ttu-id="bfb8d-281">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bfb8d-281">Next steps</span></span>
<span data-ttu-id="bfb8d-282">Per ulteriori opzioni di archiviazione dei dati in Azure, consultare altre guide alle funzionalità.</span><span class="sxs-lookup"><span data-stu-id="bfb8d-282">View more feature guides to learn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="bfb8d-283">Introduzione all'Archiviazione BLOB di Azure e ai Servizi connessi di Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="bfb8d-283">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](../storage/vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="bfb8d-284">Introduzione all'archiviazione code di Azure e ai Servizi connessi di Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="bfb8d-284">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>](../storage/vs-storage-aspnet-getting-started-queues.md)
