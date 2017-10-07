---
title: aaaGet avviato con l'archiviazione tabelle di Azure usando .NET | Documenti Microsoft
description: Archiviare dati strutturati in un cloud di hello tramite l'archiviazione tabelle di Azure, un archivio dati NoSQL.
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
ms.openlocfilehash: 9635079d61d874ff7f4bc9e7d610e0ad54b4fd6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-table-storage-using-net"></a><span data-ttu-id="a6699-103">Introduzione all'archiviazione tabelle di Azure con .NET</span><span class="sxs-lookup"><span data-stu-id="a6699-103">Get started with Azure Table storage using .NET</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

<span data-ttu-id="a6699-104">Archiviazione tabelle di Azure è un servizio che archivia NoSQL strutturati con una progettazione schemaless archiviano i dati nel cloud hello, fornendo una chiave o un attributo.</span><span class="sxs-lookup"><span data-stu-id="a6699-104">Azure Table storage is a service that stores structured NoSQL data in hello cloud, providing a key/attribute store with a schemaless design.</span></span> <span data-ttu-id="a6699-105">Poiché l'archiviazione tabelle è schemaless, è facile tooadapt i dati come hello necessita di evolve l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a6699-105">Because Table storage is schemaless, it's easy tooadapt your data as hello needs of your application evolve.</span></span> <span data-ttu-id="a6699-106">Accedere ai dati di archiviazione tooTable è veloce e conveniente per molti tipi di applicazioni e viene in genere inferiore costo SQL tradizionale per i volumi di dati simili.</span><span class="sxs-lookup"><span data-stu-id="a6699-106">Access tooTable storage data is fast and cost-effective for many types of applications, and is typically lower in cost than traditional SQL for similar volumes of data.</span></span>

<span data-ttu-id="a6699-107">È possibile utilizzare una tabella archiviazione toostore flessibile i set di dati come dati utente per applicazioni web, rubriche, informazioni sul dispositivo o altri tipi di metadati che del servizio richiede.</span><span class="sxs-lookup"><span data-stu-id="a6699-107">You can use Table storage toostore flexible datasets like user data for web applications, address books, device information, or other types of metadata your service requires.</span></span> <span data-ttu-id="a6699-108">È possibile archiviare qualsiasi numero di entità in una tabella e un account di archiviazione può contenere qualsiasi numero di tabelle, di limite di capacità toohello hello dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="a6699-108">You can store any number of entities in a table, and a storage account may contain any number of tables, up toohello capacity limit of hello storage account.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="a6699-109">Informazioni sull'esercitazione</span><span class="sxs-lookup"><span data-stu-id="a6699-109">About this tutorial</span></span>
<span data-ttu-id="a6699-110">In questa esercitazione illustra come hello toouse [Azure Storage Client Library per .NET](https://www.nuget.org/packages/WindowsAzure.Storage/) in alcuni scenari comuni di archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="a6699-110">This tutorial shows you how toouse hello [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/) in some common Azure Table storage scenarios.</span></span> <span data-ttu-id="a6699-111">Gli scenari vengono presentati con esempi C# per la creazione ed eliminazione di una tabella e l'inserimento, l'aggiornamento, l'eliminazione e l'esecuzione di query per i dati delle tabelle.</span><span class="sxs-lookup"><span data-stu-id="a6699-111">These scenarios are presented using C# examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a6699-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a6699-112">Prerequisites</span></span>

<span data-ttu-id="a6699-113">È necessario hello seguenti toocomplete questa esercitazione correttamente:</span><span class="sxs-lookup"><span data-stu-id="a6699-113">You need hello following toocomplete this tutorial successfully:</span></span>

* [<span data-ttu-id="a6699-114">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a6699-114">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="a6699-115">Libreria client di archiviazione di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="a6699-115">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="a6699-116">Gestione configurazione di Azure per .NET</span><span class="sxs-lookup"><span data-stu-id="a6699-116">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* [<span data-ttu-id="a6699-117">Account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="a6699-117">Azure storage account</span></span>](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a><span data-ttu-id="a6699-118">Altri esempi</span><span class="sxs-lookup"><span data-stu-id="a6699-118">More samples</span></span>
<span data-ttu-id="a6699-119">Per altri esempi di uso dell'archivio tabelle, vedere [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)(Introduzione all'archivio tabelle di Azure in .NET).</span><span class="sxs-lookup"><span data-stu-id="a6699-119">For additional examples using Table storage, see [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/).</span></span> <span data-ttu-id="a6699-120">È possibile scaricare l'applicazione di esempio hello ed eseguirlo o esaminare il codice hello su GitHub.</span><span class="sxs-lookup"><span data-stu-id="a6699-120">You can download hello sample application and run it, or browse hello code on GitHub.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="a6699-121">Aggiungere le direttive using</span><span class="sxs-lookup"><span data-stu-id="a6699-121">Add using directives</span></span>
<span data-ttu-id="a6699-122">Aggiungere il seguente hello **utilizzando** hello cima toohello direttive `Program.cs` file:</span><span class="sxs-lookup"><span data-stu-id="a6699-122">Add hello following **using** directives toohello top of hello `Program.cs` file:</span></span>

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Table; // Namespace for Table storage types
```

### <a name="parse-hello-connection-string"></a><span data-ttu-id="a6699-123">Analizzare la stringa di connessione hello</span><span class="sxs-lookup"><span data-stu-id="a6699-123">Parse hello connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-table-service-client"></a><span data-ttu-id="a6699-124">Creare i client del servizio tabelle hello</span><span class="sxs-lookup"><span data-stu-id="a6699-124">Create hello Table service client</span></span>
<span data-ttu-id="a6699-125">Hello [CloudTableClient] [ dotnet_CloudTableClient] classe consente tooretrieve tabelle ed entità archiviate nell'archiviazione tabelle.</span><span class="sxs-lookup"><span data-stu-id="a6699-125">hello [CloudTableClient][dotnet_CloudTableClient] class enables you tooretrieve tables and entities stored in Table storage.</span></span> <span data-ttu-id="a6699-126">Ecco un modo toocreate client del servizio tabelle hello:</span><span class="sxs-lookup"><span data-stu-id="a6699-126">Here's one way toocreate hello Table service client:</span></span>

```csharp
// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```

<span data-ttu-id="a6699-127">Si è ora pronto toowrite codice che legge i dati da e scrive tooTable archiviazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="a6699-127">Now you are ready toowrite code that reads data from and writes data tooTable storage.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="a6699-128">Creare una tabella</span><span class="sxs-lookup"><span data-stu-id="a6699-128">Create a table</span></span>
<span data-ttu-id="a6699-129">Questo esempio viene illustrato come toocreate una tabella se non esiste già:</span><span class="sxs-lookup"><span data-stu-id="a6699-129">This example shows how toocreate a table if it does not already exist:</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Retrieve a reference toohello table.
CloudTable table = tableClient.GetTableReference("people");

// Create hello table if it doesn't exist.
table.CreateIfNotExists();
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="a6699-130">Aggiungere una tabella tooa entità</span><span class="sxs-lookup"><span data-stu-id="a6699-130">Add an entity tooa table</span></span>
<span data-ttu-id="a6699-131">Entità di eseguire il mapping di oggetti tooC # utilizzando una classe personalizzata derivata da [TableEntity][dotnet_TableEntity].</span><span class="sxs-lookup"><span data-stu-id="a6699-131">Entities map tooC# objects by using a custom class derived from [TableEntity][dotnet_TableEntity].</span></span> <span data-ttu-id="a6699-132">tooadd tabella tooa un'entità, creare una classe che definisce le proprietà di hello dell'entità.</span><span class="sxs-lookup"><span data-stu-id="a6699-132">tooadd an entity tooa table, create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="a6699-133">Hello codice seguente definisce una classe di entità che utilizza nome hello del cliente come chiave di riga hello e last name come chiave di partizione hello.</span><span class="sxs-lookup"><span data-stu-id="a6699-133">hello following code defines an entity class that uses hello customer's first name as hello row key and last name as hello partition key.</span></span> <span data-ttu-id="a6699-134">Insieme, di partizione e chiave di riga identificarla in modo univoco nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="a6699-134">Together, an entity's partition and row key uniquely identify it in hello table.</span></span> <span data-ttu-id="a6699-135">Le entità con hello stessa chiave di partizione è possibile eseguire query più velocemente rispetto alle entità con diverse chiavi di partizione, ma con le chiavi di partizione diverse consente una maggiore scalabilità di operazioni parallele.</span><span class="sxs-lookup"><span data-stu-id="a6699-135">Entities with hello same partition key can be queried faster than entities with different partition keys, but using diverse partition keys allows for greater scalability of parallel operations.</span></span> <span data-ttu-id="a6699-136">Entità toobe archiviati nelle tabelle deve essere di un tipo supportato, ad esempio derivato da hello [TableEntity] [ dotnet_TableEntity] classe.</span><span class="sxs-lookup"><span data-stu-id="a6699-136">Entities toobe stored in tables must be of a supported type, for example derived from hello [TableEntity][dotnet_TableEntity] class.</span></span> <span data-ttu-id="a6699-137">Si desidera toostore in una tabella di proprietà dell'entità deve essere di proprietà pubbliche di tipo hello e supportano il recupero e impostazione dei valori.</span><span class="sxs-lookup"><span data-stu-id="a6699-137">Entity properties you'd like toostore in a table must be public properties of hello type, and support both getting and setting of values.</span></span> <span data-ttu-id="a6699-138">Il tipo di entità *deve* inoltre esporre un costruttore senza parametri.</span><span class="sxs-lookup"><span data-stu-id="a6699-138">Also, your entity type *must* expose a parameter-less constructor.</span></span>

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

<span data-ttu-id="a6699-139">Le operazioni di tabella che interessano le entità vengono eseguite tramite hello [CloudTable] [ dotnet_CloudTable] oggetto creato in precedenza nella sezione "Creazione di una tabella" hello.</span><span class="sxs-lookup"><span data-stu-id="a6699-139">Table operations that involve entities are performed via hello [CloudTable][dotnet_CloudTable] object that you created earlier in hello "Create a table" section.</span></span> <span data-ttu-id="a6699-140">Hello toobe operazione eseguita è rappresentato da un [TableOperation] [ dotnet_TableOperation] oggetto.</span><span class="sxs-lookup"><span data-stu-id="a6699-140">hello operation toobe performed is represented by a [TableOperation][dotnet_TableOperation] object.</span></span> <span data-ttu-id="a6699-141">Hello esempio di codice seguente viene illustrata hello creazione di hello [CloudTable] [ dotnet_CloudTable] oggetto e quindi un **CustomerEntity** oggetto.</span><span class="sxs-lookup"><span data-stu-id="a6699-141">hello following code example shows hello creation of hello [CloudTable][dotnet_CloudTable] object and then a **CustomerEntity** object.</span></span> <span data-ttu-id="a6699-142">operazione di hello tooprepare, un [TableOperation] [ dotnet_TableOperation] oggetto viene creato l'entità customer di tooinsert hello in tabella hello.</span><span class="sxs-lookup"><span data-stu-id="a6699-142">tooprepare hello operation, a [TableOperation][dotnet_TableOperation] object is created tooinsert hello customer entity into hello table.</span></span> <span data-ttu-id="a6699-143">Infine, operazione hello viene eseguito chiamando [CloudTable][dotnet_CloudTable].[ Eseguire][dotnet_CloudTable_Execute].</span><span class="sxs-lookup"><span data-stu-id="a6699-143">Finally, hello operation is executed by calling [CloudTable][dotnet_CloudTable].[Execute][dotnet_CloudTable_Execute].</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute hello insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="a6699-144">Inserire un batch di entità</span><span class="sxs-lookup"><span data-stu-id="a6699-144">Insert a batch of entities</span></span>
<span data-ttu-id="a6699-145">Per inserire un batch di entità in una tabella, è possibile usare un'unica operazione di scrittura.</span><span class="sxs-lookup"><span data-stu-id="a6699-145">You can insert a batch of entities into a table in one write operation.</span></span> <span data-ttu-id="a6699-146">Di seguito sono riportate altre informazioni sulle operazioni batch:</span><span class="sxs-lookup"><span data-stu-id="a6699-146">Some other notes on batch operations:</span></span>

* <span data-ttu-id="a6699-147">È possibile eseguire aggiornamenti, eliminazioni e inserimenti in hello stessa singola operazione batch.</span><span class="sxs-lookup"><span data-stu-id="a6699-147">You can perform updates, deletes, and inserts in hello same single batch operation.</span></span>
* <span data-ttu-id="a6699-148">Una singola operazione batch può includere le entità too100.</span><span class="sxs-lookup"><span data-stu-id="a6699-148">A single batch operation can include up too100 entities.</span></span>
* <span data-ttu-id="a6699-149">Tutte le entità in una singola operazione batch devono avere hello stessa chiave di partizione.</span><span class="sxs-lookup"><span data-stu-id="a6699-149">All entities in a single batch operation must have hello same partition key.</span></span>
* <span data-ttu-id="a6699-150">Sebbene sia possibile tooperform una query come un'operazione batch, deve essere unica operazione di hello in batch hello.</span><span class="sxs-lookup"><span data-stu-id="a6699-150">While it is possible tooperform a query as a batch operation, it must be hello only operation in hello batch.</span></span>

<span data-ttu-id="a6699-151">Crea due oggetti entità Hello esempio di codice seguente e lo aggiunge a ogni troppo[TableBatchOperation] [ dotnet_TableBatchOperation] utilizzando hello [inserire] [ dotnet_TableBatchOperation_Insert] metodo.</span><span class="sxs-lookup"><span data-stu-id="a6699-151">hello following code example creates two entity objects and adds each too[TableBatchOperation][dotnet_TableBatchOperation] by using hello [Insert][dotnet_TableBatchOperation_Insert] method.</span></span> <span data-ttu-id="a6699-152">Quindi, [CloudTable][dotnet_CloudTable].[ ExecuteBatch] [ dotnet_CloudTable_ExecuteBatch] viene chiamato l'operazione di hello tooexecute.</span><span class="sxs-lookup"><span data-stu-id="a6699-152">Then, [CloudTable][dotnet_CloudTable].[ExecuteBatch][dotnet_CloudTable_ExecuteBatch] is called tooexecute hello operation.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create hello batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it toohello table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it toohello table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities toohello batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute hello batch operation.
table.ExecuteBatch(batchOperation);
```

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="a6699-153">Recuperare tutte le entità di una partizione</span><span class="sxs-lookup"><span data-stu-id="a6699-153">Retrieve all entities in a partition</span></span>
<span data-ttu-id="a6699-154">tooquery una tabella per tutte le entità in una partizione, utilizzare un [TableQuery] [ dotnet_TableQuery] oggetto.</span><span class="sxs-lookup"><span data-stu-id="a6699-154">tooquery a table for all entities in a partition, use a [TableQuery][dotnet_TableQuery] object.</span></span> <span data-ttu-id="a6699-155">Hello esempio di codice seguente specifica un filtro per le entità in cui la chiave di partizione hello 'Smith'.</span><span class="sxs-lookup"><span data-stu-id="a6699-155">hello following code example specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="a6699-156">In questo esempio visualizza i campi di ogni entità nella console di toohello risultati query hello hello.</span><span class="sxs-lookup"><span data-stu-id="a6699-156">This example prints hello fields of each entity in hello query results toohello console.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Construct hello query operation for all customer entities where PartitionKey="Smith".
TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>().Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

// Print hello fields for each customer.
foreach (CustomerEntity entity in table.ExecuteQuery(query))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

## <a name="retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="a6699-157">Recuperare un intervallo di entità in una partizione</span><span class="sxs-lookup"><span data-stu-id="a6699-157">Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="a6699-158">Se non si desidera tooquery tutte le entità in una partizione, è possibile specificare un intervallo mediante la combinazione di filtri chiave di partizione hello con un filtro di riga di chiave.</span><span class="sxs-lookup"><span data-stu-id="a6699-158">If you don't want tooquery all entities in a partition, you can specify a range by combining hello partition key filter with a row key filter.</span></span> <span data-ttu-id="a6699-159">Hello esempio di codice seguente usa due filtri tooget tutte le entità nella partizione "Smith" in cui la chiave di riga hello (nome) inizia con una lettera prima 'E' alfabeto hello, quindi stampa i risultati della query hello.</span><span class="sxs-lookup"><span data-stu-id="a6699-159">hello following code example uses two filters tooget all entities in partition 'Smith' where hello row key (first name) starts with a letter before 'E' in hello alphabet, then prints hello query results.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create hello table query.
TableQuery<CustomerEntity> rangeQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.CombineFilters(
        TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"),
        TableOperators.And,
        TableQuery.GenerateFilterCondition("RowKey", QueryComparisons.LessThan, "E")));

// Loop through hello results, displaying information about hello entity.
foreach (CustomerEntity entity in table.ExecuteQuery(rangeQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="a6699-160">Recuperare una singola entità</span><span class="sxs-lookup"><span data-stu-id="a6699-160">Retrieve a single entity</span></span>
<span data-ttu-id="a6699-161">È possibile scrivere un tooretrieve query un'entità singola e specifica.</span><span class="sxs-lookup"><span data-stu-id="a6699-161">You can write a query tooretrieve a single, specific entity.</span></span> <span data-ttu-id="a6699-162">codice Hello seguente usa [TableOperation] [ dotnet_TableOperation] cliente hello toospecify 'Ben Smith'.</span><span class="sxs-lookup"><span data-stu-id="a6699-162">hello following code uses [TableOperation][dotnet_TableOperation] toospecify hello customer 'Ben Smith'.</span></span> <span data-ttu-id="a6699-163">Questo metodo restituisce una sola entità anziché una raccolta e hello ha restituito il valore in [TableResult][dotnet_TableResult].[ Risultato] [ dotnet_TableResult_Result] è un **CustomerEntity** oggetto.</span><span class="sxs-lookup"><span data-stu-id="a6699-163">This method returns just one entity rather than a collection, and hello returned value in [TableResult][dotnet_TableResult].[Result][dotnet_TableResult_Result] is a **CustomerEntity** object.</span></span> <span data-ttu-id="a6699-164">Specifica le chiavi di partizione e di riga in una query è tooretrieve modo più veloce di hello una singola entità dal servizio tabelle hello.</span><span class="sxs-lookup"><span data-stu-id="a6699-164">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello Table service.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Print hello phone number of hello result.
if (retrievedResult.Result != null)
{
    Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
}
else
{
    Console.WriteLine("hello phone number could not be retrieved.");
}
```

## <a name="replace-an-entity"></a><span data-ttu-id="a6699-165">Sostituire un'entità</span><span class="sxs-lookup"><span data-stu-id="a6699-165">Replace an entity</span></span>
<span data-ttu-id="a6699-166">tooupdate un'entità, recuperarlo dal servizio tabelle hello, modificare l'oggetto entità hello e quindi salvare le modifiche apportate hello eseguire il servizio tabelle toohello.</span><span class="sxs-lookup"><span data-stu-id="a6699-166">tooupdate an entity, retrieve it from hello Table service, modify hello entity object, and then save hello changes back toohello Table service.</span></span> <span data-ttu-id="a6699-167">Hello codice seguente modifica il numero di telefono del cliente esistente.</span><span class="sxs-lookup"><span data-stu-id="a6699-167">hello following code changes an existing customer's phone number.</span></span> <span data-ttu-id="a6699-168">Invece di una chiamata a [Insert][dotnet_TableOperation_Insert], nel codice viene usato [Replace][dotnet_TableOperation_Replace].</span><span class="sxs-lookup"><span data-stu-id="a6699-168">Instead of calling [Insert][dotnet_TableOperation_Insert], this code uses [Replace][dotnet_TableOperation_Replace].</span></span> <span data-ttu-id="a6699-169">[Sostituire] [ dotnet_TableOperation_Replace] cause hello toobe entità completamente sostituito nel server di hello, a meno che l'entità di hello sul server hello è stato modificato dopo che è stata recuperata, nel qual caso hello operazione non riuscirà.</span><span class="sxs-lookup"><span data-stu-id="a6699-169">[Replace][dotnet_TableOperation_Replace] causes hello entity toobe fully replaced on hello server, unless hello entity on hello server has changed since it was retrieved, in which case hello operation will fail.</span></span> <span data-ttu-id="a6699-170">Questo errore è tooprevent l'applicazione di sovrascrivere accidentalmente una modifica apportata tra hello il recupero e l'aggiornamento da un altro componente dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a6699-170">This failure is tooprevent your application from inadvertently overwriting a change made between hello retrieval and update by another component of your application.</span></span> <span data-ttu-id="a6699-171">Hello la corretta gestione di questo errore è tooretrieve hello entità nuovamente, apportare le modifiche (se è ancora valida) e quindi eseguire un altro [sostituire] [ dotnet_TableOperation_Replace] operazione.</span><span class="sxs-lookup"><span data-stu-id="a6699-171">hello proper handling of this failure is tooretrieve hello entity again, make your changes (if still valid), and then perform another [Replace][dotnet_TableOperation_Replace] operation.</span></span> <span data-ttu-id="a6699-172">Nella sezione successiva Hello viene illustrato come toooverride questo comportamento.</span><span class="sxs-lookup"><span data-stu-id="a6699-172">hello next section will show you how toooverride this behavior.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Assign hello result tooa CustomerEntity object.
CustomerEntity updateEntity = (CustomerEntity)retrievedResult.Result;

if (updateEntity != null)
{
    // Change hello phone number.
    updateEntity.PhoneNumber = "425-555-0105";

    // Create hello Replace TableOperation.
    TableOperation updateOperation = TableOperation.Replace(updateEntity);

    // Execute hello operation.
    table.Execute(updateOperation);

    Console.WriteLine("Entity updated.");
}
else
{
    Console.WriteLine("Entity could not be retrieved.");
}
```

## <a name="insert-or-replace-an-entity"></a><span data-ttu-id="a6699-173">Inserire o sostituire un'entità</span><span class="sxs-lookup"><span data-stu-id="a6699-173">Insert-or-replace an entity</span></span>
<span data-ttu-id="a6699-174">[Sostituire] [ dotnet_TableOperation_Replace] operazioni hanno esito negativo se l'entità hello è stato modificato dopo che è stata recuperata dal server hello.</span><span class="sxs-lookup"><span data-stu-id="a6699-174">[Replace][dotnet_TableOperation_Replace] operations will fail if hello entity has been changed since it was retrieved from hello server.</span></span> <span data-ttu-id="a6699-175">Inoltre, è necessario recuperare entità hello dal server hello innanzitutto affinché hello [sostituire] [ dotnet_TableOperation_Replace] toobe operazione ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="a6699-175">Furthermore, you must retrieve hello entity from hello server first in order for hello [Replace][dotnet_TableOperation_Replace] operation toobe successful.</span></span> <span data-ttu-id="a6699-176">In alcuni casi, tuttavia, non si conosce se entità hello esista nel server di hello e i valori correnti di hello in essa archiviati sono irrilevanti.</span><span class="sxs-lookup"><span data-stu-id="a6699-176">Sometimes, however, you don't know if hello entity exists on hello server and hello current values stored in it are irrelevant.</span></span> <span data-ttu-id="a6699-177">pertanto devono essere sovrascritti completamente dall'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="a6699-177">Your update should overwrite them all.</span></span> <span data-ttu-id="a6699-178">tooaccomplish, si utilizzerebbe un [InsertOrReplace] [ dotnet_TableOperation_InsertOrReplace] operazione.</span><span class="sxs-lookup"><span data-stu-id="a6699-178">tooaccomplish this, you would use an [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] operation.</span></span> <span data-ttu-id="a6699-179">Questa operazione inserisce l'entità di hello se non esiste oppure lo sostituisce in caso affermativo, indipendentemente dal fatto se hello ultimo aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="a6699-179">This operation inserts hello entity if it doesn't exist, or replaces it if it does, regardless of when hello last update was made.</span></span>

<span data-ttu-id="a6699-180">Nell'esempio di codice seguente di hello, un'entità customer per 'Fred Jones' è creata e inserita nella tabella 'utenti' hello.</span><span class="sxs-lookup"><span data-stu-id="a6699-180">In hello following code example, a customer entity for 'Fred Jones' is created and inserted into hello 'people' table.</span></span> <span data-ttu-id="a6699-181">Successivamente, utilizziamo hello [InsertOrReplace] [ dotnet_TableOperation_InsertOrReplace] toosave operazione un'entità con hello stessa chiave di partizione (Jones) e di riga chiave server toohello (Fred), questa volta con un valore diverso per hello di PhoneNumber proprietà.</span><span class="sxs-lookup"><span data-stu-id="a6699-181">Next, we use hello [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] operation toosave an entity with hello same partition key (Jones) and row key (Fred) toohello server, this time with a different value for hello PhoneNumber property.</span></span> <span data-ttu-id="a6699-182">Dato che si usa [InsertOrReplace][dotnet_TableOperation_InsertOrReplace], tutti i valori delle proprietà vengono sostituiti.</span><span class="sxs-lookup"><span data-stu-id="a6699-182">Because we use [InsertOrReplace][dotnet_TableOperation_InsertOrReplace], all of its property values are replaced.</span></span> <span data-ttu-id="a6699-183">Tuttavia, se un'entità 'Fred Jones' non era già esistenti nella tabella hello, si sarebbe sono stato inserito.</span><span class="sxs-lookup"><span data-stu-id="a6699-183">However, if a 'Fred Jones' entity hadn't already existed in hello table, it would have been inserted.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a customer entity.
CustomerEntity customer3 = new CustomerEntity("Jones", "Fred");
customer3.Email = "Fred@contoso.com";
customer3.PhoneNumber = "425-555-0106";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer3);

// Execute hello operation.
table.Execute(insertOperation);

// Create another customer entity with hello same partition key and row key.
// We've already created a 'Fred Jones' entity and saved it toothe
// 'people' table, but here we're specifying a different value for the
// PhoneNumber property.
CustomerEntity customer4 = new CustomerEntity("Jones", "Fred");
customer4.Email = "Fred@contoso.com";
customer4.PhoneNumber = "425-555-0107";

// Create hello InsertOrReplace TableOperation.
TableOperation insertOrReplaceOperation = TableOperation.InsertOrReplace(customer4);

// Execute hello operation. Because a 'Fred Jones' entity already exists in the
// 'people' table, its property values will be overwritten by those in this
// CustomerEntity. If 'Fred Jones' didn't already exist, hello entity would be
// added toohello table.
table.Execute(insertOrReplaceOperation);
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="a6699-184">Eseguire query su un subset di proprietà di entità</span><span class="sxs-lookup"><span data-stu-id="a6699-184">Query a subset of entity properties</span></span>
<span data-ttu-id="a6699-185">Una query di tabella è possibile recuperare solo alcune proprietà di un'entità anziché tutte le proprietà delle entità hello.</span><span class="sxs-lookup"><span data-stu-id="a6699-185">A table query can retrieve just a few properties from an entity instead of all hello entity properties.</span></span> <span data-ttu-id="a6699-186">Questa tecnica, denominata proiezione, consente di ridurre la larghezza di banda e di migliorare le prestazioni della query, in particolare per entità di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="a6699-186">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="a6699-187">query di Hello nel seguente codice hello restituisce solo hello indirizzi di posta elettronica di entità nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="a6699-187">hello query in hello following code returns only hello email addresses of entities in hello table.</span></span> <span data-ttu-id="a6699-188">A tale scopo viene usata una query di [DynamicTableEntity][dotnet_DynamicTableEntity] e anche [EntityResolver][dotnet_EntityResolver].</span><span class="sxs-lookup"><span data-stu-id="a6699-188">This is done by using a query of [DynamicTableEntity][dotnet_DynamicTableEntity] and also [EntityResolver][dotnet_EntityResolver].</span></span> <span data-ttu-id="a6699-189">Altre informazioni sulla proiezione in hello [Upsert introduzione e proiezione di Query post di blog][blog_post_upsert].</span><span class="sxs-lookup"><span data-stu-id="a6699-189">You can learn more about projection in hello [Introducing Upsert and Query Projection blog post][blog_post_upsert].</span></span> <span data-ttu-id="a6699-190">Proiezione non è supportata dall'emulatore di archiviazione hello, questo codice viene eseguito solo quando si utilizza un account del servizio tabelle hello.</span><span class="sxs-lookup"><span data-stu-id="a6699-190">Projection is not supported by hello storage emulator, so this code runs only when you're using an account in hello Table service.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Define hello query, and select only hello Email property.
TableQuery<DynamicTableEntity> projectionQuery = new TableQuery<DynamicTableEntity>().Select(new string[] { "Email" });

// Define an entity resolver toowork with hello entity after retrieval.
EntityResolver<string> resolver = (pk, rk, ts, props, etag) => props.ContainsKey("Email") ? props["Email"].StringValue : null;

foreach (string projectedEmail in table.ExecuteQuery(projectionQuery, resolver, null, null))
{
    Console.WriteLine(projectedEmail);
}
```

## <a name="delete-an-entity"></a><span data-ttu-id="a6699-191">Eliminare un'entità</span><span class="sxs-lookup"><span data-stu-id="a6699-191">Delete an entity</span></span>
<span data-ttu-id="a6699-192">È possibile eliminare un'entità facilmente dopo avere recuperato utilizzando hello stesso modello visualizzato per l'aggiornamento di un'entità.</span><span class="sxs-lookup"><span data-stu-id="a6699-192">You can easily delete an entity after you have retrieved it by using hello same pattern shown for updating an entity.</span></span> <span data-ttu-id="a6699-193">Hello seguente codice recupera ed elimina un'entità customer.</span><span class="sxs-lookup"><span data-stu-id="a6699-193">hello following code retrieves and deletes a customer entity.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that expects a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Assign hello result tooa CustomerEntity.
CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

// Create hello Delete TableOperation.
if (deleteEntity != null)
{
    TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

    // Execute hello operation.
    table.Execute(deleteOperation);

    Console.WriteLine("Entity deleted.");
}
else
{
    Console.WriteLine("Could not retrieve hello entity.");
}
```

## <a name="delete-a-table"></a><span data-ttu-id="a6699-194">Eliminare una tabella</span><span class="sxs-lookup"><span data-stu-id="a6699-194">Delete a table</span></span>
<span data-ttu-id="a6699-195">Infine, hello esempio di codice seguente elimina una tabella da un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="a6699-195">Finally, hello following code example deletes a table from a storage account.</span></span> <span data-ttu-id="a6699-196">Una tabella in cui è stata eliminata, sarà disponibile toobe ricreati per un periodo di tempo dopo l'eliminazione di hello.</span><span class="sxs-lookup"><span data-stu-id="a6699-196">A table that has been deleted will be unavailable toobe re-created for a period of time following hello deletion.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Delete hello table it if exists.
table.DeleteIfExists();
```

## <a name="retrieve-entities-in-pages-asynchronously"></a><span data-ttu-id="a6699-197">Recuperare entità nelle pagine in modo asincrono</span><span class="sxs-lookup"><span data-stu-id="a6699-197">Retrieve entities in pages asynchronously</span></span>
<span data-ttu-id="a6699-198">Se si legge un numero elevato di entità, e si desidera tooprocess/Visualizza entità che sono stati recuperati invece di attendere vengano tooreturn tutti, è possibile recuperare le entità utilizzando una query segmentata.</span><span class="sxs-lookup"><span data-stu-id="a6699-198">If you are reading a large number of entities, and you want tooprocess/display entities as they are retrieved rather than waiting for them all tooreturn, you can retrieve entities by using a segmented query.</span></span> <span data-ttu-id="a6699-199">Questo esempio mostra come tooreturn risultati in pagine utilizzando il modello di hello Async-Await in modo che non l'esecuzione viene bloccata durante l'attesa per un ampio set di risultati tooreturn.</span><span class="sxs-lookup"><span data-stu-id="a6699-199">This example shows how tooreturn results in pages by using hello Async-Await pattern so that execution is not blocked while you're waiting for a large set of results tooreturn.</span></span> <span data-ttu-id="a6699-200">Per ulteriori informazioni sull'utilizzo di hello criterio Async-Await in .NET, vedere [programmazione asincrona con Async e Await (c# e Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).</span><span class="sxs-lookup"><span data-stu-id="a6699-200">For more details on using hello Async-Await pattern in .NET, see [Asynchronous programming with Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).</span></span>

```csharp
// Initialize a default TableQuery tooretrieve all hello entities in hello table.
TableQuery<CustomerEntity> tableQuery = new TableQuery<CustomerEntity>();

// Initialize hello continuation token toonull toostart from hello beginning of hello table.
TableContinuationToken continuationToken = null;

do
{
    // Retrieve a segment (up too1,000 entities).
    TableQuerySegment<CustomerEntity> tableQueryResult =
        await table.ExecuteQuerySegmentedAsync(tableQuery, continuationToken);

    // Assign hello new continuation token tootell hello service where to
    // continue on hello next iteration (or null if it has reached hello end).
    continuationToken = tableQueryResult.ContinuationToken;

    // Print hello number of rows retrieved.
    Console.WriteLine("Rows retrieved {0}", tableQueryResult.Results.Count);

// Loop until a null continuation token is received, indicating hello end of hello table.
} while(continuationToken != null);
```

## <a name="next-steps"></a><span data-ttu-id="a6699-201">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a6699-201">Next steps</span></span>
<span data-ttu-id="a6699-202">Ora che si sono appreso i concetti fondamentali di hello dell'archiviazione tabelle, seguire questi toolearn collegamenti sulle attività più complesse di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="a6699-202">Now that you've learned hello basics of Table storage, follow these links toolearn about more complex storage tasks:</span></span>

* <span data-ttu-id="a6699-203">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) è un'app autonoma, disponibile da Microsoft che consente di toowork visivamente i dati di archiviazione di Azure in Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="a6699-203">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="a6699-204">Per altri esempi di archivio tabelle, vedere [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)</span><span class="sxs-lookup"><span data-stu-id="a6699-204">See more Table storage samples in [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)</span></span>
* <span data-ttu-id="a6699-205">Visualizzare la documentazione di riferimento del servizio tabella hello per informazioni dettagliate sulle API disponibili:</span><span class="sxs-lookup"><span data-stu-id="a6699-205">View hello Table service reference documentation for complete details about available APIs:</span></span>
* [<span data-ttu-id="a6699-206">Informazioni di riferimento sulla libreria client di archiviazione per .NET</span><span class="sxs-lookup"><span data-stu-id="a6699-206">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
* [<span data-ttu-id="a6699-207">Informazioni di riferimento sulle API REST</span><span class="sxs-lookup"><span data-stu-id="a6699-207">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="a6699-208">Informazioni su come codice hello toosimplify scrivere toowork con archiviazione di Azure tramite hello [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="a6699-208">Learn how toosimplify hello code you write toowork with Azure Storage by using hello [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)</span></span>
* <span data-ttu-id="a6699-209">Consente di visualizzare altre toolearn di guide di funzionalità sulle opzioni aggiuntive per l'archiviazione dei dati in Azure.</span><span class="sxs-lookup"><span data-stu-id="a6699-209">View more feature guides toolearn about additional options for storing data in Azure.</span></span>
* <span data-ttu-id="a6699-210">[Introduzione all'archiviazione Blob di Azure usando .NET](storage-dotnet-how-to-use-blobs.md) toostore dati non strutturati.</span><span class="sxs-lookup"><span data-stu-id="a6699-210">[Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) toostore unstructured data.</span></span>
* <span data-ttu-id="a6699-211">[Connettersi con .NET (c#) tooSQL Database](../sql-database/sql-database-develop-dotnet-simple.md) toostore di dati relazionali.</span><span class="sxs-lookup"><span data-stu-id="a6699-211">[Connect tooSQL Database by using .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) toostore relational data.</span></span>

[Download and install hello Azure SDK for .NET]: /develop/net/
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
