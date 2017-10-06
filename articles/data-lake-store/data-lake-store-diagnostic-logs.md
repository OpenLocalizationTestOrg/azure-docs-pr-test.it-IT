---
title: log di diagnostica aaaViewing per archivio Azure Data Lake | Documenti Microsoft
description: 'Comprendere come toosetup e accesso ai log di diagnostica per archivio Azure Data Lake '
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: f6e75eb1-d0ae-47cf-bdb8-06684b7c0a94
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 11fbf7f517f97abdcaf809c1ebeeb51424ab2c1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-store"></a>Accesso ai log di diagnostica per Archivio Data Lake di Azure
Informazioni sulla modalità di raccolta per l'account tooenable registrazione diagnostica per l'account archivio Data Lake e modalità di registrazione tooview hello.

Le organizzazioni possono abilitare la registrazione diagnostica per loro archivio Azure Data Lake account toocollect dati accesso gli itinerari di controllo che fornisce informazioni quali l'elenco di utenti che accedono ai dati hello, frequenza di accesso ai dati hello, la quantità di dati vengono archiviati in hello account e così via.

## <a name="prerequisites"></a>Prerequisiti
* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Account di Archivio Data Lake di Azure**. Seguire le istruzioni di hello in [introduzione archivio Azure Data Lake tramite il portale di Azure hello](data-lake-store-get-started-portal.md).

## <a name="enable-diagnostic-logging-for-your-data-lake-store-account"></a>Abilitare la registrazione diagnostica per l'account di Archivio Data Lake
1. Accedere di nuovo toohello [portale Azure](https://portal.azure.com).
2. Aprire l'account di Data Lake Store e nel pannello corrispondente fare clic su **Impostazioni** e quindi su **Log di diagnostica**.
3. In hello **log di diagnostica** pannello, fare clic su **attivare la diagnostica**.

    ![Abilitare la funzionalità di registrazione diagnostica](./media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "Abilitare i log di diagnostica")

3. In hello **diagnostica** pannello rendere hello dopo la registrazione diagnostica tooconfigure di modifiche.
   
    ![Abilitare la funzionalità di registrazione diagnostica](./media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "Abilitare i log di diagnostica")
   
   * Impostare **stato** troppo**su** tooenable la registrazione di diagnostica.
   * È possibile scegliere i dati o il processo toostore hello in modi diversi.
     
        * L'opzione hello troppo**archiviare l'account di archiviazione tooa** toostore registra tooan account di archiviazione Azure. Utilizzare questa opzione se si desidera tooarchive hello dati che saranno batch elaborato in un secondo momento. Se si seleziona questa opzione è necessario fornire i log di hello toosave per un account di archiviazione di Azure.
        
        * L'opzione hello troppo**hub di eventi di flusso tooan** toostream log dati tooan Hub di eventi di Azure. Probabilmente si utilizzerà questa opzione se si dispone di un'elaborazione a valle pipeline tooanalyze log in entrata in tempo reale. Se si seleziona questa opzione, è necessario specificare i dettagli di hello per hello desiderato toouse Hub di eventi di Azure.

        * L'opzione hello troppo**inviare tooLog Analitica** hello toouse dati di log di Azure Log Analitica servizio tooanalyze hello generato. Se si seleziona questa opzione, è necessario fornire hello i dettagli per area di lavoro di hello Operations Management Suite che si usa hello eseguire analisi dei log.
     
   * Specificare se si desidera tooget i log di controllo e/o i log delle richieste.
   * Specificare il numero di hello di giorni per cui devono essere mantenuti i dati di hello. Conservazione è applicabile solo se si utilizzano dati log tooarchive account di archiviazione di Azure.
   * Fare clic su **Salva**.

Dopo aver attivato le impostazioni di diagnostica, è possibile guardare hello accede hello **i log di diagnostica** scheda.

## <a name="view-diagnostic-logs-for-your-data-lake-store-account"></a>Visualizzare i log di diagnostica dell'account di Archivio Data Lake
Esistono due modi dati del log hello tooview per l'account archivio Data Lake.

* Dall'account archivio Data Lake hello consente di visualizzare le impostazioni
* Dall'account di archiviazione di Azure hello dove vengono archiviati dati hello

### <a name="using-hello-data-lake-store-settings-view"></a>Utilizzo di hello consente di visualizzare le impostazioni di archivio Data Lake
1. Nel pannello **Impostazioni** dell'account Data Lake Store fare clic su **Log di diagnostica**.
   
    ![Visualizzare la registrazione diagnostica](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "Visualizzare i log di diagnostica") 
2. In hello **i log di diagnostica** pannello, dovrebbe essere suddivisi in categorie i registri di hello **i log di controllo** e **log delle richieste**.
   
   * I log delle richieste di acquisire tutte le richieste API inviate su hello account archivio Data Lake.
   * I log di controllo sono registri toorequest simile, ma forniscono una suddivisione di operazioni di hello eseguite su account archivio Data Lake hello molto più dettagliata. Ad esempio, una chiamata all'API singola operazione di caricamento nel log delle richieste potrebbe comportare più operazioni di "Aggiungi" nei log di controllo hello.
3. Fare clic su hello **scaricare** collegamento su ogni voce toodownload hello registri di log.

### <a name="from-hello-azure-storage-account-that-contains-log-data"></a>Da hello account di archiviazione di Azure che contiene i dati di log
1. Aprire Pannello di account di archiviazione di Azure hello associata all'archivio Data Lake per la registrazione e quindi fare clic su BLOB. Hello **servizio Blob** blade sono elencati due contenitori.
   
    ![Visualizzare la registrazione diagnostica](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "Visualizzare i log di diagnostica")
   
   * contenitore Hello **insights-log-controllo** contiene i log di controllo hello.
   * contenitore Hello **insights-log-richieste** contiene i log delle richieste hello.
2. All'interno di questi contenitori, hello sono memorizzate in hello seguente struttura.
   
    ![Visualizzare la registrazione diagnostica](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "Visualizzare i log di diagnostica")
   
    Ad esempio, potrebbe essere log di controllo tooan hello percorso completo`https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`
   
    Allo stesso modo, potrebbe essere log delle richieste tooa hello percorso completo`https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`

## <a name="understand-hello-structure-of-hello-log-data"></a>Conoscere la struttura dei dati di log hello hello
Hello registri di controllo e di richiesta sono in formato JSON. In questa sezione è struttura hello di JSON per la richiesta e i log di controllo.

### <a name="request-logs"></a>Request Logs
Di seguito è una voce di esempio nel registro eventi di richiesta in formato JSON hello. Ogni BLOB ha un oggetto radice denominato **record** che contiene una matrice di oggetti di log.

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Requests",
             "operationName": "GETCustomerIngressEgress",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {"HttpMethod":"GET","Path":"/webhdfs/v1/Samples/Outputs/Drivers.csv","RequestContentLength":0,"ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8","StartTime":"2016-07-07T21:02:52.472Z","EndTime":"2016-07-07T21:02:53.456Z"}
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a>Schema del log delle richieste
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| time |String |timestamp (in UTC) del log hello Hello |
| resourceId |String |Inserisci Hello ID della risorsa hello che ha richiesto l'operazione in |
| category |String |categoria di log Hello. Ad esempio, **Richieste**. |
| operationName |String |Nome dell'operazione di hello che viene registrato. Ad esempio, getfilestatus. |
| resultType |String |stato di Hello dell'operazione di hello, ad esempio 200. |
| callerIpAddress |String |indirizzo IP Hello del client hello hello richiesta |
| correlationId |String |Hello log hello che può essere utilizzato l'id del toogroup insieme un set di voci di log correlate |
| identity |Oggetto |identità Hello che ha generato il log di hello |
| properties |JSON |Vedere di seguito per ulteriori dettagli |

#### <a name="request-log-properties-schema"></a>Schema delle proprietà del log di richiesta
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| HttpMethod |String |Hello metodo HTTP utilizzato per l'operazione di hello. Esempio: GET. |
| Path |String |è stata eseguita un'operazione di hello percorso Hello in |
| RequestContentLength |int |lunghezza del contenuto della richiesta HTTP hello Hello |
| ClientRequestId |String |Hello Id che identifica in modo univoco questa richiesta |
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
             "time": "2016-07-08T19:08:59.359Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Audit",
             "operationName": "SeOpenStream",
             "resultType": "0",
             "correlationId": "381110fc03534e1cb99ec52376ceebdf;Append_BrEKAmg;25.66.9.145",
             "identity": "A9DAFFAF-FFEE-4BB5-A4A0-1B6CBBF24355",
             "properties": {"StreamName":"adl://<data_lake_store_account_name>.azuredatalakestore.net/logs.csv"}
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a>Schema del log di controllo
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| time |String |timestamp (in UTC) del log hello Hello |
| resourceId |String |Inserisci Hello ID della risorsa hello che ha richiesto l'operazione in |
| category |String |categoria di log Hello. Ad esempio, **Audit**. |
| operationName |String |Nome dell'operazione di hello che viene registrato. Ad esempio, getfilestatus. |
| resultType |String |stato di Hello dell'operazione di hello, ad esempio 200. |
| correlationId |String |Hello log hello che può essere utilizzato l'id del toogroup insieme un set di voci di log correlate |
| identity |Oggetto |identità Hello che ha generato il log di hello |
| properties |JSON |Vedere di seguito per ulteriori dettagli |

#### <a name="audit-log-properties-schema"></a>Schema delle proprietà del log di controllo
| Nome | Tipo | Descrizione |
| --- | --- | --- |
| StreamName |String |è stata eseguita un'operazione di hello percorso Hello in |

## <a name="samples-tooprocess-hello-log-data"></a>Dati del log hello tooprocess esempi
Archivio Azure Data Lake viene fornito un esempio su come tooprocess e analizzare i dati di log hello. È possibile trovare l'esempio hello in [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample). 

## <a name="see-also"></a>Vedere anche
* [Panoramica di Archivio Data Lake di Azure](data-lake-store-overview.md)
* [Proteggere i dati in Data Lake Store](data-lake-store-secure-data.md)

