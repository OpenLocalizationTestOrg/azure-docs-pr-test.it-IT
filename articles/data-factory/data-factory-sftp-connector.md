---
title: aaaMove dati dal server SFTP con Data Factory di Azure | Documenti Microsoft
description: Per ulteriori informazioni vedere toomove dati da un locale o un server SFTP cloud con Data Factory di Azure.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jingwang
ms.openlocfilehash: b976289e2c1b1899634bb5565b375499077fa554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-sftp-server-using-azure-data-factory"></a>Spostare dati da un server SFTP usando Azure Data Factory
In questo articolo descrive come toouse hello attività di copia dei dati toomove Data Factory di Azure da un tooa di server SFTP in locale/cloud supportato archivio dati sink. In questo articolo si basa su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo che presenta una panoramica generale di spostamento dei dati con l'elenco di attività e hello copia di archivi dati supportata come origine/sink.

Data factory di supporta attualmente solo lo spostamento di dati da tooother un server SFTP Archivia, ma non per lo spostamento dei dati da altri dati archivia server SFTP tooan. Supporta i server SFTP locali e cloud.

> [!NOTE]
> Attività di copia non elimina i file di origine hello dopo che è la destinazione toohello copiati correttamente. Se è necessario toodelete file di origine hello dopo una copia ha esito positivo, creare un file di hello toodelete di attività personalizzata e utilizzare attività hello nella pipeline hello. 

## <a name="supported-scenarios-and-authentication-types"></a>Scenari supportati e tipi di autenticazione
È possibile utilizzare questo SFTP connettore toocopy dati **entrambi i server SFTP e server SFTP locali cloud**. **Base** e **parametri SshPublicKey** tipi di autenticazione sono supportati durante la connessione server SFTP toohello.

Quando si copiano dati da un server SFTP in locale, è necessario installare un Gateway di gestione di dati nell'ambiente locale hello/Azure VM. Vedere [Gateway di gestione dati](data-factory-data-management-gateway.md) per dettagli sul gateway hello. Vedere [lo spostamento dei dati tra le sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) articolo per istruzioni dettagliate sulla configurazione di gateway hello e l'uso.

## <a name="getting-started"></a>introduttiva
È possibile creare una pipeline con l'attività di copia che sposta i dati da un'origine SFTP usando diversi strumenti/API.

- toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**. Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.

- È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**. Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia. Per esempi di JSON dati toocopy tooAzure server SFTP nell'archiviazione Blob, vedere [esempio JSON: copiare i dati da blob di tooAzure server SFTP](#json-example-copy-data-from-sftp-server-to-azure-blob) sezione di questo articolo.

## <a name="linked-service-properties"></a>Proprietà del servizio collegato
Hello nella tabella seguente fornisce una descrizione del servizio specifico tooFTP collegati gli elementi JSON.

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- | --- |
| type | proprietà di tipo Hello deve essere impostata troppo`Sftp`. |Sì |
| host | Nome o indirizzo IP del server SFTP hello. |Sì |
| port |Porta su cui hello SFTP server è in ascolto. valore predefinito di Hello è: 21 |No |
| authenticationType |Specificare il tipo di autenticazione. Valori consentiti: **Base**, **SshPublicKey**. <br><br> Fare riferimento troppo[tramite l'autenticazione di base](#using-basic-authentication) e [tramite SSH autenticazione a chiave pubblica](#using-ssh-public-key-authentication) sezioni su altre proprietà e gli esempi JSON rispettivamente. |Sì |
| skipHostKeyValidation | Specificare se tooskip chiave convalida dell'host. | No. Hello valore predefinito: false |
| hostKeyFingerprint | Specificare impronte digitali hello della chiave host hello. | Sì se hello `skipHostKeyValidation` è impostato toofalse.  |
| gatewayName |Nome di hello Gateway di gestione dati tooconnect tooan locale server SFTP. | Sì se si copiano i dati da un server SFTP locale. |
| encryptedCredential | Server SFTP hello tooaccess credenziali crittografate. Generati automaticamente quando si specifica l'autenticazione di base (password e nome utente) o parametri SshPublicKey (nome utente + percorso della chiave privata o contenuto) nella copia guidata o hello ClickOnce finestra di dialogo popup. | No. Applicare solo se si copiano i dati da un server SFTP locale. |

### <a name="using-basic-authentication"></a>Uso dell'autenticazione di base

impostare l'autenticazione di base toouse, `authenticationType` come `Basic`e specificare le proprietà seguenti, oltre alle hello connettore SFTP oggetti generici introdotte nell'ultima sezione hello hello:

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- | --- |
| username | Utente che dispone di server di accesso toohello SFTP. |Sì |
| password | Password per l'utente di hello (nomeutente). | Sì |

#### <a name="example-basic-authentication"></a>Esempio: autenticazione di base
```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a>Esempio: autenticazione di base con credenziali crittografate

```JSON
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
      }
}
```

### <a name="using-ssh-public-key-authentication"></a>Uso dell'autenticazione con chiave pubblica SSH

impostare toouse SSH autenticazione a chiave pubblica, `authenticationType` come `SshPublicKey`e specificare le proprietà seguenti, oltre alle hello connettore SFTP oggetti generici introdotte nell'ultima sezione hello hello:

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- | --- |
| username |Utente che dispone di server di accesso toohello SFTP |Sì |
| privateKeyPath | Specificare un percorso assoluto toohello file di chiave privata accessibile tale gateway. | Specificare entrambi hello `privateKeyPath` o `privateKeyContent`. <br><br> Applicare solo se si copiano i dati da un server SFTP locale. |
| privateKeyContent | Una stringa serializzata del contenuto di chiave privata di hello. Hello Copia guidata è possibile leggere il file di chiave privata di hello ed estrarre automaticamente il contenuto di chiave privata di hello. Se si utilizza qualsiasi altro strumento o SDK, è possibile utilizzare proprietà privateKeyPath hello. | Specificare entrambi hello `privateKeyPath` o `privateKeyContent`. |
| passPhrase | Specificare hello frase/password toodecrypt hello privati passkey se i file di chiave hello è protetto da una passphrase. | Sì se il file di chiave privata di hello è protetto da una passphrase. |

> [!NOTE]
> Il connettore SFTP supporta solo chiavi OpenSSH. Assicurarsi che il file di chiave sia nel formato corretto hello. È possibile utilizzare lo strumento Putty tooconvert dal formato tooOpenSSH *.ppk.

#### <a name="example-sshpublickey-authentication-using-private-key-filepath"></a>Esempio: Autenticazione SshPublicKey con chiave privata filePath

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a>Esempio: Autenticazione SshPublicKey con contenuto della chiave privata

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

## <a name="dataset-properties"></a>Proprietà dei set di dati
Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo. Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati.

Hello **typeProperties** sezione è diverso per ogni tipo di set di dati. Fornisce informazioni che sono il tipo di set di dati toohello specifico. sezione Hello typeProperties per un set di dati di tipo **FileShare** set di dati è hello le proprietà seguenti:

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| folderPath |Toohello sottocartella percorso. Utilizzare il carattere di escape ' \ ' per i caratteri speciali nella stringa hello. Per ottenere alcuni esempi, vedere [Servizio collegato di esempio e definizioni del set di dati](#sample-linked-service-and-dataset-definitions) .<br/><br/>È possibile combinare questa proprietà con **partitionBy** toohave i percorsi delle cartelle in base a intervallo iniziale o finale data e ora. |Sì |
| fileName |Specificare il nome di hello del file hello in hello **folderPath** se si desidera hello tabella toorefer tooa specifici file nella cartella hello. Se non si specifica alcun valore per questa proprietà, la tabella hello punta tooall file nella cartella hello.<br/><br/>Quando il nome di file non viene specificato per un set di dati di output, il nome di hello del file hello generato sarebbe in hello segue questo formato: <br/><br/>Data.<Guid>.txt, ad esempio: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |No |
| fileFilter |Specificare un filtro toobe tooselect un subset di file in hello folderPath, anziché tutti i file.<br/><br/>I valori consentiti sono: `*` (più caratteri) e `?` (carattere singolo).<br/><br/>Esempi 1: `"fileFilter": "*.log"`<br/>Esempio 2: `"fileFilter": 2014-1-?.txt"`<br/><br/> fileFilter è applicabile per un set di dati di input FileShare. Questa proprietà non è supportata con HDFS. |No |
| partitionedBy |partitionedBy può essere utilizzato toospecify un folderPath dinamica, il nome file per i dati della serie temporale. Ad esempio, folderPath con parametri per ogni ora di dati. |No |
| format | è supportato i seguenti tipi di formato Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Set hello **tipo** proprietà in formato tooone di questi valori. Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Se si desidera troppo**copiare i file come-è** tra archivi basati su file (copia binaria), ignorare le sezioni di formato hello in entrambe le definizioni di set di dati di input e output. |No |
| compressione | Specificare il tipo di hello e livello di compressione per dati hello. I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**. I livelli supportati sono **Ottimale** e **Più veloce**. Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |No |
| useBinaryTransfer |Specificare se usare la modalità di trasferimento binario. True per la modalità binaria e false per ASCII. Valore predefinito: True. Questa proprietà può essere usata solo quando il tipo di servizio collegato associato è di tipo: FtpServer. |No |

> [!NOTE]
> filename e fileFilter non possono essere usati contemporaneamente.

### <a name="using-partionedby-property"></a>Uso della proprietà partionedBy
Come indicato nella sezione precedente di hello, è possibile specificare un folderPath dinamica, il nome file per i dati della serie temporale con partitionedBy. È possibile farlo con le macro Data Factory di hello e variabile di sistema hello SliceStart, SliceEnd che indicano hello periodo di tempo logico per una sezione di dati specificato.

toolearn sui set di dati serie ora, la pianificazione e le sezioni, vedere [la creazione di DataSet](data-factory-create-datasets.md), [pianificazione ed esecuzione](data-factory-scheduling-and-execution.md), e [la creazione di pipeline](data-factory-create-pipelines.md) articoli.

#### <a name="sample-1"></a>Esempio 1.

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
In questo esempio {Slice} viene sostituito con valore hello della variabile di sistema di Data Factory SliceStart nel formato hello (YYYYMMDDHH) specificato. Hello SliceStart fa riferimento l'ora toostart sezione hello. Hello folderPath è diversa per ogni sezione. Esempio: wikidatagateway/wikisampledataout/2014100103 o wikidatagateway/wikisampledataout/2014100104.

#### <a name="sample-2"></a>Esempio 2:

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
In questo esempio l'anno, il mese, il giorno e l'ora di SliceStart vengono estratti in variabili separate che vengono usate dalle proprietà folderPath e fileName.

## <a name="copy-activity-properties"></a>Proprietà dell'attività di copia
Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo. Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.

Mentre le proprietà di hello disponibili nella sezione typeProperties hello dell'attività hello variano in base a ogni tipo di attività. Per attività di copia, le proprietà del tipo hello variano a seconda di hello tipi di origini e sink.

[!INCLUDE [data-factory-file-system-source](../../includes/data-factory-file-system-source.md)]

## <a name="supported-file-and-compression-formats"></a>Formati di file e di compressione supportati
Per i dettagli, vedere l'articolo relativo ai [file e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).

## <a name="json-example-copy-data-from-sftp-server-tooazure-blob"></a>Esempio JSON: Copiare i dati da blob di tooAzure server SFTP
esempio Hello fornisce definizioni di JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Visualizzano come origine dei dati di toocopy da SFTP tooAzure nell'archiviazione Blob. Tuttavia, i dati possono essere copiati **direttamente** da una qualsiasi delle origini tooany di sink hello indicato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory.

> [!IMPORTANT]
> Questo esempio fornisce frammenti di codice JSON. Non include istruzioni dettagliate per la creazione di data factory di hello. Le istruzioni dettagliate sono disponibili nell'articolo [Spostare dati tra origini locali e il cloud](data-factory-move-data-between-onprem-and-cloud.md) .

esempio Hello è hello entità factory di dati seguenti:

* Un servizio collegato di tipo [sftp](#linked-service-properties).
* Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Un [set di dati](data-factory-create-datasets.md) di input di tipo [FileShare](#dataset-properties).
* Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [FileSystemSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

esempio Hello copia dati da un tooan server SFTP blob di Azure ogni ora. proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.

**Servizio collegato SFTP**

Nell'esempio viene utilizzata l'autenticazione di base hello con nome utente e password in testo normale. È inoltre possibile utilizzare uno dei seguenti modi hello:

* Autenticazione di base con credenziali crittografate
* Autenticazione con chiave pubblica SSH

Per i diversi tipi di autenticazione disponibili, vedere la sezione relativa al [servizio collegato FTP](#linked-service-properties).

```JSON

{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "myuser",
            "password": "mypassword",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```
**Servizio collegato Archiviazione di Azure**

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
**Set di dati di input SFTP**

Questo set di dati si riferisce cartella SFTP toohello `mysharedfolder` e file `test.csv`. Hello pipeline copie hello toohello destinazione file.

L'impostazione "external": "true" informa il servizio di Data Factory hello hello set di dati è esterna toohello data factory e non viene generato da un'attività nella data factory di hello.

```JSON
{
  "name": "SFTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "SftpLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**Set di dati di output del BLOB di Azure**

I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1). percorso della cartella Hello per blob hello viene valutato dinamicamente in base a ora di inizio hello della sezione hello che viene elaborato. percorso della cartella Hello Usa le parti di anno, mese, giorno e ore dell'ora di inizio hello.

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Pipeline con attività di copia**

pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e viene pianificata toorun ogni ora. Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**FileSystemSource** e **sink** tipo è stato impostato troppo**BlobSink**.

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
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
        "start": "2017-02-20T18:00:00Z",
        "end": "2017-02-20T19:00:00Z"
    }
}
```

## <a name="performance-and-tuning"></a>Ottimizzazione delle prestazioni
Vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.

## <a name="next-steps"></a>Passaggi successivi
Vedere hello seguenti articoli:

* [Esercitazione dell'attività di copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per le istruzioni dettagliate della creazione di una pipeline con un'attività di copia.
