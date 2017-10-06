---
title: dati aaaMove da Salesforce utilizzando Data Factory | Documenti Microsoft
description: Per ulteriori informazioni vedere toomove dati da Salesforce utilizzando Data Factory di Azure.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: dbe3bfd6-fa6a-491a-9638-3a9a10d396d1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: c1bde2a333f5a3c0a995eb8c13ecf585132888b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-salesforce-by-using-azure-data-factory"></a>Spostare dati da Salesforce usando Azure Data Factory
In questo articolo descrive come è possibile utilizzare l'attività di copia in un Azure factory toocopy dati dall'archivio di dati Salesforce tooany elencato nella colonna Sink hello hello [origini e sink supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabella. In questo articolo si basa su hello [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo, che presenta una panoramica generale di spostamento dei dati con attività di copia e combinazioni di archivio di dati supportati.

Data Factory di Azure attualmente supporta solo lo spostamento dei dati da Salesforce troppo[supportati archivi dati sink](data-factory-data-movement-activities.md#supported-data-stores-and-formats), ma non supporta lo spostamento dei dati da altri tooSalesforce di archivi dati.

## <a name="supported-versions"></a>Versioni supportate
Questo connettore supporta hello seguenti edizioni di Salesforce: edizione illimitato, Professional Edition, Enterprise Edition o Developer Edition. Supporta anche la copia dall'ambiente di produzione, dalla sandbox e dal dominio personalizzato di Salesforce.

## <a name="prerequisites"></a>Prerequisiti
* È necessario abilitare l'autorizzazione API. Vedere [How do I enable API access in Salesforce by permission set?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)
* toocopy dati da archivi dati di Salesforce tooon locali, è necessario disporre almeno Data Management Gateway 2.0 installato nell'ambiente locale.

## <a name="salesforce-request-limits"></a>Limiti delle richieste Salesforce
Salesforce presenta limiti per le richieste API totali e per le richieste API simultanee. Si noti hello seguenti punti:

- Se il numero di hello di richieste simultanee supera il limite di hello, si verifica una limitazione e verranno visualizzati errori casuali.
- Se il numero totale di hello di richieste supera il limite di hello, hello account Salesforce verrà bloccato per 24 ore.

È inoltre possibile ricevere l'errore "REQUEST_LIMIT_EXCEEDED" hello in entrambi gli scenari. Nella sezione hello "API di limiti richiesta" hello [Salesforce Developer limiti](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) articolo per informazioni dettagliate.

## <a name="getting-started"></a>introduttiva
È possibile creare una pipeline con l'attività di copia che sposta i dati da Salesforce usando diversi strumenti/API.

toocreate modo più semplice di Hello una pipeline è hello toouse **Copia guidata**. Vedere [esercitazione: creare una pipeline mediante Copia guidata](data-factory-copy-data-wizard-tutorial.md) per un'esercitazione rapida sulla creazione di una pipeline mediante Creazione guidata di hello copia dati.

È inoltre possibile utilizzare i seguenti strumenti toocreate una pipeline hello: **portale di Azure**, **Visual Studio**, **Azure PowerShell**, **modello di gestione risorse di Azure** , **API .NET**, e **API REST**. Vedere [esercitazione attività Copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) per istruzioni dettagliate toocreate una pipeline con attività di copia. 

Se si utilizza hello o le API, è eseguire hello passaggi toocreate una pipeline che consente di spostare dati da un'origine tooa archiviano dati sink seguenti: 

1. Creare **servizi collegati** toolink dati di input e output archivi tooyour data factory.
2. Creare **set di dati** toorepresent di input e output dell'operazione di copia di dati per hello. 
3. Creare una **pipeline** con un'attività di copia che accetti un set di dati come input e un set di dati come output. 

Quando si utilizza la procedura guidata hello, le definizioni di JSON per queste entità Data Factory (servizi collegati, i set di dati e della pipeline hello) vengono create automaticamente per l'utente. Quando si utilizzano strumenti o le API (ad eccezione delle API .NET), utilizzando il formato JSON hello è definire queste entità Data Factory.  Per un esempio con le definizioni di JSON per le entità Data Factory toocopy utilizzati dati di Salesforce, vedere [esempio JSON: copiare i dati da Salesforce tooAzure Blob](#json-example-copy-data-from-salesforce-to-azure-blob) sezione di questo articolo. 

Hello le sezioni seguenti fornisce dettagli sulle proprietà JSON che vengono utilizzati toodefine Data Factory entità specifiche tooSalesforce: 

## <a name="linked-service-properties"></a>Proprietà del servizio collegato
Hello nella tabella seguente vengono fornite descrizioni per gli elementi JSON sono toohello specifico del servizio collegato di Salesforce.

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| type |proprietà di tipo Hello deve essere impostata su: **Salesforce**. |Sì |
| environmentUrl | Specificare l'istanza di URL di Salesforce hello. <br><br> - Il valore predefinito è "https://login.salesforce.com". <br> -toocopy dati dalla sandbox, specificare "https://test.salesforce.com". <br> -toocopy dati da un dominio personalizzato, specificare, ad esempio, "https://[domain].my.salesforce.com". |No |
| username |Specificare un nome utente per l'account utente di hello. |Sì |
| password |Specificare una password per account utente di hello. |Sì |
| securityToken |Specificare un token di sicurezza per l'account utente di hello. Vedere [ottenere token di sicurezza](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) per istruzioni su come un token di sicurezza tooreset/get. in generale, vedere toolearn sui token di sicurezza [API di protezione e hello](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm). |Sì |

## <a name="dataset-properties"></a>Proprietà dei set di dati
Per un elenco completo delle sezioni e le proprietà disponibili per la definizione di set di dati, vedere hello [creazione dei DataSet](data-factory-create-datasets.md) articolo. Le sezioni come struttura, disponibilità e criteri di un set di dati JSON sono simili per tutti i tipi di set di dati, ad esempio Azure SQL, BLOB di Azure, tabelle di Azure e così via.

Hello **typeProperties** sezione è diverso per ogni tipo di set di dati e fornisce informazioni sulla posizione hello dei dati di hello nell'archivio dati hello. sezione Hello typeProperties per un set di dati di tipo hello **RelationalTable** è hello le proprietà seguenti:

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| tableName |Nome della tabella hello in Salesforce. |No, se è specificata una **query** di **RelationalSource** |

> [!IMPORTANT]
> parte di "__c" Hello del nome dell'API hello è necessaria per qualsiasi oggetto personalizzato.

![Data Factory - connessione Salesforce - nome API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

## <a name="copy-activity-properties"></a>Proprietà dell'attività di copia
Per un elenco completo delle sezioni e le proprietà disponibili per la definizione di attività, vedere hello [creazione di pipeline](data-factory-create-pipelines.md) articolo. Per tutti i tipi di attività sono disponibili proprietà come nome, descrizione, tabelle di input e output e diversi criteri.

sono disponibili nella proprietà Hello hello sezione typeProperties di attività hello hello invece, variano in base a ogni tipo di attività. Per attività di copia, variano a seconda dei tipi di hello di origini e sink.

Nell'attività di copia, se l'origine hello è di tipo hello **RelationalSource** (che include Salesforce), hello le proprietà seguenti sono disponibile nella sezione typeProperties:

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| query |Utilizzare i dati di tooread hello query personalizzata. |Query SQL-92 o query [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm). Ad esempio: `select * from MyTable__c`. |No (se hello **tableName** di hello **set di dati** è specificato) |

> [!IMPORTANT]
> parte di "__c" Hello del nome dell'API hello è necessaria per qualsiasi oggetto personalizzato.

![Data Factory - connessione Salesforce - nome API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)

## <a name="query-tips"></a>Suggerimenti di query
### <a name="retrieving-data-using-where-clause-on-datetime-column"></a>Recupero di dati tramite la clausola where nella colonna DateTime
Specificare quando hello SOQL o SQL query, pagamento attenzione toohello differenza formato DateTime. ad esempio:

* **Esempio SOQL**: `$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`
* **Esempio SQL**:
    * **Tramite Copia guidata toospecify hello query:**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`
    * **Mediante la modifica di query hello toospecify (carattere di escape correttamente):**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`

### <a name="retrieving-data-from-salesforce-report"></a>Recupero di dati dal report di Salesforce
È possibile recuperare i dati dai report di Salesforce specificando una query come `{call "<report name>"}`, ad esempio. `"query": "{call \"TestReport\"}"`.

### <a name="retrieving-deleted-records-from-salesforce-recycle-bin"></a>Recupero dei record eliminati dal Cestino di Salesforce
record di tooquery hello soft eliminato dal Cestino di Salesforce, è possibile specificare **"IsDeleted = 1"** nella query. Ad esempio,

* specificare tooquery solo i record eliminato hello, "selezionare * da MyTable__c **dove IsDeleted = 1**"
* tooquery tutti hello record inclusi hello esistente e hello eliminato, specificare "Seleziona * da MyTable__c **dove IsDeleted = 0 o IsDeleted = 1**"

## <a name="json-example-copy-data-from-salesforce-tooazure-blob"></a>Esempio JSON: copiare i dati da Salesforce tooAzure Blob
esempio Hello fornisce definizioni di JSON di esempio che è possibile utilizzare una pipeline toocreate utilizzando hello [portale di Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Vengono visualizzate come dati toocopy da Salesforce tooAzure nell'archiviazione Blob. Tuttavia, i dati possono essere copiati tooany di sink hello indicato [qui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizzando hello attività di copia in Azure Data Factory.   

Di seguito sono gli elementi Data Factory di hello che è necessario uno scenario di hello tooimplement toocreate. Hello che seguono l'elenco di hello che forniscono informazioni dettagliate su questi passaggi.

* Un servizio collegato di tipo hello [Salesforce](#linked-service-properties)
* Un servizio collegato di tipo hello [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
* Un input [dataset](data-factory-create-datasets.md) di tipo hello [RelationalTable](#dataset-properties)
* Un output [dataset](data-factory-create-datasets.md) di tipo hello [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)
* Una [pipeline](data-factory-create-pipelines.md) con attività di copia che usa [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)

**Servizio collegato Salesforce**

Questo esempio viene utilizzato hello **Salesforce** servizio collegato. Vedere hello [servizio collegato di Salesforce](#linked-service-properties) sezione per le proprietà di hello supportati da questo servizio collegato.  Vedere [ottenere token di sicurezza](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) per istruzioni su come tooreset/get hello token di sicurezza.

```json
{
    "name": "SalesforceLinkedService",
    "properties":
    {
        "type": "Salesforce",
        "typeProperties":
        {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```
**Servizio collegato Archiviazione di Azure**

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
**Set di dati di input Salesforce**

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"  
        },
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

Impostazione **esterno** troppo**true** informa il servizio di Data Factory hello hello set di dati è esterna toohello data factory e non viene generato da un'attività nella data factory di hello.

> [!IMPORTANT]
> parte di "__c" Hello del nome dell'API hello è necessaria per qualsiasi oggetto personalizzato.

![Data Factory - connessione Salesforce - nome API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

**Set di dati di output del BLOB di Azure**

I dati vengono scritti tooa nuovo blob ogni ora (frequenza: ora, intervallo: 1).

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/alltypes_c"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Pipeline con attività di copia**

pipeline Hello contiene le attività di copia, che viene configurato toouse hello set di dati di input e output, senza che sia pianificato toorun ogni ora. Nella pipeline hello definizione JSON, hello **origine** tipo è stato impostato troppo**RelationalSource**, hello e **sink** tipo è stato impostato troppo**BlobSink**.

Vedere [le proprietà del tipo RelationalSource](#copy-activity-properties) per elenco hello delle proprietà supportate da hello RelationalSource.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce tooan Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "SalesforceInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"                
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
> [!IMPORTANT]
> parte di "__c" Hello del nome dell'API hello è necessaria per qualsiasi oggetto personalizzato.

![Data Factory - connessione Salesforce - nome API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)


### <a name="type-mapping-for-salesforce"></a>Mapping dei tipi per Salesforce
| Tipo Salesforce | Tipo basato su .NET |
| --- | --- |
| Numero automatico |String |
| Casella di controllo |Boolean |
| Valuta |Double |
| Data |DateTime |
| Data/ora |DateTime |
| Email |String |
| ID |String |
| Relazione di ricerca |String |
| Elenco a discesa seleziona multipla |String |
| Number |Double |
| Percentuale |Double |
| Telefono |String |
| Elenco a discesa |String |
| Text |String |
| Area di testo |String |
| Area di testo (Long) |String |
| Area di testo (Rich) |String |
| Testo (Crittografato) |String |
| URL |String |

> [!NOTE]
> colonne toomap toocolumns set di dati di origine dal sink set di dati, vedere [mapping tra colonne del set di dati in Azure Data Factory](data-factory-map-columns.md).

[!INCLUDE [data-factory-structure-for-rectangualr-datasets](../../includes/data-factory-structure-for-rectangualr-datasets.md)]

## <a name="performance-and-tuning"></a>Prestazioni e ottimizzazione
Vedere hello [ottimizzazione Guida e alle prestazioni di attività di copia](data-factory-copy-activity-performance.md) toolearn sulla chiave di fattori che influiscono sulle prestazioni di spostamento dei dati (attività di copia) in Azure Data Factory e i vari modi toooptimize è.
