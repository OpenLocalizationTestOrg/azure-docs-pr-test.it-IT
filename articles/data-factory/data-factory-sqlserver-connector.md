---
title: aaaMove tooand di dati da SQL Server | Documenti Microsoft
description: "Informazioni su come dati toomove a/da SQL Server database che è locale o in una macchina virtuale di Azure usando Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 864ece28-93b5-4309-9873-b095bbe6fedd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jingwang
ms.openlocfilehash: f0cccf56a670e62ec893d75052a81eb26d562050
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-sql-server-on-premises-or-on-iaas-azure-vm-using-azure-data-factory"></a>Spostare dati tooand da SQL Server locale o in IaaS (VM di Azure) usando Azure Data Factory
Questo articolo spiega come toouse hello attività di copia nei dati di Azure Data Factory toomove a/da un database di SQL Server locale. È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello. 

## <a name="supported-scenarios"></a>Scenari supportati
È possibile copiare dati **da un database di SQL Server** toohello archivi dati seguenti:

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

È possibile copiare dati da archivi dati seguenti hello **database di SQL Server tooa**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-sql-server-versions"></a>Versioni di SQL Server supportate
Copia di dati da questo supporto di connettore SQL Server / toohello seguenti versioni di istanza ospitata in locale o in Azure IaaS tramite l'autenticazione di Windows e autenticazione di SQL Server: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005

## <a name="enabling-connectivity"></a>Abilitazione della connettività
concetti di Hello e i passaggi necessari per la connessione con SQL Server ospitato in locale o in Azure IaaS (Infrastructure-as-a-Service) VM sono hello stesso. In entrambi i casi, è necessario toouse Gateway di gestione dati per la connettività.

Vedere [lo spostamento dei dati tra le sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn articolo sul Gateway di gestione dati e istruzioni dettagliate su come configurare il gateway hello. L'impostazione di un'istanza del gateway è un prerequisito per la connessione con SQL Server.

Sebbene sia possibile installare gateway su hello stesso locali istanza macchina o di cloud della macchina virtuale come hello di SQL Server per ottenere prestazioni migliori, è consigliabile installarli in computer separati. Con gateway hello e SQL Server in computer separati riduce la contesa di risorse.

## <a name="getting-started"></a>introduttiva
È possibile creare una pipeline con l'attività di copia che sposta i dati da e verso un SQL Server locale usando diversi strumenti/API.

toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**. Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.

È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**. Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia. 

Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti: 

1. Creare una **data factory**. Una data factory può contenere una o più pipeline. 
2. Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory. Ad esempio, se si copiano dati da un tooan di database di SQL Server archiviazione blob di Azure, è creare due servizi collegati toolink il database di SQL Server e l'archiviazione di Azure account tooyour data factory. Per le proprietà di servizio collegato che sono specifici tooSQL database del Server, vedere [servizio proprietà collegate](#linked-service-properties) sezione. 
3. Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello. Nell'esempio hello indicato nell'ultimo passaggio hello, crei una tabella SQL hello toospecify set di dati nel database di SQL Server che contiene i dati di input hello. E, per creare un altro set di dati toospecify hello blob contenitore e cartella hello contenente hello dati copiati dal hello database di SQL Server. Per le proprietà di set di dati che sono specifici tooSQL database del Server, vedere [proprietà set di dati](#dataset-properties) sezione.
4. Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output. Nell'esempio hello indicato in precedenza, si usa SqlSource come un'origine e BlobSink come sink per attività di copia hello. Analogamente, se si sta copiando l'archiviazione Blob di Azure tooSQL Database del Server, utilizzare BlobSource e SqlSink nell'attività di copia hello. Per le proprietà di attività di copia che sono specifici tooSQL Database del Server, vedere [copiare le proprietà dell'attività](#copy-activity-properties) sezione. Per informazioni dettagliate su come toouse un archivio dati come origine o un sink, fare clic sul collegamento di hello nella sezione precedente di hello per l'archivio dati. 

Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente. Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.  Per esempi con definizioni di JSON per le entità Data Factory toocopy utilizzati i dati in o da un database di SQL Server locale, vedere [esempi JSON](#json-examples-for-copying-data-from-and-to-sql-server) sezione di questo articolo. 

Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che vengono utilizzati toodefine Data Factory entità specifiche tooSQL Server: 

## <a name="linked-service-properties"></a>Proprietà del servizio collegato
Creare un servizio collegato di tipo **OnPremisesSqlServer** toolink una data factory tooa di on-premise SQL Server database. Hello nella tabella seguente fornisce una descrizione del servizio collegato SQL Server locale tooon specifici elementi JSON.

Hello nella tabella seguente fornisce una descrizione JSON elementi specifici tooSQL servizio del Server collegato.

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| type |proprietà di tipo Hello deve essere impostata su: **OnPremisesSqlServer**. |Sì |
| connectionString |Specificare le informazioni connectionString necessarie tooconnect database di SQL Server on-premise toohello utilizzando l'autenticazione di SQL Server o l'autenticazione di Windows. |Sì |
| gatewayName |Nome del gateway hello hello servizio Data Factory deve utilizzare i database di SQL Server on-premise toohello tooconnect. |Sì |
| username |Specificare il nome utente se si usa l'autenticazione Windows. Esempio: **nomedominio\\nomeutente**. |No |
| password |Specificare la password per account utente di hello specificato per il nome utente hello. |No |

È possibile crittografare le credenziali utilizzando hello **New AzureRmDataFactoryEncryptValue** cmdlet e utilizzarli nella stringa di connessione hello, come illustrato nell'esempio seguente hello (**EncryptedCredential** proprietà):  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

### <a name="samples"></a>Esempi
**JSON per l'uso dell'Autenticazione di SQL**

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties":
    {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
**JSON per l'uso dell'Autenticazione Windows**

Gateway di gestione dati rappresenterà hello specificato database di SQL Server on-premise toohello tooconnect account utente. 

```json
{
     "Name": " MyOnPremisesSQLDB",
     "Properties":
     {
         "type": "OnPremisesSqlServer",
         "typeProperties": {
             "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
             "username": "<domain\\username>",
             "password": "<password>",
             "gatewayName": "<gateway name>"
        }
     }
}
```

## <a name="dataset-properties"></a>Proprietà dei set di dati
Negli esempi di hello è stato utilizzato un set di dati di tipo **SqlServerTable** toorepresent una tabella in un database di SQL Server.  

Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo. Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati (SQL Server, BLOB di Azure, tabelle di Azure e così via).

sezione typeProperties Hello è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello. Hello **typeProperties** sezione per hello set di dati di tipo **SqlServerTable** è hello le proprietà seguenti:

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| tableName |Nome della tabella hello o della vista nell'istanza di Database di SQL Server hello che il servizio collegato fa riferimento a. |Sì |

## <a name="copy-activity-properties"></a>Proprietà dell'attività di copia
Se si stanno spostando i dati da un database di SQL Server, impostare il tipo di origine hello nell'attività di copia hello troppo**SqlSource**. Analogamente, se si stanno spostando i database di SQL Server tooa di dati, impostare il tipo di sink hello nell'attività di copia hello troppo**SqlSink**. Questa sezione presenta un elenco delle proprietà supportate da SqlSource e SqlSink.

Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo. Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.

> [!NOTE]
> Hello attività di copia accetta un solo input e produce un solo output.

Mentre le proprietà disponibili nella sezione typeProperties hello dell'attività hello variano in base a ogni tipo di attività. Per attività di copia, variano a seconda dei tipi di hello di origini e sink.

### <a name="sqlsource"></a>SqlSource
Quando l'origine in un'attività di copia è di tipo **SqlSource**, hello le proprietà seguenti sono disponibile in **typeProperties** sezione:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| SqlReaderQuery |Utilizzare i dati di tooread hello query personalizzata. |Stringa di query SQL. Ad esempio: selezionare * da MyTable. Può fare riferimento a più tabelle dal database hello hello di un set di dati dell'input a cui fa riferimento. Se non specificato, hello istruzione SQL eseguita: select from MyTable. |No |
| sqlReaderStoredProcedureName |Nome di hello stored procedure che legge i dati dalla tabella di origine hello. |Nome di hello stored procedure. ultima istruzione SQL di Hello deve essere un'istruzione SELECT nella procedura hello archiviato. |No |
| storedProcedureParameters |I parametri per hello stored procedure. |Coppie nome/valore. Nomi e le maiuscole e minuscole dei parametri devono corrispondere i nomi di hello e maiuscole e minuscole di parametri di hello stored procedure. |No |

Se hello **sqlReaderQuery** specificato per hello SqlSource, hello attività di copia viene eseguita questa query hello Database di SQL Server tooget hello dati.

In alternativa, è possibile specificare una stored procedure specificando hello **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se hello stored procedure accetta parametri).

Se non si specifica sqlReaderQuery o sqlReaderStoredProcedureName, le colonne di hello definite nella sezione di struttura hello sono utilizzati toobuild toorun una query select su hello Database di SQL Server. Se non dispone di definizione del set di dati hello struttura hello, vengono selezionate tutte le colonne dalla tabella hello.

> [!NOTE]
> Quando si utilizza **sqlReaderStoredProcedureName**, è comunque necessario toospecify un valore per hello **tableName** proprietà hello set di dati JSON. Non sono disponibili convalide eseguite su questa tabella.

### <a name="sqlsink"></a>SqlSink
**SqlSink** supporta hello le proprietà seguenti:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| writeBatchTimeout |Tempo di attesa per hello batch insert operazione toocomplete prima del timeout. |Intervallo di tempo<br/><br/> Ad esempio: "00:30:00" (30 minuti). |No |
| writeBatchSize |Inserisce dati in una tabella SQL hello quando viene raggiunto writeBatchSize raggiungerà le dimensioni di buffer hello. |Numero intero (numero di righe) |No (valore predefinito: 10000) |
| sqlWriterCleanupScript |Specificare query per l'attività di copia tooexecute modo che la pulitura dei dati di una sezione specifica. Per altre informazioni, vedere la sezione [Copia ripetibile](#repeatable-copy). |Istruzione di query. |No |
| sliceIdentifierColumnName |Specificare il nome di colonna per attività di copia toofill con identificatore di sezione generati automaticamente, che è usato tooclean dei dati di una sezione specifica quando eseguire di nuovo. Per altre informazioni, vedere la sezione [Copia ripetibile](#repeatable-copy). |Nome di colonna di una colonna con tipo di dati binario (32). |No |
| sqlWriterStoredProcedureName |Nome della hello stored procedure che upserts (aggiornamenti/inserimenti) i dati nella tabella di destinazione hello. |Nome di hello stored procedure. |No |
| storedProcedureParameters |I parametri per hello stored procedure. |Coppie nome/valore. Nomi e le maiuscole e minuscole dei parametri devono corrispondere i nomi di hello e maiuscole e minuscole di parametri di hello stored procedure. |No |
| sqlWriterTableType |Specificare toobe nome tipo di tabella utilizzati in hello stored procedure. Attività di copia rende disponibili in una tabella temporanea con questo tipo di tabella dati di hello viene spostati. Codice della stored procedure può unire dati hello copiati con i dati esistenti. |Nome del tipo di tabella. |No |


## <a name="json-examples-for-copying-data-from-and-toosql-server"></a>Esempi JSON per la copia dei dati da e tooSQL Server
Negli esempi seguenti Hello forniscono definizioni JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Hello seguente mostra esempi come toocopy tooand di dati da SQL Server e archiviazione Blob di Azure. Tuttavia, i dati possono essere copiati **direttamente** da una qualsiasi delle origini tooany di sink hello indicato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory.     

## <a name="example-copy-data-from-sql-server-tooazure-blob"></a>Esempio: Copiare i dati da SQL Server tooAzure Blob
Hello nel seguente esempio viene illustrato:

1. Un servizio collegato di tipo [OnPremisesSqlServer](#linked-service-properties).
2. Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Un [set di dati](data-factory-create-datasets.md) di tipo [SqlServerTable](#dataset-properties).
4. Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Hello [pipeline](data-factory-create-pipelines.md) con attività di copia che utilizza [SqlSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

esempio Hello copia dati delle serie temporali da un tooan tabella di SQL Server blob di Azure ogni ora. proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.

Come primo passaggio, configurare il gateway di gestione dati hello. istruzioni di Hello presenti hello [lo spostamento dei dati tra le sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) articolo.

**Servizio collegato di SQL Server**
```json
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
**Servizio collegato di archiviazione BLOB di Azure**

```json
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
**Set di dati input di SQL Server**

esempio Hello presuppone di aver creato una tabella "MyTable" in SQL Server e contiene una colonna denominata "timestampcolumn" per i dati della serie temporale. È possibile eseguire query su più tabelle all'interno di hello stesso database con un singolo set di dati, ma una singola tabella deve essere utilizzato per typeProperty tableName hello del dataset.

L'impostazione "external": "true" informa il servizio Data Factory hello set di dati è esterna toohello data factory e non viene generato da un'attività nella data factory di hello.

```json
{
  "name": "SqlServerInput",
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
**Set di dati di output del BLOB di Azure**

I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1). percorso della cartella Hello per blob hello viene valutato dinamicamente in base a ora di inizio hello della sezione hello che viene elaborato. percorso della cartella Hello Usa le parti di anno, mese, giorno e ore dell'ora di inizio hello.

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
**Pipeline con attività di copia**

pipeline di Hello contiene un'attività di copia che è configurato toouse questi set di dati di input e output e toorun pianificato ogni ora. Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**SqlSource** e **sink** tipo è stato impostato troppo**BlobSink**. query SQL Hello specificata per hello **SqlReaderQuery** proprietà consente di selezionare dati hello hello oltre toocopy ora.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2016-06-01T18:00:00",
    "end":"2016-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
In questo esempio, **sqlReaderQuery** specificato per hello SqlSource. Attività di copia Hello consente di eseguire questa query hello dati hello tooget origine di Database di SQL Server. In alternativa, è possibile specificare una stored procedure specificando hello **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se hello stored procedure accetta parametri). Hello sqlReaderQuery può fare riferimento a più tabelle all'interno del database hello hello di un set di dati dell'input a cui fa riferimento. Non è limitato tooonly hello tabella impostata come hello typeProperty tableName del set di dati.

Se non si specifica sqlReaderQuery o sqlReaderStoredProcedureName, le colonne di hello definite nella sezione di struttura hello sono utilizzati toobuild toorun una query select su hello Database di SQL Server. Se non dispone di definizione del set di dati hello struttura hello, vengono selezionate tutte le colonne dalla tabella hello.

Vedere hello [origine Sql](#sqlsource) sezione e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) per elenco hello delle proprietà supportate da SqlSource e BlobSink.

## <a name="example-copy-data-from-azure-blob-toosql-server"></a>Esempio: Copiare i dati da Blob di Azure tooSQL Server
Hello nel seguente esempio viene illustrato:

1. servizio del tipo di Hello collegato [OnPremisesSqlServer](#linked-service-properties).
2. servizio del tipo di Hello collegato [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Un [set di dati](data-factory-create-datasets.md) di output di tipo [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).
5. Hello [pipeline](data-factory-create-pipelines.md) con attività di copia che utilizza [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [SqlSink](#sql-server-copy-activity-type-properties).

esempio Hello copia dati delle serie temporali da una tabella di SQL Server tooa blob di Azure ogni ora. proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.

**Servizio collegato di SQL Server**

```json
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
**Servizio collegato di archiviazione BLOB di Azure**

```json
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
**Set di dati di input del BLOB di Azure**

I dati vengono prelevati da un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1). Hello percorso e il nome della cartella per il blob hello vengono valutate in modo dinamico in base a ora di inizio hello della sezione hello che viene elaborato. percorso della cartella Hello utilizza year, month e parte del giorno dell'ora di inizio hello e nome del file utilizza parte ora hello hello ora di inizio. "external": "true" impostazione informa il servizio di Data Factory hello hello set di dati è esterna toohello data factory e non viene generato da un'attività nella data factory di hello.

```json
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
**Set di dati output di SQL Server**

esempio Hello copia tabella tooa dati denominata "MyTable" in SQL Server. Creare la tabella hello in SQL Server con hello stesso numero di colonne nel modo previsto toocontain di file CSV Blob hello. Aggiunta di nuove righe nella tabella toohello ogni ora.

```json
{
  "name": "SqlServerOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
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
**Pipeline con attività di copia**

pipeline di Hello contiene un'attività di copia che è configurato toouse questi set di dati di input e output e toorun pianificato ogni ora. Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**BlobSource** e **sink** tipo è stato impostato troppo**SqlSink**.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": " SqlServerOutput "
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlSink"
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

## <a name="troubleshooting-connection-issues"></a>Risoluzione dei problemi di connessione
1. Configurare le connessioni remote tooaccept di SQL Server. Avviare **SQL Server Management Studio**, fare clic con il pulsante destro del mouse su **server** e selezionare **Properties**. Selezionare **connessioni** dall'elenco di hello e controllo **server toohello di Consenti connessioni remote**.

    ![Abilitare le connessioni remote](./media/data-factory-sqlserver-connector/AllowRemoteConnections.png)

    Vedere [configurare accesso remoto hello opzione di configurazione del Server](https://msdn.microsoft.com/library/ms191464.aspx) per i passaggi dettagliati.
2. Avviare **Gestione configurazione SQL Server**. Espandere **configurazione di rete SQL Server** per hello istanza che si desidera, quindi selezionare **protocolli per MSSQLSERVER**. Verrà visualizzato protocolli nel riquadro di destra hello. Abilitare il protocollo TCP/IP facendo clic con il pulsante destro del mouse su **TCP/IP** e selezionando **Abilita**.

    ![Abilitare TCP/IP](./media/data-factory-sqlserver-connector/EnableTCPProptocol.png)

    Per informazioni dettagliate e modalità alternative di abilitazione del protocollo TCP/IP, vedere [Abilitare o disabilitare un protocollo di rete del server](https://msdn.microsoft.com/library/ms191294.aspx).
3. Nella stessa finestra hello fare doppio clic su **TCP/IP** toolaunch **proprietà TCP/IP** finestra.
4. Passare toohello **gli indirizzi IP** scheda. Scorrere verso il basso toosee **IPAll** sezione. Annotare hello * * la porta TCP * * (valore predefinito è **1433**).
5. Creare un **regola per il Firewall di Windows hello** hello macchina tooallow il traffico in ingresso tramite questa porta.  
6. **Verifica connessione**: tooconnect toohello SQL Server utilizzando il nome completo, utilizzare SQL Server Management Studio da un computer diverso. Ad esempio: "<machine><domain>.corp<company>.com,1433."

   > [!IMPORTANT]

   > Vedere [spostare dati tra origini locali e cloud hello con Gateway di gestione dati](data-factory-move-data-between-onprem-and-cloud.md) per informazioni dettagliate.
   >
   > Per suggerimenti sulla risoluzione di problemi correlati alla connessione o al gateway, vedere [Risoluzione dei problemi del gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) .
   >
   >


## <a name="identity-columns-in-hello-target-database"></a>Colonne Identity nel database di destinazione hello
In questa sezione viene fornito un esempio che copia i dati da una tabella di origine con alcuna tabella di destinazione tooa colonna identity con una colonna identity.

**Tabella di origine:**

```sql
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
**Tabella di destinazione:**

```sql
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```

Si noti che la tabella di destinazione hello include una colonna identity.

**Definizione JSON del set di dati di origine**

```json
{
    "name": "SampleSource",
    "properties": {
        "published": false,
        "type": " SqlServerTable",
        "linkedServiceName": "TestIdentitySQL",
        "typeProperties": {
            "tableName": "SourceTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```
**Definizione JSON del set di dati di destinazione**

```json
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "TestIdentitySQLSource",
        "typeProperties": {
            "tableName": "TargetTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

Si noti che la tabella di origine e la tabella di destinazione hanno schemi diversi (la destinazione include una colonna aggiuntiva identity). In questo scenario, è necessario toospecify **struttura** proprietà nella definizione di set di dati destinazione hello, che non include una colonna identity hello.

## <a name="invoke-stored-procedure-from-sql-sink"></a>Chiamare una stored procedure da un sink SQL
Per un esempio di come chiamare una stored procedure da un sink SQL in un'attività di copia di una pipeline, vedere l'articolo su come [richiamare una stored procedure per il sink SQL nell'attività di copia](data-factory-invoke-stored-procedure-from-copy-activity.md).

## <a name="type-mapping-for-sql-server"></a>Mapping dei tipi per SQL Server
Come accennato in hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo hello attività di copia esegue le conversioni dai tipi di origine tipi toosink automatico con hello approccio passaggio 2:

1. Conversione dal tipo di origine nativa tipi too.NET
2. Eseguire la conversione da tipo di sink toonative tipo .NET

Quando lo spostamento dei dati troppo & da SQL server, hello mapping seguenti vengono utilizzate dal tipo too.NET di tipo SQL e viceversa.

mapping di Hello è identico a hello mapping dei tipi di dati di SQL Server per ADO.NET.

| Tipo di motore di database di SQL Server | Tipo di .NET Framework |
| --- | --- |
| bigint |Int64 |
| binary |Byte[] |
| bit |Boolean |
| char |String, Char[] |
| date |DateTime |
| DateTime |DateTime |
| datetime2 |DateTime |
| Datetimeoffset |Datetimeoffset |
| Decimale |Decimale |
| FILESTREAM attribute (varbinary(max)) |Byte[] |
| Float |Double |
| immagine |Byte[] |
| int |Int32 |
| money |Decimale |
| nchar |String, Char[] |
| ntext |String, Char[] |
| numeric |Decimale |
| nvarchar |String, Char[] |
| real |Single |
| rowversion |Byte[] |
| smalldatetime |DateTime |
| smallint |Int16 |
| smallmoney |Decimale |
| sql_variant |Object * |
| text |String, Char[] |
| time |Intervallo di tempo |
| timestamp |Byte[] |
| tinyint |Byte |
| uniqueidentifier |Guid |
| varbinary |Byte[] |
| varchar |String, Char[] |
| xml |xml |

## <a name="mapping-source-toosink-columns"></a>Mapping di colonne di origine toosink
colonne toomap toocolumns set di dati di origine dal sink set di dati, vedere [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-copy"></a>Copia ripetibile
Quando si copiano dati tooSQL Database del Server, attività di copia hello Accoda tabella di dati toohello sink per impostazione predefinita. Vedere invece tooperform UPSERT [tooSqlSink scrittura Repeatable](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) articolo. 

Quando si copiano dati da archivi dati relazionali, tenere ripetibilità presente tooavoid risultati imprevisti. In Azure Data Factory è possibile rieseguire una sezione manualmente. È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore. Quando viene eseguito di nuovo una sezione in entrambi i casi, è necessario toomake assicurarsi che hello stessi dati non viene letto alcun altro aspetto come viene eseguita più volte una sezione. Vedere [Lettura ripetibile da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Ottimizzazione delle prestazioni
Vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.
