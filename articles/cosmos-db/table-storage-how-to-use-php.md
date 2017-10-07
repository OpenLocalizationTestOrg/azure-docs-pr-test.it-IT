---
title: archiviazione tabelle di toouse aaaHow da PHP | Documenti Microsoft
description: Scopri toouse hello del servizio tabelle da PHP toocreate ed eliminare una tabella e insert, delete e tabella hello di query.
services: cosmos-db
documentationcenter: php
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: 1e57f371-6208-4753-b2a0-05db4aede8e3
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: php
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 5b7c92221069d1c2a6ca951c06ae8eea8bb8478c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-php"></a>Tabella di archiviazione da PHP toouse
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Panoramica
Questa guida viene illustrato come gli scenari comuni di tooperform utilizzando hello del servizio tabelle di Azure. esempi di Hello sono scritti in PHP e utilizzare hello [Azure SDK per PHP][download]. Hello scenari trattati includono **la creazione e l'eliminazione di una tabella e inserendo, eliminando e una query sulle entità in una tabella**. Per ulteriori informazioni su hello del servizio tabelle di Azure, vedere hello [passaggi successivi](#next-steps) sezione.

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>Creare un'applicazione PHP
Hello solo requisito per la creazione di un'applicazione PHP che accede al servizio tabelle di Azure hello è hello che fanno riferimento a delle classi in hello Azure SDK per PHP all'interno del codice. È possibile utilizzare qualsiasi toocreate di strumenti di sviluppo dell'applicazione, inclusi il blocco note.

In questa guida vengono usate le funzionalità del servizio tabelle che possono essere chiamate da un'applicazione PHP in locale o nel codice in esecuzione in un ruolo Web, in un ruolo di lavoro o in un sito Web di Azure.

## <a name="get-hello-azure-client-libraries"></a>Recuperare le librerie Client di hello Azure
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-table-service"></a>Configurare il servizio di applicazione tooaccess hello tabella
toouse hello Azure API del servizio tabelle, è necessario:

1. File di riferimento autoloader hello utilizzando hello [require_once] [ require_once] istruzione, e
2. Fare riferimento a tutte le eventuali classi utilizzabili.

Hello esempio seguente viene illustrato come tooinclude hello hello di file e riferimento autoloader **ServicesBuilder** classe.

> [!NOTE]
> esempi di Hello in questo articolo presuppongono installate le librerie Client di PHP per Azure tramite Composer hello. Se le librerie di hello è stato installato manualmente, è necessario tooreference hello <code>WindowsAzure.php</code> autoloader file.
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

Negli esempi di hello riportato di seguito, hello `require_once` istruzione viene sempre visualizzata, ma solo hello classi necessarie per tooexecute esempio hello viene fatto riferimento.

## <a name="set-up-an-azure-storage-connection"></a>Configurare una connessione di archiviazione di Azure
tooinstantiate un client del servizio tabelle di Azure, è innanzitutto necessario una stringa di connessione valido. stringa di connessione del servizio tabella hello Hello formato è:

Per accedere a un servizio attivo:

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

Per l'accesso all'archiviazione di emulatore hello:

```php
UseDevelopmentStorage=true
```

toocreate qualsiasi client del servizio di Azure, è necessario hello toouse **ServicesBuilder** classe. È possibile:

* Passare la connessione hello stringa direttamente tooit o
* Hello utilizzare **CloudConfigurationManager (CCM)** toocheck origini dati esterne di più origini per la stringa di connessione hello:
  * per impostazione predefinita, viene fornito con il supporto per un'origine esterna, ovvero le variabili ambientali
  * è possibile aggiungere nuove origini estendendo hello **ConnectionStringSource** classe

Per esempi di hello descritti di seguito, la stringa di connessione hello verrà passata direttamente.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);
```

## <a name="create-a-table"></a>Creare una tabella
Oggetto **TableRestProxy** oggetto consente di creare una tabella con hello **createTable** metodo. Quando si crea una tabella, è possibile impostare timeout del servizio di tabella hello. (Per ulteriori informazioni sui timeout servizio tabella di hello, vedere [impostazione dei timeout per le operazioni del servizio tabelle][table-service-timeouts].)

```php
require_once 'vendor\autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    // Create table.
    $tableRestProxy->createTable("mytable");
}
catch(ServiceException $e){
    $code = $e->getCode();
    $error_message = $e->getMessage();
    // Handle exception based on error codes and messages.
    // Error codes and messages can be found here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
}
```

Per informazioni sulle restrizioni per i nomi di tabella, vedere [hello comprensione modello di dati del servizio tabelle][table-data-model].

## <a name="add-an-entity-tooa-table"></a>Aggiungere una tabella tooa entità
creare una nuova tabella tooa un'entità, tooadd **entità** e passarlo troppo**TableRestProxy -> insertEntity**. Si noti che durante la creazione di un'entità, è necessario specificare le chiavi `PartitionKey` e `RowKey`. Si tratta hello identificatori univoci per un'entità e sono valori che è possono eseguire una query più velocemente rispetto alle altre proprietà dell'entità. Utilizza sistema Hello `PartitionKey` tooautomatically distribuire entità della tabella hello su molti nodi di archiviazione. Le entità con hello stesso `PartitionKey` vengono archiviati in hello stesso nodo. (Operazioni in più entità archiviata nel hello stesso nodo eseguire migliori rispetto alle entità archiviate in nodi diversi.) Hello `RowKey` hello ID univoco di un'entità all'interno di una partizione.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$entity = new Entity();
$entity->setPartitionKey("tasksSeattle");
$entity->setRowKey("1");
$entity->addProperty("Description", null, "Take out hello trash.");
$entity->addProperty("DueDate",
                        EdmType::DATETIME,
                        new DateTime("2012-11-05T08:15:00-08:00"));
$entity->addProperty("Location", EdmType::STRING, "Home");

try{
    $tableRestProxy->insertEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
}
```

Per informazioni sulle proprietà di tabella e tipi, vedere [hello comprensione modello di dati del servizio tabelle][table-data-model].

Hello **TableRestProxy** classe offre due metodi alternativi per l'inserimento di entità: **insertOrMergeEntity** e **insertOrReplaceEntity**. toouse questi metodi, creare un nuovo **entità** e passarlo come un metodo tooeither di parametro. Ogni metodo inserirà entità hello se non esiste. Se l'entità di hello esiste già, **insertOrMergeEntity** Aggiorna i valori delle proprietà, se esiste già una proprietà hello e aggiunge nuove proprietà se non sono presenti, mentre **insertOrReplaceEntity** completamente sostituisce un'entità esistente. Hello seguente esempio viene illustrato come toouse **insertOrMergeEntity**. Se l'entità con hello `PartitionKey` "tasksSeattle" e `RowKey` "1" non esiste già, verrà inserito. Tuttavia, se è stato inserito in precedenza (come illustrato nell'esempio hello precedente), hello `DueDate` proprietà verrà aggiornata e hello `Status` proprietà verrà aggiunta. Hello `Description` e `Location` vengono aggiornate anche le proprietà, ma con i valori che in modo efficace lasciarli invariati. Se queste ultime due proprietà sono stati aggiunti come illustrato nell'esempio hello ma non presenti nell'entità di destinazione hello, i relativi valori esistente resterà invariati.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

//Create new entity.
$entity = new Entity();

// PartitionKey and RowKey are required.
$entity->setPartitionKey("tasksSeattle");
$entity->setRowKey("1");

// If entity exists, existing properties are updated with new values and
// new properties are added. Missing properties are unchanged.
$entity->addProperty("Description", null, "Take out hello trash.");
$entity->addProperty("DueDate", EdmType::DATETIME, new DateTime()); // Modified hello DueDate field.
$entity->addProperty("Location", EdmType::STRING, "Home");
$entity->addProperty("Status", EdmType::STRING, "Complete"); // Added Status field.

try    {
    // Calling insertOrReplaceEntity, instead of insertOrMergeEntity as shown,
    // would simply replace hello entity with PartitionKey "tasksSeattle" and RowKey "1".
    $tableRestProxy->insertOrMergeEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="retrieve-a-single-entity"></a>Recuperare una singola entità
Hello **TableRestProxy -> getEntity** metodo consente di tooretrieve una singola entità eseguendo una query per il relativo `PartitionKey` e `RowKey`. Nell'esempio hello seguente la chiave di partizione di hello `tasksSeattle` e chiave di riga `1` vengono passati toohello **getEntity** metodo.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    $result = $tableRestProxy->getEntity("mytable", "tasksSeattle", 1);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entity = $result->getEntity();

echo $entity->getPartitionKey().":".$entity->getRowKey();
```

## <a name="retrieve-all-entities-in-a-partition"></a>Recuperare tutte le entità di una partizione
Le query di entità vengono create usando i filtri. Per altre informazioni, vedere [Querying Tables and Entities][filters] (Query di tabelle ed entità). tooretrieve tutte le entità nella partizione, utilizzare il filtro di hello "eq PartitionKey *nome_partizione*". Hello seguente esempio viene illustrato come tooretrieve tutte le entità in hello `tasksSeattle` partizione passando un filtro toohello **queryEntities** metodo.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$filter = "PartitionKey eq 'tasksSeattle'";

try    {
    $result = $tableRestProxy->queryEntities("mytable", $filter);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entities = $result->getEntities();

foreach($entities as $entity){
    echo $entity->getPartitionKey().":".$entity->getRowKey()."<br />";
}
```

## <a name="retrieve-a-subset-of-entities-in-a-partition"></a>Recuperare un subset di entità in una partizione
Hello stesso modello utilizzato nell'esempio precedente hello può essere utilizzato tooretrieve qualsiasi sottoinsieme di entità in una partizione. subset di Hello di entità è recuperare sono determinati dal filtro hello è utilizzare (per ulteriori informazioni, vedere [query su tabelle ed entità][filters]) .hello seguente esempio viene illustrato come toouse tooretrieve un filtro tutte le entità con uno specifico `Location` e `DueDate` inferiore a una data specificata.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$filter = "Location eq 'Office' and DueDate lt '2012-11-5'";

try    {
    $result = $tableRestProxy->queryEntities("mytable", $filter);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entities = $result->getEntities();

foreach($entities as $entity){
    echo $entity->getPartitionKey().":".$entity->getRowKey()."<br />";
}
```

## <a name="retrieve-a-subset-of-entity-properties"></a>Recuperare un subset di proprietà di entità
È possibile recuperare un subset di proprietà di entità eseguendo una query. Questa tecnica, denominata *proiezione*, consente di ridurre la larghezza di banda e di migliorare le prestazioni della query, in particolare per entità di grandi dimensioni. recuperata una proprietà toobe toospecify, passare il nome di hello di hello proprietà toohello **Query -> addSelectField** metodo. È possibile chiamare questo metodo più volte tooadd più proprietà. Dopo l'esecuzione di **TableRestProxy -> queryEntities**, hello restituite entità disporrà solo proprietà hello selezionato. (Tooreturn un subset di entità della tabella, utilizzare un filtro come illustrato nella query hello precedenti.)

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\QueryEntitiesOptions;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$options = new QueryEntitiesOptions();
$options->addSelectField("Description");

try    {
    $result = $tableRestProxy->queryEntities("mytable", $options);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

// All entities in hello table are returned, regardless of whether
// they have hello Description field.
// toolimit hello results returned, use a filter.
$entities = $result->getEntities();

foreach($entities as $entity){
    $description = $entity->getProperty("Description")->getValue();
    echo $description."<br />";
}
```

## <a name="update-an-entity"></a>Aggiornare un'entità
Un'entità esistente può essere aggiornata tramite hello **entità -> setProperty** e **entità -> addProperty** metodi su entità hello e quindi chiamando **TableRestProxy -> updateEntity** . Hello esempio seguente recupera un'entità, viene modificata una proprietà, rimuove un'altra proprietà e aggiunge una nuova proprietà. Si noti che è possibile rimuovere una proprietà impostando il relativo valore troppo**null**.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$result = $tableRestProxy->getEntity("mytable", "tasksSeattle", 1);

$entity = $result->getEntity();

$entity->setPropertyValue("DueDate", new DateTime()); //Modified DueDate.

$entity->setPropertyValue("Location", null); //Removed Location.

$entity->addProperty("Status", EdmType::STRING, "In progress"); //Added Status.

try    {
    $tableRestProxy->updateEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="delete-an-entity"></a>Eliminare un'entità
toodelete un'entità, passare il nome di tabella hello e dell'entità hello `PartitionKey` e `RowKey` toohello **TableRestProxy -> deleteEntity** metodo.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    // Delete entity.
    $tableRestProxy->deleteEntity("mytable", "tasksSeattle", "2");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

Si noti che per i controlli di concorrenza, è possibile impostare hello Etag per un toobe entità eliminata tramite hello **DeleteEntityOptions -> setEtag** hello metodo e passando **DeleteEntityOptions** oggetto troppo**deleteEntity** come quarto parametro.

## <a name="batch-table-operations"></a>Operazioni batch su tabella
Hello **TableRestProxy -> batch** metodo consente di tooexecute più operazioni in una singola richiesta. Hello analogie prevede l'aggiunta di operazioni troppo**batchrequest seguito** oggetto e quindi passare hello **batchrequest seguito** oggetto toohello **TableRestProxy -> batch** metodo. un'operazione di tooa tooadd **batchrequest seguito** dell'oggetto, è possibile chiamare uno dei seguenti metodi più volte hello:

* **addInsertEntity** (per aggiungere un'operazione insertEntity)
* **addUpdateEntity** (per aggiungere un'operazione updateEntity)
* **addMergeEntity** (per aggiungere un'operazione mergeEntity)
* **addInsertOrReplaceEntity** (per aggiungere un'operazione insertOrReplaceEntity)
* **addInsertOrMergeEntity** (per aggiungere un'operazione insertOrMergeEntity)
* **addDeleteEntity** (per aggiungere un'operazione deleteEntity)

Hello seguente esempio viene illustrato come tooexecute **insertEntity** e **deleteEntity** operazioni in una singola richiesta:

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;
use MicrosoftAzure\Storage\Table\Models\BatchOperations;

    // Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

// Create list of batch operation.
$operations = new BatchOperations();

$entity1 = new Entity();
$entity1->setPartitionKey("tasksSeattle");
$entity1->setRowKey("2");
$entity1->addProperty("Description", null, "Clean roof gutters.");
$entity1->addProperty("DueDate",
                        EdmType::DATETIME,
                        new DateTime("2012-11-05T08:15:00-08:00"));
$entity1->addProperty("Location", EdmType::STRING, "Home");

// Add operation toolist of batch operations.
$operations->addInsertEntity("mytable", $entity1);

// Add operation toolist of batch operations.
$operations->addDeleteEntity("mytable", "tasksSeattle", "1");

try    {
    $tableRestProxy->batch($operations);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

Per altre informazioni su operazioni batch su tabelle, vedere [Performing Entity Group Transactions][entity-group-transactions] (Esecuzione di transazioni di gruppi di entità).

## <a name="delete-a-table"></a>Eliminare una tabella
Infine, toodelete una tabella, passare hello tabella nome toohello **TableRestProxy -> deleteTable** metodo.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    // Delete table.
    $tableRestProxy->deleteTable("mytable");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="next-steps"></a>Passaggi successivi
Ora che si è appreso i concetti di base di hello di hello del servizio tabelle di Azure, seguire questi toolearn collegamenti sulle attività di archiviazione più complesse.

* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) è un'app autonoma, disponibile da Microsoft che consente di toowork visivamente i dati di archiviazione di Azure in Windows, macOS e Linux.

* [Centro sviluppatori PHP](/develop/php/).

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://php.net/require_once
[table-service-timeouts]: http://msdn.microsoft.com/library/azure/dd894042.aspx

[table-data-model]: http://msdn.microsoft.com/library/azure/dd179338.aspx
[filters]: http://msdn.microsoft.com/library/azure/dd894031.aspx
[entity-group-transactions]: http://msdn.microsoft.com/library/azure/dd894038.aspx
