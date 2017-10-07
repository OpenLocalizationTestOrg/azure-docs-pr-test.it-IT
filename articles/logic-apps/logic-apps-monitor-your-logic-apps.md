---
title: stato aaaCheck, impostare la registrazione e ottenere avvisi - App Azure per la logica | Documenti Microsoft
description: Monitorare lo stato e le prestazioni per le app per la logica, registrare i dati di diagnostica e configurare gli avvisi
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 5c1b1e15-3b6c-49dc-98a6-bdbe7cb75339
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/21/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 81f186e11a669b710f4c06089597eb5a76f7a44e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-status-set-up-diagnostics-logging-and-turn-on-alerts-for-azure-logic-apps"></a>Monitorare lo stato, configurare la registrazione diagnostica e attivare gli avvisi per App per la logica di Azure

Dopo avere [creato ed eseguito un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md), è possibile controllarne la cronologia delle esecuzioni, la cronologia dei trigger, lo stato e le prestazioni. Per il monitoraggio degli eventi in tempo reale e il debug avanzato, configurare la [registrazione diagnostica](#azure-diagnostics) per l'app per la logica. In questo modo è possibile [trovare e visualizzare gli eventi](#find-events), ad esempio eventi di attivazione, eventi di esecuzione ed eventi di azione. È anche possibile usare questi [dati diagnostici con altri servizi](#extend-diagnostic-data), ad esempio Archiviazione di Azure e Hub eventi di Azure. 

Impostare notifiche tooget sugli errori o altri problemi possibili, [avvisi](#add-azure-alerts). È ad esempio possibile creare un avviso che rileva "quando più di cinque esecuzioni in un'ora hanno esito negativo". È anche possibile configurare il monitoraggio, la verifica e la registrazione a livello di codice usando [impostazioni e proprietà degli eventi di Diagnostica di Azure](#diagnostic-event-properties).

## <a name="view-runs-and-trigger-history-for-your-logic-app"></a>Visualizzare la cronologia di esecuzioni e trigger per l'app per la logica

1. toofind app logica in hello [portale di Azure](https://portal.azure.com), in hello menu principale di Azure, scegliere **più servizi**. Nella casella di ricerca hello, cercare "logica app" e scegliere **logica app**.

   ![Trovare l'app per la logica](./media/logic-apps-monitor-your-logic-apps/find-your-logic-app.png)

   portale di Azure Hello Visualizza tutte le applicazioni di logica di hello associati alla sottoscrizione di Azure. 

2. Selezionare l'app per la logica, quindi scegliere **Panoramica**.

   cronologia di esecuzione hello e trigger per l'applicazione della logica di seguito viene Hello portale di Azure. ad esempio:

   ![Cronologia delle esecuzioni e cronologia dei trigger delle app per la logica](media/logic-apps-monitor-your-logic-apps/overview.png)

   * **Cronologia di esecuzione** Mostra tutte le esecuzioni di hello per le app per la logica. 
   * **Attivare cronologia** Mostra tutte le attività hello trigger per l'app logica.

   Per le descrizioni degli stati, vedere [Risolvere i problemi relativi all'app per la logica](../logic-apps/logic-apps-diagnosing-failures.md).

   > [!TIP]
   > Se non si trova dati hello previsti, sulla barra degli strumenti hello, scegliere **aggiornamento**.

3. hello tooview i passaggi da un'esecuzione specifica, in **esegue cronologia**, selezionare che eseguono. 

   visualizzazione di monitoraggio Hello Mostra ogni passaggio eseguito. ad esempio:

   ![Azioni per una specifica esecuzione](media/logic-apps-monitor-your-logic-apps/monitor-view-updated.png)

4. Scegliere ulteriori dettagli sull'esecuzione, hello tooget **Dettagli esecuzione**. Queste informazioni vengono riepilogati i passaggi di hello, lo stato, gli input e output per hello eseguire. 

   ![Scegliere "Dettagli esecuzione"](media/logic-apps-monitor-your-logic-apps/run-details.png)

   Ad esempio, è possibile ottenere hello dell'esecuzione **ID di correlazione**, che potrebbe essere necessario quando si utilizza hello [API REST per la logica app](https://docs.microsoft.com/rest/api/logic).

5. i dettagli di tooget su un passaggio specifico, scegliere il passaggio. È ora possibile esaminare dettagli come input, output ed eventuali errori verificatisi per tale passaggio, ad esempio:

   ![Dettagli del passaggio](media/logic-apps-monitor-your-logic-apps/monitor-view-details.png)
   
   > [!NOTE]
   > Tutti i dettagli di runtime e gli eventi vengono crittografati nel servizio App per la logica di hello. Vengono decrittografate solo quando un utente richiede tooview tali dati. È inoltre possibile controllare gli eventi di accesso toothese con [gestire accesso controllo (RBAC)](../active-directory/role-based-access-control-what-is.md).

6. dettagli di tooget su un evento trigger specifico, tornare indietro toohello **Panoramica** riquadro. In **attivare cronologia**selezionare evento trigger hello. È ora possibile esaminare dettagli come input e output, ad esempio:

   ![Dettagli dell'output dell'evento di attivazione](media/logic-apps-monitor-your-logic-apps/trigger-details.png)

<a name="azure-diagnostics"></a>

## <a name="turn-on-diagnostics-logging-for-your-logic-app"></a>Attivare la registrazione diagnostica per l'app per la logica

Per il debug avanzato con dettagli ed eventi di runtime, è possibile configurare la registrazione diagnostica con [Azure Log Analytics](../log-analytics/log-analytics-overview.md). Log Analitica è un servizio in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) monitoraggio del cloud e si mantengono la disponibilità e prestazioni toohelp di ambienti locali. 

Prima di iniziare, è necessario toohave un'area di lavoro OMS. Informazioni su [come un'area di lavoro OMS toocreate](../log-analytics/log-analytics-get-started.md).

1. In hello [portale di Azure](https://portal.azure.com), individuare e selezionare l'app logica. 

2. Nel menu Pannello app logica hello in **monitoraggio**, scegliere **diagnostica** > **le impostazioni di diagnostica**.

   ![Passare le impostazioni di diagnostica tooMonitoring, diagnostica,](media/logic-apps-monitor-your-logic-apps/logic-app-diagnostics.png)

3. In **Impostazioni di diagnostica** scegliere **Sì**.

   ![Attivare i log di diagnostica](media/logic-apps-monitor-your-logic-apps/turn-on-diagnostics-logic-app.png)

4. A questo punto selezionare categoria hello OMS area di lavoro e l'evento per la registrazione come illustrato:

   1. Selezionare **inviare tooLog Analitica**. 
   2. In **Log Analytics** scegliere **Configura**. 
   3. In **aree di lavoro OMS**, selezionare hello OMS workspace toouse per la registrazione.
   4. In **Log**selezionare hello **WorkflowRuntime** categoria.
   5. Scegliere l'intervallo metrica "hello".
   6. Al termine dell'operazione, scegliere **Salva**.

   ![Selezionare l'area di lavoro di OMS e i dati per la registrazione](media/logic-apps-monitor-your-logic-apps/send-diagnostics-data-log-analytics-workspace.png)

È ora possibile trovare eventi e altri dati per eventi di attivazione, eventi di esecuzione ed eventi di azione.

<a name="find-events"></a>

## <a name="find-events-and-data-for-your-logic-app"></a>Trovare eventi e dati per l'app per la logica

toofind e visualizzare gli eventi nell'app logica, ad esempio gli eventi trigger, Esegui gli eventi e azione, seguono questi passaggi.

1. In hello [portale di Azure](https://portal.azure.com), scegliere **più servizi**. Cercare "Log Analytics", quindi scegliere **Log Analytics**, come illustrato qui:

   ![Scegliere "Log Analytics"](media/logic-apps-monitor-your-logic-apps/browseloganalytics.png)

2. In **Log Analytics** trovare e selezionare l'area di lavoro di OMS. 

   ![Selezionare l'area di lavoro di OMS](media/logic-apps-monitor-your-logic-apps/selectla.png)

3. In **Gestione** scegliere **Portale di OMS**.

   ![Scegliere "Portale di OMS"](media/logic-apps-monitor-your-logic-apps/omsportalpage.png)

4. Nella home page di OMS scegliere **Ricerca log**.

   ![Nella home page di OMS scegliere "Ricerca log"](media/logic-apps-monitor-your-logic-apps/logsearch.png)

   -oppure-

   ![Scegliere "Ricerca di Log" hello OMS menu](media/logic-apps-monitor-your-logic-apps/logsearch-2.png)

5. Nella casella di ricerca hello, specificare un campo che si desidera toofind e premere **invio**. Quando si inizia a digitare, OMS mostra le corrispondenze e operazioni che è possibile usare. 

   Ad esempio, toofind hello primi 10 eventi che si sono verificati, immettere e selezionare la query di ricerca: **categoria = WorkflowRuntime | top 10**

   ![Immettere la stringa di ricerca](media/logic-apps-monitor-your-logic-apps/oms-start-query.png)

   Altre informazioni, vedere [come toofind dati nel Log Analitica](../log-analytics/log-analytics-log-searches.md).

6. Nella pagina di risultati hello, nella barra sinistra hello scegliere hello intervallo di tempo che si desidera tooview.
Scegliere la query aggiungendo un filtro, toorefine **+ Aggiungi**.

   ![Scegliere l'intervallo di tempo per i risultati della query](media/logic-apps-monitor-your-logic-apps/query-results.png)

7. In **aggiungere filtri**, immettere il nome di filtro di hello, pertanto è possibile trovare il filtro di hello desiderato. Selezionare il filtro hello e scegliere **+ Aggiungi**.

   In questo esempio utilizza hello toofind di word "status" non è stato possibile eventi sotto **AzureDiagnostics**.
   Di seguito hello filtro per **status_s** è già selezionato.

   ![Selezionare il filtro](media/logic-apps-monitor-your-logic-apps/log-search-add-filter.png)

8. Nella barra sinistra hello, selezionare il valore del filtro hello che desidera toouse e scegliere **applica**.

   ![Selezionare il valore del filtro, scegliere "Applica"](media/logic-apps-monitor-your-logic-apps/log-search-apply-filter.png)

9. Ora restituiscono toohello query che si sta creando. La query viene aggiornata con il filtro e il valore selezionati. Vengono ora filtrati anche i risultati precedenti.

   ![Restituire tooyour query con risultati filtrati](media/logic-apps-monitor-your-logic-apps/log-search-query-filtered-results.png)

10. Scegliere la query per un utilizzo futuro, toosave **salvare**. Informazioni su [come toosave query](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).

<a name="extend-diagnostic-data"></a>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a>Estendere l'uso dei dati di diagnostica con altri servizi

Con Azure Log Analytics, è possibile usare in modo diverso i dati di diagnostica dell'app per la logica con altri servizi di Azure, ad esempio: 

* [Archiviare i log di diagnostica di Azure in Archiviazione di Microsoft Azure](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [I log di diagnostica Azure tooAzure hub eventi del flusso](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

È quindi possibile eseguire il monitoraggio in tempo reale usando i dati di telemetria e l'analisi da altri servizi, ad esempio [Analisi di flusso di Azure](../stream-analytics/stream-analytics-introduction.md) e [Power BI](../log-analytics/log-analytics-powerbi.md), ad esempio:

* [Dati di flusso da hub eventi tooStream Analitica](../stream-analytics/stream-analytics-define-inputs.md)
* [Analizzare i dati di streaming con Analisi di flusso e creare un dashboard di analisi in tempo reale in Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md)

In base alle opzioni di hello che si desidera configurare, assicurarsi che è primo [creare un account di archiviazione di Azure](../storage/common/storage-create-storage-account.md) o [creare un hub eventi Azure](../event-hubs/event-hubs-create.md). Selezionare quindi le opzioni di hello per cui si desidera toosend dati di diagnostica:

![Inviare dati tooAzure storage account o l'evento hub](./media/logic-apps-monitor-your-logic-apps/storage-account-event-hubs.png)

> [!NOTE]
> Periodi di memorizzazione si applicano solo quando si sceglie toouse un account di archiviazione.

<a name="add-azure-alerts"></a>

## <a name="set-up-alerts-for-your-logic-app"></a>Configurare gli avvisi per l'app per la logica

metriche specifiche toomonitor oppure ha superato le soglie per la logica app, configurare [gli avvisi in Azure](../monitoring-and-diagnostics/monitoring-overview-alerts.md). Informazioni sulle [metriche in Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md). 

tooset di avvisi senza [Azure Log Analitica](../log-analytics/log-analytics-overview.md), seguire questi passaggi. Per azioni e criteri di avviso più avanzati, [configurare anche Log Analytics](#azure-diagnostics).

1. Nel menu Pannello app logica hello in **monitoraggio**, scegliere **diagnostica** > **regole di avviso** > **Aggiungi avviso**come illustrato di seguito:

   ![Aggiungere un avviso per l'app per la logica](media/logic-apps-monitor-your-logic-apps/set-up-alerts.png)

2. In hello **aggiungere una regola di avviso** pannello, creare l'avviso, come illustrato:

   1. In **Risorsa** selezionare l'app per la logica, se non è già selezionata. 
   2. Specificare un nome e una descrizione per l'avviso.
   3. Selezionare un **metrica** o eventi che si desidera tootrack.
   4. Selezionare un **condizione**, specificare un **soglia** per metrica hello e seleziona hello **periodo** per il monitoraggio di questa metrica.
   5. Selezionare se toosend di posta elettronica per l'avviso hello. 
   6. Specificare altri indirizzi di posta elettronica per l'invio avviso hello. 
   È inoltre possibile specificare un URL del webhook in cui si desidera che toosend hello avviso.

   Questa regola, ad esempio, invia un avviso quando cinque o più esecuzioni in un'ora hanno esito negativo:

   ![Creare una regola di avviso per la metrica](media/logic-apps-monitor-your-logic-apps/create-alert-rule.png)

> [!TIP]
> un'app di logica toorun da un avviso, è possibile includere hello [trigger richiesta](../connectors/connectors-native-reqres.md) nel flusso di lavoro, che consente di eseguire attività come questi esempi:
> 
> * [Post tooSlack](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)
> * [Inviare un testo](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)
> * [Aggiungere una coda di messaggi tooa](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)

<a name="diagnostic-event-properties"></a>

## <a name="azure-diagnostics-event-settings-and-details"></a>Impostazioni e dettagli degli eventi di Diagnostica di Azure

Ogni evento di diagnostica con i dettagli sull'applicazione logica e che l'evento, ad esempio, lo stato di hello, ora di inizio, ora di fine e così via. tooprogrammatically impostare il monitoraggio, il rilevamento e la registrazione, unità organizzativa può utilizzare questi dettagli con hello [API REST per le app di Azure logica](https://docs.microsoft.com/rest/api/logic) hello e [API REST per la diagnostica di Azure](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).

Ad esempio, hello `ActionCompleted` evento ha hello `clientTrackingId` e `trackedProperties` proprietà che è possibile utilizzare per il rilevamento e monitoraggio:

``` json
{
    "time": "2016-07-09T17:09:54.4773148Z",
    "workflowId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP",
    "resourceId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP/RUNS/08587361146922712057/ACTIONS/HTTP",
    "category": "WorkflowRuntime",
    "level": "Information",
    "operationName": "Microsoft.Logic/workflows/workflowActionCompleted",
    "properties": {
        "$schema": "2016-06-01",
        "startTime": "2016-07-09T17:09:53.4336305Z",
        "endTime": "2016-07-09T17:09:53.5430281Z",
        "status": "Succeeded",
        "code": "OK",
        "resource": {
            "subscriptionId": "<subscription-ID>",
            "resourceGroupName": "MyResourceGroup",
            "workflowId": "cff00d5458f944d5a766f2f9ad142553",
            "workflowName": "MyLogicApp",
            "runId": "08587361146922712057",
            "location": "westus",
            "actionName": "Http"
        },
        "correlation": {
            "actionTrackingId": "e1931543-906d-4d1d-baed-dee72ddf1047",
            "clientTrackingId": "<my-custom-tracking-ID>"
        },
        "trackedProperties": {
            "myTrackedProperty": "<value>"
        }
    }
}
```

* `clientTrackingId`: Se non è fornito, Azure automaticamente questo ID viene generato e mette in correlazione gli eventi in un'app di logica di esecuzione, incluse eventuali flussi di lavoro annidati che vengono chiamati da hello logica app. È possibile specificare manualmente l'ID di un trigger, passando un `x-ms-client-tracking-id` intestazione con il valore di ID personalizzato nella richiesta di attivazione hello. È possibile usare un trigger di richiesta, un trigger HTTP o un trigger webhook.

* `trackedProperties`: tootrack input o output nei dati di diagnostica, è possibile aggiungere le proprietà rilevate tooactions nella definizione JSON logica dell'applicazione. Le proprietà rilevate possono rilevare solo una singola azione input e output, ma è possibile utilizzare hello `correlation` le proprietà di eventi toocorrelate tra azioni in un'esecuzione.

  tootrack una o più proprietà, aggiungere hello `trackedProperties` sezione e hello proprietà desiderate di definizione dell'azione toohello. Ad esempio, si supponga di che voler tootrack dati come un ID"ordine" nei dati di telemetria:

  ``` json
  "myAction": {
    "type": "http",
    "inputs": {
        "uri": "http://uri",
        "headers": {
            "Content-Type": "application/json"
        },
        "body": "@triggerBody()"
    },
    "trackedProperties": {
        "myActionHTTPStatusCode": "@action()['outputs']['statusCode']",
        "myActionHTTPValue": "@action()['outputs']['body']['<content>']",
        "transactionId": "@action()['inputs']['body']['<content>']"
    }
  }
  ```

## <a name="next-steps"></a>Passaggi successivi

* [Creare modelli per la distribuzione delle app per la logica e la gestione dei rilasci](../logic-apps/logic-apps-create-deploy-template.md)
* [Scenari B2B con Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [Monitorare i messaggi B2B](../logic-apps/logic-apps-monitor-b2b-message.md)