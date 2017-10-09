---
title: aaaGet avviato con l'archiviazione tabelle di Azure usando .NET | Documenti Microsoft
description: Archiviare dati strutturati in un cloud di hello tramite l'archiviazione tabelle di Azure, un archivio dati NoSQL.
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: fe46d883-7bed-49dd-980e-5c71df36adb3
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 04/10/2017
ms.author: mimig
ms.openlocfilehash: a3e9a4c6f6fd5e724535b86a3f99cd4c161de6de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-table-storage-using-net"></a>Introduzione all'archiviazione tabelle di Azure con .NET
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

Archiviazione tabelle di Azure è un servizio che archivia NoSQL strutturati con una progettazione schemaless archiviano i dati nel cloud hello, fornendo una chiave o un attributo. Poiché l'archiviazione tabelle è schemaless, è facile tooadapt i dati come hello necessita di evolve l'applicazione. Accedere ai dati di archiviazione tooTable è veloce e conveniente per molti tipi di applicazioni e viene in genere inferiore costo SQL tradizionale per i volumi di dati simili.

È possibile utilizzare una tabella archiviazione toostore flessibile i set di dati come dati utente per applicazioni web, rubriche, informazioni sul dispositivo o altri tipi di metadati che del servizio richiede. È possibile archiviare qualsiasi numero di entità in una tabella e un account di archiviazione può contenere qualsiasi numero di tabelle, di limite di capacità toohello hello dell'account di archiviazione.

### <a name="about-this-tutorial"></a>Informazioni sull'esercitazione
In questa esercitazione illustra come hello toouse [Azure Storage Client Library per .NET](https://www.nuget.org/packages/WindowsAzure.Storage/) in alcuni scenari comuni di archiviazione tabelle di Azure. Gli scenari vengono presentati con esempi C# per la creazione ed eliminazione di una tabella e l'inserimento, l'aggiornamento, l'eliminazione e l'esecuzione di query per i dati delle tabelle.

## <a name="prerequisites"></a>Prerequisiti

È necessario hello seguenti toocomplete questa esercitazione correttamente:

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Libreria client di archiviazione di Azure per .NET](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [Gestione configurazione di Azure per .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* [Account di archiviazione di Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a>Altri esempi
Per altri esempi di uso dell'archivio tabelle, vedere [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)(Introduzione all'archivio tabelle di Azure in .NET). È possibile scaricare l'applicazione di esempio hello ed eseguirlo o esaminare il codice hello su GitHub.

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a>Aggiungere le direttive using
Aggiungere il seguente hello **utilizzando** hello cima toohello direttive `Program.cs` file:

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Table; // Namespace for Table storage types
```

### <a name="parse-hello-connection-string"></a>Analizzare la stringa di connessione hello
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-table-service-client"></a>Creare i client del servizio tabelle hello
Hello [CloudTableClient] [ dotnet_CloudTableClient] classe consente tooretrieve tabelle ed entità archiviate nell'archiviazione tabelle. Ecco un modo toocreate client del servizio tabelle hello:

```csharp
// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```

Si è ora pronto toowrite codice che legge i dati da e scrive tooTable archiviazione dei dati.

## <a name="create-a-table"></a>Creare una tabella
Questo esempio viene illustrato come toocreate una tabella se non esiste già:

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

## <a name="add-an-entity-tooa-table"></a>Aggiungere una tabella tooa entità
Entità di eseguire il mapping di oggetti tooC # utilizzando una classe personalizzata derivata da [TableEntity][dotnet_TableEntity]. tooadd tabella tooa un'entità, creare una classe che definisce le proprietà di hello dell'entità. Hello codice seguente definisce una classe di entità che utilizza nome hello del cliente come chiave di riga hello e last name come chiave di partizione hello. Insieme, di partizione e chiave di riga identificarla in modo univoco nella tabella hello. Le entità con hello stessa chiave di partizione è possibile eseguire query più velocemente rispetto alle entità con diverse chiavi di partizione, ma con le chiavi di partizione diverse consente una maggiore scalabilità di operazioni parallele. Entità toobe archiviati nelle tabelle deve essere di un tipo supportato, ad esempio derivato da hello [TableEntity] [ dotnet_TableEntity] classe. Si desidera toostore in una tabella di proprietà dell'entità deve essere di proprietà pubbliche di tipo hello e supportano il recupero e impostazione dei valori. Il tipo di entità *deve* inoltre esporre un costruttore senza parametri.

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

Le operazioni di tabella che interessano le entità vengono eseguite tramite hello [CloudTable] [ dotnet_CloudTable] oggetto creato in precedenza nella sezione "Creazione di una tabella" hello. Hello toobe operazione eseguita è rappresentato da un [TableOperation] [ dotnet_TableOperation] oggetto. Hello esempio di codice seguente viene illustrata hello creazione di hello [CloudTable] [ dotnet_CloudTable] oggetto e quindi un **CustomerEntity** oggetto. operazione di hello tooprepare, un [TableOperation] [ dotnet_TableOperation] oggetto viene creato l'entità customer di tooinsert hello in tabella hello. Infine, operazione hello viene eseguito chiamando [CloudTable][dotnet_CloudTable].[ Eseguire][dotnet_CloudTable_Execute].

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

## <a name="insert-a-batch-of-entities"></a>Inserire un batch di entità
Per inserire un batch di entità in una tabella, è possibile usare un'unica operazione di scrittura. Di seguito sono riportate altre informazioni sulle operazioni batch:

* È possibile eseguire aggiornamenti, eliminazioni e inserimenti in hello stessa singola operazione batch.
* Una singola operazione batch può includere le entità too100.
* Tutte le entità in una singola operazione batch devono avere hello stessa chiave di partizione.
* Sebbene sia possibile tooperform una query come un'operazione batch, deve essere unica operazione di hello in batch hello.

Crea due oggetti entità Hello esempio di codice seguente e lo aggiunge a ogni troppo[TableBatchOperation] [ dotnet_TableBatchOperation] utilizzando hello [inserire] [ dotnet_TableBatchOperation_Insert] metodo. Quindi, [CloudTable][dotnet_CloudTable].[ ExecuteBatch] [ dotnet_CloudTable_ExecuteBatch] viene chiamato l'operazione di hello tooexecute.

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

## <a name="retrieve-all-entities-in-a-partition"></a>Recuperare tutte le entità di una partizione
tooquery una tabella per tutte le entità in una partizione, utilizzare un [TableQuery] [ dotnet_TableQuery] oggetto. Hello esempio di codice seguente specifica un filtro per le entità in cui la chiave di partizione hello 'Smith'. In questo esempio visualizza i campi di ogni entità nella console di toohello risultati query hello hello.

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

## <a name="retrieve-a-range-of-entities-in-a-partition"></a>Recuperare un intervallo di entità in una partizione
Se non si desidera tooquery tutte le entità in una partizione, è possibile specificare un intervallo mediante la combinazione di filtri chiave di partizione hello con un filtro di riga di chiave. Hello esempio di codice seguente usa due filtri tooget tutte le entità nella partizione "Smith" in cui la chiave di riga hello (nome) inizia con una lettera prima 'E' alfabeto hello, quindi stampa i risultati della query hello.

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

## <a name="retrieve-a-single-entity"></a>Recuperare una singola entità
È possibile scrivere un tooretrieve query un'entità singola e specifica. codice Hello seguente usa [TableOperation] [ dotnet_TableOperation] cliente hello toospecify 'Ben Smith'. Questo metodo restituisce una sola entità anziché una raccolta e hello ha restituito il valore in [TableResult][dotnet_TableResult].[ Risultato] [ dotnet_TableResult_Result] è un **CustomerEntity** oggetto. Specifica le chiavi di partizione e di riga in una query è tooretrieve modo più veloce di hello una singola entità dal servizio tabelle hello.

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

## <a name="replace-an-entity"></a>Sostituire un'entità
tooupdate un'entità, recuperarlo dal servizio tabelle hello, modificare l'oggetto entità hello e quindi salvare le modifiche apportate hello eseguire il servizio tabelle toohello. Hello codice seguente modifica il numero di telefono del cliente esistente. Invece di una chiamata a [Insert][dotnet_TableOperation_Insert], nel codice viene usato [Replace][dotnet_TableOperation_Replace]. [Sostituire] [ dotnet_TableOperation_Replace] cause hello toobe entità completamente sostituito nel server di hello, a meno che l'entità di hello sul server hello è stato modificato dopo che è stata recuperata, nel qual caso hello operazione non riuscirà. Questo errore è tooprevent l'applicazione di sovrascrivere accidentalmente una modifica apportata tra hello il recupero e l'aggiornamento da un altro componente dell'applicazione. Hello la corretta gestione di questo errore è tooretrieve hello entità nuovamente, apportare le modifiche (se è ancora valida) e quindi eseguire un altro [sostituire] [ dotnet_TableOperation_Replace] operazione. Nella sezione successiva Hello viene illustrato come toooverride questo comportamento.

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

## <a name="insert-or-replace-an-entity"></a>Inserire o sostituire un'entità
[Sostituire] [ dotnet_TableOperation_Replace] operazioni hanno esito negativo se l'entità hello è stato modificato dopo che è stata recuperata dal server hello. Inoltre, è necessario recuperare entità hello dal server hello innanzitutto affinché hello [sostituire] [ dotnet_TableOperation_Replace] toobe operazione ha esito positivo. In alcuni casi, tuttavia, non si conosce se entità hello esista nel server di hello e i valori correnti di hello in essa archiviati sono irrilevanti. pertanto devono essere sovrascritti completamente dall'aggiornamento. tooaccomplish, si utilizzerebbe un [InsertOrReplace] [ dotnet_TableOperation_InsertOrReplace] operazione. Questa operazione inserisce l'entità di hello se non esiste oppure lo sostituisce in caso affermativo, indipendentemente dal fatto se hello ultimo aggiornamento.

Nell'esempio di codice seguente di hello, un'entità customer per 'Fred Jones' è creata e inserita nella tabella 'utenti' hello. Successivamente, utilizziamo hello [InsertOrReplace] [ dotnet_TableOperation_InsertOrReplace] toosave operazione un'entità con hello stessa chiave di partizione (Jones) e di riga chiave server toohello (Fred), questa volta con un valore diverso per hello di PhoneNumber proprietà. Dato che si usa [InsertOrReplace][dotnet_TableOperation_InsertOrReplace], tutti i valori delle proprietà vengono sostituiti. Tuttavia, se un'entità 'Fred Jones' non era già esistenti nella tabella hello, si sarebbe sono stato inserito.

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

## <a name="query-a-subset-of-entity-properties"></a>Eseguire query su un subset di proprietà di entità
Una query di tabella è possibile recuperare solo alcune proprietà di un'entità anziché tutte le proprietà delle entità hello. Questa tecnica, denominata proiezione, consente di ridurre la larghezza di banda e di migliorare le prestazioni della query, in particolare per entità di grandi dimensioni. query di Hello nel seguente codice hello restituisce solo hello indirizzi di posta elettronica di entità nella tabella hello. A tale scopo viene usata una query di [DynamicTableEntity][dotnet_DynamicTableEntity] e anche [EntityResolver][dotnet_EntityResolver]. Altre informazioni sulla proiezione in hello [Upsert introduzione e proiezione di Query post di blog][blog_post_upsert]. Proiezione non è supportata dall'emulatore di archiviazione hello, questo codice viene eseguito solo quando si utilizza un account del servizio tabelle hello.

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

## <a name="delete-an-entity"></a>Eliminare un'entità
È possibile eliminare un'entità facilmente dopo avere recuperato utilizzando hello stesso modello visualizzato per l'aggiornamento di un'entità. Hello seguente codice recupera ed elimina un'entità customer.

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

## <a name="delete-a-table"></a>Eliminare una tabella
Infine, hello esempio di codice seguente elimina una tabella da un account di archiviazione. Una tabella in cui è stata eliminata, sarà disponibile toobe ricreati per un periodo di tempo dopo l'eliminazione di hello.

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

## <a name="retrieve-entities-in-pages-asynchronously"></a>Recuperare entità nelle pagine in modo asincrono
Se si legge un numero elevato di entità, e si desidera tooprocess/Visualizza entità che sono stati recuperati invece di attendere vengano tooreturn tutti, è possibile recuperare le entità utilizzando una query segmentata. Questo esempio mostra come tooreturn risultati in pagine utilizzando il modello di hello Async-Await in modo che non l'esecuzione viene bloccata durante l'attesa per un ampio set di risultati tooreturn. Per ulteriori informazioni sull'utilizzo di hello criterio Async-Await in .NET, vedere [programmazione asincrona con Async e Await (c# e Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).

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

## <a name="next-steps"></a>Passaggi successivi
Ora che si sono appreso i concetti fondamentali di hello dell'archiviazione tabelle, seguire questi toolearn collegamenti sulle attività più complesse di archiviazione:

* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) è un'app autonoma, disponibile da Microsoft che consente di toowork visivamente i dati di archiviazione di Azure in Windows, macOS e Linux.
* Per altri esempi di archivio tabelle, vedere [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)
* Visualizzare la documentazione di riferimento del servizio tabella hello per informazioni dettagliate sulle API disponibili:
* [Informazioni di riferimento sulla libreria client di archiviazione per .NET](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
* [Informazioni di riferimento sulle API REST](http://msdn.microsoft.com/library/azure/dd179355)
* Informazioni su come codice hello toosimplify scrivere toowork con archiviazione di Azure tramite hello [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)
* Consente di visualizzare altre toolearn di guide di funzionalità sulle opzioni aggiuntive per l'archiviazione dei dati in Azure.
* [Introduzione all'archiviazione Blob di Azure usando .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) toostore dati non strutturati.
* [Connettersi con .NET (c#) tooSQL Database](../sql-database/sql-database-develop-dotnet-simple.md) toostore di dati relazionali.

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
