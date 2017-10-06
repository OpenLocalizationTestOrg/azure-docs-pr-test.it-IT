---
title: aaaMove dati dal servizio di archiviazione semplice Amazon utilizzando Data Factory | Documenti Microsoft
description: Per ulteriori informazioni vedere toomove dati dal servizio di archiviazione semplice Amazon (S3) usando Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 636d3179-eba8-4841-bcb4-3563f6822a26
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 8a8cd2845fd1de74413bd0372f3aabfb4817549b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-amazon-simple-storage-service-by-using-azure-data-factory"></a>Spostare i dati da Amazon Simple Storage Service usando Azure Data Factory
Questo articolo spiega come hello toouse attività di copia dei dati di Azure Data Factory toomove dal servizio di archiviazione semplice Amazon (S3). È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello.

È possibile copiare i dati dall'archivio dati di Amazon S3 tooany supportati sink. Per un elenco di dati supportati archivi come sink dall'attività di copia hello, vedere hello [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabella. Data Factory supporta attualmente solo lo spostamento dei dati dagli archivi di dati tooother S3 Amazon, ma non lo spostamento dei dati da altri dati archivia tooAmazon S3.

## <a name="required-permissions"></a>Autorizzazioni necessarie
dati toocopy S3 Amazon, verificare che sia stato concesso hello queste autorizzazioni:

* `s3:GetObject` e `s3:GetObjectVersion` per le operazioni di oggetto Amazon S3.
* `s3:ListBucket` per le operazioni di bucket Amazon S3. Se si utilizza Copia guidata di Data Factory, hello `s3:ListAllMyBuckets` è obbligatorio.

Per informazioni dettagliate sull'elenco completo di hello di Amazon S3 autorizzazioni, vedere [che specifica le autorizzazioni in un criterio](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).

## <a name="getting-started"></a>introduttiva
È possibile creare una pipeline con l'attività di copia che sposta i dati da un'origine Amazon S3 usando diversi strumenti o API.

toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**. Per una procedura dettagliata, vedere [Esercitazione: Creare una pipeline usando la Copia guidata](data-factory-copy-data-wizard-tutorial.md).

È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**. Per istruzioni dettagliate toocreate una pipeline con attività di copia, vedere hello [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

Se si utilizzano strumenti o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:

1. Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.
2. Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello.
3. Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.

Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente. Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory. Per un esempio con le definizioni di JSON per le entità Data Factory dati toocopy utilizzato da un archivio dati S3 Amazon, vedere hello [esempio JSON: copiare i dati da Amazon S3 tooAzure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) sezione di questo articolo.

> [!NOTE]
> Per informazioni dettagliate sui formati di compressione e i file supportati per l'attività di copia, vedere [Formati di compressione e file in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).

Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che vengono utilizzati toodefine Data Factory entità specifiche tooAmazon S3.

## <a name="linked-service-properties"></a>Proprietà del servizio collegato
Un servizio collegato di collegare una data factory tooa archivio di dati. Creare un servizio collegato di tipo **AwsAccessKey** toolink data factory di tooyour di archiviare i dati di Amazon S3. Hello nella tabella seguente fornisce il servizio di descrizione per JSON elementi specifici tooAmazon S3 (AwsAccessKey) collegati.

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| accessKeyID |ID della chiave di accesso privata hello. |string |Sì |
| secretAccessKey |chiave di accesso per i segreti Hello stessa. |La stringa segreta crittografata |Sì |

Di seguito è fornito un esempio:

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

## <a name="dataset-properties"></a>Proprietà dei set di dati
toospecify toorepresent un set di dati di input troppo dati nell'archiviazione Blob di Azure, set di proprietà di tipo hello del set di dati hello**AmazonS3**. Set hello **linkedServiceName** servizio collegato di proprietà del nome di toohello hello set di dati di hello Amazon S3. Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione di set di dati, vedere l'articolo sulla [creazione di set di dati](data-factory-create-datasets.md). 

Le sezioni come struttura, disponibilità e criteri sono simili per tutti i tipi di set di dati, ad esempio database SQL, BLOB di Azure e tabelle di Azure. Hello **typeProperties** sezione è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello. Hello **typeProperties** sezione per un set di dati di tipo **AmazonS3** (che include set di dati hello Amazon S3) ha hello le proprietà seguenti:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| bucketName |nome di bucket Hello S3. |String |Sì |
| key |chiave dell'oggetto Hello S3. |String |No |
| prefix |Prefisso per la chiave dell'oggetto hello S3. Vengono selezionati gli oggetti le cui chiavi iniziano con questo prefisso. Si applica solo quando la chiave è vuota. |string |No |
| version |versione di Hello dell'oggetto hello S3, se è abilitato il controllo delle versioni S3. |String |No |
| format | è supportato i seguenti tipi di formato Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set hello **tipo** proprietà in formato tooone di questi valori. Per ulteriori informazioni, vedere hello [formato testo](data-factory-supported-file-and-compression-formats.md#text-format), [formato JSON](data-factory-supported-file-and-compression-formats.md#json-format), [formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [formato Parquet ](data-factory-supported-file-and-compression-formats.md#parquet-format) sezioni. <br><br> Se si desidera che il file toocopy come-tra basate su file archivi (copia binaria), skip hello formato sezione in entrambe le definizioni di set di dati di input e output. |No | |
| compressione | Specificare il tipo di hello e livello di compressione per dati hello. tipi di Hello supportato sono: **GZip**, **Deflate**, **BZip2**, e **ZipDeflate**. livelli di Hello supportato sono: **ottimale** e **Fastest**. Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |No | |


> [!NOTE]
> **bucketName + tasto** specifica hello percorso dell'oggetto hello S3, dove è il contenitore radice hello per gli oggetti S3 e key oggetto toohello S3 percorso completo di hello.

### <a name="sample-dataset-with-prefix"></a>Set di dati di esempio con prefisso

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "testbucket",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
### <a name="sample-dataset-with-version"></a>Set di dati di esempio (con versione)

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "testbucket",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="dynamic-paths-for-s3"></a>Percorsi dinamici per S3
Hello esempio precedente Usa valori fissi per hello **chiave** e **bucketName** proprietà nel set di dati hello Amazon S3.

```json
"key": "testFolder/test.orc",
"bucketName": "testbucket",
```

È possibile fare in modo che Data Factory calcoli queste proprietà dinamicamente in fase di runtime usando le variabili di sistema, come SliceStart.

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

È possibile eseguire stesso hello per hello **prefisso** proprietà di un set di dati di Amazon S3. Per un elenco delle funzioni e delle variabili, vedere [Funzioni e variabili di sistema di Data Factory](data-factory-functions-variables.md) .

## <a name="copy-activity-properties"></a>Proprietà dell'attività di copia
Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione delle attività, vedere l'articolo sulla [creazione di pipeline](data-factory-create-pipelines.md). Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri. Le proprietà disponibili nella hello **typeProperties** sezione dell'attività hello variano in base a ogni tipo di attività. Per attività di copia hello, le proprietà variano a seconda di hello tipi di origini e sink. Quando un'origine in attività di copia hello è di tipo **FileSystemSource** (che include Amazon S3), hello seguenti proprietà è disponibile in **typeProperties** sezione:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| ricorsiva |Specifica se l'elenco toorecursively S3 oggetti nella directory hello. |true/false |No |

## <a name="json-example-copy-data-from-amazon-s3-tooazure-blob-storage"></a>Esempio JSON: copiare i dati da Amazon S3 tooAzure nell'archiviazione Blob
Questo esempio viene illustrato come dati toocopy da Amazon S3 tooan archiviazione Blob di Azure. Tuttavia, dati possono essere copiati direttamente troppo[uno qualsiasi dei sink hello supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tramite attività di copia hello in Data Factory.

esempio Hello fornisce definizioni di JSON per hello seguenti entità Data Factory. È possibile utilizzare questi toocreate definizioni una pipeline di dati dall'archivio tooBlob S3 Amazon, toocopy utilizzando hello [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), o [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).   

* Un servizio collegato di tipo [AwsAccessKey](#linked-service-properties).
* Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Un [set di dati](data-factory-create-datasets.md) di input di tipo [AmazonS3](#dataset-properties).
* Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [FileSystemSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

esempio Hello copia dati da Amazon S3 tooan blob di Azure ogni ora. proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.

### <a name="amazon-s3-linked-service"></a>Servizio collegato Amazon S3

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a>Servizio collegato Archiviazione di Azure

```json
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

### <a name="amazon-s3-input-dataset"></a>Set di dati di input Amazon S3

Impostazione **"external": true** informa servizio Data Factory hello di set di dati hello è data factory di toohello esterno. Impostare tootrue questa proprietà su un set di dati di input che non è stato generato da un'attività nella pipeline hello.

```json
    {
        "name": "AmazonS3InputDataset",
        "properties": {
            "type": "AmazonS3",
            "linkedServiceName": "AmazonS3LinkedService",
            "typeProperties": {
                "key": "testFolder/test.orc",
                "bucketName": "testbucket",
                "format": {
                    "type": "OrcFormat"
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "external": true
        }
    }
```


### <a name="azure-blob-output-dataset"></a>Set di dati di output del BLOB di Azure

I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1). percorso della cartella Hello per blob hello viene valutato dinamicamente in base a ora di inizio hello della sezione hello che viene elaborato. percorso della cartella Hello Usa le parti di anno, mese, giorno e ore hello hello ora di inizio.

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazons3/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
            "partitionedBy": [
                {
                    "name": "Year",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "yyyy"
                    }
                },
                {
                    "name": "Month",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "MM"
                    }
                },
                {
                    "name": "Day",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "dd"
                    }
                },
                {
                    "name": "Hour",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "HH"
                    }
                }
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```


### <a name="copy-activity-in-a-pipeline-with-an-amazon-s3-source-and-a-blob-sink"></a>Attività di copia in una pipeline con un'origine Amazon S3 e un sink BLOB

pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output, senza che sia pianificato toorun ogni ora. Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**FileSystemSource**, e **sink** tipo è stato impostato troppo**BlobSink**.

```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "FileSystemSource",
                        "recursive": true
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonS3InputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "AmazonS3ToBlob"
            }
        ],
        "start": "2014-08-08T18:00:00Z",
        "end": "2014-08-08T19:00:00Z"
    }
}
```
> [!NOTE]
> vedere toomap colonne da un toocolumns di set di dati di origine da un set di dati sink [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).


## <a name="next-steps"></a>Passaggi successivi
Vedere hello seguenti articoli:

* toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento (attività di copia) dei dati in Data Factory e toooptimize modi diversi, vedere hello [copiare ottimizzazione Guida e alle prestazioni di attività](data-factory-copy-activity-performance.md).

* Per istruzioni dettagliate per la creazione di una pipeline con attività di copia, vedere hello [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
