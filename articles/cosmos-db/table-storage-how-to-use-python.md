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
# <a name="how-toouse-table-storage-in-python"></a>Come toouse archiviazione tabelle di Python

[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

Questa guida viene spiegato come tooperform tabella Azure storage scenari comuni in Python mediante hello [Microsoft Azure Storage SDK per Python](https://github.com/Azure/azure-storage-python). scenari di Hello trattati includono la creazione e l'eliminazione di una tabella, inserimento e query su entità.

Mentre vengono elaborati i scenari di hello in questa esercitazione, è preferibile toorefer toohello [Azure Storage SDK per Python API reference](https://azure-storage.readthedocs.io/en/latest/index.html).

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="install-hello-azure-storage-sdk-for-python"></a>Installare hello Azure Storage SDK per Python

Dopo aver creato un account di archiviazione, il passaggio successivo è hello tooinstall [Microsoft Azure Storage SDK per Python](https://github.com/Azure/azure-storage-python). Per informazioni dettagliate sull'installazione hello SDK, vedere toohello [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) file in hello Azure Storage SDK per il repository di Python su GitHub.

## <a name="create-a-table"></a>Creare una tabella

toowork con hello servizio tabelle di Azure di Python, è necessario importare hello [TableService] [ py_TableService] modulo. Poiché lavorerà con entità di tabella, è necessario anche hello [entità] [ py_Entity] classe. Aggiungere questo codice superiore hello il file Python tooimport entrambi:

```python
from azure.storage.table import TableService, Entity
```

Creare un oggetto [TableService][py_TableService] passando il nome dell'account di archiviazione e la chiave dell'account. Sostituire `myaccount` e `mykey` con il nome di account e una chiave e una chiamata [create_table] [ py_create_table] tabella hello toocreate in archiviazione di Azure.

```python
table_service = TableService(account_name='myaccount', account_key='mykey')

table_service.create_table('tasktable')
```

## <a name="add-an-entity-tooa-table"></a>Aggiungere una tabella tooa entità

tooadd un'entità, creare innanzitutto un oggetto che rappresenta l'entità, quindi passare hello oggetto toohello [TableService][py_TableService].[ insert_entity] [ py_insert_entity] metodo. oggetto entità Hello può essere un dizionario o un oggetto di tipo [entità][py_Entity]e definisce i nomi delle proprietà e i valori dell'entità. Ogni entità devono includere hello necessario [PartitionKey e RowKey](#partitionkey-and-rowkey) proprietà, in aggiunta tooany altre proprietà è possibile definire per entità hello.

Questo esempio viene creato un oggetto dizionario che rappresenta un'entità, quindi passarlo toohello [insert_entity] [ py_insert_entity] metodo tooadd è toohello tabella:

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello trash', 'priority' : 200}
table_service.insert_entity('tasktable', task)
```

Questo esempio viene creato un [entità] [ py_Entity] dell'oggetto, quindi passarlo toohello [insert_entity] [ py_insert_entity] metodo tooadd è toohello tabella:

```python
task = Entity()
task.PartitionKey = 'tasksSeattle'
task.RowKey = '002'
task.description = 'Wash hello car'
task.priority = 100
table_service.insert_entity('tasktable', task)
```

### <a name="partitionkey-and-rowkey"></a>PartitionKey e RowKey

È necessario specificare entrambe le proprietà **PartitionKey** e **RowKey** per ogni entità. Questi sono identificatori univoci di hello delle entità, come insieme formano una chiave primaria di hello di un'entità. È possibile eseguire query usando questi valori in modo molto più rapido rispetto a quanto è possibile fare su qualsiasi altra proprietà dell'entità, perché solo queste proprietà sono indicizzate.

servizio tabelle utilizza Hello **PartitionKey** toointelligently distribuire le entità di tabella in nodi di archiviazione. Entità che dispongono di hello stesso **PartitionKey** vengono archiviati in hello stesso nodo. **RowKey** hello ID univoco dell'entità hello all'interno della partizione hello a cui appartiene.

## <a name="update-an-entity"></a>Aggiornare un'entità

tooupdate tutti di valori di proprietà dell'entità, chiamare hello [update_entity] [ py_update_entity] metodo. Questo esempio viene illustrato come tooreplace un'entità esistente con una versione aggiornata:

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage', 'priority' : 250}
table_service.update_entity('tasktable', task)
```

Se l'entità hello in corso di aggiornamento non esiste già, l'operazione di aggiornamento hello avrà esito negativo. Se si desidera toostore un'entità se esista o meno, utilizzare [insert_or_replace_entity][py_insert_or_replace_entity]. Nell'esempio seguente di hello, prima chiamata hello sostituirà entità esistente hello. seconda chiamata Hello verrà inserita una nuova entità, poiché alcuna entità con hello non specificati PartitionKey e RowKey esiste nella tabella hello.

```python
# Replace hello entity created earlier
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage again', 'priority' : 250}
table_service.insert_or_replace_entity('tasktable', task)

# Insert a new entity
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '003', 'description' : 'Buy detergent', 'priority' : 300}
table_service.insert_or_replace_entity('tasktable', task)
```

> [!TIP]
> Hello [update_entity] [ py_update_entity] metodo sostituisce tutte le proprietà e valori di un'entità esistente, è inoltre possibile utilizzare la proprietà tooremove da un'entità esistente. È possibile utilizzare hello [merge_entity] [ py_merge_entity] tooupdate metodo un'entità esistente con i valori delle proprietà di nuovi o modificati senza sostituire completamente entità hello.

## <a name="modify-multiple-entities"></a>Modificare più entità

tooensure hello elaborazione atomica di una richiesta dal servizio tabelle hello, è possibile inviare più operazioni in un batch. Innanzitutto, utilizzare hello [TableBatch] [ py_TableBatch] classe tooadd più operazioni tooa unica. Successivamente, chiamare [TableService][py_TableService].[ commit_batch] [ py_commit_batch] operazioni hello toosubmit in un'operazione atomica. Deve essere modificato in batch tutti toobe di entità in hello stessa partizione.

Questo esempio aggiunge due entità in un batch:

```python
from azure.storage.table import TableBatch
batch = TableBatch()
task004 = {'PartitionKey': 'tasksSeattle', 'RowKey': '004', 'description' : 'Go grocery shopping', 'priority' : 400}
task005 = {'PartitionKey': 'tasksSeattle', 'RowKey': '005', 'description' : 'Clean hello bathroom', 'priority' : 100}
batch.insert_entity(task004)
batch.insert_entity(task005)
table_service.commit_batch('tasktable', batch)
```

Batch utilizzabile anche con la sintassi di gestione di hello contesto:

```python
task006 = {'PartitionKey': 'tasksSeattle', 'RowKey': '006', 'description' : 'Go grocery shopping', 'priority' : 400}
task007 = {'PartitionKey': 'tasksSeattle', 'RowKey': '007', 'description' : 'Clean hello bathroom', 'priority' : 100}

with table_service.batch('tasktable') as batch:
    batch.insert_entity(task006)
    batch.insert_entity(task007)
```

## <a name="query-for-an-entity"></a>Eseguire una query su un'entità

tooquery per un'entità in una tabella, passare il relativo toohello PartitionKey e RowKey [TableService][py_TableService].[ get_entity] [ py_get_entity] metodo.

```python
task = table_service.get_entity('tasktable', 'tasksSeattle', '001')
print(task.description)
print(task.priority)
```

## <a name="query-a-set-of-entities"></a>Eseguire query su un set di entità

È possibile eseguire una query per un set di entità specificando una stringa di filtro con hello **filtro** parametro. Questo esempio trova tutte le attività di Seattle applicando un filtro a PartitionKey:

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'")
for task in tasks:
    print(task.description)
    print(task.priority)
```

## <a name="query-a-subset-of-entity-properties"></a>Eseguire query su un subset di proprietà di entità

È anche possibile limitare le proprietà restituite per ogni entità in una query. Questa tecnica, denominata *proiezione*, consente di ridurre la larghezza di banda e di migliorare le prestazioni di query, in particolare per entità o set di risultati di grandi dimensioni. Hello utilizzare **selezionare** parametro e passare i nomi di hello di proprietà hello desiderate restituito toohello client.

query di Hello nel seguente codice hello restituisce solo le descrizioni di hello di entità nella tabella hello.

> [!NOTE]
> Hello seguente frammento di codice funziona solo con hello archiviazione di Azure. Non è supportata dall'emulatore di archiviazione hello.

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'", select='description')
for task in tasks:
    print(task.description)
```

## <a name="delete-an-entity"></a>Eliminare un'entità

Eliminare un'entità mediante il passaggio relativo toohello PartitionKey e RowKey [delete_entity] [ py_delete_entity] metodo.

```python
table_service.delete_entity('tasktable', 'tasksSeattle', '001')
```

## <a name="delete-a-table"></a>Eliminare una tabella

Se non è più necessario una tabella o una delle entità hello in esso contenuti, chiamare hello [delete_table] [ py_delete_table] toopermanently metodo Elimina tabella hello da archiviazione di Azure.

```python
table_service.delete_table('tasktable')
```

## <a name="next-steps"></a>Passaggi successivi

* [Informazioni di riferimento sull'API dell'SDK di Archiviazione di Azure per Python](https://azure-storage.readthedocs.io/en/latest/index.html)
* [SDK di Archiviazione di Azure per Python](https://github.com/Azure/azure-storage-python)
* [Centro per sviluppatori Python](https://azure.microsoft.com/develop/python/)
* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md): un'applicazione gratuita multipiattaforma per lavorare in modo visivo con i dati di Archiviazione di Azure in Windows, macOS e Linux.

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
