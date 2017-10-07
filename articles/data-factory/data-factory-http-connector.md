---
title: aaaMove dati da un'origine HTTP - Azure | Documenti Microsoft
description: Informazioni su come origine dei dati toomove da un locale o un cloud HTTP usando Azure Data Factory.
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
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: e39b9cbff870aef4be91938cacff39a2fd12d64a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-http-source-using-azure-data-factory"></a>Spostare i dati da un'origine HTTP usando Azure Data Factory
In questo articolo descrive come toouse hello attività di copia dei dati toomove Data Factory di Azure da un tooa di endpoint HTTP in locale/cloud supportato archivio dati sink. In questo articolo si basa su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo che presenta una panoramica generale di spostamento dei dati con l'elenco di attività e hello copia di archivi dati supportata come origine/sink.

Data factory di attualmente supporta solo lo spostamento di dati da un HTTP origine tooother archivi di dati, ma non lo spostamento dei dati da altri dati archivia destinazione tooan HTTP.

## <a name="supported-scenarios-and-authentication-types"></a>Scenari supportati e tipi di autenticazione
È possibile utilizzare HTTP connettore tooretrieve dati **sia in locale e cloud endpoint HTTP/s** mediante il protocollo HTTP **ottenere** o **POST** metodo. è supportato i seguenti tipi di autenticazione Hello: **anonimo**, **base**, **Digest**, **Windows**, e  **ClientCertificate**. Si noti la differenza hello tra questo connettore e hello [connettore tabella Web](data-factory-web-table-connector.md) è: hello quest'ultimo è utilizzato tooextract tabella contenuta da una pagina web HTML.

Quando si copiano dati da un endpoint HTTP locale, è necessario installare un Gateway di gestione di dati nell'ambiente locale hello/Azure VM. Vedere [lo spostamento dei dati tra le sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn articolo sul Gateway di gestione dati e istruzioni dettagliate su come configurare il gateway hello.

## <a name="getting-started"></a>introduttiva
È possibile creare una pipeline con l'attività di copia che sposta i dati da un'origine HTTP usando diversi strumenti/API.

- toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**. Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.

- È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**. Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia. Per esempi di JSON dati toocopy tooAzure origine HTTP nell'archiviazione Blob, vedere [esempi JSON](#json-examples) sezione di questo articolo.

## <a name="linked-service-properties"></a>Proprietà del servizio collegato
Hello nella tabella seguente fornisce una descrizione del servizio specifico tooHTTP collegati gli elementi JSON.

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| type | proprietà di tipo Hello deve essere impostata su: `Http`. | Sì |
| URL | URL toohello Server Web di base | Sì |
| authenticationType | Specifica il tipo di autenticazione hello. I valori consentiti sono: **Anonymous**, **Basic**, **Digest**, **Windows** e **ClientCertificate**. <br><br> Vedere rispettivamente toosections riportata sotto questa tabella in più proprietà e gli esempi JSON per i tipi di autenticazione. | Sì |
| enableServerCertificateValidation | Specificare se il server tooenable SSL la convalida del certificato se l'origine è il Server Web HTTPS | No, il valore predefinito è true |
| gatewayName | Nome di hello Gateway di gestione dati tooconnect tooan locale origine HTTP. | Sì se si copiano i dati da un'origine HTTP locale. |
| encryptedCredential | Credenziali crittografate tooaccess hello endpoint HTTP. Generati automaticamente quando si configurano le informazioni di autenticazione hello in copia guidata o hello ClickOnce finestra di dialogo popup. | No. Applicare solo se si copiano i dati da un server HTTP locale. |

Vedere [spostare dati tra origini locali e cloud hello con Gateway di gestione dati](data-factory-move-data-between-onprem-and-cloud.md) per informazioni dettagliate sull'impostazione delle credenziali per l'origine dati di connettore HTTP locale.

### <a name="using-basic-digest-or-windows-authentication"></a>Usando l'autenticazione Basic, Digest o Windows

Impostare `authenticationType` come `Basic`, `Digest`, o `Windows`e specificare le proprietà seguenti, oltre alle hello generico connettore HTTP quelli illustrati in precedenza hello:

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| username | Nome utente tooaccess hello endpoint HTTP. | Sì |
| password | Password per l'utente di hello (nomeutente). | Sì |

#### <a name="example-using-basic-digest-or-windows-authentication"></a>Esempio: usando l'autenticazione Basic, Digest or Windows

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "basic",
            "url" : "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

### <a name="using-clientcertificate-authentication"></a>Usando l'autenticazione ClientCertificate

impostare l'autenticazione di base toouse, `authenticationType` come `ClientCertificate`e specificare le proprietà seguenti, oltre alle hello generico connettore HTTP quelli illustrati in precedenza hello:

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| embeddedCertData | Hello contenuto con codifica Base64 di dati binari del file di scambio di informazioni personali (PFX) hello. | Specificare entrambi hello `embeddedCertData` o `certThumbprint`. |
| certThumbprint | Hello identificazione personale del certificato hello che è stata installata nell'archivio certificati del computer gateway. Applicare solo se si copiano i dati da un'origine HTTP locale. | Specificare entrambi hello `embeddedCertData` o `certThumbprint`. |
| password | Password associata al certificato hello. | No |

Se si utilizza `certThumbprint` per hello e autenticazione il certificato è installato nell'archivio personale di hello del computer locale hello, è necessario che il servizio gateway toogrant hello autorizzazione di lettura toohello:

1. Avviare Microsoft Management Console (MMC). Aggiungere hello **certificati** snap-in tale hello destinazioni **Computer locale**.
2. Espandere **Certificati**, **Personali** e fare clic su **Certificati**.
3. Certificato hello dall'archivio personale hello e scegliere **tutte le attività**->**Gestisci chiavi Private...**
3. In hello **sicurezza** scheda, aggiungere l'account utente di hello in cui è in esecuzione servizio Host di Gateway di gestione di dati con certificato toohello di hello accesso in lettura.  

#### <a name="example-using-client-certificate"></a>Esempio: utilizzo di un certificato client
Questo collegato collegamenti al servizio data factory tooan locale HTTP server web. Usa un certificato client è installato nel computer di hello con Gateway di gestione di dati installati.

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"

        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a>Esempio: utilizzo di un certificato client in un file
Questo collegato collegamenti al servizio data factory tooan locale HTTP server web. Usa un file del certificato client nel computer di hello con Gateway di gestione di dati installati.

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

## <a name="dataset-properties"></a>Proprietà dei set di dati
Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo. Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.

Hello **typeProperties** sezione è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello. sezione Hello typeProperties per set di dati di tipo **Http** ha hello seguenti proprietà

| Proprietà | Descrizione | Obbligatorio |
|:--- |:--- |:--- |
| type | Tipo di hello di hello set di dati specificato. deve essere impostato troppo`Http`. | Sì |
| relativeUrl | Una risorsa relativa di URL toohello che contiene dati hello. Quando non viene specificato alcun percorso, viene utilizzato solo URL hello specificato nella definizione di servizio collegato hello. <br><br> tooconstruct URL dinamico, è possibile utilizzare [funzioni di Data Factory e le variabili di sistema](data-factory-functions-variables.md), ad esempio, "URL relativo": "$$Text.Format ('/ my/report? mese = {0:yyyy}-{0:MM} & fmt = csv', SliceStart)". | No |
| requestMethod | Metodo HTTP. I valori consentiti sono **GET** o **POST**. | No. Il valore predefinito è `GET`. |
| additionalHeaders | Intestazioni richiesta HTTP aggiuntive. | No |
| requestBody | Il corpo della richiesta HTTP. | No |
| format | Se si desidera toosimply **recuperare i dati di hello da endpoint HTTP come-è** senza analizzarlo, ignorare questa impostazione di formato. <br><br> Se si desidera tooparse hello HTTP risposta contenuto durante la copia, è supportato i seguenti tipi di formato hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**. Per altre informazioni, vedere le sezioni [TextFormat](data-factory-supported-file-and-compression-formats.md#text-format), [JsonFormat](data-factory-supported-file-and-compression-formats.md#json-format), [AvroFormat](data-factory-supported-file-and-compression-formats.md#avro-format), [OrcFormat](data-factory-supported-file-and-compression-formats.md#orc-format) e [ParquetFormat](data-factory-supported-file-and-compression-formats.md#parquet-format). |No |
| compressione | Specificare il tipo di hello e livello di compressione per dati hello. I tipi supportati sono **GZip**, **Deflate**, **BZip2** e **ZipDeflate**. I livelli supportati sono **Ottimale** e **Più veloce**. Per altre informazioni, vedere [File e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |No |

### <a name="example-using-hello-get-default-method"></a>Esempio: hello metodo GET (impostazione predefinita)

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

### <a name="example-using-hello-post-method"></a>Esempio: utilizzo di metodo POST hello

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
           "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a>Proprietà dell'attività di copia
Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo. Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.

Le proprietà disponibili nella hello **typeProperties** sezione di attività hello hello invece variano in base a ogni tipo di attività. Per attività di copia, variano a seconda dei tipi di hello di origini e sink.

Attualmente, quando origine hello in attività di copia è di tipo **HttpSource**, hello le proprietà seguenti è supportato.

| Proprietà | Descrizione | Obbligatorio |
| -------- | ----------- | -------- |
| httpRequestTimeout | Hello timeout (TimeSpan) per hello HTTP richiesta tooget una risposta. È hello timeout tooget una risposta, dati di risposta non hello timeout tooread. | No. Valore predefinito: 00:01:40 |

## <a name="supported-file-and-compression-formats"></a>Formati di file e di compressione supportati
Per i dettagli, vedere l'articolo relativo ai [file e formati di compressione in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).

## <a name="json-examples"></a>Esempi JSON
Hello di esempio seguente fornisce una definizione JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Visualizzano come origine dei dati di toocopy da HTTP tooAzure nell'archiviazione Blob. Tuttavia, i dati possono essere copiati **direttamente** da una qualsiasi delle origini tooany di sink hello indicato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory.

### <a name="example-copy-data-from-http-source-tooazure-blob-storage"></a>Esempio: Copiare i dati da tooAzure origine HTTP nell'archiviazione Blob
soluzione di Data Factory per l'esempio Hello contiene hello entità Data Factory di seguito:

1. Un servizio collegato di tipo [HTTP](#linked-service-properties).
2. Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Un [set di dati](data-factory-create-datasets.md) di input di tipo [HTTP](#dataset-properties).
4. Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [HttpSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

esempio Hello copia dati da un tooan origine HTTP blob di Azure ogni ora. proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.

### <a name="http-linked-service"></a>Servizio collegato HTTP
In questo esempio utilizza hello HTTP collegato del servizio con l'autenticazione anonima. Per i diversi tipi di autenticazione disponibili, vedere la sezione relativa al [servizio collegato HTTP](#linked-service-properties).

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
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

### <a name="http-input-dataset"></a>Set di dati di input HTTP
Impostazione **esterno** troppo**true** informa il servizio di Data Factory hello hello set di dati è esterna toohello data factory e non viene generato da un'attività nella data factory di hello.

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}

```

### <a name="azure-blob-output-dataset"></a>Set di dati di output del BLOB di Azure

I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1).

```JSON
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/Movies"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

### <a name="pipeline-with-copy-activity"></a>Pipeline con attività di copia

pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e viene pianificata toorun ogni ora. Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**HttpSource** e **sink** tipo è stato impostato troppo**BlobSink**.

Vedere [HttpSource](#copy-activity-properties) per elenco hello delle proprietà supportate da hello HttpSource.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "HttpSourceToAzureBlob",
        "description": "Copy from an HTTP source tooan Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "HttpSourceDataInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "HttpSource"
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

> [!NOTE]
> colonne toomap toocolumns set di dati di origine dal sink set di dati, vedere [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Ottimizzazione delle prestazioni
Vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.
