---
title: aaaMove dati da e verso Azure Cosmos DB | Documenti Microsoft
description: Informazioni su come spostare i dati da e verso la raccolta di Azure Cosmos DB mediante Azure Data Factory
services: data-factory, cosmosdb
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c9297b71-1bb4-4b29-ba3c-4cf1f5575fac
ms.service: multiple
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: bd23ce4e004a972ce6f3e4165cfdea4f0c18fecc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-cosmos-db-using-azure-data-factory"></a>Spostare dati tooand da DB Cosmos Azure usando Azure Data Factory
Questo articolo spiega come toouse hello attività di copia nei dati toomove Azure Data Factory di Azure Cosmos DB (API DocumentDB). È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello. 

È possibile copiare dati da qualsiasi origine supportati dati archiviano tooAzure DB Cosmos o dai dati di Azure Cosmos DB tooany supportati sink archiviano. Per un elenco di archivi dati come origini o sink è supportato dall'attività di copia hello, vedere hello [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabella. 

> [!IMPORTANT]
> Il connettore Azure Cosmos DB supporta solo l'API DocumentDB.

dati toocopy come-è a/da file JSON o un'altra raccolta Cosmos DB, vedere [documenti JSON di importazione/esportazione](#importexport-json-documents).

## <a name="getting-started"></a>introduttiva
È possibile creare una pipeline con l'attività di copia che sposta i dati da e verso Azure Cosmos DB usando diversi strumenti/API.

toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**. Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.

È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**. Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia. 

Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti: 

1. Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.
2. Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello. 
3. Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output. 

Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente. Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.  Per esempi con definizioni di JSON per le entità Data Factory toocopy utilizzati dati da e verso Cosmos DB, vedere [esempi JSON](#json-examples) sezione di questo articolo. 

Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che vengono utilizzati toodefine Data Factory entità specifiche tooCosmos DB: 

## <a name="linked-service-properties"></a>Proprietà del servizio collegato
Hello nella tabella seguente fornisce una descrizione JSON elementi specifici tooAzure servizio DB Cosmos collegato.

| **Proprietà** | **Descrizione** | **Obbligatorio** |
| --- | --- | --- |
| type |proprietà di tipo Hello deve essere impostata su: **DocumentDb** |Sì |
| connectionString |Specificare le informazioni necessarie tooconnect tooAzure DB Cosmos database. |Sì |

Esempio:

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```

## <a name="dataset-properties"></a>Proprietà dei set di dati
Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni, vedere toohello [creazione dei DataSet](data-factory-create-datasets.md) articolo. Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.

sezione typeProperties Hello è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello. Hello typeProperties sezione hello set di dati di tipo **DocumentDbCollection** è hello le proprietà seguenti.

| **Proprietà** | **Descrizione** | **Obbligatorio** |
| --- | --- | --- |
| collectionName |Nome della raccolta documenti Cosmos DB hello. |Sì |

Esempio:

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
### <a name="schema-by-data-factory"></a>Schema da Data Factory
Per gli archivi dati privi di schema, ad esempio Azure Cosmos DB hello servizio Data Factory di inferenza dello schema di hello in uno dei seguenti modi hello:  

1. Se si specifica la struttura hello dei dati tramite hello **struttura** proprietà nella definizione di set di dati hello, hello servizio Data Factory rispetta questa struttura come schema hello. In questo caso, se una riga non contiene un valore per una colonna, verrà inserito un valore null.
2. Se non si specifica la struttura hello dei dati tramite hello **struttura** proprietà nella definizione di set di dati hello, hello servizio Data Factory di inferenza dello schema di hello utilizzando prima riga hello nei dati hello. In questo caso, se hello prima riga contiene schema completo hello, alcune colonne sarà presente nel risultato hello dell'operazione di copia.

Pertanto, per le origini dati privi di schema consigliata hello è struttura hello toospecify dei dati tramite hello **struttura** proprietà.

## <a name="copy-activity-properties"></a>Proprietà dell'attività di copia
Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere toohello [la creazione di pipeline](data-factory-create-pipelines.md) articolo. Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.

> [!NOTE]
> Hello attività di copia accetta un solo input e produce un solo output.

Le proprietà disponibili nella sezione typeProperties hello di attività hello hello invece variano con ogni tipo di attività e in caso di attività di copia variano a seconda dei tipi di hello di origini e sink.

In caso di attività di copia, l'origine è di tipo **DocumentDbCollectionSource** hello le proprietà seguenti sono disponibile in **typeProperties** sezione:

| **Proprietà** | **Descrizione** | **Valori consentiti** | **Obbligatorio** |
| --- | --- | --- | --- |
| query |Specificare i dati di tooread query hello. |Stringa di query supportata da Azure Cosmos DB. <br/><br/>Esempio: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"` |No <br/><br/>Se non specificato, hello istruzione SQL eseguita:`select <columns defined in structure> from mycollection` |
| nestingSeparator |Carattere speciale tooindicate che hello documento nidificato |Qualsiasi carattere. <br/><br/>Azure Cosmos DB è un archivio NoSQL per i documenti JSON, dove sono consentite strutture nidificate. Data Factory di Azure consente gerarchia toodenote utente tramite nestingSeparator, ovvero "." in hello esempi sopra riportati. Con il separatore di hello, attività di copia hello genererà l'oggetto "Name" hello con elementi tre figli prima, intermedio e ultimo, in base too"Name.First", "Name.Middle" e "." in hello "Cognome" definizione di tabella. |No |

**DocumentDbCollectionSink** supporta hello le proprietà seguenti:

| **Proprietà** | **Descrizione** | **Valori consentiti** | **Obbligatorio** |
| --- | --- | --- | --- |
| nestingSeparator |È necessario un carattere speciale nel hello origine colonna nome tooindicate annidati di documento. <br/><br/>Ad esempio sopra: `Name.First` nell'output di hello tabella produce hello seguente struttura JSON nel documento Cosmos DB hello:<br/><br/>"Name": {<br/>    "First": "John"<br/>}, |Carattere usato tooseparate livelli di annidamento.<br/><br/>Il valore predefinito è `.` (punto). |Carattere usato tooseparate livelli di annidamento. <br/><br/>Il valore predefinito è `.` (punto). |
| writeBatchSize |Numero parallelo di richieste di documenti di toocreate tooAzure DB Cosmos del servizio.<br/><br/>È possibile ottimizzare le prestazioni di hello quando si copiano dati da e verso Cosmos DB usando questa proprietà. È possibile prevedere prestazioni migliori quando si aumenta viene raggiunto writeBatchSize poiché vengono inviate altre richieste in parallelo tooCosmos DB. Tuttavia, occorre tooavoid la limitazione delle richieste che possono generare il messaggio di errore hello: "Richiesta frequenza è grande".<br/><br/>La limitazione è dovuta a diversi fattori, inclusi la dimensione dei documenti, il numero di termini nei documenti, i criteri di indicizzazione della raccolta di destinazione, ecc. Per le operazioni di copia, è possibile utilizzare un migliore hello toohave raccolta (ad esempio S3) la maggior parte delle velocità effettiva disponibile (2.500 richiesta unità al secondo). |Integer |No (valore predefinito: 5) |
| writeBatchTimeout |Tempo di attesa per hello operazione toocomplete prima del timeout. |Intervallo di tempo<br/><br/> Ad esempio: "00:30:00" (30 minuti). |No |

## <a name="importexport-json-documents"></a>Importare/esportare documenti JSON
Usando questo connettore Cosmos DB, è possibile:

* Importare i documenti JSON da diverse origini in Cosmos DB, tra cui BLOB di Azure, Azure Data Lake, file system locale o altri archivi di file supportati da Azure Data Factory.
* Esportare i documenti JSON da raccolte Cosmos DB in diversi archivi basati su file.
* Eseguire la migrazione dei dati tra due raccolte Cosmos DB così come sono.

tooachieve copiare tale schema indipendente, 
* Quando si utilizza Copia guidata, selezionare hello **"esportazione-è tooJSON file o una raccolta di Cosmos DB"** opzione.
* Quando utilizzare la funzione JSON, non si specifica sezione "struttura" hello in set di dati DB Cosmos né "nestingSeparator" proprietà Cosmos DB origine/sink nell'attività di copia. tooimport da / tooJSON file di esportazione, nel set di dati archivio file hello specificare il tipo di formato come "JsonFormat", "filePattern" configurazione e ignorare le impostazioni del formato di hello rest, vedere [formato JSON](data-factory-supported-file-and-compression-formats.md#json-format) sezione sui dettagli.

## <a name="json-examples"></a>Esempi JSON
Negli esempi seguenti Hello forniscono definizioni JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Vengono visualizzate come toocopy tooand di dati da database Cosmos di Azure e archiviazione Blob di Azure. Tuttavia, i dati possono essere copiati **direttamente** da qualsiasi hello origini tooany di sink hello indicato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory.

## <a name="example-copy-data-from-azure-cosmos-db-tooazure-blob"></a>Esempio: Copiare i dati da Azure Cosmos DB tooAzure Blob
viene illustrato l'esempio Hello riportato di seguito:

1. Un servizio collegato di tipo [DocumentDB](#linked-service-properties).
2. Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Un [set di dati](data-factory-create-datasets.md) di input di tipo [DocumentDbCollection](#dataset-properties).
4. Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [DocumentDbCollectionSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

esempio Hello copia di dati in Azure Cosmos DB tooAzure Blob. proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.

**Servizio collegato di Azure Cosmos DB:**

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
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
**Set di dati di input di Azure DocumentDB:**

esempio Hello presuppone di disporre di una raccolta denominata **persona** in un database di Azure Cosmos DB.

L'impostazione "external": "true" e specificando externalData informazioni sui criteri del servizio tabella hello hello Azure Data Factory è data factory di toohello esterni e non prodotte da un'attività nella data factory di hello.

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**Set di dati di output del BLOB di Azure:**

Dati viene copiato tooa nuovo blob ogni ora con il percorso di hello per blob hello Reflection hello specifico datetime con granularità oraria.

```JSON
{
  "name": "PersonBlobTableOut",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
Documento JSON di esempio nella raccolta di persona in un database DB Cosmos hello:

```JSON
{
  "PersonId": 2,
  "Name": {
    "First": "Jane",
    "Middle": "",
    "Last": "Doe"
  }
}
```
Cosmos DB supporta l’esecuzione di query di documenti utilizzando una sintassi come SQL su documenti JSON gerarchici.

Esempio: 

```sql
SELECT Person.PersonId, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person
```

esempio Hello pipeline copia i dati da hello raccolta persona in hello Azure Cosmos DB database tooan blob di Azure. Come parte di hello attività di copia hello set di dati di input e output sono stati specificati.  

```JSON
{
  "name": "DocDbToBlobPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "DocumentDbCollectionSource",
            "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
            "nestingSeparator": "."
          },
          "sink": {
            "type": "BlobSink",
            "blobWriterAddHeader": true,
            "writeBatchSize": 1000,
            "writeBatchTimeout": "00:00:59"
          }
        },
        "inputs": [
          {
            "name": "PersonCosmosDbTable"
          }
        ],
        "outputs": [
          {
            "name": "PersonBlobTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromDocDbToBlob"
      }
    ],
    "start": "2015-04-01T00:00:00Z",
    "end": "2015-04-02T00:00:00Z"
  }
}
```
## <a name="example-copy-data-from-azure-blob-tooazure-cosmos-db"></a>Esempio: Copiare i dati da Blob di Azure tooAzure Cosmos DB 
viene illustrato l'esempio Hello riportato di seguito:

1. Un servizio collegato di tipo [DocumentDB](#azure-documentdb-linked-service-properties).
2. Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Un [set di dati](data-factory-create-datasets.md) di input di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Un [set di dati](data-factory-create-datasets.md) di output di tipo [DocumentDbCollection](#azure-documentdb-dataset-type-properties).
5. Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).

esempio Hello copia dati da blob di Azure tooAzure DB Cosmos. proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.

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
**Servizio collegato di Azure Cosmos DB:**

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
**Set di dati di input del BLOB di Azure:**

```JSON
{
  "name": "PersonBlobTableIn",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "MiddleName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "fileName": "input.csv",
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
**Set di dati di output di Azure Cosmos DB:**

esempio Hello copia raccolta tooa dati denominato "Person".

```JSON
{
  "name": "PersonCosmosDbTableOut",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "Name.First",
        "type": "String"
      },
      {
        "name": "Name.Middle",
        "type": "String"
      },
      {
        "name": "Name.Last",
        "type": "String"
      }
    ],
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
esempio Hello pipeline copia i dati da Blob di Azure toohello raccolta persona in hello DB Cosmos. Come parte di hello attività di copia hello set di dati di input e output sono stati specificati.

```JSON
{
  "name": "BlobToDocDbPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "DocumentDbCollectionSink",
            "nestingSeparator": ".",
            "writeBatchSize": 2,
            "writeBatchTimeout": "00:00:00"
          }
          "translator": {
              "type": "TabularTranslator",
              "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix, EmailPromotion: EmailPromotion, rowguid: rowguid, ModifiedDate: ModifiedDate"
          }
        },
        "inputs": [
          {
            "name": "PersonBlobTableIn"
          }
        ],
        "outputs": [
          {
            "name": "PersonCosmosDbTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromBlobToDocDb"
      }
    ],
    "start": "2015-04-14T00:00:00Z",
    "end": "2015-04-15T00:00:00Z"
  }
}
```
Se utilizzato come input blob di esempio hello

```
1,John,,Doe
```
Quindi l'output di hello JSON in DB Cosmos sarà come:

```JSON
{
  "Id": 1,
  "Name": {
    "First": "John",
    "Middle": null,
    "Last": "Doe"
  },
  "id": "a5e8595c-62ec-4554-a118-3940f4ff70b6"
}
```
Azure Cosmos DB è un archivio NoSQL per i documenti JSON, dove sono consentite strutture nidificate. Data Factory di Azure consente gerarchia toodenote utente tramite **nestingSeparator**, ovvero "." in questo esempio. Con il separatore di hello, attività di copia hello genererà l'oggetto "Name" hello con elementi tre figli prima, intermedio e ultimo, in base too"Name.First", "Name.Middle" e "." in hello "Cognome" definizione di tabella.

## <a name="appendix"></a>Appendice
1. **Domanda:** hello aggiornamento di attività di copia del supporto dei record esistenti?

    **Risposta:** No.
2. **Domanda:** funzionamento un nuovo tentativo di una copia tooAzure Cosmos DB gestiscono già copiati i record?

    **Risposta:** se record hanno un campo "ID" e l'operazione di copia hello tenta tooinsert un record con hello stesso ID, l'operazione di copia hello genera un errore.  
3. **Domanda:** Data Factory supporta il [partizionamento dei dati basato su hash o su intervalli](../documentdb/documentdb-partition-data.md)?

    **Risposta:** No.
4. **Domanda:** è possibile specificare più raccolte di Azure Cosmos DB per una tabella?

    **Risposta:** No. In questo momento, è possibile specificare solo una raccolta.

## <a name="performance-and-tuning"></a>Ottimizzazione delle prestazioni
Vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.
