---
title: aaaMove dati da SAP HANA utilizzando Data Factory di Azure | Documenti Microsoft
description: Per ulteriori informazioni vedere toomove dati da SAP HANA usando Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 5cefe4c8ed01ea4e86e02496b2f8a9083d0b949c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sap-hana-using-azure-data-factory"></a>Spostare dati da SAP HANA usando Azure Data Factory
Questo articolo spiega come toouse hello attività di copia dei dati toomove Data Factory di Azure da un SAP HANA locale. È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello.

È possibile copiare dati da un archivio di dati di on-premise SAP HANA dati archivio tooany supportati sink. Per un elenco di dati supportati archivi come sink dall'attività di copia hello, vedere hello [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabella. Data factory di supporta attualmente solo lo spostamento di archivi di dati da un tooother SAP HANA, ma non per lo spostamento dei dati da altri dati archivia tooan SAP HANA.

## <a name="supported-versions-and-installation"></a>Versioni supportate e installazione
Questo connettore supporta qualsiasi versione del database SAP HANA. Supporta anche la copia di dati da modelli di informazioni HANA (ad esempio, dalle viste di analisi e calcolo) e da tabelle Riga/Colonna tramite query SQL.

tooenable hello connettività toohello istanza SAP HANA, installare hello seguenti componenti:
- **Gateway di gestione dati**: servizio di Data Factory supporta la connessione dati locali tooon archivi (incluso SAP HANA) utilizzando un componente chiamato Gateway di gestione dati. toolearn sul Gateway di gestione dati e istruzioni dettagliate per la configurazione di gateway di hello, vedere [dati di spostamento tra i dati locali toocloud archiviano dati](data-factory-move-data-between-onprem-and-cloud.md) articolo. Gateway è necessario anche se hello SAP HANA è ospitato in una macchina virtuale IaaS di Azure (VM). È possibile installare il gateway di hello in hello stessa macchina virtuale come dati hello archiviare o su una macchina virtuale diversa, purché il gateway hello può connettersi toohello database.
- **Il driver ODBC di SAP HANA** nel computer gateway hello. È possibile scaricare i driver ODBC di SAP HANA hello da hello [area Download di Software SAP](https://support.sap.com/swdc). Ricerca con la parola chiave hello **SAP HANA CLIENT per Windows**. 

## <a name="getting-started"></a>introduttiva
È possibile creare una pipeline con l'attività di copia che sposta i dati da un archivio dati Cassandra usando diversi strumenti/API. 

- toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**. Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati. 
- È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**. Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia. 

Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:

1. Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.
2. Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello. 
3. Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output. 

Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente. Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.  Per un esempio con le definizioni di JSON per le entità Data Factory dati toocopy utilizzato da un SAP HANA locale, vedere [esempio JSON: copiare i dati da SAP HANA tooAzure Blob](#json-example-copy-data-from-sap-hana-to-azure-blob) sezione di questo articolo. 

Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che costituiscono toodefine utilizzato Data Factory archivio dati di entità specifico tooan SAP HANA:

## <a name="linked-service-properties"></a>Proprietà del servizio collegato
Hello nella tabella seguente fornisce una descrizione per JSON elementi specifici tooSAP HANA servizio collegato.

Proprietà | Descrizione | Valori consentiti | Obbligatoria
-------- | ----------- | -------------- | --------
server | Nome del server di hello in SAP HANA quali hello si trova l'istanza. Se il server usa una porta personalizzata, specificare `server:port`. | string | Sì
authenticationType | Tipo di autenticazione. | string. "Basic" o "Windows" | Sì 
username | Nome dell'utente di hello con server di accesso toohello SAP | string | Sì
password | Password utente hello. | string | Sì
gatewayName | Nome del gateway hello hello servizio Data Factory deve utilizzare l'istanza di SAP HANA tooconnect toohello locale. | string | Sì
encryptedCredential | stringa di credenziale crittografato Hello. | string | No

## <a name="dataset-properties"></a>Proprietà dei set di dati
Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo. Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.

Hello **typeProperties** sezione è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello. Non esistono proprietà specifiche del tipo supportato per i set di dati SAP HANA hello di tipo **RelationalTable**. 


## <a name="copy-activity-properties"></a>Proprietà dell'attività di copia
Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo. Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.

Mentre le proprietà disponibili nella hello **typeProperties** sezione dell'attività hello variano in base a ogni tipo di attività. Per attività di copia, variano a seconda dei tipi di hello di origini e sink.

Quando l'origine in attività di copia è di tipo **RelationalSource** (che include SAP HANA), hello le proprietà seguenti sono disponibile nella sezione typeProperties:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| query | Specifica i dati di tooread query SQL hello dall'istanza di SAP HANA hello. | Query SQL. | Sì |

## <a name="json-example-copy-data-from-sap-hana-tooazure-blob"></a>Esempio JSON: copiare i dati da SAP HANA tooAzure Blob
esempio Hello fornisce definizioni di JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Questo esempio viene illustrato come toocopy dati da un tooan di SAP HANA locale archiviazione Blob di Azure. Tuttavia, i dati possono essere copiati **direttamente** tooany di sink hello elencati [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory.  

> [!IMPORTANT]
> Questo esempio fornisce frammenti di codice JSON. Non include istruzioni dettagliate per la creazione di data factory di hello. Le istruzioni dettagliate sono disponibili nell'articolo [Spostare dati tra origini locali e il cloud](data-factory-move-data-between-onprem-and-cloud.md) .

esempio Hello è hello entità factory di dati seguenti:

1. Un servizio collegato di tipo [SapHana](#linked-service-properties).
2. Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Un [set di dati](data-factory-create-datasets.md) di input di tipo [RelationalTable](#dataset-properties).
4. Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

esempio Hello copia dati da un tooan di SAP HANA istanza blob di Azure ogni ora. proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.

Come primo passaggio, configurare il gateway di gestione dati hello. istruzioni di Hello presenti hello [lo spostamento dei dati tra le sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) articolo.

### <a name="sap-hana-linked-service"></a>Servizio collegato SAP HANA
Questo collegato collegamenti al servizio la data factory toohello istanza di SAP HANA. proprietà tipo Hello è troppo**SapHana**. sezione typeProperties Hello fornisce informazioni di connessione per l'istanza di SAP HANA hello.

```json
{
    "name": "SapHanaLinkedService",
    "properties":
    {
        "type": "SapHana",
        "typeProperties":
        {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```

### <a name="azure-storage-linked-service"></a>Servizio collegato Archiviazione di Azure
Questo collegamento collegamenti al servizio la data factory toohello account di archiviazione di Azure. proprietà tipo Hello è troppo**AzureStorage**. sezione typeProperties Hello fornisce informazioni di connessione per l'account di archiviazione Azure hello.

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

### <a name="sap-hana-input-dataset"></a>Set di dati input di SAP HANA

Questo set di dati definisce i set di dati SAP HANA hello. Impostare il tipo di hello del set di dati Data Factory hello troppo**RelationalTable**. mentre per il set di dati SAP HANA non è attualmente necessario specificare alcuna proprietà relativa al tipo. query Hello nella definizione di attività di copia hello specifica quali tooread dati dall'istanza di SAP HANA hello. 

L'impostazione di proprietà esterna tootrue informa servizio Data Factory hello tabella hello è data factory di toohello esterni e non viene generato da un'attività nella data factory di hello.

Frequenza e l'intervallo di proprietà definisce la pianificazione hello. In questo caso, i dati di hello viene letto dall'istanza di SAP HANA hello ogni ora. 

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="azure-blob-output-dataset"></a>Set di dati di output del BLOB di Azure
Questo set di dati definisce il set di dati di hello output Blob di Azure. proprietà di tipo Hello è tooAzureBlob. Hello typeProperties fornite dove vengono archiviati dati hello copiati dall'istanza di SAP HANA hello. Hello vengono scritti dati tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1). percorso della cartella Hello per blob hello viene valutato dinamicamente in base a ora di inizio hello della sezione hello che viene elaborato. percorso della cartella Hello Usa le parti di anno, mese, giorno e ore dell'ora di inizio hello.

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/saphana/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="pipeline-with-copy-activity"></a>Pipeline con attività di copia

pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e viene pianificata toorun ogni ora. Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**RelationalSource** (per l'origine di SAP HANA) e **sink** tipo è stato impostato troppo**BlobSink**. query SQL Hello specificata per hello **query** proprietà consente di selezionare dati hello hello oltre toocopy ora.

```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<SQL Query for HANA>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapHanaDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDataSet"
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
                "name": "SapHanaToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```


### <a name="type-mapping-for-sap-hana"></a>Mapping dei tipi per SAP HANA
Come accennato in hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, attività di copia esegue le conversioni dai tipi di origine tipi toosink automatico con hello approccio in due passaggi:

1. Conversione dal tipo di origine nativa tipi too.NET
2. Eseguire la conversione da tipo di sink toonative tipo .NET

Quando si spostano dati da SAP HANA, hello seguendo i mapping viene utilizzato dai tipi too.NET tipi di SAP HANA.

Tipo SAP HANA | Tipo basato su .Net
------------- | ---------------
TINYINT | Byte
SMALLINT | Int16
INT | Int32
BIGINT | Int64
REAL | Single
DOUBLE | Single
DECIMAL | Decimale
BOOLEAN | Byte
VARCHAR | String
NVARCHAR | String
CLOB | Byte[]
ALPHANUM | String
BLOB | Byte[]
DATE | DateTime
TIME | Intervallo di tempo
TIMESTAMP | DateTime
SECONDDATE | DateTime

## <a name="known-limitations"></a>Limitazioni note
Quando si copiano dati da SAP HANA, è necessario tenere conto di alcune limitazioni:

- Le stringhe NVARCHAR vengono troncate toomaximum lunghezza di 4000 caratteri Unicode
- SMALLDECIMAL non è supportato
- VARBINARY non è supportato
- Le date valide sono tra comprese tra il 30/12/1899 e il 31/12/9999

## <a name="map-source-toosink-columns"></a>Eseguire il mapping di colonne di origine toosink
toolearn sui mapping delle colonne in toocolumns di set di dati di origine nel sink set di dati, vedere [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Lettura ripetibile da origini relazionali
Quando si copiano dati da archivi dati relazionali, tenere ripetibilità presente tooavoid risultati imprevisti. In Azure Data Factory è possibile rieseguire una sezione manualmente. È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore. Quando viene eseguito di nuovo una sezione in entrambi i casi, è necessario toomake assicurarsi che hello stessi dati non viene letto alcun altro aspetto come viene eseguita più volte una sezione. Vedere [Lettura ripetibile da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)

## <a name="performance-and-tuning"></a>Ottimizzazione delle prestazioni
Vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.
