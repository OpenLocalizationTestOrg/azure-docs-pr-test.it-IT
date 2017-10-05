---
title: Introduzione all'archiviazione tabelle e ai servizi connessi di Visual Studio (ASP.NET Core) |Microsoft Docs
description: Informazioni su come iniziare con il servizio di archiviazione tabelle di Azure in un progetto ASP.NET Core in Visual Studio dopo aver eseguito la connessione a un account di archiviazione con i servizi connessi di Visual Studio
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: c3c451d1-71ff-4222-a348-c41c98a02b85
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: b64d4f7e55977c7ce144987f7600e5ddcb25596c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-get-started-with-azure-table-storage-and-visual-studio-connected-services"></a><span data-ttu-id="d928d-103">Introduzione all'archiviazione tabelle di Azure e ai servizi relativi a Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d928d-103">How to get started with Azure Table storage and Visual Studio connected services</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="d928d-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="d928d-104">Overview</span></span>
<span data-ttu-id="d928d-105">Questo articolo descrive come iniziare a usare l'archiviazione tabelle di Azure in Visual Studio dopo avere creato o fatto riferimento a un account di archiviazione di Azure in un progetto ASP.NET Core usando la finestra di dialogo **Aggiungi servizi connessi** di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d928d-105">This article describes how get started using Azure Table storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using the Visual Studio **Add Connected Services** dialog.</span></span>

<span data-ttu-id="d928d-106">Il servizio di archiviazione tabelle di Azure consente di archiviare grandi quantità di dati strutturati.</span><span class="sxs-lookup"><span data-stu-id="d928d-106">The Azure Table storage service enables you to store large amounts of structured data.</span></span> <span data-ttu-id="d928d-107">Il servizio è un datastore NoSQL che accetta chiamate autenticate dall'interno e dall'esterno del cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="d928d-107">The service is a NoSQL data store that accepts authenticated calls from inside and outside the Azure cloud.</span></span> <span data-ttu-id="d928d-108">Le tabelle di Azure sono ideali per l'archiviazione di dati strutturati non relazionali.</span><span class="sxs-lookup"><span data-stu-id="d928d-108">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="d928d-109">L'operazione **Aggiungi servizi connessi** consente di installare i pacchetti NuGet appropriati per accedere all'archiviazione di Azure nel progetto e di aggiungere la stringa di connessione per l'account di archiviazione ai file di configurazione del progetto.</span><span class="sxs-lookup"><span data-stu-id="d928d-109">The **Add Connected Services** operation installs the appropriate NuGet packages to access Azure storage in your project and adds the connection string for the storage account to your project configuration files.</span></span>

<span data-ttu-id="d928d-110">Per ulteriori informazioni generali sull'utilizzo dell'archiviazione tabelle di Azure, vedere [Introduzione all'archiviazione tabelle di Azure con .NET](storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="d928d-110">For more general information about using Azure Table storage, see [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md).</span></span>

<span data-ttu-id="d928d-111">Per iniziare, è innanzitutto necessario creare una tabella nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d928d-111">To get started, you first need to create a table in your storage account.</span></span> <span data-ttu-id="d928d-112">Verrà mostrato come creare una tabella di Azure nel codice.</span><span class="sxs-lookup"><span data-stu-id="d928d-112">We'll show you how to create an Azure table in code.</span></span> <span data-ttu-id="d928d-113">Infine verrà mostrato come eseguire operazioni relative alle tabelle e all'entità di base, come l'aggiunta, la modifica, la lettura e la lettura delle entità delle tabelle.</span><span class="sxs-lookup"><span data-stu-id="d928d-113">We'll also show you how to perform basic table and entity operations, such as adding, modifying, reading and reading table entities.</span></span> <span data-ttu-id="d928d-114">Negli esempi, scritti in codice C\# viene usata la libreria client di Archiviazione di Azure per .NET.</span><span class="sxs-lookup"><span data-stu-id="d928d-114">The samples are written in C\# code and use the Azure Storage Client Library for .NET.</span></span>

<span data-ttu-id="d928d-115">**NOTA:** alcune API che eseguono chiamate ad Archiviazione di Azure in ASP.NET Core sono asincrone.</span><span class="sxs-lookup"><span data-stu-id="d928d-115">**NOTE** - Some of the APIs that perform calls out to Azure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="d928d-116">Per ulteriori informazioni, vedere [Programmazione asincrona con Async e Await](http://msdn.microsoft.com/library/hh191443.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d928d-116">See [Asynchronous Programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="d928d-117">Nel codice riportato di seguito si presuppone vengano utilizzati i metodi di programmazione asincrona.</span><span class="sxs-lookup"><span data-stu-id="d928d-117">The code below assumes Async programming methods are being used.</span></span>

## <a name="access-tables-in-code"></a><span data-ttu-id="d928d-118">Accesso alle tabelle nel codice</span><span class="sxs-lookup"><span data-stu-id="d928d-118">Access tables in code</span></span>
<span data-ttu-id="d928d-119">Per accedere alle tabelle nei progetti ASP.NET Core, è necessario includere gli elementi seguenti ai file di origine C# che consentono di accedere all'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="d928d-119">To access tables in ASP.NET Core projects, you need to include the following items to any C# source files that access Azure table storage.</span></span>

1. <span data-ttu-id="d928d-120">Assicurarsi che le dichiarazioni dello spazio dei nomi all'inizio del file C# includano queste istruzioni **using** .</span><span class="sxs-lookup"><span data-stu-id="d928d-120">Make sure the namespace declarations at the top of the C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="d928d-121">Ottenere un oggetto **CloudStorageAccount** che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d928d-121">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="d928d-122">Utilizzare il codice seguente per ottenere la stringa di connessione di archiviazione e le informazioni sull'account di archiviazione dalla configurazione del servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="d928d-122">Use the following code to get the your storage connection string and storage account information from the Azure service configuration.</span></span>
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
            CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
   
    <span data-ttu-id="d928d-123">**NOTA:** utilizzare tutto il codice riportato in precedenza prima del codice indicato negli esempi seguenti.</span><span class="sxs-lookup"><span data-stu-id="d928d-123">**NOTE** - Use all of the above code in front of the code in the following samples.</span></span>
3. <span data-ttu-id="d928d-124">Ottenere un oggetto **CloudTableClient** per fare riferimento agli oggetti delle tabelle nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d928d-124">Get a **CloudTableClient** object to reference the table objects in your storage account.</span></span>  
   
        // Create the table client.
        CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. <span data-ttu-id="d928d-125">Ottenere un oggetto di riferimento **CloudTable** per fare riferimento a tabelle ed entità specifiche.</span><span class="sxs-lookup"><span data-stu-id="d928d-125">Get a **CloudTable** reference object to reference a specific table and entities.</span></span>
   
        // Get a reference to a table named "peopleTable"
        CloudTable table = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a><span data-ttu-id="d928d-126">Creazione di una tabella in codice</span><span class="sxs-lookup"><span data-stu-id="d928d-126">Create a table in code</span></span>
<span data-ttu-id="d928d-127">Per creare la tabella di Azure, è sufficiente aggiungere una chiamata a **CreateIfNotExistsAsync()**.</span><span class="sxs-lookup"><span data-stu-id="d928d-127">To create the Azure table, just add a call to **CreateIfNotExistsAsync()**.</span></span>

    // Create the CloudTable if it does not exist
    await table.CreateIfNotExistsAsync();

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="d928d-128">Aggiungere un'entità a una tabella</span><span class="sxs-lookup"><span data-stu-id="d928d-128">Add an entity to a table</span></span>
<span data-ttu-id="d928d-129">Per aggiungere un'entità a una classe, creare una classe che definisca le proprietà dell'entità.</span><span class="sxs-lookup"><span data-stu-id="d928d-129">To add an entity to a table you create a class that defines the properties of your entity.</span></span> <span data-ttu-id="d928d-130">Il codice seguente permette di definire una classe di entità denominata **CustomerEntity** che usa il nome e il cognome del cliente rispettivamente come chiave di riga e chiave di partizione.</span><span class="sxs-lookup"><span data-stu-id="d928d-130">The following code defines an entity class called **CustomerEntity** that uses the customer's first name as the row key and last name as the partition key.</span></span>

    public class CustomerEntity : TableEntity
    {
        public CustomerEntity(string lastName, string firstName)
        {
            this.PartitionKey = lastName;
            this.RowKey = firstName;
        }

        public CustomerEntity() { }

        public string Email { get; set; }

        public string PhoneNumber { get; set; }
    }

<span data-ttu-id="d928d-131">Per eseguire le operazioni su tabelle che interessano entità, viene utilizzato l'oggetto **CloudTable** creato in precedenza in "Accesso alle tabelle nel codice".</span><span class="sxs-lookup"><span data-stu-id="d928d-131">Table operations involving entities are done using the **CloudTable** object you created earlier in "Access tables in code."</span></span> <span data-ttu-id="d928d-132">L'oggetto **TableOperation** rappresenta l'operazione da eseguire.</span><span class="sxs-lookup"><span data-stu-id="d928d-132">The **TableOperation** object represents the operation to be done.</span></span> <span data-ttu-id="d928d-133">L'esempio di codice seguente mostra come creare un oggetto **CloudTable** e un oggetto **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="d928d-133">The following code example shows how to create a **CloudTable** object and a **CustomerEntity** object.</span></span> <span data-ttu-id="d928d-134">Per preparare l'operazione, viene creato un oggetto **TableOperation** per inserire l'entità customer nella tabella.</span><span class="sxs-lookup"><span data-stu-id="d928d-134">To prepare the operation, a **TableOperation** is created to insert the customer entity into the table.</span></span> <span data-ttu-id="d928d-135">Infine, per eseguire l'operazione viene chiamato CloudTable.ExecuteAsync.</span><span class="sxs-lookup"><span data-stu-id="d928d-135">Finally, the operation is executed by calling CloudTable.ExecuteAsync.</span></span>

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create the TableOperation that inserts the customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute the insert operation.
    await peopleTable.ExecuteAsync(insertOperation);

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="d928d-136">Inserire un batch di entità</span><span class="sxs-lookup"><span data-stu-id="d928d-136">Insert a batch of entities</span></span>
<span data-ttu-id="d928d-137">È possibile inserire più entità in una tabella in una singola operazione di scrittura.</span><span class="sxs-lookup"><span data-stu-id="d928d-137">You can insert multiple entities into a table in a single write operation.</span></span> <span data-ttu-id="d928d-138">L'esempio di codice seguente crea due oggetti entità ("Jeff Smith" e "Ben Smith"), li aggiunge a un oggetto **TableBatchOperation** usando il metodo **Insert**, quindi avvia l'operazione richiamando CloudTable.ExecuteBatchAsync.</span><span class="sxs-lookup"><span data-stu-id="d928d-138">The following code example creates two entity objects ("Jeff Smith" and "Ben Smith"), adds them to a **TableBatchOperation** object using the **Insert** method, and then starts the operation by calling CloudTable.ExecuteBatchAsync.</span></span>

    // Create the batch operation.
    TableBatchOperation batchOperation = new TableBatchOperation();

    // Create a customer entity and add it to the table.
    CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
    customer1.Email = "Jeff@contoso.com";
    customer1.PhoneNumber = "425-555-0104";

    // Create another customer entity and add it to the table.
    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.Email = "Ben@contoso.com";
    customer2.PhoneNumber = "425-555-0102";

    // Add both customer entities to the batch insert operation.
    batchOperation.Insert(customer1);
    batchOperation.Insert(customer2);

    // Execute the batch operation.
    await peopleTable.ExecuteBatchAsync(batchOperation);

## <a name="get-all-of-the-entities-in-a-partition"></a><span data-ttu-id="d928d-139">Ottenere tutte le entità di una partizione</span><span class="sxs-lookup"><span data-stu-id="d928d-139">Get all of the entities in a partition</span></span>
<span data-ttu-id="d928d-140">Per eseguire una query su una tabella e recuperare tutte le entità di una partizione, usare un oggetto **TableQuery** .</span><span class="sxs-lookup"><span data-stu-id="d928d-140">To query a table for all of the entities in a partition, use a **TableQuery** object.</span></span> <span data-ttu-id="d928d-141">Nell'esempio di codice seguente viene specificato un filtro per le entità in cui la chiave di partizione è 'Smith'.</span><span class="sxs-lookup"><span data-stu-id="d928d-141">The following code example specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="d928d-142">Questo esempio consente di stampare sulla console i campi di ogni entità inclusa nei risultati della query.</span><span class="sxs-lookup"><span data-stu-id="d928d-142">This example prints the fields of each entity in the query results to the console.</span></span>

    // Construct the query operation for all customer entities where PartitionKey="Smith".
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>().Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

    // Print the fields for each customer.
    TableContinuationToken token = null;
    do
    {
        TableQuerySegment<CustomerEntity> resultSegment = await peopleTable.ExecuteQuerySegmentedAsync(query, token);
        token = resultSegment.ContinuationToken;

        foreach (CustomerEntity entity in resultSegment.Results)
        {
            Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
            entity.Email, entity.PhoneNumber);
        }
    } while (token != null);

## <a name="get-a-single-entity"></a><span data-ttu-id="d928d-143">Ottenere una singola entità</span><span class="sxs-lookup"><span data-stu-id="d928d-143">Get a single entity</span></span>
<span data-ttu-id="d928d-144">È possibile scrivere una query per ottenere una singola entità specifica.</span><span class="sxs-lookup"><span data-stu-id="d928d-144">You can write a query to get a single, specific entity.</span></span> <span data-ttu-id="d928d-145">Il codice seguente usa un oggetto **TableOperation** per specificare un cliente denominato 'Ben Smith'.</span><span class="sxs-lookup"><span data-stu-id="d928d-145">The following code uses a **TableOperation** object to specify a customer named 'Ben Smith'.</span></span> <span data-ttu-id="d928d-146">Questo metodo restituisce solo un'entità, anziché una raccolta, e il valore restituito in **TableResult.Result** è un oggetto **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="d928d-146">This method returns just one entity, rather than a collection, and the returned value in **TableResult.Result** is a **CustomerEntity** object.</span></span> <span data-ttu-id="d928d-147">La specifica delle chiavi di partizione e di riga in una query costituisce la soluzione più rapida per recuperare una singola entità dal servizio **tabelle** .</span><span class="sxs-lookup"><span data-stu-id="d928d-147">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the **Table** service.</span></span>

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute the retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print the phone number of the result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("The phone number could not be retrieved.");

## <a name="delete-an-entity"></a><span data-ttu-id="d928d-148">Eliminare un'entità</span><span class="sxs-lookup"><span data-stu-id="d928d-148">Delete an entity</span></span>
<span data-ttu-id="d928d-149">È possibile eliminare un'entità dopo averla individuata.</span><span class="sxs-lookup"><span data-stu-id="d928d-149">You can delete an entity after you find it.</span></span> <span data-ttu-id="d928d-150">Il codice seguente cerca un'entità customer denominata "Ben Smith" e, se la trova, la elimina.</span><span class="sxs-lookup"><span data-stu-id="d928d-150">The following code looks for a customer entity named "Ben Smith" and if it finds it, it deletes it.</span></span>

    // Create a retrieve operation that expects a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute the operation.
    TableResult retrievedResult = peopleTable.Execute(retrieveOperation);

    // Assign the result to a CustomerEntity object.
    CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

    // Create the Delete TableOperation and then execute it.
    if (deleteEntity != null)
    {
       TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

       // Execute the operation.
       await peopleTable.ExecuteAsync(deleteOperation);

       Console.WriteLine("Entity deleted.");
    }

    else
       Console.WriteLine("Couldn't delete the entity.");

## <a name="next-steps"></a><span data-ttu-id="d928d-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d928d-151">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

