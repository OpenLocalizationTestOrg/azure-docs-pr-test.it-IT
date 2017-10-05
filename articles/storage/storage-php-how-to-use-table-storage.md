---
title: Come usare l'archiviazione tabelle da PHP | Microsoft Docs
description: Informazioni su come usare il Servizio tabelle da PHP per creare ed eliminare una tabella e per inserire, eliminare ed eseguire query su tabelle.
services: storage
documentationcenter: php
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 1e57f371-6208-4753-b2a0-05db4aede8e3
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: php
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 15d3216ef5bb1d7ff312bd886837a3a7b0335afd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-table-storage-from-php"></a><span data-ttu-id="4d70f-103">Come usare l'archiviazione tabelle da PHP</span><span class="sxs-lookup"><span data-stu-id="4d70f-103">How to use table storage from PHP</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="4d70f-104">Overview</span><span class="sxs-lookup"><span data-stu-id="4d70f-104">Overview</span></span>
<span data-ttu-id="4d70f-105">Questa guida illustra come eseguire scenari comuni con il servizio tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="4d70f-105">This guide shows you how to perform common scenarios using the Azure Table service.</span></span> <span data-ttu-id="4d70f-106">Gli esempi sono scritti in PHP e usano [Azure SDK per PHP][download].</span><span class="sxs-lookup"><span data-stu-id="4d70f-106">The samples are written in PHP and use the [Azure SDK for PHP][download].</span></span> <span data-ttu-id="4d70f-107">Gli scenari presentati includono **creazione ed eliminazione di una tabella, inserimento ed eliminazione di entità ed esecuzione di query sulle entità in una tabella**.</span><span class="sxs-lookup"><span data-stu-id="4d70f-107">The scenarios covered include **creating and deleting a table, and inserting, deleting, and querying entities in a table**.</span></span> <span data-ttu-id="4d70f-108">Per altre informazioni sul servizio tabelle di Azure, vedere la sezione [Passaggi successivi](#next-steps) .</span><span class="sxs-lookup"><span data-stu-id="4d70f-108">For more information on the Azure Table service, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="4d70f-109">Creare un'applicazione PHP</span><span class="sxs-lookup"><span data-stu-id="4d70f-109">Create a PHP application</span></span>
<span data-ttu-id="4d70f-110">Per creare un'applicazione PHP che accede al Servizio tabelle di Azure, è sufficiente fare riferimento alle classi in Azure SDK per PHP dall'interno del codice.</span><span class="sxs-lookup"><span data-stu-id="4d70f-110">The only requirement for creating a PHP application that accesses the Azure Table service is the referencing of classes in the Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="4d70f-111">Per creare l'applicazione, è possibile usare qualsiasi strumento di sviluppo, incluso il Blocco note.</span><span class="sxs-lookup"><span data-stu-id="4d70f-111">You can use any development tools to create your application, including Notepad.</span></span>

<span data-ttu-id="4d70f-112">In questa guida vengono usate le funzionalità del servizio tabelle che possono essere chiamate da un'applicazione PHP in locale o nel codice in esecuzione in un ruolo Web, in un ruolo di lavoro o in un sito Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="4d70f-112">In this guide, you use Table service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="4d70f-113">Acquisire le librerie client di Azure</span><span class="sxs-lookup"><span data-stu-id="4d70f-113">Get the Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-access-the-table-service"></a><span data-ttu-id="4d70f-114">Configurare l'applicazione per accedere al Servizio tabelle</span><span class="sxs-lookup"><span data-stu-id="4d70f-114">Configure your application to access the Table service</span></span>
<span data-ttu-id="4d70f-115">Per utilizzare le API del Servizio tabelle di Azure, è necessario:</span><span class="sxs-lookup"><span data-stu-id="4d70f-115">To use the Azure Table service APIs, you need to:</span></span>

1. <span data-ttu-id="4d70f-116">Fare riferimento al file autoloader mediante l'istruzione [require_once][require_once]</span><span class="sxs-lookup"><span data-stu-id="4d70f-116">Reference the autoloader file using the [require_once][require_once] statement, and</span></span>
2. <span data-ttu-id="4d70f-117">Fare riferimento a tutte le eventuali classi utilizzabili.</span><span class="sxs-lookup"><span data-stu-id="4d70f-117">Reference any classes you might use.</span></span>

<span data-ttu-id="4d70f-118">Nell'esempio seguente viene indicato come includere il file autoloader e fare riferimento alla classe **ServicesBuilder** .</span><span class="sxs-lookup"><span data-stu-id="4d70f-118">The following example shows how to include the autoloader file and reference the **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="4d70f-119">Gli esempi in questo articolo presuppongono che siano state installate le librerie client PHP per Azure tramite Composer.</span><span class="sxs-lookup"><span data-stu-id="4d70f-119">The examples in this article assume you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="4d70f-120">Se le librerie sono state installate manualmente, sarà necessario fare riferimento al file autoloader <code>WindowsAzure.php</code> .</span><span class="sxs-lookup"><span data-stu-id="4d70f-120">If you installed the libraries manually, you need to reference the <code>WindowsAzure.php</code> autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="4d70f-121">Negli esempi seguenti viene mostrata sempre l'istruzione `require_once` , ma si fa riferimento solo alle classi necessarie per l'esecuzione dell'esempio.</span><span class="sxs-lookup"><span data-stu-id="4d70f-121">In the examples below, the `require_once` statement is always shown, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="4d70f-122">Configurare una connessione di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="4d70f-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="4d70f-123">Per creare un'istanza di un client del servizio tabelle di Azure, è necessario avere prima una stringa di connessione valida.</span><span class="sxs-lookup"><span data-stu-id="4d70f-123">To instantiate an Azure Table service client, you must first have a valid connection string.</span></span> <span data-ttu-id="4d70f-124">Il formato della stringa di connessione del servizio tabelle è:</span><span class="sxs-lookup"><span data-stu-id="4d70f-124">The format for the Table service connection string is:</span></span>

<span data-ttu-id="4d70f-125">Per accedere a un servizio attivo:</span><span class="sxs-lookup"><span data-stu-id="4d70f-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="4d70f-126">Per accedere alla memoria dell'emulatore:</span><span class="sxs-lookup"><span data-stu-id="4d70f-126">For accessing the emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="4d70f-127">Per creare un client di servizio di Azure, è necessario usare la classe **ServicesBuilder** .</span><span class="sxs-lookup"><span data-stu-id="4d70f-127">To create any Azure service client, you need to use the **ServicesBuilder** class.</span></span> <span data-ttu-id="4d70f-128">È possibile:</span><span class="sxs-lookup"><span data-stu-id="4d70f-128">You can:</span></span>

* <span data-ttu-id="4d70f-129">passare la stringa di connessione direttamente a essa o</span><span class="sxs-lookup"><span data-stu-id="4d70f-129">pass the connection string directly to it or</span></span>
* <span data-ttu-id="4d70f-130">utilizzare **CloudConfigurationManager (CCM)** per cercare la stringa di connessione in più origini esterne:</span><span class="sxs-lookup"><span data-stu-id="4d70f-130">use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="4d70f-131">per impostazione predefinita, viene fornito con il supporto per un'origine esterna, ovvero le variabili ambientali</span><span class="sxs-lookup"><span data-stu-id="4d70f-131">by default, it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="4d70f-132">è possibile aggiungere nuove origini estendendo la classe **ConnectionStringSource**</span><span class="sxs-lookup"><span data-stu-id="4d70f-132">you can add new sources by extending the **ConnectionStringSource** class</span></span>

<span data-ttu-id="4d70f-133">Per gli esempi illustrati in questo articolo, la stringa di connessione verrà passata direttamente.</span><span class="sxs-lookup"><span data-stu-id="4d70f-133">For the examples outlined here, the connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);
```

## <a name="create-a-table"></a><span data-ttu-id="4d70f-134">Creare una tabella</span><span class="sxs-lookup"><span data-stu-id="4d70f-134">Create a table</span></span>
<span data-ttu-id="4d70f-135">Un oggetto **TableRestProxy** consente di creare una tabella usando il metodo **createTable**.</span><span class="sxs-lookup"><span data-stu-id="4d70f-135">A **TableRestProxy** object lets you create a table with the **createTable** method.</span></span> <span data-ttu-id="4d70f-136">Durante la creazione di una tabella, è possibile impostare il timeout del servizio tabelle.</span><span class="sxs-lookup"><span data-stu-id="4d70f-136">When creating a table, you can set the Table service timeout.</span></span> <span data-ttu-id="4d70f-137">Per altre informazioni sul timeout del servizio tabelle, vedere [Setting Timeouts for Table Service Operations][table-service-timeouts] (Impostazione di timeout per le operazioni del servizio tabelle).</span><span class="sxs-lookup"><span data-stu-id="4d70f-137">(For more information about the Table service timeout, see [Setting Timeouts for Table Service Operations][table-service-timeouts].)</span></span>

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

<span data-ttu-id="4d70f-138">Per informazioni sulle restrizioni ai nomi delle tabelle, vedere [Understanding the Table Service Data Model][table-data-model] (Informazioni sul modello di dati del servizio tabelle).</span><span class="sxs-lookup"><span data-stu-id="4d70f-138">For information about restrictions on table names, see [Understanding the Table Service Data Model][table-data-model].</span></span>

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="4d70f-139">Aggiungere un'entità a una tabella</span><span class="sxs-lookup"><span data-stu-id="4d70f-139">Add an entity to a table</span></span>
<span data-ttu-id="4d70f-140">Per aggiungere un'entità a una tabella, creare un nuovo oggetto **Entity** e passarlo a **TableRestProxy->insertEntity**.</span><span class="sxs-lookup"><span data-stu-id="4d70f-140">To add an entity to a table, create a new **Entity** object and pass it to **TableRestProxy->insertEntity**.</span></span> <span data-ttu-id="4d70f-141">Si noti che durante la creazione di un'entità, è necessario specificare le chiavi `PartitionKey` e `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="4d70f-141">Note that when you create an entity, you must specify a `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="4d70f-142">Si tratta di identificatori univoci dell'entità e sono valori che possono essere interrogati molto più velocemente rispetto ad altre proprietà dell'entità.</span><span class="sxs-lookup"><span data-stu-id="4d70f-142">These are the unique identifiers for an entity and are values that can be queried much faster than other entity properties.</span></span> <span data-ttu-id="4d70f-143">Il sistema usa `PartitionKey` per distribuire automaticamente le entità della tabella su molti nodi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4d70f-143">The system uses `PartitionKey` to automatically distribute the table's entities over many storage nodes.</span></span> <span data-ttu-id="4d70f-144">Le entità con lo stesso `PartitionKey` vengono archiviate nello stesso nodo.</span><span class="sxs-lookup"><span data-stu-id="4d70f-144">Entities with the same `PartitionKey` are stored on the same node.</span></span> <span data-ttu-id="4d70f-145">Operazioni su più entità archiviate nello stesso nodo vengono eseguite più efficacemente che non su entità archiviate in nodi diversi. `RowKey` è l'ID univoco di un'entità all'interno di una partizione.</span><span class="sxs-lookup"><span data-stu-id="4d70f-145">(Operations on multiple entities stored on the same node perform better than on entities stored across different nodes.) The `RowKey` is the unique ID of an entity within a partition.</span></span>

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
$entity->addProperty("Description", null, "Take out the trash.");
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

<span data-ttu-id="4d70f-146">Per informazioni sulle proprietà e i tipi di tabelle, vedere [Understanding the Table Service Data Model][table-data-model] (Informazioni sul modello di dati del servizio tabelle).</span><span class="sxs-lookup"><span data-stu-id="4d70f-146">For information about Table properties and types, see [Understanding the Table Service Data Model][table-data-model].</span></span>

<span data-ttu-id="4d70f-147">La classe **TableRestProxy** offre due metodi alternativi per l'inserimento di entità: **insertOrMergeEntity** e **insertOrReplaceEntity**.</span><span class="sxs-lookup"><span data-stu-id="4d70f-147">The **TableRestProxy** class offers two alternative methods for inserting entities: **insertOrMergeEntity** and **insertOrReplaceEntity**.</span></span> <span data-ttu-id="4d70f-148">Per utilizzare questi metodi, creare una nuova **Entity** e passarla come parametro a uno dei due metodi.</span><span class="sxs-lookup"><span data-stu-id="4d70f-148">To use these methods, create a new **Entity** and pass it as a parameter to either method.</span></span> <span data-ttu-id="4d70f-149">Ogni metodo inserirà l'entità se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="4d70f-149">Each method will insert the entity if it does not exist.</span></span> <span data-ttu-id="4d70f-150">Se l'entità esiste già, **insertOrMergeEntity** aggiornerà i valori delle proprietà esistenti e aggiungerà nuove proprietà se non esistono, mentre **insertOrReplaceEntity** sostituirà completamente un'entità esistente.</span><span class="sxs-lookup"><span data-stu-id="4d70f-150">If the entity already exists, **insertOrMergeEntity** updates property values if the properties already exist and adds new properties if they do not exist, while **insertOrReplaceEntity** completely replaces an existing entity.</span></span> <span data-ttu-id="4d70f-151">Nell'esempio seguente viene illustrato come utilizzare **insertOrMergeEntity**.</span><span class="sxs-lookup"><span data-stu-id="4d70f-151">The following example shows how to use **insertOrMergeEntity**.</span></span> <span data-ttu-id="4d70f-152">Se l'entità con `PartitionKey` "tasksSeattle" e `RowKey` "1" non esiste già, verrà inserita.</span><span class="sxs-lookup"><span data-stu-id="4d70f-152">If the entity with `PartitionKey` "tasksSeattle" and `RowKey` "1" does not already exist, it will be inserted.</span></span> <span data-ttu-id="4d70f-153">Se è stata inserita in precedenza (come illustrato nell'esempio precedente), la proprietà `DueDate` verrà aggiornata e verrà aggiunta la proprietà `Status`.</span><span class="sxs-lookup"><span data-stu-id="4d70f-153">However, if it has previously been inserted (as shown in the example above), the `DueDate` property will be updated, and the `Status` property will be added.</span></span> <span data-ttu-id="4d70f-154">Verranno aggiornate anche le proprietà `Description` e `Location`, ma con valori che non apporteranno alcuna modifica.</span><span class="sxs-lookup"><span data-stu-id="4d70f-154">The `Description` and `Location` properties are also updated, but with values that effectively leave them unchanged.</span></span> <span data-ttu-id="4d70f-155">Se queste due ultime proprietà non sono state aggiunte come illustrato nell'esempio, ma erano disponibili nell'entità di destinazione, i loro valori esistenti non subiranno alcuna modifica.</span><span class="sxs-lookup"><span data-stu-id="4d70f-155">If these latter two properties were not added as shown in the example, but existed on the target entity, their existing values would remain unchanged.</span></span>

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
$entity->addProperty("Description", null, "Take out the trash.");
$entity->addProperty("DueDate", EdmType::DATETIME, new DateTime()); // Modified the DueDate field.
$entity->addProperty("Location", EdmType::STRING, "Home");
$entity->addProperty("Status", EdmType::STRING, "Complete"); // Added Status field.

try    {
    // Calling insertOrReplaceEntity, instead of insertOrMergeEntity as shown,
    // would simply replace the entity with PartitionKey "tasksSeattle" and RowKey "1".
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

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="4d70f-156">Recuperare una singola entità</span><span class="sxs-lookup"><span data-stu-id="4d70f-156">Retrieve a single entity</span></span>
<span data-ttu-id="4d70f-157">Il metodo **TableRestProxy->getEntity** consente di recuperare una singola entità eseguendo una query su `PartitionKey` e `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="4d70f-157">The **TableRestProxy->getEntity** method allows you to retrieve a single entity by querying for its `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="4d70f-158">Nell'esempio seguente la chiave di partizione `tasksSeattle` e la chiave di riga `1` vengono passate al metodo **getEntity**.</span><span class="sxs-lookup"><span data-stu-id="4d70f-158">In the example below, the partition key `tasksSeattle` and row key `1` are passed to the **getEntity** method.</span></span>

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

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="4d70f-159">Recuperare tutte le entità di una partizione</span><span class="sxs-lookup"><span data-stu-id="4d70f-159">Retrieve all entities in a partition</span></span>
<span data-ttu-id="4d70f-160">Le query di entità vengono create usando i filtri. Per altre informazioni, vedere [Querying Tables and Entities][filters] (Query di tabelle ed entità).</span><span class="sxs-lookup"><span data-stu-id="4d70f-160">Entity queries are constructed using filters (for more information, see [Querying Tables and Entities][filters]).</span></span> <span data-ttu-id="4d70f-161">Per recuperare tutte le entità in una partizione usare il filtro "PartitionKey eq *partition_name*".</span><span class="sxs-lookup"><span data-stu-id="4d70f-161">To retrieve all entities in partition, use the filter "PartitionKey eq *partition_name*".</span></span> <span data-ttu-id="4d70f-162">Nell'esempio seguente viene illustrato come recuperare tutte le entità nella partizione `tasksSeattle` passando un filtro al metodo **queryEntities** .</span><span class="sxs-lookup"><span data-stu-id="4d70f-162">The following example shows how to retrieve all entities in the `tasksSeattle` partition by passing a filter to the **queryEntities** method.</span></span>

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

## <a name="retrieve-a-subset-of-entities-in-a-partition"></a><span data-ttu-id="4d70f-163">Recuperare un subset di entità in una partizione</span><span class="sxs-lookup"><span data-stu-id="4d70f-163">Retrieve a subset of entities in a partition</span></span>
<span data-ttu-id="4d70f-164">Lo stesso modello applicato nell'esempio precedente può essere usato per recuperare un subset di entità in una partizione.</span><span class="sxs-lookup"><span data-stu-id="4d70f-164">The same pattern used in the previous example can be used to retrieve any subset of entities in a partition.</span></span> <span data-ttu-id="4d70f-165">Il subset di entità recuperato viene determinato dal filtro usato. Per altre informazioni, vedere [Querying Tables and Entities][filters] (Query di tabelle ed entità). L'esempio seguente illustra come usare un filtro per recuperare tutte le entità con un valore `Location` specifico e un valore `DueDate` precedente a una data specificata.</span><span class="sxs-lookup"><span data-stu-id="4d70f-165">The subset of entities you retrieve are determined by the filter you use (for more information, see [Querying Tables and Entities][filters]).The following example shows how to use a filter to retrieve all entities with a specific `Location` and a `DueDate` less than a specified date.</span></span>

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

## <a name="retrieve-a-subset-of-entity-properties"></a><span data-ttu-id="4d70f-166">Recuperare un subset di proprietà di entità</span><span class="sxs-lookup"><span data-stu-id="4d70f-166">Retrieve a subset of entity properties</span></span>
<span data-ttu-id="4d70f-167">È possibile recuperare un subset di proprietà di entità eseguendo una query.</span><span class="sxs-lookup"><span data-stu-id="4d70f-167">A query can retrieve a subset of entity properties.</span></span> <span data-ttu-id="4d70f-168">Questa tecnica, denominata *proiezione*, consente di ridurre la larghezza di banda e di migliorare le prestazioni della query, in particolare per entità di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="4d70f-168">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="4d70f-169">Per specificare la proprietà da recuperare, passare il nome della proprietà al metodo **Query->addSelectField**.</span><span class="sxs-lookup"><span data-stu-id="4d70f-169">To specify a property to be retrieved, pass the name of the property to the **Query->addSelectField** method.</span></span> <span data-ttu-id="4d70f-170">Per aggiungere altre proprietà, è possibile chiamare questo metodo più volte.</span><span class="sxs-lookup"><span data-stu-id="4d70f-170">You can call this method multiple times to add more properties.</span></span> <span data-ttu-id="4d70f-171">Dopo l'esecuzione di **TableRestProxy->queryEntities**, per le entità restituite saranno presenti solo le proprietà selezionate.</span><span class="sxs-lookup"><span data-stu-id="4d70f-171">After executing **TableRestProxy->queryEntities**, the returned entities will only have the selected properties.</span></span> <span data-ttu-id="4d70f-172">Se si desidera restituire un subset di entità di tabella, utilizzare un filtro come illustrato nelle query precedenti.</span><span class="sxs-lookup"><span data-stu-id="4d70f-172">(If you want to return a subset of Table entities, use a filter as shown in the queries above.)</span></span>

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

// All entities in the table are returned, regardless of whether
// they have the Description field.
// To limit the results returned, use a filter.
$entities = $result->getEntities();

foreach($entities as $entity){
    $description = $entity->getProperty("Description")->getValue();
    echo $description."<br />";
}
```

## <a name="update-an-entity"></a><span data-ttu-id="4d70f-173">Aggiornare un'entità</span><span class="sxs-lookup"><span data-stu-id="4d70f-173">Update an entity</span></span>
<span data-ttu-id="4d70f-174">È possibile aggiornare un'entità esistente usando i metodi **Entity->setProperty** e **Entity->addProperty** sull'entità e quindi chiamando **TableRestProxy->updateEntity**.</span><span class="sxs-lookup"><span data-stu-id="4d70f-174">An existing entity can be updated by using the **Entity->setProperty** and **Entity->addProperty** methods on the entity, and then calling **TableRestProxy->updateEntity**.</span></span> <span data-ttu-id="4d70f-175">Nell'esempio seguente viene recuperata un'entità, modificata una proprietà, rimossa un'altra proprietà e aggiunta una nuova proprietà.</span><span class="sxs-lookup"><span data-stu-id="4d70f-175">The following example retrieves an entity, modifies one property, removes another property, and adds a new property.</span></span> <span data-ttu-id="4d70f-176">Si noti che per rimuovere una proprietà, è necessario impostarne il valore su **Null**.</span><span class="sxs-lookup"><span data-stu-id="4d70f-176">Note that you can remove a property by setting its value to **null**.</span></span>

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

## <a name="delete-an-entity"></a><span data-ttu-id="4d70f-177">Eliminare un'entità</span><span class="sxs-lookup"><span data-stu-id="4d70f-177">Delete an entity</span></span>
<span data-ttu-id="4d70f-178">Per eliminare un'entità passare il nome della tabella e le chiavi `PartitionKey` e `RowKey` dell'entità al metodo **TableRestProxy->deleteEntity**.</span><span class="sxs-lookup"><span data-stu-id="4d70f-178">To delete an entity, pass the table name, and the entity's `PartitionKey` and `RowKey` to the **TableRestProxy->deleteEntity** method.</span></span>

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

<span data-ttu-id="4d70f-179">Si noti che per effettuare controlli di concorrenza è possibile impostare il valore Etag per un'entità da eliminare usando il metodo **DeleteEntityOptions->setEtag** e passando l'oggetto **DeleteEntityOptions** a **deleteEntity** come quarto parametro.</span><span class="sxs-lookup"><span data-stu-id="4d70f-179">Note that for concurrency checks, you can set the Etag for an entity to be deleted by using the **DeleteEntityOptions->setEtag** method and passing the **DeleteEntityOptions** object to **deleteEntity** as a fourth parameter.</span></span>

## <a name="batch-table-operations"></a><span data-ttu-id="4d70f-180">Operazioni batch su tabella</span><span class="sxs-lookup"><span data-stu-id="4d70f-180">Batch table operations</span></span>
<span data-ttu-id="4d70f-181">Il metodo **TableRestProxy->batch** consente di eseguire più operazioni in una sola richiesta.</span><span class="sxs-lookup"><span data-stu-id="4d70f-181">The **TableRestProxy->batch** method allows you to execute multiple operations in a single request.</span></span> <span data-ttu-id="4d70f-182">In questo caso è necessario aggiungere le operazioni all'oggetto **BatchRequest** e quindi passare l'oggetto **BatchRequest** al metodo **TableRestProxy->batch**.</span><span class="sxs-lookup"><span data-stu-id="4d70f-182">The pattern here involves adding operations to **BatchRequest** object and then passing the **BatchRequest** object to the **TableRestProxy->batch** method.</span></span> <span data-ttu-id="4d70f-183">Per aggiungere un'operazione all'oggetto **BatchRequest** , è possibile chiamare più volte uno dei metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="4d70f-183">To add an operation to a **BatchRequest** object, you can call any of the following methods multiple times:</span></span>

* <span data-ttu-id="4d70f-184">**addInsertEntity** (per aggiungere un'operazione insertEntity)</span><span class="sxs-lookup"><span data-stu-id="4d70f-184">**addInsertEntity** (adds an insertEntity operation)</span></span>
* <span data-ttu-id="4d70f-185">**addUpdateEntity** (per aggiungere un'operazione updateEntity)</span><span class="sxs-lookup"><span data-stu-id="4d70f-185">**addUpdateEntity** (adds an updateEntity operation)</span></span>
* <span data-ttu-id="4d70f-186">**addMergeEntity** (per aggiungere un'operazione mergeEntity)</span><span class="sxs-lookup"><span data-stu-id="4d70f-186">**addMergeEntity** (adds a mergeEntity operation)</span></span>
* <span data-ttu-id="4d70f-187">**addInsertOrReplaceEntity** (per aggiungere un'operazione insertOrReplaceEntity)</span><span class="sxs-lookup"><span data-stu-id="4d70f-187">**addInsertOrReplaceEntity** (adds an insertOrReplaceEntity operation)</span></span>
* <span data-ttu-id="4d70f-188">**addInsertOrMergeEntity** (per aggiungere un'operazione insertOrMergeEntity)</span><span class="sxs-lookup"><span data-stu-id="4d70f-188">**addInsertOrMergeEntity** (adds an insertOrMergeEntity operation)</span></span>
* <span data-ttu-id="4d70f-189">**addDeleteEntity** (per aggiungere un'operazione deleteEntity)</span><span class="sxs-lookup"><span data-stu-id="4d70f-189">**addDeleteEntity** (adds a deleteEntity operation)</span></span>

<span data-ttu-id="4d70f-190">L'esempio seguente illustra come eseguire le operazioni **insertEntity** e **deleteEntity** in una sola richiesta:</span><span class="sxs-lookup"><span data-stu-id="4d70f-190">The following example shows how to execute **insertEntity** and **deleteEntity** operations in a single request:</span></span>

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

// Add operation to list of batch operations.
$operations->addInsertEntity("mytable", $entity1);

// Add operation to list of batch operations.
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

<span data-ttu-id="4d70f-191">Per altre informazioni su operazioni batch su tabelle, vedere [Performing Entity Group Transactions][entity-group-transactions] (Esecuzione di transazioni di gruppi di entità).</span><span class="sxs-lookup"><span data-stu-id="4d70f-191">For more information about batching Table operations, see [Performing Entity Group Transactions][entity-group-transactions].</span></span>

## <a name="delete-a-table"></a><span data-ttu-id="4d70f-192">Eliminare una tabella</span><span class="sxs-lookup"><span data-stu-id="4d70f-192">Delete a table</span></span>
<span data-ttu-id="4d70f-193">Infine, per eliminare una tabella, passare il nome della tabella al metodo **TableRestProxy->deleteTable**.</span><span class="sxs-lookup"><span data-stu-id="4d70f-193">Finally, to delete a table, pass the table name to the **TableRestProxy->deleteTable** method.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="4d70f-194">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4d70f-194">Next steps</span></span>
<span data-ttu-id="4d70f-195">A questo punto, dopo avere appreso le nozioni di base del servizio tabelle di Azure, usare i collegamenti seguenti per altre informazioni su attività di archiviazione più complesse.</span><span class="sxs-lookup"><span data-stu-id="4d70f-195">Now that you've learned the basics of the Azure Table service, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="4d70f-196">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) è un'app autonoma gratuita di Microsoft che consente di rappresentare facilmente dati di Archiviazione di Azure in Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="4d70f-196">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

* <span data-ttu-id="4d70f-197">[Centro sviluppatori PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="4d70f-197">[PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://php.net/require_once
[table-service-timeouts]: http://msdn.microsoft.com/library/azure/dd894042.aspx

[table-data-model]: http://msdn.microsoft.com/library/azure/dd179338.aspx
[filters]: http://msdn.microsoft.com/library/azure/dd894031.aspx
[entity-group-transactions]: http://msdn.microsoft.com/library/azure/dd894038.aspx
