---
title: Come usare l'archiviazione tabelle da Java | Microsoft Docs
description: Archiviare dati non strutturati nel cloud con il servizio di archiviazione tabelle di Azure, ovvero un archivio dati NoSQL.
services: cosmos-db
documentationcenter: java
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: 45145189-e67f-4ca6-b15d-43af7bfd3f97
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 7f92b1e14a514e9eda39f7ca94f63fc761dfdf41
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-table-storage-from-java"></a><span data-ttu-id="e64cc-103">Come usare l'archiviazione tabelle da Java</span><span class="sxs-lookup"><span data-stu-id="e64cc-103">How to use Table storage from Java</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="e64cc-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="e64cc-104">Overview</span></span>
<span data-ttu-id="e64cc-105">Questa guida illustra diversi scenari di utilizzo comuni del servizio di archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="e64cc-105">This guide will show you how to perform common scenarios using the Azure Table storage service.</span></span> <span data-ttu-id="e64cc-106">Gli esempi sono scritti in Java e usano [Azure Storage SDK per Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="e64cc-106">The samples are written in Java and use the [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="e64cc-107">Gli scenari presentati includono **creazione**, **visualizzazione di un elenco** ed **eliminazione** di tabelle, nonché **inserimento**, **esecuzione di query**, **modifica** ed **eliminazione** di entità in una tabella.</span><span class="sxs-lookup"><span data-stu-id="e64cc-107">The scenarios covered include **creating**, **listing**, and **deleting** tables, as well as **inserting**, **querying**, **modifying**, and **deleting** entities in a table.</span></span> <span data-ttu-id="e64cc-108">Per altre informazioni sulle tabelle, vedere la sezione [Passaggi successivi](#Next-Steps) .</span><span class="sxs-lookup"><span data-stu-id="e64cc-108">For more information on tables, see the [Next steps](#Next-Steps) section.</span></span>

<span data-ttu-id="e64cc-109">Nota: per gli sviluppatori che usano il servizio di archiviazione di Azure in dispositivi Android, è disponibile un SDK specifico.</span><span class="sxs-lookup"><span data-stu-id="e64cc-109">Note: An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="e64cc-110">Per altre informazioni, vedere [Azure Storage SDK per Android][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="e64cc-110">For more information, see the [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="e64cc-111">Creare un'applicazione Java</span><span class="sxs-lookup"><span data-stu-id="e64cc-111">Create a Java application</span></span>
<span data-ttu-id="e64cc-112">In questa guida si utilizzeranno le funzionalità di archiviazione che possono essere eseguite in un'applicazione Java in locale o nel codice in esecuzione in un ruolo Web, in un ruolo di lavoro o in Azure.</span><span class="sxs-lookup"><span data-stu-id="e64cc-112">In this guide, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="e64cc-113">A questo scopo, è necessario installare Java Development Kit (JDK) e creare un account di archiviazione di Azure nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e64cc-113">To do so, you will need to install the Java Development Kit (JDK) and create an Azure storage account in your Azure subscription.</span></span> <span data-ttu-id="e64cc-114">Dopo avere eseguito questa operazione, sarà necessario verificare che il sistema di sviluppo in uso soddisfi i requisiti minimi e le dipendenze elencate nel repository [Azure Storage SDK per Java][Azure Storage SDK for Java] su GitHub.</span><span class="sxs-lookup"><span data-stu-id="e64cc-114">Once you have done so, you will need to verify that your development system meets the minimum requirements and dependencies which are listed in the [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="e64cc-115">Se il sistema soddisfa i requisiti, è possibile seguire le istruzioni per scaricare e installare le librerie di archiviazione di Azure per Java nel sistema dall'archivio indicato.</span><span class="sxs-lookup"><span data-stu-id="e64cc-115">If your system meets those requirements, you can follow the instructions for downloading and installing the Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="e64cc-116">Dopo avere completato queste attività, sarà possibile creare un'applicazione Java che usa gli esempi illustrati in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="e64cc-116">Once you have completed those tasks, you will be able to create a Java application which uses the examples in this article.</span></span>

## <a name="configure-your-application-to-access-table-storage"></a><span data-ttu-id="e64cc-117">Configurare l'applicazione per l'accesso all'archiviazione tabelle</span><span class="sxs-lookup"><span data-stu-id="e64cc-117">Configure your application to access table storage</span></span>
<span data-ttu-id="e64cc-118">Aggiungere le istruzioni import seguenti all'inizio del file Java in cui si useranno le API di archiviazione di Microsoft Azure per accedere alle tabelle:</span><span class="sxs-lookup"><span data-stu-id="e64cc-118">Add the following import statements to the top of the Java file where you want to use Microsoft Azure storage APIs to access tables:</span></span>

```java
// Include the following imports to use table APIs
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.table.*;
import com.microsoft.azure.storage.table.TableQuery.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="e64cc-119">Impostare una stringa di connessione di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e64cc-119">Set up an Azure storage connection string</span></span>
<span data-ttu-id="e64cc-120">I client di archiviazione di Azure usano le stringhe di connessione di archiviazione per archiviare endpoint e credenziali per l'accesso ai servizi di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="e64cc-120">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="e64cc-121">Quando si esegue un'applicazione client, è necessario specificare la stringa di connessione di archiviazione nel formato seguente, usando il nome dell'account di archiviazione e la chiave di accesso primaria relativa all'account di archiviazione riportata nel [portale di Azure](https://portal.azure.com) per i valori *AccountName* e *AccountKey*.</span><span class="sxs-lookup"><span data-stu-id="e64cc-121">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the Primary access key for the storage account listed in the [Azure portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="e64cc-122">In questo esempio viene illustrato come dichiarare un campo statico per memorizzare la stringa di connessione:</span><span class="sxs-lookup"><span data-stu-id="e64cc-122">This example shows how you can declare a static field to hold the connection string:</span></span>

```java
// Define the connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="e64cc-123">In un'applicazione in esecuzione in un ruolo di Microsoft Azure, questa stringa può essere archiviata nel file di configurazione del servizio *ServiceConfiguration.cscfg*ed è accessibile con una chiamata al metodo **RoleEnvironment.getConfigurationSettings** .</span><span class="sxs-lookup"><span data-stu-id="e64cc-123">In an application running within a role in Microsoft Azure, this string can be stored in the service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call to the **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="e64cc-124">Nell'esempio seguente viene recuperata la stringa di connessione da un elemento **Setting** denominato *StorageConnectionString* nel file di configurazione del servizio:</span><span class="sxs-lookup"><span data-stu-id="e64cc-124">Here's an example of getting the connection string from a **Setting** element named *StorageConnectionString* in the service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="e64cc-125">Gli esempi seguenti presumono che sia stato usato uno di questi due metodi per ottenere la stringa di connessione di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e64cc-125">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>

## <a name="how-to-create-a-table"></a><span data-ttu-id="e64cc-126">Procedura: creare una tabella</span><span class="sxs-lookup"><span data-stu-id="e64cc-126">How to: Create a table</span></span>
<span data-ttu-id="e64cc-127">Per ottenere oggetti di riferimento per tabelle ed entità, è possibile usare un oggetto **CloudTableClient**.</span><span class="sxs-lookup"><span data-stu-id="e64cc-127">A **CloudTableClient** object lets you get reference objects for tables and entities.</span></span> <span data-ttu-id="e64cc-128">Il codice seguente consente di creare un oggetto **CloudTableClient** e di usarlo per creare un oggetto **CloudTable** che rappresenta una tabella denominata "people".</span><span class="sxs-lookup"><span data-stu-id="e64cc-128">The following code creates a **CloudTableClient** object and uses it to create a new **CloudTable** object which represents a table named "people".</span></span> <span data-ttu-id="e64cc-129">(Nota: esistono altri modi per creare oggetti **CloudStorageAccount**. Per altre informazioni, vedere **CloudStorageAccount** nel [Riferimento all'SDK del client di archiviazione di Azure]).</span><span class="sxs-lookup"><span data-stu-id="e64cc-129">(Note: There are additional ways to create **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in the [Azure Storage Client SDK Reference].)</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create the table if it doesn't exist.
    String tableName = "people";
    CloudTable cloudTable = tableClient.getTableReference(tableName);
    cloudTable.createIfNotExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-the-tables"></a><span data-ttu-id="e64cc-130">Procedura: elencare le tabelle</span><span class="sxs-lookup"><span data-stu-id="e64cc-130">How to: List the tables</span></span>
<span data-ttu-id="e64cc-131">Per ottenere un elenco di tabelle, chiamare il metodo **CloudTableClient.listTables()** per recuperare un elenco iterabile di nomi di tabelle.</span><span class="sxs-lookup"><span data-stu-id="e64cc-131">To get a list of tables, call the **CloudTableClient.listTables()** method to retrieve an iterable list of table names.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Loop through the collection of table names.
    for (String table : tableClient.listTables())
    {
        // Output each table name.
        System.out.println(table);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-an-entity-to-a-table"></a><span data-ttu-id="e64cc-132">Procedura: aggiungere un’entità a una tabella</span><span class="sxs-lookup"><span data-stu-id="e64cc-132">How to: Add an entity to a table</span></span>
<span data-ttu-id="e64cc-133">Per eseguire il mapping di entità a oggetti Java viene utilizzata una classe personalizzata che implementa **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="e64cc-133">Entities map to Java objects using a custom class implementing **TableEntity**.</span></span> <span data-ttu-id="e64cc-134">Per comodità, la classe **TableServiceEntity** implementa **TableEntity** e usa la reflection per eseguire il mapping di proprietà ai metodi Get e Set denominati per le proprietà.</span><span class="sxs-lookup"><span data-stu-id="e64cc-134">For convenience, the **TableServiceEntity** class implements **TableEntity** and uses reflection to map properties to getter and setter methods named for the properties.</span></span> <span data-ttu-id="e64cc-135">Per aggiungere un'entità a una classe, creare prima una classe che definisca le proprietà dell'entità.</span><span class="sxs-lookup"><span data-stu-id="e64cc-135">To add an entity to a table, first create a class that defines the properties of your entity.</span></span> <span data-ttu-id="e64cc-136">Il codice seguente consente di definire una classe di entità che usa il nome e il cognome del cliente rispettivamente come chiave di riga e chiave di partizione.</span><span class="sxs-lookup"><span data-stu-id="e64cc-136">The following code defines an entity class which uses the customer's first name as the row key, and last name as the partition key.</span></span> <span data-ttu-id="e64cc-137">La combinazione della chiave di riga e della chiave di partizione di un'entità consentono di identificare in modo univoco l'entità nella tabella.</span><span class="sxs-lookup"><span data-stu-id="e64cc-137">Together, an entity's partition and row key uniquely identify the entity in the table.</span></span> <span data-ttu-id="e64cc-138">Le query su entità con la stessa chiave di partizione vengono eseguite più rapidamente di quelle con chiavi di partizione diverse.</span><span class="sxs-lookup"><span data-stu-id="e64cc-138">Entities with the same partition key can be queried faster than those with different partition keys.</span></span>

```java
public class CustomerEntity extends TableServiceEntity {
    public CustomerEntity(String lastName, String firstName) {
        this.partitionKey = lastName;
        this.rowKey = firstName;
    }

    public CustomerEntity() { }

    String email;
    String phoneNumber;

    public String getEmail() {
        return this.email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public String getPhoneNumber() {
        return this.phoneNumber;
    }

    public void setPhoneNumber(String phoneNumber) {
        this.phoneNumber = phoneNumber;
    }
}
```

<span data-ttu-id="e64cc-139">Per le operazioni su tabella che interessano entità è necessario un oggetto **TableServiceContext** .</span><span class="sxs-lookup"><span data-stu-id="e64cc-139">Table operations involving entities require a **TableOperation** object.</span></span> <span data-ttu-id="e64cc-140">Questo oggetto definisce l'operazione da eseguire su un'entità, che può essere eseguita con un oggetto **CloudTable** .</span><span class="sxs-lookup"><span data-stu-id="e64cc-140">This object defines the operation to be performed on an entity, which can be executed with a **CloudTable** object.</span></span> <span data-ttu-id="e64cc-141">Il codice seguente crea una nuova istanza della classe **CustomerEntity** con alcuni dati del cliente da memorizzare.</span><span class="sxs-lookup"><span data-stu-id="e64cc-141">The following code creates a new instance of the **CustomerEntity** class with some customer data to be stored.</span></span> <span data-ttu-id="e64cc-142">Il codice chiama quindi **TableOperation.insertOrReplace** per creare un oggetto **TableOperation** in modo da inserire un'entità in una tabella e vi associa la nuova classe **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="e64cc-142">The code next calls **TableOperation.insertOrReplace** to create a **TableOperation** object to insert an entity into a table, and associates the new **CustomerEntity** with it.</span></span> <span data-ttu-id="e64cc-143">Infine, il codice chiama il metodo **execute** sull'oggetto **CloudTable**, specificando la tabella "people" e il nuovo oggetto **TableOperation**, che quindi invia una richiesta al servizio di archiviazione per inserire la nuova entità cliente nella tabella "people" o sostituire l'entità se ne esiste già una.</span><span class="sxs-lookup"><span data-stu-id="e64cc-143">Finally, the code calls the **execute** method on the **CloudTable** object, specifying the "people" table and the new **TableOperation**, which then sends a request to the storage service to insert the new customer entity into the "people" table, or replace the entity if it already exists.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.setEmail("Walter@contoso.com");
    customer1.setPhoneNumber("425-555-0101");

    // Create an operation to add the new customer to the people table.
    TableOperation insertCustomer1 = TableOperation.insertOrReplace(customer1);

    // Submit the operation to the table service.
    cloudTable.execute(insertCustomer1);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-a-batch-of-entities"></a><span data-ttu-id="e64cc-144">Procedura: inserire un batch di entità</span><span class="sxs-lookup"><span data-stu-id="e64cc-144">How to: Insert a batch of entities</span></span>
<span data-ttu-id="e64cc-145">Per inserire un batch di entità nel servizio tabelle, è possibile usare un'unica operazione di scrittura.</span><span class="sxs-lookup"><span data-stu-id="e64cc-145">You can insert a batch of entities to the table service in one write operation.</span></span> <span data-ttu-id="e64cc-146">Il codice seguente crea un oggetto **TableBatchOperation** quindi vi aggiunge tre operazioni di inserimento.</span><span class="sxs-lookup"><span data-stu-id="e64cc-146">The following code creates a **TableBatchOperation** object, then adds three insert operations to it.</span></span> <span data-ttu-id="e64cc-147">Ciascuna operazione di inserimento viene aggiunta creando un nuovo oggetto entità, impostandone i valori, quindi chiamando il metodo **insert** sull'oggetto **TableBatchOperation** per associare l'entità a una nuova operazione di inserimento.</span><span class="sxs-lookup"><span data-stu-id="e64cc-147">Each insert operation is added by creating a new entity object, setting its values, and then calling the **insert** method on the **TableBatchOperation** object to associate the entity with a new insert operation.</span></span> <span data-ttu-id="e64cc-148">Il codice chiama quindi il metodo **execute** sull'oggetto **CloudTable**, specificando la tabella "people" e l'oggetto **TableBatchOperation**, che invia il batch di operazioni su tabella al servizio di archiviazione in un'unica richiesta.</span><span class="sxs-lookup"><span data-stu-id="e64cc-148">Then the code calls **execute** on the **CloudTable** object, specifying the "people" table and the **TableBatchOperation** object, which sends the batch of table operations to the storage service in a single request.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Define a batch operation.
    TableBatchOperation batchOperation = new TableBatchOperation();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a customer entity to add to the table.
    CustomerEntity customer = new CustomerEntity("Smith", "Jeff");
    customer.setEmail("Jeff@contoso.com");
    customer.setPhoneNumber("425-555-0104");
    batchOperation.insertOrReplace(customer);

    // Create another customer entity to add to the table.
    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.setEmail("Ben@contoso.com");
    customer2.setPhoneNumber("425-555-0102");
    batchOperation.insertOrReplace(customer2);

    // Create a third customer entity to add to the table.
    CustomerEntity customer3 = new CustomerEntity("Smith", "Denise");
    customer3.setEmail("Denise@contoso.com");
    customer3.setPhoneNumber("425-555-0103");
    batchOperation.insertOrReplace(customer3);

    // Execute the batch of operations on the "people" table.
    cloudTable.execute(batchOperation);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="e64cc-149">Di seguito sono riportate alcune informazioni sulle operazioni batch:</span><span class="sxs-lookup"><span data-stu-id="e64cc-149">Some things to note on batch operations:</span></span>

* <span data-ttu-id="e64cc-150">È possibile eseguire fino a 100 operazioni di inserimento, eliminazione, unione, sostituzione, inserimento o unione e inserimento o sostituzione in qualsiasi combinazione in un unico batch.</span><span class="sxs-lookup"><span data-stu-id="e64cc-150">You can perform up to 100 insert, delete, merge, replace, insert or merge, and insert or replace operations in any combination in a single batch.</span></span>
* <span data-ttu-id="e64cc-151">Un'operazione batch può prevedere un'operazione di recupero, se è l'unica operazione nel batch.</span><span class="sxs-lookup"><span data-stu-id="e64cc-151">A batch operation can have a retrieve operation, if it is the only operation in the batch.</span></span>
* <span data-ttu-id="e64cc-152">A tutte le entità di una singola operazione batch deve essere associata la stessa chiave di partizione.</span><span class="sxs-lookup"><span data-stu-id="e64cc-152">All entities in a single batch operation must have the same partition key.</span></span>
* <span data-ttu-id="e64cc-153">Un'operazione batch è limitata a un payload di dati di 4 MB.</span><span class="sxs-lookup"><span data-stu-id="e64cc-153">A batch operation is limited to a 4MB data payload.</span></span>

## <a name="how-to-retrieve-all-entities-in-a-partition"></a><span data-ttu-id="e64cc-154">Procedura: recuperare tutte le entità di una partizione</span><span class="sxs-lookup"><span data-stu-id="e64cc-154">How to: Retrieve all entities in a partition</span></span>
<span data-ttu-id="e64cc-155">Per eseguire una query su una tabella relativa alle entità in una partizione è possibile utilizzare **TableQuery**.</span><span class="sxs-lookup"><span data-stu-id="e64cc-155">To query a table for entities in a partition, you can use a **TableQuery**.</span></span> <span data-ttu-id="e64cc-156">Chiamare **TableQuery.from** per creare su una particolare tabella una query che restituisca un tipo di risultato specificato.</span><span class="sxs-lookup"><span data-stu-id="e64cc-156">Call **TableQuery.from** to create a query on a particular table that returns a specified result type.</span></span> <span data-ttu-id="e64cc-157">Nel codice seguente viene specificato un filtro per le entità in cui la chiave di partizione è 'Smith'.</span><span class="sxs-lookup"><span data-stu-id="e64cc-157">The following code specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="e64cc-158">**TableQuery.generateFilterCondition** è un metodo helper che consente di creare filtri per le query.</span><span class="sxs-lookup"><span data-stu-id="e64cc-158">**TableQuery.generateFilterCondition** is a helper method to create filters for queries.</span></span> <span data-ttu-id="e64cc-159">Chiamare **where** sul riferimento restituito dal metodo **TableQuery.from** per applicare il filtro alla query.</span><span class="sxs-lookup"><span data-stu-id="e64cc-159">Call **where** on the reference returned by the **TableQuery.from** method to apply the filter to the query.</span></span> <span data-ttu-id="e64cc-160">Quando la query viene eseguita con una chiamata a **execute** sull'oggetto **CloudTable** restituisce un oggetto **Iterator** con il tipo di risultato **CustomerEntity** specificato.</span><span class="sxs-lookup"><span data-stu-id="e64cc-160">When the query is executed with a call to **execute** on the **CloudTable** object, it returns an **Iterator** with the **CustomerEntity** result type specified.</span></span> <span data-ttu-id="e64cc-161">Per usufruire dei risultati, è quindi possibile utilizzare l'oggetto **Iterator** restituito in ogni ciclo.</span><span class="sxs-lookup"><span data-stu-id="e64cc-161">You can then use the **Iterator** returned in a for each loop to consume the results.</span></span> <span data-ttu-id="e64cc-162">Il codice seguente consente di stampare sulla console i campi di ogni entità inclusa nei risultati della query.</span><span class="sxs-lookup"><span data-stu-id="e64cc-162">This code prints the fields of each entity in the query results to the console.</span></span>

```java
try
{
    // Define constants for filters.
    final String PARTITION_KEY = "PartitionKey";
    final String ROW_KEY = "RowKey";
    final String TIMESTAMP = "Timestamp";

    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where the partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Specify a partition query, using "Smith" as the partition key filter.
    TableQuery<CustomerEntity> partitionQuery =
        TableQuery.from(CustomerEntity.class)
        .where(partitionFilter);

    // Loop through the results, displaying information about the entity.
    for (CustomerEntity entity : cloudTable.execute(partitionQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="e64cc-163">Procedura: recuperare un intervallo di entità in una partizione</span><span class="sxs-lookup"><span data-stu-id="e64cc-163">How to: Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="e64cc-164">Se non si desidera eseguire una query su tutte le entità di una partizione, è possibile specificare un intervallo usando gli operatori di confronto in un filtro.</span><span class="sxs-lookup"><span data-stu-id="e64cc-164">If you don't want to query all the entities in a partition, you can specify a range by using comparison operators in a filter.</span></span> <span data-ttu-id="e64cc-165">Nel codice seguente vengono combinati due filtri per recuperare tutte le entità della partizione "Smith" in cui la chiave di riga (nome) inizia con una lettera che precede la 'E' nell'alfabeto</span><span class="sxs-lookup"><span data-stu-id="e64cc-165">The following code combines two filters to get all entities in partition "Smith" where the row key (first name) starts with a letter up to 'E' in the alphabet.</span></span> <span data-ttu-id="e64cc-166">e quindi stampare i risultati della query.</span><span class="sxs-lookup"><span data-stu-id="e64cc-166">Then it prints the query results.</span></span> <span data-ttu-id="e64cc-167">Se si utilizzano le entità aggiunte alla tabella nella sezione di inserimento batch di questa guida, questa volta verranno restituite solo due entità, ovvero Ben e Denise Smith, mentre Jeff Smith non sarà incluso.</span><span class="sxs-lookup"><span data-stu-id="e64cc-167">If you use the entities added to the table in the batch insert section of this guide, only two entities are returned this time (Ben and Denise Smith); Jeff Smith is not included.</span></span>

```java
try
{
    // Define constants for filters.
    final String PARTITION_KEY = "PartitionKey";
    final String ROW_KEY = "RowKey";
    final String TIMESTAMP = "Timestamp";

    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where the partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Create a filter condition where the row key is less than the letter "E".
    String rowFilter = TableQuery.generateFilterCondition(
        ROW_KEY,
        QueryComparisons.LESS_THAN,
        "E");

    // Combine the two conditions into a filter expression.
    String combinedFilter = TableQuery.combineFilters(partitionFilter,
        Operators.AND, rowFilter);

    // Specify a range query, using "Smith" as the partition key,
    // with the row key being up to the letter "E".
    TableQuery<CustomerEntity> rangeQuery =
        TableQuery.from(CustomerEntity.class)
        .where(combinedFilter);

    // Loop through the results, displaying information about the entity
    for (CustomerEntity entity : cloudTable.execute(rangeQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-single-entity"></a><span data-ttu-id="e64cc-168">Procedura: recuperare una singola entità</span><span class="sxs-lookup"><span data-stu-id="e64cc-168">How to: Retrieve a single entity</span></span>
<span data-ttu-id="e64cc-169">Per recuperare una singola entità specifica, è possibile scrivere una query.</span><span class="sxs-lookup"><span data-stu-id="e64cc-169">You can write a query to retrieve a single, specific entity.</span></span> <span data-ttu-id="e64cc-170">Il codice seguente chiama **TableOperation.retrieve** con i parametri della chiave di partizione e della chiave di riga per specificare il cliente "Jeff Smith", invece di creare un oggetto **TableQuery** e usare filtri per eseguire la stessa operazione.</span><span class="sxs-lookup"><span data-stu-id="e64cc-170">The following code calls **TableOperation.retrieve** with partition key and row key parameters to specify the customer "Jeff Smith", instead of creating a **TableQuery** and using filters to do the same thing.</span></span> <span data-ttu-id="e64cc-171">Quando si esegue l'operazione di recupero viene restituita una sola entità piuttosto che una raccolta.</span><span class="sxs-lookup"><span data-stu-id="e64cc-171">When executed, the retrieve operation returns just one entity, rather than a collection.</span></span> <span data-ttu-id="e64cc-172">Il metodo **getResultAsType** esegue il cast del risultato al tipo di destinazione dell'assegnazione, un oggetto **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="e64cc-172">The **getResultAsType** method casts the result to the type of the assignment target, a **CustomerEntity** object.</span></span> <span data-ttu-id="e64cc-173">Se questo tipo non è compatibile con il tipo specificato per la query, verrà generata un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="e64cc-173">If this type is not compatible with the type specified for the query, an exception will be thrown.</span></span> <span data-ttu-id="e64cc-174">Viene restituito un valore Null se per nessuna entità è disponibile una corrispondenza esatta di chiave di riga e chiave di partizione.</span><span class="sxs-lookup"><span data-stu-id="e64cc-174">A null value is returned if no entity has an exact partition and row key match.</span></span> <span data-ttu-id="e64cc-175">La specifica delle chiavi di partizione e di riga in una query costituisce la soluzione più rapida per recuperare una singola entità dal servizio tabelle.</span><span class="sxs-lookup"><span data-stu-id="e64cc-175">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the Table service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve the entity with partition key of "Smith" and row key of "Jeff"
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit the operation to the table service and get the specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Output the entity.
    if (specificEntity != null)
    {
        System.out.println(specificEntity.getPartitionKey() +
            " " + specificEntity.getRowKey() +
            "\t" + specificEntity.getEmail() +
            "\t" + specificEntity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-modify-an-entity"></a><span data-ttu-id="e64cc-176">Procedura: modificare un'entità</span><span class="sxs-lookup"><span data-stu-id="e64cc-176">How to: Modify an entity</span></span>
<span data-ttu-id="e64cc-177">Per modificare un'entità, recuperarla dal servizio tabelle, modificare l'oggetto entità e quindi salvare le modifiche nel servizio tabelle con un'operazione di sostituzione o unione.</span><span class="sxs-lookup"><span data-stu-id="e64cc-177">To modify an entity, retrieve it from the table service, make changes to the entity object, and save the changes back to the table service with a replace or merge operation.</span></span> <span data-ttu-id="e64cc-178">Il codice seguente consente di modificare il numero di telefono di un cliente esistente.</span><span class="sxs-lookup"><span data-stu-id="e64cc-178">The following code changes an existing customer's phone number.</span></span> <span data-ttu-id="e64cc-179">Anziché **TableOperation.insert** come effettuato in precedenza per l'inserimento, in questo codice viene chiamato **TableOperation.replace**.</span><span class="sxs-lookup"><span data-stu-id="e64cc-179">Instead of calling **TableOperation.insert** like we did to insert, this code calls **TableOperation.replace**.</span></span> <span data-ttu-id="e64cc-180">Il metodo **CloudTable.execute** chiama il servizio tabelle e l'entità viene sostituita a meno che non sia stata modificata da un'altra applicazione da quando è stata recuperata dall'applicazione corrente.</span><span class="sxs-lookup"><span data-stu-id="e64cc-180">The **CloudTable.execute** method calls the table service, and the entity is replaced, unless another application changed it in the time since this application retrieved it.</span></span> <span data-ttu-id="e64cc-181">Se si verifica questa situazione, viene generata un'eccezione, pertanto è necessario recuperare, modificare e salvare di nuovo l'entità.</span><span class="sxs-lookup"><span data-stu-id="e64cc-181">When that happens, an exception is thrown, and the entity must be retrieved, modified, and saved again.</span></span> <span data-ttu-id="e64cc-182">Questo schema di ripetizione dei tentativi che supporta la concorrenza ottimistica è comune in un sistema di sistema di archiviazione distribuita.</span><span class="sxs-lookup"><span data-stu-id="e64cc-182">This optimistic concurrency retry pattern is common in a distributed storage system.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve the entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit the operation to the table service and get the specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Specify a new phone number.
    specificEntity.setPhoneNumber("425-555-0105");

    // Create an operation to replace the entity.
    TableOperation replaceEntity = TableOperation.replace(specificEntity);

    // Submit the operation to the table service.
    cloudTable.execute(replaceEntity);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-query-a-subset-of-entity-properties"></a><span data-ttu-id="e64cc-183">Procedura: eseguire query su un subset di proprietà di entità</span><span class="sxs-lookup"><span data-stu-id="e64cc-183">How to: Query a subset of entity properties</span></span>
<span data-ttu-id="e64cc-184">Mediante una query su una tabella è possibile recuperare solo alcune proprietà da un'entità.</span><span class="sxs-lookup"><span data-stu-id="e64cc-184">A query to a table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="e64cc-185">Questa tecnica, denominata proiezione, consente di ridurre la larghezza di banda e di migliorare le prestazioni della query, in particolare per entità di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="e64cc-185">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="e64cc-186">La query nel codice seguente utilizza il metodo **select** per restituire solo gli indirizzi di posta elettronica di entità nella tabella.</span><span class="sxs-lookup"><span data-stu-id="e64cc-186">The query in the following code uses the **select** method to return only the email addresses of entities in the table.</span></span> <span data-ttu-id="e64cc-187">I risultati vengono proiettati in una raccolta di **stringhe** con l'aiuto di un oggetto **EntityResolver**, che esegue la conversione di tipo sulle entità restituite dal server.</span><span class="sxs-lookup"><span data-stu-id="e64cc-187">The results are projected into a collection of **String** with the help of an **EntityResolver**, which does the type conversion on the entities returned from the server.</span></span> <span data-ttu-id="e64cc-188">Per altre informazioni sulla proiezione, vedere [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection] (Tabelle di Azure: Introduzione di Upsert e proiezione di query in tabelle di Azure).</span><span class="sxs-lookup"><span data-stu-id="e64cc-188">You can learn more about projection in [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span> <span data-ttu-id="e64cc-189">Si noti che la proiezione non è supportata nell'emulatore di archiviazione locale, pertanto questo codice viene eseguito solo se si utilizza un account sul servizio tabelle.</span><span class="sxs-lookup"><span data-stu-id="e64cc-189">Note that projection is not supported on the local storage emulator, so this code runs only when using an account on the table service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Define a projection query that retrieves only the Email property
    TableQuery<CustomerEntity> projectionQuery =
        TableQuery.from(CustomerEntity.class)
        .select(new String[] {"Email"});

    // Define a Entity resolver to project the entity to the Email value.
    EntityResolver<String> emailResolver = new EntityResolver<String>() {
        @Override
        public String resolve(String PartitionKey, String RowKey, Date timeStamp, HashMap<String, EntityProperty> properties, String etag) {
            return properties.get("Email").getValueAsString();
        }
    };

    // Loop through the results, displaying the Email values.
    for (String projectedString :
        cloudTable.execute(projectionQuery, emailResolver)) {
            System.out.println(projectedString);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-or-replace-an-entity"></a><span data-ttu-id="e64cc-190">Procedura: inserire o sostituire un'entità</span><span class="sxs-lookup"><span data-stu-id="e64cc-190">How to: Insert or Replace an entity</span></span>
<span data-ttu-id="e64cc-191">Spesso si desidera aggiungere un'entità a una tabella senza sapere se sia già esistente nella tabella.</span><span class="sxs-lookup"><span data-stu-id="e64cc-191">Often you want to add an entity to a table without knowing if it already exists in the table.</span></span> <span data-ttu-id="e64cc-192">Con un'operazione di inserimento o sostituzione è possibile creare una singola richiesta e inserire l'entità se non esiste oppure sostituirla se è già esistente.</span><span class="sxs-lookup"><span data-stu-id="e64cc-192">An insert-or-replace operation allows you to make a single request which will insert the entity if it does not exist or replace the existing one if it does.</span></span> <span data-ttu-id="e64cc-193">Sulla base degli esempi precedenti, il codice seguente consente di inserire o sostituire l'entità per "Walter Harp".</span><span class="sxs-lookup"><span data-stu-id="e64cc-193">Building on prior examples, the following code inserts or replaces the entity for "Walter Harp".</span></span> <span data-ttu-id="e64cc-194">Dopo aver creato una nuova entità, nel codice viene chiamato il metodo **TableOperation.insertOrReplace** .</span><span class="sxs-lookup"><span data-stu-id="e64cc-194">After creating a new entity, this code calls the **TableOperation.insertOrReplace** method.</span></span> <span data-ttu-id="e64cc-195">Questo codice chiama quindi il metodo **execute** sull'oggetto **CloudTable** con la tabella e l'operazione di inserimento o sostituzione tabella come parametri.</span><span class="sxs-lookup"><span data-stu-id="e64cc-195">This code then calls **execute** on the **CloudTable** object with the table and the insert or replace table operation as the parameters.</span></span> <span data-ttu-id="e64cc-196">Per aggiornare solo parte di un'entità, è invece possibile utilizzare il metodo **TableOperation.insertOrMerge** .</span><span class="sxs-lookup"><span data-stu-id="e64cc-196">To update only part of an entity, the **TableOperation.insertOrMerge** method can be used instead.</span></span> <span data-ttu-id="e64cc-197">Si noti che l'operazione di inserimento o sostituzione non è supportata nell'emulatore di archiviazione locale, pertanto questo codice viene eseguito solo se si usa un account sul servizio tabelle.</span><span class="sxs-lookup"><span data-stu-id="e64cc-197">Note that insert-or-replace is not supported on the local storage emulator, so this code runs only when using an account on the table service.</span></span> <span data-ttu-id="e64cc-198">Per altre informazioni sull'operazione di inserimento o sostituzione e l'operazione di inserimento o unione, vedere [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection] (Tabelle di Azure: Introduzione di Upsert e proiezione di query in tabelle di Azure).</span><span class="sxs-lookup"><span data-stu-id="e64cc-198">You can learn more about insert-or-replace and insert-or-merge in this [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer5 = new CustomerEntity("Harp", "Walter");
    customer5.setEmail("Walter@contoso.com");
    customer5.setPhoneNumber("425-555-0106");

    // Create an operation to add the new customer to the people table.
    TableOperation insertCustomer5 = TableOperation.insertOrReplace(customer5);

    // Submit the operation to the table service.
    cloudTable.execute(insertCustomer5);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-an-entity"></a><span data-ttu-id="e64cc-199">Procedura: eliminare un'entità</span><span class="sxs-lookup"><span data-stu-id="e64cc-199">How to: Delete an entity</span></span>
<span data-ttu-id="e64cc-200">È possibile eliminare facilmente un'entità dopo averla recuperata.</span><span class="sxs-lookup"><span data-stu-id="e64cc-200">You can easily delete an entity after you have retrieved it.</span></span> <span data-ttu-id="e64cc-201">Dopo il recupero dell'entità, chiamare **TableOperation.delete** con l'entità da eliminare.</span><span class="sxs-lookup"><span data-stu-id="e64cc-201">Once the entity is retrieved, call **TableOperation.delete** with the entity to delete.</span></span> <span data-ttu-id="e64cc-202">Chiamare **execute** sull'oggetto **CloudTable**.</span><span class="sxs-lookup"><span data-stu-id="e64cc-202">Then call **execute** on the **CloudTable** object.</span></span> <span data-ttu-id="e64cc-203">Il codice seguente consente di recuperare ed eliminare un'entità customer.</span><span class="sxs-lookup"><span data-stu-id="e64cc-203">The following code retrieves and deletes a customer entity.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create an operation to retrieve the entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff = TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Retrieve the entity with partition key of "Smith" and row key of "Jeff".
    CustomerEntity entitySmithJeff =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Create an operation to delete the entity.
    TableOperation deleteSmithJeff = TableOperation.delete(entitySmithJeff);

    // Submit the delete operation to the table service.
    cloudTable.execute(deleteSmithJeff);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-table"></a><span data-ttu-id="e64cc-204">Procedura: eliminare una tabella</span><span class="sxs-lookup"><span data-stu-id="e64cc-204">How to: Delete a table</span></span>
<span data-ttu-id="e64cc-205">Nell'esempio di codice seguente viene infine illustrato come eliminare una tabella da un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e64cc-205">Finally, the following code deletes a table from a storage account.</span></span> <span data-ttu-id="e64cc-206">Una tabella eliminata non potrà essere creata nuovamente per un certo periodo di tempo, di solito inferiore a 40 secondi.</span><span class="sxs-lookup"><span data-stu-id="e64cc-206">A table which has been deleted will be unavailable to be recreated for a period of time following the deletion, usually less than forty seconds.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Delete the table and all its data if it exists.
    CloudTable cloudTable = tableClient.getTableReference("people");
    cloudTable.deleteIfExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```
[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="next-steps"></a><span data-ttu-id="e64cc-207">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e64cc-207">Next steps</span></span>

* <span data-ttu-id="e64cc-208">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) è un'app autonoma gratuita di Microsoft che consente di rappresentare facilmente dati di Archiviazione di Azure in Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="e64cc-208">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="e64cc-209">[Azure Storage SDK per Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="e64cc-209">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="e64cc-210">[Riferimento all'SDK del client di archiviazione di Azure][Riferimento all'SDK del client di archiviazione di Azure]</span><span class="sxs-lookup"><span data-stu-id="e64cc-210">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="e64cc-211">[API REST di Archiviazione di Azure][Azure Storage REST API]</span><span class="sxs-lookup"><span data-stu-id="e64cc-211">[Azure Storage REST API][Azure Storage REST API]</span></span>
* <span data-ttu-id="e64cc-212">[Blog del team di Archiviazione di Azure][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="e64cc-212">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

<span data-ttu-id="e64cc-213">Per altre informazioni, vedere [Azure for Java developers](/java/azure) (Azure per sviluppatori Java).</span><span class="sxs-lookup"><span data-stu-id="e64cc-213">For more information, visit [Azure for Java developers](/java/azure).</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[Riferimento all'SDK del client di archiviazione di Azure]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Tables: Introducing Upsert and Query Projection]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx
