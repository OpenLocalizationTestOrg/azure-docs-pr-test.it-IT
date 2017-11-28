---
title: aaaHow tooget avviato con Visual Studio e l'archiviazione tabelle di servizi connessi (ASP.NET Core) | Documenti Microsoft
description: "La modalità di avvio tooget con l'archiviazione tabelle di Azure in un progetto ASP.NET Core in Visual Studio dopo la connessione di account di archiviazione tooa utilizzando Visual Studio di servizi connessi"
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
ms.openlocfilehash: 6a8fb6aa085d78a087fcd14adbc765a0d59e0308
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-started-with-azure-table-storage-and-visual-studio-connected-services"></a><span data-ttu-id="9577a-103">La modalità di avvio con l'archiviazione tabelle di Azure e Visual Studio tooget servizi connessi</span><span class="sxs-lookup"><span data-stu-id="9577a-103">How tooget started with Azure Table storage and Visual Studio connected services</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="9577a-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="9577a-104">Overview</span></span>
<span data-ttu-id="9577a-105">Questo articolo viene descritto come ottenere avviato utilizzando tabelle di Azure in Visual Studio dopo aver creato o riferimento a un account di archiviazione di Azure in un progetto ASP.NET Core tramite archiviazione hello Visual Studio **aggiungere servizi connessi** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="9577a-105">This article describes how get started using Azure Table storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using hello Visual Studio **Add Connected Services** dialog.</span></span>

<span data-ttu-id="9577a-106">servizio di archiviazione tabelle Azure Hello consente toostore grandi quantità di dati strutturati.</span><span class="sxs-lookup"><span data-stu-id="9577a-106">hello Azure Table storage service enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="9577a-107">servizio Hello è un archivio dati NoSQL che accetta chiamate autenticate dall'interno ed esterno hello cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="9577a-107">hello service is a NoSQL data store that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="9577a-108">Le tabelle di Azure sono ideali per l'archiviazione di dati strutturati non relazionali.</span><span class="sxs-lookup"><span data-stu-id="9577a-108">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="9577a-109">Hello **aggiungere servizi connessi** operazione installa hello appropriato NuGet pacchetti tooaccess archiviazione di Azure nel progetto e aggiunge la stringa di connessione hello per hello dell'account di archiviazione tooyour i file di configurazione di progetto.</span><span class="sxs-lookup"><span data-stu-id="9577a-109">hello **Add Connected Services** operation installs hello appropriate NuGet packages tooaccess Azure storage in your project and adds hello connection string for hello storage account tooyour project configuration files.</span></span>

<span data-ttu-id="9577a-110">Per ulteriori informazioni generali sull'utilizzo dell'archiviazione tabelle di Azure, vedere [Introduzione all'archiviazione tabelle di Azure con .NET](storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="9577a-110">For more general information about using Azure Table storage, see [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md).</span></span>

<span data-ttu-id="9577a-111">tooget avviato, è necessario innanzitutto toocreate una tabella nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="9577a-111">tooget started, you first need toocreate a table in your storage account.</span></span> <span data-ttu-id="9577a-112">Vi mostreremo come tabella di toocreate di Azure nel codice.</span><span class="sxs-lookup"><span data-stu-id="9577a-112">We'll show you how toocreate an Azure table in code.</span></span> <span data-ttu-id="9577a-113">È inoltre mostreremo come tabella di base tooperform e operazioni di entità, ad esempio aggiunta, modifica, lettura e la lettura della tabella entità.</span><span class="sxs-lookup"><span data-stu-id="9577a-113">We'll also show you how tooperform basic table and entity operations, such as adding, modifying, reading and reading table entities.</span></span> <span data-ttu-id="9577a-114">Hello esempi sono scritti in C\# del codice e utilizzare hello Azure Storage Client Library per .NET.</span><span class="sxs-lookup"><span data-stu-id="9577a-114">hello samples are written in C\# code and use hello Azure Storage Client Library for .NET.</span></span>

<span data-ttu-id="9577a-115">**Nota** -alcune delle API che eseguono chiamate archiviazione tooAzure in ASP.NET Core hello sono asincrone.</span><span class="sxs-lookup"><span data-stu-id="9577a-115">**NOTE** - Some of hello APIs that perform calls out tooAzure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="9577a-116">Per ulteriori informazioni, vedere [Programmazione asincrona con Async e Await](http://msdn.microsoft.com/library/hh191443.aspx) .</span><span class="sxs-lookup"><span data-stu-id="9577a-116">See [Asynchronous Programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="9577a-117">codice Hello riportato di seguito si presuppone che vengono utilizzati i metodi di programmazione asincrono.</span><span class="sxs-lookup"><span data-stu-id="9577a-117">hello code below assumes Async programming methods are being used.</span></span>

## <a name="access-tables-in-code"></a><span data-ttu-id="9577a-118">Accesso alle tabelle nel codice</span><span class="sxs-lookup"><span data-stu-id="9577a-118">Access tables in code</span></span>
<span data-ttu-id="9577a-119">tooaccess nei progetti ASP.NET Core, è necessario che le tabelle hello tooinclude i seguenti file di origine c# tooany gli elementi che accedere all'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="9577a-119">tooaccess tables in ASP.NET Core projects, you need tooinclude hello following items tooany C# source files that access Azure table storage.</span></span>

1. <span data-ttu-id="9577a-120">Verificare che le dichiarazioni dello spazio dei nomi hello all'inizio di hello del file hello c# includono queste **utilizzando** istruzioni.</span><span class="sxs-lookup"><span data-stu-id="9577a-120">Make sure hello namespace declarations at hello top of hello C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="9577a-121">Ottenere un oggetto **CloudStorageAccount** che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="9577a-121">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="9577a-122">Hello utilizzare seguente tooget codice hello la stringa di connessione di archiviazione e informazioni sull'account di archiviazione dalla configurazione del servizio Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9577a-122">Use hello following code tooget hello your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
            CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
   
    <span data-ttu-id="9577a-123">**Nota** -utilizzare tutti hello sopra codice codice hello in hello seguendo gli esempi.</span><span class="sxs-lookup"><span data-stu-id="9577a-123">**NOTE** - Use all of hello above code in front of hello code in hello following samples.</span></span>
3. <span data-ttu-id="9577a-124">Ottenere un **CloudTableClient** tooreference hello tabella oggetti nell'account di archiviazione di oggetti.</span><span class="sxs-lookup"><span data-stu-id="9577a-124">Get a **CloudTableClient** object tooreference hello table objects in your storage account.</span></span>  
   
        // Create hello table client.
        CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. <span data-ttu-id="9577a-125">Ottenere un **CloudTable** fanno riferimento a entità e oggetto tooreference una tabella specifica.</span><span class="sxs-lookup"><span data-stu-id="9577a-125">Get a **CloudTable** reference object tooreference a specific table and entities.</span></span>
   
        // Get a reference tooa table named "peopleTable"
        CloudTable table = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a><span data-ttu-id="9577a-126">Creazione di una tabella in codice</span><span class="sxs-lookup"><span data-stu-id="9577a-126">Create a table in code</span></span>
<span data-ttu-id="9577a-127">hello toocreate tabelle di Azure, è sufficiente aggiungere una chiamata troppo**CreateIfNotExistsAsync()**.</span><span class="sxs-lookup"><span data-stu-id="9577a-127">toocreate hello Azure table, just add a call too**CreateIfNotExistsAsync()**.</span></span>

    // Create hello CloudTable if it does not exist
    await table.CreateIfNotExistsAsync();

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="9577a-128">Aggiungere una tabella tooa entità</span><span class="sxs-lookup"><span data-stu-id="9577a-128">Add an entity tooa table</span></span>
<span data-ttu-id="9577a-129">tooadd una tabella tooa entità si crea una classe che definisce le proprietà di hello dell'entità.</span><span class="sxs-lookup"><span data-stu-id="9577a-129">tooadd an entity tooa table you create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="9577a-130">il codice seguente Hello definisce una classe di entità denominata **CustomerEntity** che utilizza hello nome del cliente come chiave di riga hello e il cognome come chiave di partizione hello.</span><span class="sxs-lookup"><span data-stu-id="9577a-130">hello following code defines an entity class called **CustomerEntity** that uses hello customer's first name as hello row key and last name as hello partition key.</span></span>

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

<span data-ttu-id="9577a-131">Le operazioni di tabella che include le entità vengono eseguite utilizzando hello **CloudTable** dell'oggetto è stato creato in precedenza in "Tabelle di Access in codice".</span><span class="sxs-lookup"><span data-stu-id="9577a-131">Table operations involving entities are done using hello **CloudTable** object you created earlier in "Access tables in code."</span></span> <span data-ttu-id="9577a-132">Hello **TableOperation** oggetto rappresenta hello toobe di operazione eseguita.</span><span class="sxs-lookup"><span data-stu-id="9577a-132">hello **TableOperation** object represents hello operation toobe done.</span></span> <span data-ttu-id="9577a-133">Hello seguente esempio di codice viene illustrato come toocreate un **CloudTable** oggetto e un **CustomerEntity** oggetto.</span><span class="sxs-lookup"><span data-stu-id="9577a-133">hello following code example shows how toocreate a **CloudTable** object and a **CustomerEntity** object.</span></span> <span data-ttu-id="9577a-134">operazione di hello tooprepare, un **TableOperation** viene creata l'entità customer di tooinsert hello in tabella hello.</span><span class="sxs-lookup"><span data-stu-id="9577a-134">tooprepare hello operation, a **TableOperation** is created tooinsert hello customer entity into hello table.</span></span> <span data-ttu-id="9577a-135">Infine, l'operazione di hello viene eseguita chiamando CloudTable.ExecuteAsync.</span><span class="sxs-lookup"><span data-stu-id="9577a-135">Finally, hello operation is executed by calling CloudTable.ExecuteAsync.</span></span>

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create hello TableOperation that inserts hello customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute hello insert operation.
    await peopleTable.ExecuteAsync(insertOperation);

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="9577a-136">Inserire un batch di entità</span><span class="sxs-lookup"><span data-stu-id="9577a-136">Insert a batch of entities</span></span>
<span data-ttu-id="9577a-137">È possibile inserire più entità in una tabella in una singola operazione di scrittura.</span><span class="sxs-lookup"><span data-stu-id="9577a-137">You can insert multiple entities into a table in a single write operation.</span></span> <span data-ttu-id="9577a-138">Crea due oggetti entità ("Jeff Smith" e "Cavaglieri Federico") Hello esempio di codice seguente, li aggiunge tooa **TableBatchOperation** oggetto utilizzando hello **inserire** (metodo), quindi avvia hello operazione da la chiamata CloudTable.ExecuteBatchAsync.</span><span class="sxs-lookup"><span data-stu-id="9577a-138">hello following code example creates two entity objects ("Jeff Smith" and "Ben Smith"), adds them tooa **TableBatchOperation** object using hello **Insert** method, and then starts hello operation by calling CloudTable.ExecuteBatchAsync.</span></span>

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
    await peopleTable.ExecuteBatchAsync(batchOperation);

## <a name="get-all-of-hello-entities-in-a-partition"></a><span data-ttu-id="9577a-139">Ottenere tutte le entità hello in una partizione</span><span class="sxs-lookup"><span data-stu-id="9577a-139">Get all of hello entities in a partition</span></span>
<span data-ttu-id="9577a-140">tooquery una tabella per tutte le entità hello in una partizione, utilizzare un **TableQuery** oggetto.</span><span class="sxs-lookup"><span data-stu-id="9577a-140">tooquery a table for all of hello entities in a partition, use a **TableQuery** object.</span></span> <span data-ttu-id="9577a-141">Hello esempio di codice seguente specifica un filtro per le entità in cui la chiave di partizione hello 'Smith'.</span><span class="sxs-lookup"><span data-stu-id="9577a-141">hello following code example specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="9577a-142">In questo esempio visualizza i campi di ogni entità nella console di toohello risultati query hello hello.</span><span class="sxs-lookup"><span data-stu-id="9577a-142">This example prints hello fields of each entity in hello query results toohello console.</span></span>

    // Construct hello query operation for all customer entities where PartitionKey="Smith".
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>().Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

    // Print hello fields for each customer.
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

## <a name="get-a-single-entity"></a><span data-ttu-id="9577a-143">Ottenere una singola entità</span><span class="sxs-lookup"><span data-stu-id="9577a-143">Get a single entity</span></span>
<span data-ttu-id="9577a-144">È possibile scrivere un tooget query un'entità singola e specifica.</span><span class="sxs-lookup"><span data-stu-id="9577a-144">You can write a query tooget a single, specific entity.</span></span> <span data-ttu-id="9577a-145">codice Hello seguente viene utilizzato un **TableOperation** toospecify un cliente denominata 'Ben Smith' dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9577a-145">hello following code uses a **TableOperation** object toospecify a customer named 'Ben Smith'.</span></span> <span data-ttu-id="9577a-146">Questo metodo restituisce una sola entità, anziché una raccolta e hello ha restituito il valore in **TableResult.Result** è un **CustomerEntity** oggetto.</span><span class="sxs-lookup"><span data-stu-id="9577a-146">This method returns just one entity, rather than a collection, and hello returned value in **TableResult.Result** is a **CustomerEntity** object.</span></span> <span data-ttu-id="9577a-147">Specifica le chiavi di partizione e di riga in una query è tooretrieve modo più veloce di hello una singola entità da hello **tabella** servizio.</span><span class="sxs-lookup"><span data-stu-id="9577a-147">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello **Table** service.</span></span>

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print hello phone number of hello result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("hello phone number could not be retrieved.");

## <a name="delete-an-entity"></a><span data-ttu-id="9577a-148">Eliminare un'entità</span><span class="sxs-lookup"><span data-stu-id="9577a-148">Delete an entity</span></span>
<span data-ttu-id="9577a-149">È possibile eliminare un'entità dopo averla individuata.</span><span class="sxs-lookup"><span data-stu-id="9577a-149">You can delete an entity after you find it.</span></span> <span data-ttu-id="9577a-150">Hello codice riportato di seguito per un'entità customer denominata "Ben Smith" e se viene trovata, questo viene eliminato.</span><span class="sxs-lookup"><span data-stu-id="9577a-150">hello following code looks for a customer entity named "Ben Smith" and if it finds it, it deletes it.</span></span>

    // Create a retrieve operation that expects a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello operation.
    TableResult retrievedResult = peopleTable.Execute(retrieveOperation);

    // Assign hello result tooa CustomerEntity object.
    CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

    // Create hello Delete TableOperation and then execute it.
    if (deleteEntity != null)
    {
       TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

       // Execute hello operation.
       await peopleTable.ExecuteAsync(deleteOperation);

       Console.WriteLine("Entity deleted.");
    }

    else
       Console.WriteLine("Couldn't delete hello entity.");

## <a name="next-steps"></a><span data-ttu-id="9577a-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9577a-151">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

