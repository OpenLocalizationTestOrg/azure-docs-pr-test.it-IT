---
title: aaaHow toouse archiviazione tabelle da Java | Documenti Microsoft
description: Archiviare dati strutturati in un cloud di hello tramite l'archiviazione tabelle di Azure, un archivio dati NoSQL.
services: storage
documentationcenter: java
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 45145189-e67f-4ca6-b15d-43af7bfd3f97
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: f72cac3fc10cf0aef74780b84c515d93d715d787
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-java"></a>Come toouse archiviazione tabelle da Java
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Panoramica
Questa guida illustra come gli scenari comuni di tooperform utilizzando hello servizio di archiviazione tabelle di Azure. esempi di Hello sono scritti in Java e usano hello [Azure Storage SDK per Java][Azure Storage SDK for Java]. Hello scenari trattati includono **creazione**, **elenco**, e **eliminazione** tabelle, nonché **inserimento**,  **l'esecuzione di query**, **modifica**, e **eliminazione** entità in una tabella. Per ulteriori informazioni sulle tabelle, vedere hello [passaggi successivi](#Next-Steps) sezione.

Nota: per gli sviluppatori che usano il servizio di archiviazione di Azure in dispositivi Android, è disponibile un SDK specifico. Per ulteriori informazioni, vedere hello [Azure Storage SDK per Android][Azure Storage SDK for Android].

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a>Creare un'applicazione Java
In questa guida si utilizzeranno le funzionalità di archiviazione che possono essere eseguite in un'applicazione Java in locale o nel codice in esecuzione in un ruolo Web, in un ruolo di lavoro o in Azure.

toodo in tal caso, sarà necessario tooinstall hello Java Development Kit (JDK) e creare un account di archiviazione di Azure nella sottoscrizione di Azure. Dopo aver eseguito questa operazione, sarà necessario tooverify che il sistema di sviluppo soddisfi i requisiti minimi di hello e le dipendenze sono elencate in hello [Azure Storage SDK per Java] [ Azure Storage SDK for Java] repository in GitHub. Se il sistema soddisfi tali requisiti, è possibile seguire le istruzioni di hello per scaricare e installare le librerie di archiviazione di Azure hello for Java nel sistema da quel repository. Dopo aver completato queste attività, sarà in grado di toocreate un'applicazione Java che utilizza esempi hello in questo articolo.

## <a name="configure-your-application-tooaccess-table-storage"></a>Configurare l'archiviazione tabelle tooaccess di applicazione
Aggiungere hello dopo l'inizio di toohello di istruzioni di importazione del file di Java hello in cui si desidera tabelle di tooaccess le API di archiviazione di toouse Microsoft Azure:

```java
// Include hello following imports toouse table APIs
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.table.*;
import com.microsoft.azure.storage.table.TableQuery.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a>Impostare una stringa di connessione di archiviazione di Azure
Un client di archiviazione di Azure Usa un endpoint di toostore stringa di connessione archiviazione e le credenziali per l'accesso a servizi di gestione dati. Quando si esegue un'applicazione client, è necessario fornire una stringa di connessione di archiviazione hello in hello seguente formato, utilizzando nome hello dell'account di archiviazione e chiave di accesso primaria per l'account di archiviazione hello elencati in hello hello [il portale di Azure](https://portal.azure.com)per hello *AccountName* e *AccountKey* valori. In questo esempio viene illustrato come dichiarare una stringa di connessione di un campo statico toohold hello:

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

In un'applicazione in esecuzione all'interno di un ruolo in Microsoft Azure, questa stringa può essere archiviata nel file di configurazione del servizio hello *ServiceConfiguration. cscfg*ed è possibile accedervi con una chiamata toohello  **RoleEnvironment.getConfigurationSettings** metodo. Di seguito è riportato un esempio di recupero della stringa di connessione hello da un **impostazione** elemento denominato *StorageConnectionString* nel file di configurazione del servizio hello:

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

Hello negli esempi seguenti si presuppongono che si usa uno di questi due metodi tooget hello stringa di connessione.

## <a name="how-to-create-a-table"></a>Procedura: creare una tabella
Per ottenere oggetti di riferimento per tabelle ed entità, è possibile usare un oggetto **CloudTableClient**. Hello codice seguente viene creata una **CloudTableClient** dell'oggetto e lo usa toocreate un nuovo **CloudTable** oggetto che rappresenta una tabella denominata "persone". (Nota: esistono altri modi toocreate **CloudStorageAccount** oggetti; per ulteriori informazioni, vedere **CloudStorageAccount** in hello [Azure Storage Client SDK riferimento].)

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

## <a name="how-to-list-hello-tables"></a>Procedura: elencare le tabelle di hello
un elenco di tabelle, chiamata hello tooget **CloudTableClient.listTables()** metodo tooretrieve un elenco dei nomi di tabella iterabile.

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

## <a name="how-to-add-an-entity-tooa-table"></a>Procedura: aggiungere una tabella tooa entità
Eseguire il mapping di entità tooJava oggetti usando una classe personalizzata che implementa **TableEntity**. Per praticità, hello **TableServiceEntity** implementa **TableEntity** e utilizza le proprietà di toomap reflection metodi toogetter e set denominati per hello proprietà. tooadd tabella tooa un'entità, creare innanzitutto una classe che definisce le proprietà di hello dell'entità. Hello codice seguente definisce una classe di entità che utilizza nome hello del cliente come chiave di riga hello e last name come chiave di partizione hello. Insieme, di partizione e chiave di riga identificano entità hello nella tabella di hello. Entità con hello stessa chiave di partizione è possibile eseguire query più velocemente rispetto a quelle con le chiavi di partizione diverso.

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

Per le operazioni su tabella che interessano entità è necessario un oggetto **TableServiceContext** . Questo oggetto definisce hello toobe di operazione eseguita su un'entità che può essere eseguita con un **CloudTable** oggetto. esempio di codice Hello crea una nuova istanza di hello **CustomerEntity** classe con alcuni toobe dati cliente archiviati. Hello successiva chiama codice **TableOperation.insertOrReplace** toocreate un **TableOperation** tooinsert un'entità dell'oggetto in una tabella, e associa hello nuovi **CustomerEntity**con esso. Infine, il codice hello chiama hello **eseguire** metodo hello **CloudTable** oggetto specificando una tabella "persone" hello e hello nuovo **TableOperation**, che invia quindi un entità della richiesta toohello archiviazione servizio tooinsert hello nuovo cliente nella tabella "persone" hello, o sostituire entità hello se esiste già.

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

## <a name="how-to-insert-a-batch-of-entities"></a>Procedura: inserire un batch di entità
È possibile inserire un batch di servizio tabelle toohello di entità in un'unica operazione di scrittura. Hello codice seguente viene creata una **TableBatchOperation** dell'oggetto, quindi aggiunge tre tooit operazioni di inserimento. Ogni operazione di inserimento viene aggiunto per la creazione di un nuovo oggetto entità, impostarne i valori e chiamando quindi hello **inserire** metodo hello **TableBatchOperation** entità hello tooassociate con un nuovo oggetto operazione di inserimento. Quindi hello codice chiama **eseguire** su hello **CloudTable** oggetto specificando una tabella di "people" hello e hello **TableBatchOperation** oggetto, che invia il batch hello della tabella servizio di archiviazione toohello operazioni in una singola richiesta.

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

Toonote alcune operazioni per le operazioni batch:

* È possibile eseguire backup too100 insert, delete, merge, replace, insert o merge, inserire o sostituire operazioni in qualsiasi combinazione in un unico batch.
* Un'operazione batch può avere un'operazione di recupero, se è l'unica operazione di hello in batch hello.
* Tutte le entità in una singola operazione batch devono avere hello stessa chiave di partizione.
* Un'operazione batch è limitato tooa payload di dati di 4MB.

## <a name="how-to-retrieve-all-entities-in-a-partition"></a>Procedura: recuperare tutte le entità di una partizione
tooquery una tabella per le entità in una partizione, è possibile utilizzare un **TableQuery**. Chiamare **TableQuery.from** toocreate una query su una determinata tabella che restituisce un tipo di risultato specificato. Hello codice seguente specifica un filtro per le entità in cui la chiave di partizione hello 'Smith'. **TableQuery.generateFilterCondition** è un metodo helper toocreate filtri per le query. Chiamare **in** su hello riferimento restituito da hello **TableQuery.from** query toohello del metodo tooapply hello filtro. Quando viene eseguita la query hello con una chiamata troppo**eseguire** su hello **CloudTable** specificato, viene restituito un **iteratore** con hello **CustomerEntity**specificato tipo di risultato. È quindi possibile utilizzare hello **iteratore** restituiti in un per ottenere risultati hello tooconsume ogni ciclo. Questo codice visualizza i campi di ogni entità nella console di toohello risultati query hello hello.

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

## <a name="how-to-retrieve-a-range-of-entities-in-a-partition"></a>Procedura: recuperare un intervallo di entità in una partizione
Se non si desidera tooquery tutte le entità hello in una partizione, è possibile specificare un intervallo con gli operatori di confronto in un filtro. Hello seguente combina codice due filtri tooget tutte le entità nella partizione "Smith" in cui la chiave di riga hello (nome) inizia con una lettera di too'E' alfabeto hello. Vengono quindi i risultati di query hello. Se si utilizza hello entità toohello aggiunto tabella batch hello inserire sezione di questa Guida, solo due entità vengono restituite a questo momento (Ben e Denise Smith); Jeff Smith non è incluso.

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

## <a name="how-to-retrieve-a-single-entity"></a>Procedura: recuperare una singola entità
È possibile scrivere un tooretrieve query un'entità singola e specifica. codice Hello seguente chiama **TableOperation.retrieve** con partizione chiave e riga di parametri chiave toospecify hello cliente "Jeff Smith", anziché creare un **TableQuery** e l'utilizzo di hello toodo filtri Stessa cosa. Quando viene eseguita, hello recuperare operazione restituisce una sola entità, anziché una raccolta. Hello **getResultAsType** metodo esegue il cast di tipo di toohello hello risultato della destinazione di assegnazione hello, un **CustomerEntity** oggetto. Se questo tipo non è compatibile con il tipo di hello specificato per la query hello, verrà generata un'eccezione. Viene restituito un valore Null se per nessuna entità è disponibile una corrispondenza esatta di chiave di riga e chiave di partizione. Specifica le chiavi di partizione e di riga in una query è tooretrieve modo più veloce di hello una singola entità dal servizio tabelle hello.

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

## <a name="how-to-modify-an-entity"></a>Procedura: modificare un'entità
toomodify un'entità, recuperarlo dal servizio tabelle hello, rendere l'oggetto entità toohello di modifiche e salvare le modifiche di hello del servizio tabelle toohello indietro con un'operazione di sostituzione o unione. Hello codice seguente modifica il numero di telefono del cliente esistente. Anziché chiamare **TableOperation.insert** come abbiamo visto tooinsert, questo codice chiama **TableOperation.replace**. Hello **CloudTable.execute** chiamate del servizio tabelle hello e l'entità hello viene sostituita, a meno che un'altra applicazione sono stati modificati da nel tempo hello questa applicazione è stato recuperato. In questo caso, viene generata un'eccezione ed entità hello deve essere recuperato, modificato e salvato di nuovo. Questo schema di ripetizione dei tentativi che supporta la concorrenza ottimistica è comune in un sistema di sistema di archiviazione distribuita.

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

## <a name="how-to-query-a-subset-of-entity-properties"></a>Procedura: eseguire query su un subset di proprietà di entità
Una tabella di tooa query è possibile recuperare solo alcune proprietà di un'entità. Questa tecnica, denominata proiezione, consente di ridurre la larghezza di banda e di migliorare le prestazioni della query, in particolare per entità di grandi dimensioni. query nel seguente codice hello Hello utilizza hello **selezionare** metodo tooreturn solo hello indirizzi di posta elettronica di entità nella tabella hello. Hello risultati vengono proiettati in un insieme di **stringa** insieme hello un **EntityResolver**, quale does hello sulle entità hello hello server ha restituito una conversione del tipo. Per altre informazioni sulla proiezione, vedere [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection] (Tabelle di Azure: Introduzione di Upsert e proiezione di query in tabelle di Azure). Si noti che proiezione non è supportata sull'emulatore di archiviazione locale di hello, pertanto questo codice viene eseguito solo quando si utilizza un account nel servizio tabelle hello.

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

## <a name="how-to-insert-or-replace-an-entity"></a>Procedura: inserire o sostituire un'entità
Frequenza con cui una tabella tooa entità tooadd senza sapere se esiste già nella tabella hello. Un'operazione di inserimento o sostituzione consente di toomake una singola richiesta cui inserirà entità hello se non esiste o sostituire uno esistente in caso di hello. Compilazione su esempi precedenti, hello codice seguente inserisce o sostituisce l'entità hello per "Walter arpa". Dopo aver creato una nuova entità, questo codice chiama hello **TableOperation.insertOrReplace** metodo. Questo codice chiama quindi **eseguire** su hello **CloudTable** dell'oggetto con l'istruzione insert nella tabella e hello hello o sostituire l'operazione di tabella come parametri hello. solo una parte di un'entità, tooupdate hello **TableOperation.insertOrMerge** metodo può essere utilizzato invece. Si noti che insert-o-sostituire non è supportato sull'emulatore di archiviazione locale di hello, pertanto questo codice viene eseguito solo quando si utilizza un account nel servizio tabelle hello. Per altre informazioni sull'operazione di inserimento o sostituzione e l'operazione di inserimento o unione, vedere [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection] (Tabelle di Azure: Introduzione di Upsert e proiezione di query in tabelle di Azure).

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

## <a name="how-to-delete-an-entity"></a>Procedura: eliminare un'entità
È possibile eliminare facilmente un'entità dopo averla recuperata. Una volta recuperato entità hello, chiamare **TableOperation.delete** con toodelete entità hello. Chiamare quindi **eseguire** su hello **CloudTable** oggetto. Hello seguente codice recupera ed elimina un'entità customer.

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

## <a name="how-to-delete-a-table"></a>Procedura: eliminare una tabella
Infine, hello codice seguente elimina una tabella da un account di archiviazione. Una tabella che è stata eliminata, sarà disponibile toobe ricreati per un periodo di tempo dopo l'eliminazione di hello, in genere meno di 40 secondi.

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

## <a name="next-steps"></a>Passaggi successivi

* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) è un'app autonoma, disponibile da Microsoft che consente di toowork visivamente i dati di archiviazione di Azure in Windows, macOS e Linux.
* [Azure Storage SDK per Java][Azure Storage SDK for Java]
* [Azure Storage Client SDK riferimento][Azure Storage Client SDK riferimento]
* [API REST di Archiviazione di Azure][Azure Storage REST API]
* [Blog del team di Archiviazione di Azure][Azure Storage Team Blog]

Per ulteriori informazioni, vedere anche hello [Centro per sviluppatori Java](/develop/java/).

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[Azure Storage Client SDK riferimento]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Tables: Introducing Upsert and Query Projection]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx
