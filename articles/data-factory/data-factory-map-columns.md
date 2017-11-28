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
# <a name="map-source-dataset-columns-toodestination-dataset-columns"></a><span data-ttu-id="11203-103">Eseguire il mapping di colonne di set di dati di origine del dataset colonne toodestination</span><span class="sxs-lookup"><span data-stu-id="11203-103">Map source dataset columns toodestination dataset columns</span></span>
<span data-ttu-id="11203-104">Mapping della colonna può essere utilizzato toospecify come colonne specificate nella hello "struttura" di toocolumns mappa tabella di origine specificate in hello "struttura" della tabella del sink.</span><span class="sxs-lookup"><span data-stu-id="11203-104">Column mapping can be used toospecify how columns specified in hello “structure” of source table map toocolumns specified in hello “structure” of sink table.</span></span> <span data-ttu-id="11203-105">Hello **columnMapping** proprietà è disponibile in hello **typeProperties** sezione di hello attività di copia.</span><span class="sxs-lookup"><span data-stu-id="11203-105">hello **columnMapping** property is available in hello **typeProperties** section of hello Copy activity.</span></span>

<span data-ttu-id="11203-106">Mapping di colonne supporta hello seguenti scenari:</span><span class="sxs-lookup"><span data-stu-id="11203-106">Column mapping supports hello following scenarios:</span></span>

* <span data-ttu-id="11203-107">Tutte le colonne nella struttura di set di dati di origine hello sono mappate tooall nella struttura di hello sink set di dati.</span><span class="sxs-lookup"><span data-stu-id="11203-107">All columns in hello source dataset structure are mapped tooall columns in hello sink dataset structure.</span></span>
* <span data-ttu-id="11203-108">Un subset di colonne hello nella struttura di set di dati di origine hello è mappato tooall colonne struttura di set di dati di hello sink.</span><span class="sxs-lookup"><span data-stu-id="11203-108">A subset of hello columns in hello source dataset structure is mapped tooall columns in hello sink dataset structure.</span></span>

<span data-ttu-id="11203-109">di seguito Hello sono condizioni di errore che comporta un'eccezione:</span><span class="sxs-lookup"><span data-stu-id="11203-109">hello following are error conditions that result in an exception:</span></span>

* <span data-ttu-id="11203-110">Un numero di colonne o altre colonne in hello "struttura" della tabella del sink specificato nel mapping hello.</span><span class="sxs-lookup"><span data-stu-id="11203-110">Either fewer columns or more columns in hello “structure” of sink table than specified in hello mapping.</span></span>
* <span data-ttu-id="11203-111">Mapping duplicato.</span><span class="sxs-lookup"><span data-stu-id="11203-111">Duplicate mapping.</span></span>
* <span data-ttu-id="11203-112">Risultato della query SQL non dispone di un nome di colonna specificato nel mapping hello.</span><span class="sxs-lookup"><span data-stu-id="11203-112">SQL query result does not have a column name that is specified in hello mapping.</span></span>

> [!NOTE]
> <span data-ttu-id="11203-113">Hello negli esempi seguenti sono per SQL Azure e Blob di Azure ma sono applicabili tooany archivio di dati che supporta i set di dati rettangolare.</span><span class="sxs-lookup"><span data-stu-id="11203-113">hello following samples are for Azure SQL and Azure Blob but are applicable tooany data store that supports rectangular datasets.</span></span> <span data-ttu-id="11203-114">Modificare i set di dati e le definizioni di servizio collegato in toodata toopoint esempi nell'origine dati rilevanti hello.</span><span class="sxs-lookup"><span data-stu-id="11203-114">Adjust dataset and linked service definitions in examples toopoint toodata in hello relevant data source.</span></span>

## <a name="sample-1--column-mapping-from-azure-sql-tooazure-blob"></a><span data-ttu-id="11203-115">Esempio 1: mapping dal blob di Azure SQL tooAzure colonne</span><span class="sxs-lookup"><span data-stu-id="11203-115">Sample 1 – column mapping from Azure SQL tooAzure blob</span></span>
<span data-ttu-id="11203-116">In questo esempio, tabella di input hello ha una struttura e tabella SQL tooa punti in un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="11203-116">In this sample, hello input table has a structure and it points tooa SQL table in an Azure SQL database.</span></span>

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

<span data-ttu-id="11203-117">In questo esempio, tabella di output di hello ha una struttura e punti tooa blob in un archivio blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="11203-117">In this sample, hello output table has a structure and it points tooa blob in an Azure blob storage.</span></span>

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

<span data-ttu-id="11203-118">Hello JSON seguente definisce un'attività di copia in una pipeline.</span><span class="sxs-lookup"><span data-stu-id="11203-118">hello following JSON defines a copy activity in a pipeline.</span></span> <span data-ttu-id="11203-119">mapping delle colonne di Hello dall'origine toocolumns nel sink (**columnMappings**) utilizzando hello **traduttore** proprietà.</span><span class="sxs-lookup"><span data-stu-id="11203-119">hello columns from source mapped toocolumns in sink (**columnMappings**) by using hello **Translator** property.</span></span>

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
<span data-ttu-id="11203-120">**Flusso del mapping di colonne:**</span><span class="sxs-lookup"><span data-stu-id="11203-120">**Column mapping flow:**</span></span>

![Flusso del mapping di colonne](./media/data-factory-map-columns/column-mapping-flow.png)

## <a name="sample-2--column-mapping-with-sql-query-from-azure-sql-tooazure-blob"></a><span data-ttu-id="11203-122">Esempio 2: mapping con query SQL da blob di Azure SQL tooAzure colonne</span><span class="sxs-lookup"><span data-stu-id="11203-122">Sample 2 – column mapping with SQL query from Azure SQL tooAzure blob</span></span>
<span data-ttu-id="11203-123">In questo esempio, una query SQL è usato tooextract dati da SQL Azure anziché specificare semplicemente il nome di tabella hello e nomi di colonna hello nella sezione "struttura".</span><span class="sxs-lookup"><span data-stu-id="11203-123">In this sample, a SQL query is used tooextract data from Azure SQL instead of simply specifying hello table name and hello column names in “structure” section.</span></span> 

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
<span data-ttu-id="11203-124">In questo caso, i risultati della query hello sono prima toocolumns mappato specificato in "struttura" dell'origine.</span><span class="sxs-lookup"><span data-stu-id="11203-124">In this case, hello query results are first mapped toocolumns specified in “structure” of source.</span></span> <span data-ttu-id="11203-125">Successivamente, le colonne di hello dall'origine "struttura" sono mappate toocolumns nel sink "struttura" con le regole specificate in elementi columnMappings.</span><span class="sxs-lookup"><span data-stu-id="11203-125">Next, hello columns from source “structure” are mapped toocolumns in sink “structure” with rules specified in columnMappings.</span></span>  <span data-ttu-id="11203-126">Si supponga che la query hello restituisce 5 colonne, altre due colonne rispetto a quelle specificate in hello "struttura" dell'origine.</span><span class="sxs-lookup"><span data-stu-id="11203-126">Suppose hello query returns 5 columns, two more columns than those specified in hello “structure” of source.</span></span>

<span data-ttu-id="11203-127">**Flusso del mapping di colonne**</span><span class="sxs-lookup"><span data-stu-id="11203-127">**Column mapping flow**</span></span>

![Flusso del mapping di colonne-2](./media/data-factory-map-columns/column-mapping-flow-2.png)

## <a name="next-steps"></a><span data-ttu-id="11203-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="11203-129">Next steps</span></span>
<span data-ttu-id="11203-130">Per un'esercitazione sull'uso di attività di copia, vedere l'articolo di hello:</span><span class="sxs-lookup"><span data-stu-id="11203-130">See hello article for a tutorial on using Copy Activity:</span></span> 

- [<span data-ttu-id="11203-131">Copiare i dati da archiviazione Blob tooSQL Database</span><span class="sxs-lookup"><span data-stu-id="11203-131">Copy data from Blob Storage tooSQL Database</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
