---
title: Spostare dati da e verso le tabelle di Azure | Documentazione Microsoft
description: Informazioni su come spostare i dati da e verso l'archiviazione tabelle di Azure mediante Data factory di Azure.
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
robots: noindex
ms.openlocfilehash: 6ddcde7e0c0f665eac9d749107db107e652c0be1
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="move-data-to-and-from-azure-table-using-azure-data-factory"></a>Spostare dati da e verso le tabelle di Azure mediante Data factory di Azure
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Versione 1 - Disponibilità generale](data-factory-azure-table-connector.md)
> * [Versione 2 - Anteprima](../connector-azure-table-storage.md)

> [!NOTE]
> Questo articolo si applica alla versione 1 di Data Factory, che è disponibile a livello generale. Se si usa la versione 2 del servizio Data Factory, disponibile in anteprima, vedere [Connettore di archiviazione tabelle di Azure nella versione 2](../connector-azure-table-storage.md).

Questo articolo illustra come usare l'attività di copia in Azure Data Factory per spostare i dati da e verso un'archiviazione tabelle di Azure. Si basa sull'articolo relativo alle [attività di spostamento dei dati](data-factory-data-movement-activities.md), che offre una panoramica generale dello spostamento dei dati con l'attività di copia. 

È possibile copiare i dati da qualsiasi archivio dati di origine supportato a un'archiviazione tabelle di Azure o da un'archiviazione tabelle di Azure a qualsiasi archivio dati sink supportato. Per un elenco degli archivi dati supportati come origini o sink dall'attività di copia, vedere la tabella relativa agli [archivi dati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats). 

## <a name="getting-started"></a>Introduzione
È possibile creare una pipeline con l'attività di copia che sposta i dati da e verso un'archiviazione tabelle di Azure usando diversi strumenti/API.

Il modo più semplice per creare una pipeline è usare la **Copia guidata**. Vedere [Esercitazione: Creare una pipeline usando la Copia guidata](data-factory-copy-data-wizard-tutorial.md) per la procedura dettagliata sulla creazione di una pipeline attenendosi alla procedura guidata per copiare i dati.

È possibile anche usare gli strumenti seguenti per creare una pipeline: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di Azure Resource Manager**, **API .NET** e **API REST**. Vedere l'[esercitazione sull'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per le istruzioni dettagliate sulla creazione di una pipeline con un'attività di copia. 

Se si usano gli strumenti o le API, eseguire la procedura seguente per creare una pipeline che sposta i dati da un archivio dati di origine a un archivio dati sink: 

1. Creare i **servizi collegati** per collegare gli archivi di dati di input e output alla data factory.
2. Creare i **set di dati** per rappresentare i dati di input e di output per le operazioni di copia. 
3. Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output. 

Quando si usa la procedura guidata, le definizioni JSON per queste entità di data factory (servizi, set di dati e pipeline collegati) vengono create automaticamente. Quando si usano gli strumenti o le API, ad eccezione delle API .NET, usare il formato JSON per definire le entità di data factory.  Per esempi con definizioni JSON per entità di data factory utilizzate per copiare i dati da e verso un'archiviazione tabelle di Azure, vedere la sezione degli [esempi JSON](#json-examples) in questo articolo. 

Le sezioni seguenti riportano informazioni dettagliate sulle proprietà JSON che vengono usate per definire entità di data factory specifiche di un'archiviazione tabelle di Azure: 

## <a name="linked-service-properties"></a>Proprietà del servizio collegato
Esistono due tipi di servizi collegati, che consentono di collegare un archivio BLOB di Azure a una data factory di Azure. I due tipi di servizi sono il servizio collegato **AzureStorage** e il servizio collegato **AzureStorageSas**. Il servizio collegato Archiviazione di Azure garantisce alla data factory l'accesso globale ad Archiviazione di Azure. Invece il servizio collegato Firma di accesso condiviso di Archiviazione di Azure garantisce alla data factory l'accesso limitato o a scadenza ad Archiviazione di Azure. Non esistono altre differenze tra questi due servizi collegati. Scegliere il servizio collegato più adatto alle proprie esigenze. Le sezioni seguenti forniscono altri dettagli su questi due servizi collegati.

[!INCLUDE [data-factory-azure-storage-linked-services](../../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a>Proprietà dei set di dati
Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione di set di dati, vedere l'articolo sulla [creazione di set di dati](data-factory-create-datasets.md). Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.

La sezione typeProperties è diversa per ogni tipo di set di dati e contiene informazioni sulla posizione dei dati nell'archivio dati. La sezione **typeProperties** per il set di dati di tipo **AzureTable** presenta le proprietà seguenti.

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| tableName |Nome della tabella nell'istanza del database di tabelle di Azure a cui fa riferimento il servizio collegato. |Sì. Quando si specifica tableName senza azureTableSourceQuery, tutti i record della tabella vengono copiati nella destinazione. Se si specifica anche azureTableSourceQuery, i record della tabella che soddisfa la query vengono copiati nella destinazione. |

### <a name="schema-by-data-factory"></a>Schema da Data Factory
Per gli archivi di dati privi di schema, ad esempio Tabella di Azure, il servizio Data Factory deduce lo schema in uno dei modi seguenti:

1. Se si specifica la struttura dei dati usando la proprietà **structure** nella definizione del set di dati, il servizio Data Factory considera la struttura come schema. In questo caso, se una riga non contiene un valore per una colonna, viene inserito un valore null.
2. Se non si specifica la struttura dei dati usando la proprietà **structure** nella definizione del set di dati, Data Factory deduce lo schema usando la prima riga di dati. In questo caso, se la prima riga non contiene lo schema completo, alcune colonne non sono presenti nel risultato dell'operazione di copia.

Di conseguenza, per le origini dati prive di schema, la procedura consigliata consiste nello specificare la struttura dei dati usando la proprietà **structure** .

## <a name="copy-activity-properties"></a>Proprietà dell'attività di copia
Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione delle attività, fare riferimento all'articolo [Creazione di pipeline](data-factory-create-pipelines.md). Proprietà quali nome, descrizione, criteri e set di dati di input e di output sono disponibili per tutti i tipi di attività.

Le proprietà disponibili nella sezione typeProperties dell'attività variano invece in base al tipo di attività. Per l'attività di copia variano in base ai tipi di origine e sink.

**AzureTableSource** supporta le seguenti proprietà della sezione typeProperties:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| AzureTableSourceQuery |Usare la query personalizzata per leggere i dati. |Stringa di query della tabella di Azure. Vedere gli esempi nella sezione successiva. |No. Quando si specifica tableName senza azureTableSourceQuery, tutti i record della tabella vengono copiati nella destinazione. Se si specifica anche azureTableSourceQuery, i record della tabella che soddisfa la query vengono copiati nella destinazione. |
| azureTableSourceIgnoreTableNotFound |Indica se ignorare l'eccezione di tabella inesistente. |TRUE<br/>FALSE |No |

### <a name="azuretablesourcequery-examples"></a>esempi di azureTableSourceQuery
Se la colonna della tabella di Azure è di tipo stringa:

```JSON
azureTableSourceQuery": "$$Text.Format('PartitionKey ge \\'{0:yyyyMMddHH00_0000}\\' and PartitionKey le \\'{0:yyyyMMddHH00_9999}\\'', SliceStart)"
```

Se la colonna della tabella di Azure è di tipo datetime:

```JSON
"azureTableSourceQuery": "$$Text.Format('DeploymentEndTime gt datetime\\'{0:yyyy-MM-ddTHH:mm:ssZ}\\' and DeploymentEndTime le datetime\\'{1:yyyy-MM-ddTHH:mm:ssZ}\\'', SliceStart, SliceEnd)"
```

**AzureTableSink** supporta le seguenti proprietà della sezione typeProperties:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| azureTableDefaultPartitionKeyValue |Valore predefinito della chiave di partizione che può essere usato dal sink. |Valore stringa. |No |
| azureTablePartitionKeyName |Specificare il nome della colonna i cui valori vengono usati come chiavi di partizione. Se non specificato, AzureTableDefaultPartitionKeyValue viene usato come chiave di partizione. |Nome colonna. |No |
| azureTableRowKeyName |Specificare il nome della colonna i cui valori vengono usati come chiavi di riga. Se non specificato, usare un GUID per ogni riga. |Nome colonna. |No |
| azureTableInsertType |Modalità di inserimento dei dati in una tabella di Azure.<br/><br/>Questa proprietà verifica se per le righe esistenti nella tabella di output con chiavi di partizione e di riga corrispondenti i valori vengono sostituiti o uniti. <br/><br/>Per scoprire come funzionano queste impostazioni (unione e sostituzione), vedere gli argomenti [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) (Inserire o unire un'entità) e [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) (Inserire o sostituire un'entità). <br/><br> Queste impostazioni vengono applicate a livello di riga, non a livello di tabella, e nessuna delle due opzioni elimina le righe della tabella di output che non esistono nell'input. |merge (impostazione predefinita)<br/>replace |No |
| writeBatchSize |Inserisce dati nella tabella di Azure quando viene raggiunto il writeBatchSize o writeBatchTimeout. |Numero intero (numero di righe) |No (valore predefinito: 10000) |
| writeBatchTimeout |Inserisce i dati nella tabella di Azure quando viene raggiunto writeBatchSize o writeBatchTimeout |Intervallo di tempo<br/><br/>Ad esempio: "00:20:00" (20 minuti) |No. (il valore predefinito è il timeout del client di archiviazione pari a 90 secondi) |

### <a name="azuretablepartitionkeyname"></a>azureTablePartitionKeyName
Eseguire il mapping di una colonna di origine a una colonna di destinazione usando la funzione di conversione proprietà JSON prima di poter usare la colonna di destinazione come azureTablePartitionKeyName.

Nell'esempio seguente, la colonna di origine DivisionID viene eseguito il mapping alla colonna di destinazione: DivisionID.  

```JSON
"translator": {
    "type": "TabularTranslator",
    "columnMappings": "DivisionID: DivisionID, FirstName: FirstName, LastName: LastName"
}
```
DivisionID è specificato come chiave di partizione.

```JSON
"sink": {
    "type": "AzureTableSink",
    "azureTablePartitionKeyName": "DivisionID",
    "writeBatchSize": 100,
    "writeBatchTimeout": "01:00:00"
}
```
## <a name="json-examples"></a>Esempi JSON
Gli esempi seguenti forniscono le definizioni JSON di esempio da usare per creare una pipeline con il [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Tali esempi mostrano come copiare dati in e dall'archivio tabelle di Azure e in e dal database BLOB di Azure. I dati possono tuttavia essere copiati **direttamente** da qualsiasi origine a qualsiasi sink supportato. Per altre informazioni, vedere la sezione "Archivi dati e formati supportati" in [Spostare dati con l'attività di copia](data-factory-data-movement-activities.md).

## <a name="example-copy-data-from-azure-table-to-azure-blob"></a>Esempio: Copiare dati da tabelle di Azure al BLOB di Azure
L'esempio seguente mostra:

1. Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (usato sia per tabelle che per BLOB).
2. Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureTable](#dataset-properties).
3. Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. La [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [AzureTableSource](#activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Nell'esempio vengono copiati i dati appartenenti alla partizione predefinita in una tabella di Azure a un BLOB ogni ora. Le proprietà JSON usate in questi esempi sono descritte nelle sezioni riportate dopo gli esempi.

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
Azure Data Factory supporta due tipi di servizi collegati di Archiviazione di Azure, **AzureStorage** e **AzureStorageSas**. Per il primo specificare la stringa di connessione che include la chiave dell'account e per il secondo specificare l'URI di firma di accesso condiviso. Per informazioni dettagliate, vedere la sezione [Servizi collegati](#linked-service-properties) .  

**Set di dati di input di tabelle di Azure**

Nell'esempio si presuppone di aver creato una tabella "MyTable" in tabelle di Azure.

Impostando "external" su "true" si comunica al servizio Data Factory che il set di dati è esterno alla data factory e non è prodotto da un'attività al suo interno.

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

I dati vengono scritti in un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1). Il percorso della cartella per il BLOB viene valutato dinamicamente in base all'ora di inizio della sezione in fase di elaborazione. Il percorso della cartella usa le parti anno, mese, giorno e ora dell'ora di inizio.

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

La pipeline contiene un'attività di copia configurata per usare i set di dati di input e output ed è programmata per essere eseguita ogni ora. Nella definizione JSON della pipeline, il tipo di **origine** è impostato su **AzureTableSource** e il tipo di **sink** è impostato su **BlobSink**. La query SQL specificata con la proprietà **AzureTableSourceQuery** seleziona i dati da copiare dalla partizione predefinita ogni ora.

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

## <a name="example-copy-data-from-azure-blob-to-azure-table"></a>Esempio: Copiare i dati dal BLOB di Azure in tabelle di Azure
L'esempio seguente mostra:

1. Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (usato sia per tabelle che per BLOB).
2. Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
3. Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureTable](#dataset-properties).
4. La [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [AzureTableSink](#copy-activity-properties).

L'esempio copia i dati di una serie temporale da un BLOB di Azure a una tabella di Azure ogni ora. Le proprietà JSON usate in questi esempi sono descritte nelle sezioni riportate dopo gli esempi.

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

Azure Data Factory supporta due tipi di servizi collegati di Archiviazione di Azure, **AzureStorage** e **AzureStorageSas**. Per il primo specificare la stringa di connessione che include la chiave dell'account e per il secondo specificare l'URI di firma di accesso condiviso. Per informazioni dettagliate, vedere la sezione [Servizi collegati](#linked-service-properties) .

**Set di dati di input del BLOB di Azure:**

I dati vengono prelevati da un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1). Il percorso della cartella e il nome del file per il BLOB vengono valutati dinamicamente in base all'ora di inizio della sezione in fase di elaborazione. Il percorso della cartella usa le parti anno, mese, e giorno dell'ora di inizio e il nome del file usa la parte dell'ora di inizio relativa all'ora. L'impostazione di "external" su "true" comunica al servizio Data Factory che il set di dati è esterno a Data Factory e non è prodotto da un'attività al suo interno.

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

Nell’esempio vengono copiati dati in una tabella denominata "MyTable" in tabelle di Azure. Creare una tabella di Azure con il numero di colonne atteso nel file CSV del BLOB. Alla tabella vengono aggiunte nuove righe ogni ora.

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

La pipeline contiene un'attività di copia configurata per usare i set di dati di input e output ed è programmata per essere eseguita ogni ora. Nella definizione JSON della pipeline, il tipo di **origine** è impostato su **BlobSource** e il tipo di **sink** è impostato su **AzureTableSink**.

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
Come accennato nell'articolo sulle [attività di spostamento dei dati](data-factory-data-movement-activities.md) , l'attività di copia esegue conversioni di tipo automatiche dai tipi di origine ai tipi di sink con l'approccio in due passaggi seguente:

1. Conversione dai tipi di origine nativi al tipo .NET
2. Conversione dal tipo .NET al tipo di sink nativo

Quando si spostano i dati da e verso tabelle di Azure, i seguenti [mapping definiti dal servizio tabelle di Azure](https://msdn.microsoft.com/library/azure/dd179338.aspx) vengono usati dai tipi di OData di tabelle di Azure al tipo di .NET e viceversa.

| Tipo di dati OData | Tipo di .NET | Dettagli |
| --- | --- | --- |
| Edm.Binary |byte[] |Una matrice di byte di dimensioni fino a 64 KB. |
| Edm.Boolean |bool |Valore booleano. |
| Edm.DateTime |DateTime |Un valore a 64 bit espresso come Coordinated Universal Time (UTC). L'intervallo DateTime supportato inizia dalle 00:00, 1 gennaio, 1601 D.C. (C.E.), UTC. L'intervallo termina il 31 dicembre 9999. |
| Edm.Double |double |Un valore a virgola mobile a 64 bit. |
| Edm.Guid |Guid |Un identificatore univoco globale a 128 bit. |
| Edm.Int32 |Int32 |Un valore integer a 32 bit. |
| Edm.Int64 |Int64 |Un valore integer a 64 bit. |
| Edm.String |String |Un valore con codifica UTF-16. I valori delle stringhe possono essere di dimensioni fino a 64 KB. |

### <a name="type-conversion-sample"></a>Esempio di conversione di tipo
L'esempio seguente riguarda la copia dei dati da un BLOB di Azure a tabelle di Azure con conversioni del tipo.

Si supponga che il set di dati BLOB sia in formato CSV e contenga tre colonne. Una di esse è una colonna datetime con un formato datetime personalizzato che utilizza nomi abbreviati francesi per il giorno della settimana.

Definire il set di dati di origine BLOB come indicato di seguito e le definizioni di tipo per le colonne.

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
Dato il precedente mapping dei tipi dal tipo OData di tabelle di Azure al tipo di .NET è possibile definire la tabella in tabelle di Azure con lo schema seguente.

**Schema di tabelle di Azure:**

| Nome colonna | Tipo |
| --- | --- |
| userid |Edm.Int64 |
| name |Edm.String |
| lastlogindate |Edm.DateTime |

Quindi si definisce il set di dati di tabelle di Azure come indicato di seguito. Non è necessario specificare la sezione "struttura" con informazioni sul tipo perché le informazioni sul tipo sono già state specificate nell'archivio dati sottostante.

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

In questo caso Data Factory esegue automaticamente la conversione del tipo incluso il campo Datetime con il formato data personalizzato usando "fr-fr" quando si spostano dati da BLOB a tabelle di Azure.

> [!NOTE]
> Per eseguire il mapping dal set di dati di origine alle colonne del set di dati sink, vedere [Mapping delle colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Ottimizzazione delle prestazioni
Per informazioni sui fattori chiave che influiscono sulle prestazioni dello spostamento dei dati, ovvero dell'attività di copia, in Azure Data Factory e sui vari modi per ottimizzare tali prestazioni, vedere la [Guida alle prestazioni dell'attività di copia e all'ottimizzazione](data-factory-copy-activity-performance.md).
