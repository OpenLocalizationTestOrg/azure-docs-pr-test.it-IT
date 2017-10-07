---
title: aaaMove dati da e verso tabelle di Azure | Documenti Microsoft
description: Informazioni su come toomove dati in o dall'archiviazione tabelle di Azure usando Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 07b046b1-7884-4e57-a613-337292416319
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 3dc3da6d88854674a9108b600534bc5d07575f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-table-using-azure-data-factory"></a>Spostare dati tooand dalla tabella di Azure usando Azure Data Factory
Questo articolo spiega come toouse hello attività di copia dei dati di Azure Data Factory toomove a/da Archiviazione tabelle di Azure. È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello. 

È possibile copiare dati da qualsiasi origine supportati dati archiviano tooAzure archiviazione tabelle o da dati di archiviazione tabelle di Azure supportata tooany sink archivio. Per un elenco di archivi dati come origini o sink è supportato dall'attività di copia hello, vedere hello [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabella. 

## <a name="getting-started"></a>introduttiva
È possibile creare una pipeline con l'attività di copia che sposta i dati da e verso un'archiviazione tabelle di Azure usando diversi strumenti/API.

toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**. Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.

È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**. Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia. 

Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti: 

1. Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.
2. Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello. 
3. Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output. 

Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente. Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.  Per esempi con definizioni di JSON per le entità Data Factory toocopy utilizzati dati da e verso un archivio tabelle di Azure, vedere [esempi JSON](#json-examples) sezione di questo articolo. 

Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che vengono utilizzati toodefine Data Factory entità specifiche tooAzure archiviazione tabelle: 

## <a name="linked-service-properties"></a>Proprietà del servizio collegato
Esistono due tipi di servizi collegati è possibile utilizzare toolink un blob di Azure storage tooan data factory di Azure. I due tipi di servizi sono il servizio collegato **AzureStorage** e il servizio collegato **AzureStorageSas**. Hello servizio collegato di archiviazione di Azure fornisce data factory di hello con accesso globale toohello di archiviazione di Azure. Mentre, hello Azure archiviazione SAS (firma di accesso condiviso) collegati servizio fornisce data factory di hello con accesso limitato/scadenza toohello di archiviazione di Azure. Non esistono altre differenze tra questi due servizi collegati. Scegliere servizio hello collegato alle proprie esigenze. Hello nelle sezioni seguenti vengono forniscono ulteriori informazioni su questi due servizi collegati.

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a>Proprietà dei set di dati
Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo. Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.

sezione typeProperties Hello è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello. Hello **typeProperties** sezione per hello set di dati di tipo **AzureTable** è hello le proprietà seguenti.

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| tableName |Nome della tabella hello nell'istanza di Database della tabella di Azure hello che il servizio collegato fa riferimento a. |Sì. Quando un tableName viene specificato senza un azureTableSourceQuery, tutti i record dalla tabella hello vengono copiati toohello destinazione. Se viene specificato anche un azureTableSourceQuery, i record dalla tabella hello che soddisfa la query hello sono destinazione toohello copiato. |

### <a name="schema-by-data-factory"></a>Schema da Data Factory
Per gli archivi dati privi di schema, ad esempio tabelle di Azure, servizio Data Factory hello viene dedotto schema hello in uno dei seguenti modi hello:

1. Se si specifica la struttura hello dei dati tramite hello **struttura** proprietà nella definizione di set di dati hello, hello servizio Data Factory rispetta questa struttura come schema hello. In questo caso, se una riga non contiene un valore per una colonna, viene inserito un valore null.
2. Se non si specifica la struttura hello dei dati tramite hello **struttura** proprietà nella definizione di set di dati hello, Data Factory di inferenza dello schema di hello utilizzando prima riga hello nei dati hello. In questo caso, se hello prima riga contiene schema completo hello, alcune colonne vengono persi nel risultato hello dell'operazione di copia.

Pertanto, per le origini dati privi di schema consigliata hello è struttura hello toospecify dei dati tramite hello **struttura** proprietà.

## <a name="copy-activity-properties"></a>Proprietà dell'attività di copia
Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo. Proprietà quali nome, descrizione, criteri e set di dati di input e di output sono disponibili per tutti i tipi di attività.

Le proprietà disponibili nella sezione typeProperties hello di attività hello hello invece variano in base a ogni tipo di attività. Per attività di copia, variano a seconda dei tipi di hello di origini e sink.

**AzureTableSource** supporta hello le proprietà nella sezione typeProperties seguenti:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| AzureTableSourceQuery |Utilizzare i dati di tooread hello query personalizzata. |Stringa di query della tabella di Azure. Vedere gli esempi nella sezione successiva hello. |No. Quando un tableName viene specificato senza un azureTableSourceQuery, tutti i record dalla tabella hello vengono copiati toohello destinazione. Se viene specificato anche un azureTableSourceQuery, i record dalla tabella hello che soddisfa la query hello sono destinazione toohello copiato. |
| azureTableSourceIgnoreTableNotFound |Indica se ignorare hello eccezione della tabella non esiste. |TRUE<br/>FALSE |No |

### <a name="azuretablesourcequery-examples"></a>esempi di azureTableSourceQuery
Se la colonna della tabella di Azure è di tipo stringa:

```JSON
azureTableSourceQuery": "$$Text.Format('PartitionKey ge \\'{0:yyyyMMddHH00_0000}\\' and PartitionKey le \\'{0:yyyyMMddHH00_9999}\\'', SliceStart)"
```

Se la colonna della tabella di Azure è di tipo datetime:

```JSON
"azureTableSourceQuery": "$$Text.Format('DeploymentEndTime gt datetime\\'{0:yyyy-MM-ddTHH:mm:ssZ}\\' and DeploymentEndTime le datetime\\'{1:yyyy-MM-ddTHH:mm:ssZ}\\'', SliceStart, SliceEnd)"
```

**AzureTableSink** supporta hello le proprietà nella sezione typeProperties seguenti:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| azureTableDefaultPartitionKeyValue |Partizione chiave valore predefinito che può essere usato dal sink hello. |Valore stringa. |No |
| azureTablePartitionKeyName |Nome della colonna hello i cui valori vengono utilizzati come chiavi di partizione. Se non specificato, AzureTableDefaultPartitionKeyValue viene utilizzato come chiave di partizione hello. |Nome colonna. |No |
| azureTableRowKeyName |Nome della colonna hello i cui valori di colonna vengono utilizzati come chiave di riga. Se non specificato, usare un GUID per ogni riga. |Nome colonna. |No |
| azureTableInsertType |Hello modalità tooinsert i dati in tabelle di Azure.<br/><br/>Questa proprietà controlla se le righe esistenti nella tabella di output di hello con le chiavi di riga e di partizione corrispondenti hanno valori di sostituzione o unione. <br/><br/>toolearn sul funzionano di queste impostazioni (merge e la sostituzione), vedere [Insert o l'entità di tipo Merge](https://msdn.microsoft.com/library/azure/hh452241.aspx) e [Insert o sostituire entità](https://msdn.microsoft.com/library/azure/hh452242.aspx) argomenti. <br/><br> Questa impostazione si applica a livello di riga hello, non a livello tabella hello, e nessuna delle due opzioni consente di eliminare le righe nella tabella di output di hello che non esistono nell'input hello. |merge (impostazione predefinita)<br/>replace |No |
| writeBatchSize |Inserisce dati nella tabella di Azure hello quando hello di viene raggiunto writeBatchSize o writeBatchTimeout. |Numero intero (numero di righe) |No (valore predefinito: 10000) |
| writeBatchTimeout |Inserisce i dati in tabelle di Azure hello quando viene raggiunto writeBatchSize hello o writeBatchTimeout |Intervallo di tempo<br/><br/>Ad esempio: "00:20:00" (20 minuti) |No (valore di timeout predefinito del client predefinito toostorage 90 secondi) |

### <a name="azuretablepartitionkeyname"></a>azureTablePartitionKeyName
Eseguire il mapping di una colonna di destinazione tooa colonna di origine utilizzando proprietà JSON traduttore hello prima di poter utilizzare le colonne di destinazione hello come hello azureTablePartitionKeyName.

Nell'esempio seguente di hello, la colonna di origine DivisionID è la colonna di destinazione mappata toohello: DivisionID.  

```JSON
"translator": {
    "type": "TabularTranslator",
    "columnMappings": "DivisionID: DivisionID, FirstName: FirstName, LastName: LastName"
}
```
Hello DivisionID viene specificato come chiave di partizione hello.

```JSON
"sink": {
    "type": "AzureTableSink",
    "azureTablePartitionKeyName": "DivisionID",
    "writeBatchSize": 100,
    "writeBatchTimeout": "01:00:00"
}
```
## <a name="json-examples"></a>Esempi JSON
Negli esempi seguenti Hello forniscono definizioni JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Vengono visualizzate come toocopy tooand di dati da Archiviazione tabelle di Azure e Database di Blob di Azure. Tuttavia, i dati possono essere copiati **direttamente** da qualsiasi hello origini tooany di sink hello è supportato. Per ulteriori informazioni, vedere sezione hello "archivi di dati supportati e formati" in [spostare i dati utilizzando l'attività di copia](data-factory-data-movement-activities.md).

## <a name="example-copy-data-from-azure-table-tooazure-blob"></a>Esempio: Copiare i dati da tabelle di Azure tooAzure Blob
Hello nel seguente esempio viene illustrato:

1. Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (usato sia per tabelle che per BLOB).
2. Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureTable](#dataset-properties).
3. Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Hello [pipeline](data-factory-create-pipelines.md) con attività di copia che utilizza [AzureTableSource](#activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

esempio Hello copia i dati appartenenti a partizione predefinita toohello in un blob tooa tabelle di Azure ogni ora. proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.

**Servizio collegato di archiviazione di Azure:**

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
Azure Data Factory supporta due tipi di servizi collegati di Archiviazione di Azure, **AzureStorage** e **AzureStorageSas**. Per hello prima, specificare una stringa di connessione hello che include una chiave dell'account di hello e per la versione più recente di hello, specificare hello Uri di firma di accesso condiviso (SAS). Per informazioni dettagliate, vedere la sezione [Servizi collegati](#linked-service-properties) .  

**Set di dati di input di tabelle di Azure**

esempio Hello presuppone di che aver creato una tabella "MyTable" nella tabella di Azure.

L'impostazione "external": "true" informa il servizio di Data Factory hello hello set di dati è esterna toohello data factory e non viene generato da un'attività nella data factory di hello.

```JSON
{
  "name": "AzureTableInput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
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

**Set di dati di output del BLOB di Azure:**

I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1). percorso della cartella Hello per blob hello viene valutato dinamicamente in base a ora di inizio hello della sezione hello che viene elaborato. percorso della cartella Hello Usa le parti di anno, mese, giorno e ore dell'ora di inizio hello.

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**Attività di copia in una pipeline con AzureTableSource e BlobSink:**

pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e viene pianificata toorun ogni ora. Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**AzureTableSource** e **sink** tipo è stato impostato troppo**BlobSink**. query SQL Hello specificata con **AzureTableSourceQuery** proprietà consente di selezionare dati hello dalla partizione predefinita hello toocopy ogni ora.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "AzureTabletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                      {
                        "name": "AzureTableInput"
                    }
                ],
                "outputs": [
                      {
                            "name": "AzureBlobOutput"
                      }
                ],
                "typeProperties": {
                      "source": {
                        "type": "AzureTableSource",
                        "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
                      },
                      "sink": {
                        "type": "BlobSink"
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

## <a name="example-copy-data-from-azure-blob-tooazure-table"></a>Esempio: Copiare i dati da Blob di Azure tooAzure tabella
Hello nel seguente esempio viene illustrato:

1. Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (usato sia per tabelle che per BLOB).
2. Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
3. Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureTable](#dataset-properties).
4. Hello [pipeline](data-factory-create-pipelines.md) con attività di copia che utilizza [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [AzureTableSink](#copy-activity-properties).

esempio Hello copia i dati delle serie temporali da una tabella di Azure di tooan blob di Azure ogni ora. proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.

**Servizio collegato di Archiviazione di Azure (per tabelle di Azure e BLOB):**

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

Azure Data Factory supporta due tipi di servizi collegati di Archiviazione di Azure, **AzureStorage** e **AzureStorageSas**. Per hello prima, specificare una stringa di connessione hello che include una chiave dell'account di hello e per la versione più recente di hello, specificare hello Uri di firma di accesso condiviso (SAS). Per informazioni dettagliate, vedere la sezione [Servizi collegati](#linked-service-properties) .

**Set di dati di input del BLOB di Azure:**

I dati vengono prelevati da un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1). Hello percorso e il nome della cartella per il blob hello vengono valutate in modo dinamico in base a ora di inizio hello della sezione hello che viene elaborato. percorso della cartella Hello utilizza year, month e parte del giorno dell'ora di inizio hello e nome del file utilizza parte ora hello hello ora di inizio. "external": "true" impostazione informa il servizio di Data Factory hello hello set di dati è esterna toohello data factory e non viene generato da un'attività nella data factory di hello.

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
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
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
      }
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

**Set di dati di output di tabelle di Azure**

esempio Hello copia tabella tooa dati denominata "MyTable" nella tabella di Azure. Creare una tabella di Azure con hello stesso numero di colonne nel modo previsto toocontain di file CSV Blob hello. Aggiunta di nuove righe nella tabella toohello ogni ora.

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**Copiare attività in una pipeline con BlobSource e AzureTableSink:**

pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e viene pianificata toorun ogni ora. Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**BlobSource** e **sink** tipo è stato impostato troppo**AzureTableSink**.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoTable",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureTableOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "AzureTableSink",
            "writeBatchSize": 100,
            "writeBatchTimeout": "01:00:00"
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
## <a name="type-mapping-for-azure-table"></a>Mapping dei tipi per tabelle di Azure
Come accennato in hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, attività di copia esegue le conversioni dai tipi di origine tipi toosink automatico con hello approccio in due passaggi.

1. Conversione dal tipo di origine nativa tipi too.NET
2. Eseguire la conversione da tipo di sink toonative tipo .NET

Quando si spostano dati troppo & dalla tabella di Azure, hello seguente [mapping definiti dal servizio tabelle di Azure](https://msdn.microsoft.com/library/azure/dd179338.aspx) vengono utilizzati dal tipo di too.NET tipi OData di tabella di Azure e viceversa.

| Tipo di dati OData | Tipo di .NET | Dettagli |
| --- | --- | --- |
| Edm.Binary |byte[] |Matrice di byte too64 KB. |
| Edm.Boolean |bool |Valore booleano. |
| Edm.DateTime |DateTime |Un valore a 64 bit espresso come Coordinated Universal Time (UTC). Hello supportato DateTime intervallo inizia a mezzanotte, 1 gennaio 1601 D.C. (C.E.), UTC. Hello intervallo termina il 31 dicembre 9999. |
| Edm.Double |double |Un valore a virgola mobile a 64 bit. |
| Edm.Guid |Guid |Un identificatore univoco globale a 128 bit. |
| Edm.Int32 |Int32 |Un valore integer a 32 bit. |
| Edm.Int64 |Int64 |Un valore integer a 64 bit. |
| Edm.String |String |Un valore con codifica UTF-16. I valori stringa possono essere too64 KB. |

### <a name="type-conversion-sample"></a>Esempio di conversione di tipo
Dopo l'esempio Hello è per la copia di dati da una tabella di tooAzure Blob di Azure con conversioni del tipo.

Si supponga di set di dati Blob hello è in formato CSV e contiene tre colonne. Uno di essi è una colonna datetime con un formato di data e ora personalizzate utilizzando nomi francesi abbreviati per giorno della settimana hello.

Definire il set di dati di hello origine Blob come indicato di seguito, insieme a definizioni di tipo per le colonne di hello.

```JSON
{
    "name": " AzureBlobInput",
    "properties":
    {
         "structure":
          [
                { "name": "userid", "type": "Int64"},
                { "name": "name", "type": "String"},
                { "name": "lastlogindate", "type": "Datetime", "culture": "fr-fr", "format": "ddd-MM-YYYY"}
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
        "external": true,
        "availability":
        {
            "frequency": "Hour",
            "interval": 1,
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
Dato il mapping dei tipi hello dal tipo di too.NET tipo OData di tabella di Azure, si definirebbe tabella hello in tabelle di Azure con hello seguente schema.

**Schema di tabelle di Azure:**

| Nome colonna | Tipo |
| --- | --- |
| userid |Edm.Int64 |
| name |Edm.String |
| lastlogindate |Edm.DateTime |

Successivamente, definire set di dati di hello tabelle di Azure come indicato di seguito. Sezione "struttura" toospecify con informazioni sul tipo hello non è necessario perché le informazioni sul tipo hello è già specificati in hello archivio dati sottostante.

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

In questo caso, Data Factory automaticamente conversioni di tipi tra i campi Datetime hello con il formato di data e ora personalizzate hello utilizzando le impostazioni cultura "fr-fr" hello, quando si spostano dati da Blob tooAzure tabella.

> [!NOTE]
> colonne toomap toocolumns set di dati di origine dal sink set di dati, vedere [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Ottimizzazione delle prestazioni
toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize, vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md).
