---
title: aaaGet avviato con Visual Studio e l'archiviazione tabelle di servizi connessi (servizi cloud) | Documenti Microsoft
description: "La modalità di avvio tooget utilizzando l'archiviazione tabelle di Azure in un progetto di servizio cloud in Visual Studio dopo la connessione di account di archiviazione tooa utilizzando Visual Studio di servizi connessi"
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
ms.openlocfilehash: 36da6ed4a12a3595e7234482e3040ecee8c33b8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-table-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="be2ab-103">Introduzione all’archiviazione di tabella di Azure e ai servizi connessi di Visual Studio (progetti servizi cloud)</span><span class="sxs-lookup"><span data-stu-id="be2ab-103">Getting started with Azure table storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="be2ab-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="be2ab-104">Overview</span></span>
<span data-ttu-id="be2ab-105">Questo articolo descrive la modalità di avvio con l'archiviazione tabelle di Azure in Visual Studio dopo aver creato o a cui fa riferimento a un account di archiviazione di Azure in un progetto di servizi cloud con Visual Studio hello tooget **aggiungere servizi connessi** finestra di dialogo .</span><span class="sxs-lookup"><span data-stu-id="be2ab-105">This article describes how tooget started using Azure table storage in Visual Studio after you have created or referenced an Azure storage account in a cloud services project by using hello Visual Studio **Add Connected Services** dialog.</span></span> <span data-ttu-id="be2ab-106">Hello **aggiungere servizi connessi** operazione installa hello appropriato NuGet pacchetti tooaccess archiviazione di Azure nel progetto e aggiunge la stringa di connessione hello per hello dell'account di archiviazione tooyour i file di configurazione di progetto.</span><span class="sxs-lookup"><span data-stu-id="be2ab-106">hello **Add Connected Services** operation installs hello appropriate NuGet packages tooaccess Azure storage in your project and adds hello connection string for hello storage account tooyour project configuration files.</span></span>

<span data-ttu-id="be2ab-107">servizio di archiviazione tabelle Azure Hello consente toostore grandi quantità di dati strutturati.</span><span class="sxs-lookup"><span data-stu-id="be2ab-107">hello Azure Table storage service enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="be2ab-108">servizio Hello è un archivio dati NoSQL che accetta chiamate autenticate dall'interno ed esterno hello cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="be2ab-108">hello service is a NoSQL datastore that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="be2ab-109">Le tabelle di Azure sono ideali per l'archiviazione di dati strutturati non relazionali.</span><span class="sxs-lookup"><span data-stu-id="be2ab-109">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="be2ab-110">tooget avviato, è necessario innanzitutto toocreate una tabella nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="be2ab-110">tooget started, you first need toocreate a table in your storage account.</span></span> <span data-ttu-id="be2ab-111">Vi mostreremo come toocreate di Azure table nel codice e anche come tabella di base tooperform e operazioni di entità, ad esempio aggiunta, modifica, lettura e la lettura della tabella entità.</span><span class="sxs-lookup"><span data-stu-id="be2ab-111">We'll show you how toocreate an Azure table in code, and also how tooperform basic table and entity operations, such as adding, modifying, reading and reading table entities.</span></span> <span data-ttu-id="be2ab-112">Hello esempi sono scritti in C\# del codice e utilizzare hello [libreria client di archiviazione di Microsoft Azure per .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="be2ab-112">hello samples are written in C\# code and use hello [Microsoft Azure Storage client library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="be2ab-113">**Nota:** alcune delle API che eseguono chiamate archiviazione tooAzure hello sono asincrone.</span><span class="sxs-lookup"><span data-stu-id="be2ab-113">**NOTE:** Some of hello APIs that perform calls out tooAzure storage are asynchronous.</span></span> <span data-ttu-id="be2ab-114">Per ulteriori informazioni, vedere [Programmazione asincrona con Async e Await](http://msdn.microsoft.com/library/hh191443.aspx) .</span><span class="sxs-lookup"><span data-stu-id="be2ab-114">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="be2ab-115">codice Hello riportato di seguito si presuppone che vengono utilizzati i metodi di programmazione asincrono.</span><span class="sxs-lookup"><span data-stu-id="be2ab-115">hello code below assumes async programming methods are being used.</span></span>

* <span data-ttu-id="be2ab-116">Per altre informazioni sulla modifica delle tabelle a livello di codice, vedere [Introduzione all'archiviazione tabelle di Azure con .NET](../storage/storage-dotnet-how-to-use-tables.md) .</span><span class="sxs-lookup"><span data-stu-id="be2ab-116">See [Get started with Azure Table storage using .NET](../storage/storage-dotnet-how-to-use-tables.md) for more information on programmatically manipulating tables.</span></span>
* <span data-ttu-id="be2ab-117">Vedere la [documentazione di archiviazione](https://azure.microsoft.com/documentation/services/storage/) per informazioni generali sull'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="be2ab-117">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="be2ab-118">Vedere la [documentazione dei servizi Cloud](https://azure.microsoft.com/documentation/services/cloud-services/) per informazioni generali sui servizi cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="be2ab-118">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="be2ab-119">Vedere [ASP.NET](http://www.asp.net) per ulteriori informazioni sulle applicazioni di programmazione di ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="be2ab-119">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

## <a name="access-tables-in-code"></a><span data-ttu-id="be2ab-120">Accesso alle tabelle nel codice</span><span class="sxs-lookup"><span data-stu-id="be2ab-120">Access tables in code</span></span>
<span data-ttu-id="be2ab-121">tooaccess nei progetti del servizio cloud, è necessario che le tabelle hello tooinclude i seguenti file di origine c# tooany gli elementi che accedere all'archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="be2ab-121">tooaccess tables in cloud service projects, you need tooinclude hello following items tooany C# source files that access Azure table storage.</span></span>

1. <span data-ttu-id="be2ab-122">Verificare che le dichiarazioni dello spazio dei nomi hello all'inizio di hello del file hello c# includono queste **utilizzando** istruzioni.</span><span class="sxs-lookup"><span data-stu-id="be2ab-122">Make sure hello namespace declarations at hello top of hello C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="be2ab-123">Ottenere un oggetto **CloudStorageAccount** che rappresenta le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="be2ab-123">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="be2ab-124">Utilizzare hello seguendo codice tooget hello archiviazione stringa e l'archiviazione account informazioni di connessione dalla configurazione del servizio Azure hello.</span><span class="sxs-lookup"><span data-stu-id="be2ab-124">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage account name>
         _AzureStorageConnectionString"));
   > [!NOTE]
   > <span data-ttu-id="be2ab-125">Utilizzare tutti hello sopra codice codice hello in hello seguendo gli esempi.</span><span class="sxs-lookup"><span data-stu-id="be2ab-125">Use all of hello above code in front of hello code in hello following samples.</span></span>
   > 
   > 
3. <span data-ttu-id="be2ab-126">Ottenere un **CloudTableClient** tooreference hello tabella oggetti nell'account di archiviazione di oggetti.</span><span class="sxs-lookup"><span data-stu-id="be2ab-126">Get a **CloudTableClient** object tooreference hello table objects in your storage account.</span></span>
   
         // Create hello table client.
         CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. <span data-ttu-id="be2ab-127">Ottenere un **CloudTable** fanno riferimento a entità e oggetto tooreference una tabella specifica.</span><span class="sxs-lookup"><span data-stu-id="be2ab-127">Get a **CloudTable** reference object tooreference a specific table and entities.</span></span>
   
        // Get a reference tooa table named "peopleTable".
        CloudTable peopleTable = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a><span data-ttu-id="be2ab-128">Creazione di una tabella in codice</span><span class="sxs-lookup"><span data-stu-id="be2ab-128">Create a table in code</span></span>
<span data-ttu-id="be2ab-129">hello toocreate tabelle di Azure, è sufficiente aggiungere una chiamata troppo**CreateIfNotExistsAsync** toohello dopo avere ottenuto un **CloudTable** come descritto nella sezione "Tabelle di Access in codice" hello dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="be2ab-129">toocreate hello Azure table, just add a call too**CreateIfNotExistsAsync** toohello after you get a **CloudTable** object as described in hello "Access tables in code" section.</span></span>

    // Create hello CloudTable if it does not exist.
    await peopleTable.CreateIfNotExistsAsync();

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="be2ab-130">Aggiungere una tabella tooa entità</span><span class="sxs-lookup"><span data-stu-id="be2ab-130">Add an entity tooa table</span></span>
<span data-ttu-id="be2ab-131">tooadd tabella tooa un'entità, creare una classe che definisce le proprietà di hello dell'entità.</span><span class="sxs-lookup"><span data-stu-id="be2ab-131">tooadd an entity tooa table, create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="be2ab-132">il codice seguente Hello definisce una classe di entità denominata **CustomerEntity** che utilizza hello nome del cliente come chiave di riga hello e il cognome di hello come chiave di partizione hello.</span><span class="sxs-lookup"><span data-stu-id="be2ab-132">hello following code defines an entity class called **CustomerEntity** that uses hello customer's first name as hello row key and hello last name as hello partition key.</span></span>

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

<span data-ttu-id="be2ab-133">Le operazioni di tabella che include le entità vengono eseguite utilizzando hello **CloudTable** oggetto creato in precedenza in "Tabelle di Access in codice".</span><span class="sxs-lookup"><span data-stu-id="be2ab-133">Table operations involving entities are done using hello **CloudTable** object that you created earlier in "Access tables in code."</span></span> <span data-ttu-id="be2ab-134">Hello **TableOperation** oggetto rappresenta hello toobe di operazione eseguita.</span><span class="sxs-lookup"><span data-stu-id="be2ab-134">hello **TableOperation** object represents hello operation toobe done.</span></span> <span data-ttu-id="be2ab-135">Hello seguente esempio di codice viene illustrato come toocreate un **CloudTable** oggetto e un **CustomerEntity** oggetto.</span><span class="sxs-lookup"><span data-stu-id="be2ab-135">hello following code example shows how toocreate a **CloudTable** object and a **CustomerEntity** object.</span></span> <span data-ttu-id="be2ab-136">operazione di hello tooprepare, un **TableOperation** viene creata l'entità customer di tooinsert hello in tabella hello.</span><span class="sxs-lookup"><span data-stu-id="be2ab-136">tooprepare hello operation, a **TableOperation** is created tooinsert hello customer entity into hello table.</span></span> <span data-ttu-id="be2ab-137">Infine, operazione hello viene eseguito chiamando **CloudTable.ExecuteAsync**.</span><span class="sxs-lookup"><span data-stu-id="be2ab-137">Finally, hello operation is executed by calling **CloudTable.ExecuteAsync**.</span></span>

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create hello TableOperation that inserts hello customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute hello insert operation.
    await peopleTable.ExecuteAsync(insertOperation);


## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="be2ab-138">Inserire un batch di entità</span><span class="sxs-lookup"><span data-stu-id="be2ab-138">Insert a batch of entities</span></span>
<span data-ttu-id="be2ab-139">È possibile inserire più entità in una tabella in una singola operazione di scrittura.</span><span class="sxs-lookup"><span data-stu-id="be2ab-139">You can insert multiple entities into a table in a single write operation.</span></span> <span data-ttu-id="be2ab-140">Crea due oggetti entità ("Jeff Smith" e "Ben Smith") Hello esempio di codice seguente, li aggiunge tooa **TableBatchOperation** oggetto utilizzando hello metodo Insert e quindi avvia hello operazione chiamando  **CloudTable.ExecuteBatchAsync**.</span><span class="sxs-lookup"><span data-stu-id="be2ab-140">hello following code example creates two entity objects ("Jeff Smith" and "Ben Smith"), adds them tooa **TableBatchOperation** object using hello Insert method, and then starts hello operation by calling **CloudTable.ExecuteBatchAsync**.</span></span>

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

## <a name="get-all-of-hello-entities-in-a-partition"></a><span data-ttu-id="be2ab-141">Ottenere tutte le entità hello in una partizione</span><span class="sxs-lookup"><span data-stu-id="be2ab-141">Get all of hello entities in a partition</span></span>
<span data-ttu-id="be2ab-142">tooquery una tabella per tutte le entità hello in una partizione, utilizzare un **TableQuery** oggetto.</span><span class="sxs-lookup"><span data-stu-id="be2ab-142">tooquery a table for all of hello entities in a partition, use a **TableQuery** object.</span></span> <span data-ttu-id="be2ab-143">Hello esempio di codice seguente specifica un filtro per le entità in cui la chiave di partizione hello 'Smith'.</span><span class="sxs-lookup"><span data-stu-id="be2ab-143">hello following code example specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="be2ab-144">In questo esempio visualizza i campi di ogni entità nella console di toohello risultati query hello hello.</span><span class="sxs-lookup"><span data-stu-id="be2ab-144">This example prints hello fields of each entity in hello query results toohello console.</span></span>

    // Construct hello query operation for all customer entities where PartitionKey="Smith".
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

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

    return View();


## <a name="get-a-single-entity"></a><span data-ttu-id="be2ab-145">Ottenere una singola entità</span><span class="sxs-lookup"><span data-stu-id="be2ab-145">Get a single entity</span></span>
<span data-ttu-id="be2ab-146">È possibile scrivere un tooget query un'entità singola e specifica.</span><span class="sxs-lookup"><span data-stu-id="be2ab-146">You can write a query tooget a single, specific entity.</span></span> <span data-ttu-id="be2ab-147">codice Hello seguente viene utilizzato un **TableOperation** toospecify un cliente denominata 'Ben Smith' dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="be2ab-147">hello following code uses a **TableOperation** object toospecify a customer named 'Ben Smith'.</span></span> <span data-ttu-id="be2ab-148">Questo metodo restituisce una sola entità, anziché una raccolta e hello ha restituito il valore in **TableResult.Result** è un **CustomerEntity** oggetto.</span><span class="sxs-lookup"><span data-stu-id="be2ab-148">This method returns just one entity, rather than a collection, and hello returned value in **TableResult.Result** is a **CustomerEntity** object.</span></span> <span data-ttu-id="be2ab-149">Specifica le chiavi di partizione e di riga in una query è tooretrieve modo più veloce di hello una singola entità da hello **tabella** servizio.</span><span class="sxs-lookup"><span data-stu-id="be2ab-149">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello **Table** service.</span></span>

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print hello phone number of hello result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("hello phone number could not be retrieved.");

## <a name="delete-an-entity"></a><span data-ttu-id="be2ab-150">Eliminare un'entità</span><span class="sxs-lookup"><span data-stu-id="be2ab-150">Delete an entity</span></span>
<span data-ttu-id="be2ab-151">È possibile eliminare un'entità dopo averla individuata.</span><span class="sxs-lookup"><span data-stu-id="be2ab-151">You can delete an entity after you find it.</span></span> <span data-ttu-id="be2ab-152">Hello codice riportato di seguito per un'entità customer denominata "Ben Smith" e, se viene trovata, questo viene eliminato.</span><span class="sxs-lookup"><span data-stu-id="be2ab-152">hello following code looks for a customer entity named "Ben Smith", and if it finds it, it deletes it.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="be2ab-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="be2ab-153">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

