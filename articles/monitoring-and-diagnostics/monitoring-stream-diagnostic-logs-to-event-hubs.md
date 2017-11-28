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
# <a name="stream-azure-diagnostic-logs-tooan-event-hubs-namespace"></a><span data-ttu-id="f9fcd-103">I log di diagnostica Azure tooan Namespace hub eventi del flusso</span><span class="sxs-lookup"><span data-stu-id="f9fcd-103">Stream Azure Diagnostic Logs tooan Event Hubs Namespace</span></span>
<span data-ttu-id="f9fcd-104">**[I log di diagnostica Azure](monitoring-overview-of-diagnostic-logs.md)**  può essere trasmesso quasi in tempo reale tooany applicazione utilizzando l'hello incorporati "Esportazione tooEvent hub" opzione in hello portale o abilitando hello ID regola Bus di servizio in un'impostazione di diagnostica tramite hello Azure PowerShell I cmdlet o Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f9fcd-104">**[Azure diagnostic logs](monitoring-overview-of-diagnostic-logs.md)** can be streamed in near real time tooany application using hello built-in “Export tooEvent Hubs” option in hello Portal, or by enabling hello Service Bus Rule ID in a diagnostic setting via hello Azure PowerShell Cmdlets or Azure CLI.</span></span>

## <a name="what-you-can-do-with-diagnostics-logs-and-event-hubs"></a><span data-ttu-id="f9fcd-105">Che cosa si può fare con i log di diagnostica e Hub eventi</span><span class="sxs-lookup"><span data-stu-id="f9fcd-105">What you can do with diagnostics logs and Event Hubs</span></span>
<span data-ttu-id="f9fcd-106">Ecco alcune delle modalità è possibile utilizzare hello lo streaming di funzionalità per i log di diagnostica:</span><span class="sxs-lookup"><span data-stu-id="f9fcd-106">Here are just a few ways you might use hello streaming capability for Diagnostic Logs:</span></span>

* <span data-ttu-id="f9fcd-107">**Flusso registra sistemi di registrazione e i dati di telemetria di terze parti too3rd** – nel tempo, gli hub di eventi di flusso diventeranno hello meccanismo toopipe i log di diagnostica in parti toothird Siem e soluzioni analitica di log.</span><span class="sxs-lookup"><span data-stu-id="f9fcd-107">**Stream logs too3rd party logging and telemetry systems** – Over time, Event Hubs streaming will become hello mechanism toopipe your diagnostic logs in toothird-party SIEMs and log analytics solutions.</span></span>
* <span data-ttu-id="f9fcd-108">**Integrità del servizio per visualizzare, streaming "percorso critico" dati tooPowerBI** – tramite hub di eventi, flusso Analitica e Power BI, è possibile trasformare facilmente i dati di diagnostica in informazioni in tempo reale toonear in servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="f9fcd-108">**View service health by streaming “hot path” data tooPowerBI** – Using Event Hubs, Stream Analytics, and PowerBI, you can easily transform your diagnostics data in toonear real-time insights on your Azure services.</span></span> <span data-ttu-id="f9fcd-109">[In questo articolo di documentazione fornisce una panoramica del tooset di hub di eventi, elaborano i dati con flusso Analitica e usare Power BI come output](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="f9fcd-109">[This documentation article gives a great overview of how tooset up Event Hubs, process data with Stream Analytics, and use PowerBI as an output](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span></span> <span data-ttu-id="f9fcd-110">Ecco alcuni suggerimenti per la configurazione dei log di diagnostica:</span><span class="sxs-lookup"><span data-stu-id="f9fcd-110">Here are a few tips for getting set up with diagnostic logs:</span></span>
  
  * <span data-ttu-id="f9fcd-111">Un hub di eventi per una categoria di log di diagnostica viene creato automaticamente quando si archiviano opzione hello nel portale di hello o abilitarla tramite PowerShell, pertanto si hub di eventi tooselect hello hello dello spazio dei nomi con nome hello che inizia con **insights**.</span><span class="sxs-lookup"><span data-stu-id="f9fcd-111">An event hub for a category of diagnostic logs is created automatically when you check hello option in hello portal or enable it through PowerShell, so you want tooselect hello event hub in hello namespace with hello name that starts with **insights-**.</span></span>
  * <span data-ttu-id="f9fcd-112">Hello codice SQL seguente è riportato un esempio flusso Analitica query che è possibile utilizzare tooparse tutti i dati di log hello nella tabella di Power BI tooa:</span><span class="sxs-lookup"><span data-stu-id="f9fcd-112">hello following SQL code is a sample Stream Analytics query that you can use tooparse all hello log data in tooa PowerBI table:</span></span>

    ```sql
    SELECT
    records.ArrayValue.[Properties you want tootrack]
    INTO
    [OutputSourceName – hello PowerBI source]
    FROM
    [InputSourceName] AS e
    CROSS APPLY GetArrayElements(e.records) AS records
    ```

* <span data-ttu-id="f9fcd-113">**Compilare una piattaforma di registrazione e i dati di telemetria personalizzati** : se si dispone già di una piattaforma dati di telemetria personalizzati o sono solo le compilazione uno, hello altamente scalabile di pubblicazione-sottoscrizione natura degli hub di eventi consente tooflexibly inserimento diagnostica log.</span><span class="sxs-lookup"><span data-stu-id="f9fcd-113">**Build a custom telemetry and logging platform** – If you already have a custom-built telemetry platform or are just thinking about building one, hello highly scalable publish-subscribe nature of Event Hubs allows you tooflexibly ingest diagnostic logs.</span></span> <span data-ttu-id="f9fcd-114">[Vedere toousing di Guida di Dan Rosanova hub eventi in una piattaforma di dati di telemetria di su scala globale](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span><span class="sxs-lookup"><span data-stu-id="f9fcd-114">[See Dan Rosanova’s guide toousing Event Hubs in a global scale telemetry platform here](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span></span>

## <a name="enable-streaming-of-diagnostic-logs"></a><span data-ttu-id="f9fcd-115">Abilitare la trasmissione dei log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="f9fcd-115">Enable streaming of diagnostic logs</span></span>
<span data-ttu-id="f9fcd-116">È possibile abilitare il flusso di log di diagnostica a livello di codice, tramite il portale di hello, o tramite hello [API REST di Azure monitoraggio](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings).</span><span class="sxs-lookup"><span data-stu-id="f9fcd-116">You can enable streaming of diagnostic logs programmatically, via hello portal, or using hello [Azure Monitor REST APIs](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings).</span></span> <span data-ttu-id="f9fcd-117">In entrambi i casi, si crea un'impostazione di diagnostica in cui specificare uno spazio dei nomi dell'hub eventi e categorie log hello e metriche da toosend toohello dello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="f9fcd-117">Either way, you create a diagnostic setting in which you specify an Event Hubs namespace and hello log categories and metrics you want toosend in toohello namespace.</span></span> <span data-ttu-id="f9fcd-118">Un hub eventi viene creato nello spazio dei nomi hello per ogni categoria di log che attiva.</span><span class="sxs-lookup"><span data-stu-id="f9fcd-118">An event hub is created in hello namespace for each log category you enable.</span></span> <span data-ttu-id="f9fcd-119">Una **categoria di log** di diagnostica è un tipo di log che una risorsa può raccogliere.</span><span class="sxs-lookup"><span data-stu-id="f9fcd-119">A diagnostic **log category** is a type of log that a resource may collect.</span></span>

> [!WARNING]
> <span data-ttu-id="f9fcd-120">Per abilitare la trasmissione dei log di diagnostica da risorse di calcolo, ad esempio le macchine virtuali o Service Fabric, è necessario [seguire una procedura diversa](../event-hubs/event-hubs-streaming-azure-diags-data.md).</span><span class="sxs-lookup"><span data-stu-id="f9fcd-120">Enabling and streaming diagnostic logs from Compute resources (for example, VMs or Service Fabric) [requires a different set of steps](../event-hubs/event-hubs-streaming-azure-diags-data.md).</span></span>
> 
> 

<span data-ttu-id="f9fcd-121">Hello Bus di servizio o hub eventi dello spazio dei nomi è disponibile toobe hello stessa sottoscrizione di risorse hello la creazione di log come utente di hello che configura l'impostazione di hello dispone di sottoscrizioni di tooboth accesso RBAC appropriate.</span><span class="sxs-lookup"><span data-stu-id="f9fcd-121">hello Service Bus or Event Hubs namespace does not have toobe in hello same subscription as hello resource emitting logs as long as hello user who configures hello setting has appropriate RBAC access tooboth subscriptions.</span></span>

## <a name="stream-diagnostic-logs-using-hello-portal"></a><span data-ttu-id="f9fcd-122">Log di diagnostica di flusso tramite il portale di hello</span><span class="sxs-lookup"><span data-stu-id="f9fcd-122">Stream diagnostic logs using hello portal</span></span>
1. <span data-ttu-id="f9fcd-123">Nel portale di hello passare tooAzure Monitor e fare clic su **le impostazioni di diagnostica**</span><span class="sxs-lookup"><span data-stu-id="f9fcd-123">In hello portal, navigate tooAzure Monitor and click on **Diagnostic Settings**</span></span>

    ![Sezione relativa al monitoraggio di Monitoraggio di Azure](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-blade.png)

2. <span data-ttu-id="f9fcd-125">Se lo si desidera filtrare l'elenco hello in base al tipo di risorsa o gruppo di risorse, fare clic sul risorse hello per il quale si desidera tooset un'impostazione di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="f9fcd-125">Optionally filter hello list by resource group or resource type, then click on hello resource for which you would like tooset a diagnostic setting.</span></span>

3. <span data-ttu-id="f9fcd-126">Se nessuna impostazione esistano nella risorsa hello selezionata, verrà richiesta toocreate un'impostazione.</span><span class="sxs-lookup"><span data-stu-id="f9fcd-126">If no settings exist on hello resource you have selected, you are prompted toocreate a setting.</span></span> <span data-ttu-id="f9fcd-127">Fare clic su "Attiva diagnostica".</span><span class="sxs-lookup"><span data-stu-id="f9fcd-127">Click "Turn on diagnostics."</span></span>

   ![Aggiungi impostazione di diagnostica - Nessuna impostazione esistente](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-none.png)

   <span data-ttu-id="f9fcd-129">Se sono presenti le impostazioni esistenti sulla risorsa hello, vedrai un elenco di impostazioni già configurato per questa risorsa.</span><span class="sxs-lookup"><span data-stu-id="f9fcd-129">If there are existing settings on hello resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="f9fcd-130">Fare clic su "Add diagnostic setting" (Aggiungi impostazione di diagnostica).</span><span class="sxs-lookup"><span data-stu-id="f9fcd-130">Click "Add diagnostic setting."</span></span>

   !["Add diagnostic setting" (Aggiungi impostazione di diagnostica) - impostazioni esistenti](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="f9fcd-132">Assegnare un nome all'impostazione e casella hello per **hub di eventi di flusso tooan**, quindi selezionare uno spazio dei nomi dell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="f9fcd-132">Give your setting a name and check hello box for **Stream tooan event hub**, then select an Event Hubs namespace.</span></span>
   
   !["Add diagnostic setting" (Aggiungi impostazione di diagnostica) - impostazioni esistenti](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-configure.png)
    
   <span data-ttu-id="f9fcd-134">Hello dello spazio dei nomi selezionato sarà in hub eventi hello è creato (se questa è la prima volta che i log di diagnostica di streaming) o inviati nel flusso troppo (se sono già presenti risorse in tale spazio dei nomi di registro categoria toothis streaming), e i criteri di hello definiscono hello dispone di autorizzazioni che hello meccanismo di flusso.</span><span class="sxs-lookup"><span data-stu-id="f9fcd-134">hello namespace selected will be where hello event hub is created (if this is your first time streaming diagnostic logs) or streamed too(if there are already resources that are streaming that log category toothis namespace), and hello policy defines hello permissions that hello streaming mechanism has.</span></span> <span data-ttu-id="f9fcd-135">Oggi, streaming tooan richiede le autorizzazioni di ascolto, invio e gestione in hub eventi.</span><span class="sxs-lookup"><span data-stu-id="f9fcd-135">Today, streaming tooan event hub requires Manage, Send, and Listen permissions.</span></span> <span data-ttu-id="f9fcd-136">È possibile creare o modificare i criteri di accesso condiviso di spazio dei nomi di hub eventi nel portale di hello nella scheda Configura hello dello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="f9fcd-136">You can create or modify Event Hubs namespace shared access policies in hello portal under hello Configure tab for your namespace.</span></span> <span data-ttu-id="f9fcd-137">tooupdate una di queste impostazioni di diagnostica, hello client disponga di autorizzazioni ListKey hello nella regola di autorizzazione hello hub eventi.</span><span class="sxs-lookup"><span data-stu-id="f9fcd-137">tooupdate one of these diagnostic settings, hello client must have hello ListKey permission on hello Event Hubs authorization rule.</span></span>

4. <span data-ttu-id="f9fcd-138">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="f9fcd-138">Click **Save**.</span></span>

<span data-ttu-id="f9fcd-139">Dopo alcuni istanti, hello nuova impostazione è visualizzata nell'elenco delle impostazioni per questa risorsa e i log di diagnostica sono state trasmesse toothat account di archiviazione come nuovi dati di evento viene generati.</span><span class="sxs-lookup"><span data-stu-id="f9fcd-139">After a few moments, hello new setting appears in your list of settings for this resource, and diagnostic logs are streamed toothat storage account as soon as new event data is generated.</span></span>

### <a name="via-powershell-cmdlets"></a><span data-ttu-id="f9fcd-140">Tramite i cmdlet di PowerShell</span><span class="sxs-lookup"><span data-stu-id="f9fcd-140">Via PowerShell Cmdlets</span></span>
<span data-ttu-id="f9fcd-141">streaming tramite hello tooenable [i cmdlet di PowerShell Azure](insights-powershell-samples.md), è possibile utilizzare hello `Set-AzureRmDiagnosticSetting` cmdlet con i seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="f9fcd-141">tooenable streaming via hello [Azure PowerShell Cmdlets](insights-powershell-samples.md), you can use hello `Set-AzureRmDiagnosticSetting` cmdlet with these parameters:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource ID] -ServiceBusRuleId [your Service Bus rule ID] -Enabled $true
```

<span data-ttu-id="f9fcd-142">Hello ID regola Bus di servizio è una stringa con questo formato: `{Service Bus resource ID}/authorizationrules/{key name}`, ad esempio, `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`.</span><span class="sxs-lookup"><span data-stu-id="f9fcd-142">hello Service Bus Rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`, for example, `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`.</span></span>

### <a name="via-azure-cli"></a><span data-ttu-id="f9fcd-143">Tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="f9fcd-143">Via Azure CLI</span></span>
<span data-ttu-id="f9fcd-144">streaming tramite hello tooenable [CLI di Azure](insights-cli-samples.md), è possibile utilizzare hello `insights diagnostic set` comando simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="f9fcd-144">tooenable streaming via hello [Azure CLI](insights-cli-samples.md), you can use hello `insights diagnostic set` command like this:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceID> --serviceBusRuleId <serviceBusRuleID> --enabled true
```

<span data-ttu-id="f9fcd-145">Utilizzare hello stesso formato per ID regola Bus di servizio, come illustrato per hello Cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f9fcd-145">Use hello same format for Service Bus Rule ID as explained for hello PowerShell Cmdlet.</span></span>

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a><span data-ttu-id="f9fcd-146">Come utilizzano i dati del log hello dagli hub eventi?</span><span class="sxs-lookup"><span data-stu-id="f9fcd-146">How do I consume hello log data from Event Hubs?</span></span>
<span data-ttu-id="f9fcd-147">Di seguito è riportato un esempio di dati di output da Hub eventi:</span><span class="sxs-lookup"><span data-stu-id="f9fcd-147">Here is sample output data from Event Hubs:</span></span>

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

| <span data-ttu-id="f9fcd-148">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="f9fcd-148">Element Name</span></span> | <span data-ttu-id="f9fcd-149">Description</span><span class="sxs-lookup"><span data-stu-id="f9fcd-149">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f9fcd-150">records</span><span class="sxs-lookup"><span data-stu-id="f9fcd-150">records</span></span> |<span data-ttu-id="f9fcd-151">Matrice di tutti gli eventi di log nel payload.</span><span class="sxs-lookup"><span data-stu-id="f9fcd-151">An array of all log events in this payload.</span></span> |
| <span data-ttu-id="f9fcd-152">time</span><span class="sxs-lookup"><span data-stu-id="f9fcd-152">time</span></span> |<span data-ttu-id="f9fcd-153">Ora di hello evento.</span><span class="sxs-lookup"><span data-stu-id="f9fcd-153">Time at which hello event occurred.</span></span> |
| <span data-ttu-id="f9fcd-154">category</span><span class="sxs-lookup"><span data-stu-id="f9fcd-154">category</span></span> |<span data-ttu-id="f9fcd-155">Categoria di log per l'evento.</span><span class="sxs-lookup"><span data-stu-id="f9fcd-155">Log category for this event.</span></span> |
| <span data-ttu-id="f9fcd-156">resourceId</span><span class="sxs-lookup"><span data-stu-id="f9fcd-156">resourceId</span></span> |<span data-ttu-id="f9fcd-157">ID risorsa della risorsa hello che ha generato questo evento.</span><span class="sxs-lookup"><span data-stu-id="f9fcd-157">Resource ID of hello resource that generated this event.</span></span> |
| <span data-ttu-id="f9fcd-158">operationName</span><span class="sxs-lookup"><span data-stu-id="f9fcd-158">operationName</span></span> |<span data-ttu-id="f9fcd-159">Nome dell'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="f9fcd-159">Name of hello operation.</span></span> |
| <span data-ttu-id="f9fcd-160">level</span><span class="sxs-lookup"><span data-stu-id="f9fcd-160">level</span></span> |<span data-ttu-id="f9fcd-161">Facoltativo.</span><span class="sxs-lookup"><span data-stu-id="f9fcd-161">Optional.</span></span> <span data-ttu-id="f9fcd-162">Indica il livello di evento log hello.</span><span class="sxs-lookup"><span data-stu-id="f9fcd-162">Indicates hello log event level.</span></span> |
| <span data-ttu-id="f9fcd-163">properties</span><span class="sxs-lookup"><span data-stu-id="f9fcd-163">properties</span></span> |<span data-ttu-id="f9fcd-164">Proprietà di evento hello.</span><span class="sxs-lookup"><span data-stu-id="f9fcd-164">Properties of hello event.</span></span> |

<span data-ttu-id="f9fcd-165">È possibile visualizzare un elenco di tutti i provider di risorse che supportano flussi hub tooEvent [qui](monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="f9fcd-165">You can view a list of all resource providers that support streaming tooEvent Hubs [here](monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="stream-data-from-compute-resources"></a><span data-ttu-id="f9fcd-166">Eseguire lo streaming di dati dalle risorse di calcolo</span><span class="sxs-lookup"><span data-stu-id="f9fcd-166">Stream data from Compute resources</span></span>
<span data-ttu-id="f9fcd-167">È inoltre possibile trasmettere i log di diagnostica dalle risorse di calcolo utilizzando hello agente di diagnostica Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="f9fcd-167">You can also stream diagnostic logs from Compute resources using hello Windows Azure Diagnostics agent.</span></span> <span data-ttu-id="f9fcd-168">[Vedere l'articolo](../event-hubs/event-hubs-streaming-azure-diags-data.md) come tooset tale backup.</span><span class="sxs-lookup"><span data-stu-id="f9fcd-168">[See this article](../event-hubs/event-hubs-streaming-azure-diags-data.md) for how tooset that up.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9fcd-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f9fcd-169">Next steps</span></span>
* [<span data-ttu-id="f9fcd-170">Altre informazioni sui log di diagnostica di Azure</span><span class="sxs-lookup"><span data-stu-id="f9fcd-170">Read more about Azure Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
* [<span data-ttu-id="f9fcd-171">Introduzione all'Hub eventi</span><span class="sxs-lookup"><span data-stu-id="f9fcd-171">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

