---
title: aaaHow toouse archiviazione tabelle da Java | Documenti Microsoft
description: Archiviare dati strutturati in un cloud di hello tramite l'archiviazione tabelle di Azure, un archivio dati NoSQL.
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
ms.openlocfilehash: 20d03e867219cc254da8dad37cf3cf61bca65671
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-java"></a><span data-ttu-id="7e1dc-103">Come toouse archiviazione tabelle da Java</span><span class="sxs-lookup"><span data-stu-id="7e1dc-103">How toouse Table storage from Java</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="7e1dc-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="7e1dc-104">Overview</span></span>
<span data-ttu-id="7e1dc-105">Questa guida illustra come gli scenari comuni di tooperform utilizzando hello servizio di archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-105">This guide will show you how tooperform common scenarios using hello Azure Table storage service.</span></span> <span data-ttu-id="7e1dc-106">esempi di Hello sono scritti in Java e usano hello [Azure Storage SDK per Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="7e1dc-106">hello samples are written in Java and use hello [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="7e1dc-107">Hello scenari trattati includono **creazione**, **elenco**, e **eliminazione** tabelle, nonché **inserimento**,  **l'esecuzione di query**, **modifica**, e **eliminazione** entità in una tabella.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-107">hello scenarios covered include **creating**, **listing**, and **deleting** tables, as well as **inserting**, **querying**, **modifying**, and **deleting** entities in a table.</span></span> <span data-ttu-id="7e1dc-108">Per ulteriori informazioni sulle tabelle, vedere hello [passaggi successivi](#Next-Steps) sezione.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-108">For more information on tables, see hello [Next steps](#Next-Steps) section.</span></span>

<span data-ttu-id="7e1dc-109">Nota: per gli sviluppatori che usano il servizio di archiviazione di Azure in dispositivi Android, è disponibile un SDK specifico.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-109">Note: An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="7e1dc-110">Per ulteriori informazioni, vedere hello [Azure Storage SDK per Android][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="7e1dc-110">For more information, see hello [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="7e1dc-111">Creare un'applicazione Java</span><span class="sxs-lookup"><span data-stu-id="7e1dc-111">Create a Java application</span></span>
<span data-ttu-id="7e1dc-112">In questa guida si utilizzeranno le funzionalità di archiviazione che possono essere eseguite in un'applicazione Java in locale o nel codice in esecuzione in un ruolo Web, in un ruolo di lavoro o in Azure.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-112">In this guide, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="7e1dc-113">toodo in tal caso, sarà necessario tooinstall hello Java Development Kit (JDK) e creare un account di archiviazione di Azure nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-113">toodo so, you will need tooinstall hello Java Development Kit (JDK) and create an Azure storage account in your Azure subscription.</span></span> <span data-ttu-id="7e1dc-114">Dopo aver eseguito questa operazione, sarà necessario tooverify che il sistema di sviluppo soddisfi i requisiti minimi di hello e le dipendenze sono elencate in hello [Azure Storage SDK per Java] [ Azure Storage SDK for Java] repository in GitHub.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-114">Once you have done so, you will need tooverify that your development system meets hello minimum requirements and dependencies which are listed in hello [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="7e1dc-115">Se il sistema soddisfi tali requisiti, è possibile seguire le istruzioni di hello per scaricare e installare le librerie di archiviazione di Azure hello for Java nel sistema da quel repository.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-115">If your system meets those requirements, you can follow hello instructions for downloading and installing hello Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="7e1dc-116">Dopo aver completato queste attività, sarà in grado di toocreate un'applicazione Java che utilizza esempi hello in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-116">Once you have completed those tasks, you will be able toocreate a Java application which uses hello examples in this article.</span></span>

## <a name="configure-your-application-tooaccess-table-storage"></a><span data-ttu-id="7e1dc-117">Configurare l'archiviazione tabelle tooaccess di applicazione</span><span class="sxs-lookup"><span data-stu-id="7e1dc-117">Configure your application tooaccess table storage</span></span>
<span data-ttu-id="7e1dc-118">Aggiungere hello dopo l'inizio di toohello di istruzioni di importazione del file di Java hello in cui si desidera tabelle di tooaccess le API di archiviazione di toouse Microsoft Azure:</span><span class="sxs-lookup"><span data-stu-id="7e1dc-118">Add hello following import statements toohello top of hello Java file where you want toouse Microsoft Azure storage APIs tooaccess tables:</span></span>

```java
// Include hello following imports toouse table APIs
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.table.*;
import com.microsoft.azure.storage.table.TableQuery.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="7e1dc-119">Impostare una stringa di connessione di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="7e1dc-119">Set up an Azure storage connection string</span></span>
<span data-ttu-id="7e1dc-120">Un client di archiviazione di Azure Usa un endpoint di toostore stringa di connessione archiviazione e le credenziali per l'accesso a servizi di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-120">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="7e1dc-121">Quando si esegue un'applicazione client, è necessario fornire una stringa di connessione di archiviazione hello in hello seguente formato, utilizzando nome hello dell'account di archiviazione e chiave di accesso primaria per l'account di archiviazione hello elencati in hello hello [il portale di Azure](https://portal.azure.com)per hello *AccountName* e *AccountKey* valori.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-121">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello Primary access key for hello storage account listed in hello [Azure portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="7e1dc-122">In questo esempio viene illustrato come dichiarare una stringa di connessione di un campo statico toohold hello:</span><span class="sxs-lookup"><span data-stu-id="7e1dc-122">This example shows how you can declare a static field toohold hello connection string:</span></span>

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="7e1dc-123">In un'applicazione in esecuzione all'interno di un ruolo in Microsoft Azure, questa stringa può essere archiviata nel file di configurazione del servizio hello *ServiceConfiguration. cscfg*ed è possibile accedervi con una chiamata toohello  **RoleEnvironment.getConfigurationSettings** metodo.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-123">In an application running within a role in Microsoft Azure, this string can be stored in hello service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call toohello **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="7e1dc-124">Di seguito è riportato un esempio di recupero della stringa di connessione hello da un **impostazione** elemento denominato *StorageConnectionString* nel file di configurazione del servizio hello:</span><span class="sxs-lookup"><span data-stu-id="7e1dc-124">Here's an example of getting hello connection string from a **Setting** element named *StorageConnectionString* in hello service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="7e1dc-125">Hello negli esempi seguenti si presuppongono che si usa uno di questi due metodi tooget hello stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-125">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="how-to-create-a-table"></a><span data-ttu-id="7e1dc-126">Procedura: creare una tabella</span><span class="sxs-lookup"><span data-stu-id="7e1dc-126">How to: Create a table</span></span>
<span data-ttu-id="7e1dc-127">Per ottenere oggetti di riferimento per tabelle ed entità, è possibile usare un oggetto **CloudTableClient**.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-127">A **CloudTableClient** object lets you get reference objects for tables and entities.</span></span> <span data-ttu-id="7e1dc-128">Hello codice seguente viene creata una **CloudTableClient** dell'oggetto e lo usa toocreate un nuovo **CloudTable** oggetto che rappresenta una tabella denominata "persone".</span><span class="sxs-lookup"><span data-stu-id="7e1dc-128">hello following code creates a **CloudTableClient** object and uses it toocreate a new **CloudTable** object which represents a table named "people".</span></span> <span data-ttu-id="7e1dc-129">(Nota: esistono altri modi toocreate **CloudStorageAccount** oggetti; per ulteriori informazioni, vedere **CloudStorageAccount** in hello [Azure Storage Client SDK riferimento].)</span><span class="sxs-lookup"><span data-stu-id="7e1dc-129">(Note: There are additional ways toocreate **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in hello [Azure Storage Client SDK Reference].)</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create hello table if it doesn't exist.
    String tableName = "people";
    CloudTable cloudTable = tableClient.getTableReference(tableName);
    cloudTable.createIfNotExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-hello-tables"></a><span data-ttu-id="7e1dc-130">Procedura: elencare le tabelle di hello</span><span class="sxs-lookup"><span data-stu-id="7e1dc-130">How to: List hello tables</span></span>
<span data-ttu-id="7e1dc-131">un elenco di tabelle, chiamata hello tooget **CloudTableClient.listTables()** metodo tooretrieve un elenco dei nomi di tabella iterabile.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-131">tooget a list of tables, call hello **CloudTableClient.listTables()** method tooretrieve an iterable list of table names.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Loop through hello collection of table names.
    for (String table : tableClient.listTables())
    {
        // Output each table name.
        System.out.println(table);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-an-entity-tooa-table"></a><span data-ttu-id="7e1dc-132">Procedura: aggiungere una tabella tooa entità</span><span class="sxs-lookup"><span data-stu-id="7e1dc-132">How to: Add an entity tooa table</span></span>
<span data-ttu-id="7e1dc-133">Eseguire il mapping di entità tooJava oggetti usando una classe personalizzata che implementa **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-133">Entities map tooJava objects using a custom class implementing **TableEntity**.</span></span> <span data-ttu-id="7e1dc-134">Per praticità, hello **TableServiceEntity** implementa **TableEntity** e utilizza le proprietà di toomap reflection metodi toogetter e set denominati per hello proprietà.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-134">For convenience, hello **TableServiceEntity** class implements **TableEntity** and uses reflection toomap properties toogetter and setter methods named for hello properties.</span></span> <span data-ttu-id="7e1dc-135">tooadd tabella tooa un'entità, creare innanzitutto una classe che definisce le proprietà di hello dell'entità.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-135">tooadd an entity tooa table, first create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="7e1dc-136">Hello codice seguente definisce una classe di entità che utilizza nome hello del cliente come chiave di riga hello e last name come chiave di partizione hello.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-136">hello following code defines an entity class which uses hello customer's first name as hello row key, and last name as hello partition key.</span></span> <span data-ttu-id="7e1dc-137">Insieme, di partizione e chiave di riga identificano entità hello nella tabella di hello.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-137">Together, an entity's partition and row key uniquely identify hello entity in hello table.</span></span> <span data-ttu-id="7e1dc-138">Entità con hello stessa chiave di partizione è possibile eseguire query più velocemente rispetto a quelle con le chiavi di partizione diverso.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-138">Entities with hello same partition key can be queried faster than those with different partition keys.</span></span>

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

<span data-ttu-id="7e1dc-139">Per le operazioni su tabella che interessano entità è necessario un oggetto **TableServiceContext** .</span><span class="sxs-lookup"><span data-stu-id="7e1dc-139">Table operations involving entities require a **TableOperation** object.</span></span> <span data-ttu-id="7e1dc-140">Questo oggetto definisce hello toobe di operazione eseguita su un'entità che può essere eseguita con un **CloudTable** oggetto.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-140">This object defines hello operation toobe performed on an entity, which can be executed with a **CloudTable** object.</span></span> <span data-ttu-id="7e1dc-141">esempio di codice Hello crea una nuova istanza di hello **CustomerEntity** classe con alcuni toobe dati cliente archiviati.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-141">hello following code creates a new instance of hello **CustomerEntity** class with some customer data toobe stored.</span></span> <span data-ttu-id="7e1dc-142">Hello successiva chiama codice **TableOperation.insertOrReplace** toocreate un **TableOperation** tooinsert un'entità dell'oggetto in una tabella, e associa hello nuovi **CustomerEntity**con esso.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-142">hello code next calls **TableOperation.insertOrReplace** toocreate a **TableOperation** object tooinsert an entity into a table, and associates hello new **CustomerEntity** with it.</span></span> <span data-ttu-id="7e1dc-143">Infine, il codice hello chiama hello **eseguire** metodo hello **CloudTable** oggetto specificando una tabella "persone" hello e hello nuovo **TableOperation**, che invia quindi un entità della richiesta toohello archiviazione servizio tooinsert hello nuovo cliente nella tabella "persone" hello, o sostituire entità hello se esiste già.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-143">Finally, hello code calls hello **execute** method on hello **CloudTable** object, specifying hello "people" table and hello new **TableOperation**, which then sends a request toohello storage service tooinsert hello new customer entity into hello "people" table, or replace hello entity if it already exists.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.setEmail("Walter@contoso.com");
    customer1.setPhoneNumber("425-555-0101");

    // Create an operation tooadd hello new customer toohello people table.
    TableOperation insertCustomer1 = TableOperation.insertOrReplace(customer1);

    // Submit hello operation toohello table service.
    cloudTable.execute(insertCustomer1);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-a-batch-of-entities"></a><span data-ttu-id="7e1dc-144">Procedura: inserire un batch di entità</span><span class="sxs-lookup"><span data-stu-id="7e1dc-144">How to: Insert a batch of entities</span></span>
<span data-ttu-id="7e1dc-145">È possibile inserire un batch di servizio tabelle toohello di entità in un'unica operazione di scrittura.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-145">You can insert a batch of entities toohello table service in one write operation.</span></span> <span data-ttu-id="7e1dc-146">Hello codice seguente viene creata una **TableBatchOperation** dell'oggetto, quindi aggiunge tre tooit operazioni di inserimento.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-146">hello following code creates a **TableBatchOperation** object, then adds three insert operations tooit.</span></span> <span data-ttu-id="7e1dc-147">Ogni operazione di inserimento viene aggiunto per la creazione di un nuovo oggetto entità, impostarne i valori e chiamando quindi hello **inserire** metodo hello **TableBatchOperation** entità hello tooassociate con un nuovo oggetto operazione di inserimento.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-147">Each insert operation is added by creating a new entity object, setting its values, and then calling hello **insert** method on hello **TableBatchOperation** object tooassociate hello entity with a new insert operation.</span></span> <span data-ttu-id="7e1dc-148">Quindi hello codice chiama **eseguire** su hello **CloudTable** oggetto specificando una tabella di "people" hello e hello **TableBatchOperation** oggetto, che invia il batch hello della tabella servizio di archiviazione toohello operazioni in una singola richiesta.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-148">Then hello code calls **execute** on hello **CloudTable** object, specifying hello "people" table and hello **TableBatchOperation** object, which sends hello batch of table operations toohello storage service in a single request.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Define a batch operation.
    TableBatchOperation batchOperation = new TableBatchOperation();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a customer entity tooadd toohello table.
    CustomerEntity customer = new CustomerEntity("Smith", "Jeff");
    customer.setEmail("Jeff@contoso.com");
    customer.setPhoneNumber("425-555-0104");
    batchOperation.insertOrReplace(customer);

    // Create another customer entity tooadd toohello table.
    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.setEmail("Ben@contoso.com");
    customer2.setPhoneNumber("425-555-0102");
    batchOperation.insertOrReplace(customer2);

    // Create a third customer entity tooadd toohello table.
    CustomerEntity customer3 = new CustomerEntity("Smith", "Denise");
    customer3.setEmail("Denise@contoso.com");
    customer3.setPhoneNumber("425-555-0103");
    batchOperation.insertOrReplace(customer3);

    // Execute hello batch of operations on hello "people" table.
    cloudTable.execute(batchOperation);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="7e1dc-149">Toonote alcune operazioni per le operazioni batch:</span><span class="sxs-lookup"><span data-stu-id="7e1dc-149">Some things toonote on batch operations:</span></span>

* <span data-ttu-id="7e1dc-150">È possibile eseguire backup too100 insert, delete, merge, replace, insert o merge, inserire o sostituire operazioni in qualsiasi combinazione in un unico batch.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-150">You can perform up too100 insert, delete, merge, replace, insert or merge, and insert or replace operations in any combination in a single batch.</span></span>
* <span data-ttu-id="7e1dc-151">Un'operazione batch può avere un'operazione di recupero, se è l'unica operazione di hello in batch hello.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-151">A batch operation can have a retrieve operation, if it is hello only operation in hello batch.</span></span>
* <span data-ttu-id="7e1dc-152">Tutte le entità in una singola operazione batch devono avere hello stessa chiave di partizione.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-152">All entities in a single batch operation must have hello same partition key.</span></span>
* <span data-ttu-id="7e1dc-153">Un'operazione batch è limitato tooa payload di dati di 4MB.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-153">A batch operation is limited tooa 4MB data payload.</span></span>

## <a name="how-to-retrieve-all-entities-in-a-partition"></a><span data-ttu-id="7e1dc-154">Procedura: recuperare tutte le entità di una partizione</span><span class="sxs-lookup"><span data-stu-id="7e1dc-154">How to: Retrieve all entities in a partition</span></span>
<span data-ttu-id="7e1dc-155">tooquery una tabella per le entità in una partizione, è possibile utilizzare un **TableQuery**.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-155">tooquery a table for entities in a partition, you can use a **TableQuery**.</span></span> <span data-ttu-id="7e1dc-156">Chiamare **TableQuery.from** toocreate una query su una determinata tabella che restituisce un tipo di risultato specificato.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-156">Call **TableQuery.from** toocreate a query on a particular table that returns a specified result type.</span></span> <span data-ttu-id="7e1dc-157">Hello codice seguente specifica un filtro per le entità in cui la chiave di partizione hello 'Smith'.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-157">hello following code specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="7e1dc-158">**TableQuery.generateFilterCondition** è un metodo helper toocreate filtri per le query.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-158">**TableQuery.generateFilterCondition** is a helper method toocreate filters for queries.</span></span> <span data-ttu-id="7e1dc-159">Chiamare **in** su hello riferimento restituito da hello **TableQuery.from** query toohello del metodo tooapply hello filtro.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-159">Call **where** on hello reference returned by hello **TableQuery.from** method tooapply hello filter toohello query.</span></span> <span data-ttu-id="7e1dc-160">Quando viene eseguita la query hello con una chiamata troppo**eseguire** su hello **CloudTable** specificato, viene restituito un **iteratore** con hello **CustomerEntity**specificato tipo di risultato.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-160">When hello query is executed with a call too**execute** on hello **CloudTable** object, it returns an **Iterator** with hello **CustomerEntity** result type specified.</span></span> <span data-ttu-id="7e1dc-161">È quindi possibile utilizzare hello **iteratore** restituiti in un per ottenere risultati hello tooconsume ogni ciclo.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-161">You can then use hello **Iterator** returned in a for each loop tooconsume hello results.</span></span> <span data-ttu-id="7e1dc-162">Questo codice visualizza i campi di ogni entità nella console di toohello risultati query hello hello.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-162">This code prints hello fields of each entity in hello query results toohello console.</span></span>

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

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where hello partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Specify a partition query, using "Smith" as hello partition key filter.
    TableQuery<CustomerEntity> partitionQuery =
        TableQuery.from(CustomerEntity.class)
        .where(partitionFilter);

    // Loop through hello results, displaying information about hello entity.
    for (CustomerEntity entity : cloudTable.execute(partitionQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="7e1dc-163">Procedura: recuperare un intervallo di entità in una partizione</span><span class="sxs-lookup"><span data-stu-id="7e1dc-163">How to: Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="7e1dc-164">Se non si desidera tooquery tutte le entità hello in una partizione, è possibile specificare un intervallo con gli operatori di confronto in un filtro.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-164">If you don't want tooquery all hello entities in a partition, you can specify a range by using comparison operators in a filter.</span></span> <span data-ttu-id="7e1dc-165">Hello seguente combina codice due filtri tooget tutte le entità nella partizione "Smith" in cui la chiave di riga hello (nome) inizia con una lettera di too'E' alfabeto hello.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-165">hello following code combines two filters tooget all entities in partition "Smith" where hello row key (first name) starts with a letter up too'E' in hello alphabet.</span></span> <span data-ttu-id="7e1dc-166">Vengono quindi i risultati di query hello.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-166">Then it prints hello query results.</span></span> <span data-ttu-id="7e1dc-167">Se si utilizza hello entità toohello aggiunto tabella batch hello inserire sezione di questa Guida, solo due entità vengono restituite a questo momento (Ben e Denise Smith); Jeff Smith non è incluso.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-167">If you use hello entities added toohello table in hello batch insert section of this guide, only two entities are returned this time (Ben and Denise Smith); Jeff Smith is not included.</span></span>

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

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where hello partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Create a filter condition where hello row key is less than hello letter "E".
    String rowFilter = TableQuery.generateFilterCondition(
        ROW_KEY,
        QueryComparisons.LESS_THAN,
        "E");

    // Combine hello two conditions into a filter expression.
    String combinedFilter = TableQuery.combineFilters(partitionFilter,
        Operators.AND, rowFilter);

    // Specify a range query, using "Smith" as hello partition key,
    // with hello row key being up toohello letter "E".
    TableQuery<CustomerEntity> rangeQuery =
        TableQuery.from(CustomerEntity.class)
        .where(combinedFilter);

    // Loop through hello results, displaying information about hello entity
    for (CustomerEntity entity : cloudTable.execute(rangeQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-single-entity"></a><span data-ttu-id="7e1dc-168">Procedura: recuperare una singola entità</span><span class="sxs-lookup"><span data-stu-id="7e1dc-168">How to: Retrieve a single entity</span></span>
<span data-ttu-id="7e1dc-169">È possibile scrivere un tooretrieve query un'entità singola e specifica.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-169">You can write a query tooretrieve a single, specific entity.</span></span> <span data-ttu-id="7e1dc-170">codice Hello seguente chiama **TableOperation.retrieve** con partizione chiave e riga di parametri chiave toospecify hello cliente "Jeff Smith", anziché creare un **TableQuery** e l'utilizzo di hello toodo filtri Stessa cosa.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-170">hello following code calls **TableOperation.retrieve** with partition key and row key parameters toospecify hello customer "Jeff Smith", instead of creating a **TableQuery** and using filters toodo hello same thing.</span></span> <span data-ttu-id="7e1dc-171">Quando viene eseguita, hello recuperare operazione restituisce una sola entità, anziché una raccolta.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-171">When executed, hello retrieve operation returns just one entity, rather than a collection.</span></span> <span data-ttu-id="7e1dc-172">Hello **getResultAsType** metodo esegue il cast di tipo di toohello hello risultato della destinazione di assegnazione hello, un **CustomerEntity** oggetto.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-172">hello **getResultAsType** method casts hello result toohello type of hello assignment target, a **CustomerEntity** object.</span></span> <span data-ttu-id="7e1dc-173">Se questo tipo non è compatibile con il tipo di hello specificato per la query hello, verrà generata un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-173">If this type is not compatible with hello type specified for hello query, an exception will be thrown.</span></span> <span data-ttu-id="7e1dc-174">Viene restituito un valore Null se per nessuna entità è disponibile una corrispondenza esatta di chiave di riga e chiave di partizione.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-174">A null value is returned if no entity has an exact partition and row key match.</span></span> <span data-ttu-id="7e1dc-175">Specifica le chiavi di partizione e di riga in una query è tooretrieve modo più veloce di hello una singola entità dal servizio tabelle hello.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-175">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello Table service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve hello entity with partition key of "Smith" and row key of "Jeff"
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit hello operation toohello table service and get hello specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Output hello entity.
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
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-modify-an-entity"></a><span data-ttu-id="7e1dc-176">Procedura: modificare un'entità</span><span class="sxs-lookup"><span data-stu-id="7e1dc-176">How to: Modify an entity</span></span>
<span data-ttu-id="7e1dc-177">toomodify un'entità, recuperarlo dal servizio tabelle hello, rendere l'oggetto entità toohello di modifiche e salvare le modifiche di hello del servizio tabelle toohello indietro con un'operazione di sostituzione o unione.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-177">toomodify an entity, retrieve it from hello table service, make changes toohello entity object, and save hello changes back toohello table service with a replace or merge operation.</span></span> <span data-ttu-id="7e1dc-178">Hello codice seguente modifica il numero di telefono del cliente esistente.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-178">hello following code changes an existing customer's phone number.</span></span> <span data-ttu-id="7e1dc-179">Anziché chiamare **TableOperation.insert** come abbiamo visto tooinsert, questo codice chiama **TableOperation.replace**.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-179">Instead of calling **TableOperation.insert** like we did tooinsert, this code calls **TableOperation.replace**.</span></span> <span data-ttu-id="7e1dc-180">Hello **CloudTable.execute** chiamate del servizio tabelle hello e l'entità hello viene sostituita, a meno che un'altra applicazione sono stati modificati da nel tempo hello questa applicazione è stato recuperato.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-180">hello **CloudTable.execute** method calls hello table service, and hello entity is replaced, unless another application changed it in hello time since this application retrieved it.</span></span> <span data-ttu-id="7e1dc-181">In questo caso, viene generata un'eccezione ed entità hello deve essere recuperato, modificato e salvato di nuovo.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-181">When that happens, an exception is thrown, and hello entity must be retrieved, modified, and saved again.</span></span> <span data-ttu-id="7e1dc-182">Questo schema di ripetizione dei tentativi che supporta la concorrenza ottimistica è comune in un sistema di sistema di archiviazione distribuita.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-182">This optimistic concurrency retry pattern is common in a distributed storage system.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit hello operation toohello table service and get hello specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Specify a new phone number.
    specificEntity.setPhoneNumber("425-555-0105");

    // Create an operation tooreplace hello entity.
    TableOperation replaceEntity = TableOperation.replace(specificEntity);

    // Submit hello operation toohello table service.
    cloudTable.execute(replaceEntity);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-query-a-subset-of-entity-properties"></a><span data-ttu-id="7e1dc-183">Procedura: eseguire query su un subset di proprietà di entità</span><span class="sxs-lookup"><span data-stu-id="7e1dc-183">How to: Query a subset of entity properties</span></span>
<span data-ttu-id="7e1dc-184">Una tabella di tooa query è possibile recuperare solo alcune proprietà di un'entità.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-184">A query tooa table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="7e1dc-185">Questa tecnica, denominata proiezione, consente di ridurre la larghezza di banda e di migliorare le prestazioni della query, in particolare per entità di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-185">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="7e1dc-186">query nel seguente codice hello Hello utilizza hello **selezionare** metodo tooreturn solo hello indirizzi di posta elettronica di entità nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-186">hello query in hello following code uses hello **select** method tooreturn only hello email addresses of entities in hello table.</span></span> <span data-ttu-id="7e1dc-187">Hello risultati vengono proiettati in un insieme di **stringa** insieme hello un **EntityResolver**, quale does hello sulle entità hello hello server ha restituito una conversione del tipo.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-187">hello results are projected into a collection of **String** with hello help of an **EntityResolver**, which does hello type conversion on hello entities returned from hello server.</span></span> <span data-ttu-id="7e1dc-188">Per altre informazioni sulla proiezione, vedere [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection] (Tabelle di Azure: Introduzione di Upsert e proiezione di query in tabelle di Azure).</span><span class="sxs-lookup"><span data-stu-id="7e1dc-188">You can learn more about projection in [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span> <span data-ttu-id="7e1dc-189">Si noti che proiezione non è supportata sull'emulatore di archiviazione locale di hello, pertanto questo codice viene eseguito solo quando si utilizza un account nel servizio tabelle hello.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-189">Note that projection is not supported on hello local storage emulator, so this code runs only when using an account on hello table service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Define a projection query that retrieves only hello Email property
    TableQuery<CustomerEntity> projectionQuery =
        TableQuery.from(CustomerEntity.class)
        .select(new String[] {"Email"});

    // Define a Entity resolver tooproject hello entity toohello Email value.
    EntityResolver<String> emailResolver = new EntityResolver<String>() {
        @Override
        public String resolve(String PartitionKey, String RowKey, Date timeStamp, HashMap<String, EntityProperty> properties, String etag) {
            return properties.get("Email").getValueAsString();
        }
    };

    // Loop through hello results, displaying hello Email values.
    for (String projectedString :
        cloudTable.execute(projectionQuery, emailResolver)) {
            System.out.println(projectedString);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-or-replace-an-entity"></a><span data-ttu-id="7e1dc-190">Procedura: inserire o sostituire un'entità</span><span class="sxs-lookup"><span data-stu-id="7e1dc-190">How to: Insert or Replace an entity</span></span>
<span data-ttu-id="7e1dc-191">Frequenza con cui una tabella tooa entità tooadd senza sapere se esiste già nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-191">Often you want tooadd an entity tooa table without knowing if it already exists in hello table.</span></span> <span data-ttu-id="7e1dc-192">Un'operazione di inserimento o sostituzione consente di toomake una singola richiesta cui inserirà entità hello se non esiste o sostituire uno esistente in caso di hello.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-192">An insert-or-replace operation allows you toomake a single request which will insert hello entity if it does not exist or replace hello existing one if it does.</span></span> <span data-ttu-id="7e1dc-193">Compilazione su esempi precedenti, hello codice seguente inserisce o sostituisce l'entità hello per "Walter arpa".</span><span class="sxs-lookup"><span data-stu-id="7e1dc-193">Building on prior examples, hello following code inserts or replaces hello entity for "Walter Harp".</span></span> <span data-ttu-id="7e1dc-194">Dopo aver creato una nuova entità, questo codice chiama hello **TableOperation.insertOrReplace** metodo.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-194">After creating a new entity, this code calls hello **TableOperation.insertOrReplace** method.</span></span> <span data-ttu-id="7e1dc-195">Questo codice chiama quindi **eseguire** su hello **CloudTable** dell'oggetto con l'istruzione insert nella tabella e hello hello o sostituire l'operazione di tabella come parametri hello.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-195">This code then calls **execute** on hello **CloudTable** object with hello table and hello insert or replace table operation as hello parameters.</span></span> <span data-ttu-id="7e1dc-196">solo una parte di un'entità, tooupdate hello **TableOperation.insertOrMerge** metodo può essere utilizzato invece.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-196">tooupdate only part of an entity, hello **TableOperation.insertOrMerge** method can be used instead.</span></span> <span data-ttu-id="7e1dc-197">Si noti che insert-o-sostituire non è supportato sull'emulatore di archiviazione locale di hello, pertanto questo codice viene eseguito solo quando si utilizza un account nel servizio tabelle hello.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-197">Note that insert-or-replace is not supported on hello local storage emulator, so this code runs only when using an account on hello table service.</span></span> <span data-ttu-id="7e1dc-198">Per altre informazioni sull'operazione di inserimento o sostituzione e l'operazione di inserimento o unione, vedere [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection] (Tabelle di Azure: Introduzione di Upsert e proiezione di query in tabelle di Azure).</span><span class="sxs-lookup"><span data-stu-id="7e1dc-198">You can learn more about insert-or-replace and insert-or-merge in this [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer5 = new CustomerEntity("Harp", "Walter");
    customer5.setEmail("Walter@contoso.com");
    customer5.setPhoneNumber("425-555-0106");

    // Create an operation tooadd hello new customer toohello people table.
    TableOperation insertCustomer5 = TableOperation.insertOrReplace(customer5);

    // Submit hello operation toohello table service.
    cloudTable.execute(insertCustomer5);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-an-entity"></a><span data-ttu-id="7e1dc-199">Procedura: eliminare un'entità</span><span class="sxs-lookup"><span data-stu-id="7e1dc-199">How to: Delete an entity</span></span>
<span data-ttu-id="7e1dc-200">È possibile eliminare facilmente un'entità dopo averla recuperata.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-200">You can easily delete an entity after you have retrieved it.</span></span> <span data-ttu-id="7e1dc-201">Una volta recuperato entità hello, chiamare **TableOperation.delete** con toodelete entità hello.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-201">Once hello entity is retrieved, call **TableOperation.delete** with hello entity toodelete.</span></span> <span data-ttu-id="7e1dc-202">Chiamare quindi **eseguire** su hello **CloudTable** oggetto.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-202">Then call **execute** on hello **CloudTable** object.</span></span> <span data-ttu-id="7e1dc-203">Hello seguente codice recupera ed elimina un'entità customer.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-203">hello following code retrieves and deletes a customer entity.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff = TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
    CustomerEntity entitySmithJeff =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Create an operation toodelete hello entity.
    TableOperation deleteSmithJeff = TableOperation.delete(entitySmithJeff);

    // Submit hello delete operation toohello table service.
    cloudTable.execute(deleteSmithJeff);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-table"></a><span data-ttu-id="7e1dc-204">Procedura: eliminare una tabella</span><span class="sxs-lookup"><span data-stu-id="7e1dc-204">How to: Delete a table</span></span>
<span data-ttu-id="7e1dc-205">Infine, hello codice seguente elimina una tabella da un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-205">Finally, hello following code deletes a table from a storage account.</span></span> <span data-ttu-id="7e1dc-206">Una tabella che è stata eliminata, sarà disponibile toobe ricreati per un periodo di tempo dopo l'eliminazione di hello, in genere meno di 40 secondi.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-206">A table which has been deleted will be unavailable toobe recreated for a period of time following hello deletion, usually less than forty seconds.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Delete hello table and all its data if it exists.
    CloudTable cloudTable = tableClient.getTableReference("people");
    cloudTable.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```
[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="next-steps"></a><span data-ttu-id="7e1dc-207">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7e1dc-207">Next steps</span></span>

* <span data-ttu-id="7e1dc-208">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) è un'app autonoma, disponibile da Microsoft che consente di toowork visivamente i dati di archiviazione di Azure in Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="7e1dc-208">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="7e1dc-209">[Azure Storage SDK per Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="7e1dc-209">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="7e1dc-210">[Azure Storage Client SDK riferimento][Azure Storage Client SDK riferimento]</span><span class="sxs-lookup"><span data-stu-id="7e1dc-210">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="7e1dc-211">[API REST di Archiviazione di Azure][Azure Storage REST API]</span><span class="sxs-lookup"><span data-stu-id="7e1dc-211">[Azure Storage REST API][Azure Storage REST API]</span></span>
* <span data-ttu-id="7e1dc-212">[Blog del team di Archiviazione di Azure][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="7e1dc-212">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

<span data-ttu-id="7e1dc-213">Per altre informazioni, vedere [Azure for Java developers](/java/azure) (Azure per sviluppatori Java).</span><span class="sxs-lookup"><span data-stu-id="7e1dc-213">For more information, visit [Azure for Java developers](/java/azure).</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[Azure Storage Client SDK riferimento]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Tables: Introducing Upsert and Query Projection]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx
