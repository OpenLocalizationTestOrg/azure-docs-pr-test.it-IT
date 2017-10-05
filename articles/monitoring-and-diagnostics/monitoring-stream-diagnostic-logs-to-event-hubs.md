---
title: Trasmettere log di diagnostica di Azure a uno spazio dei nomi di Hub eventi | Microsoft Docs
description: Informazioni su come trasmettere log di diagnostica di Azure a uno spazio dei nomi di Hub eventi.
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
ms.openlocfilehash: 01ba8ddfcf90e1368ac147296fd180f99420d96f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="stream-azure-diagnostic-logs-to-an-event-hubs-namespace"></a><span data-ttu-id="05360-103">Trasmettere log di diagnostica di Azure a uno spazio dei nomi di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="05360-103">Stream Azure Diagnostic Logs to an Event Hubs Namespace</span></span>
<span data-ttu-id="05360-104">I **[log di diagnostica di Azure](monitoring-overview-of-diagnostic-logs.md)** possono essere trasmessi quasi in tempo reale a qualsiasi applicazione con l'opzione "Esporta in hub eventi" incorporata nel portale oppure abilitando l'ID regola del bus di servizio in un'impostazione di diagnostica tramite i cmdlet di Azure PowerShell o l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="05360-104">**[Azure diagnostic logs](monitoring-overview-of-diagnostic-logs.md)** can be streamed in near real time to any application using the built-in “Export to Event Hubs” option in the Portal, or by enabling the Service Bus Rule ID in a diagnostic setting via the Azure PowerShell Cmdlets or Azure CLI.</span></span>

## <a name="what-you-can-do-with-diagnostics-logs-and-event-hubs"></a><span data-ttu-id="05360-105">Che cosa si può fare con i log di diagnostica e Hub eventi</span><span class="sxs-lookup"><span data-stu-id="05360-105">What you can do with diagnostics logs and Event Hubs</span></span>
<span data-ttu-id="05360-106">Ecco alcuni esempi di come è possibile usare la funzionalità di trasmissione per i log di diagnostica:</span><span class="sxs-lookup"><span data-stu-id="05360-106">Here are just a few ways you might use the streaming capability for Diagnostic Logs:</span></span>

* <span data-ttu-id="05360-107">**Trasmettere log a sistemi di telemetria e registrazione di terze parti**: in futuro, la funzionalità di trasmissione di Hub eventi diventerà il meccanismo di invio dei log di diagnostica a soluzioni di analisi di log e SIEM di terze parti.</span><span class="sxs-lookup"><span data-stu-id="05360-107">**Stream logs to 3rd party logging and telemetry systems** – Over time, Event Hubs streaming will become the mechanism to pipe your diagnostic logs in to third-party SIEMs and log analytics solutions.</span></span>
* <span data-ttu-id="05360-108">**Visualizzare lo stato di integrità del servizio mediante la trasmissione di dati sul "percorso critico" a Power BI**: Hub eventi, Stream Analytics e Power BI permettono di trasformare facilmente i dati di diagnostica in informazioni quasi in tempo reale sui servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="05360-108">**View service health by streaming “hot path” data to PowerBI** – Using Event Hubs, Stream Analytics, and PowerBI, you can easily transform your diagnostics data in to near real-time insights on your Azure services.</span></span> <span data-ttu-id="05360-109">[Questo articolo della documentazione offre un'utile panoramica della configurazione di Hub eventi, dell'elaborazione di dati con analisi di flusso e dell'uso di Power BI come output](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="05360-109">[This documentation article gives a great overview of how to set up Event Hubs, process data with Stream Analytics, and use PowerBI as an output](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span></span> <span data-ttu-id="05360-110">Ecco alcuni suggerimenti per la configurazione dei log di diagnostica:</span><span class="sxs-lookup"><span data-stu-id="05360-110">Here are a few tips for getting set up with diagnostic logs:</span></span>
  
  * <span data-ttu-id="05360-111">Viene creato automaticamente un hub eventi per una categoria di log di diagnostica quando si seleziona l'opzione nel portale o lo si abilita tramite PowerShell. Nello spazio dei nomi del bus di servizio è quindi consigliabile selezionare l'hub eventi il cui nome inizia con **insights-**.</span><span class="sxs-lookup"><span data-stu-id="05360-111">An event hub for a category of diagnostic logs is created automatically when you check the option in the portal or enable it through PowerShell, so you want to select the event hub in the namespace with the name that starts with **insights-**.</span></span>
  * <span data-ttu-id="05360-112">Il codice SQL di esempio seguente è una query di esempio di analisi di flusso che è possibile usare per analizzare tutti i dati di log in una tabella di Power BI:</span><span class="sxs-lookup"><span data-stu-id="05360-112">The following SQL code is a sample Stream Analytics query that you can use to parse all the log data in to a PowerBI table:</span></span>

    ```sql
    SELECT
    records.ArrayValue.[Properties you want to track]
    INTO
    [OutputSourceName – the PowerBI source]
    FROM
    [InputSourceName] AS e
    CROSS APPLY GetArrayElements(e.records) AS records
    ```

* <span data-ttu-id="05360-113">**Compilare una piattaforma di registrazione e telemetria personalizzata** : se è disponibile una piattaforma di telemetria personalizzata o si intende crearne una, le caratteristiche di pubblicazione-sottoscrizione altamente scalabili di Hub eventi offrono grande flessibilità per l'inserimento dei log di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="05360-113">**Build a custom telemetry and logging platform** – If you already have a custom-built telemetry platform or are just thinking about building one, the highly scalable publish-subscribe nature of Event Hubs allows you to flexibly ingest diagnostic logs.</span></span> <span data-ttu-id="05360-114">[Vedere la guida all'uso di Hub eventi in una piattaforma di telemetria su scala globale di Dan Rosanova](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span><span class="sxs-lookup"><span data-stu-id="05360-114">[See Dan Rosanova’s guide to using Event Hubs in a global scale telemetry platform here](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span></span>

## <a name="enable-streaming-of-diagnostic-logs"></a><span data-ttu-id="05360-115">Abilitare la trasmissione dei log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="05360-115">Enable streaming of diagnostic logs</span></span>
<span data-ttu-id="05360-116">È possibile abilitare la trasmissione dei log di diagnostica a livello di codice tramite il portale o tramite le [API REST di Monitoraggio di Azure](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings).</span><span class="sxs-lookup"><span data-stu-id="05360-116">You can enable streaming of diagnostic logs programmatically, via the portal, or using the [Azure Monitor REST APIs](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings).</span></span> <span data-ttu-id="05360-117">In entrambi i casi, si crea un'impostazione di diagnostica in cui specificare uno spazio dei nomi dell'hub eventi e le categorie di log e le metriche che si vuole inviare nello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="05360-117">Either way, you create a diagnostic setting in which you specify an Event Hubs namespace and the log categories and metrics you want to send in to the namespace.</span></span> <span data-ttu-id="05360-118">Nello spazio dei nomi per ogni categoria di log abilitata viene creato un hub eventi.</span><span class="sxs-lookup"><span data-stu-id="05360-118">An event hub is created in the namespace for each log category you enable.</span></span> <span data-ttu-id="05360-119">Una **categoria di log** di diagnostica è un tipo di log che una risorsa può raccogliere.</span><span class="sxs-lookup"><span data-stu-id="05360-119">A diagnostic **log category** is a type of log that a resource may collect.</span></span>

> [!WARNING]
> <span data-ttu-id="05360-120">Per abilitare la trasmissione dei log di diagnostica da risorse di calcolo, ad esempio le macchine virtuali o Service Fabric, è necessario [seguire una procedura diversa](../event-hubs/event-hubs-streaming-azure-diags-data.md).</span><span class="sxs-lookup"><span data-stu-id="05360-120">Enabling and streaming diagnostic logs from Compute resources (for example, VMs or Service Fabric) [requires a different set of steps](../event-hubs/event-hubs-streaming-azure-diags-data.md).</span></span>
> 
> 

<span data-ttu-id="05360-121">Lo spazio dei nomi del bus di servizio o di Hub eventi non deve trovarsi nella stessa sottoscrizione della risorsa che crea i log, purché l'utente che configura l'impostazione disponga dell'accesso RBAC appropriato a entrambe le sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="05360-121">The Service Bus or Event Hubs namespace does not have to be in the same subscription as the resource emitting logs as long as the user who configures the setting has appropriate RBAC access to both subscriptions.</span></span>

## <a name="stream-diagnostic-logs-using-the-portal"></a><span data-ttu-id="05360-122">Eseguire lo streaming dei log di diagnostica usando il portale</span><span class="sxs-lookup"><span data-stu-id="05360-122">Stream diagnostic logs using the portal</span></span>
1. <span data-ttu-id="05360-123">Nel portale passare a Monitoraggio di Azure e fare clic su **Impostazioni di diagnostica**</span><span class="sxs-lookup"><span data-stu-id="05360-123">In the portal, navigate to Azure Monitor and click on **Diagnostic Settings**</span></span>

    ![Sezione relativa al monitoraggio di Monitoraggio di Azure](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-blade.png)

2. <span data-ttu-id="05360-125">Facoltativamente filtrare l'elenco in base al tipo di risorsa o al gruppo di risorse, quindi fare clic sulla risorsa per cui si vuole specificare un'impostazione di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="05360-125">Optionally filter the list by resource group or resource type, then click on the resource for which you would like to set a diagnostic setting.</span></span>

3. <span data-ttu-id="05360-126">Se non esiste un'impostazione sulla risorsa selezionata, viene chiesto di creare un'impostazione.</span><span class="sxs-lookup"><span data-stu-id="05360-126">If no settings exist on the resource you have selected, you are prompted to create a setting.</span></span> <span data-ttu-id="05360-127">Fare clic su "Attiva diagnostica".</span><span class="sxs-lookup"><span data-stu-id="05360-127">Click "Turn on diagnostics."</span></span>

   ![Aggiungi impostazione di diagnostica - Nessuna impostazione esistente](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-none.png)

   <span data-ttu-id="05360-129">Se esistono già impostazioni sulla risorsa, verrò visualizzato un elenco di impostazioni già configurate per questa risorsa.</span><span class="sxs-lookup"><span data-stu-id="05360-129">If there are existing settings on the resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="05360-130">Fare clic su "Add diagnostic setting" (Aggiungi impostazione di diagnostica).</span><span class="sxs-lookup"><span data-stu-id="05360-130">Click "Add diagnostic setting."</span></span>

   !["Add diagnostic setting" (Aggiungi impostazione di diagnostica) - impostazioni esistenti](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="05360-132">Assegnare un nome all'impostazione, selezionare la casella per **Streaming in un hub eventi**, quindi selezionare uno spazio dei nomi di Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="05360-132">Give your setting a name and check the box for **Stream to an event hub**, then select an Event Hubs namespace.</span></span>
   
   !["Add diagnostic setting" (Aggiungi impostazione di diagnostica) - impostazioni esistenti](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-configure.png)
    
   <span data-ttu-id="05360-134">Se si trasmettono i log di diagnostica per la prima volta, nello spazio dei nomi selezionato viene creato l'hub eventi. Se esistono già risorse che trasmettono tale categoria di log a questo spazio dei nomi, l'hub eventi vi viene trasmesso. I criteri definiscono le autorizzazioni del meccanismo di trasmissione.</span><span class="sxs-lookup"><span data-stu-id="05360-134">The namespace selected will be where the event hub is created (if this is your first time streaming diagnostic logs) or streamed to (if there are already resources that are streaming that log category to this namespace), and the policy defines the permissions that the streaming mechanism has.</span></span> <span data-ttu-id="05360-135">Al momento, per trasmettere a un hub eventi sono necessarie autorizzazioni di gestione, invio e ascolto.</span><span class="sxs-lookup"><span data-stu-id="05360-135">Today, streaming to an event hub requires Manage, Send, and Listen permissions.</span></span> <span data-ttu-id="05360-136">È possibile creare o modificare i criteri di accesso condiviso per lo spazio dei nomi di Hub eventi nel portale nella scheda Configura relativa allo spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="05360-136">You can create or modify Event Hubs namespace shared access policies in the portal under the Configure tab for your namespace.</span></span> <span data-ttu-id="05360-137">Per aggiornare una di queste impostazioni di diagnostica, il client deve avere l'autorizzazione ListKey per la regola di autorizzazione di Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="05360-137">To update one of these diagnostic settings, the client must have the ListKey permission on the Event Hubs authorization rule.</span></span>

4. <span data-ttu-id="05360-138">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="05360-138">Click **Save**.</span></span>

<span data-ttu-id="05360-139">Dopo qualche istante, la nuova impostazione viene visualizzata nell'elenco delle impostazioni per questa risorsa e viene eseguito lo streaming dei log di diagnostica in tale account di archiviazione non appena vengono generati nuovi dati di eventi.</span><span class="sxs-lookup"><span data-stu-id="05360-139">After a few moments, the new setting appears in your list of settings for this resource, and diagnostic logs are streamed to that storage account as soon as new event data is generated.</span></span>

### <a name="via-powershell-cmdlets"></a><span data-ttu-id="05360-140">Tramite i cmdlet di PowerShell</span><span class="sxs-lookup"><span data-stu-id="05360-140">Via PowerShell Cmdlets</span></span>
<span data-ttu-id="05360-141">Per abilitare la trasmissione tramite i [cmdlet di Azure PowerShell](insights-powershell-samples.md), è possibile usare il cmdlet `Set-AzureRmDiagnosticSetting` con i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="05360-141">To enable streaming via the [Azure PowerShell Cmdlets](insights-powershell-samples.md), you can use the `Set-AzureRmDiagnosticSetting` cmdlet with these parameters:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource ID] -ServiceBusRuleId [your Service Bus rule ID] -Enabled $true
```

<span data-ttu-id="05360-142">L'ID regola del bus di servizio è una stringa nel formato seguente: `{Service Bus resource ID}/authorizationrules/{key name}`. Ad esempio, `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`.</span><span class="sxs-lookup"><span data-stu-id="05360-142">The Service Bus Rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`, for example, `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`.</span></span>

### <a name="via-azure-cli"></a><span data-ttu-id="05360-143">Tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="05360-143">Via Azure CLI</span></span>
<span data-ttu-id="05360-144">Per abilitare la trasmissione tramite l'[interfaccia della riga di comando di Azure](insights-cli-samples.md), è possibile usare il comando `insights diagnostic set` come segue:</span><span class="sxs-lookup"><span data-stu-id="05360-144">To enable streaming via the [Azure CLI](insights-cli-samples.md), you can use the `insights diagnostic set` command like this:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceID> --serviceBusRuleId <serviceBusRuleID> --enabled true
```

<span data-ttu-id="05360-145">Usare lo stesso formato per l'ID regola del bus di servizio, come illustrato per il cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="05360-145">Use the same format for Service Bus Rule ID as explained for the PowerShell Cmdlet.</span></span>

## <a name="how-do-i-consume-the-log-data-from-event-hubs"></a><span data-ttu-id="05360-146">Come utilizzare i dati di log da Hub eventi</span><span class="sxs-lookup"><span data-stu-id="05360-146">How do I consume the log data from Event Hubs?</span></span>
<span data-ttu-id="05360-147">Di seguito è riportato un esempio di dati di output da Hub eventi:</span><span class="sxs-lookup"><span data-stu-id="05360-147">Here is sample output data from Event Hubs:</span></span>

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

| <span data-ttu-id="05360-148">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="05360-148">Element Name</span></span> | <span data-ttu-id="05360-149">Description</span><span class="sxs-lookup"><span data-stu-id="05360-149">Description</span></span> |
| --- | --- |
| <span data-ttu-id="05360-150">records</span><span class="sxs-lookup"><span data-stu-id="05360-150">records</span></span> |<span data-ttu-id="05360-151">Matrice di tutti gli eventi di log nel payload.</span><span class="sxs-lookup"><span data-stu-id="05360-151">An array of all log events in this payload.</span></span> |
| <span data-ttu-id="05360-152">time</span><span class="sxs-lookup"><span data-stu-id="05360-152">time</span></span> |<span data-ttu-id="05360-153">Ora in cui si è verificato l'evento.</span><span class="sxs-lookup"><span data-stu-id="05360-153">Time at which the event occurred.</span></span> |
| <span data-ttu-id="05360-154">category</span><span class="sxs-lookup"><span data-stu-id="05360-154">category</span></span> |<span data-ttu-id="05360-155">Categoria di log per l'evento.</span><span class="sxs-lookup"><span data-stu-id="05360-155">Log category for this event.</span></span> |
| <span data-ttu-id="05360-156">resourceId</span><span class="sxs-lookup"><span data-stu-id="05360-156">resourceId</span></span> |<span data-ttu-id="05360-157">ID risorsa della risorsa che ha generato l'evento.</span><span class="sxs-lookup"><span data-stu-id="05360-157">Resource ID of the resource that generated this event.</span></span> |
| <span data-ttu-id="05360-158">operationName</span><span class="sxs-lookup"><span data-stu-id="05360-158">operationName</span></span> |<span data-ttu-id="05360-159">Nome dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="05360-159">Name of the operation.</span></span> |
| <span data-ttu-id="05360-160">level</span><span class="sxs-lookup"><span data-stu-id="05360-160">level</span></span> |<span data-ttu-id="05360-161">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="05360-161">Optional.</span></span> <span data-ttu-id="05360-162">Indica il livello dell'evento di log.</span><span class="sxs-lookup"><span data-stu-id="05360-162">Indicates the log event level.</span></span> |
| <span data-ttu-id="05360-163">properties</span><span class="sxs-lookup"><span data-stu-id="05360-163">properties</span></span> |<span data-ttu-id="05360-164">Proprietà dell'evento.</span><span class="sxs-lookup"><span data-stu-id="05360-164">Properties of the event.</span></span> |

<span data-ttu-id="05360-165">Per un elenco di tutti i provider di risorse che supportano la trasmissione a Hub eventi, vedere [questo articolo](monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="05360-165">You can view a list of all resource providers that support streaming to Event Hubs [here](monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="stream-data-from-compute-resources"></a><span data-ttu-id="05360-166">Eseguire lo streaming di dati dalle risorse di calcolo</span><span class="sxs-lookup"><span data-stu-id="05360-166">Stream data from Compute resources</span></span>
<span data-ttu-id="05360-167">È anche possibile eseguire lo streaming di log di diagnostica dalle risorse di calcolo usando l'agente di Diagnostica di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="05360-167">You can also stream diagnostic logs from Compute resources using the Windows Azure Diagnostics agent.</span></span> <span data-ttu-id="05360-168">Per informazioni sulla configurazione, [vedere questo articolo](../event-hubs/event-hubs-streaming-azure-diags-data.md).</span><span class="sxs-lookup"><span data-stu-id="05360-168">[See this article](../event-hubs/event-hubs-streaming-azure-diags-data.md) for how to set that up.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05360-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="05360-169">Next steps</span></span>
* [<span data-ttu-id="05360-170">Altre informazioni sui log di diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="05360-170">Read more about Azure Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
* [<span data-ttu-id="05360-171">Introduzione all'Hub eventi</span><span class="sxs-lookup"><span data-stu-id="05360-171">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

