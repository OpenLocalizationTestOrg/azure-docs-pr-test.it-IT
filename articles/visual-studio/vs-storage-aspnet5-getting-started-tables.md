---
title: aaaHow tooget avviato con Visual Studio e l'archiviazione tabelle di servizi connessi (ASP.NET Core) | Documenti Microsoft
description: "La modalità di avvio tooget con l'archiviazione tabelle di Azure in un progetto ASP.NET Core in Visual Studio dopo la connessione di account di archiviazione tooa utilizzando Visual Studio di servizi connessi"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: c3c451d1-71ff-4222-a348-c41c98a02b85
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: e3eb3f3e65456108dd3cde7e3e470f98ba456e35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-started-with-azure-table-storage-and-visual-studio-connected-services"></a>La modalità di avvio con l'archiviazione tabelle di Azure e Visual Studio tooget servizi connessi
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a>Panoramica
Questo articolo viene descritto come ottenere avviato utilizzando tabelle di Azure in Visual Studio dopo aver creato o riferimento a un account di archiviazione di Azure in un progetto ASP.NET Core tramite archiviazione hello Visual Studio **aggiungere servizi connessi** finestra di dialogo.

servizio di archiviazione tabelle Azure Hello consente toostore grandi quantità di dati strutturati. servizio Hello è un archivio dati NoSQL che accetta chiamate autenticate dall'interno ed esterno hello cloud di Azure. Le tabelle di Azure sono ideali per l'archiviazione di dati strutturati non relazionali.

Hello **aggiungere servizi connessi** operazione installa hello appropriato NuGet pacchetti tooaccess archiviazione di Azure nel progetto e aggiunge la stringa di connessione hello per hello dell'account di archiviazione tooyour i file di configurazione di progetto.

Per ulteriori informazioni generali sull'utilizzo dell'archiviazione tabelle di Azure, vedere [Introduzione all'archiviazione tabelle di Azure con .NET](../storage/storage-dotnet-how-to-use-tables.md).

tooget avviato, è necessario innanzitutto toocreate una tabella nell'account di archiviazione. Vi mostreremo come tabella di toocreate di Azure nel codice. È inoltre mostreremo come tabella di base tooperform e operazioni di entità, ad esempio aggiunta, modifica, lettura e la lettura della tabella entità. Hello esempi sono scritti in C\# del codice e utilizzare hello Azure Storage Client Library per .NET.

**Nota** -alcune delle API che eseguono chiamate archiviazione tooAzure in ASP.NET Core hello sono asincrone. Per ulteriori informazioni, vedere [Programmazione asincrona con Async e Await](http://msdn.microsoft.com/library/hh191443.aspx) . codice Hello riportato di seguito si presuppone che vengono utilizzati i metodi di programmazione asincrono.

## <a name="access-tables-in-code"></a>Accesso alle tabelle nel codice
tooaccess nei progetti ASP.NET Core, è necessario che le tabelle hello tooinclude i seguenti file di origine c# tooany gli elementi che accedere all'archiviazione tabelle di Azure.

1. Verificare che le dichiarazioni dello spazio dei nomi hello all'inizio di hello del file hello c# includono queste **utilizzando** istruzioni.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. Ottenere un oggetto **CloudStorageAccount** che rappresenta le informazioni sull'account di archiviazione. Hello utilizzare seguente tooget codice hello la stringa di connessione di archiviazione e informazioni sull'account di archiviazione dalla configurazione del servizio Azure hello.
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
            CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
   
    **Nota** -utilizzare tutti hello sopra codice codice hello in hello seguendo gli esempi.
3. Ottenere un **CloudTableClient** tooreference hello tabella oggetti nell'account di archiviazione di oggetti.  
   
        // Create hello table client.
        CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. Ottenere un **CloudTable** fanno riferimento a entità e oggetto tooreference una tabella specifica.
   
        // Get a reference tooa table named "peopleTable"
        CloudTable table = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a>Creazione di una tabella in codice
hello toocreate tabelle di Azure, è sufficiente aggiungere una chiamata troppo**CreateIfNotExistsAsync()**.

    // Create hello CloudTable if it does not exist
    await table.CreateIfNotExistsAsync();

## <a name="add-an-entity-tooa-table"></a>Aggiungere una tabella tooa entità
tooadd una tabella tooa entità si crea una classe che definisce le proprietà di hello dell'entità. il codice seguente Hello definisce una classe di entità denominata **CustomerEntity** che utilizza hello nome del cliente come chiave di riga hello e il cognome come chiave di partizione hello.

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

Le operazioni di tabella che include le entità vengono eseguite utilizzando hello **CloudTable** dell'oggetto è stato creato in precedenza in "Tabelle di Access in codice". Hello **TableOperation** oggetto rappresenta hello toobe di operazione eseguita. Hello seguente esempio di codice viene illustrato come toocreate un **CloudTable** oggetto e un **CustomerEntity** oggetto. operazione di hello tooprepare, un **TableOperation** viene creata l'entità customer di tooinsert hello in tabella hello. Infine, l'operazione di hello viene eseguita chiamando CloudTable.ExecuteAsync.

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create hello TableOperation that inserts hello customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute hello insert operation.
    await peopleTable.ExecuteAsync(insertOperation);

## <a name="insert-a-batch-of-entities"></a>Inserire un batch di entità
È possibile inserire più entità in una tabella in una singola operazione di scrittura. Crea due oggetti entità ("Jeff Smith" e "Cavaglieri Federico") Hello esempio di codice seguente, li aggiunge tooa **TableBatchOperation** oggetto utilizzando hello **inserire** (metodo), quindi avvia hello operazione da la chiamata CloudTable.ExecuteBatchAsync.

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

## <a name="get-all-of-hello-entities-in-a-partition"></a>Ottenere tutte le entità hello in una partizione
tooquery una tabella per tutte le entità hello in una partizione, utilizzare un **TableQuery** oggetto. Hello esempio di codice seguente specifica un filtro per le entità in cui la chiave di partizione hello 'Smith'. In questo esempio visualizza i campi di ogni entità nella console di toohello risultati query hello hello.

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

## <a name="get-a-single-entity"></a>Ottenere una singola entità
È possibile scrivere un tooget query un'entità singola e specifica. codice Hello seguente viene utilizzato un **TableOperation** toospecify un cliente denominata 'Ben Smith' dell'oggetto. Questo metodo restituisce una sola entità, anziché una raccolta e hello ha restituito il valore in **TableResult.Result** è un **CustomerEntity** oggetto. Specifica le chiavi di partizione e di riga in una query è tooretrieve modo più veloce di hello una singola entità da hello **tabella** servizio.

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print hello phone number of hello result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("hello phone number could not be retrieved.");

## <a name="delete-an-entity"></a>Eliminare un'entità
È possibile eliminare un'entità dopo averla individuata. Hello codice riportato di seguito per un'entità customer denominata "Ben Smith" e se viene trovata, questo viene eliminato.

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

## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

