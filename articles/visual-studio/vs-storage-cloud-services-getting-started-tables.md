---
title: Introduzione all'archiviazione tabelle e ai Servizi connessi di Visual Studio (servizi cloud) | Documentazione Microsoft
description: Informazioni su come iniziare a usare il servizio di archiviazione di tabella in un progetto di servizio di cloud in Visual Studio dopo aver eseguito la connessione a un account di archiviazione con i servizi connessi di Visual Studio.
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: a3a11ed8-ba7f-4193-912b-e555f5b72184
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 51b71d783806d9b0d58d4473b8c07f77441dadd8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="getting-started-with-azure-table-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="7f347-103">Introduzione all’archiviazione di tabella di Azure e ai servizi connessi di Visual Studio (progetti servizi cloud)</span><span class="sxs-lookup"><span data-stu-id="7f347-103">Getting started with Azure table storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="7f347-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="7f347-104">Overview</span></span>
<span data-ttu-id="7f347-105">In questo articolo viene descritto come iniziare a utilizzare l'archiviazione tabelle di Azure in Visual Studio dopo aver creato o fatto riferimento a un account di archiviazione di Azure in un progetto servizi cloud usando la finestra di dialogo **Aggiungi servizi connessi** di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7f347-105">This article describes how to get started using Azure table storage in Visual Studio after you have created or referenced an Azure storage account in a cloud services project by using the Visual Studio **Add Connected Services** dialog.</span></span> <span data-ttu-id="7f347-106">L'operazione **Aggiungi servizi connessi** consente di installare i pacchetti NuGet appropriati per accedere all'archiviazione di Azure nel progetto e di aggiungere la stringa di connessione per l'account di archiviazione ai file di configurazione del progetto.</span><span class="sxs-lookup"><span data-stu-id="7f347-106">The **Add Connected Services** operation installs the appropriate NuGet packages to access Azure storage in your project and adds the connection string for the storage account to your project configuration files.</span></span>

<span data-ttu-id="7f347-107">Il servizio di archiviazione tabelle di Azure consente di archiviare grandi quantità di dati strutturati.</span><span class="sxs-lookup"><span data-stu-id="7f347-107">The Azure Table storage service enables you to store large amounts of structured data.</span></span> <span data-ttu-id="7f347-108">Il servizio è un datastore NoSQL che accetta chiamate autenticate dall'interno e dall'esterno del cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="7f347-108">The service is a NoSQL datastore that accepts authenticated calls from inside and outside the Azure cloud.</span></span> <span data-ttu-id="7f347-109">Le tabelle di Azure sono ideali per l'archiviazione di dati strutturati non relazionali.</span><span class="sxs-lookup"><span data-stu-id="7f347-109">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="7f347-110">Per iniziare, è innanzitutto necessario creare una tabella nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7f347-110">To get started, you first need to create a table in your storage account.</span></span> <span data-ttu-id="7f347-111">Infine verrà mostrato come eseguire operazioni relative alle tabelle e all'entità di base, come l'aggiunta, la modifica, la lettura e la lettura delle entità delle tabelle.</span><span class="sxs-lookup"><span data-stu-id="7f347-111">We'll show you how to create an Azure table in code, and also how to perform basic table and entity operations, such as adding, modifying, reading and reading table entities.</span></span> <span data-ttu-id="7f347-112">Negli esempi, scritti in codice C\#, viene usata la [libreria client di Archiviazione di Microsoft Azure per .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f347-112">The samples are written in C\# code and use the [Microsoft Azure Storage client library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="7f347-113">**NOTA:** alcune API che eseguono chiamate ad Archiviazione di Azure sono asincrone.</span><span class="sxs-lookup"><span data-stu-id="7f347-113">**NOTE:** Some of the APIs that perform calls out to Azure storage are asynchronous.</span></span> <span data-ttu-id="7f347-114">Per altre informazioni, vedere [Programmazione asincrona con Async e Await](http://msdn.microsoft.com/library/hh191443.aspx) .</span><span class="sxs-lookup"><span data-stu-id="7f347-114">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="7f347-115">Nel codice riportato di seguito si presuppone vengano utilizzati i metodi di programmazione asincrona.</span><span class="sxs-lookup"><span data-stu-id="7f347-115">The code below assumes async programming methods are being used.</span></span>

* <span data-ttu-id="7f347-116">Per altre informazioni sulla modifica delle tabelle a livello di codice, vedere [Introduzione all'archiviazione tabelle di Azure con .NET](../storage/storage-dotnet-how-to-use-tables.md) .</span><span class="sxs-lookup"><span data-stu-id="7f347-116">See [Get started with Azure Table storage using .NET](../storage/storage-dotnet-how-to-use-tables.md) for more information on programmatically manipulating tables.</span></span>
* <span data-ttu-id="7f347-117">Vedere la [documentazione di archiviazione](https://azure.microsoft.com/documentation/services/storage/) per informazioni generali sull'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7f347-117">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="7f347-118">Vedere la [documentazione dei servizi Cloud](https://azure.microsoft.com/documentation/services/cloud-services/) per informazioni generali sui servizi cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="7f347-118">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="7f347-119">Vedere [ASP.NET](http://www.asp.net) per ulteriori informazioni sulle applicazioni di programmazione di ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="7f347-119">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

## <a name="access-tables-in-code"></a><span data-ttu-id="7f347-120">Accesso alle tabelle nel codice</span><span class="sxs-lookup"><span data-stu-id="7f347-120">Access tables in code</span></span>
<span data-ttu-id="7f347-121">Per accedere alle tabelle nei progetti di servizio cloud, è necessario includere gli elementi seguenti ai file di origine C# che consentono di accedere all'archiviazione delle tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="7f347-121">To access tables in cloud service projects, you need to include the following items to any C# source files that access Azure table storage.</span></span>

1. <span data-ttu-id="7f347-122">Assicurarsi che le dichiarazioni dello spazio dei nomi all'inizio del file C# includano queste istruzioni **using** .</span><span class="sxs-lookup"><span data-stu-id="7f347-122">Make sure the namespace declarations at the top of the C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="7f347-123">Ottenere un oggetto **CloudStorageAccount** che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7f347-123">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="7f347-124">Utilizzare il codice seguente per ottenere la stringa di connessione di archiviazione e le informazioni sull'account di archiviazione dalla configurazione del servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="7f347-124">Use the following code to get the storage connection string and storage account information from the Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage account name>
         _AzureStorageConnectionString"));
   > [!NOTE]
   > <span data-ttu-id="7f347-125">Utilizzare tutto il codice riportato in precedenza prima del codice indicato negli esempi seguenti.</span><span class="sxs-lookup"><span data-stu-id="7f347-125">Use all of the above code in front of the code in the following samples.</span></span>
   > 
   > 
3. <span data-ttu-id="7f347-126">Ottenere un oggetto **CloudTableClient** per fare riferimento agli oggetti delle tabelle nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7f347-126">Get a **CloudTableClient** object to reference the table objects in your storage account.</span></span>
   
         // Create the table client.
         CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. <span data-ttu-id="7f347-127">Ottenere un oggetto di riferimento **CloudTable** per fare riferimento a tabelle ed entità specifiche.</span><span class="sxs-lookup"><span data-stu-id="7f347-127">Get a **CloudTable** reference object to reference a specific table and entities.</span></span>
   
        // Get a reference to a table named "peopleTable".
        CloudTable peopleTable = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a><span data-ttu-id="7f347-128">Creazione di una tabella in codice</span><span class="sxs-lookup"><span data-stu-id="7f347-128">Create a table in code</span></span>
<span data-ttu-id="7f347-129">Per creare la tabella di Azure, è sufficiente aggiungere una chiamata a **CreateIfNotExistsAsync** per ottenere poi un oggetto **CloudTable** come descritto nella sezione "Accesso alle tabelle nel codice".</span><span class="sxs-lookup"><span data-stu-id="7f347-129">To create the Azure table, just add a call to **CreateIfNotExistsAsync** to the after you get a **CloudTable** object as described in the "Access tables in code" section.</span></span>

    // Create the CloudTable if it does not exist.
    await peopleTable.CreateIfNotExistsAsync();

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="7f347-130">Aggiungere un'entità a una tabella</span><span class="sxs-lookup"><span data-stu-id="7f347-130">Add an entity to a table</span></span>
<span data-ttu-id="7f347-131">Per aggiungere un'entità a una classe, creare una classe che definisca le proprietà dell'entità.</span><span class="sxs-lookup"><span data-stu-id="7f347-131">To add an entity to a table, create a class that defines the properties of your entity.</span></span> <span data-ttu-id="7f347-132">Il codice seguente permette di definire una classe di entità denominata **CustomerEntity** che usa il nome e il cognome del cliente rispettivamente come chiave di riga e chiave di partizione.</span><span class="sxs-lookup"><span data-stu-id="7f347-132">The following code defines an entity class called **CustomerEntity** that uses the customer's first name as the row key and the last name as the partition key.</span></span>

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

<span data-ttu-id="7f347-133">Per eseguire le operazioni su tabelle che interessano entità viene utilizzato l'oggetto **CloudTable** creato in precedenza in "Accesso alle tabelle nel codice".</span><span class="sxs-lookup"><span data-stu-id="7f347-133">Table operations involving entities are done using the **CloudTable** object that you created earlier in "Access tables in code."</span></span> <span data-ttu-id="7f347-134">L'oggetto **TableOperation** rappresenta l'operazione da eseguire.</span><span class="sxs-lookup"><span data-stu-id="7f347-134">The **TableOperation** object represents the operation to be done.</span></span> <span data-ttu-id="7f347-135">L'esempio di codice seguente mostra come creare un oggetto **CloudTable** e un oggetto **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="7f347-135">The following code example shows how to create a **CloudTable** object and a **CustomerEntity** object.</span></span> <span data-ttu-id="7f347-136">Per preparare l'operazione, viene creato un oggetto **TableOperation** per inserire l'entità customer nella tabella.</span><span class="sxs-lookup"><span data-stu-id="7f347-136">To prepare the operation, a **TableOperation** is created to insert the customer entity into the table.</span></span> <span data-ttu-id="7f347-137">Infine, per eseguire l'operazione viene chiamato **CloudTable.ExecuteAsync**.</span><span class="sxs-lookup"><span data-stu-id="7f347-137">Finally, the operation is executed by calling **CloudTable.ExecuteAsync**.</span></span>

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create the TableOperation that inserts the customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute the insert operation.
    await peopleTable.ExecuteAsync(insertOperation);


## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="7f347-138">Inserire un batch di entità</span><span class="sxs-lookup"><span data-stu-id="7f347-138">Insert a batch of entities</span></span>
<span data-ttu-id="7f347-139">È possibile inserire più entità in una tabella in una singola operazione di scrittura.</span><span class="sxs-lookup"><span data-stu-id="7f347-139">You can insert multiple entities into a table in a single write operation.</span></span> <span data-ttu-id="7f347-140">L'esempio di codice seguente crea due oggetti entità ("Jeff Smith" e "Ben Smith"), li aggiunge a un oggetto **TableBatchOperation** usando il metodo Insert, quindi avvia l'operazione richiamando **CloudTable.ExecuteBatchAsync**.</span><span class="sxs-lookup"><span data-stu-id="7f347-140">The following code example creates two entity objects ("Jeff Smith" and "Ben Smith"), adds them to a **TableBatchOperation** object using the Insert method, and then starts the operation by calling **CloudTable.ExecuteBatchAsync**.</span></span>

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

## <a name="get-all-of-the-entities-in-a-partition"></a><span data-ttu-id="7f347-141">Ottenere tutte le entità di una partizione</span><span class="sxs-lookup"><span data-stu-id="7f347-141">Get all of the entities in a partition</span></span>
<span data-ttu-id="7f347-142">Per eseguire una query su una tabella e recuperare tutte le entità di una partizione, usare un oggetto **TableQuery** .</span><span class="sxs-lookup"><span data-stu-id="7f347-142">To query a table for all of the entities in a partition, use a **TableQuery** object.</span></span> <span data-ttu-id="7f347-143">Nell'esempio di codice seguente viene specificato un filtro per le entità in cui la chiave di partizione è 'Smith'.</span><span class="sxs-lookup"><span data-stu-id="7f347-143">The following code example specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="7f347-144">Questo esempio consente di stampare sulla console i campi di ogni entità inclusa nei risultati della query.</span><span class="sxs-lookup"><span data-stu-id="7f347-144">This example prints the fields of each entity in the query results to the console.</span></span>

    // Construct the query operation for all customer entities where PartitionKey="Smith".
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

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

    return View();


## <a name="get-a-single-entity"></a><span data-ttu-id="7f347-145">Ottenere una singola entità</span><span class="sxs-lookup"><span data-stu-id="7f347-145">Get a single entity</span></span>
<span data-ttu-id="7f347-146">È possibile scrivere una query per ottenere una singola entità specifica.</span><span class="sxs-lookup"><span data-stu-id="7f347-146">You can write a query to get a single, specific entity.</span></span> <span data-ttu-id="7f347-147">Il codice seguente usa un oggetto **TableOperation** per specificare un cliente denominato 'Ben Smith'.</span><span class="sxs-lookup"><span data-stu-id="7f347-147">The following code uses a **TableOperation** object to specify a customer named 'Ben Smith'.</span></span> <span data-ttu-id="7f347-148">Questo metodo restituisce solo un'entità, anziché una raccolta, e il valore restituito in **TableResult.Result** è un oggetto **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="7f347-148">This method returns just one entity, rather than a collection, and the returned value in **TableResult.Result** is a **CustomerEntity** object.</span></span> <span data-ttu-id="7f347-149">La specifica delle chiavi di partizione e di riga in una query costituisce la soluzione più rapida per recuperare una singola entità dal servizio **tabelle** .</span><span class="sxs-lookup"><span data-stu-id="7f347-149">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the **Table** service.</span></span>

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute the retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print the phone number of the result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("The phone number could not be retrieved.");

## <a name="delete-an-entity"></a><span data-ttu-id="7f347-150">Eliminare un'entità</span><span class="sxs-lookup"><span data-stu-id="7f347-150">Delete an entity</span></span>
<span data-ttu-id="7f347-151">È possibile eliminare un'entità dopo averla individuata.</span><span class="sxs-lookup"><span data-stu-id="7f347-151">You can delete an entity after you find it.</span></span> <span data-ttu-id="7f347-152">Il codice seguente cerca un'entità customer denominata "Ben Smith" e, se la trova, la elimina.</span><span class="sxs-lookup"><span data-stu-id="7f347-152">The following code looks for a customer entity named "Ben Smith", and if it finds it, it deletes it.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="7f347-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7f347-153">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

