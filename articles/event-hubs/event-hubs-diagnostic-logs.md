---
title: log di diagnostica di hub eventi aaaAzure | Documenti Microsoft
description: Informazioni su come tooset dei log di diagnostica per gli hub di eventi in Azure.
keywords: 
documentationcenter: 
services: event-hubs
author: banisadr
manager: 
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: sethm;babanisa
ms.openlocfilehash: d2054e2e444e715e5077fe2608fe1e009e6c1d84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-diagnostic-logs"></a><span data-ttu-id="e1c13-103">Log di diagnostica di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="e1c13-103">Event Hubs diagnostic logs</span></span>

<span data-ttu-id="e1c13-104">È possibile visualizzare due tipi di log per Hub eventi di Azure:</span><span class="sxs-lookup"><span data-stu-id="e1c13-104">You can view two types of logs for Azure Event Hubs:</span></span>
* <span data-ttu-id="e1c13-105">**[Log attività](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="e1c13-105">**[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span></span> <span data-ttu-id="e1c13-106">Questi log contengono informazioni sulle operazioni eseguite in un processo.</span><span class="sxs-lookup"><span data-stu-id="e1c13-106">These logs have information about operations performed on a job.</span></span> <span data-ttu-id="e1c13-107">registri Hello sono sempre abilitati.</span><span class="sxs-lookup"><span data-stu-id="e1c13-107">hello logs are always enabled.</span></span>
* <span data-ttu-id="e1c13-108">**[Log di diagnostica](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="e1c13-108">**[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span></span> <span data-ttu-id="e1c13-109">È possibile configurare i log di diagnostica per una visualizzazione più completa di tutto ciò che accade in un processo.</span><span class="sxs-lookup"><span data-stu-id="e1c13-109">You can configure diagnostic logs for a richer view of everything that happens with a job.</span></span> <span data-ttu-id="e1c13-110">Le attività di copertura di log di diagnostica da ora hello hello processo viene creato fino a quando non viene eliminato il processo di hello, inclusi gli aggiornamenti e le attività che si verificano durante l'esecuzione del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="e1c13-110">Diagnostic logs cover activities from hello time hello job is created until hello job is deleted, including updates and activities that occur while hello job is running.</span></span>

## <a name="turn-on-diagnostic-logs"></a><span data-ttu-id="e1c13-111">Attivare i log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="e1c13-111">Turn on diagnostic logs</span></span>
<span data-ttu-id="e1c13-112">I log di diagnostica sono disabilitati per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="e1c13-112">Diagnostics logs are disabled by default.</span></span> <span data-ttu-id="e1c13-113">log di diagnostica tooenable:</span><span class="sxs-lookup"><span data-stu-id="e1c13-113">tooenable diagnostic logs:</span></span>

1.  <span data-ttu-id="e1c13-114">In hello [portale di Azure](https://portal.azure.com)in **monitoraggio + gestione**, fare clic su **log di diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="e1c13-114">In hello [Azure portal](https://portal.azure.com), under **Monitoring + Management**, click **Diagnostics logs**.</span></span>

    ![pannello navigazione toodiagnostic log](./media/event-hubs-diagnostic-logs/image1.png)

2.  <span data-ttu-id="e1c13-116">Fare clic sulla risorsa hello da toomonitor.</span><span class="sxs-lookup"><span data-stu-id="e1c13-116">Click hello resource you want toomonitor.</span></span>

3.  <span data-ttu-id="e1c13-117">Fare clic su **Attiva diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="e1c13-117">Click **Turn on diagnostics**.</span></span>

    ![Attivare i log di diagnostica](./media/event-hubs-diagnostic-logs/image2.png)

4.  <span data-ttu-id="e1c13-119">Per **Stato** fare clic su **Attivato**.</span><span class="sxs-lookup"><span data-stu-id="e1c13-119">For **Status**, click **On**.</span></span>

    ![Modificare lo stato di hello del log di diagnostica](./media/event-hubs-diagnostic-logs/image3.png)

5.  <span data-ttu-id="e1c13-121">Destinazione di archiviazione hello set che si desidera. ad esempio, un account di archiviazione, un hub eventi o Analitica di Log di Azure.</span><span class="sxs-lookup"><span data-stu-id="e1c13-121">Set hello archive target that you want; for example, a storage account, an event hub, or Azure Log Analytics.</span></span>

6.  <span data-ttu-id="e1c13-122">Salvare le impostazioni di diagnostica nuovo hello.</span><span class="sxs-lookup"><span data-stu-id="e1c13-122">Save hello new diagnostics settings.</span></span>

<span data-ttu-id="e1c13-123">Le nuove impostazioni diventano effettive in circa 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="e1c13-123">New settings take effect in about 10 minutes.</span></span> <span data-ttu-id="e1c13-124">Successivamente, i log vengono visualizzati nella destinazione di archiviazione configurato hello, su hello **log di diagnostica** blade.</span><span class="sxs-lookup"><span data-stu-id="e1c13-124">After that, logs appear in hello configured archival target, on hello **Diagnostics logs** blade.</span></span>

<span data-ttu-id="e1c13-125">Per ulteriori informazioni sulla configurazione di diagnostica, vedere hello [panoramica dei log di diagnostica Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="e1c13-125">For more information about configuring diagnostics, see hello [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="diagnostic-logs-categories"></a><span data-ttu-id="e1c13-126">Categorie dei log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="e1c13-126">Diagnostic logs categories</span></span>
<span data-ttu-id="e1c13-127">Hub eventi consente di acquisire i log di diagnostica per due categorie:</span><span class="sxs-lookup"><span data-stu-id="e1c13-127">Event Hubs captures diagnostic logs for two categories:</span></span>

* <span data-ttu-id="e1c13-128">**ArchiveLogs**: log relativi archivi hub tooEvent, in particolare, registra gli errori di tooarchive correlati.</span><span class="sxs-lookup"><span data-stu-id="e1c13-128">**ArchiveLogs**: logs related tooEvent Hubs archives, specifically, logs related tooarchive errors.</span></span>
* <span data-ttu-id="e1c13-129">**OperationalLogs**: informazioni su ciò che avviene durante le operazioni di hub eventi, in particolare, il tipo di operazione, inclusa la creazione di hub eventi, le risorse usate, hello e hello lo stato dell'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="e1c13-129">**OperationalLogs**: information about what is happening during Event Hubs operations, specifically, hello operation type, including event hub creation, resources used, and hello status of hello operation.</span></span>

## <a name="diagnostic-logs-schema"></a><span data-ttu-id="e1c13-130">Schema dei log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="e1c13-130">Diagnostic logs schema</span></span>
<span data-ttu-id="e1c13-131">Tutti i log vengono archiviati in formato JavaScript Object Notation (JSON).</span><span class="sxs-lookup"><span data-stu-id="e1c13-131">All logs are stored in JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="e1c13-132">Ogni voce include i campi stringa di formato hello descritto in hello le sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="e1c13-132">Each entry has string fields that use hello format described in hello following sections.</span></span>

### <a name="archive-logs-schema"></a><span data-ttu-id="e1c13-133">Schema dei log di archiviazione</span><span class="sxs-lookup"><span data-stu-id="e1c13-133">Archive logs schema</span></span>

<span data-ttu-id="e1c13-134">Le stringhe JSON di log di archiviazione includono gli elementi elencati in hello nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="e1c13-134">Archive log JSON strings include elements listed in hello following table:</span></span>

<span data-ttu-id="e1c13-135">Nome</span><span class="sxs-lookup"><span data-stu-id="e1c13-135">Name</span></span> | <span data-ttu-id="e1c13-136">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e1c13-136">Description</span></span>
------- | -------
<span data-ttu-id="e1c13-137">TaskName</span><span class="sxs-lookup"><span data-stu-id="e1c13-137">TaskName</span></span> | <span data-ttu-id="e1c13-138">Descrizione dell'attività hello che non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="e1c13-138">Description of hello task that failed.</span></span>
<span data-ttu-id="e1c13-139">ActivityId</span><span class="sxs-lookup"><span data-stu-id="e1c13-139">ActivityId</span></span> | <span data-ttu-id="e1c13-140">ID interno, usato a scopo di rilevamento.</span><span class="sxs-lookup"><span data-stu-id="e1c13-140">Internal ID, used for tracking.</span></span>
<span data-ttu-id="e1c13-141">trackingId</span><span class="sxs-lookup"><span data-stu-id="e1c13-141">trackingId</span></span> | <span data-ttu-id="e1c13-142">ID interno, usato a scopo di rilevamento.</span><span class="sxs-lookup"><span data-stu-id="e1c13-142">Internal ID, used for tracking.</span></span>
<span data-ttu-id="e1c13-143">resourceId</span><span class="sxs-lookup"><span data-stu-id="e1c13-143">resourceId</span></span> | <span data-ttu-id="e1c13-144">ID della risorsa di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e1c13-144">Azure Resource Manager resource ID.</span></span>
<span data-ttu-id="e1c13-145">eventHub</span><span class="sxs-lookup"><span data-stu-id="e1c13-145">eventHub</span></span> | <span data-ttu-id="e1c13-146">Nome completo dell'hub eventi, include il nome dello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="e1c13-146">Event hub full name (includes namespace name).</span></span>
<span data-ttu-id="e1c13-147">partitionId</span><span class="sxs-lookup"><span data-stu-id="e1c13-147">partitionId</span></span> | <span data-ttu-id="e1c13-148">Partizione dell'hub eventi per l'operazione di scrittura.</span><span class="sxs-lookup"><span data-stu-id="e1c13-148">Event Hub partition being written to.</span></span>
<span data-ttu-id="e1c13-149">archiveStep</span><span class="sxs-lookup"><span data-stu-id="e1c13-149">archiveStep</span></span> | <span data-ttu-id="e1c13-150">ArchiveFlushWriter</span><span class="sxs-lookup"><span data-stu-id="e1c13-150">ArchiveFlushWriter</span></span>
<span data-ttu-id="e1c13-151">startTime</span><span class="sxs-lookup"><span data-stu-id="e1c13-151">startTime</span></span> | <span data-ttu-id="e1c13-152">Ora di inizio di un errore.</span><span class="sxs-lookup"><span data-stu-id="e1c13-152">Failure start time.</span></span>
<span data-ttu-id="e1c13-153">errori</span><span class="sxs-lookup"><span data-stu-id="e1c13-153">failures</span></span> | <span data-ttu-id="e1c13-154">Numero di volte in cui si è verificato un errore.</span><span class="sxs-lookup"><span data-stu-id="e1c13-154">Number of times failure occurred.</span></span>
<span data-ttu-id="e1c13-155">durationInSeconds</span><span class="sxs-lookup"><span data-stu-id="e1c13-155">durationInSeconds</span></span> | <span data-ttu-id="e1c13-156">Durata dell'errore.</span><span class="sxs-lookup"><span data-stu-id="e1c13-156">Duration of failure.</span></span>
<span data-ttu-id="e1c13-157">Message</span><span class="sxs-lookup"><span data-stu-id="e1c13-157">message</span></span> | <span data-ttu-id="e1c13-158">Messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="e1c13-158">Error message.</span></span>
<span data-ttu-id="e1c13-159">category</span><span class="sxs-lookup"><span data-stu-id="e1c13-159">category</span></span> | <span data-ttu-id="e1c13-160">ArchiveLogs</span><span class="sxs-lookup"><span data-stu-id="e1c13-160">ArchiveLogs</span></span>

<span data-ttu-id="e1c13-161">Hello codice riportato di seguito è riportato un esempio di un stringa JSON del log di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="e1c13-161">hello following code is an example of an archive log JSON string:</span></span>

```json
{
     "TaskName": "EventHubArchiveUserError",
     "ActivityId": "21b89a0b-8095-471a-9db8-d151d74ecf26",
     "trackingId": "21b89a0b-8095-471a-9db8-d151d74ecf26_B7",
     "resourceId": "/SUBSCRIPTIONS/854D368F-1828-428F-8F3C-F2AFFA9B2F7D/RESOURCEGROUPS/DEFAULT-EVENTHUB-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/FBETTATI-OPERA-EVENTHUB",
     "eventHub": "fbettati-opera-eventhub:eventhub:eh123~32766",
     "partitionId": "1",
     "archiveStep": "ArchiveFlushWriter",
     "startTime": "9/22/2016 5:11:21 AM",
     "failures": 3,
     "durationInSeconds": 360,
     "message": "Microsoft.WindowsAzure.Storage.StorageException: hello remote server returned an error: (404) Not Found. ---> System.Net.WebException: hello remote server returned an error: (404) Not Found.\r\n   at Microsoft.WindowsAzure.Storage.Shared.Protocol.HttpResponseParsers.ProcessExpectedStatusCodeNoException[T](HttpStatusCode expectedStatusCode, HttpStatusCode actualStatusCode, T retVal, StorageCommandBase`1 cmd, Exception ex)\r\n   at Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob.<PutBlockImpl>b__3e(RESTCommand`1 cmd, HttpWebResponse resp, Exception ex, OperationContext ctx)\r\n   at Microsoft.WindowsAzure.Storage.Core.Executor.Executor.EndGetResponse[T](IAsyncResult getResponseResult)\r\n   --- End of inner exception stack trace ---\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.StorageAsyncResult`1.End()\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.AsyncExtensions.<>c__DisplayClass4.<CreateCallbackVoid>b__3(IAsyncResult ar)\r\n--- End of stack trace from previous location where exception was thrown ---\r\n   at System.",
     "category": "ArchiveLogs"
}
```

### <a name="operational-logs-schema"></a><span data-ttu-id="e1c13-162">Schema di log operativi</span><span class="sxs-lookup"><span data-stu-id="e1c13-162">Operational logs schema</span></span>

<span data-ttu-id="e1c13-163">Le stringhe JSON registro operativo includono gli elementi elencati in hello nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="e1c13-163">Operational log JSON strings include elements listed in hello following table:</span></span>

<span data-ttu-id="e1c13-164">Nome</span><span class="sxs-lookup"><span data-stu-id="e1c13-164">Name</span></span> | <span data-ttu-id="e1c13-165">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e1c13-165">Description</span></span>
------- | -------
<span data-ttu-id="e1c13-166">ActivityId</span><span class="sxs-lookup"><span data-stu-id="e1c13-166">ActivityId</span></span> | <span data-ttu-id="e1c13-167">ID interno, utilizzato tootrack scopo.</span><span class="sxs-lookup"><span data-stu-id="e1c13-167">Internal ID, used tootrack purpose.</span></span>
<span data-ttu-id="e1c13-168">EventName</span><span class="sxs-lookup"><span data-stu-id="e1c13-168">EventName</span></span> | <span data-ttu-id="e1c13-169">Nome operazione.</span><span class="sxs-lookup"><span data-stu-id="e1c13-169">Operation name.</span></span>  
<span data-ttu-id="e1c13-170">resourceId</span><span class="sxs-lookup"><span data-stu-id="e1c13-170">resourceId</span></span> | <span data-ttu-id="e1c13-171">ID della risorsa di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e1c13-171">Azure Resource Manager resource ID.</span></span>
<span data-ttu-id="e1c13-172">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="e1c13-172">SubscriptionId</span></span> | <span data-ttu-id="e1c13-173">l'ID sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="e1c13-173">Subscription ID.</span></span>
<span data-ttu-id="e1c13-174">EventTimeString</span><span class="sxs-lookup"><span data-stu-id="e1c13-174">EventTimeString</span></span> | <span data-ttu-id="e1c13-175">Durata dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="e1c13-175">Operation time.</span></span>
<span data-ttu-id="e1c13-176">EventProperties</span><span class="sxs-lookup"><span data-stu-id="e1c13-176">EventProperties</span></span> | <span data-ttu-id="e1c13-177">Proprietà dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="e1c13-177">Operation properties.</span></span>
<span data-ttu-id="e1c13-178">Status</span><span class="sxs-lookup"><span data-stu-id="e1c13-178">Status</span></span> | <span data-ttu-id="e1c13-179">Stato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="e1c13-179">Operation status.</span></span>
<span data-ttu-id="e1c13-180">Chiamante</span><span class="sxs-lookup"><span data-stu-id="e1c13-180">Caller</span></span> | <span data-ttu-id="e1c13-181">Chiamante dell'operazione (Portale di Azure o client di gestione).</span><span class="sxs-lookup"><span data-stu-id="e1c13-181">Caller of operation (Azure portal or management client).</span></span>
<span data-ttu-id="e1c13-182">category</span><span class="sxs-lookup"><span data-stu-id="e1c13-182">category</span></span> | <span data-ttu-id="e1c13-183">OperationalLogs</span><span class="sxs-lookup"><span data-stu-id="e1c13-183">OperationalLogs</span></span>

<span data-ttu-id="e1c13-184">Hello codice riportato di seguito è riportato un esempio di una stringa JSON registro operativo:</span><span class="sxs-lookup"><span data-stu-id="e1c13-184">hello following code is an example of an operational log JSON string:</span></span>

```json
Example:
{
     "ActivityId": "6aa994ac-b56e-4292-8448-0767a5657cc7",
     "EventName": "Create EventHub",
     "resourceId": "/SUBSCRIPTIONS/1A2109E3-9DA0-455B-B937-E35E36C1163C/RESOURCEGROUPS/DEFAULT-SERVICEBUS-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/SHOEBOXEHNS-CY4001",
     "SubscriptionId": "1a2109e3-9da0-455b-b937-e35e36c1163c",
     "EventTimeString": "9/28/2016 8:40:06 PM +00:00",
     "EventProperties": "{\"SubscriptionId\":\"1a2109e3-9da0-455b-b937-e35e36c1163c\",\"Namespace\":\"shoeboxehns-cy4001\",\"Via\":\"https://shoeboxehns-cy4001.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",
     "Status": "Succeeded",
     "Caller": "ServiceBus Client",
     "category": "OperationalLogs"
}
```

## <a name="next-steps"></a><span data-ttu-id="e1c13-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e1c13-185">Next steps</span></span>
* [<span data-ttu-id="e1c13-186">Introduzione tooEvent hub</span><span class="sxs-lookup"><span data-stu-id="e1c13-186">Introduction tooEvent Hubs</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="e1c13-187">Panoramica dell'API di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="e1c13-187">Event Hubs API overview</span></span>](event-hubs-api-overview.md)
* [<span data-ttu-id="e1c13-188">Introduzione all'Hub eventi</span><span class="sxs-lookup"><span data-stu-id="e1c13-188">Get started with Event Hubs</span></span>](event-hubs-csharp-ephcs-getstarted.md)
