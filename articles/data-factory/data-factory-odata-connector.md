---
title: aaaMove dati da origini di OData | Documenti Microsoft
description: Informazioni su come origini dei dati toomove da OData usando Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: de28fa56-3204-4546-a4df-21a21de43ed7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 328efe4fd274fb3e54c1d2f209e4614c77c1ff37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-a-odata-source-using-azure-data-factory"></a>Spostare i dati da un'origine OData usando Azure Data Factory
Questo articolo spiega come toouse hello attività di copia dei dati toomove Data Factory di Azure da un'origine OData. È basato su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia hello.

È possibile copiare dati da un archivio di dati OData origine tooany supportati sink. Per un elenco di dati supportati archivi come sink dall'attività di copia hello, vedere hello [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabella. Data factory di supporta attualmente solo lo spostamento di archivi di dati da dati tooother origine OData, ma non per lo spostamento dei dati da altri dati di origine OData tooan Archivia. 

## <a name="supported-versions-and-authentication-types"></a>Versioni supportate e tipi di autenticazione
Questo connettore OData supporta OData versione 3.0 e 4.0 e la copia dei dati dalle origini OData cloud e locali. Per hello quest'ultimo, è necessario tooinstall hello Gateway di gestione dati. Vedere l’articolo [Spostare dati tra cloud e locale](data-factory-move-data-between-onprem-and-cloud.md) per informazioni dettagliate sui Gateway di Gestione dati.

Sono supportati i tipi di autenticazione seguenti:

* tooaccess **cloud** feed OData, è possibile utilizzare anonima, base (nome utente e password) o Azure Active Directory basato su autenticazione OAuth.
* tooaccess **locale** feed OData, è possibile usare anonima, base (nome utente e password), o l'autenticazione di Windows.

## <a name="getting-started"></a>introduttiva
È possibile creare una pipeline con l'attività di copia che sposta i dati da un'origine OData usando diversi strumenti/API.

toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**. Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.

È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**. Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia. 

Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti: 

1. Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.
2. Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello. 
3. Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output. 

Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente. Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.  Per un esempio con le definizioni di JSON per le entità Data Factory dati toocopy utilizzato da un'origine OData, vedere [esempio JSON: copiare i dati da tooAzure origine OData Blob](#json-example-copy-data-from-odata-source-to-azure-blob) sezione di questo articolo. 

Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che sono utilizzati toodefine Data Factory entità specifiche tooOData origine:

## <a name="linked-service-properties"></a>Proprietà del servizio collegato
Hello nella tabella seguente fornisce una descrizione del servizio specifico tooOData collegato gli elementi JSON.

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| type |proprietà di tipo Hello deve essere impostata su: **OData** |Sì |
| URL |URL del servizio OData hello. |Sì |
| authenticationType |Tipo di autenticazione usato tooconnect toohello un'origine OData. <br/><br/> Per OData in cloud, i valori possibili sono Anonymous, Basic e OAuth. Si noti che Azure Data Factory attualmente supporta solo OAuth basato su Azure Active Directory). <br/><br/> Per OData locale, i valori possibili sono Anonima, Di base e Windows. |Sì |
| username |Specificare il nome utente se si usa l'autenticazione di base. |Sì (solo se si usa l'autenticazione di base) |
| password |Specificare la password per account utente di hello specificato per il nome utente hello. |Sì (solo se si usa l'autenticazione di base) |
| authorizedCredential |Se si utilizza OAuth, fare clic su **Authorize** pulsante nell'Editor o hello Data Factory Copia guidata e immettere le credenziali, il valore di hello di questa proprietà verrà generato automaticamente. |Sì (solo se si usa l'autenticazione OAuth) |
| gatewayName |Nome del gateway hello hello servizio Data Factory deve usare servizio OData di tooconnect toohello locale. Specificare solo se si copiano dati da un'origine OData locale. |No |

### <a name="using-basic-authentication"></a>Uso dell'autenticazione di base
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Basic",
            "username": "username",
            "password": "password"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a>Uso dell'autenticazione anonima
```json
{
    "name": "ODataLinkedService",
        "properties":
    {
        "type": "OData",
        "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        }
    }
}
```

### <a name="using-windows-authentication-accessing-on-premises-odata-source"></a>Uso dell'autenticazione di Windows per accedere all'origine OData locale
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of on-premises OData source e.g. Dynamics CRM>",
            "authenticationType": "Windows",
            "username": "domain\\user",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-oauth-authentication-accessing-cloud-odata-source"></a>Uso dell'autenticazione OAuth per accedere all'origine OData cloud
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of cloud OData source e.g. https://<tenant>.crm.dynamics.com/XRMServices/2011/OrganizationData.svc>",
            "authenticationType": "OAuth",
            "authorizedCredential": "<auto generated by clicking hello Authorize button on UI>"
        }
    }
}
```

## <a name="dataset-properties"></a>Proprietà dei set di dati
Per un elenco completo delle proprietà disponibili per la definizione di set di dati e sezioni, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo. Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.

Hello **typeProperties** sezione è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello. sezione Hello typeProperties per set di dati di tipo **ODataResource** (che include set di dati OData) è hello seguenti proprietà

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| path |Percorso toohello risorse OData |No |

## <a name="copy-activity-properties"></a>Proprietà dell'attività di copia
Per un elenco completo delle proprietà disponibili per la definizione delle attività e delle sezioni, vedere hello [la creazione di pipeline](data-factory-create-pipelines.md) articolo. Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e criteri.

Le proprietà disponibili nella sezione typeProperties hello di attività hello hello invece variano in base a ogni tipo di attività. Per attività di copia, variano a seconda dei tipi di hello di origini e sink.

Quando l'origine è di tipo **RelationalSource** (che include OData) hello le proprietà seguenti sono disponibile nella sezione typeProperties:

| Proprietà | Descrizione | Esempio | Obbligatorio |
| --- | --- | --- | --- |
| query |Utilizzare i dati di tooread hello query personalizzata. |"?$select=Name, Description&$top=5" |No |

## <a name="type-mapping-for-odata"></a>Mapping dei tipi per OData
Come accennato in hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, attività di copia esegue le conversioni dai tipi di origine tipi toosink automatico con hello approccio in due passaggi.

1. Conversione dal tipo di origine nativa tipi too.NET
2. Eseguire la conversione da tipo di sink toonative tipo .NET

Quando si spostano dati da OData, hello mapping seguenti vengono utilizzati dal tipo di too.NET tipi OData.

| Tipo di dati OData | Tipo .NET |
| --- | --- |
| Edm.Binary |Byte[] |
| Edm.Boolean |Booleano |
| Edm.Byte |Byte[] |
| Edm.DateTime |DateTime |
| Edm.Decimal |Decimale |
| Edm.Double |Double |
| Edm.Single |Single |
| Edm.Guid |Guid |
| Edm.Int16 |Int16 |
| Edm.Int32 |Int32 |
| Edm.Int64 |Int64 |
| Edm.SByte |Int16 |
| Edm.String |String |
| Edm.Time |Intervallo di tempo |
| Edm.DateTimeOffset |Datetimeoffset |

> [!Note]
> Tipi di dati OData complessi. Gli oggetti, ad esempio, non sono supportati.

## <a name="json-example-copy-data-from-odata-source-tooazure-blob"></a>Esempio JSON: copiare i dati da tooAzure origine OData Blob
In questo esempio vengono fornite le definizioni di JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Visualizzano come origine dei dati di toocopy da OData tooan archiviazione Blob di Azure. Tuttavia, i dati possono essere copiati tooany di sink hello indicato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory. esempio Hello è hello entità Data Factory di seguito:

1. Un servizio collegato di tipo [OData](#linked-service-properties).
2. Un servizio collegato di tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Un [set di dati](data-factory-create-datasets.md) di input di tipo [ODataResource](#dataset-properties).
4. Un [set di dati](data-factory-create-datasets.md) di output di tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

esempio Hello copia dati da una query su un tooan origine OData blob di Azure ogni ora. proprietà JSON Hello usata in questi esempi sono descritti nelle sezioni riportate di seguito esempi di hello.

**Servizio collegato di OData:** in questo esempio viene utilizzata l'autenticazione anonima di hello. Per i diversi tipi di autenticazione disponibili, vedere la sezione [Servizio collegato OData](#linked-service-properties) .

```json
{
    "name": "ODataLinkedService",
        "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
            }
        }
}
```

**Servizio collegato Archiviazione di Azure:**

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

**Set di dati di input OData:**

L'impostazione "external": "true" informa il servizio di Data Factory hello hello set di dati è esterna toohello data factory e non viene generato da un'attività nella data factory di hello.

```json
{
    "name": "ODataDataset",
    "properties":
    {
        "type": "ODataResource",
        "typeProperties":
        {
                "path": "Products"
        },
        "linkedServiceName": "ODataLinkedService",
        "structure": [],
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3                
        }
    }
}
```

Specifica di **percorso** nel set di dati hello definizione è facoltativa.

**Set di dati di output del BLOB di Azure:**

I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1). percorso della cartella Hello per blob hello viene valutato dinamicamente in base a ora di inizio hello della sezione hello che viene elaborato. percorso della cartella Hello Usa le parti di anno, mese, giorno e ore dell'ora di inizio hello.

```json
{
    "name": "AzureBlobODataDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odata/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


**Attività di copia in una pipeline con un'origine OData e un sink BLOB:**

pipeline Hello contiene un'attività di copia che è configurato toouse hello set di dati di input e output e viene pianificata toorun ogni ora. Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**RelationalSource** e **sink** tipo è stato impostato troppo**BlobSink**. query SQL Hello specificata per hello **query** proprietà consente di selezionare dati (il più recente) più recenti hello dall'origine OData hello.

```json
{
    "name": "CopyODataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "?$select=Name, Description&$top=5",
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "ODataDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobODataDataSet"
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
                "name": "ODataToBlob"
            }
        ],
        "start": "2017-02-01T18:00:00Z",
        "end": "2017-02-03T19:00:00Z"
    }
}
```

Specifica di **query** nella pipeline hello definizione è facoltativa. Hello **URL** è che il servizio di Data Factory hello utilizza dati tooretrieve: l'URL specificato nel hello servizio collegato (obbligatorio) + percorso specificato nel set di dati hello (facoltativo) + eseguire una query nella pipeline di hello (facoltativa).


### <a name="type-mapping-for-odata"></a>Mapping dei tipi per OData
Come accennato in hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, attività di copia esegue le conversioni dai tipi di origine tipi toosink automatico con hello approccio passaggio 2:

1. Conversione dal tipo di origine nativa tipi too.NET
2. Eseguire la conversione da tipo di sink toonative tipo .NET

Quando si spostano dati da archivi dati OData, tipi di dati OData sono tipi too.NET mappato.

## <a name="map-source-toosink-columns"></a>Eseguire il mapping di colonne di origine toosink
toolearn sui mapping delle colonne in toocolumns di set di dati di origine nel sink set di dati, vedere [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Lettura ripetibile da origini relazionali
Quando si copiano dati da archivi dati relazionali, tenere ripetibilità presente tooavoid risultati imprevisti. In Azure Data Factory è possibile rieseguire una sezione manualmente. È anche possibile configurare i criteri di ripetizione per un set di dati in modo da rieseguire una sezione in caso di errore. Quando viene eseguito di nuovo una sezione in entrambi i casi, è necessario toomake assicurarsi che hello stessi dati non viene letto alcun altro aspetto come viene eseguita più volte una sezione. Vedere [Lettura ripetibile da origini relazionali](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Ottimizzazione delle prestazioni
Vedere [prestazioni attività di copia di & ottimizzazione Guida](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.
