---
title: Copiare dati da/in Salesforce usando Azure Data Factory | Microsoft Docs
description: "Informazioni su come copiare dati da Salesforce in archivi dati di sink supportati o da archivi dati di origine supportati in Salesforce usando un'attività di copia in una pipeline di Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2018
ms.author: jingwang
ms.openlocfilehash: 7cd86922b0445fc81766ca54080e2fd3e64a6c61
ms.sourcegitcommit: c4cc4d76932b059f8c2657081577412e8f405478
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/11/2018
---
# <a name="copy-data-fromto-salesforce-using-azure-data-factory"></a>Copiare dati da/in Salesforce usando Azure Data Factory
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Versione 1 - Disponibilità generale](v1/data-factory-salesforce-connector.md)
> * [Versione 2 - Anteprima](connector-salesforce.md)

Questo articolo illustra come usare l'attività di copia in Azure Data Factory per copiare dati da e in Salesforce. Si basa sull'articolo di [panoramica dell'attività di copia](copy-activity-overview.md) che presenta una panoramica generale sull'attività di copia.

> [!NOTE]
> Questo articolo si applica alla versione 2 del servizio Data Factory, attualmente in versione di anteprima. Se si usa la versione 1 del servizio Data Factory, disponibile a livello generale, vedere le informazioni sul [connettore Salesforce nella versione 1](v1/data-factory-salesforce-connector.md).

## <a name="supported-capabilities"></a>Funzionalità supportate

È possibile copiare dati da Salesforce in qualsiasi archivio dati di sink supportato o da qualsiasi archivio dati di origine supportato in Salesforce. Per un elenco degli archivi dati supportati come origini/sink dall'attività di copia, vedere la tabella relativa agli [archivi dati supportati](copy-activity-overview.md#supported-data-stores-and-formats).

In particolare, il connettore Salesforce supporta:

- Le seguenti edizioni di Salesforce: **Developer Edition, Professional Edition, Enterprise Edition o Unlimited Edition**.
- La copia di dati da/nell'ambiente di **produzione, dalla sandbox e dal dominio personalizzato** di Salesforce.

## <a name="prerequisites"></a>Prerequisiti

* In Salesforce deve essere abilitata l'autorizzazione API. Vedere [How do I enable API access in Salesforce by permission set?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)

## <a name="salesforce-request-limits"></a>Limiti delle richieste Salesforce

Salesforce presenta limiti per le richieste API totali e per le richieste API simultanee. Tenere presente quanto segue:

- Se il numero di richieste simultanee supera il limite, si verifica una limitazione e vengono visualizzati errori casuali.
- Se il numero totale di richieste supera il limite, l'account di Salesforce viene bloccato per 24 ore.

In entrambi gli scenari è anche possibile che venga visualizzato l'errore "REQUEST_LIMIT_EXCEEDED" ("LIMITE_RICHIESTE_SUPERATO"). Per i dettagli, vedere la sezione API Request Limits (Limiti delle richieste API) nell'articolo [Salesforce API Request Limits](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) (Limiti delle richieste API di Salesforce).

## <a name="getting-started"></a>Attività iniziali

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

Le sezioni seguenti riportano informazioni dettagliate sulle proprietà che vengono usate per definire entità di Data Factory specifiche per il connettore Salesforce.

## <a name="linked-service-properties"></a>Proprietà del servizio collegato

Per il servizio collegato di Salesforce sono supportate le proprietà seguenti:

| Proprietà | Descrizione | Obbligatorio |
|:--- |:--- |:--- |
| type |La proprietà type deve essere impostata su **Salesforce**. |Sì |
| environmentUrl | Specificare l'URL dell'istanza di Salesforce. <br> - Il valore predefinito è `"https://login.salesforce.com"`. <br> - Per copiare dati dalla sandbox, specificare `"https://test.salesforce.com"`. <br> - Per copiare dati dal dominio personalizzato, specificare ad esempio `"https://[domain].my.salesforce.com"`. |No |
| nome utente |Specificare un nome utente per l'account utente. |Sì |
| password |Specificare la password per l'account utente.<br/><br/>È possibile scegliere di contrassegnare questo campo come SecureString per archiviarlo in modo sicuro in ADF o archiviare la password in Azure Key Vault e consentire all'attività di copia di eseguire il pull da tale posizione durante l'esecuzione della copia dei dati. Per altre informazioni, vedere [Archiviare le credenziali in Azure Key Vault](store-credentials-in-key-vault.md). |Sì |
| securityToken |Specificare un token di sicurezza per l'account utente. Per istruzioni su come ottenere o reimpostare un token di sicurezza, vedere [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) (Ottenere un token di sicurezza). Per informazioni generali sui token di sicurezza, vedere [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm)(Sicurezza e API).<br/><br/>È possibile scegliere di contrassegnare questo campo come SecureString per archiviarlo in modo sicuro in ADF o archiviare il token di sicurezza in Azure Key Vault e consentire all'attività di copia di eseguire il pull da tale posizione durante l'esecuzione della copia dei dati. Per altre informazioni, vedere [Archiviare le credenziali in Azure Key Vault](store-credentials-in-key-vault.md). |Sì |
| connectVia | Il [runtime di integrazione](concepts-integration-runtime.md) da usare per la connessione all'archivio dati. Se non specificato, viene usato il runtime di integrazione di Azure predefinito. | No per l'origine, Sì per il sink se il servizio collegato all'origine non dispone del runtime di integrazione. |

>[!IMPORTANT]
>Quando si copiano dati **in** Salesforce, non è possibile usare il runtime di integrazione di Azure predefinito per eseguire l'attività di copia. In altri termini, se il servizio collegato all'origine non dispone di un runtime di integrazione specifico, [creare un runtime di integrazione di Azure](create-azure-integration-runtime.md#create-azure-ir) in modo esplicito con una posizione prossima a Salesforce e associarlo al servizio collegato in Salesforce come illustrato nell'esempio seguente.

**Esempio: archiviazione delle credenziali in ADF**

```json
{
    "name": "SalesforceLinkedService",
    "properties": {
        "type": "Salesforce",
        "typeProperties": {
            "username": "<username>",
            "password": {
                "type": "SecureString",
                "value": "<password>"
            },
            "securityToken": {
                "type": "SecureString",
                "value": "<security token>"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

**Esempio: archiviazione delle credenziali in Azure Key Vault**

```json
{
    "name": "SalesforceLinkedService",
    "properties": {
        "type": "Salesforce",
        "typeProperties": {
            "username": "<username>",
            "password": {
                "type": "AzureKeyVaultSecret",
                "secretName": "<secret name of password in AKV>",
                "store":{
                    "referenceName": "<Azure Key Vault linked service>",
                    "type": "LinkedServiceReference"
                }
            },
            "securityToken": {
                "type": "AzureKeyVaultSecret",
                "secretName": "<secret name of security token in AKV>",
                "store":{
                    "referenceName": "<Azure Key Vault linked service>",
                    "type": "LinkedServiceReference"
                }
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-properties"></a>Proprietà dei set di dati

Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione di set di dati, vedere l'articolo sui [set di dati](concepts-datasets-linked-services.md). Questa sezione presenta un elenco delle proprietà supportate dal set di dati Salesforce.

Per copiare dati da/in Salesforce, impostare la proprietà type del set di dati su **SalesforceObject**. Sono supportate le proprietà seguenti:

| Proprietà | Descrizione | Obbligatorio |
|:--- |:--- |:--- |
| type | La proprietà type deve essere impostata su **SalesforceObject**.  | Sì |
| objectApiName | Nome dell'oggetto di Salesforce da cui recuperare i dati. | No per l'origine, Sì per il sink |

> [!IMPORTANT]
> La parte "__c" del nome dell'API è necessaria per qualsiasi oggetto personalizzato.

![Data Factory - connessione Salesforce - nome API](media/copy-data-from-salesforce/data-factory-salesforce-api-name.png)

**Esempio:**

```json
{
    "name": "SalesforceDataset",
    "properties": {
        "type": "SalesforceObject",
        "linkedServiceName": {
            "referenceName": "<Salesforce linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "objectApiName": "MyTable__c"
        }
    }
}
```

>[!NOTE]
>Per quando riguarda la compatibilità con le versioni precedenti, quando si copiano dati da Salesforce, l'uso del set di dati di tipo "RelationalTable" continuerà a funzionare, anche se verrà consigliato di passare all'uso del nuovo tipo "SalesforceObject".

| Proprietà | Descrizione | Obbligatorio |
|:--- |:--- |:--- |
| type | La proprietà type del set di dati deve essere impostata su: **RelationalTable** | Sì |
| tableName | Nome della tabella in Salesforce. | No (se nell'origine dell'attività è specificato "query") |

## <a name="copy-activity-properties"></a>Proprietà dell'attività di copia

Per un elenco completo delle sezioni e delle proprietà disponibili per la definizione delle attività, vedere l'articolo sulle [pipeline](concepts-pipelines-activities.md). Questa sezione presenta un elenco delle proprietà supportate dall'origine e dal sink Salesforce.

### <a name="salesforce-as-source"></a>Salesforce come origine

Per copiare dati da Salesforce, impostare il tipo di origine nell'attività di copia su **SalesforceSource**. Nella sezione **origine** dell'attività di copia sono supportate le proprietà seguenti:

| Proprietà | Descrizione | Obbligatorio |
|:--- |:--- |:--- |
| type | La proprietà type dell'origine dell'attività di copia deve essere impostata su: **SalesforceSource** | Sì |
| query |Usare la query personalizzata per leggere i dati. È possibile usare una query SQL-92 o una query [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm). Ad esempio: `select * from MyTable__c`. | No (se nel set di dati è specificato "tableName") |

> [!IMPORTANT]
> La parte "__c" del nome dell'API è necessaria per qualsiasi oggetto personalizzato.

![Data Factory - connessione Salesforce - nome API](media/copy-data-from-salesforce/data-factory-salesforce-api-name-2.png)

**Esempio:**

```json
"activities":[
    {
        "name": "CopyFromSalesforce",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Salesforce input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "SalesforceSource",
                "query": "SELECT Col_Currency__c, Col_Date__c, Col_Email__c FROM AllDataType__c"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

>[!NOTE]
>Per quando riguarda la compatibilità con le versioni precedenti, quando si copiano dati da Salesforce, l'uso dell'origine della copia di tipo "RelationalSource" continuerà a funzionare, anche se verrà consigliato di passare all'uso del nuovo tipo "SalesforceSource".

### <a name="salesforce-as-sink"></a>Salesforce come sink

Per copiare dati in Salesforce, impostare il tipo di sink nell'attività di copia su **SalesforceSink**. Nella sezione **sink** dell'attività di copia sono supportate le proprietà seguenti:

| Proprietà | Descrizione | Obbligatorio |
|:--- |:--- |:--- |
| type | La proprietà type del sink dell'attività di copia deve essere impostata su: **SalesforceSink** | Sì |
| writebehavior | Comportamento dell'azione di scrittura per l'operazione.<br/>I valori consentiti sono: **Insert** e **Upsert**. | No (il valore predefinito è Insert) |
| externalIdFieldName | Nome del campo ID esterno per l'operazione upsert. Il campo specificato deve essere definito come "External Id Field" (Campo ID esterno) nell'oggetto Salesforce e non può avere i valori NULL nei dati di input corrispondenti. | Sì per "Upsert" |
| writeBatchSize | Conteggio delle righe di dati scritti da Salesforce in ogni batch. | No (il valore predefinito è 5000) |
| ignoreNullValues | Indica se ignorare i valori null dai dati di input durante l'operazione di scrittura.<br/>I valori consentiti sono: **true** e **false**.<br>- **true**: lascia invariati i dati nell'oggetto di destinazione durante l'operazione di upsert/aggiornamento e inserisce il valore predefinito durante l'operazione di inserimento.<br/>- **false**: aggiorna i dati nell'oggetto di destinazione impostandoli su NULL durante l'operazione di upsert/aggiornamento e inserisce il valore NULL durante l'operazione di inserimento. | No (il valore predefinito è false) |

### <a name="example-salesforce-sink-in-copy-activity"></a>Esempio: sink Salesforce nell'attività di copia

```json
"activities":[
    {
        "name": "CopyToSalesforce",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<Salesforce output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "<source type>"
            },
            "sink": {
                "type": "SalesforceSink",
                "writeBehavior": "Upsert",
                "externalIdFieldName": "CustomerId__c",
                "writeBatchSize": 10000,
                "ignoreNullValues": true
            }
        }
    }
]
```

## <a name="query-tips"></a>Suggerimenti di query

### <a name="retrieving-data-from-salesforce-report"></a>Recupero di dati dal report di Salesforce

È possibile recuperare i dati dai report di Salesforce specificando una query come `{call "<report name>"}`. Esempio: `"query": "{call \"TestReport\"}"`.

### <a name="retrieving-deleted-records-from-salesforce-recycle-bin"></a>Recupero dei record eliminati dal Cestino di Salesforce

Per eseguire una query sui record eliminati temporaneamente dal Cestino di Salesforce, è possibile specificare **"IsDeleted = 1"** nella query. Ad esempio,

* Per eseguire una query solo sui record eliminati, specificare MyTable__c **where IsDeleted= 1**"
* Per eseguire query su tutti i record inclusi quelli esistenti ed eliminati, specificare "select * from MyTable__c **where IsDeleted = 0 or IsDeleted = 1**"

### <a name="retrieving-data-using-where-clause-on-datetime-column"></a>Recupero di dati tramite la clausola where nella colonna DateTime

Quando si specifica la query SQL o SOQL, prestare attenzione alla differenza di formato di DateTime. Ad esempio: 

* **Esempio SOQL**: `SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= @{formatDateTime(pipeline().parameters.StartTime,'yyyy-MM-ddTHH:mm:ssZ')} AND LastModifiedDate < @{formatDateTime(pipeline().parameters.EndTime,'yyyy-MM-ddTHH:mm:ssZ')}`
* **Esempio SQL**: `SELECT * FROM Account WHERE LastModifiedDate >= {ts'@{formatDateTime(pipeline().parameters.StartTime,'yyyy-MM-dd HH:mm:ss')}'} AND LastModifiedDate < {ts'@{formatDateTime(pipeline().parameters.EndTime,'yyyy-MM-dd HH:mm:ss')}'}"`

## <a name="data-type-mapping-for-salesforce"></a>Mapping dei tipi di dati per Salesforce

Quando si copiano dati da Salesforce, vengono usati i mapping seguenti tra i tipi di dati di Salesforce e i tipi di dati provvisori di Azure Data Factory. Vedere [Mapping dello schema e del tipo di dati](copy-activity-schema-and-type-mapping.md) per informazioni su come l'attività di copia esegue il mapping dello schema di origine e del tipo di dati al sink.

| Tipo di dati di Salesforce | Tipo di dati provvisori di Data Factory |
|:--- |:--- |
| Numero automatico |Stringa |
| Casella di controllo |Booleano |
| Valuta |A due righe |
| Data |Data/Ora |
| Data/Ora |Data/Ora |
| Immettere l'indirizzo di posta elettronica |Stringa |
| ID |Stringa |
| Relazione di ricerca |Stringa |
| Elenco a discesa seleziona multipla |Stringa |
| Numero |A due righe |
| Percentuale |A due righe |
| Telefono |Stringa |
| Elenco a discesa |Stringa |
| Testo |Stringa |
| Area di testo |Stringa |
| Area di testo (Long) |Stringa |
| Area di testo (Rich) |Stringa |
| Testo (Crittografato) |Stringa |
| URL |Stringa |

## <a name="next-steps"></a>Passaggi successivi
Per un elenco degli archivi dati supportati come origini o sink dall'attività di copia in Azure Data Factory, vedere gli [archivi dati supportati](copy-activity-overview.md#supported-data-stores-and-formats).