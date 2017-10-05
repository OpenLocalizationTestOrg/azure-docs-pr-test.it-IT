---
title: Introduzione all'archiviazione tabelle di Azure con .NET | Documentazione Microsoft
description: Archiviare dati non strutturati nel cloud con il servizio di archiviazione tabelle di Azure, ovvero un archivio dati NoSQL.
services: storage
documentationcenter: .net
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: fe46d883-7bed-49dd-980e-5c71df36adb3
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 04/10/2017
ms.author: marsma
ms.openlocfilehash: 16a9dad1b01fdbef5ec8949bf9ff25497f33d994
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-table-storage-using-net"></a><span data-ttu-id="ee863-103">Introduzione all'archiviazione tabelle di Azure con .NET</span><span class="sxs-lookup"><span data-stu-id="ee863-103">Get started with Azure Table storage using .NET</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

<span data-ttu-id="ee863-104">L'archiviazione tabelle di Azure è un servizio che archivia dati NoSQL strutturati nel cloud, mettendo a disposizione un archivio di chiavi/attributi senza schema.</span><span class="sxs-lookup"><span data-stu-id="ee863-104">Azure Table storage is a service that stores structured NoSQL data in the cloud, providing a key/attribute store with a schemaless design.</span></span> <span data-ttu-id="ee863-105">Poiché l'archiviazione tabelle è senza schema, è facile adattare i dati con il variare delle esigenze dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ee863-105">Because Table storage is schemaless, it's easy to adapt your data as the needs of your application evolve.</span></span> <span data-ttu-id="ee863-106">L'accesso ai dati dell'archiviazione tabelle è rapido ed economico per molti tipi di applicazioni e presenta costi generalmente più bassi rispetto alle soluzioni SQL tradizionali per volumi di dati simili.</span><span class="sxs-lookup"><span data-stu-id="ee863-106">Access to Table storage data is fast and cost-effective for many types of applications, and is typically lower in cost than traditional SQL for similar volumes of data.</span></span>

<span data-ttu-id="ee863-107">È possibile usare l'archiviazione tabelle per archiviare set di dati flessibili, ad esempio i dati utente per le applicazioni Web, le rubriche, le informazioni sui dispositivi o altri tipi di metadati richiesti dal servizio.</span><span class="sxs-lookup"><span data-stu-id="ee863-107">You can use Table storage to store flexible datasets like user data for web applications, address books, device information, or other types of metadata your service requires.</span></span> <span data-ttu-id="ee863-108">In una tabella possono essere archiviate il numero desiderato di tabelle e un account di archiviazione può contenere un numero qualsiasi di tabelle, fino a che non viene raggiunto il limite di capacità dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ee863-108">You can store any number of entities in a table, and a storage account may contain any number of tables, up to the capacity limit of the storage account.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="ee863-109">Informazioni sull'esercitazione</span><span class="sxs-lookup"><span data-stu-id="ee863-109">About this tutorial</span></span>
<span data-ttu-id="ee863-110">Questa esercitazione illustra come usare la [libreria client di archiviazione di Azure per .NET](https://www.nuget.org/packages/WindowsAzure.Storage/) in alcuni scenari comuni dell'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="ee863-110">This tutorial shows you how to use the [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/) in some common Azure Table storage scenarios.</span></span> <span data-ttu-id="ee863-111">Gli scenari vengono presentati con esempi C# per la creazione ed eliminazione di una tabella e l'inserimento, l'aggiornamento, l'eliminazione e l'esecuzione di query per i dati delle tabelle.</span><span class="sxs-lookup"><span data-stu-id="ee863-111">These scenarios are presented using C# examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ee863-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ee863-112">Prerequisites</span></span>

<span data-ttu-id="ee863-113">Per completare l'esercitazione sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ee863-113">You need the following to complete this tutorial successfully:</span></span>

* [<span data-ttu-id="ee863-114">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ee863-114">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="ee863-115">Libreria client di archiviazione di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="ee863-115">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="ee863-116">Gestione configurazione di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="ee863-116">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* [<span data-ttu-id="ee863-117">Account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="ee863-117">Azure storage account</span></span>](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a><span data-ttu-id="ee863-118">Altri esempi</span><span class="sxs-lookup"><span data-stu-id="ee863-118">More samples</span></span>
<span data-ttu-id="ee863-119">Per altri esempi di uso dell'archivio tabelle, vedere [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)(Introduzione all'archivio tabelle di Azure in .NET).</span><span class="sxs-lookup"><span data-stu-id="ee863-119">For additional examples using Table storage, see [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/).</span></span> <span data-ttu-id="ee863-120">È possibile scaricare l'applicazione di esempio ed eseguirla oppure esaminare il codice in GitHub.</span><span class="sxs-lookup"><span data-stu-id="ee863-120">You can download the sample application and run it, or browse the code on GitHub.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="ee863-121">Aggiungere le direttive using</span><span class="sxs-lookup"><span data-stu-id="ee863-121">Add using directives</span></span>
<span data-ttu-id="ee863-122">Aggiungere le direttive **using** seguenti all'inizio del file `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="ee863-122">Add the following **using** directives to the top of the `Program.cs` file:</span></span>

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Table; // Namespace for Table storage types
```

### <a name="parse-the-connection-string"></a><span data-ttu-id="ee863-123">Analizzare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="ee863-123">Parse the connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-the-table-service-client"></a><span data-ttu-id="ee863-124">Creare il client del servizio tabelle</span><span class="sxs-lookup"><span data-stu-id="ee863-124">Create the Table service client</span></span>
<span data-ttu-id="ee863-125">La classe [CloudTableClient][dotnet_CloudTableClient] consente di recuperare le tabelle e le entità archiviate nell'archiviazione tabelle.</span><span class="sxs-lookup"><span data-stu-id="ee863-125">The [CloudTableClient][dotnet_CloudTableClient] class enables you to retrieve tables and entities stored in Table storage.</span></span> <span data-ttu-id="ee863-126">Di seguito è illustrato un modo per creare il client del servizio tabelle:</span><span class="sxs-lookup"><span data-stu-id="ee863-126">Here's one way to create the Table service client:</span></span>

```csharp
// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```

<span data-ttu-id="ee863-127">A questo punto si è pronti a scrivere codice che legge e scrive i dati nell'archivio tabelle.</span><span class="sxs-lookup"><span data-stu-id="ee863-127">Now you are ready to write code that reads data from and writes data to Table storage.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="ee863-128">Creare una tabella</span><span class="sxs-lookup"><span data-stu-id="ee863-128">Create a table</span></span>
<span data-ttu-id="ee863-129">Questo esempio illustra come creare una tabella, se non esiste già:</span><span class="sxs-lookup"><span data-stu-id="ee863-129">This example shows how to create a table if it does not already exist:</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Retrieve a reference to the table.
CloudTable table = tableClient.GetTableReference("people");

// Create the table if it doesn't exist.
table.CreateIfNotExists();
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="ee863-130">Aggiungere un'entità a una tabella</span><span class="sxs-lookup"><span data-stu-id="ee863-130">Add an entity to a table</span></span>
<span data-ttu-id="ee863-131">Per eseguire il mapping di entità a oggetti C# viene usata una classe personalizzata derivata da [TableEntity][dotnet_TableEntity].</span><span class="sxs-lookup"><span data-stu-id="ee863-131">Entities map to C# objects by using a custom class derived from [TableEntity][dotnet_TableEntity].</span></span> <span data-ttu-id="ee863-132">Per aggiungere un'entità a una classe, creare una classe che definisca le proprietà dell'entità.</span><span class="sxs-lookup"><span data-stu-id="ee863-132">To add an entity to a table, create a class that defines the properties of your entity.</span></span> <span data-ttu-id="ee863-133">Il codice seguente consente di definire una classe di entità che utilizza il nome e il cognome del cliente rispettivamente come chiave di riga e chiave di partizione.</span><span class="sxs-lookup"><span data-stu-id="ee863-133">The following code defines an entity class that uses the customer's first name as the row key and last name as the partition key.</span></span> <span data-ttu-id="ee863-134">La partizione e la chiave di riga di un'entità consentono di identificare in modo univoco l'entità nella tabella.</span><span class="sxs-lookup"><span data-stu-id="ee863-134">Together, an entity's partition and row key uniquely identify it in the table.</span></span> <span data-ttu-id="ee863-135">Le query su entità con la stessa chiave di partizione vengono eseguite più rapidamente di quelle con chiavi di partizione diverse, tuttavia l'uso di chiavi di partizione diverse assicura una maggiore scalabilità delle operazioni parallele.</span><span class="sxs-lookup"><span data-stu-id="ee863-135">Entities with the same partition key can be queried faster than entities with different partition keys, but using diverse partition keys allows for greater scalability of parallel operations.</span></span> <span data-ttu-id="ee863-136">Le entità da archiviare nelle tabelle devono essere di un tipo supportato, ad esempio derivato dalla classe [TableEntity][dotnet_TableEntity].</span><span class="sxs-lookup"><span data-stu-id="ee863-136">Entities to be stored in tables must be of a supported type, for example derived from the [TableEntity][dotnet_TableEntity] class.</span></span> <span data-ttu-id="ee863-137">Le proprietà dell'entità da archiviare in una tabella devono essere proprietà pubbliche del tipo e supportare sia l'ottenimento che l'impostazione di valori.</span><span class="sxs-lookup"><span data-stu-id="ee863-137">Entity properties you'd like to store in a table must be public properties of the type, and support both getting and setting of values.</span></span> <span data-ttu-id="ee863-138">Il tipo di entità *deve* inoltre esporre un costruttore senza parametri.</span><span class="sxs-lookup"><span data-stu-id="ee863-138">Also, your entity type *must* expose a parameter-less constructor.</span></span>

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

    public string PhoneNumber { get; set; }
}
```

<span data-ttu-id="ee863-139">Le operazioni su tabella che interessano le entità vengono eseguite tramite l'oggetto [CloudTable][dotnet_CloudTable] creato precedentemente nella sezione "Creare una tabella".</span><span class="sxs-lookup"><span data-stu-id="ee863-139">Table operations that involve entities are performed via the [CloudTable][dotnet_CloudTable] object that you created earlier in the "Create a table" section.</span></span> <span data-ttu-id="ee863-140">L'operazione da eseguire è rappresentata da un oggetto [TableOperation][dotnet_TableOperation].</span><span class="sxs-lookup"><span data-stu-id="ee863-140">The operation to be performed is represented by a [TableOperation][dotnet_TableOperation] object.</span></span> <span data-ttu-id="ee863-141">L'esempio di codice seguente illustra la creazione dell'oggetto [CloudTable][dotnet_CloudTable] e quindi di un oggetto **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="ee863-141">The following code example shows the creation of the [CloudTable][dotnet_CloudTable] object and then a **CustomerEntity** object.</span></span> <span data-ttu-id="ee863-142">Per preparare l'operazione, viene creato un oggetto [TableOperation][dotnet_TableOperation] per inserire l'entità customer nella tabella.</span><span class="sxs-lookup"><span data-stu-id="ee863-142">To prepare the operation, a [TableOperation][dotnet_TableOperation] object is created to insert the customer entity into the table.</span></span> <span data-ttu-id="ee863-143">L'operazione viene infine eseguita chiamando [CloudTable][dotnet_CloudTable].[Execute][dotnet_CloudTable_Execute].</span><span class="sxs-lookup"><span data-stu-id="ee863-143">Finally, the operation is executed by calling [CloudTable][dotnet_CloudTable].[Execute][dotnet_CloudTable_Execute].</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create the TableOperation object that inserts the customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute the insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="ee863-144">Inserire un batch di entità</span><span class="sxs-lookup"><span data-stu-id="ee863-144">Insert a batch of entities</span></span>
<span data-ttu-id="ee863-145">Per inserire un batch di entità in una tabella, è possibile usare un'unica operazione di scrittura.</span><span class="sxs-lookup"><span data-stu-id="ee863-145">You can insert a batch of entities into a table in one write operation.</span></span> <span data-ttu-id="ee863-146">Di seguito sono riportate altre informazioni sulle operazioni batch:</span><span class="sxs-lookup"><span data-stu-id="ee863-146">Some other notes on batch operations:</span></span>

* <span data-ttu-id="ee863-147">È possibile utilizzare una singola operazione batch per eseguire operazioni di aggiornamento, eliminazione e inserimento.</span><span class="sxs-lookup"><span data-stu-id="ee863-147">You can perform updates, deletes, and inserts in the same single batch operation.</span></span>
* <span data-ttu-id="ee863-148">Una singola operazione batch può includere fino a 100 entità.</span><span class="sxs-lookup"><span data-stu-id="ee863-148">A single batch operation can include up to 100 entities.</span></span>
* <span data-ttu-id="ee863-149">A tutte le entità di una singola operazione batch deve essere associata la stessa chiave di partizione.</span><span class="sxs-lookup"><span data-stu-id="ee863-149">All entities in a single batch operation must have the same partition key.</span></span>
* <span data-ttu-id="ee863-150">È possibile eseguire una query come operazione batch, ma deve essere l'unica operazione del batch.</span><span class="sxs-lookup"><span data-stu-id="ee863-150">While it is possible to perform a query as a batch operation, it must be the only operation in the batch.</span></span>

<span data-ttu-id="ee863-151">L'esempio di codice seguente consente di creare due oggetti entità e di aggiungere ciascuno a un oggetto [TableBatchOperation][dotnet_TableBatchOperation] usando il metodo [Insert][dotnet_TableBatchOperation_Insert].</span><span class="sxs-lookup"><span data-stu-id="ee863-151">The following code example creates two entity objects and adds each to [TableBatchOperation][dotnet_TableBatchOperation] by using the [Insert][dotnet_TableBatchOperation_Insert] method.</span></span> <span data-ttu-id="ee863-152">Per eseguire l'operazione viene quindi chiamato [CloudTable][dotnet_CloudTable].[ExecuteBatch][dotnet_CloudTable_ExecuteBatch].</span><span class="sxs-lookup"><span data-stu-id="ee863-152">Then, [CloudTable][dotnet_CloudTable].[ExecuteBatch][dotnet_CloudTable_ExecuteBatch] is called to execute the operation.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

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
table.ExecuteBatch(batchOperation);
```

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="ee863-153">Recuperare tutte le entità di una partizione</span><span class="sxs-lookup"><span data-stu-id="ee863-153">Retrieve all entities in a partition</span></span>
<span data-ttu-id="ee863-154">Per eseguire una query su una tabella e recuperare tutte le entità di una partizione, usare un oggetto [TableQuery][dotnet_TableQuery].</span><span class="sxs-lookup"><span data-stu-id="ee863-154">To query a table for all entities in a partition, use a [TableQuery][dotnet_TableQuery] object.</span></span> <span data-ttu-id="ee863-155">Nell'esempio di codice seguente viene specificato un filtro per le entità in cui la chiave di partizione è 'Smith'.</span><span class="sxs-lookup"><span data-stu-id="ee863-155">The following code example specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="ee863-156">Questo esempio consente di stampare sulla console i campi di ogni entità inclusa nei risultati della query.</span><span class="sxs-lookup"><span data-stu-id="ee863-156">This example prints the fields of each entity in the query results to the console.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Construct the query operation for all customer entities where PartitionKey="Smith".
TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>().Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

// Print the fields for each customer.
foreach (CustomerEntity entity in table.ExecuteQuery(query))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

## <a name="retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="ee863-157">Recuperare un intervallo di entità in una partizione</span><span class="sxs-lookup"><span data-stu-id="ee863-157">Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="ee863-158">Se non si vuole eseguire una query su tutte le entità di una partizione, è possibile specificare un intervallo combinando il filtro della chiave di partizione con quello della chiave di riga.</span><span class="sxs-lookup"><span data-stu-id="ee863-158">If you don't want to query all entities in a partition, you can specify a range by combining the partition key filter with a row key filter.</span></span> <span data-ttu-id="ee863-159">L'esempio di codice seguente usa due filtri per recuperare tutte le entità della partizione 'Smith' in cui la chiave di riga (nome) inizia con una lettera che precede la 'E' nell'alfabeto. Stampa quindi i risultati della query.</span><span class="sxs-lookup"><span data-stu-id="ee863-159">The following code example uses two filters to get all entities in partition 'Smith' where the row key (first name) starts with a letter before 'E' in the alphabet, then prints the query results.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create the table query.
TableQuery<CustomerEntity> rangeQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.CombineFilters(
        TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"),
        TableOperators.And,
        TableQuery.GenerateFilterCondition("RowKey", QueryComparisons.LessThan, "E")));

// Loop through the results, displaying information about the entity.
foreach (CustomerEntity entity in table.ExecuteQuery(rangeQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="ee863-160">Recuperare una singola entità</span><span class="sxs-lookup"><span data-stu-id="ee863-160">Retrieve a single entity</span></span>
<span data-ttu-id="ee863-161">Per recuperare una singola entità specifica, è possibile scrivere una query.</span><span class="sxs-lookup"><span data-stu-id="ee863-161">You can write a query to retrieve a single, specific entity.</span></span> <span data-ttu-id="ee863-162">Il codice seguente usa [TableOperation][dotnet_TableOperation] per specificare il cliente 'Ben Smith'.</span><span class="sxs-lookup"><span data-stu-id="ee863-162">The following code uses [TableOperation][dotnet_TableOperation] to specify the customer 'Ben Smith'.</span></span> <span data-ttu-id="ee863-163">Questo metodo restituisce una sola entità anziché una raccolta e il valore restituito in [TableResult][dotnet_TableResult].[Result][dotnet_TableResult_Result] è un oggetto **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="ee863-163">This method returns just one entity rather than a collection, and the returned value in [TableResult][dotnet_TableResult].[Result][dotnet_TableResult_Result] is a **CustomerEntity** object.</span></span> <span data-ttu-id="ee863-164">La specifica delle chiavi di partizione e di riga in una query costituisce la soluzione più rapida per recuperare una singola entità dal servizio tabelle.</span><span class="sxs-lookup"><span data-stu-id="ee863-164">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the Table service.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Print the phone number of the result.
if (retrievedResult.Result != null)
{
    Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
}
else
{
    Console.WriteLine("The phone number could not be retrieved.");
}
```

## <a name="replace-an-entity"></a><span data-ttu-id="ee863-165">Sostituire un'entità</span><span class="sxs-lookup"><span data-stu-id="ee863-165">Replace an entity</span></span>
<span data-ttu-id="ee863-166">Per aggiornare un'entità, recuperarla dal servizio tabelle, modificare l'oggetto entità e quindi salvare le modifiche nel servizio tabelle.</span><span class="sxs-lookup"><span data-stu-id="ee863-166">To update an entity, retrieve it from the Table service, modify the entity object, and then save the changes back to the Table service.</span></span> <span data-ttu-id="ee863-167">Il codice seguente consente di modificare il numero di telefono di un cliente esistente.</span><span class="sxs-lookup"><span data-stu-id="ee863-167">The following code changes an existing customer's phone number.</span></span> <span data-ttu-id="ee863-168">Invece di una chiamata a [Insert][dotnet_TableOperation_Insert], nel codice viene usato [Replace][dotnet_TableOperation_Replace].</span><span class="sxs-lookup"><span data-stu-id="ee863-168">Instead of calling [Insert][dotnet_TableOperation_Insert], this code uses [Replace][dotnet_TableOperation_Replace].</span></span> <span data-ttu-id="ee863-169">Con [Replace][dotnet_TableOperation_Replace], l'entità viene completamente sostituita nel server, a meno che non sia stata modificata dopo essere stata recuperata.</span><span class="sxs-lookup"><span data-stu-id="ee863-169">[Replace][dotnet_TableOperation_Replace] causes the entity to be fully replaced on the server, unless the entity on the server has changed since it was retrieved, in which case the operation will fail.</span></span> <span data-ttu-id="ee863-170">In questo caso, infatti, l'operazione non viene eseguita per impedire all'applicazione di sovrascrivere inavvertitamente una modifica effettuata tra il recupero e l'aggiornamento da parte di un altro componente dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ee863-170">This failure is to prevent your application from inadvertently overwriting a change made between the retrieval and update by another component of your application.</span></span> <span data-ttu-id="ee863-171">Per risolvere questo errore, recuperare di nuovo l'entità, apportare le modifiche, se ancora valide, quindi eseguire un'altra operazione [Replace][dotnet_TableOperation_Replace].</span><span class="sxs-lookup"><span data-stu-id="ee863-171">The proper handling of this failure is to retrieve the entity again, make your changes (if still valid), and then perform another [Replace][dotnet_TableOperation_Replace] operation.</span></span> <span data-ttu-id="ee863-172">La sezione successiva illustra come ovviare a questo comportamento.</span><span class="sxs-lookup"><span data-stu-id="ee863-172">The next section will show you how to override this behavior.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Assign the result to a CustomerEntity object.
CustomerEntity updateEntity = (CustomerEntity)retrievedResult.Result;

if (updateEntity != null)
{
    // Change the phone number.
    updateEntity.PhoneNumber = "425-555-0105";

    // Create the Replace TableOperation.
    TableOperation updateOperation = TableOperation.Replace(updateEntity);

    // Execute the operation.
    table.Execute(updateOperation);

    Console.WriteLine("Entity updated.");
}
else
{
    Console.WriteLine("Entity could not be retrieved.");
}
```

## <a name="insert-or-replace-an-entity"></a><span data-ttu-id="ee863-173">Inserire o sostituire un'entità</span><span class="sxs-lookup"><span data-stu-id="ee863-173">Insert-or-replace an entity</span></span>
<span data-ttu-id="ee863-174">Le operazioni [Replace][dotnet_TableOperation_Replace] non vengono eseguite se l'entità è stata modificata dopo essere stata recuperata dal server.</span><span class="sxs-lookup"><span data-stu-id="ee863-174">[Replace][dotnet_TableOperation_Replace] operations will fail if the entity has been changed since it was retrieved from the server.</span></span> <span data-ttu-id="ee863-175">Per la corretta esecuzione dell'operazione [Replace][dotnet_TableOperation_Replace] è anche necessario recuperare prima l'entità dal server.</span><span class="sxs-lookup"><span data-stu-id="ee863-175">Furthermore, you must retrieve the entity from the server first in order for the [Replace][dotnet_TableOperation_Replace] operation to be successful.</span></span> <span data-ttu-id="ee863-176">In alcuni casi, tuttavia, non è noto se l'entità è già esistente nel server e i valori in essa archiviati sono irrilevanti,</span><span class="sxs-lookup"><span data-stu-id="ee863-176">Sometimes, however, you don't know if the entity exists on the server and the current values stored in it are irrelevant.</span></span> <span data-ttu-id="ee863-177">pertanto devono essere sovrascritti completamente dall'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="ee863-177">Your update should overwrite them all.</span></span> <span data-ttu-id="ee863-178">A tale scopo è necessario usare un'operazione [InsertOrReplace][dotnet_TableOperation_InsertOrReplace].</span><span class="sxs-lookup"><span data-stu-id="ee863-178">To accomplish this, you would use an [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] operation.</span></span> <span data-ttu-id="ee863-179">Questa operazione inserisce l'entità se non è già esistente oppure la sostituisce se esiste già, indipendentemente dalla data dell'ultimo aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="ee863-179">This operation inserts the entity if it doesn't exist, or replaces it if it does, regardless of when the last update was made.</span></span>

<span data-ttu-id="ee863-180">Nell'esempio di codice seguente, viene creata e inserita nella tabella 'people' un'entità customer per 'Fred Jones'.</span><span class="sxs-lookup"><span data-stu-id="ee863-180">In the following code example, a customer entity for 'Fred Jones' is created and inserted into the 'people' table.</span></span> <span data-ttu-id="ee863-181">Viene quindi usata l'operazione [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] per salvare nel server un'entità con la stessa chiave di partizione (Jones) e chiave di riga (Fred), questa volta con un valore diverso per la proprietà PhoneNumber.</span><span class="sxs-lookup"><span data-stu-id="ee863-181">Next, we use the [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] operation to save an entity with the same partition key (Jones) and row key (Fred) to the server, this time with a different value for the PhoneNumber property.</span></span> <span data-ttu-id="ee863-182">Dato che si usa [InsertOrReplace][dotnet_TableOperation_InsertOrReplace], tutti i valori delle proprietà vengono sostituiti.</span><span class="sxs-lookup"><span data-stu-id="ee863-182">Because we use [InsertOrReplace][dotnet_TableOperation_InsertOrReplace], all of its property values are replaced.</span></span> <span data-ttu-id="ee863-183">Se tuttavia un'entità 'Fred Jones' non fosse già esistita nella tabella, sarebbe stata inserita.</span><span class="sxs-lookup"><span data-stu-id="ee863-183">However, if a 'Fred Jones' entity hadn't already existed in the table, it would have been inserted.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a customer entity.
CustomerEntity customer3 = new CustomerEntity("Jones", "Fred");
customer3.Email = "Fred@contoso.com";
customer3.PhoneNumber = "425-555-0106";

// Create the TableOperation object that inserts the customer entity.
TableOperation insertOperation = TableOperation.Insert(customer3);

// Execute the operation.
table.Execute(insertOperation);

// Create another customer entity with the same partition key and row key.
// We've already created a 'Fred Jones' entity and saved it to the
// 'people' table, but here we're specifying a different value for the
// PhoneNumber property.
CustomerEntity customer4 = new CustomerEntity("Jones", "Fred");
customer4.Email = "Fred@contoso.com";
customer4.PhoneNumber = "425-555-0107";

// Create the InsertOrReplace TableOperation.
TableOperation insertOrReplaceOperation = TableOperation.InsertOrReplace(customer4);

// Execute the operation. Because a 'Fred Jones' entity already exists in the
// 'people' table, its property values will be overwritten by those in this
// CustomerEntity. If 'Fred Jones' didn't already exist, the entity would be
// added to the table.
table.Execute(insertOrReplaceOperation);
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="ee863-184">Eseguire query su un subset di proprietà di entità</span><span class="sxs-lookup"><span data-stu-id="ee863-184">Query a subset of entity properties</span></span>
<span data-ttu-id="ee863-185">Una query tabella consente di recuperare alcune proprietà da un'entità, ma non tutte.</span><span class="sxs-lookup"><span data-stu-id="ee863-185">A table query can retrieve just a few properties from an entity instead of all the entity properties.</span></span> <span data-ttu-id="ee863-186">Questa tecnica, denominata proiezione, consente di ridurre la larghezza di banda e di migliorare le prestazioni della query, in particolare per entità di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="ee863-186">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="ee863-187">La query nel codice seguente restituisce solo gli indirizzi di posta elettronica di entità nella tabella.</span><span class="sxs-lookup"><span data-stu-id="ee863-187">The query in the following code returns only the email addresses of entities in the table.</span></span> <span data-ttu-id="ee863-188">A tale scopo viene usata una query di [DynamicTableEntity][dotnet_DynamicTableEntity] e anche [EntityResolver][dotnet_EntityResolver].</span><span class="sxs-lookup"><span data-stu-id="ee863-188">This is done by using a query of [DynamicTableEntity][dotnet_DynamicTableEntity] and also [EntityResolver][dotnet_EntityResolver].</span></span> <span data-ttu-id="ee863-189">Per altre informazioni sulla proiezione, vedere il post di blog [Introducing Upsert and Query Projection][blog_post_upsert] (Introduzione di Upsert e proiezione di query).</span><span class="sxs-lookup"><span data-stu-id="ee863-189">You can learn more about projection in the [Introducing Upsert and Query Projection blog post][blog_post_upsert].</span></span> <span data-ttu-id="ee863-190">La proiezione non è supportata dall'emulatore di archiviazione, quindi questo codice viene eseguito solo se si usa un account nel servizio tabelle.</span><span class="sxs-lookup"><span data-stu-id="ee863-190">Projection is not supported by the storage emulator, so this code runs only when you're using an account in the Table service.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Define the query, and select only the Email property.
TableQuery<DynamicTableEntity> projectionQuery = new TableQuery<DynamicTableEntity>().Select(new string[] { "Email" });

// Define an entity resolver to work with the entity after retrieval.
EntityResolver<string> resolver = (pk, rk, ts, props, etag) => props.ContainsKey("Email") ? props["Email"].StringValue : null;

foreach (string projectedEmail in table.ExecuteQuery(projectionQuery, resolver, null, null))
{
    Console.WriteLine(projectedEmail);
}
```

## <a name="delete-an-entity"></a><span data-ttu-id="ee863-191">Eliminare un'entità</span><span class="sxs-lookup"><span data-stu-id="ee863-191">Delete an entity</span></span>
<span data-ttu-id="ee863-192">Per eliminare facilmente un'entità dopo averla recuperata, è possibile usare lo stesso modello illustrato per aggiornare un'entità.</span><span class="sxs-lookup"><span data-stu-id="ee863-192">You can easily delete an entity after you have retrieved it by using the same pattern shown for updating an entity.</span></span> <span data-ttu-id="ee863-193">Il codice seguente consente di recuperare ed eliminare un'entità customer.</span><span class="sxs-lookup"><span data-stu-id="ee863-193">The following code retrieves and deletes a customer entity.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that expects a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Assign the result to a CustomerEntity.
CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

// Create the Delete TableOperation.
if (deleteEntity != null)
{
    TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

    // Execute the operation.
    table.Execute(deleteOperation);

    Console.WriteLine("Entity deleted.");
}
else
{
    Console.WriteLine("Could not retrieve the entity.");
}
```

## <a name="delete-a-table"></a><span data-ttu-id="ee863-194">Eliminare una tabella</span><span class="sxs-lookup"><span data-stu-id="ee863-194">Delete a table</span></span>
<span data-ttu-id="ee863-195">L'esempio di codice seguente consente infine di eliminare una tabella dall'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ee863-195">Finally, the following code example deletes a table from a storage account.</span></span> <span data-ttu-id="ee863-196">Una tabella eliminata non potrà essere creata nuovamente per un certo periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="ee863-196">A table that has been deleted will be unavailable to be re-created for a period of time following the deletion.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Delete the table it if exists.
table.DeleteIfExists();
```

## <a name="retrieve-entities-in-pages-asynchronously"></a><span data-ttu-id="ee863-197">Recuperare entità nelle pagine in modo asincrono</span><span class="sxs-lookup"><span data-stu-id="ee863-197">Retrieve entities in pages asynchronously</span></span>
<span data-ttu-id="ee863-198">Se si legge un numero elevato di entità e si desidera elaborare/visualizzare le entità man mano che vengono recuperate anziché attendere che vengano tutte restituite, è possibile recuperare le entità utilizzando una query segmentata.</span><span class="sxs-lookup"><span data-stu-id="ee863-198">If you are reading a large number of entities, and you want to process/display entities as they are retrieved rather than waiting for them all to return, you can retrieve entities by using a segmented query.</span></span> <span data-ttu-id="ee863-199">In questo esempio viene spiegato come restituire i risultati nelle pagine utilizzando il modello Async-Await, in modo che l'esecuzione non venga bloccata durante l'attesa della restituzione di un set di risultati di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="ee863-199">This example shows how to return results in pages by using the Async-Await pattern so that execution is not blocked while you're waiting for a large set of results to return.</span></span> <span data-ttu-id="ee863-200">Per ulteriori informazioni sull'utilizzo del modello Async-Await in .NET, vedere [Programmazione asincrona con Async e Await (C# e Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).</span><span class="sxs-lookup"><span data-stu-id="ee863-200">For more details on using the Async-Await pattern in .NET, see [Asynchronous programming with Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).</span></span>

```csharp
// Initialize a default TableQuery to retrieve all the entities in the table.
TableQuery<CustomerEntity> tableQuery = new TableQuery<CustomerEntity>();

// Initialize the continuation token to null to start from the beginning of the table.
TableContinuationToken continuationToken = null;

do
{
    // Retrieve a segment (up to 1,000 entities).
    TableQuerySegment<CustomerEntity> tableQueryResult =
        await table.ExecuteQuerySegmentedAsync(tableQuery, continuationToken);

    // Assign the new continuation token to tell the service where to
    // continue on the next iteration (or null if it has reached the end).
    continuationToken = tableQueryResult.ContinuationToken;

    // Print the number of rows retrieved.
    Console.WriteLine("Rows retrieved {0}", tableQueryResult.Results.Count);

// Loop until a null continuation token is received, indicating the end of the table.
} while(continuationToken != null);
```

## <a name="next-steps"></a><span data-ttu-id="ee863-201">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ee863-201">Next steps</span></span>
<span data-ttu-id="ee863-202">A questo punto, dopo aver appreso le nozioni di base dell'archiviazione tabelle, visitare i collegamenti seguenti per altre informazioni sulle attività di archiviazione più complesse:</span><span class="sxs-lookup"><span data-stu-id="ee863-202">Now that you've learned the basics of Table storage, follow these links to learn about more complex storage tasks:</span></span>

* <span data-ttu-id="ee863-203">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) è un'app autonoma gratuita di Microsoft che consente di rappresentare facilmente dati di Archiviazione di Azure in Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="ee863-203">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="ee863-204">Per altri esempi di archivio tabelle, vedere [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)</span><span class="sxs-lookup"><span data-stu-id="ee863-204">See more Table storage samples in [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)</span></span>
* <span data-ttu-id="ee863-205">Per informazioni dettagliate sulle API disponibili, vedere la documentazione di riferimento del servizio tabelle:</span><span class="sxs-lookup"><span data-stu-id="ee863-205">View the Table service reference documentation for complete details about available APIs:</span></span>
* [<span data-ttu-id="ee863-206">Informazioni di riferimento sulla libreria client di archiviazione per .NET</span><span class="sxs-lookup"><span data-stu-id="ee863-206">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
* [<span data-ttu-id="ee863-207">Informazioni di riferimento sulle API REST</span><span class="sxs-lookup"><span data-stu-id="ee863-207">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="ee863-208">Per altre informazioni su come semplificare il codice scritto da usare con Archiviazione di Azure, vedere [Informazioni su Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="ee863-208">Learn how to simplify the code you write to work with Azure Storage by using the [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)</span></span>
* <span data-ttu-id="ee863-209">Per ulteriori opzioni di archiviazione dei dati in Azure, consultare altre guide alle funzionalità.</span><span class="sxs-lookup"><span data-stu-id="ee863-209">View more feature guides to learn about additional options for storing data in Azure.</span></span>
* <span data-ttu-id="ee863-210">[Introduzione all'archivio BLOB di Azure con .NET](storage-dotnet-how-to-use-blobs.md) .</span><span class="sxs-lookup"><span data-stu-id="ee863-210">[Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) to store unstructured data.</span></span>
* <span data-ttu-id="ee863-211">Per archiviare i dati relazionali, vedere [Connettersi al database SQL tramite .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md).</span><span class="sxs-lookup"><span data-stu-id="ee863-211">[Connect to SQL Database by using .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) to store relational data.</span></span>

[Download and install the Azure SDK for .NET]: /develop/net/
[Creating an Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx

[blog_post_upsert]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx

[dotnet_api_ref]: https://msdn.microsoft.com/library/azure/mt347887.aspx
[dotnet_CloudTableClient]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtableclient.aspx
[dotnet_CloudTable]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtable.aspx
[dotnet_CloudTable_Execute]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtable.execute.aspx
[dotnet_CloudTable_ExecuteBatch]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtable.executebatch.aspx
[dotnet_DynamicTableEntity]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.dynamictableentity.aspx
[dotnet_EntityResolver]: https://msdn.microsoft.com/library/jj733144.aspx
[dotnet_TableBatchOperation]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablebatchoperation.aspx
[dotnet_TableBatchOperation_Insert]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablebatchoperation.insert.aspx
[dotnet_TableEntity]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableentity.aspx
[dotnet_TableOperation]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.aspx
[dotnet_TableOperation_Insert]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.insert.aspx
[dotnet_TableOperation_InsertOrReplace]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.insertorreplace.aspx
[dotnet_TableOperation_Replace]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.replace.aspx
[dotnet_TableQuery]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablequery.aspx
[dotnet_TableResult]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableresult.aspx
[dotnet_TableResult_Result]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableresult.result.aspx
