---
title: log di diagnostica per Azure Data Lake Analitica aaaViewing | Documenti Microsoft
description: 'Comprendere come toosetup e accesso diagnostica nei registri dati di Azure analitica Lake '
services: data-lake-analytics
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf5633d4-bc43-444e-90fc-f90fbd0b7935
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 4cd1eb6f585c1ef96c358340232ef85721a972b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-analytics"></a>Accesso ai log di diagnostica per Azure Data Lake Analytics

La registrazione diagnostica consente di itinerari di controllo di accesso ai dati toocollect. Questi registri includono informazioni quali:

* Un elenco di utenti che accede a dati hello.
* Frequenza hello di accesso ai dati.
* La quantità di dati viene archiviato nell'account hello.

## <a name="enable-logging"></a>Abilitazione della registrazione

1. Accesso toohello [portale di Azure](https://portal.azure.com).

2. Aprire l'account Data Lake Analitica e selezionare **log di diagnostica** da hello __monitoraggio__ sezione. Selezionare quindi __Turn on diagnostics__ (Attiva diagnostica).

    ![Attivare la diagnostica toocollect audit e registri di richieste](./media/data-lake-analytics-diagnostic-logs/turn-on-logging.png)

3. Da __le impostazioni di diagnostica__, impostare too__On__ stato hello e selezionare le opzioni di registrazione.

    ![Attivare la diagnostica toocollect audit e registri di richieste](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "abilitare i log di diagnostica")

   * Impostare **stato** troppo**su** tooenable la registrazione di diagnostica.

   * È possibile scegliere i dati hello toostore o il processo in tre modi diversi.

     * Selezionare __archiviare l'account di archiviazione tooa__ toostore registra in un account di archiviazione di Azure. Utilizzare questa opzione se si desidera tooarchive hello dati. Se si seleziona questa opzione, è necessario fornire un log hello toosave dell'account di archiviazione di Azure per.

     * Selezionare **tooan Hub eventi del flusso** toostream log dati tooan Hub di eventi di Azure. Usare questa opzione se si ha una pipeline di elaborazione downstream che analizza in tempo reale i log in ingresso. Se si seleziona questa opzione, è necessario specificare i dettagli di hello per hello desiderato toouse Hub di eventi di Azure.

     * Selezionare __inviare tooLog Analitica__ toosend hello dati toohello servizio Analitica di Log. Utilizzare questa opzione se si desidera toouse Analitica Log toogather e analizzare i log.
   * Specificare se si desidera tooget i log di controllo e/o i log delle richieste.  Un log delle richieste acquisisce tutte le richieste API. Un log di controllo registra tutte le operazioni attivate dalla richiesta dell'API.

   * Per __archiviare l'account di archiviazione tooa__, specificare il numero di hello di dati di hello tooretain giorni.

   * Fare clic su __Salva__.

        > [!NOTE]
        > È necessario selezionare una __archiviare l'account di archiviazione tooa__, __tooan Hub eventi del flusso__ o __inviare tooLog Analitica__ prima di scegliere hello __salvare__pulsante.

Dopo aver attivato le impostazioni di diagnostica, è possibile restituire toohello __log di diagnostica__ pannello tooview hello registri.

## <a name="view-logs"></a>Visualizzare i log

### <a name="use-hello-data-lake-analytics-view"></a>Utilizzare la visualizzazione di dati Lake Analitica hello

1. Da Analitica di Lake i dati dell'account pannello in **monitoraggio**selezionare **i log di diagnostica** e quindi selezionare i registri toodisplay una voce per.

    ![Visualizzare la registrazione diagnostica](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "Visualizzare i log di diagnostica")

2. Hello registri sono organizzati per **i log di controllo** e **log delle richieste**.

    ![Voci del log](./media/data-lake-analytics-diagnostic-logs/diagnostic-log-entries.png)

   * I log delle richieste di acquisire tutte le richieste API inviate su hello account Data Lake Analitica.
   * I log di controllo sono registri toorequest simile, ma forniscono una suddivisione di operazioni di hello molto più dettagliata. Ad esempio, una singola chiamata API di caricamento in un log delle richieste può restituire più operazioni di aggiunta nel log di controllo.

3. Fare clic su hello **scaricare** collegamento per un toodownload voce di log che di log.

### <a name="use-hello-azure-storage-account-that-contains-log-data"></a>Utilizzare account di archiviazione Azure hello che contiene i dati di log

1. Aprire Pannello di account di archiviazione di Azure hello associata a dati Lake Analitica per la registrazione e quindi fare clic su __BLOB__. Hello **servizio Blob** blade sono elencati due contenitori.

    ![Visualizzare la registrazione diagnostica](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "Visualizzare i log di diagnostica")

   * contenitore Hello **insights-log-controllo** contiene i log di controllo hello.
   * contenitore Hello **insights-log-richieste** contiene i log delle richieste hello.
2. All'interno di questi contenitori, hello sono memorizzate in hello seguente struttura:

        resourceId=/
          SUBSCRIPTIONS/
            <<SUBSCRIPTION_ID>>/
              RESOURCEGROUPS/
                <<RESOURCE_GRP_NAME>>/
                  PROVIDERS/
                    MICROSOFT.DATALAKEANALYTICS/
                      ACCOUNTS/
                        <DATA_LAKE_ANALYTICS_NAME>>/
                          y=####/
                            m=##/
                              d=##/
                                h=##/
                                  m=00/
                                    PT1H.json

   > [!NOTE]
   > Hello `##` voci presenti nel percorso hello contengono hello anno, mese, giorno e ora in cui hello log è stato creato. Data Lake Analytics crea un file ogni ora, in modo `m=` contenga sempre un valore di `00`.

    Ad esempio, potrebbe essere log di controllo tooan hello percorso completo:

        https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=04/m=00/PT1H.json

    Analogamente, log delle richieste tooa hello percorso completo può essere:

        https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=14/m=00/PT1H.json

## <a name="log-structure"></a>Struttura di log

Hello registri di controllo e di richiesta sono in formato JSON strutturato.

### <a name="request-logs"></a>Request Logs

Di seguito è una voce di esempio nel registro eventi di richiesta in formato JSON hello. Ogni BLOB ha un oggetto radice denominato **record** che contiene una matrice di oggetti di log.

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_analytics_account_name>",
             "category": "Requests",
             "operationName": "GetAggregatedJobHistory",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {
                 "HttpMethod":"POST",
                 "Path":"/JobAggregatedHistory",
                 "RequestContentLength":122,
                 "ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8",
                 "StartTime":"2016-07-07T21:02:52.472Z",
                 "EndTime":"2016-07-07T21:02:53.456Z"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a>Schema del log delle richieste

| Nome | Tipo | Descrizione |
| --- | --- | --- |
| time |String |timestamp (in UTC) del log hello Hello |
| resourceId |String |Identificatore Hello della risorsa hello che ha richiesto l'operazione Inserisci in |
| category |String |categoria di log Hello. Ad esempio, **Richieste**. |
| operationName |String |Nome dell'operazione di hello che viene registrato. Ad esempio, GetAggregatedJobHistory. |
| resultType |String |stato di Hello dell'operazione di hello, ad esempio 200. |
| callerIpAddress |String |indirizzo IP Hello del client hello hello richiesta |
| correlationId |String |Identificatore Hello del log hello. Questo valore può essere utilizzato toogroup un set di voci di log correlate. |
| identity |Oggetto |identità Hello che ha generato il log di hello |
| properties |JSON |Nella sezione hello successivo (schema di proprietà del Registro di richiesta) per informazioni dettagliate |

#### <a name="request-log-properties-schema"></a>Schema delle proprietà del log di richiesta

| Nome | Tipo | Descrizione |
| --- | --- | --- |
| HttpMethod |String |Hello metodo HTTP utilizzato per l'operazione di hello. Esempio: GET. |
| Path |String |è stata eseguita un'operazione di hello percorso Hello in |
| RequestContentLength |int |lunghezza del contenuto della richiesta HTTP hello Hello |
| ClientRequestId |String |Identificatore Hello che identifica in modo univoco questa richiesta |
| StartTime |String |ora di Hello in quale richiesta di hello hello server ricevuto |
| EndTime |String |ora di Hello in cui hello server inviato una risposta |

### <a name="audit-logs"></a>Log di controllo

Di seguito è una voce di esempio nel log di controllo in formato JSON di hello. Ogni BLOB ha un oggetto radice denominato **record** che contiene una matrice di oggetti di log.

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-28T19:15:16.245Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_ANALYTICS_account_name>",
             "category": "Audit",
             "operationName": "JobSubmitted",
             "identity": "user@somewhere.com",
             "properties": {
                 "JobId":"D74B928F-5194-4E6C-971F-C27026C290E6",
                 "JobName": "New Job",
                 "JobRuntimeName": "default",
                 "SubmitTime": "7/28/2016 7:14:57 PM"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a>Schema del log di controllo

| Nome | Tipo | Descrizione |
| --- | --- | --- |
| time |String |timestamp (in UTC) del log hello Hello |
| resourceId |String |Identificatore Hello della risorsa hello che ha richiesto l'operazione Inserisci in |
| category |String |categoria di log Hello. Ad esempio, **Audit**. |
| operationName |String |Nome dell'operazione di hello che viene registrato. Ad esempio, JobSubmitted. |
| resultType |String |Uno stato secondario per lo stato del processo hello (operationName). |
| resultSignature |String |Dettagli aggiuntivi sullo stato del processo hello (operationName). |
| identity |String |utente Hello che ha richiesto l'operazione di hello. ad esempio susan@contoso.com. |
| properties |JSON |Nella sezione hello successivo (schema di proprietà del Registro di controllo) per informazioni dettagliate |

> [!NOTE]
> **elemento resultType** e **resultSignature** forniscono informazioni sul risultato di hello di un'operazione e contenere solo un valore se un'operazione è stata completata. Ad esempio, contengono un valore solo quando **operationName** contiene un valore **JobStarted** o **JobEnded**.
>
>

#### <a name="audit-log-properties-schema"></a>Schema delle proprietà del log di controllo

| Nome | Tipo | Descrizione |
| --- | --- | --- |
| JobId |String |processo di Hello ID assegnato toohello |
| JobName |String |nome fornito per il processo di hello Hello |
| JobRunTime |String |runtime di Hello utilizzato processo hello tooprocess |
| SubmitTime |String |tempo di Hello (in UTC) che il processo di hello è stato inviato |
| StartTime |String |processo di hello ora Hello avviato dopo l'invio (in UTC) |
| EndTime |String |Hello ora hello processo terminato |
| Parallelismo |String |numero di Hello di unità Data Lake Analitica richieste per il processo durante l'invio |

> [!NOTE]
> **SubmitTime**, **StartTime**, **EndTime** e **Parallelism** forniscono informazioni su un'operazione. Queste voci contengono un valore solo se l'operazione è stata avviata o completata. Ad esempio, **SubmitTime** contiene solo un valore dopo **operationName** ha valore hello **JobSubmitted**.

## <a name="process-hello-log-data"></a>Dati del log hello processo

Azure Data Lake Analitica viene fornito un esempio su come tooprocess e analizzare i dati di log hello. È possibile trovare l'esempio hello in [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).

## <a name="next-steps"></a>Passaggi successivi
* [Panoramica di Azure Data Lake Analytics](data-lake-analytics-overview.md)
