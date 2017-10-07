---
title: dati aaaTransform utilizzando lo script U-SQL - Azure | Documenti Microsoft
description: Informazioni su come servizio di calcolo tooprocess o la trasformazione dei dati eseguendo gli script U-SQL in Azure Data Lake Analitica.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e17c1255-62c2-4e2e-bb60-d25274903e80
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: spelluru
ms.openlocfilehash: 51fdb40334d0c131720f65c3a96b4c5045a98b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-by-running-u-sql-scripts-on-azure-data-lake-analytics"></a>Trasformare i dati eseguendo script U-SQL in Azure Data Lake Analytics 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Attività Hive](data-factory-hive-activity.md) 
> * [Attività di Pig](data-factory-pig-activity.md)
> * [Attività MapReduce](data-factory-map-reduce.md)
> * [Attività di Hadoop Streaming](data-factory-hadoop-streaming-activity.md)
> * [Attività Spark](data-factory-spark.md)
> * [Attività di esecuzione batch di Machine Learning](data-factory-azure-ml-batch-execution-activity.md)
> * [Attività della risorsa di aggiornamento di Machine Learning](data-factory-azure-ml-update-resource-activity.md)
> * [Attività stored procedure](data-factory-stored-proc-activity.md)
> * [Attività U-SQL di Data Lake Analytics](data-factory-usql-activity.md)
> * [Attività personalizzata di .NET](data-factory-use-custom-activities.md)

Una pipeline in un'istanza di Data factory di Azure elabora i dati nei servizi di archiviazione collegati usando i servizi di calcolo collegati. Contiene una sequenza di attività in cui ogni attività esegue una specifica operazione di elaborazione. Questo articolo descrive hello **Data Lake Analitica U-SQL attività** che esegue un **U-SQL** script un **Azure Data Lake Analitica** servizio collegato di calcolo. 

> [!NOTE]
> Creare un account di Azure Data Lake Analytics prima di creare una pipeline con un'attività U-SQL di Data Lake Analytics. toolearn su Azure Data Lake Analitica, vedere [Guida introduttiva di Azure Data Lake Analitica](../data-lake-analytics/data-lake-analytics-get-started-portal.md).
> 
> Hello revisione [compilare la prima esercitazione di pipeline](data-factory-build-your-first-pipeline.md) per i passaggi dettagliati toocreate una data factory, collegato a una pipeline, i set di dati e servizi. Usare i frammenti di codice JSON con l'Editor delle Data Factory o le entità di Visual Studio o PowerShell di Azure Data Factory di toocreate.

## <a name="supported-authentication-types"></a>Tipi di autenticazione supportati
L'attività U-SQL supporta i tipi di autenticazione in Data Lake Analytics indicati di seguito:
* Autenticazione di un'entità servizio
* Autenticazione basata su credenziali dell'utente (OAuth) 

È consigliabile usare l'autenticazione basata sull'entità servizio, in particolare per un'esecuzione U-SQL pianificata. Con l'autenticazione basata sulle credenziali dell'utente può verificarsi la scadenza del token. Per informazioni sulla configurazione, vedere hello [servizio proprietà collegate](#azure-data-lake-analytics-linked-service) sezione.

## <a name="azure-data-lake-analytics-linked-service"></a>Servizio collegato di Azure Data Lake Analytics
Si crea un **Azure Data Lake Analitica** collegato servizio toolink una factory di dati di Azure tooan del servizio di calcolo di Azure Data Lake Analitica. attività Data Lake Analitica U-SQL nella pipeline hello Hello fa riferimento a servizio toothis collegato. 

Hello nella tabella seguente vengono fornite descrizioni per hello generica proprietà utilizzate nella definizione JSON hello. È possibile scegliere anche tra l'autenticazione basata sull'entità servizio e l'autenticazione basata sulle credenziali utente.

| Proprietà | Descrizione | Obbligatorio |
| --- | --- | --- |
| **type** |proprietà di tipo Hello deve essere impostata su: **AzureDataLakeAnalytics**. |Sì |
| **accountName** |Nome dell'account di Azure Data Lake Analytics. |Sì |
| **dataLakeAnalyticsUri** |URI di Azure Data Lake Analytics. |No |
| **subscriptionId** |ID sottoscrizione di Azure |No (se non specificato, sottoscrizione di hello viene utilizzata una data factory). |
| **resourceGroupName** |Nome del gruppo di risorse di Azure |No (se non specificato, il gruppo di risorse di hello viene utilizzata una data factory). |

### <a name="service-principal-authentication-recommended"></a>Autenticazione basata su entità servizio (opzione consigliata)
toouse l'autenticazione dell'entità servizio, registrare un'entità di applicazione in Azure Active Directory (Azure AD) e concedere hello accedere all'archivio Lake tooData. Per la procedura dettaglia, vedere [Autenticazione da servizio a servizio](../data-lake-store/data-lake-store-authenticate-using-active-directory.md). Prendere nota dei seguenti valori, che permette di hello hello toodefine servizio collegato:
* ID applicazione
* Chiave applicazione 
* ID tenant

Utilizzare l'autenticazione dell'entità servizio specificando hello le proprietà seguenti:

| Proprietà | Descrizione | Obbligatorio |
|:--- |:--- |:--- |
| **servicePrincipalId** | Specificare un ID client. dell'applicazione hello | Sì |
| **servicePrincipalKey** | Specificare la chiave dell'applicazione hello. | Sì |
| **tenant** | Specificare le informazioni di hello tenant (dominio tenant o nome ID) in cui risiede l'applicazione. È possibile recuperarlo dal passaggio del mouse hello nell'angolo superiore destro di hello di hello portale di Azure. | Sì |

**Esempio: autenticazione basata su entità servizio**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

### <a name="user-credential-authentication"></a>Autenticazione basata su credenziali utente
In alternativa, è possibile utilizzare l'autenticazione delle credenziali utente per Data Lake Analitica specificando hello le proprietà seguenti:

| Proprietà | Descrizione | Obbligatorio |
|:--- |:--- |:--- |
| **authorization** | Fare clic su hello **Authorize** pulsante hello Editor delle Data Factory e immettere le credenziali dell'utente che assegna la proprietà toothis hello generato automaticamente autorizzazione URL. | Sì |
| **sessionId** | ID di sessione OAuth della sessione di autorizzazione OAuth hello. Ogni ID di sessione è univoco e può essere usato solo una volta. Questa impostazione viene generata automaticamente quando si utilizza hello Editor delle Data Factory. | Sì |

**Esempio: autenticazione basata su credenziali utente**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>", 
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

#### <a name="token-expiration"></a>Scadenza del token
codice di autorizzazione è stato generato utilizzando hello Hello **Authorize** pulsante scade dopo qualche minuto. Vedere hello nella tabella seguente per date di scadenza hello per diversi tipi di account utente. Si può vedere hello seguente messaggio di errore hello quando l'autenticazione **scadenza del token**: errore nell'operazione di credenziali: invalid_grant - AADSTS70002: errore di convalida delle credenziali. AADSTS70008: hello fornito concessione di accesso è scaduto o revocato. ID traccia: d18629e8-af88-43c5-88e3-d8419eb1fca1 ID correlazione: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21:09:31Z.

| Tipo di utente | Scade dopo |
|:--- |:--- |
| Account utente NON gestiti da Azure Active Directory (@hotmail.com, @live.com e così via). |12 ore |
| Account utente gestiti da Azure Active Directory (AAD) |eseguire 14 giorni dopo l'ultima sezione di hello. <br/><br/>90 giorni, se viene eseguita una sezione basata sul servizio collegato OAuth almeno una volta ogni 14 giorni. |

tooavoid e risolvere questo errore, riautorizzare utilizzando hello **Authorize** pulsante quando hello **scadenza del token** e ridistribuire il servizio collegato hello. È anche possibile generare valori per le proprietà **sessionId** e **authorization** a livello di codice usando il codice seguente:

```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```

Vedere [AzureDataLakeStoreLinkedService classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), e [AuthorizationSessionGetResponse classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) argomenti per informazioni dettagliate informazioni sulle classi di Data Factory hello usate nel codice hello. Aggiungere un riferimento a: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll per hello WindowsFormsWebAuthenticationDialog classe. 

## <a name="data-lake-analytics-u-sql-activity"></a>Attività U-SQL di Data Lake Analytics
Hello frammento di codice JSON seguente definisce una pipeline con attività Data Lake Analitica U-SQL. definizione di attività Hello è toohello un riferimento del servizio Azure Data Lake Analitica collegato, creato in precedenza.   

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This is a pipeline toocompute events for en-gb locale and date less than 2012/02/19.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00Z",
        "end": "2015-08-08T01:00:00Z",
        "isPaused": false
    }
}
```

Hello nella tabella seguente descrive i nomi e le descrizioni delle proprietà che sono attività toothis specifico. 

| Proprietà | Descrizione | Obbligatorio |
|:--- |:--- |:--- |
| type |proprietà di tipo Hello deve essere impostata troppo**DataLakeAnalyticsU SQL**. |Sì |
| scriptPath |Toofolder percorso che contiene lo script hello U-SQL. Nome del file hello è tra maiuscole e minuscole. |No (se si usa uno script) |
| scriptLinkedService |Servizio collegato che si collega archiviazione hello che contiene una data factory di hello script toohello |No (se si usa uno script) |
| script |Specificare lo script inline anziché scriptPath e scriptLinkedService. Ad esempio: `"script": "CREATE DATABASE test"`. |No (se si usano le proprietà scriptPath e scriptLinkedService) |
| degreeOfParallelism |numero massimo di Hello di nodi utilizzati contemporaneamente processo hello toorun. |No |
| priority |Determina innanzitutto quali processi, tra tutti quelli accodati devono essere toorun selezionato. Hello hello numero inferiore, priorità più alta hello hello. |No |
| parameters |Parametri per hello U-SQL script |No |
| runtimeVersion | Versione di runtime di toouse motore hello U-SQL | No | 
| compilationMode | <p>Modalità di compilazione di U-SQL. Deve essere uno dei valori seguenti:</p> <ul><li>**Semantic:** esegue solo controlli semantici e i controlli di integrità necessari.</li><li>**Full:** eseguire una compilazione completa hello, quali controllo della sintassi, l'ottimizzazione, la generazione di codice, e così via.</li><li>**SingleBox:** eseguire una compilazione completa hello, con tooSingleBox di impostazione di TargetType.</li></ul><p>Se non si specifica un valore per questa proprietà, il server di hello determina la modalità di compilazione ottimale hello. </p>| No | 

Vedere [SearchLogProcessing.txt crea Script per definizione](#sample-u-sql-script) per la definizione di script hello. 

## <a name="sample-input-and-output-datasets"></a>Set di dati di input e output di esempio
### <a name="input-dataset"></a>Set di dati di input
In questo esempio, i dati di input hello si trovano in un archivio Azure Data Lake (SearchLog.tsv file nella cartella Lake/input hello). 

```json
{
    "name": "DataLakeTable",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}    
```

### <a name="output-dataset"></a>Set di dati di output
In questo esempio, i dati di output di hello prodotti da hello script U-SQL vengono archiviati in un archivio Azure Data Lake (cartella Lake/output). 

```json
{
    "name": "EventsByRegionTable",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="sample-data-lake-store-linked-service"></a>Servizio collegato di Data Lake Store di esempio
Di seguito è la definizione hello dell'esempio hello che archivio Azure Data Lake collegato servizio utilizzato dal set di dati di input/output di hello. 

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
        }
    }
}
```

Vedere [spostare tooand dati dall'archivio Azure Data Lake](data-factory-azure-datalake-connector.md) articolo per una descrizione delle proprietà JSON. 

## <a name="sample-u-sql-script"></a>Script U-SQL di esempio

```
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM @in
    USING Extractors.Tsv(nullEscape:"#NULL#");

@rs1 =
    SELECT Start, Region, Duration
    FROM @searchlog
WHERE Region == "en-gb";

@rs1 =
    SELECT Start, Region, Duration
    FROM @rs1
    WHERE Start <= DateTime.Parse("2012/02/19");

OUTPUT @rs1   
    too@out
      USING Outputters.Tsv(quoting:false, dateTimeFormat:null);
```

i valori per Hello  **@in**  e  **@out**  parametri nello script hello U-SQL vengono passati in modo dinamico dal file ADF mediante sezione 'parameters' hello. Vedere la sezione 'parameters' hello definizione pipeline hello.

È possibile specificare anche altre proprietà, ad esempio la priorità e degreeOfParallelism nella definizione di pipeline per i processi di hello eseguiti sul servizio Azure Data Lake Analitica hello.

## <a name="dynamic-parameters"></a>Parametri dinamici
Nella definizione di pipeline di esempio hello, i parametri vengono assegnati con i valori hardcoded. 

```json
"parameters": {
    "in": "/datalake/input/SearchLog.tsv",
    "out": "/datalake/output/Result.tsv"
}
```

È invece possibile toouse dei parametri dinamici. ad esempio: 

```json
"parameters": {
    "in": "$$Text.Format('/datalake/input/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)",
    "out": "$$Text.Format('/datalake/output/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)"
}
```

In questo caso, i file di input sono ancora prelevati dalla cartella /datalake/input hello e vengono generati file di output nella cartella /datalake/output hello. i nomi di file Hello sono dinamici in base a ora di inizio sezione hello.  

