---
title: Flusso di log di diagnostica di Azure a un hub eventi | Documenti Microsoft
description: Informazioni su come eseguire il flusso di log di diagnostica di Azure a un hub eventi.
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 42bc4845-c564-4568-b72d-0614591ebd80
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/22/2017
ms.author: johnkem
ms.openlocfilehash: bcb9fcb2371217e7082d96ddbba4a095e6d9a00f
ms.sourcegitcommit: a648f9d7a502bfbab4cd89c9e25aa03d1a0c412b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="stream-azure-diagnostic-logs-to-an-event-hub"></a>Log di diagnostica Azure flusso a un hub eventi
**[I log di diagnostica Azure](monitoring-overview-of-diagnostic-logs.md)**  può essere trasmesso quasi in tempo reale per qualsiasi applicazione che utilizza l'opzione "Esportazione per gli hub di eventi" incorporato nel portale o abilitando l'ID di regola di autorizzazione Hub eventi in un'impostazione di diagnostica tramite Azure Cmdlet di PowerShell o Azure CLI.

## <a name="what-you-can-do-with-diagnostics-logs-and-event-hubs"></a>Che cosa si può fare con i log di diagnostica e Hub eventi
Ecco alcuni esempi di come è possibile usare la funzionalità di trasmissione per i log di diagnostica:

* **Flusso log ai sistemi di registrazione e telemetria parti 3rd** : È possibile trasmettere tutti i log di diagnostica a un hub di eventi solo ai dati di log di pipe per uno strumento analitica SIEM o di log di terze parti.
* **Visualizzare lo stato di integrità del servizio mediante la trasmissione di dati sul "percorso critico" a Power BI**: Hub eventi, Stream Analytics e Power BI permettono di trasformare facilmente i dati di diagnostica in informazioni quasi in tempo reale sui servizi di Azure. [Questo articolo della documentazione offre un'utile panoramica della configurazione di Hub eventi, dell'elaborazione di dati con analisi di flusso e dell'uso di Power BI come output](../stream-analytics/stream-analytics-power-bi-dashboard.md). Ecco alcuni suggerimenti per la configurazione dei log di diagnostica:
  
  * Viene creato automaticamente un hub eventi per una categoria di log di diagnostica quando si seleziona l'opzione nel portale o lo si abilita tramite PowerShell. Nello spazio dei nomi del bus di servizio è quindi consigliabile selezionare l'hub eventi il cui nome inizia con **insights-**.
  * Il codice SQL di esempio seguente è una query di esempio di analisi di flusso che è possibile usare per analizzare tutti i dati di log in una tabella di Power BI:

    ```sql
    SELECT
    records.ArrayValue.[Properties you want to track]
    INTO
    [OutputSourceName – the PowerBI source]
    FROM
    [InputSourceName] AS e
    CROSS APPLY GetArrayElements(e.records) AS records
    ```

* **Compilare una piattaforma di registrazione e telemetria personalizzata** : se è disponibile una piattaforma di telemetria personalizzata o si intende crearne una, le caratteristiche di pubblicazione-sottoscrizione altamente scalabili di Hub eventi offrono grande flessibilità per l'inserimento dei log di diagnostica. [Vedere la guida all'uso di Hub eventi in una piattaforma di telemetria su scala globale di Dan Rosanova](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).

## <a name="enable-streaming-of-diagnostic-logs"></a>Abilitare la trasmissione dei log di diagnostica
È possibile abilitare la trasmissione dei log di diagnostica a livello di codice tramite il portale o tramite le [API REST di Monitoraggio di Azure](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings). In entrambi i casi, si crea un'impostazione di diagnostica in cui specificare uno spazio dei nomi dell'hub eventi e le categorie di log e le metriche che si vuole inviare nello spazio dei nomi. Nello spazio dei nomi per ogni categoria di log abilitata viene creato un hub eventi. Una **categoria di log** di diagnostica è un tipo di log che una risorsa può raccogliere.

> [!WARNING]
> Per abilitare la trasmissione dei log di diagnostica da risorse di calcolo, ad esempio le macchine virtuali o Service Fabric, è necessario [seguire una procedura diversa](../event-hubs/event-hubs-streaming-azure-diags-data.md).
> 
> 

Lo spazio dei nomi dell'hub eventi non deve essere nella stessa sottoscrizione della risorsa di emissione dei registri, purché l'utente che configura l'impostazione disponga di accesso RBAC appropriata per entrambe le sottoscrizioni.

## <a name="stream-diagnostic-logs-using-the-portal"></a>Eseguire lo streaming dei log di diagnostica usando il portale
1. Nel portale passare a Monitoraggio di Azure e fare clic su **Impostazioni di diagnostica**

    ![Sezione relativa al monitoraggio di Monitoraggio di Azure](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-blade.png)

2. Facoltativamente filtrare l'elenco in base al tipo di risorsa o al gruppo di risorse, quindi fare clic sulla risorsa per cui si vuole specificare un'impostazione di diagnostica.

3. Se non esiste un'impostazione sulla risorsa selezionata, viene chiesto di creare un'impostazione. Fare clic su "Attiva diagnostica".

   ![Aggiungi impostazione di diagnostica - Nessuna impostazione esistente](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-none.png)

   Se esistono già impostazioni sulla risorsa, verrò visualizzato un elenco di impostazioni già configurate per questa risorsa. Fare clic su "Add diagnostic setting" (Aggiungi impostazione di diagnostica).

   !["Add diagnostic setting" (Aggiungi impostazione di diagnostica) - impostazioni esistenti](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-multiple.png)

3. Assegnare un nome all'impostazione, selezionare la casella per **Streaming in un hub eventi**, quindi selezionare uno spazio dei nomi di Hub eventi.
   
   !["Add diagnostic setting" (Aggiungi impostazione di diagnostica) - impostazioni esistenti](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-configure.png)
    
   Se si trasmettono i log di diagnostica per la prima volta, nello spazio dei nomi selezionato viene creato l'hub eventi. Se esistono già risorse che trasmettono tale categoria di log a questo spazio dei nomi, l'hub eventi vi viene trasmesso. I criteri definiscono le autorizzazioni del meccanismo di trasmissione. Al momento, per trasmettere a un hub eventi sono necessarie autorizzazioni di gestione, invio e ascolto. È possibile creare o modificare i criteri di accesso condiviso per lo spazio dei nomi di Hub eventi nel portale nella scheda Configura relativa allo spazio dei nomi. Per aggiornare una di queste impostazioni di diagnostica, il client deve avere l'autorizzazione ListKey per la regola di autorizzazione di Hub eventi. È anche possibile specificare un nome hub di eventi. Se si specifica un nome di hub eventi, i log vengono indirizzati all'hub eventi anziché a un hub eventi appena creato per ogni categoria di log.

4. Fare clic su **Save**.

Dopo qualche istante, la nuova impostazione viene visualizzata nell'elenco delle impostazioni per questa risorsa e i log di diagnostica sono state trasmesse all'hub eventi come nuovi dati di evento viene generati.

### <a name="via-powershell-cmdlets"></a>Tramite i cmdlet di PowerShell
Per abilitare la trasmissione tramite i [cmdlet di Azure PowerShell](insights-powershell-samples.md), è possibile usare il cmdlet `Set-AzureRmDiagnosticSetting` con i parametri seguenti:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource ID] -ServiceBusRuleId [your Service Bus rule ID] -Enabled $true
```

L'ID regola del bus di servizio è una stringa nel formato seguente: `{Service Bus resource ID}/authorizationrules/{key name}`. Ad esempio, `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`. Attualmente, è possibile selezionare un nome di hub eventi specifico con PowerShell.

### <a name="via-azure-cli"></a>Tramite l'interfaccia della riga di comando di Azure
Per abilitare la trasmissione tramite l'[interfaccia della riga di comando di Azure](insights-cli-samples.md), è possibile usare il comando `insights diagnostic set` come segue:

```azurecli
azure insights diagnostic set --resourceId <resourceID> --serviceBusRuleId <serviceBusRuleID> --enabled true
```

Usare lo stesso formato per l'ID regola del bus di servizio, come illustrato per il cmdlet di PowerShell. Attualmente, è possibile selezionare un nome di hub eventi specifico con l'interfaccia CLI di Azure.

## <a name="how-do-i-consume-the-log-data-from-event-hubs"></a>Come utilizzare i dati di log da Hub eventi
Di seguito è riportato un esempio di dati di output da Hub eventi:

```json
{
    "records": [
        {
            "time": "2016-07-15T18:00:22.6235064Z",
            "workflowId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA",
            "resourceId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA/RUNS/08587330013509921957/ACTIONS/SEND_EMAIL",
            "category": "WorkflowRuntime",
            "level": "Error",
            "operationName": "Microsoft.Logic/workflows/workflowActionCompleted",
            "properties": {
                "$schema": "2016-04-01-preview",
                "startTime": "2016-07-15T17:58:55.048482Z",
                "endTime": "2016-07-15T18:00:22.4109204Z",
                "status": "Failed",
                "code": "BadGateway",
                "resource": {
                    "subscriptionId": "df602c9c-7aa0-407d-a6fb-eb20c8bd1192",
                    "resourceGroupName": "JohnKemTest",
                    "workflowId": "243aac67fe904cf195d4a28297803785",
                    "workflowName": "JohnKemTestLA",
                    "runId": "08587330013509921957",
                    "location": "westus",
                    "actionName": "Send_email"
                },
                "correlation": {
                    "actionTrackingId": "29a9862f-969b-4c70-90c4-dfbdc814e413",
                    "clientTrackingId": "08587330013509921958"
                }
            }
        },
        {
            "time": "2016-07-15T18:01:15.7532989Z",
            "workflowId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA",
            "resourceId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA/RUNS/08587330012106702630/ACTIONS/SEND_EMAIL",
            "category": "WorkflowRuntime",
            "level": "Information",
            "operationName": "Microsoft.Logic/workflows/workflowActionStarted",
            "properties": {
                "$schema": "2016-04-01-preview",
                "startTime": "2016-07-15T18:01:15.5828115Z",
                "status": "Running",
                "resource": {
                    "subscriptionId": "df602c9c-7aa0-407d-a6fb-eb20c8bd1192",
                    "resourceGroupName": "JohnKemTest",
                    "workflowId": "243aac67fe904cf195d4a28297803785",
                    "workflowName": "JohnKemTestLA",
                    "runId": "08587330012106702630",
                    "location": "westus",
                    "actionName": "Send_email"
                },
                "correlation": {
                    "actionTrackingId": "042fb72c-7bd4-439e-89eb-3cf4409d429e",
                    "clientTrackingId": "08587330012106702632"
                }
            }
        }
    ]
}
```

| Nome dell'elemento | DESCRIZIONE |
| --- | --- |
| records |Matrice di tutti gli eventi di log nel payload. |
| time |Ora in cui si è verificato l'evento. |
| category |Categoria di log per l'evento. |
| ResourceId |ID risorsa della risorsa che ha generato l'evento. |
| operationName |Nome dell'operazione. |
| level |facoltativo. Indica il livello dell'evento di log. |
| properties |Proprietà dell'evento. |

Per un elenco di tutti i provider di risorse che supportano la trasmissione a Hub eventi, vedere [questo articolo](monitoring-overview-of-diagnostic-logs.md).

## <a name="stream-data-from-compute-resources"></a>Eseguire lo streaming di dati dalle risorse di calcolo
È anche possibile eseguire lo streaming di log di diagnostica dalle risorse di calcolo usando l'agente di Diagnostica di Microsoft Azure. Per informazioni sulla configurazione, [vedere questo articolo](../event-hubs/event-hubs-streaming-azure-diags-data.md).

## <a name="next-steps"></a>Passaggi successivi
* [Altre informazioni sui log di diagnostica di Azure](monitoring-overview-of-diagnostic-logs.md)
* [Introduzione all'Hub eventi](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

