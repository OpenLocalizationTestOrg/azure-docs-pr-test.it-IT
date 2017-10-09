---
title: aaaHow toouse archiviazione tabella (C++) | Documenti Microsoft
description: Archiviare dati strutturati in un cloud di hello tramite l'archiviazione tabelle di Azure, un archivio dati NoSQL.
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jahogg
editor: tysonn
ms.assetid: f191f308-e4b2-4de9-85cb-551b82b1ea7c
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: mimig
ms.openlocfilehash: 8096fe531427ba4858f7f4cb7f664f941892d1c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-c"></a>Come toouse archiviazione tabelle da C++
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Panoramica
Questa guida illustra come gli scenari comuni di tooperform usando hello servizio di archiviazione tabelle di Azure. esempi di Hello sono scritti in C++ e utilizzare hello [libreria Client di archiviazione di Azure per C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md). Hello scenari trattati includono **creazione ed eliminazione di una tabella** e **utilizzo delle entità tabella**.

> [!NOTE]
> Le destinazioni di questa guida hello Azure Storage Client Library per la versione 1.0.0 di C++ e versioni successive. Hello consiglia versione libreria di Client di archiviazione 2.2.0, disponibile tramite [NuGet](http://www.nuget.org/packages/wastorage) o [GitHub](https://github.com/Azure/azure-storage-cpp/).
> 
> 

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a>Creazione di un’applicazione C++
In questa guida verranno usate le funzionalità di archiviazione che è possibile eseguire all'interno di un'applicazione C++. toodo in tal caso, sarà necessario tooinstall hello Azure Storage Client Library per C++ e creare un account di archiviazione di Azure nella sottoscrizione di Azure.  

tooinstall hello Azure Storage Client Library per C++, è possibile utilizzare hello dei seguenti metodi:

* **Linux:** seguire le istruzioni di hello fornite hello [Azure Storage Client Library per il file README C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) pagina.  
* **Windows:** in Visual Studio, fare clic su **Strumenti &gt; Gestione pacchetti NuGet &gt; console di Gestione pacchetti**. Comando che segue di tipo hello in hello [console di gestione pacchetti NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) e premere INVIO.  
  
     Install-Package knockoutjs

## <a name="configure-your-application-tooaccess-table-storage"></a>Configurare l'archiviazione tabelle di tooaccess applicazione
Aggiungere i seguenti hello includono hello C++ file in cui tabelle di tooaccess le API di archiviazione di Azure di toouse hello cima toohello istruzioni:  

```cpp
#include <was/storage_account.h>
#include <was/table.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a>Impostare una stringa di connessione di archiviazione di Azure
Un client di archiviazione di Azure Usa un endpoint di toostore stringa di connessione archiviazione e le credenziali per l'accesso a servizi di gestione dati. Quando si esegue un'applicazione client, è necessario fornire una stringa di connessione di archiviazione hello nel seguente formato hello. Utilizza il nome di hello dell'archiviazione hello e account di archiviazione chiave di accesso per account di archiviazione hello elencati in hello [portale Azure](https://portal.azure.com) per hello *AccountName* e *AccountKey* valori. Per informazioni sugli account di archiviazione e sulle chiavi di accesso, vedere [Informazioni sugli account di archiviazione di Azure](../storage/common/storage-create-storage-account.md). In questo esempio viene illustrato come dichiarare una stringa di connessione di un campo statico toohold hello:  

```cpp
// Define hello connection string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

tootest l'applicazione in computer basati su Windows locale, è possibile utilizzare hello Azure [emulatore di archiviazione](../storage/common/storage-use-emulator.md) che viene installato con hello [Azure SDK](https://azure.microsoft.com/downloads/). emulatore di archiviazione Hello è un'utilità che simula hello Azure Blob, coda e tabella servizi disponibili nel computer di sviluppo locale. Hello esempio seguente viene illustrato come è possibile dichiarare un emulatore di archiviazione locale di un campo statico toohold hello connessione stringa tooyour:  

```cpp
// Define hello connection string with Azure storage emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

toostart hello emulatore di archiviazione di Azure, fare clic su hello **avviare** o preme tasto di Windows hello. Iniziare a digitare **emulatore di archiviazione Azure**, quindi selezionare **emulatore di archiviazione di Microsoft Azure** elenco hello di applicazioni.  

Hello negli esempi seguenti si presuppongono che si usa uno di questi due metodi tooget hello stringa di connessione.  

## <a name="retrieve-your-connection-string"></a>Recuperare la stringa di connessione
È possibile utilizzare hello **cloud_storage_account** classe toorepresent le informazioni sull'account di archiviazione. tooretrieve informazioni dalla stringa di connessione di archiviazione hello dell'account di archiviazione, è possibile utilizzare il metodo di analisi hello.

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

Quindi, ottenere un riferimento tooa **cloud_table_client** classe, consente di ottenere gli oggetti di riferimento per le tabelle e le entità archiviate all'interno di hello servizio di archiviazione tabelle. Hello codice seguente viene creata una **cloud_table_client** oggetto utilizzando l'oggetto account di archiviazione hello è recuperato in precedenza:  

```cpp
// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();
```

## <a name="create-a-table"></a>Creare una tabella
L'oggetto **cloud_table_client** consente di ottenere oggetti di riferimento per tabelle ed entità. Hello codice seguente viene creata una **cloud_table_client** dell'oggetto e lo usa toocreate una nuova tabella.

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);  

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference tooa table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table if it doesn't exist.
table.create_if_not_exists();  
```

## <a name="add-an-entity-tooa-table"></a>Aggiungere una tabella tooa entità
creare una nuova tabella tooa un'entità, tooadd **table_entity** e passarlo troppo**table_operation:: insert_entity**. Hello codice seguente Usa nome hello del cliente come chiave di riga hello e last name come chiave di partizione hello. Insieme, di partizione e chiave di riga identificano entità hello nella tabella di hello. Le entità con hello stessa chiave di partizione è possibile eseguire query più velocemente rispetto a quelle con diverse chiavi di partizione, ma con le chiavi di partizione diverse consente una maggiore scalabilità operazione parallela. Per altre informazioni, vedere [Elenco di controllo di prestazioni e scalabilità per Archiviazione di Microsoft Azure](../storage/common/storage-performance-checklist.md).

Hello codice seguente viene creata una nuova istanza della **table_entity** con alcuni toobe dati cliente archiviati. Hello successiva chiama codice **table_operation:: insert_entity** toocreate un **table_operation** tooinsert un'entità dell'oggetto in una tabella, e associa hello nuova entità di tabella con esso. Infine, chiama codice hello hello eseguire il metodo su hello **cloud_table** oggetto. Nuovo hello e **table_operation** invia un toohello richiesta tabella servizio tooinsert hello nuova entità cliente nella tabella "persone" hello.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference tooa table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table if it doesn't exist.
table.create_if_not_exists();

// Create a new customer entity.
azure::storage::table_entity customer1(U("Harp"), U("Walter"));

azure::storage::table_entity::properties_type& properties = customer1.properties();
properties.reserve(2);
properties[U("Email")] = azure::storage::entity_property(U("Walter@contoso.com"));

properties[U("Phone")] = azure::storage::entity_property(U("425-555-0101"));

// Create hello table operation that inserts hello customer entity.
azure::storage::table_operation insert_operation = azure::storage::table_operation::insert_entity(customer1);

// Execute hello insert operation.
azure::storage::table_result insert_result = table.execute(insert_operation);
```

## <a name="insert-a-batch-of-entities"></a>Inserire un batch di entità
È possibile inserire un batch di entità toohello del servizio tabelle in un'unica operazione di scrittura. Hello codice seguente viene creata una **table_batch_operation** e quindi aggiunge tre tooit operazioni di inserimento. Ogni operazione di inserimento viene aggiunto tramite la creazione di un nuovo oggetto entità, impostarne i valori e chiamando quindi hello insert (metodo) su hello **table_batch_operation** entità hello tooassociate di oggetto con una nuova operazione di inserimento. Quindi, **cloud_table.execute** viene chiamato l'operazione di hello tooexecute.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define a batch operation.
azure::storage::table_batch_operation batch_operation;

// Create a customer entity and add it toohello table.
azure::storage::table_entity customer1(U("Smith"), U("Jeff"));

azure::storage::table_entity::properties_type& properties1 = customer1.properties();
properties1.reserve(2);
properties1[U("Email")] = azure::storage::entity_property(U("Jeff@contoso.com"));
properties1[U("Phone")] = azure::storage::entity_property(U("425-555-0104"));

// Create another customer entity and add it toohello table.
azure::storage::table_entity customer2(U("Smith"), U("Ben"));

azure::storage::table_entity::properties_type& properties2 = customer2.properties();
properties2.reserve(2);
properties2[U("Email")] = azure::storage::entity_property(U("Ben@contoso.com"));
properties2[U("Phone")] = azure::storage::entity_property(U("425-555-0102"));

// Create a third customer entity tooadd toohello table.
azure::storage::table_entity customer3(U("Smith"), U("Denise"));

azure::storage::table_entity::properties_type& properties3 = customer3.properties();
properties3.reserve(2);
properties3[U("Email")] = azure::storage::entity_property(U("Denise@contoso.com"));
properties3[U("Phone")] = azure::storage::entity_property(U("425-555-0103"));

// Add customer entities toohello batch insert operation.
batch_operation.insert_or_replace_entity(customer1);
batch_operation.insert_or_replace_entity(customer2);
batch_operation.insert_or_replace_entity(customer3);

// Execute hello batch operation.
std::vector<azure::storage::table_result> results = table.execute_batch(batch_operation);
```

Toonote alcune operazioni per le operazioni batch:  

* È possibile eseguire backup too100 insert, delete, merge, replace, insert o merge e inserire o sostituire operazioni in qualsiasi combinazione in un unico batch.  
* Un'operazione batch può avere un'operazione di recupero, se è l'unica operazione di hello in batch hello.  
* Tutte le entità in una singola operazione batch devono avere hello stessa chiave di partizione.  
* Un'operazione batch è limitato tooa payload dei dati di 4 MB.  

## <a name="retrieve-all-entities-in-a-partition"></a>Recuperare tutte le entità di una partizione
tooquery una tabella per tutte le entità in una partizione, utilizzare un **table_query** oggetto. Hello esempio di codice seguente specifica un filtro per le entità in cui la chiave di partizione hello 'Smith'. In questo esempio visualizza i campi di ogni entità nella console di toohello risultati query hello hello.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Construct hello query operation for all customer entities where PartitionKey="Smith".
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::generate_filter_condition(U("PartitionKey"), azure::storage::query_comparison_operator::equal, U("Smith")));

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Print hello fields for each customer.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

query Hello in questo esempio visualizza tutte le entità hello che soddisfano i criteri di filtro hello. Se si dispongono di tabelle di grandi dimensioni e le entità di tabella hello toodownload spesso, è consigliabile archiviare i dati nei blob di archiviazione di Azure invece.

## <a name="retrieve-a-range-of-entities-in-a-partition"></a>Recuperare un intervallo di entità in una partizione
Se non si desidera tooquery tutte le entità hello in una partizione, è possibile specificare un intervallo mediante la combinazione di filtri chiave di partizione hello con un filtro di riga di chiave. Hello esempio di codice seguente usa due filtri tooget tutte le entità nella partizione "Smith" in cui la chiave di riga hello (nome) inizia con una lettera precedente a 'E' alfabeto hello e quindi Visualizza i risultati della query hello.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table query.
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::combine_filter_conditions(
    azure::storage::table_query::generate_filter_condition(U("PartitionKey"),
    azure::storage::query_comparison_operator::equal, U("Smith")),
    azure::storage::query_logical_operator::op_and,
    azure::storage::table_query::generate_filter_condition(U("RowKey"), azure::storage::query_comparison_operator::less_than, U("E"))));

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Loop through hello results, displaying information about hello entity.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

## <a name="retrieve-a-single-entity"></a>Recuperare una singola entità
È possibile scrivere un tooretrieve query un'entità singola e specifica. codice Hello seguente usa **table_operation:: retrieve_entity** cliente hello toospecify "Jeff Smith". Questo metodo restituisce una sola entità, anziché una raccolta e hello valore restituito è **table_result**. Specifica le chiavi di partizione e di riga in una query è tooretrieve modo più veloce di hello una singola entità dal servizio tabelle hello.  

```cpp
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Output hello entity.
azure::storage::table_entity entity = retrieve_result.entity();
const azure::storage::table_entity::properties_type& properties = entity.properties();

std::wcout << U("PartitionKey: ") << entity.partition_key() << U(", RowKey: ") << entity.row_key()
    << U(", Property1: ") << properties.at(U("Email")).string_value()
    << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
```

## <a name="replace-an-entity"></a>Sostituire un'entità
tooreplace un'entità, recuperarlo dal servizio tabelle hello, modificare l'oggetto entità hello e quindi salvare le modifiche apportate hello eseguire il servizio tabelle toohello. Hello codice riportato di seguito modifica indirizzo di posta elettronica e il numero di telefono del cliente esistente. Anziché chiamare **table_operation:: insert_entity**, in questo codice viene usato **table_operation:: replace_entity**. In questo modo hello entità toobe completamente sostituito nel server di hello, a meno che l'entità di hello sul server hello è stato modificato dopo che è stata recuperata, nel qual caso hello operazione non riuscirà. Questo errore è tooprevent l'applicazione di sovrascrivere accidentalmente una modifica apportata tra hello il recupero e l'aggiornamento da un altro componente dell'applicazione. Hello la corretta gestione di questo errore è tooretrieve hello entità nuovamente, apportare le modifiche (se è ancora valida) e quindi eseguire un altro **table_operation:: replace_entity** operazione. Nella sezione successiva Hello viene illustrato come toooverride questo comportamento.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Replace an entity.
azure::storage::table_entity entity_to_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_replace = entity_to_replace.properties();
properties_to_replace.reserve(2);

// Specify a new phone number.
properties_to_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0106"));

// Specify a new email address.
properties_to_replace[U("Email")] = azure::storage::entity_property(U("JeffS@contoso.com"));

// Create an operation tooreplace hello entity.
azure::storage::table_operation replace_operation = azure::storage::table_operation::replace_entity(entity_to_replace);

// Submit hello operation toohello Table service.
azure::storage::table_result replace_result = table.execute(replace_operation);
```

## <a name="insert-or-replace-an-entity"></a>Inserire o sostituire un'entità
**table_operation:: replace_entity** operazioni hanno esito negativo se l'entità hello è stato modificato dopo che è stata recuperata dal server hello. Inoltre, è necessario recuperare entità hello dal server hello prima in ordine per **table_operation:: replace_entity** toobe ha esito positivo. In alcuni casi, tuttavia, non si conosce se entità hello esista nel server di hello e i valori correnti di hello in essa archiviati sono irrilevanti, ovvero l'aggiornamento deve sovrascrivere tutti. tooaccomplish, si utilizzerebbe un **table_operation:: insert_or_replace_entity** operazione. Questa operazione inserisce l'entità di hello se non esiste oppure lo sostituisce in caso affermativo, indipendentemente dal fatto se hello ultimo aggiornamento. Nell'esempio di codice seguente di hello, entità customer hello per Jeff Smith viene ancora recuperato, ma viene quindi salvato server back-toohello tramite **table_operation:: insert_or_replace_entity**. Gli aggiornamenti effettuati toohello entità di operazione di aggiornamento e recupero hello verranno sovrascritto.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Insert-or-replace an entity.
azure::storage::table_entity entity_to_insert_or_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_insert_or_replace = entity_to_insert_or_replace.properties();

properties_to_insert_or_replace.reserve(2);

// Specify a phone number.
properties_to_insert_or_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0107"));

// Specify an email address.
properties_to_insert_or_replace[U("Email")] = azure::storage::entity_property(U("Jeffsm@contoso.com"));

// Create an operation tooinsert-or-replace hello entity.
azure::storage::table_operation insert_or_replace_operation = azure::storage::table_operation::insert_or_replace_entity(entity_to_insert_or_replace);

// Submit hello operation toohello Table service.
azure::storage::table_result insert_or_replace_result = table.execute(insert_or_replace_operation);
```

## <a name="query-a-subset-of-entity-properties"></a>Eseguire query su un subset di proprietà di entità
Una tabella di tooa query è possibile recuperare solo alcune proprietà di un'entità. query nel seguente codice hello Hello utilizza hello **table_query:: set_select_columns** metodo tooreturn solo hello indirizzi di posta elettronica di entità nella tabella hello.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define hello query, and select only hello Email property.
azure::storage::table_query query;
std::vector<utility::string_t> columns;

columns.push_back(U("Email"));
query.set_select_columns(columns);

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Display hello results.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key();

    const azure::storage::table_entity::properties_type& properties = it->properties();
    for (auto prop_it = properties.begin(); prop_it != properties.end(); ++prop_it)
    {
        std::wcout << ", " << prop_it->first << ": " << prop_it->second.str();
    }

    std::wcout << std::endl;
}
```

> [!NOTE]
> L'esecuzione di una query di alcune proprietà di un'entità è un'operazione più efficiente rispetto al recupero di tutte le proprietà.
> 
> 

## <a name="delete-an-entity"></a>Eliminare un'entità
È possibile eliminare facilmente un'entità dopo averla recuperata. Una volta recuperato entità hello, chiamare **table_operation:: delete_entity** con toodelete entità hello. Chiamare quindi hello **cloud_table.execute** metodo. Hello codice seguente recupera ed elimina un'entità con una chiave di partizione "Smith" e una chiave di riga di "Jeff".  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation toodelete hello entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit hello delete operation toohello Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);  
```

## <a name="delete-a-table"></a>Eliminare una tabella
Infine, hello esempio di codice seguente elimina una tabella da un account di archiviazione. Una tabella in cui è stata eliminata, sarà disponibile toobe ricreati per un periodo di tempo dopo l'eliminazione di hello.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation toodelete hello entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit hello delete operation toohello Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);
```

## <a name="next-steps"></a>Passaggi successivi
Ora che si sono appreso i concetti fondamentali di hello dell'archiviazione tabelle, seguire questi toolearn collegamenti ulteriori informazioni sull'archiviazione di Azure:  

* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) è un'app autonoma, disponibile da Microsoft che consente di toowork visivamente i dati di archiviazione di Azure in Windows, macOS e Linux.
* [Come toouse archiviazione Blob da C++](../storage/blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [Come toouse l'archiviazione delle code da C++](../storage/queues/storage-c-plus-plus-how-to-use-queues.md)
* [Elenco delle risorse di archiviazione di Azure in C++](../storage/common/storage-c-plus-plus-enumeration.md)
* [Informazioni di riferimento sulla libreria client di archiviazione per C++](http://azure.github.io/azure-storage-cpp)
* [Documentazione di Archiviazione di Azure](https://azure.microsoft.com/documentation/services/storage/)
