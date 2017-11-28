---
title: aaaHow toouse archiviazione tabelle di Azure con Python | Documenti Microsoft
description: Archiviare dati strutturati in un cloud di hello tramite l'archiviazione tabelle di Azure, un archivio dati NoSQL.
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
ms.openlocfilehash: 3382fcd5667a93d5533b5f8fad1d3d1c27f23482
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-in-python"></a><span data-ttu-id="087c5-103">Come toouse archiviazione tabelle di Python</span><span class="sxs-lookup"><span data-stu-id="087c5-103">How toouse Table storage in Python</span></span>

[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

<span data-ttu-id="087c5-104">Questa guida viene spiegato come tooperform tabella Azure storage scenari comuni in Python mediante hello [Microsoft Azure Storage SDK per Python](https://github.com/Azure/azure-storage-python).</span><span class="sxs-lookup"><span data-stu-id="087c5-104">This guide shows you how tooperform common Azure Table storage scenarios in Python using hello [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="087c5-105">scenari di Hello trattati includono la creazione e l'eliminazione di una tabella, inserimento e query su entità.</span><span class="sxs-lookup"><span data-stu-id="087c5-105">hello scenarios covered include creating and deleting a table, and inserting and querying entities.</span></span>

<span data-ttu-id="087c5-106">Mentre vengono elaborati i scenari di hello in questa esercitazione, è preferibile toorefer toohello [Azure Storage SDK per Python API reference](https://azure-storage.readthedocs.io/en/latest/index.html).</span><span class="sxs-lookup"><span data-stu-id="087c5-106">While working through hello scenarios in this tutorial, you may wish toorefer toohello [Azure Storage SDK for Python API reference](https://azure-storage.readthedocs.io/en/latest/index.html).</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="install-hello-azure-storage-sdk-for-python"></a><span data-ttu-id="087c5-107">Installare hello Azure Storage SDK per Python</span><span class="sxs-lookup"><span data-stu-id="087c5-107">Install hello Azure Storage SDK for Python</span></span>

<span data-ttu-id="087c5-108">Dopo aver creato un account di archiviazione, il passaggio successivo è hello tooinstall [Microsoft Azure Storage SDK per Python](https://github.com/Azure/azure-storage-python).</span><span class="sxs-lookup"><span data-stu-id="087c5-108">Once you've created a storage account, your next step is tooinstall hello [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="087c5-109">Per informazioni dettagliate sull'installazione hello SDK, vedere toohello [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) file in hello Azure Storage SDK per il repository di Python su GitHub.</span><span class="sxs-lookup"><span data-stu-id="087c5-109">For details on installing hello SDK, refer toohello [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) file in hello Storage SDK for Python repository on GitHub.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="087c5-110">Creare una tabella</span><span class="sxs-lookup"><span data-stu-id="087c5-110">Create a table</span></span>

<span data-ttu-id="087c5-111">toowork con hello servizio tabelle di Azure di Python, è necessario importare hello [TableService] [ py_TableService] modulo.</span><span class="sxs-lookup"><span data-stu-id="087c5-111">toowork with hello Azure Table service in Python, you must import hello [TableService][py_TableService] module.</span></span> <span data-ttu-id="087c5-112">Poiché lavorerà con entità di tabella, è necessario anche hello [entità] [ py_Entity] classe.</span><span class="sxs-lookup"><span data-stu-id="087c5-112">Since you'll be working with Table entities, you also need hello [Entity][py_Entity] class.</span></span> <span data-ttu-id="087c5-113">Aggiungere questo codice superiore hello il file Python tooimport entrambi:</span><span class="sxs-lookup"><span data-stu-id="087c5-113">Add this code near hello top your Python file tooimport both:</span></span>

```python
from azure.storage.table import TableService, Entity
```

<span data-ttu-id="087c5-114">Creare un oggetto [TableService][py_TableService] passando il nome dell'account di archiviazione e la chiave dell'account.</span><span class="sxs-lookup"><span data-stu-id="087c5-114">Create a [TableService][py_TableService] object, passing in your storage account name and account key.</span></span> <span data-ttu-id="087c5-115">Sostituire `myaccount` e `mykey` con il nome di account e una chiave e una chiamata [create_table] [ py_create_table] tabella hello toocreate in archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="087c5-115">Replace `myaccount` and `mykey` with your account name and key, and call [create_table][py_create_table] toocreate hello table in Azure Storage.</span></span>

```python
table_service = TableService(account_name='myaccount', account_key='mykey')

table_service.create_table('tasktable')
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="087c5-116">Aggiungere una tabella tooa entità</span><span class="sxs-lookup"><span data-stu-id="087c5-116">Add an entity tooa table</span></span>

<span data-ttu-id="087c5-117">tooadd un'entità, creare innanzitutto un oggetto che rappresenta l'entità, quindi passare hello oggetto toohello [TableService][py_TableService].[ insert_entity] [ py_insert_entity] metodo.</span><span class="sxs-lookup"><span data-stu-id="087c5-117">tooadd an entity, you first create an object that represents your entity, then pass hello object toohello [TableService][py_TableService].[insert_entity][py_insert_entity] method.</span></span> <span data-ttu-id="087c5-118">oggetto entità Hello può essere un dizionario o un oggetto di tipo [entità][py_Entity]e definisce i nomi delle proprietà e i valori dell'entità.</span><span class="sxs-lookup"><span data-stu-id="087c5-118">hello entity object can be a dictionary or an object of type [Entity][py_Entity], and defines your entity's property names and values.</span></span> <span data-ttu-id="087c5-119">Ogni entità devono includere hello necessario [PartitionKey e RowKey](#partitionkey-and-rowkey) proprietà, in aggiunta tooany altre proprietà è possibile definire per entità hello.</span><span class="sxs-lookup"><span data-stu-id="087c5-119">Every entity must include hello required [PartitionKey and RowKey](#partitionkey-and-rowkey) properties, in addition tooany other properties you define for hello entity.</span></span>

<span data-ttu-id="087c5-120">Questo esempio viene creato un oggetto dizionario che rappresenta un'entità, quindi passarlo toohello [insert_entity] [ py_insert_entity] metodo tooadd è toohello tabella:</span><span class="sxs-lookup"><span data-stu-id="087c5-120">This example creates a dictionary object representing an entity, then passes it toohello [insert_entity][py_insert_entity] method tooadd it toohello table:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello trash', 'priority' : 200}
table_service.insert_entity('tasktable', task)
```

<span data-ttu-id="087c5-121">Questo esempio viene creato un [entità] [ py_Entity] dell'oggetto, quindi passarlo toohello [insert_entity] [ py_insert_entity] metodo tooadd è toohello tabella:</span><span class="sxs-lookup"><span data-stu-id="087c5-121">This example creates an [Entity][py_Entity] object, then passes it toohello [insert_entity][py_insert_entity] method tooadd it toohello table:</span></span>

```python
task = Entity()
task.PartitionKey = 'tasksSeattle'
task.RowKey = '002'
task.description = 'Wash hello car'
task.priority = 100
table_service.insert_entity('tasktable', task)
```

### <a name="partitionkey-and-rowkey"></a><span data-ttu-id="087c5-122">PartitionKey e RowKey</span><span class="sxs-lookup"><span data-stu-id="087c5-122">PartitionKey and RowKey</span></span>

<span data-ttu-id="087c5-123">È necessario specificare entrambe le proprietà **PartitionKey** e **RowKey** per ogni entità.</span><span class="sxs-lookup"><span data-stu-id="087c5-123">You must specify both a **PartitionKey** and a **RowKey** property for every entity.</span></span> <span data-ttu-id="087c5-124">Questi sono identificatori univoci di hello delle entità, come insieme formano una chiave primaria di hello di un'entità.</span><span class="sxs-lookup"><span data-stu-id="087c5-124">These are hello unique identifiers of your entities, as together they form hello primary key of an entity.</span></span> <span data-ttu-id="087c5-125">È possibile eseguire query usando questi valori in modo molto più rapido rispetto a quanto è possibile fare su qualsiasi altra proprietà dell'entità, perché solo queste proprietà sono indicizzate.</span><span class="sxs-lookup"><span data-stu-id="087c5-125">You can query using these values much faster than you can query any other entity properties because only these properties are indexed.</span></span>

<span data-ttu-id="087c5-126">servizio tabelle utilizza Hello **PartitionKey** toointelligently distribuire le entità di tabella in nodi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="087c5-126">hello Table service uses **PartitionKey** toointelligently distribute table entities across storage nodes.</span></span> <span data-ttu-id="087c5-127">Entità che dispongono di hello stesso **PartitionKey** vengono archiviati in hello stesso nodo.</span><span class="sxs-lookup"><span data-stu-id="087c5-127">Entities that have hello same  **PartitionKey** are stored on hello same node.</span></span> <span data-ttu-id="087c5-128">**RowKey** hello ID univoco dell'entità hello all'interno della partizione hello a cui appartiene.</span><span class="sxs-lookup"><span data-stu-id="087c5-128">**RowKey** is hello unique ID of hello entity within hello partition it belongs to.</span></span>

## <a name="update-an-entity"></a><span data-ttu-id="087c5-129">Aggiornare un'entità</span><span class="sxs-lookup"><span data-stu-id="087c5-129">Update an entity</span></span>

<span data-ttu-id="087c5-130">tooupdate tutti di valori di proprietà dell'entità, chiamare hello [update_entity] [ py_update_entity] metodo.</span><span class="sxs-lookup"><span data-stu-id="087c5-130">tooupdate all of an entity's property values, call hello [update_entity][py_update_entity] method.</span></span> <span data-ttu-id="087c5-131">Questo esempio viene illustrato come tooreplace un'entità esistente con una versione aggiornata:</span><span class="sxs-lookup"><span data-stu-id="087c5-131">This example shows how tooreplace an existing entity with an updated version:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage', 'priority' : 250}
table_service.update_entity('tasktable', task)
```

<span data-ttu-id="087c5-132">Se l'entità hello in corso di aggiornamento non esiste già, l'operazione di aggiornamento hello avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="087c5-132">If hello entity that is being updated doesn't already exist, then hello update operation will fail.</span></span> <span data-ttu-id="087c5-133">Se si desidera toostore un'entità se esista o meno, utilizzare [insert_or_replace_entity][py_insert_or_replace_entity].</span><span class="sxs-lookup"><span data-stu-id="087c5-133">If you want toostore an entity whether it exists or not, use [insert_or_replace_entity][py_insert_or_replace_entity].</span></span> <span data-ttu-id="087c5-134">Nell'esempio seguente di hello, prima chiamata hello sostituirà entità esistente hello.</span><span class="sxs-lookup"><span data-stu-id="087c5-134">In hello following example, hello first call will replace hello existing entity.</span></span> <span data-ttu-id="087c5-135">seconda chiamata Hello verrà inserita una nuova entità, poiché alcuna entità con hello non specificati PartitionKey e RowKey esiste nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="087c5-135">hello second call will insert a new entity, since no entity with hello specified PartitionKey and RowKey exists in hello table.</span></span>

```python
# Replace hello entity created earlier
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage again', 'priority' : 250}
table_service.insert_or_replace_entity('tasktable', task)

# Insert a new entity
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '003', 'description' : 'Buy detergent', 'priority' : 300}
table_service.insert_or_replace_entity('tasktable', task)
```

> [!TIP]
> <span data-ttu-id="087c5-136">Hello [update_entity] [ py_update_entity] metodo sostituisce tutte le proprietà e valori di un'entità esistente, è inoltre possibile utilizzare la proprietà tooremove da un'entità esistente.</span><span class="sxs-lookup"><span data-stu-id="087c5-136">hello [update_entity][py_update_entity] method replaces all properties and values of an existing entity, which you can also use tooremove properties from an existing entity.</span></span> <span data-ttu-id="087c5-137">È possibile utilizzare hello [merge_entity] [ py_merge_entity] tooupdate metodo un'entità esistente con i valori delle proprietà di nuovi o modificati senza sostituire completamente entità hello.</span><span class="sxs-lookup"><span data-stu-id="087c5-137">You can use hello [merge_entity][py_merge_entity] method tooupdate an existing entity with new or modified property values without completely replacing hello entity.</span></span>

## <a name="modify-multiple-entities"></a><span data-ttu-id="087c5-138">Modificare più entità</span><span class="sxs-lookup"><span data-stu-id="087c5-138">Modify multiple entities</span></span>

<span data-ttu-id="087c5-139">tooensure hello elaborazione atomica di una richiesta dal servizio tabelle hello, è possibile inviare più operazioni in un batch.</span><span class="sxs-lookup"><span data-stu-id="087c5-139">tooensure hello atomic processing of a request by hello Table service, you can submit multiple operations together in a batch.</span></span> <span data-ttu-id="087c5-140">Innanzitutto, utilizzare hello [TableBatch] [ py_TableBatch] classe tooadd più operazioni tooa unica.</span><span class="sxs-lookup"><span data-stu-id="087c5-140">First, use hello [TableBatch][py_TableBatch] class tooadd multiple operations tooa single batch.</span></span> <span data-ttu-id="087c5-141">Successivamente, chiamare [TableService][py_TableService].[ commit_batch] [ py_commit_batch] operazioni hello toosubmit in un'operazione atomica.</span><span class="sxs-lookup"><span data-stu-id="087c5-141">Next, call [TableService][py_TableService].[commit_batch][py_commit_batch] toosubmit hello operations in an atomic operation.</span></span> <span data-ttu-id="087c5-142">Deve essere modificato in batch tutti toobe di entità in hello stessa partizione.</span><span class="sxs-lookup"><span data-stu-id="087c5-142">All entities toobe modified in batch must be in hello same partition.</span></span>

<span data-ttu-id="087c5-143">Questo esempio aggiunge due entità in un batch:</span><span class="sxs-lookup"><span data-stu-id="087c5-143">This example adds two entities together in a batch:</span></span>

```python
from azure.storage.table import TableBatch
batch = TableBatch()
task004 = {'PartitionKey': 'tasksSeattle', 'RowKey': '004', 'description' : 'Go grocery shopping', 'priority' : 400}
task005 = {'PartitionKey': 'tasksSeattle', 'RowKey': '005', 'description' : 'Clean hello bathroom', 'priority' : 100}
batch.insert_entity(task004)
batch.insert_entity(task005)
table_service.commit_batch('tasktable', batch)
```

<span data-ttu-id="087c5-144">Batch utilizzabile anche con la sintassi di gestione di hello contesto:</span><span class="sxs-lookup"><span data-stu-id="087c5-144">Batches can also be used with hello context manager syntax:</span></span>

```python
task006 = {'PartitionKey': 'tasksSeattle', 'RowKey': '006', 'description' : 'Go grocery shopping', 'priority' : 400}
task007 = {'PartitionKey': 'tasksSeattle', 'RowKey': '007', 'description' : 'Clean hello bathroom', 'priority' : 100}

with table_service.batch('tasktable') as batch:
    batch.insert_entity(task006)
    batch.insert_entity(task007)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="087c5-145">Eseguire una query su un'entità</span><span class="sxs-lookup"><span data-stu-id="087c5-145">Query for an entity</span></span>

<span data-ttu-id="087c5-146">tooquery per un'entità in una tabella, passare il relativo toohello PartitionKey e RowKey [TableService][py_TableService].[ get_entity] [ py_get_entity] metodo.</span><span class="sxs-lookup"><span data-stu-id="087c5-146">tooquery for an entity in a table, pass its PartitionKey and RowKey toohello [TableService][py_TableService].[get_entity][py_get_entity] method.</span></span>

```python
task = table_service.get_entity('tasktable', 'tasksSeattle', '001')
print(task.description)
print(task.priority)
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="087c5-147">Eseguire query su un set di entità</span><span class="sxs-lookup"><span data-stu-id="087c5-147">Query a set of entities</span></span>

<span data-ttu-id="087c5-148">È possibile eseguire una query per un set di entità specificando una stringa di filtro con hello **filtro** parametro.</span><span class="sxs-lookup"><span data-stu-id="087c5-148">You can query for a set of entities by supplying a filter string with hello **filter** parameter.</span></span> <span data-ttu-id="087c5-149">Questo esempio trova tutte le attività di Seattle applicando un filtro a PartitionKey:</span><span class="sxs-lookup"><span data-stu-id="087c5-149">This example finds all tasks in Seattle by applying a filter on PartitionKey:</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'")
for task in tasks:
    print(task.description)
    print(task.priority)
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="087c5-150">Eseguire query su un subset di proprietà di entità</span><span class="sxs-lookup"><span data-stu-id="087c5-150">Query a subset of entity properties</span></span>

<span data-ttu-id="087c5-151">È anche possibile limitare le proprietà restituite per ogni entità in una query.</span><span class="sxs-lookup"><span data-stu-id="087c5-151">You can also restrict which properties are returned for each entity in a query.</span></span> <span data-ttu-id="087c5-152">Questa tecnica, denominata *proiezione*, consente di ridurre la larghezza di banda e di migliorare le prestazioni di query, in particolare per entità o set di risultati di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="087c5-152">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities or result sets.</span></span> <span data-ttu-id="087c5-153">Hello utilizzare **selezionare** parametro e passare i nomi di hello di proprietà hello desiderate restituito toohello client.</span><span class="sxs-lookup"><span data-stu-id="087c5-153">Use hello **select** parameter and pass hello names of hello properties you want returned toohello client.</span></span>

<span data-ttu-id="087c5-154">query di Hello nel seguente codice hello restituisce solo le descrizioni di hello di entità nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="087c5-154">hello query in hello following code returns only hello descriptions of entities in hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="087c5-155">Hello seguente frammento di codice funziona solo con hello archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="087c5-155">hello following snippet works only against hello Azure Storage.</span></span> <span data-ttu-id="087c5-156">Non è supportata dall'emulatore di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="087c5-156">It is not supported by hello storage emulator.</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'", select='description')
for task in tasks:
    print(task.description)
```

## <a name="delete-an-entity"></a><span data-ttu-id="087c5-157">Eliminare un'entità</span><span class="sxs-lookup"><span data-stu-id="087c5-157">Delete an entity</span></span>

<span data-ttu-id="087c5-158">Eliminare un'entità mediante il passaggio relativo toohello PartitionKey e RowKey [delete_entity] [ py_delete_entity] metodo.</span><span class="sxs-lookup"><span data-stu-id="087c5-158">Delete an entity by passing its PartitionKey and RowKey toohello [delete_entity][py_delete_entity] method.</span></span>

```python
table_service.delete_entity('tasktable', 'tasksSeattle', '001')
```

## <a name="delete-a-table"></a><span data-ttu-id="087c5-159">Eliminare una tabella</span><span class="sxs-lookup"><span data-stu-id="087c5-159">Delete a table</span></span>

<span data-ttu-id="087c5-160">Se non è più necessario una tabella o una delle entità hello in esso contenuti, chiamare hello [delete_table] [ py_delete_table] toopermanently metodo Elimina tabella hello da archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="087c5-160">If you no longer need a table or any of hello entities within it, call hello [delete_table][py_delete_table] method toopermanently delete hello table from Azure Storage.</span></span>

```python
table_service.delete_table('tasktable')
```

## <a name="next-steps"></a><span data-ttu-id="087c5-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="087c5-161">Next steps</span></span>

* [<span data-ttu-id="087c5-162">Informazioni di riferimento sull'API dell'SDK di Archiviazione di Azure per Python</span><span class="sxs-lookup"><span data-stu-id="087c5-162">Azure Storage SDK for Python API reference</span></span>](https://azure-storage.readthedocs.io/en/latest/index.html)
* [<span data-ttu-id="087c5-163">SDK di Archiviazione di Azure per Python</span><span class="sxs-lookup"><span data-stu-id="087c5-163">Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)
* [<span data-ttu-id="087c5-164">Centro per sviluppatori Python</span><span class="sxs-lookup"><span data-stu-id="087c5-164">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* <span data-ttu-id="087c5-165">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md): un'applicazione gratuita multipiattaforma per lavorare in modo visivo con i dati di Archiviazione di Azure in Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="087c5-165">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md): A free, cross-platform application for working visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

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
