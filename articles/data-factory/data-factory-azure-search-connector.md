---
title: indice di tooSearch aaaPush dati utilizzando Data Factory | Documenti Microsoft
description: Per ulteriori informazioni vedere toopush dati tooAzure indice di ricerca usando Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f8d46e1e-5c37-4408-80fb-c54be532a4ab
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: f2d973d0a2c24d6448e2d59e37e24503aa433018
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="push-data-tooan-azure-search-index-by-using-azure-data-factory"></a>Push di dati tooan indice di ricerca Azure mediante Azure Data Factory
In questo articolo viene descritto come dati toopush di attività di copia toouse hello dai dati di origine supportata archiviano tooAzure indice di ricerca. Archivi dati di origine supportati sono elencati nella colonna di origine hello di hello [origini e sink supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabella. In questo articolo si basa su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia e combinazioni di archivio di dati supportati.

## <a name="enabling-connectivity"></a>Abilitazione della connettività
servizio Data Factory tooallow connettersi tooan archivio di dati locale, si installa il Gateway di gestione di dati nell'ambiente locale. È possibile installare gateway in hello nello stesso computer che ospita i dati di origine hello archiviare o in tooavoid un computer separato competono per le risorse con i dati di hello archivio.

Gateway di gestione dati si connette servizi toocloud origini di dati locali in modo sicuro e gestito. Vedere l’articolo [Spostare dati tra cloud e locale](data-factory-move-data-between-onprem-and-cloud.md) per informazioni dettagliate sui Gateway di Gestione dati.

## <a name="getting-started"></a>introduttiva
È possibile creare una pipeline con un'attività di copia che inserisce i dati da un indice di ricerca di origine dati archivio tooAzure tramite diversi strumenti/API.

toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**. Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.

È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**. Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia. 

Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti: 

1. Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.
2. Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello. 
3. Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output. 

Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente. Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.  Per un esempio con le definizioni di JSON per le entità Data Factory indice di ricerca tooAzure toocopy utilizzati dati, vedere [esempio JSON: copiare i dati dall'indice di ricerca tooAzure SQL Server on-premise](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) sezione di questo articolo. 

Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che vengono utilizzati toodefine Data Factory entità specifiche tooAzure indice di ricerca:

## <a name="linked-service-properties"></a>Proprietà del servizio collegato

Hello nella tabella seguente vengono fornite descrizioni per gli elementi JSON che il servizio di ricerca di Azure collegati toohello specifico.

| Proprietà | Descrizione | Obbligatorio |
| -------- | ----------- | -------- |
| type | proprietà di tipo Hello deve essere impostata su: **AzureSearch**. | Sì |
| URL | URL per il servizio di ricerca di Azure hello. | Sì |
| key | Chiave di amministrazione per hello del servizio di ricerca di Azure. | Sì |

## <a name="dataset-properties"></a>Proprietà dei set di dati

Per un elenco completo delle sezioni e le proprietà disponibili per la definizione di set di dati, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo. Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati. Hello **typeProperties** sezione è diverso per ogni tipo di set di dati. sezione Hello typeProperties per un set di dati di tipo hello **AzureSearchIndex** è hello le proprietà seguenti:

| Proprietà | Descrizione | Obbligatorio |
| -------- | ----------- | -------- |
| type | proprietà di tipo Hello deve essere impostata troppo**AzureSearchIndex**.| Sì |
| indexName | Nome dell'indice di ricerca di Azure hello. Data Factory di creare l'indice di hello. indice di Hello deve esistere in ricerca di Azure. | Sì |


## <a name="copy-activity-properties"></a>Proprietà dell'attività di copia
Per un elenco completo delle sezioni e le proprietà disponibili per la definizione di attività, vedere hello [creazione di pipeline](data-factory-create-pipelines.md) articolo. Proprietà come nome, descrizione, tabelle di input e output e criteri diversi sono disponibili per tutti i tipi di attività. Mentre le proprietà disponibili nella sezione typeProperties hello variano in base a ogni tipo di attività. Per attività di copia, variano a seconda dei tipi di hello di origini e sink.

Per attività di copia, quando il sink di hello è di tipo hello **AzureSearchIndexSink**, hello le proprietà seguenti sono disponibile nella sezione typeProperties:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| -------- | ----------- | -------------- | -------- |
| WriteBehavior | Specifica se toomerge o Sostituisci quando un documento già presente nell'indice hello. Vedere hello [WriteBehavior proprietà](#writebehavior-property).| Merge (impostazione predefinita)<br/>Carica| No |
| WriteBatchSize | Carica i dati nell'indice di ricerca di Azure hello quando viene raggiunto writeBatchSize raggiungerà le dimensioni di buffer hello. Vedere hello [viene raggiunto WriteBatchSize proprietà](#writebatchsize-property) per informazioni dettagliate. | 1 too1, 000. Il valore predefinito è 1000. | No |

### <a name="writebehavior-property"></a>Proprietà WriteBehavior
Durante la scrittura di dati, AzureSearchSink esegue operazioni di upsert. In altre parole, quando si scrive un documento, se la chiave di documento hello esiste già nell'indice di ricerca di Azure hello, ricerca di Azure Aggiorna documento esistente hello anziché generare un'eccezione di conflitto.

Hello AzureSearchSink fornisce hello seguenti due comportamenti upsert (utilizzando il SDK AzureSearch):

- **Merge**: combinare tutte le colonne di hello nel documento nuovo hello con hello uno esistente. Per le colonne con valore null nel nuovo documento hello, viene mantenuto il valore di hello in hello uno esistente.
- **Caricare**: sostituisce documento nuovo hello hello uno esistente. Per le colonne non è specificate nel documento nuovo hello, hello è impostato toonull se è presente un valore non null nel documento di hello esistente o non.

comportamento predefinito di Hello **Merge**.

### <a name="writebatchsize-property"></a>Proprietà WriteBatchSize
Il servizio Ricerca di Azure supporta la scrittura di documenti come batch. Un batch può contenere 1 too1, azioni 000. Un'azione gestisce un'operazione di caricamento/merge hello di tooperform documento.

### <a name="data-type-support"></a>Supporto dei tipi di dati
Hello nella tabella seguente specifica se un tipo di dati di ricerca di Azure è supportato o meno.

| Tipo di dati di Ricerca di Azure | Supportato nel sink di Ricerca di Azure |
| ---------------------- | ------------------------------ |
| String | S |
| Int32 | S |
| Int64 | S |
| Double | S |
| Boolean | S |
| DataTimeOffset | S |
| String Array | N |
| GeographyPoint | N |

## <a name="json-example-copy-data-from-on-premises-sql-server-tooazure-search-index"></a>Esempio JSON: copiare i dati dall'indice di ricerca tooAzure SQL Server locale

Hello nel seguente esempio viene illustrato:

1.  Un servizio collegato di tipo [AzureSearch](#linked-service-properties).
2.  Un servizio collegato di tipo [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).
3.  Un [set di dati](data-factory-create-datasets.md) di tipo [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).
4.  Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureSearchIndex](#dataset-properties).
4.  Una [pipeline](data-factory-create-pipelines.md) con un'attività di copia che usa [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) e [AzureSearchIndexSink](#copy-activity-properties).

esempio Hello copia i dati delle serie temporali da un indice di ricerca di Azure locale tooan database di SQL Server ogni ora. proprietà JSON Hello utilizzate in questo esempio sono descritti nelle sezioni riportate di seguito esempi di hello.

Come primo passaggio, configurare il gateway di gestione dati hello nel computer locale. istruzioni di Hello presenti hello [lo spostamento dei dati tra le sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) articolo.

**Servizio collegato Ricerca di Azure**

```JSON
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

**Servizio collegato di SQL Server**

```JSON
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```

**Set di dati input di SQL Server**

esempio Hello presuppone di aver creato una tabella "MyTable" in SQL Server e contiene una colonna denominata "timestampcolumn" per i dati della serie temporale. È possibile eseguire query su più tabelle all'interno di hello stesso database con un singolo set di dati, ma una singola tabella deve essere utilizzato per typeProperty tableName hello del dataset.

L'impostazione "external": "true" informa il servizio Data Factory hello set di dati è esterna toohello data factory e non viene generato da un'attività nella data factory di hello.

```JSON
{
  "name": "SqlServerDataset",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
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

**Set di dati di output di Ricerca di Azure**

Hello esempio copie dei dati tooan Azure indice di ricerca denominato **prodotti**. Data Factory di creare l'indice di hello. hello tootest di esempio, creare un indice con questo nome. Creare l'indice di ricerca di Azure hello con hello stesso numero di colonne come set di dati input hello. Vengono aggiunte nuove voci toohello indice di ricerca di Azure ogni ora.

```JSON
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties" : {
            "indexName": "products",
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
   }
}
```

**Attività di copia in una pipeline con un'origine SQL e il sink dell'indice di Ricerca di Azure:**

pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e viene pianificata toorun ogni ora. Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**SqlSource** e **sink** tipo è stato impostato troppo**AzureSearchIndexSink**. query SQL Hello specificata per hello **SqlReaderQuery** proprietà consente di selezionare dati hello hello oltre toocopy ora.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoAzureSearchIndex",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSearchIndexDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "AzureSearchIndexSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```

Se si copiano dati da un archivio dati cloud a Ricerca di Azure, la proprietà `executionLocation` è obbligatoria. frammento di codice JSON seguente Hello Mostra hello modifica necessaria nell'attività di copia `typeProperties` come esempio. Per informazioni sui valori supportati e altri dettagli, vedere la sezione [Copiare dati tra archivi dati cloud](data-factory-data-movement-activities.md#global).

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```


## <a name="copy-from-a-cloud-source"></a>Copiare da un'origine cloud
Se si copiano dati da un archivio dati cloud a Ricerca di Azure, la proprietà `executionLocation` è obbligatoria. frammento di codice JSON seguente Hello Mostra hello modifica necessaria nell'attività di copia `typeProperties` come esempio. Per informazioni sui valori supportati e altri dettagli, vedere la sezione [Copiare dati tra archivi dati cloud](data-factory-data-movement-activities.md#global).

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```

È anche possibile mappare le colonne di origine toocolumns di set di dati dal set di dati di sink nella definizione di attività di copia hello. Per altre informazioni, vedere [Mapping delle colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Prestazioni e ottimizzazione  
Vedere hello [ottimizzazione Guida e alle prestazioni di attività di copia](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) e i vari modi toooptimize è.

## <a name="next-steps"></a>Passaggi successivi
Vedere hello seguenti articoli:

* [Esercitazione dell'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per le istruzioni dettagliate della creazione di una pipeline con un'attività di copia.
