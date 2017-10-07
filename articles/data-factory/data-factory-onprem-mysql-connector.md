---
title: aaaMove dati da MySQL con Data Factory di Azure | Documenti Microsoft
description: Informazioni su come toomove dati da MySQL database usando Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 452f4fce-9eb5-40a0-92f8-1e98691bea4c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: jingwang
ms.openlocfilehash: 3ffe969e42ce1a54b265c4739df43fdc594ea891
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-mysql-using-azure-data-factory"></a>Spostare i dati da MySQL mediante Data factory di Azure
Questo articolo spiega come toouse hello attività di copia dei dati toomove Data Factory di Azure da un database MySQL locale. È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello.

È possibile copiare dati da un archivio di dati di on-premise MySQL dati archivio tooany supportati sink. Per un elenco di dati supportati archivi come sink dall'attività di copia hello, vedere hello [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabella. Data factory di attualmente supporta solo lo spostamento di dati da un MySQL archiviano tooother archivi di dati, ma non per lo spostamento dei dati da altro archivio dati di MySQL tooan di archivi di dati. 

## <a name="prerequisites"></a>Prerequisiti
Servizio Data Factory supporta origini di MySQL locale tooon connessione hello Gateway di gestione dati di utilizzo. Vedere [lo spostamento dei dati tra le sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn articolo sul Gateway di gestione dati e istruzioni dettagliate su come configurare il gateway hello.

Gateway è necessario anche se il database di MySQL hello è ospitato in una macchina virtuale IaaS di Azure (VM). È possibile installare il gateway di hello in hello stessa macchina virtuale come dati hello archiviare o su una macchina virtuale diversa, purché il gateway hello può connettersi toohello database.

> [!NOTE]
> Per suggerimenti sulla risoluzione di problemi correlati alla connessione o al gateway, vedere [Risoluzione dei problemi del gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) .

## <a name="supported-versions-and-installation"></a>Versioni supportate e installazione
Per Gateway di gestione dati tooconnect toohello MySQL Database, è necessario hello tooinstall [MySQL Connector/Net per Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (versione 6.6.5 o versione successiva) hello nella stesso sistema come hello Gateway di gestione dati. Sono supportate le versioni di MySQL a partire dalla 5.1.

> [!TIP]
> Se si riscontra errori "Autenticazione non riuscita perché è chiuso parte remota hello flusso di trasporto hello.", è consigliabile hello tooupgrade versione toohigher MySQL Connector/Net.

## <a name="getting-started"></a>introduttiva
È possibile creare una pipeline con l'attività di copia che sposta i dati da un archivio dati Cassandra usando diversi strumenti/API. 

- toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**. Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati. 
- È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**. Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia. 

Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:

1. Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.
2. Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello. 
3. Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output. 

Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente. Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.  Per un esempio con le definizioni di JSON per le entità Data Factory dati toocopy utilizzato da un archivio dati di MySQL in locale, vedere [esempio JSON: copiare i dati da MySQL tooAzure Blob](#json-example-copy-data-from-mysql-to-azure-blob) sezione di questo articolo. 

Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che costituiscono toodefine utilizzato Data Factory archivio dati di entità specifico tooa MySQL:

## <a name="linked-service-properties"></a>Proprietà del servizio collegato
Hello nella tabella seguente fornisce una descrizione del servizio specifico tooMySQL collegati gli elementi JSON.

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| type |proprietà di tipo Hello deve essere impostata su: **OnPremisesMySql** |Sì |
| server |Nome del server MySQL hello. |Sì |
| database |Nome del database MySQL hello. |Sì |
| schema |Nome dello schema hello nel database di hello. |No |
| authenticationType |Tipo di autenticazione usato toohello tooconnect di database MySQL. I valori possibili sono:`Basic`. |Sì |
| username |Specificare i database di MySQL toohello tooconnect nome utente. |Sì |
| password |Specificare la password per l'account utente di hello specificato. |Sì |
| gatewayName |Nome del gateway hello hello servizio Data Factory deve utilizzare database MySQL di tooconnect toohello locale. |Sì |

## <a name="dataset-properties"></a>Proprietà dei set di dati
Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo. Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.

Hello **typeProperties** sezione è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello. sezione Hello typeProperties per set di dati di tipo **RelationalTable** (che include set di dati MySQL) ha le proprietà seguenti hello

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| tableName |Nome della tabella hello nell'istanza di MySQL Database che fa riferimento il servizio collegato a hello. |No (se la **query** di **RelationalSource** è specificata) |

## <a name="copy-activity-properties"></a>Proprietà dell'attività di copia
Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo. Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.

Mentre le proprietà disponibili nella hello **typeProperties** sezione dell'attività hello variano in base a ogni tipo di attività. Per attività di copia, variano a seconda dei tipi di hello di origini e sink.

Quando l'origine in attività di copia è di tipo **RelationalSource** (che include MySQL), hello le proprietà seguenti sono disponibile nella sezione typeProperties:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| query |Utilizzare i dati di tooread hello query personalizzata. |Stringa di query SQL. Ad esempio: selezionare * da MyTable. |No (se **tableName** di **set di dati** è specificato) |


## <a name="json-example-copy-data-from-mysql-tooazure-blob"></a>Esempio JSON: copiare i dati da MySQL tooAzure Blob
In questo esempio vengono fornite le definizioni di JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Viene illustrato come toocopy dati da un MySQL locale database tooan archiviazione Blob di Azure. Tuttavia, i dati possono essere copiati tooany di sink hello indicato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory.

> [!IMPORTANT]
> Questo esempio fornisce frammenti di codice JSON. Non include istruzioni dettagliate per la creazione di data factory di hello. Le istruzioni dettagliate sono disponibili nell'articolo [Spostare dati tra origini locali e il cloud](data-factory-move-data-between-onprem-and-cloud.md) .

esempio Hello è hello entità factory di dati seguenti:

1. Un servizio collegato di tipo [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).
2. Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Un [set di dati](data-factory-create-datasets.md) di input di tipo [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).
4. Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

esempio Hello copia dati da un risultato della query nel blob tooa di database MySQL ogni ora. proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.

Come primo passaggio, configurare il gateway di gestione dati hello. istruzioni di Hello presenti hello [lo spostamento dei dati tra le sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) articolo.

**Servizio collegato MySQL**

```JSON
    {
      "name": "OnPremMySqlLinkedService",
      "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
          "server": "<server name>",
          "database": "<database name>",
          "schema": "<schema name>",
          "authenticationType": "<authentication type>",
          "userName": "<user name>",
          "password": "<password>",
          "gatewayName": "<gateway>"
        }
      }
    }
```

**Servizio collegato Archiviazione di Azure:**

```JSON
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

**Set di dati di input MySQL**

esempio Hello presuppone aver creato una tabella "MyTable" di MySQL e contiene una colonna denominata "timestampcolumn" per i dati della serie temporale.

L'impostazione "external": "true" informa il servizio di Data Factory hello tabella hello è data factory di toohello esterni e non viene generato da un'attività nella data factory di hello.

```JSON
    {
        "name": "MySqlDataSet",
        "properties": {
            "published": false,
            "type": "RelationalTable",
            "linkedServiceName": "OnPremMySqlLinkedService",
            "typeProperties": {},
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

**Set di dati di output del BLOB di Azure:**

I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1). percorso della cartella Hello per blob hello viene valutato dinamicamente in base a ora di inizio hello della sezione hello che viene elaborato. percorso della cartella Hello Usa le parti di anno, mese, giorno e ore dell'ora di inizio hello.

```JSON
    {
        "name": "AzureBlobMySqlDataSet",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "mycontainer/mysql/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Pipeline con attività di copia:**

pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e viene pianificata toorun ogni ora. Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**RelationalSource** e **sink** tipo è stato impostato troppo**BlobSink**. query SQL Hello specificata per hello **query** proprietà consente di selezionare dati hello hello oltre toocopy ora.

```JSON
    {
        "name": "CopyMySqlToBlob",
        "properties": {
            "description": "pipeline for copy activity",
            "activities": [
                {
                    "type": "Copy",
                    "typeProperties": {
                        "source": {
                            "type": "RelationalSource",
                            "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                        },
                        "sink": {
                            "type": "BlobSink",
                            "writeBatchSize": 0,
                            "writeBatchTimeout": "00:00:00"
                        }
                    },
                    "inputs": [
                        {
                            "name": "MySqlDataSet"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "AzureBlobMySqlDataSet"
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
                    "name": "MySqlToBlob"
                }
            ],
            "start": "2014-06-01T18:00:00Z",
            "end": "2014-06-01T19:00:00Z"
        }
    }
```


### <a name="type-mapping-for-mysql"></a>Mapping dei tipi per MySQL
Come accennato in hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, attività di copia esegue le conversioni dai tipi di origine tipi toosink automatico con hello approccio in due passaggi:

1. Conversione dal tipo di origine nativa tipi too.NET
2. Eseguire la conversione da tipo di sink toonative tipo .NET

Quando si spostano dati tooMySQL, hello mapping seguenti vengono utilizzati dai tipi too.NET tipi di MySQL.

| Tipo di database MySQL | Tipo di .NET Framework |
| --- | --- |
| bigint unsigned |Decimal |
| bigint |Int64 |
| Bit |Decimal |
| BLOB |Byte[] |
| bool |Boolean |
| char |String |
| date |Datetime |
| Datetime |Datetime |
| Decimal |Decimal |
| double precision |Double |
| Double |Double |
| enum |String |
| float |Single |
| int unsigned |Int64 |
| int |Int32 |
| integer unsigned |Int64 |
| integer |Int32 |
| long varbinary |Byte[] |
| long varchar |String |
| longblob |Byte[] |
| longtext |String |
| mediumblob |Byte[] |
| mediumint unsigned |Int64 |
| mediumint |Int32 |
| mediumtext |String |
| numeric |Decimal |
| real |Double |
| set |String |
| smallint unsigned |Int32 |
| smallint |Int16 |
| text |String |
| time |Intervallo di tempo |
| timestamp |Datetime |
| tinyblob |Byte[] |
| tinyint unsigned |Int16 |
| tinyint |Int16 |
| tinytext |String |
| varchar |String |
| year |int |

## <a name="map-source-toosink-columns"></a>Eseguire il mapping di colonne di origine toosink
toolearn sui mapping delle colonne in toocolumns di set di dati di origine nel sink set di dati, vedere [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Lettura ripetibile da origini relazionali
Quando si copiano dati da archivi dati relazionali, tenere ripetibilità presente tooavoid risultati imprevisti. In Azure Data Factory è possibile rieseguire una sezione manualmente. È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore. Quando viene eseguito di nuovo una sezione in entrambi i casi, è necessario toomake assicurarsi che hello stessi dati non viene letto alcun altro aspetto come viene eseguita più volte una sezione. Vedere [Lettura ripetibile da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Ottimizzazione delle prestazioni
Vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.
