---
title: aaaMove dati da un server FTP tramite Data Factory di Azure | Documenti Microsoft
description: Per ulteriori informazioni vedere toomove dati da un server FTP con Data Factory di Azure.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: eea3bab0-a6e4-4045-ad44-9ce06229c718
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jingwang
ms.openlocfilehash: c707e29532b2a8a870603948cb6150ab857bd6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-ftp-server-by-using-azure-data-factory"></a>Spostare dati da un server FTP usando Azure Data Factory
Questo articolo spiega come hello toouse attività di copia dei dati toomove Data Factory di Azure da un server FTP. È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello.

È possibile copiare dati da un archivio dati di sink FTP server tooany è supportato. Per un elenco di dati supportati archivi come sink dall'attività di copia hello, vedere hello [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabella. Data Factory supporta attualmente solo archivia dati mobili da tooother un server FTP, ma non lo spostamento dei dati da altri dati archivia server tooan FTP. Supporta i server FTP locali e cloud.

> [!NOTE]
> attività di copia Hello non elimina i file di origine hello dopo che è la destinazione toohello copiati correttamente. Se è necessario toodelete file di origine hello dopo una copia ha esito positivo, creare un file hello toodelete di attività personalizzata e utilizzare attività hello nella pipeline hello. 

## <a name="enable-connectivity"></a>Abilitare la connettività
Se si stanno spostando i dati da un **locale** archivio dati di cloud tooa server FTP (ad esempio, tooAzure nell'archiviazione Blob), installare e usare Gateway di gestione dati. Hello Gateway di gestione dati è un agente client installato nel computer locale e consente una risorsa locale tooan tooconnect dei servizi cloud. Per informazioni dettagliate, vedere [Gateway di gestione dati](data-factory-data-management-gateway.md). Per istruzioni dettagliate sulla configurazione di gateway hello e l'uso, vedere [lo spostamento dei dati tra le sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md). Si utilizza server di tooan FTP di hello gateway tooconnect, anche se il server di hello in un'infrastruttura di Azure come servizio (IaaS) macchina virtuale (VM).

È possibile tooinstall hello gateway hello stesso in locale macchina o VM IaaS come hello server FTP. Tuttavia, si consiglia di installare gateway hello in un computer distinto o contesa delle risorse tooavoid VM IaaS e per ottenere prestazioni migliori. Quando si installa il gateway hello in un computer separato, macchina hello debba essere server FTP di hello tooaccess in grado di.

## <a name="get-started"></a>Attività iniziali
È possibile creare una pipeline con l'attività di copia che sposta i dati da un'origine FTP usando diversi strumenti o API.

toocreate modo più semplice di Hello una pipeline è hello toouse **Data Factory Copia guidata**. Per una procedura dettagliata, vedere [Esercitazione: Creare una pipeline usando la Copia guidata](data-factory-copy-data-wizard-tutorial.md).

È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **PowerShell**, **modellodigestionerisorsediAzure**, **API .NET**, e **API REST**. Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia.

Se si utilizza hello o le API, eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti:

1. Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.
2. Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello.
3. Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output.

Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente. Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory. Per un esempio con le definizioni di JSON per le entità Data Factory dati toocopy utilizzato da un archivio dati FTP, vedere hello [esempio JSON: copiare i dati da blob tooAzure di server FTP](#json-example-copy-data-from-ftp-server-to-azure-blob) sezione di questo articolo.

> [!NOTE]
> Per informazioni dettagliate su toouse di formati di file e compressione supportati, vedere [formati di File e la compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).

Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che vengono utilizzati toodefine Data Factory entità specifiche tooFTP.

## <a name="linked-service-properties"></a>Proprietà del servizio collegato
Hello nella tabella seguente descrive servizio FTP collegato tooan specifico di elementi JSON.

| Proprietà | Descrizione | Obbligatorio | Predefinito |
| --- | --- | --- | --- |
| type |Impostare questo tooFtpServer. |Sì |&nbsp; |
| host |Specifica il nome di hello o indirizzo IP del server FTP hello. |Sì |&nbsp; |
| authenticationType |Specificare il tipo di autenticazione hello. |Sì |Di base, anonimo |
| username |Specificare gli utenti hello con server di accesso toohello FTP. |No |&nbsp; |
| password |Specificare la password hello per l'utente di hello (nomeutente). |No |&nbsp; |
| encryptedCredential |Specificare crittografato hello credenziali tooaccess hello FTP server. |No |&nbsp; |
| gatewayName |Specificare il nome di hello del gateway hello nel server FTP di Gateway di gestione dati tooconnect tooan locale. |No |&nbsp; |
| port |Specificare hello porta su cui hello FTP server è in ascolto. |No |21 |
| enableSsl |Specificare se toouse FTP su un canale SSL/TLS. |No |true |
| enableServerCertificateValidation |Specificare se il server tooenable SSL la convalida del certificato quando si utilizza FTP tramite il canale SSL/TLS. |No |true |

### <a name="use-anonymous-authentication"></a>Usare l'autenticazione anonima

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {        
            "authenticationType": "Anonymous",
              "host": "myftpserver.com"
        }
    }
}
```

### <a name="use-username-and-password-in-plain-text-for-basic-authentication"></a>Usare nome utente e password in testo normale per l'autenticazione di base

```JSON
{
    "name": "FTPLinkedService",
      "properties": {
    "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
      }
}
```

### <a name="use-port-enablessl-enableservercertificatevalidation"></a>Usare port, enableSsl, enableServerCertificateValidation

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

### <a name="use-encryptedcredential-for-authentication-and-gateway"></a>Usare encryptedCredential per autenticazione e gateway

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "mygateway"
        }
      }
}
```

## <a name="dataset-properties"></a>Proprietà dei set di dati
Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione di set di dati, vedere l'articolo sulla [creazione di set di dati](data-factory-create-datasets.md). Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati.

Hello **typeProperties** sezione è diverso per ogni tipo di set di dati. Fornisce informazioni che sono il tipo di set di dati toohello specifico. Hello **typeProperties** sezione per un set di dati di tipo **FileShare** ha hello le proprietà seguenti:

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| folderPath |Cartella toohello sottopercorso. Utilizzare il carattere di escape ' \ ' per i caratteri speciali nella stringa hello. Per ottenere alcuni esempi, vedere [Servizio collegato di esempio e definizioni del set di dati](#sample-linked-service-and-dataset-definitions) .<br/><br/>È possibile combinare questa proprietà con **partitionBy** toohave i percorsi delle cartelle in base alle sezioni di inizio e fine di data e ora. |Sì |
| fileName |Specificare il nome di hello del file hello in hello **folderPath** se si desidera hello tabella toorefer tooa specifici file nella cartella hello. Se non si specifica alcun valore per questa proprietà, la tabella hello punta tooall file nella cartella hello.<br/><br/>Quando **fileName** non specificato per un set di dati di output, hello nome del file hello generato è hello seguente formato: <br/><br/>Data<Guid>.txt, ad esempio: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |No |
| fileFilter |Specificare un tooselect toobe utilizzato filtro un subset di file in hello **folderPath**, anziché tutti i file.<br/><br/>I valori consentiti sono: `*` (più caratteri) e `?` (carattere singolo).<br/><br/>Esempio 1: `"fileFilter": "*.log"`<br/>Esempio 2: `"fileFilter": 2014-1-?.txt"`<br/><br/> **fileFilter** è applicabile per un set di dati di input FileShare. Questa proprietà non è supportata con Hadoop Distributed File System (HDFS). |No |
| partitionedBy |Utilizzato toospecify dinamico **folderPath** e **fileName** per dati della serie temporale. È ad esempio possibile specificare un **folderPath** contenente i parametri per ogni ora di dati. |No |
| format | è supportato i seguenti tipi di formato Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set hello **tipo** proprietà in formato tooone di questi valori. Per ulteriori informazioni, vedere hello [formato testo](data-factory-supported-file-and-compression-formats.md#text-format), [formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Parquet formato ](data-factory-supported-file-and-compression-formats.md#parquet-format) sezioni. <br><br> Se si desidera che il file toocopy come se fossero tra archivi basati su file (copia binaria), ignorare sezione formato hello in entrambe le definizioni di set di dati di input e output. |No |
| compressione | Specificare il tipo di hello e livello di compressione per dati hello. I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**, mentre i livelli supportati sono **Ottimale** e **Più veloce**. Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |No |
| useBinaryTransfer |Specificare se binario hello toouse modalità di trasferimento. Hello valori sono true per la modalità binaria (si tratta di valore predefinito di hello) e false per ASCII. Questa proprietà può essere utilizzata solo quando hello tipo di servizio collegato associata è di tipo: server FTP. |No |

> [!NOTE]
> **fileName** e **fileFilter** non possono essere usati contemporaneamente.

### <a name="use-hello-partionedby-property"></a>Utilizzare proprietà partionedBy hello
Come indicato nella sezione precedente di hello, è possibile specificare un dinamico **folderPath** e **fileName** per dati della serie temporale con hello **partitionedBy** proprietà.

toolearn sui set di dati serie ora, la pianificazione e le sezioni, vedere [creazione dei DataSet](data-factory-create-datasets.md), [pianificazione ed esecuzione](data-factory-scheduling-and-execution.md), e [creazione di pipeline](data-factory-create-pipelines.md).

#### <a name="sample-1"></a>Esempio 1

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
In questo esempio, {Slice} viene sostituito con il valore di hello della variabile di sistema di Data Factory SliceStart, in hello formato (YYYYMMDDHH) specificato. Hello SliceStart fa riferimento l'ora toostart sezione hello. percorso della cartella Hello è diversa per ogni sezione. Ad esempio: wikidatagateway/wikisampledataout/2014100103 o wikidatagateway/wikisampledataout/2014100104.

#### <a name="sample-2"></a>Esempio 2

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
In questo esempio hello anno, mese, giorno e ora della proprietà SliceStart vengono estratti in variabili distinte che vengono utilizzate da hello **folderPath** e **fileName** proprietà.

## <a name="copy-activity-properties"></a>Proprietà dell'attività di copia
Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione delle attività, vedere l'articolo sulla [creazione di pipeline](data-factory-create-pipelines.md). Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.

Le proprietà disponibili nella hello **typeProperties** sezione di hello hello attività, invece, variano in base a ogni tipo di attività. Per attività di copia hello, le proprietà del tipo hello variano a seconda di hello tipi di origini e sink.

Nell'attività di copia, l'origine hello è di tipo **FileSystemSource**, hello seguenti proprietà è disponibile in **typeProperties** sezione:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| ricorsiva |Indica se hello i dati letti in modo ricorsivo dalle sottocartelle di hello o solo dalla cartella specificata hello. |True, False (valore predefinito) |No |

## <a name="json-example-copy-data-from-ftp-server-tooazure-blob"></a>Esempio JSON: copiare i dati da tooAzure server FTP Blob
Questo esempio viene illustrato come toocopy dati da un tooAzure server FTP nell'archiviazione Blob. Tuttavia, i dati possono essere copiati direttamente tooany di hello sink hello dichiarato nella [archivi dati e formati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats), utilizzando attività di copia hello in Data Factory.  

Negli esempi seguenti Hello forniscono definizioni JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), o [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):

* Un servizio collegato di tipo [FtpServer](#linked-service-properties)
* Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
* Un [set di dati](data-factory-create-datasets.md) di input di tipo [FileShare](#dataset-properties)
* Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)
* Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [FileSystemSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)

esempio Hello copia dati da un tooan server FTP blob di Azure ogni ora. proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.

### <a name="ftp-linked-service"></a>Servizio collegato FTP

In questo esempio viene utilizzata l'autenticazione di base, con nome utente hello e una password in testo normale. È inoltre possibile utilizzare uno dei seguenti modi hello:

* Autenticazione anonima
* Autenticazione di base con credenziali crittografate
* FTP su SSL/TLS (FTPS)

Vedere hello [servizio collegato FTP](#linked-service-properties) sezione per diversi tipi di autenticazione è possibile utilizzare.

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
    "type": "FtpServer",
    "typeProperties": {
        "host": "myftpserver.com",           
        "authenticationType": "Basic",
        "username": "Admin",
        "password": "123456"
    }
  }
}
```
### <a name="azure-storage-linked-service"></a>Servizio collegato Archiviazione di Azure

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
### <a name="ftp-input-dataset"></a>Set di dati di input FTP

Questo set di dati fa riferimento la cartella FTP toohello `mysharedfolder` e file `test.csv`. Hello pipeline copie hello toohello destinazione file.

Impostazione **esterno** troppo**true** informa il servizio di Data Factory hello hello set di dati è esterno toohello data factory e non viene generato da un'attività nella data factory di hello.

```JSON
{
  "name": "FTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "FTPLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv",
      "useBinaryTransfer": true
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

### <a name="azure-blob-output-dataset"></a>Set di dati di output del BLOB di Azure

I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1). percorso della cartella Hello per blob hello viene valutato dinamicamente, in base a ora di inizio hello della sezione hello che viene elaborato. percorso della cartella Hello Usa le parti di anno, mese, giorno e ore hello hello ora di inizio.

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/ftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="a-copy-activity-in-a-pipeline-with-file-system-source-and-blob-sink"></a>Un'attività di copia in una pipeline con un'origine su file system e un sink BLOB

pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output, senza che sia pianificato toorun ogni ora. Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**FileSystemSource**, hello e **sink** tipo è stato impostato troppo**BlobSink**.

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
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
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00Z",
        "end": "2016-08-24T19:00:00Z"
    }
}
```
> [!NOTE]
> colonne toomap toocolumns set di dati di origine dal sink set di dati, vedere [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).

## <a name="next-steps"></a>Passaggi successivi
Vedere hello seguenti articoli:

* toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento (attività di copia) dei dati in Data Factory e toooptimize modi diversi, vedere hello [copiare ottimizzazione Guida e alle prestazioni di attività](data-factory-copy-activity-performance.md).

* Per istruzioni dettagliate per la creazione di una pipeline con attività di copia, vedere hello [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
