---
title: i log di diagnostica di Azure di aaaStream tooan Namespace hub eventi | Documenti Microsoft
description: "Informazioni su modalità di registrazione dello spazio dei nomi di hub eventi tooan toostream diagnostica Azure."
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
ms.date: 08/21/2017
ms.author: johnkem
ms.openlocfilehash: 00092ea8f3fe4fa1476e3a697bf1e8645dd21e6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="stream-azure-diagnostic-logs-tooan-event-hubs-namespace"></a>I log di diagnostica Azure tooan Namespace hub eventi del flusso
**[I log di diagnostica Azure](monitoring-overview-of-diagnostic-logs.md)**  può essere trasmesso quasi in tempo reale tooany applicazione utilizzando l'hello incorporati "Esportazione tooEvent hub" opzione in hello portale o abilitando hello ID regola Bus di servizio in un'impostazione di diagnostica tramite hello Azure PowerShell I cmdlet o Azure CLI.

## <a name="what-you-can-do-with-diagnostics-logs-and-event-hubs"></a>Che cosa si può fare con i log di diagnostica e Hub eventi
Ecco alcune delle modalità è possibile utilizzare hello lo streaming di funzionalità per i log di diagnostica:

* **Flusso registra sistemi di registrazione e i dati di telemetria di terze parti too3rd** – nel tempo, gli hub di eventi di flusso diventeranno hello meccanismo toopipe i log di diagnostica in parti toothird Siem e soluzioni analitica di log.
* **Integrità del servizio per visualizzare, streaming "percorso critico" dati tooPowerBI** – tramite hub di eventi, flusso Analitica e Power BI, è possibile trasformare facilmente i dati di diagnostica in informazioni in tempo reale toonear in servizi di Azure. [In questo articolo di documentazione fornisce una panoramica del tooset di hub di eventi, elaborano i dati con flusso Analitica e usare Power BI come output](../stream-analytics/stream-analytics-power-bi-dashboard.md). Ecco alcuni suggerimenti per la configurazione dei log di diagnostica:
  
  * Un hub di eventi per una categoria di log di diagnostica viene creato automaticamente quando si archiviano opzione hello nel portale di hello o abilitarla tramite PowerShell, pertanto si hub di eventi tooselect hello hello dello spazio dei nomi con nome hello che inizia con **insights**.
  * Hello codice SQL seguente è riportato un esempio flusso Analitica query che è possibile utilizzare tooparse tutti i dati di log hello nella tabella di Power BI tooa:

    ```sql
    SELECT
    records.ArrayValue.[Properties you want tootrack]
    INTO
    [OutputSourceName – hello PowerBI source]
    FROM
    [InputSourceName] AS e
    CROSS APPLY GetArrayElements(e.records) AS records
    ```

* **Compilare una piattaforma di registrazione e i dati di telemetria personalizzati** : se si dispone già di una piattaforma dati di telemetria personalizzati o sono solo le compilazione uno, hello altamente scalabile di pubblicazione-sottoscrizione natura degli hub di eventi consente tooflexibly inserimento diagnostica log. [Vedere toousing di Guida di Dan Rosanova hub eventi in una piattaforma di dati di telemetria di su scala globale](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).

## <a name="enable-streaming-of-diagnostic-logs"></a>Abilitare la trasmissione dei log di diagnostica
È possibile abilitare il flusso di log di diagnostica a livello di codice, tramite il portale di hello, o tramite hello [API REST di Azure monitoraggio](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings). In entrambi i casi, si crea un'impostazione di diagnostica in cui specificare uno spazio dei nomi dell'hub eventi e categorie log hello e metriche da toosend toohello dello spazio dei nomi. Un hub eventi viene creato nello spazio dei nomi hello per ogni categoria di log che attiva. Una **categoria di log** di diagnostica è un tipo di log che una risorsa può raccogliere.

> [!WARNING]
> Per abilitare la trasmissione dei log di diagnostica da risorse di calcolo, ad esempio le macchine virtuali o Service Fabric, è necessario [seguire una procedura diversa](../event-hubs/event-hubs-streaming-azure-diags-data.md).
> 
> 

Hello Bus di servizio o hub eventi dello spazio dei nomi è disponibile toobe hello stessa sottoscrizione di risorse hello la creazione di log come utente di hello che configura l'impostazione di hello dispone di sottoscrizioni di tooboth accesso RBAC appropriate.

## <a name="stream-diagnostic-logs-using-hello-portal"></a>Log di diagnostica di flusso tramite il portale di hello
1. Nel portale di hello passare tooAzure Monitor e fare clic su **le impostazioni di diagnostica**

    ![Sezione relativa al monitoraggio di Monitoraggio di Azure](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-blade.png)

2. Se lo si desidera filtrare l'elenco hello in base al tipo di risorsa o gruppo di risorse, fare clic sul risorse hello per il quale si desidera tooset un'impostazione di diagnostica.

3. Se nessuna impostazione esistano nella risorsa hello selezionata, verrà richiesta toocreate un'impostazione. Fare clic su "Attiva diagnostica".

   ![Aggiungi impostazione di diagnostica - Nessuna impostazione esistente](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-none.png)

   Se sono presenti le impostazioni esistenti sulla risorsa hello, vedrai un elenco di impostazioni già configurato per questa risorsa. Fare clic su "Add diagnostic setting" (Aggiungi impostazione di diagnostica).

   !["Add diagnostic setting" (Aggiungi impostazione di diagnostica) - impostazioni esistenti](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-multiple.png)

3. Assegnare un nome all'impostazione e casella hello per **hub di eventi di flusso tooan**, quindi selezionare uno spazio dei nomi dell'hub eventi.
   
   !["Add diagnostic setting" (Aggiungi impostazione di diagnostica) - impostazioni esistenti](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-configure.png)
    
   Hello dello spazio dei nomi selezionato sarà in hub eventi hello è creato (se questa è la prima volta che i log di diagnostica di streaming) o inviati nel flusso troppo (se sono già presenti risorse in tale spazio dei nomi di registro categoria toothis streaming), e i criteri di hello definiscono hello dispone di autorizzazioni che hello meccanismo di flusso. Oggi, streaming tooan richiede le autorizzazioni di ascolto, invio e gestione in hub eventi. È possibile creare o modificare i criteri di accesso condiviso di spazio dei nomi di hub eventi nel portale di hello nella scheda Configura hello dello spazio dei nomi. tooupdate una di queste impostazioni di diagnostica, hello client disponga di autorizzazioni ListKey hello nella regola di autorizzazione hello hub eventi.

4. Fare clic su **Salva**.

Dopo alcuni istanti, hello nuova impostazione è visualizzata nell'elenco delle impostazioni per questa risorsa e i log di diagnostica sono state trasmesse toothat account di archiviazione come nuovi dati di evento viene generati.

### <a name="via-powershell-cmdlets"></a>Tramite i cmdlet di PowerShell
streaming tramite hello tooenable [i cmdlet di PowerShell Azure](insights-powershell-samples.md), è possibile utilizzare hello `Set-AzureRmDiagnosticSetting` cmdlet con i seguenti parametri:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource ID] -ServiceBusRuleId [your Service Bus rule ID] -Enabled $true
```

Hello ID regola Bus di servizio è una stringa con questo formato: `{Service Bus resource ID}/authorizationrules/{key name}`, ad esempio, `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`.

### <a name="via-azure-cli"></a>Tramite l'interfaccia della riga di comando di Azure
streaming tramite hello tooenable [CLI di Azure](insights-cli-samples.md), è possibile utilizzare hello `insights diagnostic set` comando simile al seguente:

```azurecli
azure insights diagnostic set --resourceId <resourceID> --serviceBusRuleId <serviceBusRuleID> --enabled true
```

Utilizzare hello stesso formato per ID regola Bus di servizio, come illustrato per hello Cmdlet di PowerShell.

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a>Come utilizzano i dati del log hello dagli hub eventi?
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

| Nome dell'elemento | Description |
| --- | --- |
| records |Matrice di tutti gli eventi di log nel payload. |
| time |Ora di hello evento. |
| category |Categoria di log per l'evento. |
| resourceId |ID risorsa della risorsa hello che ha generato questo evento. |
| operationName |Nome dell'operazione di hello. |
| level |Facoltativo. Indica il livello di evento log hello. |
| properties |Proprietà di evento hello. |

È possibile visualizzare un elenco di tutti i provider di risorse che supportano flussi hub tooEvent [qui](monitoring-overview-of-diagnostic-logs.md).

## <a name="stream-data-from-compute-resources"></a>Eseguire lo streaming di dati dalle risorse di calcolo
È inoltre possibile trasmettere i log di diagnostica dalle risorse di calcolo utilizzando hello agente di diagnostica Windows Azure. [Vedere l'articolo](../event-hubs/event-hubs-streaming-azure-diags-data.md) come tooset tale backup.

## <a name="next-steps"></a>Passaggi successivi
* [Altre informazioni sui log di diagnostica di Azure](monitoring-overview-of-diagnostic-logs.md)
* [Introduzione all'Hub eventi](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

