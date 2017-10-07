---
title: aaaCopy dati da e verso il Database SQL di Azure | Documenti Microsoft
description: Informazioni su come toocopy dati da e verso il Database SQL di Azure usando Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 484f735b-8464-40ba-a9fc-820e6553159e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: d2ff16191afb028da75699c5e4d0bb310538db0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-database-using-azure-data-factory"></a>Copia dati tooand dal Database di SQL Azure con Data Factory di Azure
Questo articolo spiega come toouse hello attività di copia in Azure Data Factory toomove dati tooand dal Database di SQL Azure. È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello.  

## <a name="supported-scenarios"></a>Scenari supportati
È possibile copiare dati **dal Database di SQL Azure** toohello archivi dati seguenti:

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

È possibile copiare dati da archivi dati seguenti hello **tooAzure Database SQL**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-authentication-type"></a>Tipo di autenticazione supportato
Il connettore per database SQL di Azure supporta l'autenticazione di base.

## <a name="getting-started"></a>Introduzione
È possibile creare una pipeline con l'attività di copia che sposta i dati da e verso un database SQL di Azure usando diversi strumenti/API.

toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**. Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.

È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**. Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia. 

Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti: 

1. Creare una **data factory**. Una data factory può contenere una o più pipeline. 
2. Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory. Ad esempio, se si copiano dati da un database di SQL Azure tooan di archiviazione blob di Azure, è creare due servizi collegati toolink l'account di archiviazione di Azure e la data factory di Azure SQL database tooyour. Per le proprietà di servizio collegato che sono tooAzure specifico Database SQL, vedere [servizio proprietà collegate](#linked-service-properties) sezione. 
3. Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello. Nell'esempio hello indicato nell'ultimo passaggio hello è creare un contenitore di blob hello toospecify set di dati e una cartella che contiene i dati di input hello. E, alla creazione di un altro set di dati toospecify hello SQL nella tabella nel database di SQL Azure hello che contiene dati hello copiati dall'archiviazione blob hello. Per le proprietà di set di dati che sono specifici tooAzure archivio Data Lake, vedere [proprietà set di dati](#dataset-properties) sezione.
4. Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output. Nell'esempio hello indicato in precedenza, si usa BlobSource come un'origine e di SqlSink come sink per attività di copia hello. Analogamente, se si sta copiando tooAzure Database SQL di Azure nell'archiviazione Blob, utilizzare SqlSource e BlobSink nell'attività di copia hello. Per le proprietà di attività di copia che sono specifici tooAzure Database SQL, vedere [copiare le proprietà dell'attività](#copy-activity-properties) sezione. Per informazioni dettagliate su come toouse un archivio dati come origine o un sink, fare clic sul collegamento di hello nella sezione precedente di hello per l'archivio dati.

Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente. Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.  Per esempi con definizioni di JSON per le entità Data Factory toocopy utilizzati i dati in o da un Database di SQL Azure, vedere [esempi JSON](#json-examples-for-copying-data-to-and-from-sql-database) sezione di questo articolo. 

Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che vengono utilizzati toodefine Data Factory entità specifiche tooAzure Database SQL: 

## <a name="linked-service-properties"></a>Proprietà del servizio collegato
SQL Azure collegato collegamenti al servizio una data factory di Azure SQL database tooyour. Hello nella tabella seguente fornisce una descrizione per JSON elementi specifici tooAzure SQL servizio collegato.

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| type |proprietà di tipo Hello deve essere impostata su: **AzureSqlDatabase** |Sì |
| connectionString |Specificare l'istanza del Database di SQL Azure toohello tooconnect necessarie informazioni per la proprietà connectionString hello. È supportata solo l'autenticazione di base. |Sì |

> [!IMPORTANT]
> Configurare [Firewall di Database SQL di Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) hello server di database troppo[consentire a servizi di Azure tooaccess hello server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure). Inoltre, se si copiano dati tooAzure Database SQL da inclusi Azure esterno da origini dati locali con gateway factory di dati, configurare l'intervallo di indirizzi IP appropriata per la macchina hello che invia dati tooAzure Database SQL.

## <a name="dataset-properties"></a>Proprietà dei set di dati
toospecify toorepresent un set di dati dati di input o outpui in un database SQL di Azure, impostare proprietà di tipo hello del set di dati hello: **AzureSqlTable**. Set hello **linkedServiceName** proprietà del nome di toohello hello set di dati di SQL Azure hello servizio collegato.  

Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo. Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.

sezione typeProperties Hello è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello. Hello **typeProperties** sezione per hello set di dati di tipo **AzureSqlTable** è hello le proprietà seguenti:

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| tableName |Nome della tabella hello o della vista nell'istanza di Database SQL di Azure hello che il servizio collegato fa riferimento a. |Sì |

## <a name="copy-activity-properties"></a>Proprietà dell'attività di copia
Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo. Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.

> [!NOTE]
> Hello attività di copia accetta un solo input e produce un solo output.

Mentre le proprietà disponibili nella hello **typeProperties** sezione dell'attività hello variano in base a ogni tipo di attività. Per attività di copia, variano a seconda dei tipi di hello di origini e sink.

Se si spostano dati da un database SQL di Azure, impostare il tipo di origine di hello nell'attività di copia hello troppo**SqlSource**. Analogamente, se si stanno spostando i database SQL di Azure tooan di dati, impostare il tipo di sink hello nell'attività di copia hello troppo**SqlSink**. Questa sezione presenta un elenco delle proprietà supportate da SqlSource e SqlSink.

### <a name="sqlsource"></a>SqlSource
Nell'attività di copia, l'origine hello è di tipo **SqlSource**, hello le proprietà seguenti sono disponibile in **typeProperties** sezione:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| SqlReaderQuery |Utilizzare i dati di tooread hello query personalizzata. |Stringa di query SQL. Esempio: `select * from MyTable`. |No |
| sqlReaderStoredProcedureName |Nome di hello stored procedure che legge i dati dalla tabella di origine hello. |Nome di hello stored procedure. ultima istruzione SQL di Hello deve essere un'istruzione SELECT nella procedura hello archiviato. |No |
| storedProcedureParameters |I parametri per hello stored procedure. |Coppie nome/valore. Nomi e le maiuscole e minuscole dei parametri devono corrispondere i nomi di hello e maiuscole e minuscole di parametri di hello stored procedure. |No |

Se hello **sqlReaderQuery** specificato per hello SqlSource, hello attività di copia viene eseguita questa query hello Database SQL di Azure tooget hello dati. In alternativa, è possibile specificare una stored procedure specificando hello **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se hello stored procedure accetta parametri).

Se non si specifica sqlReaderQuery o sqlReaderStoredProcedureName, le colonne di hello definite nella sezione di struttura hello del set di dati hello JSON sono toobuild utilizzata una query (`select column1, column2 from mytable`) toorun contro hello Database SQL di Azure. Se non dispone di definizione del set di dati hello struttura hello, vengono selezionate tutte le colonne dalla tabella hello.

> [!NOTE]
> Quando si utilizza **sqlReaderStoredProcedureName**, è comunque necessario toospecify un valore per hello **tableName** proprietà hello set di dati JSON. Non sono disponibili convalide eseguite su questa tabella.
>
>

### <a name="sqlsource-example"></a>Esempio SqlSource

```JSON
"source": {
    "type": "SqlSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```

**definizione della stored procedure Hello archiviato:**

```SQL
CREATE PROCEDURE CopyTestSrcStoredProcedureWithParameters
(
    @stringData varchar(20),
    @identifier int
)
AS
SET NOCOUNT ON;
BEGIN
     select *
     from dbo.UnitTestSrcTable
     where dbo.UnitTestSrcTable.stringData != stringData
    and dbo.UnitTestSrcTable.identifier != identifier
END
GO
```

### <a name="sqlsink"></a>SqlSink
**SqlSink** supporta hello le proprietà seguenti:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| writeBatchTimeout |Tempo di attesa per hello batch insert operazione toocomplete prima del timeout. |Intervallo di tempo<br/><br/> Ad esempio: "00:30:00" (30 minuti). |No |
| writeBatchSize |Inserisce dati in una tabella SQL hello quando viene raggiunto writeBatchSize raggiungerà le dimensioni di buffer hello. |Numero intero (numero di righe) |No (valore predefinito: 10000) |
| sqlWriterCleanupScript |Specificare una query per attività di copia tooexecute modo che la pulitura dei dati di una sezione specifica. Per altre informazioni, vedere la [copia ripetibile](#repeatable-copy). |Istruzione di query. |No |
| sliceIdentifierColumnName |Specificare un nome di colonna per attività di copia toofill con identificatore di sezione generati automaticamente, che è usato tooclean dei dati di una sezione specifica quando eseguire di nuovo. Per altre informazioni, vedere la [copia ripetibile](#repeatable-copy). |Nome di colonna di una colonna con tipo di dati binario (32). |No |
| sqlWriterStoredProcedureName |Nome della hello stored procedure che upserts (aggiornamenti/inserimenti) i dati nella tabella di destinazione hello. |Nome di hello stored procedure. |No |
| storedProcedureParameters |I parametri per hello stored procedure. |Coppie nome/valore. Nomi e le maiuscole e minuscole dei parametri devono corrispondere i nomi di hello e maiuscole e minuscole di parametri di hello stored procedure. |No |
| sqlWriterTableType |Specificare un toobe nome tipo di tabella utilizzati in hello stored procedure. Attività di copia rende disponibili in una tabella temporanea con questo tipo di tabella dati di hello viene spostati. Codice della stored procedure può unire dati hello copiati con i dati esistenti. |Nome del tipo di tabella. |No |

#### <a name="sqlsink-example"></a>Esempio SqlSink

```JSON
"sink": {
    "type": "SqlSink",
    "writeBatchSize": 1000000,
    "writeBatchTimeout": "00:05:00",
    "sqlWriterStoredProcedureName": "CopyTestStoredProcedureWithParameters",
    "sqlWriterTableType": "CopyTestTableType",
    "storedProcedureParameters": {
        "identifier": { "value": "1", "type": "Int" },
        "stringData": { "value": "str1" },
        "decimalData": { "value": "1", "type": "Decimal" }
    }
}
```

## <a name="json-examples-for-copying-data-tooand-from-sql-database"></a>Esempi JSON per la copia dei dati tooand dal Database SQL
Negli esempi seguenti Hello forniscono definizioni JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Vengono visualizzate come toocopy tooand di dati dal Database di SQL Azure e archiviazione Blob di Azure. Tuttavia, i dati possono essere copiati **direttamente** da una qualsiasi delle origini tooany di sink hello indicato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory.

### <a name="example-copy-data-from-azure-sql-database-tooazure-blob"></a>Esempio: Copiare i dati da Database SQL di Azure tooAzure Blob
Hello stesso definisce hello entità Data Factory di seguito:

1. Un servizio collegato di tipo [AzureSqlDatabase](#linked-service-properties).
2. Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureSqlTable](#dataset-properties).
4. Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Una [pipeline](data-factory-create-pipelines.md) con un'attività di copia che usa [SqlSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

esempio Hello copia dati della serie temporale (oraria, giornaliera, ecc.) da una tabella in blob tooa di database SQL di Azure ogni ora. proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.  

**Servizio collegato per il database SQL Azure:**

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
Vedere hello [servizio collegato di Azure SQL](#linked-service) sezione per hello elenco delle proprietà supportate da questo servizio collegato.

**Servizio collegato di archiviazione BLOB di Azure:**

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
Vedere hello [Blob di Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) articolo per elenco hello delle proprietà supportate da questo servizio collegato.


**Set di dati di input SQL Azure:**

esempio Hello presuppone di aver creato una tabella "MyTable" in SQL Azure e contiene una colonna denominata "timestampcolumn" per i dati della serie temporale.

L'impostazione "external": "true" informa il servizio di Azure Data Factory hello hello set di dati è esterna toohello data factory e non viene generato da un'attività nella data factory di hello.

```JSON
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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

Vedere hello [proprietà del tipo di set di dati SQL di Azure](#dataset) sezione per hello elenco delle proprietà supportate da questo tipo di set di dati.  

**Set di dati di output del BLOB di Azure:**

I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1). percorso della cartella Hello per blob hello viene valutato dinamicamente in base a ora di inizio hello della sezione hello che viene elaborato. percorso della cartella Hello Usa le parti di anno, mese, giorno e ore dell'ora di inizio hello.

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}/",
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
Vedere hello [proprietà del tipo di set di dati Blob di Azure](data-factory-azure-blob-connector.md#dataset-properties) sezione per hello elenco delle proprietà supportate da questo tipo di set di dati.  

**Un'attività di copia in una pipeline con un'origine SQL e un sink BLOB:**

pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e viene pianificata toorun ogni ora. Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**SqlSource** e **sink** tipo è stato impostato troppo**BlobSink**. query SQL Hello specificata per hello **SqlReaderQuery** proprietà consente di selezionare dati hello hello oltre toocopy ora.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
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
Nell'esempio hello **sqlReaderQuery** specificato per hello SqlSource. Attività di copia Hello consente di eseguire questa query hello dati hello tooget origine di Database SQL di Azure. In alternativa, è possibile specificare una stored procedure specificando hello **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se hello stored procedure accetta parametri).

Se non si specifica sqlReaderQuery o sqlReaderStoredProcedureName, le colonne di hello definite nella sezione di struttura hello del set di dati hello JSON sono utilizzati toobuild toorun una query sul Database SQL di Azure hello. Ad esempio: `select column1, column2 from mytable`. Se non dispone di definizione del set di dati hello struttura hello, vengono selezionate tutte le colonne dalla tabella hello.

Vedere hello [origine Sql](#sqlsource) sezione e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) per elenco hello delle proprietà supportate da SqlSource e BlobSink.

### <a name="example-copy-data-from-azure-blob-tooazure-sql-database"></a>Esempio: Copiare i dati da Blob di Azure tooAzure Database SQL
esempio Hello definisce hello entità Data Factory di seguito:  

1. Un servizio collegato di tipo [AzureSqlDatabase](#linked-service-properties).
2. Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureSqlTable](#dataset-properties).
5. Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [SqlSink](#copy-activity-properties).

esempio Hello copia dati della serie temporale (oraria, giornaliera, ecc.) dalla tabella tooa blob di Azure nel database SQL di Azure ogni ora. proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.

**Servizio collegato SQL di Azure:**

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
Vedere hello [servizio collegato di Azure SQL](#linked-service) sezione per hello elenco delle proprietà supportate da questo servizio collegato.

**Servizio collegato di archiviazione BLOB di Azure:**

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
Vedere hello [Blob di Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) articolo per elenco hello delle proprietà supportate da questo servizio collegato.


**Set di dati di input del BLOB di Azure:**

I dati vengono prelevati da un nuovo BLOB ogni ora (frequenza: ora, intervallo: 1). Hello percorso e il nome della cartella per il blob hello vengono valutate in modo dinamico in base a ora di inizio hello della sezione hello che viene elaborato. percorso della cartella Hello utilizza year, month e parte del giorno dell'ora di inizio hello e nome del file utilizza parte ora hello hello ora di inizio. "external": "true" impostazione informa il servizio di Data Factory hello che questa tabella è data factory di toohello esterni e non viene generata da un'attività nella data factory di hello.

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
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
Vedere hello [proprietà del tipo di set di dati Blob di Azure](data-factory-azure-blob-connector.md#dataset-properties) sezione per hello elenco delle proprietà supportate da questo tipo di set di dati.

**Set di dati di aoutput del database SQL di Azure**

esempio Hello copia tabella tooa dati denominata "MyTable" in SQL Azure. Creare la tabella hello in SQL Azure con hello stesso numero di colonne nel modo previsto toocontain di file CSV Blob hello. Aggiunta di nuove righe nella tabella toohello ogni ora.

```JSON
{
  "name": "AzureSqlOutput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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
Vedere hello [proprietà del tipo di set di dati SQL di Azure](#dataset) sezione per hello elenco delle proprietà supportate da questo tipo di set di dati.

**Un'attività di copia in una pipeline con un'origine BLOB e un sink SQL:**

pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e viene pianificata toorun ogni ora. Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**BlobSource** e **sink** tipo è stato impostato troppo**SqlSink**.

```JSON
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
            "name": "AzureSqlOutput"
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
Vedere hello [Sql Sink](#sqlsink) sezione e [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) per elenco hello delle proprietà supportate da SqlSink e BlobSource.

## <a name="identity-columns-in-hello-target-database"></a>Colonne Identity nel database di destinazione hello
In questa sezione viene fornito un esempio per la copia di dati da una tabella di origine senza una tabella di destinazione tooa colonna identity con una colonna identity.

**Tabella di origine:**

```SQL
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
**Tabella di destinazione:**

```SQL
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```
Si noti che la tabella di destinazione hello include una colonna identity.

**Definizione JSON del set di dati di origine**

```JSON
{
    "name": "SampleSource",
    "properties": {
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

```JSON
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
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

## <a name="type-mapping-for-azure-sql-database"></a>Mapping dei tipi per il database SQL di Azure
Come accennato in hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo attività di copia esegue le conversioni dai tipi di origine tipi toosink automatico con hello approccio passaggio 2:

1. Conversione dal tipo di origine nativa tipi too.NET
2. Eseguire la conversione da tipo di sink toonative tipo .NET

Quando si spostano dati tooand dal Database SQL di Azure, hello mapping seguenti vengono utilizzate dal tipo too.NET di tipo SQL e viceversa. mapping di Hello è identico a hello mapping dei tipi di dati di SQL Server per ADO.NET.

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

## <a name="map-source-toosink-columns"></a>Eseguire il mapping di colonne di origine toosink
toolearn sui mapping delle colonne in toocolumns di set di dati di origine nel sink set di dati, vedere [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-copy"></a>Copia ripetibile
Quando si copiano dati tooSQL Database del Server, attività di copia hello Accoda tabella di dati toohello sink per impostazione predefinita. Vedere invece tooperform UPSERT [tooSqlSink scrittura Repeatable](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) articolo. 

Quando si copiano dati da archivi dati relazionali, tenere ripetibilità presente tooavoid risultati imprevisti. In Azure Data Factory è possibile rieseguire una sezione manualmente. È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore. Quando viene eseguito di nuovo una sezione in entrambi i casi, è necessario toomake assicurarsi che hello stessi dati non viene letto alcun altro aspetto come viene eseguita più volte una sezione. Vedere [Lettura ripetibile da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Ottimizzazione delle prestazioni
Vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.
