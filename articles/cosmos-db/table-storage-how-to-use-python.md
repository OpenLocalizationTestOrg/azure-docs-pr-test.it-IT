---
title: Come usare l'archiviazione tabelle di Azure con Python | Microsoft Docs
description: Archiviare dati non strutturati nel cloud con il servizio di archiviazione tabelle di Azure, ovvero un archivio dati NoSQL.
services: cosmos-db
documentationcenter: python
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: 7ddb9f3e-4e6d-4103-96e6-f0351d69a17b
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/16/2017
ms.author: mimig
ms.openlocfilehash: 0c46f04786ba4b62bd7ca22c5e25643123e6e136
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-table-storage-in-python"></a><span data-ttu-id="abc44-103">Come usare l'archiviazione tabelle in Python</span><span class="sxs-lookup"><span data-stu-id="abc44-103">How to use Table storage in Python</span></span>

[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

<span data-ttu-id="abc44-104">Questa guida illustra come eseguire scenari comuni di archiviazione tabelle di Azure in Python usando l'[SDK di Archiviazione di Microsoft Azure per Python](https://github.com/Azure/azure-storage-python).</span><span class="sxs-lookup"><span data-stu-id="abc44-104">This guide shows you how to perform common Azure Table storage scenarios in Python using the [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="abc44-105">Gli scenari presentati includono la creazione e l'eliminazione di una tabella, oltre che l'inserimento di entità e l'esecuzione di query sulle entità.</span><span class="sxs-lookup"><span data-stu-id="abc44-105">The scenarios covered include creating and deleting a table, and inserting and querying entities.</span></span>

<span data-ttu-id="abc44-106">Mentre si lavora agli scenari di questa esercitazione, è possibile vedere le [informazioni di riferimento sull'API dell'SDK di Archiviazione di Azure per Python](https://azure-storage.readthedocs.io/en/latest/index.html).</span><span class="sxs-lookup"><span data-stu-id="abc44-106">While working through the scenarios in this tutorial, you may wish to refer to the [Azure Storage SDK for Python API reference](https://azure-storage.readthedocs.io/en/latest/index.html).</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="install-the-azure-storage-sdk-for-python"></a><span data-ttu-id="abc44-107">Installare l'SDK di Archiviazione di Azure per Python</span><span class="sxs-lookup"><span data-stu-id="abc44-107">Install the Azure Storage SDK for Python</span></span>

<span data-ttu-id="abc44-108">Dopo aver creato un account di archiviazione, il passaggio successivo consiste nell'[installare l'SDK di Archiviazione di Microsoft Azure per Python](https://github.com/Azure/azure-storage-python).</span><span class="sxs-lookup"><span data-stu-id="abc44-108">Once you've created a storage account, your next step is to install the [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="abc44-109">Per informazioni dettagliate sull'installazione dell'SDK, vedere il file [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) nell'archivio relativo all'SDK di Archiviazione per Python su GitHub.</span><span class="sxs-lookup"><span data-stu-id="abc44-109">For details on installing the SDK, refer to the [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) file in the Storage SDK for Python repository on GitHub.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="abc44-110">Creare una tabella</span><span class="sxs-lookup"><span data-stu-id="abc44-110">Create a table</span></span>

<span data-ttu-id="abc44-111">Per usare il servizio tabelle di Azure in Python, è necessario importare il modulo [TableService][py_TableService].</span><span class="sxs-lookup"><span data-stu-id="abc44-111">To work with the Azure Table service in Python, you must import the [TableService][py_TableService] module.</span></span> <span data-ttu-id="abc44-112">Poiché si useranno entità tabella, è necessaria anche la classe [Entity][py_Entity].</span><span class="sxs-lookup"><span data-stu-id="abc44-112">Since you'll be working with Table entities, you also need the [Entity][py_Entity] class.</span></span> <span data-ttu-id="abc44-113">Aggiungere il codice seguente nella parte iniziale del file Python per importare entrambi gli elementi:</span><span class="sxs-lookup"><span data-stu-id="abc44-113">Add this code near the top your Python file to import both:</span></span>

```python
from azure.storage.table import TableService, Entity
```

<span data-ttu-id="abc44-114">Creare un oggetto [TableService][py_TableService] passando il nome dell'account di archiviazione e la chiave dell'account.</span><span class="sxs-lookup"><span data-stu-id="abc44-114">Create a [TableService][py_TableService] object, passing in your storage account name and account key.</span></span> <span data-ttu-id="abc44-115">Sostituire `myaccount` e `mykey` con il nome e la chiave dell'account e chiamare [create_table][py_create_table] per creare la tabella in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="abc44-115">Replace `myaccount` and `mykey` with your account name and key, and call [create_table][py_create_table] to create the table in Azure Storage.</span></span>

```python
table_service = TableService(account_name='myaccount', account_key='mykey')

table_service.create_table('tasktable')
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="abc44-116">Aggiungere un'entità a una tabella</span><span class="sxs-lookup"><span data-stu-id="abc44-116">Add an entity to a table</span></span>

<span data-ttu-id="abc44-117">Per aggiungere un'entità, creare innanzitutto un oggetto che rappresenta l'entità, quindi passare l'oggetto al metodo [TableService][py_TableService].[insert_entity][py_insert_entity].</span><span class="sxs-lookup"><span data-stu-id="abc44-117">To add an entity, you first create an object that represents your entity, then pass the object to the [TableService][py_TableService].[insert_entity][py_insert_entity] method.</span></span> <span data-ttu-id="abc44-118">L'oggetto entità può essere un dizionario o un oggetto di tipo [Entity][py_Entity] e definisce i nomi e i valori delle proprietà dell'entità.</span><span class="sxs-lookup"><span data-stu-id="abc44-118">The entity object can be a dictionary or an object of type [Entity][py_Entity], and defines your entity's property names and values.</span></span> <span data-ttu-id="abc44-119">Ogni entità deve includere le proprietà [PartitionKey e RowKey](#partitionkey-and-rowkey) necessarie, oltre a tutte le altre proprietà definite per l'entità.</span><span class="sxs-lookup"><span data-stu-id="abc44-119">Every entity must include the required [PartitionKey and RowKey](#partitionkey-and-rowkey) properties, in addition to any other properties you define for the entity.</span></span>

<span data-ttu-id="abc44-120">Questo esempio crea un oggetto dizionario che rappresenta un'entità e quindi passa l'oggetto al metodo [insert_entity][py_insert_entity] per aggiungerlo alla tabella:</span><span class="sxs-lookup"><span data-stu-id="abc44-120">This example creates a dictionary object representing an entity, then passes it to the [insert_entity][py_insert_entity] method to add it to the table:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out the trash', 'priority' : 200}
table_service.insert_entity('tasktable', task)
```

<span data-ttu-id="abc44-121">Questo esempio crea un oggetto [Entity][py_Entity] e quindi lo passa al metodo [insert_entity][py_insert_entity] per aggiungerlo alla tabella:</span><span class="sxs-lookup"><span data-stu-id="abc44-121">This example creates an [Entity][py_Entity] object, then passes it to the [insert_entity][py_insert_entity] method to add it to the table:</span></span>

```python
task = Entity()
task.PartitionKey = 'tasksSeattle'
task.RowKey = '002'
task.description = 'Wash the car'
task.priority = 100
table_service.insert_entity('tasktable', task)
```

### <a name="partitionkey-and-rowkey"></a><span data-ttu-id="abc44-122">PartitionKey e RowKey</span><span class="sxs-lookup"><span data-stu-id="abc44-122">PartitionKey and RowKey</span></span>

<span data-ttu-id="abc44-123">È necessario specificare entrambe le proprietà **PartitionKey** e **RowKey** per ogni entità.</span><span class="sxs-lookup"><span data-stu-id="abc44-123">You must specify both a **PartitionKey** and a **RowKey** property for every entity.</span></span> <span data-ttu-id="abc44-124">Si tratta degli identificatori univoci delle entità, che insieme formano la chiave primaria di un'entità.</span><span class="sxs-lookup"><span data-stu-id="abc44-124">These are the unique identifiers of your entities, as together they form the primary key of an entity.</span></span> <span data-ttu-id="abc44-125">È possibile eseguire query usando questi valori in modo molto più rapido rispetto a quanto è possibile fare su qualsiasi altra proprietà dell'entità, perché solo queste proprietà sono indicizzate.</span><span class="sxs-lookup"><span data-stu-id="abc44-125">You can query using these values much faster than you can query any other entity properties because only these properties are indexed.</span></span>

<span data-ttu-id="abc44-126">Il servizio tabelle usa **PartitionKey** per distribuire in modo intelligente le entità della tabella nei nodi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="abc44-126">The Table service uses **PartitionKey** to intelligently distribute table entities across storage nodes.</span></span> <span data-ttu-id="abc44-127">Le entità con la stessa proprietà **PartitionKey** vengono archiviate nello stesso nodo.</span><span class="sxs-lookup"><span data-stu-id="abc44-127">Entities that have the same  **PartitionKey** are stored on the same node.</span></span> <span data-ttu-id="abc44-128">**RowKey** è l'ID univoco dell'entità all'interno della partizione a cui appartiene.</span><span class="sxs-lookup"><span data-stu-id="abc44-128">**RowKey** is the unique ID of the entity within the partition it belongs to.</span></span>

## <a name="update-an-entity"></a><span data-ttu-id="abc44-129">Aggiornare un'entità</span><span class="sxs-lookup"><span data-stu-id="abc44-129">Update an entity</span></span>

<span data-ttu-id="abc44-130">Per aggiornare tutti i valori delle proprietà di un'entità, chiamare il metodo [update_entity][py_update_entity].</span><span class="sxs-lookup"><span data-stu-id="abc44-130">To update all of an entity's property values, call the [update_entity][py_update_entity] method.</span></span> <span data-ttu-id="abc44-131">Questo esempio mostra come sostituire un'entità esistente con una versione aggiornata:</span><span class="sxs-lookup"><span data-stu-id="abc44-131">This example shows how to replace an existing entity with an updated version:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out the garbage', 'priority' : 250}
table_service.update_entity('tasktable', task)
```

<span data-ttu-id="abc44-132">Se l'entità da aggiornare non esiste già, l'operazione di aggiornamento non riuscirà.</span><span class="sxs-lookup"><span data-stu-id="abc44-132">If the entity that is being updated doesn't already exist, then the update operation will fail.</span></span> <span data-ttu-id="abc44-133">Se si vuole archiviare un'entità indipendentemente dal fatto che esista o meno, usare [insert_or_replace_entity][py_insert_or_replace_entity].</span><span class="sxs-lookup"><span data-stu-id="abc44-133">If you want to store an entity whether it exists or not, use [insert_or_replace_entity][py_insert_or_replace_entity].</span></span> <span data-ttu-id="abc44-134">Nell'esempio seguente, la prima chiamata sostituirà l'entità esistente.</span><span class="sxs-lookup"><span data-stu-id="abc44-134">In the following example, the first call will replace the existing entity.</span></span> <span data-ttu-id="abc44-135">La seconda chiamata inserisce una nuova entità, perché nella tabella non c'è alcuna entità con le proprietà PartitionKey e RowKey specificate.</span><span class="sxs-lookup"><span data-stu-id="abc44-135">The second call will insert a new entity, since no entity with the specified PartitionKey and RowKey exists in the table.</span></span>

```python
# Replace the entity created earlier
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out the garbage again', 'priority' : 250}
table_service.insert_or_replace_entity('tasktable', task)

# Insert a new entity
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '003', 'description' : 'Buy detergent', 'priority' : 300}
table_service.insert_or_replace_entity('tasktable', task)
```

> [!TIP]
> <span data-ttu-id="abc44-136">Il metodo [update_entity][py_update_entity] sostituisce tutte le proprietà e i valori di un'entità esistente e può anche essere usato per rimuovere le proprietà da un'entità esistente.</span><span class="sxs-lookup"><span data-stu-id="abc44-136">The [update_entity][py_update_entity] method replaces all properties and values of an existing entity, which you can also use to remove properties from an existing entity.</span></span> <span data-ttu-id="abc44-137">È possibile usare il metodo [merge_entity][py_merge_entity] per aggiornare un'entità esistente con i valori delle proprietà nuovi o modificati senza sostituire completamente l'entità.</span><span class="sxs-lookup"><span data-stu-id="abc44-137">You can use the [merge_entity][py_merge_entity] method to update an existing entity with new or modified property values without completely replacing the entity.</span></span>

## <a name="modify-multiple-entities"></a><span data-ttu-id="abc44-138">Modificare più entità</span><span class="sxs-lookup"><span data-stu-id="abc44-138">Modify multiple entities</span></span>

<span data-ttu-id="abc44-139">Per garantire l'elaborazione atomica delle richieste da parte del servizio tabelle, è possibile inviare più operazioni insieme in un batch.</span><span class="sxs-lookup"><span data-stu-id="abc44-139">To ensure the atomic processing of a request by the Table service, you can submit multiple operations together in a batch.</span></span> <span data-ttu-id="abc44-140">Usare prima di tutto la classe [TableBatch][py_TableBatch] per aggiungere più operazioni a un singolo batch.</span><span class="sxs-lookup"><span data-stu-id="abc44-140">First, use the [TableBatch][py_TableBatch] class to add multiple operations to a single batch.</span></span> <span data-ttu-id="abc44-141">Chiamare quindi [TableService][py_TableService].[commit_batch][py_commit_batch] per inviare le operazioni in un'operazione atomica.</span><span class="sxs-lookup"><span data-stu-id="abc44-141">Next, call [TableService][py_TableService].[commit_batch][py_commit_batch] to submit the operations in an atomic operation.</span></span> <span data-ttu-id="abc44-142">Tutte le entità da modificare in batch devono trovarsi nella stessa partizione.</span><span class="sxs-lookup"><span data-stu-id="abc44-142">All entities to be modified in batch must be in the same partition.</span></span>

<span data-ttu-id="abc44-143">Questo esempio aggiunge due entità in un batch:</span><span class="sxs-lookup"><span data-stu-id="abc44-143">This example adds two entities together in a batch:</span></span>

```python
from azure.storage.table import TableBatch
batch = TableBatch()
task004 = {'PartitionKey': 'tasksSeattle', 'RowKey': '004', 'description' : 'Go grocery shopping', 'priority' : 400}
task005 = {'PartitionKey': 'tasksSeattle', 'RowKey': '005', 'description' : 'Clean the bathroom', 'priority' : 100}
batch.insert_entity(task004)
batch.insert_entity(task005)
table_service.commit_batch('tasktable', batch)
```

<span data-ttu-id="abc44-144">I batch possono essere usati anche con la sintassi di gestione contesto:</span><span class="sxs-lookup"><span data-stu-id="abc44-144">Batches can also be used with the context manager syntax:</span></span>

```python
task006 = {'PartitionKey': 'tasksSeattle', 'RowKey': '006', 'description' : 'Go grocery shopping', 'priority' : 400}
task007 = {'PartitionKey': 'tasksSeattle', 'RowKey': '007', 'description' : 'Clean the bathroom', 'priority' : 100}

with table_service.batch('tasktable') as batch:
    batch.insert_entity(task006)
    batch.insert_entity(task007)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="abc44-145">Eseguire una query su un'entità</span><span class="sxs-lookup"><span data-stu-id="abc44-145">Query for an entity</span></span>

<span data-ttu-id="abc44-146">Per eseguire una query per un'entità in una tabella, passare le relative proprietà PartitionKey e RowKey al metodo [TableService][py_TableService].[get_entity][py_get_entity].</span><span class="sxs-lookup"><span data-stu-id="abc44-146">To query for an entity in a table, pass its PartitionKey and RowKey to the [TableService][py_TableService].[get_entity][py_get_entity] method.</span></span>

```python
task = table_service.get_entity('tasktable', 'tasksSeattle', '001')
print(task.description)
print(task.priority)
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="abc44-147">Eseguire query su un set di entità</span><span class="sxs-lookup"><span data-stu-id="abc44-147">Query a set of entities</span></span>

<span data-ttu-id="abc44-148">È possibile eseguire query per un set di entità specificando una stringa di filtro con il parametro **filter**.</span><span class="sxs-lookup"><span data-stu-id="abc44-148">You can query for a set of entities by supplying a filter string with the **filter** parameter.</span></span> <span data-ttu-id="abc44-149">Questo esempio trova tutte le attività di Seattle applicando un filtro a PartitionKey:</span><span class="sxs-lookup"><span data-stu-id="abc44-149">This example finds all tasks in Seattle by applying a filter on PartitionKey:</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'")
for task in tasks:
    print(task.description)
    print(task.priority)
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="abc44-150">Eseguire query su un subset di proprietà di entità</span><span class="sxs-lookup"><span data-stu-id="abc44-150">Query a subset of entity properties</span></span>

<span data-ttu-id="abc44-151">È anche possibile limitare le proprietà restituite per ogni entità in una query.</span><span class="sxs-lookup"><span data-stu-id="abc44-151">You can also restrict which properties are returned for each entity in a query.</span></span> <span data-ttu-id="abc44-152">Questa tecnica, denominata *proiezione*, consente di ridurre la larghezza di banda e di migliorare le prestazioni di query, in particolare per entità o set di risultati di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="abc44-152">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities or result sets.</span></span> <span data-ttu-id="abc44-153">Usare il parametro **select** e passare i nomi delle proprietà da restituire al client.</span><span class="sxs-lookup"><span data-stu-id="abc44-153">Use the **select** parameter and pass the names of the properties you want returned to the client.</span></span>

<span data-ttu-id="abc44-154">La query nel codice seguente restituisce solo le descrizioni delle entità nella tabella.</span><span class="sxs-lookup"><span data-stu-id="abc44-154">The query in the following code returns only the descriptions of entities in the table.</span></span>

> [!NOTE]
> <span data-ttu-id="abc44-155">Il frammento di codice seguente funziona solo in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="abc44-155">The following snippet works only against the Azure Storage.</span></span> <span data-ttu-id="abc44-156">Non è supportato dall'emulatore di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="abc44-156">It is not supported by the storage emulator.</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'", select='description')
for task in tasks:
    print(task.description)
```

## <a name="delete-an-entity"></a><span data-ttu-id="abc44-157">Eliminare un'entità</span><span class="sxs-lookup"><span data-stu-id="abc44-157">Delete an entity</span></span>

<span data-ttu-id="abc44-158">Eliminare un'entità passando le relative proprietà PartitionKey e RowKey al metodo [delete_entity][py_delete_entity].</span><span class="sxs-lookup"><span data-stu-id="abc44-158">Delete an entity by passing its PartitionKey and RowKey to the [delete_entity][py_delete_entity] method.</span></span>

```python
table_service.delete_entity('tasktable', 'tasksSeattle', '001')
```

## <a name="delete-a-table"></a><span data-ttu-id="abc44-159">Eliminare una tabella</span><span class="sxs-lookup"><span data-stu-id="abc44-159">Delete a table</span></span>

<span data-ttu-id="abc44-160">Se una tabella o una delle entità al suo interno non è più necessaria, chiamare il metodo [delete_table][py_delete_table] per eliminare definitivamente la tabella da Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="abc44-160">If you no longer need a table or any of the entities within it, call the [delete_table][py_delete_table] method to permanently delete the table from Azure Storage.</span></span>

```python
table_service.delete_table('tasktable')
```

## <a name="next-steps"></a><span data-ttu-id="abc44-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="abc44-161">Next steps</span></span>

* [<span data-ttu-id="abc44-162">Informazioni di riferimento sull'API dell'SDK di Archiviazione di Azure per Python</span><span class="sxs-lookup"><span data-stu-id="abc44-162">Azure Storage SDK for Python API reference</span></span>](https://azure-storage.readthedocs.io/en/latest/index.html)
* [<span data-ttu-id="abc44-163">SDK di Archiviazione di Azure per Python</span><span class="sxs-lookup"><span data-stu-id="abc44-163">Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)
* [<span data-ttu-id="abc44-164">Centro per sviluppatori Python</span><span class="sxs-lookup"><span data-stu-id="abc44-164">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* <span data-ttu-id="abc44-165">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md): un'applicazione gratuita multipiattaforma per lavorare in modo visivo con i dati di Archiviazione di Azure in Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="abc44-165">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md): A free, cross-platform application for working visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

[py_commit_batch]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.commit_batch
[py_create_table]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.create_table
[py_delete_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.delete_entity
[py_delete_table]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.delete_table
[py_Entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.models.html#azure.storage.table.models.Entity
[py_get_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.get_entity
[py_insert_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.insert_entity
[py_insert_or_replace_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.insert_or_replace_entity
[py_merge_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.merge_entity
[py_update_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.update_entity
[py_TableService]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html
[py_TableBatch]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tablebatch.html#azure.storage.table.tablebatch.TableBatch
