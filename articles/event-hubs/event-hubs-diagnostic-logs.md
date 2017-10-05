---
title: Log di diagnostica di Hub eventi in Azure | Microsoft Docs
description: Informazioni su come configurare log di diagnostica per gli hub eventi in Azure.
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
ms.openlocfilehash: 09bc62f4918635419d74ef3ae400a41d4ce58b5a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="event-hubs-diagnostic-logs"></a><span data-ttu-id="6bd4a-103">Log di diagnostica di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="6bd4a-103">Event Hubs diagnostic logs</span></span>

<span data-ttu-id="6bd4a-104">È possibile visualizzare due tipi di log per Hub eventi di Azure:</span><span class="sxs-lookup"><span data-stu-id="6bd4a-104">You can view two types of logs for Azure Event Hubs:</span></span>
* <span data-ttu-id="6bd4a-105">**[Log attività](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="6bd4a-105">**[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span></span> <span data-ttu-id="6bd4a-106">Questi log contengono informazioni sulle operazioni eseguite in un processo.</span><span class="sxs-lookup"><span data-stu-id="6bd4a-106">These logs have information about operations performed on a job.</span></span> <span data-ttu-id="6bd4a-107">I log sono sempre attivati.</span><span class="sxs-lookup"><span data-stu-id="6bd4a-107">The logs are always enabled.</span></span>
* <span data-ttu-id="6bd4a-108">**[Log di diagnostica](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="6bd4a-108">**[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span></span> <span data-ttu-id="6bd4a-109">È possibile configurare i log di diagnostica per una visualizzazione più completa di tutto ciò che accade in un processo.</span><span class="sxs-lookup"><span data-stu-id="6bd4a-109">You can configure diagnostic logs for a richer view of everything that happens with a job.</span></span> <span data-ttu-id="6bd4a-110">I log di diagnostica coprono le attività che si verificano dal momento della creazione del processo fino alla sua eliminazione, inclusi gli aggiornamenti e le attività che si verificano durante l'esecuzione del processo.</span><span class="sxs-lookup"><span data-stu-id="6bd4a-110">Diagnostic logs cover activities from the time the job is created until the job is deleted, including updates and activities that occur while the job is running.</span></span>

## <a name="turn-on-diagnostic-logs"></a><span data-ttu-id="6bd4a-111">Attivare i log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="6bd4a-111">Turn on diagnostic logs</span></span>
<span data-ttu-id="6bd4a-112">I log di diagnostica sono disabilitati per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="6bd4a-112">Diagnostics logs are disabled by default.</span></span> <span data-ttu-id="6bd4a-113">Per abilitare i log di diagnostica:</span><span class="sxs-lookup"><span data-stu-id="6bd4a-113">To enable diagnostic logs:</span></span>

1.  <span data-ttu-id="6bd4a-114">Nel [portale di Azure](https://portal.azure.com) in **Monitoraggio + Gestione** fare clic su **Log di diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="6bd4a-114">In the [Azure portal](https://portal.azure.com), under **Monitoring + Management**, click **Diagnostics logs**.</span></span>

    ![Navigazione tra i pannelli per trovare i log di diagnostica](./media/event-hubs-diagnostic-logs/image1.png)

2.  <span data-ttu-id="6bd4a-116">Fare clic sulla risorsa da monitorare.</span><span class="sxs-lookup"><span data-stu-id="6bd4a-116">Click the resource you want to monitor.</span></span>

3.  <span data-ttu-id="6bd4a-117">Fare clic su **Attiva diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="6bd4a-117">Click **Turn on diagnostics**.</span></span>

    ![Attivare i log di diagnostica](./media/event-hubs-diagnostic-logs/image2.png)

4.  <span data-ttu-id="6bd4a-119">Per **Stato** fare clic su **Attivato**.</span><span class="sxs-lookup"><span data-stu-id="6bd4a-119">For **Status**, click **On**.</span></span>

    ![Modifica dello lo stato dei log di diagnostica](./media/event-hubs-diagnostic-logs/image3.png)

5.  <span data-ttu-id="6bd4a-121">Impostare la destinazione di archiviazione desiderata, ad esempio un account di archiviazione, un hub eventi o Azure Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="6bd4a-121">Set the archive target that you want; for example, a storage account, an event hub, or Azure Log Analytics.</span></span>

6.  <span data-ttu-id="6bd4a-122">Salvare le nuove impostazioni di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="6bd4a-122">Save the new diagnostics settings.</span></span>

<span data-ttu-id="6bd4a-123">Le nuove impostazioni diventano effettive in circa 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="6bd4a-123">New settings take effect in about 10 minutes.</span></span> <span data-ttu-id="6bd4a-124">Trascorso questo tempo, i log vengono visualizzati nella destinazione di archiviazione configurata, all'interno del pannello **Log di diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="6bd4a-124">After that, logs appear in the configured archival target, on the **Diagnostics logs** blade.</span></span>

<span data-ttu-id="6bd4a-125">Per altre informazioni sulla configurazione della diagnostica, vedere la [panoramica dei log di diagnostica di Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="6bd4a-125">For more information about configuring diagnostics, see the [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="diagnostic-logs-categories"></a><span data-ttu-id="6bd4a-126">Categorie dei log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="6bd4a-126">Diagnostic logs categories</span></span>
<span data-ttu-id="6bd4a-127">Hub eventi consente di acquisire i log di diagnostica per due categorie:</span><span class="sxs-lookup"><span data-stu-id="6bd4a-127">Event Hubs captures diagnostic logs for two categories:</span></span>

* <span data-ttu-id="6bd4a-128">**ArchiveLogs**: log correlati agli archivi dell'hub eventi, in particolare quelli relativi agli errori di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="6bd4a-128">**ArchiveLogs**: logs related to Event Hubs archives, specifically, logs related to archive errors.</span></span>
* <span data-ttu-id="6bd4a-129">**OperationalLogs**: acquisisce informazioni su ciò che avviene durante il funzionamento dell'hub eventi, in particolare il tipo di operazione, come creazione dell'hub eventi, risorse usate e stato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="6bd4a-129">**OperationalLogs**: information about what is happening during Event Hubs operations, specifically, the operation type, including event hub creation, resources used, and the status of the operation.</span></span>

## <a name="diagnostic-logs-schema"></a><span data-ttu-id="6bd4a-130">Schema dei log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="6bd4a-130">Diagnostic logs schema</span></span>
<span data-ttu-id="6bd4a-131">Tutti i log vengono archiviati in formato JavaScript Object Notation (JSON).</span><span class="sxs-lookup"><span data-stu-id="6bd4a-131">All logs are stored in JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="6bd4a-132">Ogni voce presenta campi stringa che usano il formato descritto nelle sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="6bd4a-132">Each entry has string fields that use the format described in the following sections.</span></span>

### <a name="archive-logs-schema"></a><span data-ttu-id="6bd4a-133">Schema dei log di archiviazione</span><span class="sxs-lookup"><span data-stu-id="6bd4a-133">Archive logs schema</span></span>

<span data-ttu-id="6bd4a-134">Le stringhe JSON dei log di archiviazione includono gli elementi elencati nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="6bd4a-134">Archive log JSON strings include elements listed in the following table:</span></span>

<span data-ttu-id="6bd4a-135">Nome</span><span class="sxs-lookup"><span data-stu-id="6bd4a-135">Name</span></span> | <span data-ttu-id="6bd4a-136">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6bd4a-136">Description</span></span>
------- | -------
<span data-ttu-id="6bd4a-137">TaskName</span><span class="sxs-lookup"><span data-stu-id="6bd4a-137">TaskName</span></span> | <span data-ttu-id="6bd4a-138">Descrizione dell'attività non riuscita.</span><span class="sxs-lookup"><span data-stu-id="6bd4a-138">Description of the task that failed.</span></span>
<span data-ttu-id="6bd4a-139">ActivityId</span><span class="sxs-lookup"><span data-stu-id="6bd4a-139">ActivityId</span></span> | <span data-ttu-id="6bd4a-140">ID interno, usato a scopo di rilevamento.</span><span class="sxs-lookup"><span data-stu-id="6bd4a-140">Internal ID, used for tracking.</span></span>
<span data-ttu-id="6bd4a-141">trackingId</span><span class="sxs-lookup"><span data-stu-id="6bd4a-141">trackingId</span></span> | <span data-ttu-id="6bd4a-142">ID interno, usato a scopo di rilevamento.</span><span class="sxs-lookup"><span data-stu-id="6bd4a-142">Internal ID, used for tracking.</span></span>
<span data-ttu-id="6bd4a-143">resourceId</span><span class="sxs-lookup"><span data-stu-id="6bd4a-143">resourceId</span></span> | <span data-ttu-id="6bd4a-144">ID della risorsa di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6bd4a-144">Azure Resource Manager resource ID.</span></span>
<span data-ttu-id="6bd4a-145">eventHub</span><span class="sxs-lookup"><span data-stu-id="6bd4a-145">eventHub</span></span> | <span data-ttu-id="6bd4a-146">Nome completo dell'hub eventi, include il nome dello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="6bd4a-146">Event hub full name (includes namespace name).</span></span>
<span data-ttu-id="6bd4a-147">partitionId</span><span class="sxs-lookup"><span data-stu-id="6bd4a-147">partitionId</span></span> | <span data-ttu-id="6bd4a-148">Partizione dell'hub eventi per l'operazione di scrittura.</span><span class="sxs-lookup"><span data-stu-id="6bd4a-148">Event Hub partition being written to.</span></span>
<span data-ttu-id="6bd4a-149">archiveStep</span><span class="sxs-lookup"><span data-stu-id="6bd4a-149">archiveStep</span></span> | <span data-ttu-id="6bd4a-150">ArchiveFlushWriter</span><span class="sxs-lookup"><span data-stu-id="6bd4a-150">ArchiveFlushWriter</span></span>
<span data-ttu-id="6bd4a-151">startTime</span><span class="sxs-lookup"><span data-stu-id="6bd4a-151">startTime</span></span> | <span data-ttu-id="6bd4a-152">Ora di inizio di un errore.</span><span class="sxs-lookup"><span data-stu-id="6bd4a-152">Failure start time.</span></span>
<span data-ttu-id="6bd4a-153">errori</span><span class="sxs-lookup"><span data-stu-id="6bd4a-153">failures</span></span> | <span data-ttu-id="6bd4a-154">Numero di volte in cui si è verificato un errore.</span><span class="sxs-lookup"><span data-stu-id="6bd4a-154">Number of times failure occurred.</span></span>
<span data-ttu-id="6bd4a-155">durationInSeconds</span><span class="sxs-lookup"><span data-stu-id="6bd4a-155">durationInSeconds</span></span> | <span data-ttu-id="6bd4a-156">Durata dell'errore.</span><span class="sxs-lookup"><span data-stu-id="6bd4a-156">Duration of failure.</span></span>
<span data-ttu-id="6bd4a-157">Message</span><span class="sxs-lookup"><span data-stu-id="6bd4a-157">message</span></span> | <span data-ttu-id="6bd4a-158">Messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="6bd4a-158">Error message.</span></span>
<span data-ttu-id="6bd4a-159">category</span><span class="sxs-lookup"><span data-stu-id="6bd4a-159">category</span></span> | <span data-ttu-id="6bd4a-160">ArchiveLogs</span><span class="sxs-lookup"><span data-stu-id="6bd4a-160">ArchiveLogs</span></span>

<span data-ttu-id="6bd4a-161">Il codice seguente è un esempio di stringa JSON di log di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="6bd4a-161">The following code is an example of an archive log JSON string:</span></span>

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
     "message": "Microsoft.WindowsAzure.Storage.StorageException: The remote server returned an error: (404) Not Found. ---> System.Net.WebException: The remote server returned an error: (404) Not Found.\r\n   at Microsoft.WindowsAzure.Storage.Shared.Protocol.HttpResponseParsers.ProcessExpectedStatusCodeNoException[T](HttpStatusCode expectedStatusCode, HttpStatusCode actualStatusCode, T retVal, StorageCommandBase`1 cmd, Exception ex)\r\n   at Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob.<PutBlockImpl>b__3e(RESTCommand`1 cmd, HttpWebResponse resp, Exception ex, OperationContext ctx)\r\n   at Microsoft.WindowsAzure.Storage.Core.Executor.Executor.EndGetResponse[T](IAsyncResult getResponseResult)\r\n   --- End of inner exception stack trace ---\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.StorageAsyncResult`1.End()\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.AsyncExtensions.<>c__DisplayClass4.<CreateCallbackVoid>b__3(IAsyncResult ar)\r\n--- End of stack trace from previous location where exception was thrown ---\r\n   at System.",
     "category": "ArchiveLogs"
}
```

### <a name="operational-logs-schema"></a><span data-ttu-id="6bd4a-162">Schema di log operativi</span><span class="sxs-lookup"><span data-stu-id="6bd4a-162">Operational logs schema</span></span>

<span data-ttu-id="6bd4a-163">Le stringhe JSON dei log operativi includono gli elementi elencati nella seguente tabella:</span><span class="sxs-lookup"><span data-stu-id="6bd4a-163">Operational log JSON strings include elements listed in the following table:</span></span>

<span data-ttu-id="6bd4a-164">Nome</span><span class="sxs-lookup"><span data-stu-id="6bd4a-164">Name</span></span> | <span data-ttu-id="6bd4a-165">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6bd4a-165">Description</span></span>
------- | -------
<span data-ttu-id="6bd4a-166">ActivityId</span><span class="sxs-lookup"><span data-stu-id="6bd4a-166">ActivityId</span></span> | <span data-ttu-id="6bd4a-167">ID interno, usato a scopo di rilevamento.</span><span class="sxs-lookup"><span data-stu-id="6bd4a-167">Internal ID, used to track purpose.</span></span>
<span data-ttu-id="6bd4a-168">EventName</span><span class="sxs-lookup"><span data-stu-id="6bd4a-168">EventName</span></span> | <span data-ttu-id="6bd4a-169">Nome operazione.</span><span class="sxs-lookup"><span data-stu-id="6bd4a-169">Operation name.</span></span>  
<span data-ttu-id="6bd4a-170">resourceId</span><span class="sxs-lookup"><span data-stu-id="6bd4a-170">resourceId</span></span> | <span data-ttu-id="6bd4a-171">ID della risorsa di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6bd4a-171">Azure Resource Manager resource ID.</span></span>
<span data-ttu-id="6bd4a-172">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="6bd4a-172">SubscriptionId</span></span> | <span data-ttu-id="6bd4a-173">l'ID sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="6bd4a-173">Subscription ID.</span></span>
<span data-ttu-id="6bd4a-174">EventTimeString</span><span class="sxs-lookup"><span data-stu-id="6bd4a-174">EventTimeString</span></span> | <span data-ttu-id="6bd4a-175">Durata dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="6bd4a-175">Operation time.</span></span>
<span data-ttu-id="6bd4a-176">EventProperties</span><span class="sxs-lookup"><span data-stu-id="6bd4a-176">EventProperties</span></span> | <span data-ttu-id="6bd4a-177">Proprietà dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="6bd4a-177">Operation properties.</span></span>
<span data-ttu-id="6bd4a-178">Status</span><span class="sxs-lookup"><span data-stu-id="6bd4a-178">Status</span></span> | <span data-ttu-id="6bd4a-179">Stato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="6bd4a-179">Operation status.</span></span>
<span data-ttu-id="6bd4a-180">Chiamante</span><span class="sxs-lookup"><span data-stu-id="6bd4a-180">Caller</span></span> | <span data-ttu-id="6bd4a-181">Chiamante dell'operazione (Portale di Azure o client di gestione).</span><span class="sxs-lookup"><span data-stu-id="6bd4a-181">Caller of operation (Azure portal or management client).</span></span>
<span data-ttu-id="6bd4a-182">category</span><span class="sxs-lookup"><span data-stu-id="6bd4a-182">category</span></span> | <span data-ttu-id="6bd4a-183">OperationalLogs</span><span class="sxs-lookup"><span data-stu-id="6bd4a-183">OperationalLogs</span></span>

<span data-ttu-id="6bd4a-184">Il codice seguente è un esempio di stringa JSON di log operativo:</span><span class="sxs-lookup"><span data-stu-id="6bd4a-184">The following code is an example of an operational log JSON string:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="6bd4a-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6bd4a-185">Next steps</span></span>
* [<span data-ttu-id="6bd4a-186">Introduzione a Hub eventi</span><span class="sxs-lookup"><span data-stu-id="6bd4a-186">Introduction to Event Hubs</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="6bd4a-187">Panoramica dell'API di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="6bd4a-187">Event Hubs API overview</span></span>](event-hubs-api-overview.md)
* [<span data-ttu-id="6bd4a-188">Introduzione all'Hub eventi</span><span class="sxs-lookup"><span data-stu-id="6bd4a-188">Get started with Event Hubs</span></span>](event-hubs-csharp-ephcs-getstarted.md)
