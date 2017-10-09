---
title: dati aaaCopy a/da Oracle utilizzando Data Factory | Documenti Microsoft
description: Informazioni su come dati toocopy a/da database Oracle in locale con Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3c20aa95-a8a1-4aae-9180-a6a16d64a109
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: adb6d5fbe38e18791616ac77e8179970bbea37fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tofrom-on-premises-oracle-using-azure-data-factory"></a>Copiare dati da/verso un database Oracle locale con Azure Data Factory
Questo articolo spiega come toouse hello attività di copia dei dati di Azure Data Factory toomove a/da un database Oracle locale. È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello.

## <a name="supported-scenarios"></a>Scenari supportati
È possibile copiare dati **da un database Oracle** toohello archivi dati seguenti:

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

È possibile copiare dati da archivi dati seguenti hello **database Oracle tooan**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="prerequisites"></a>Prerequisiti
Data Factory supporta origini di Oracle locale tooon connessione hello Gateway di gestione dati di utilizzo. Vedere [Gateway di gestione dati](data-factory-data-management-gateway.md) toolearn articolo sul Gateway di gestione dati e [spostare i dati da on-premise toocloud](data-factory-move-data-between-onprem-and-cloud.md) per istruzioni dettagliate su come configurare il gateway hello una pipeline di dati dati toomove.

Anche se hello Oracle è ospitato in una macchina virtuale IaaS di Azure, è necessario gateway. È possibile installare il gateway di hello in hello stessa VM IaaS come dati hello archiviare o su una macchina virtuale diversa, purché il gateway hello può connettersi toohello database.

> [!NOTE]
> Per suggerimenti sulla risoluzione di problemi correlati alla connessione o al gateway, vedere [Risoluzione dei problemi del gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) .

## <a name="supported-versions-and-installation"></a>Versioni supportate e installazione
Il connettore Oracle supporta due versioni di driver:

- **Driver Microsoft per Oracle (scelta consigliata)**: a partire dal Gateway di gestione dati versione 2.7, un driver Microsoft per Oracle viene installato automaticamente insieme ai gateway hello, pertanto non è necessario driver hello di handle tooadditionally in ordine tooestablish connettività tooOracle ed è possibile inoltre prestazioni migliori copia utilizzando questo driver. Di seguito sono indicate le versioni dei database di Oracle supportate:
    - Oracle 12c R1 (12.1)
    - Oracle 11g R1, R2 (11.1, 11.2)
    - Oracle 10g R1, R2 (10.1, 10.2)
    - Oracle 9i R1, R2 (9.0.1, 9.2)
    - Oracle 8i R3 (8.1.7)

> [!IMPORTANT]
> Driver Microsoft per Oracle supporta attualmente solo copia dati da Oracle ma non di scrivere tooOracle. E funzionalità di connessione di test nota hello nella scheda diagnostica Gateway di gestione dati non supporta questo driver. In alternativa, è possibile utilizzare la connettività hello hello Copia guidata toovalidate.
>

- **Provider di dati Oracle per .NET:** è anche possibile scegliere i dati di toocopy toouse Provider di dati Oracle da / tooOracle. Questo componente è incluso in [Oracle Data Access Components for Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/). Installare la versione appropriata hello (32/64 bit) nel computer di hello in cui è installato il gateway hello. [Il Provider di dati Oracle .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) possono accedere tooOracle Database 10g Release 2 o versione successiva.

    Se si sceglie "Installazione di XCopy", seguire i passaggi in hello Readme. htm. Si consiglia di che scegliere installazione hello con interfaccia utente (non-XCopy uno).

    Dopo avere installato il provider di hello, **riavviare** hello servizio host di Gateway di gestione dati nel computer utilizzando servizi applet (o) Gestione configurazione di Gateway di gestione di dati.  

Se si utilizza Copia guidata tooauthor hello copia pipeline, il tipo di driver hello sarà determinato automaticamente. Verrà usato il driver Microsoft per impostazione predefinita, a meno che la versione del gateway sia inferiore a 2.7 o se si sceglie Oracle come sink.

## <a name="getting-started"></a>Introduzione
È possibile creare una pipeline con l'attività di copia che sposta i dati da e verso un database di Oracle locale usando diversi strumenti/API.

toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**. Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.

È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**. Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia.

Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:

1. Creare una **data factory**. Una data factory può contenere una o più pipeline. 
2. Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory. Ad esempio, se si copiano dati da un tooan database Oralce archiviazione blob di Azure, è creare due servizi collegati toolink il database Oracle e la data factory tooyour account di archiviazione di Azure. Per le proprietà di servizio collegato che sono tooOracle specifici, vedere [servizio proprietà collegate](#linked-service-properties) sezione.
3. Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello. Nell'esempio hello indicato nell'ultimo passaggio hello creare una tabella di hello toospecify di set di dati nel database Oracle che contiene i dati di input hello. E, per creare un altro set di dati toospecify hello blob contenitore e cartella hello contenente hello dati copiati dal hello database Oracle. Per le proprietà di set di dati che sono tooOracle specifici, vedere [proprietà set di dati](#dataset-properties) sezione.
4. Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output. Nell'esempio hello indicato in precedenza, si usa OracleSource come un'origine e BlobSink come sink per attività di copia hello. Analogamente, se si sta copiando l'archiviazione Blob di Azure tooOracle Database, utilizzare BlobSource e OracleSink nell'attività di copia hello. Per le proprietà di attività di copia che sono tooOracle specifici database, vedere [copiare le proprietà dell'attività](#copy-activity-properties) sezione. Per informazioni dettagliate su come toouse un archivio dati come origine o un sink, fare clic sul collegamento di hello nella sezione precedente di hello per l'archivio dati. 

Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente. Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.  Per esempi con definizioni di JSON per le entità Data Factory toocopy utilizzati i dati in o da un database Oracle locale, vedere [esempi JSON](#json-examples-for-copying-data-to-and-from-oracle-database) sezione di questo articolo.

Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che sono utilizzati toodefine Data Factory entità:

## <a name="linked-service-properties"></a>Proprietà del servizio collegato
Hello nella tabella seguente fornisce una descrizione del servizio specifico tooOracle collegati gli elementi JSON.

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| type |proprietà di tipo Hello deve essere impostata su: **OnPremisesOracle** |Sì |
| driverType | Specificare i dati del driver toouse toocopy da / tooOracle Database. I valori consentiti sono **Microsoft** o **ODP** (impostazione predefinita). Per informazioni dettagliate sui driver, vedere la sezione [Versione e installazione supportate](#supported-versions-and-installation). | No |
| connectionString | Specificare l'istanza di Oracle Database toohello tooconnect necessarie informazioni per la proprietà connectionString hello. | Sì |
| gatewayName | Nome del gateway hello che viene utilizzato tooconnect toohello server Oracle locale |Sì |

**Esempio: mediante il driver Microsoft:**
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

**Esempio: mediante il driver ODP**

Fare riferimento troppo[questo sito](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) per hello formati consentito.

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

## <a name="dataset-properties"></a>Proprietà dei set di dati
Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo. Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati (Oracle, BLOB di Azure, tabelle di Azure e così via).

sezione typeProperties Hello è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello. sezione di typeProperties Hello per hello set di dati di tipo OracleTable ha hello le proprietà seguenti:

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| tableName |Nome della tabella hello nel Database Oracle per il servizio collegato di hello hello fa riferimento a. |No, se **oracleReaderQuery** di **OracleSource** è specificato |

## <a name="copy-activity-properties"></a>Proprietà dell'attività di copia
Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo. Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.

> [!NOTE]
> Hello attività di copia accetta un solo input e produce un solo output.

Mentre le proprietà disponibili nella sezione typeProperties hello dell'attività hello variano in base a ogni tipo di attività. Per attività di copia, variano a seconda dei tipi di hello di origini e sink.

### <a name="oraclesource"></a>OracleSource
Nell'attività di copia, l'origine hello è di tipo **OracleSource** hello le proprietà seguenti sono disponibile in **typeProperties** sezione:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| oracleReaderQuery |Utilizzare i dati di tooread hello query personalizzata. |Stringa di query SQL. Ad esempio: selezionare * da MyTable <br/><br/>Se non specificato, hello istruzione SQL eseguita: selezionare * from MyTable |No (se **tableName** di **set di dati** è specificato) |

### <a name="oraclesink"></a>OracleSink
**OracleSink** supporta hello le proprietà seguenti:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| writeBatchTimeout |Tempo di attesa per hello batch insert operazione toocomplete prima del timeout. |Intervallo di tempo<br/><br/> Ad esempio: "00:30:00" (30 minuti). |No |
| writeBatchSize |Inserisce dati in una tabella SQL hello quando viene raggiunto writeBatchSize raggiungerà le dimensioni di buffer hello. |Numero intero (numero di righe) |No (valore predefinito: 100) |
| sqlWriterCleanupScript |Specificare una query per attività di copia tooexecute modo che la pulitura dei dati di una sezione specifica. |Istruzione di query. |No |
| sliceIdentifierColumnName |Specificare il nome di colonna per attività di copia toofill con identificatore di sezione generati automaticamente, che è usato tooclean dei dati di una sezione specifica quando eseguire di nuovo. |Nome di colonna di una colonna con tipo di dati binario (32). |No |

## <a name="json-examples-for-copying-data-tooand-from-oracle-database"></a>Esempi JSON per la copia dei dati tooand da database Oracle
esempio Hello fornisce definizioni di JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Vengono visualizzate come dati toocopy da tooan Oracle database da e verso l'archiviazione Blob di Azure. Tuttavia, i dati possono essere copiati tooany di sink hello indicato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory.   

## <a name="example-copy-data-from-oracle-tooazure-blob"></a>Esempio: Copiare i dati da Oracle tooAzure Blob

esempio Hello è hello entità factory di dati seguenti:

1. Un servizio collegato di tipo [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).
2. Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Un [set di dati](data-factory-create-datasets.md) di input di tipo [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).
4. Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) come origine e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) come sink.

esempio Hello copia dati da una tabella in un blob di tooa database Oracle locale ogni ora. Per ulteriori informazioni su varie proprietà utilizzate nell'esempio hello, vedere la documentazione nelle sezioni riportate di seguito esempi di hello.

**Servizio collegato Oracle:**

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

**Servizio collegato di archiviazione BLOB di Azure:**

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

**Set di dati di input Oracle:**

esempio Hello presuppone di aver creato una tabella "MyTable" in Oracle e contiene una colonna denominata "timestampcolumn" per i dati della serie temporale.

L'impostazione "external": "true" informa il servizio di Data Factory hello hello set di dati è esterna toohello data factory e non viene generato da un'attività nella data factory di hello.

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2014-02-27T12:00:00",
            "frequency": "Hour"
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

I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1). Hello percorso e il nome della cartella per il blob hello vengono valutate in modo dinamico in base a ora di inizio hello della sezione hello che viene elaborato. percorso della cartella Hello Usa le parti di anno, mese, giorno e ore dell'ora di inizio hello.

```json
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

**Pipeline con attività di copia:**

pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e si svolge ogni ora toorun pianificato. Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**OracleSource** e **sink** tipo è stato impostato troppo**BlobSink**.  query SQL Hello specificata con **oracleReaderQuery** proprietà consente di selezionare dati hello hello oltre toocopy ora.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "OracletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": " OracleInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "OracleSource",
                        "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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

## <a name="example-copy-data-from-azure-blob-toooracle"></a>Esempio: Copiare i dati da Blob di Azure tooOracle
Questo esempio viene illustrato come toocopy dati da un tooan di archiviazione Blob di Azure in locale il database Oracle. Tuttavia, i dati possono essere copiati **direttamente** da una delle origini di hello indicate [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory.  

esempio Hello è hello entità factory di dati seguenti:

1. Un servizio collegato di tipo [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).
2. Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Un [set di dati](data-factory-create-datasets.md) di output di tipo [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).
5. Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) come origine e [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) come sink.

esempio Hello copia dati da una tabella tooa blob in un database Oracle locale ogni ora. Per ulteriori informazioni su varie proprietà utilizzate nell'esempio hello, vedere la documentazione nelle sezioni riportate di seguito esempi di hello.

**Servizio collegato Oracle:**
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
            User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

**Servizio collegato di archiviazione BLOB di Azure:**
```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

**Set di dati di input del BLOB di Azure**

I dati vengono prelevati da un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1). Hello percorso e il nome della cartella per il blob hello vengono valutate in modo dinamico in base a ora di inizio hello della sezione hello che viene elaborato. percorso della cartella Hello utilizza year, month e parte del giorno dell'ora di inizio hello e nome del file utilizza parte ora hello hello ora di inizio. "external": "true" impostazione informa il servizio di Data Factory hello che questa tabella è data factory di toohello esterni e non viene generata da un'attività nella data factory di hello.

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
            "frequency": "Day",
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

**Set di dati di output Oracle:**

esempio Hello presuppone che aver creato una tabella "MyTable" in Oracle. Creare la tabella hello in Oracle con hello stesso numero di colonne nel modo previsto toocontain di file CSV Blob hello. Aggiunta di nuove righe nella tabella toohello ogni ora.

```json
{
    "name": "OracleOutput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Day",
            "interval": "1"
        }
    }
}
```

**Pipeline con attività di copia:**

pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e viene pianificata toorun ogni ora. Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**BlobSource** hello e **sink** tipo è stato impostato troppo**OracleSink**.  

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-05T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
            {
                "name": "AzureBlobtoOracle",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "OracleOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "OracleSink"
                    }
                },
                "scheduler": {
                    "frequency": "Day",
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


## <a name="troubleshooting-tips"></a>Suggerimenti per la risoluzione dei problemi
### <a name="problem-1-net-framework-data-provider"></a>Problema 1: provider di dati .NET Framework

Verrà visualizzata la seguente hello **messaggio di errore**:

    Copy activity met invalid parameters: 'UnknownParameterName', Detailed message: Unable toofind hello requested .Net Framework Data Provider. It may not be installed”.  

**Possibili cause:**

1. non è stato installato il Provider di dati .NET Framework per Oracle Hello.
2. Hello Provider di dati .NET Framework per Oracle è stato installato too.NET Framework 2.0 e non viene trovato in cartelle hello .NET Framework 4.0.

**Risoluzione/Soluzione alternativa:**

1. Se non è stato installato il Provider .NET per Oracle, hello [installarlo](http://www.oracle.com/technetwork/topics/dotnet/downloads/) e ripetere scenario hello.
2. Se viene visualizzato il messaggio di errore hello anche dopo l'installazione del provider di hello, hello i passaggi seguenti:
   1. Aprire la configurazione macchina di .NET 2.0 dalla cartella hello: <system disk>: \Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.
   2. Cercare **Oracle Data Provider for .NET**, e dovrebbe essere in grado di toofind una voce, come illustrato nel seguente esempio in hello **System. Data** -> **DbProviderFactories**: "<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Provider di dati oracle per .NET" type="Oracle.DataAccess.Client.OracleClientFactory, Oracle.DataAccess, Version=2.112.3.0, Culture=neutral, PublicKeyToken=89b483f429c47342" />"
3. Copiare il file Machine. config di voce toohello nella seguente cartella v 4.0 hello: <system disk>: \Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config e modifica hello versione too4.xxx.x.x.
4. Installare "< percorso di installazione ODP.NET > \11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll" nella hello global assembly cache (GAC) eseguendo `gacutil /i [provider path]`. # # suggerimenti di risoluzione dei problemi

### <a name="problem-2-datetime-formatting"></a>Problema 2: formattazione di DateTime

Verrà visualizzata la seguente hello **messaggio di errore**:

    Message=Operation failed in Oracle Database with hello following error: 'ORA-01861: literal does not match format string'.,Source=,''Type=Oracle.DataAccess.Client.OracleException,Message=ORA-01861: literal does not match format string,Source=Oracle Data Provider for .NET,'.

**Risoluzione/Soluzione alternativa:**

Stringa di query hello tooadjust potrebbe essere necessario l'attività di copia in base alle modalità di configurazione delle date nel database Oracle, come illustrato nell'esempio hello (tramite la funzione to_date hello) esempio:

    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= to_date(\\'{0:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\')  AND timestampcolumn < to_date(\\'{1:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\') ', WindowStart, WindowEnd)"


## <a name="type-mapping-for-oracle"></a>Mapping dei tipi per Oracle
Come accennato in hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo attività di copia esegue le conversioni dai tipi di origine tipi toosink automatico con hello approccio passaggio 2:

1. Conversione dal tipo di origine nativa tipi too.NET
2. Eseguire la conversione da tipo di sink toonative tipo .NET

Quando si spostano dati da Oracle, hello seguendo i mapping viene utilizzato dal tipo too.NET tipo di dati Oracle e viceversa.

| Tipo di dati Oracle | Tipo di dati .NET Framework |
| --- | --- |
| BFILE |Byte[] |
| BLOB |Byte[] |
| CHAR |String |
| CLOB |String |
| DATE |DateTime |
| FLOAT |Decimal, String (se la precisione > 28) |
| INTEGER |Decimal, String (se la precisione > 28) |
| INTERVALLO anno tooMONTH |Int32 |
| INTERVALLO giorno tooSECOND |TimeSpan |
| LONG |String |
| LONG RAW |Byte[] |
| NCHAR |String |
| NCLOB |String |
| NUMBER |Decimal, String (se la precisione > 28) |
| NVARCHAR2 |String |
| RAW |Byte[] |
| ROWID |String |
| TIMESTAMP |DateTime |
| TIMESTAMP WITH LOCAL TIME ZONE |DateTime |
| TIMESTAMP WITH TIME ZONE |DateTime |
| UNSIGNED INTEGER |NUMBER |
| VARCHAR2 |String |
| XML |String |

> [!NOTE]
> Tipo di dati **intervallo anno tooMONTH** e **tooSECOND INTERVAL DAY** non sono supportati quando si utilizza il driver Microsoft.

## <a name="map-source-toosink-columns"></a>Eseguire il mapping di colonne di origine toosink
toolearn sui mapping delle colonne in toocolumns di set di dati di origine nel sink set di dati, vedere [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Lettura ripetibile da origini relazionali
Quando si copiano dati da archivi dati relazionali, tenere ripetibilità presente tooavoid risultati imprevisti. In Azure Data Factory è possibile rieseguire una sezione manualmente. È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore. Quando viene eseguito di nuovo una sezione in entrambi i casi, è necessario toomake assicurarsi che hello stessi dati non viene letto alcun altro aspetto come viene eseguita più volte una sezione. Vedere [Lettura ripetibile da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Ottimizzazione delle prestazioni
Vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.
