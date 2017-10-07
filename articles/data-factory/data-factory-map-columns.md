---
title: colonne di set di dati aaaMapping nella Data Factory di Azure | Documenti Microsoft
description: Informazioni su come toomap colonne toodestination di colonne di origine.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 8f78d4af675bec0a70e5f6e83ec1ffb511408b5a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="map-source-dataset-columns-toodestination-dataset-columns"></a>Eseguire il mapping di colonne di set di dati di origine del dataset colonne toodestination
Mapping della colonna può essere utilizzato toospecify come colonne specificate nella hello "struttura" di toocolumns mappa tabella di origine specificate in hello "struttura" della tabella del sink. Hello **columnMapping** proprietà è disponibile in hello **typeProperties** sezione di hello attività di copia.

Mapping di colonne supporta hello seguenti scenari:

* Tutte le colonne nella struttura di set di dati di origine hello sono mappate tooall nella struttura di hello sink set di dati.
* Un subset di colonne hello nella struttura di set di dati di origine hello è mappato tooall colonne struttura di set di dati di hello sink.

di seguito Hello sono condizioni di errore che comporta un'eccezione:

* Un numero di colonne o altre colonne in hello "struttura" della tabella del sink specificato nel mapping hello.
* Mapping duplicato.
* Risultato della query SQL non dispone di un nome di colonna specificato nel mapping hello.

> [!NOTE]
> Hello negli esempi seguenti sono per SQL Azure e Blob di Azure ma sono applicabili tooany archivio di dati che supporta i set di dati rettangolare. Modificare i set di dati e le definizioni di servizio collegato in toodata toopoint esempi nell'origine dati rilevanti hello.

## <a name="sample-1--column-mapping-from-azure-sql-tooazure-blob"></a>Esempio 1: mapping dal blob di Azure SQL tooAzure colonne
In questo esempio, tabella di input hello ha una struttura e tabella SQL tooa punti in un database SQL di Azure.

```json
{
    "name": "AzureSQLInput",
    "properties": {
        "structure": 
         [
           { "name": "userid"},
           { "name": "name"},
           { "name": "group"}
         ],
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

In questo esempio, tabella di output di hello ha una struttura e punti tooa blob in un archivio blob di Azure.

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
         "structure": 
          [
                { "name": "myuserid"},
                { "name": "myname" },
                { "name": "mygroup"}
          ],
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder",
            "fileName":"myfile.csv",
            "format":
            {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Hello JSON seguente definisce un'attività di copia in una pipeline. mapping delle colonne di Hello dall'origine toocolumns nel sink (**columnMappings**) utilizzando hello **traduttore** proprietà.

```json
{
    "name": "CopyActivity",
    "description": "description", 
    "type": "Copy",
    "inputs":  [ { "name": "AzureSQLInput"  } ],
    "outputs":  [ { "name": "AzureBlobOutput" } ],
    "typeProperties":    {
        "source":
        {
            "type": "SqlSource"
        },
        "sink":
        {
            "type": "BlobSink"
        },
        "translator": 
        {
            "type": "TabularTranslator",
            "ColumnMappings": "UserId: MyUserId, Group: MyGroup, Name: MyName"
        }
    },
   "scheduler": {
          "frequency": "Hour",
          "interval": 1
        }
}
```
**Flusso del mapping di colonne:**

![Flusso del mapping di colonne](./media/data-factory-map-columns/column-mapping-flow.png)

## <a name="sample-2--column-mapping-with-sql-query-from-azure-sql-tooazure-blob"></a>Esempio 2: mapping con query SQL da blob di Azure SQL tooAzure colonne
In questo esempio, una query SQL è usato tooextract dati da SQL Azure anziché specificare semplicemente il nome di tabella hello e nomi di colonna hello nella sezione "struttura". 

```json
{
    "name": "CopyActivity",
    "description": "description", 
    "type": "CopyActivity",
    "inputs":  [ { "name": " AzureSQLInput"  } ],
    "outputs":  [ { "name": " AzureBlobOutput" } ],
    "typeProperties":
    {
        "source":
        {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartDateTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
        },
        "sink":
        {
            "type": "BlobSink"
        },
        "Translator": 
        {
            "type": "TabularTranslator",
            "ColumnMappings": "UserId: MyUserId, Group: MyGroup,Name: MyName"
        }
    },
    "scheduler": {
          "frequency": "Hour",
          "interval": 1
        }
}
```
In questo caso, i risultati della query hello sono prima toocolumns mappato specificato in "struttura" dell'origine. Successivamente, le colonne di hello dall'origine "struttura" sono mappate toocolumns nel sink "struttura" con le regole specificate in elementi columnMappings.  Si supponga che la query hello restituisce 5 colonne, altre due colonne rispetto a quelle specificate in hello "struttura" dell'origine.

**Flusso del mapping di colonne**

![Flusso del mapping di colonne-2](./media/data-factory-map-columns/column-mapping-flow-2.png)

## <a name="next-steps"></a>Passaggi successivi
Per un'esercitazione sull'uso di attività di copia, vedere l'articolo di hello: 

- [Copiare i dati da archiviazione Blob tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
