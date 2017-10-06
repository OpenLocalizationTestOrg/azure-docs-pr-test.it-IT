---
title: log di diagnostica del Bus di servizio aaaAzure | Documenti Microsoft
description: Informazioni su come tooset backup log di diagnostica per il Bus di servizio in Azure.
keywords: 
documentationcenter: .net
services: service-bus-messaging
author: banisadr
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: babanisa;sethm
ms.openlocfilehash: e48d6eaba6e865ae39f5b07ed6cd53d74c92e2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-diagnostic-logs"></a><span data-ttu-id="67c80-103">Log di diagnostica del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="67c80-103">Service Bus diagnostic logs</span></span>

<span data-ttu-id="67c80-104">È possibile visualizzare due tipi di log per il bus di servizio di Azure:</span><span class="sxs-lookup"><span data-stu-id="67c80-104">You can view two types of logs for Azure Service Bus:</span></span>
* <span data-ttu-id="67c80-105">**[Log attività](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="67c80-105">**[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span></span> <span data-ttu-id="67c80-106">Questi log contengono informazioni sulle operazioni eseguite in un processo.</span><span class="sxs-lookup"><span data-stu-id="67c80-106">These logs contain information about operations performed on a job.</span></span> <span data-ttu-id="67c80-107">registri Hello sono sempre abilitati.</span><span class="sxs-lookup"><span data-stu-id="67c80-107">hello logs are always enabled.</span></span>
* <span data-ttu-id="67c80-108">**[Log di diagnostica](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="67c80-108">**[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span></span> <span data-ttu-id="67c80-109">È possibile configurare i log di diagnostica per informazioni più complete su tutto ciò che accade in un processo.</span><span class="sxs-lookup"><span data-stu-id="67c80-109">You can configure diagnostic logs for richer information about everything that happens within a job.</span></span> <span data-ttu-id="67c80-110">Le attività di copertura di log di diagnostica da ora hello hello processo viene creato fino a quando non viene eliminato il processo di hello, inclusi gli aggiornamenti e le attività che si verificano durante l'esecuzione del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="67c80-110">Diagnostic logs cover activities from hello time hello job is created until hello job is deleted, including updates and activities that occur while hello job is running.</span></span>

## <a name="turn-on-diagnostic-logs"></a><span data-ttu-id="67c80-111">Attivare i log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="67c80-111">Turn on diagnostic logs</span></span>

<span data-ttu-id="67c80-112">I log di diagnostica sono disabilitati per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="67c80-112">Diagnostics logs are disabled by default.</span></span> <span data-ttu-id="67c80-113">i log di diagnostica tooenable, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="67c80-113">tooenable diagnostic logs, perform hello following steps:</span></span>

1.  <span data-ttu-id="67c80-114">In hello [portale di Azure](https://portal.azure.com)in **monitoraggio + gestione**, fare clic su **log di diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="67c80-114">In hello [Azure portal](https://portal.azure.com), under **Monitoring + Management**, click **Diagnostics logs**.</span></span>

    ![pannello navigazione toodiagnostic log](./media/service-bus-diagnostic-logs/image1.png)

2. <span data-ttu-id="67c80-116">Fare clic sulla risorsa hello da toomonitor.</span><span class="sxs-lookup"><span data-stu-id="67c80-116">Click hello resource you want toomonitor.</span></span>  

3.  <span data-ttu-id="67c80-117">Fare clic su **Attiva diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="67c80-117">Click **Turn on diagnostics**.</span></span>

    ![attivazione dei log di diagnostica](./media/service-bus-diagnostic-logs/image2.png)

4.  <span data-ttu-id="67c80-119">Per **Stato** fare clic su **Attivato**.</span><span class="sxs-lookup"><span data-stu-id="67c80-119">For **Status**, click **On**.</span></span>

    ![modifica dello stato dei log di diagnostica](./media/service-bus-diagnostic-logs/image3.png)

5.  <span data-ttu-id="67c80-121">Destinazione di archiviazione hello set che si desidera. ad esempio, un account di archiviazione, un Hub eventi o Analitica di Log di Azure.</span><span class="sxs-lookup"><span data-stu-id="67c80-121">Set hello archive target that you want; for example, a storage account, an Event Hub, or Azure Log Analytics.</span></span>

6.  <span data-ttu-id="67c80-122">Salvare le impostazioni di diagnostica nuovo hello.</span><span class="sxs-lookup"><span data-stu-id="67c80-122">Save hello new diagnostics settings.</span></span>

<span data-ttu-id="67c80-123">Le nuove impostazioni diventano effettive in circa 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="67c80-123">New settings take effect in about 10 minutes.</span></span> <span data-ttu-id="67c80-124">Successivamente, i log vengono visualizzati nella destinazione di archiviazione configurato hello, su hello **log di diagnostica** blade.</span><span class="sxs-lookup"><span data-stu-id="67c80-124">After that, logs appear in hello configured archival target, on hello **Diagnostics logs** blade.</span></span>

<span data-ttu-id="67c80-125">Per ulteriori informazioni sulla configurazione di diagnostica, vedere hello [panoramica dei log di diagnostica Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="67c80-125">For more information about configuring diagnostics, see hello [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="diagnostic-logs-schema"></a><span data-ttu-id="67c80-126">Schema dei log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="67c80-126">Diagnostic logs schema</span></span>

<span data-ttu-id="67c80-127">Tutti i log vengono archiviati in formato JavaScript Object Notation (JSON).</span><span class="sxs-lookup"><span data-stu-id="67c80-127">All logs are stored in JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="67c80-128">Ogni voce include i campi stringa di formato hello descritti nella seguente sezione hello.</span><span class="sxs-lookup"><span data-stu-id="67c80-128">Each entry has string fields that use hello format described in hello following section.</span></span>

## <a name="operational-logs-schema"></a><span data-ttu-id="67c80-129">Schema di log operativi</span><span class="sxs-lookup"><span data-stu-id="67c80-129">Operational logs schema</span></span>

<span data-ttu-id="67c80-130">Registra in hello **OperationalLogs** categoria acquisire cosa accade durante operazioni del Bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="67c80-130">Logs in hello **OperationalLogs** category capture what happens during Service Bus operations.</span></span> <span data-ttu-id="67c80-131">In particolare, tali registri acquisire il tipo di operazione hello, inclusa la creazione della coda, le risorse usate e lo stato dell'operazione hello hello.</span><span class="sxs-lookup"><span data-stu-id="67c80-131">Specifically, these logs capture hello operation type, including queue creation, resources used, and hello status of hello operation.</span></span>

<span data-ttu-id="67c80-132">Le stringhe JSON registro operativo includono gli elementi elencati in hello nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="67c80-132">Operational log JSON strings include elements listed in hello following table:</span></span>

<span data-ttu-id="67c80-133">Nome</span><span class="sxs-lookup"><span data-stu-id="67c80-133">Name</span></span> | <span data-ttu-id="67c80-134">Descrizione</span><span class="sxs-lookup"><span data-stu-id="67c80-134">Description</span></span>
------- | -------
<span data-ttu-id="67c80-135">ActivityId</span><span class="sxs-lookup"><span data-stu-id="67c80-135">ActivityId</span></span> | <span data-ttu-id="67c80-136">ID interno, usato a scopo di rilevamento</span><span class="sxs-lookup"><span data-stu-id="67c80-136">Internal ID, used for tracking</span></span>
<span data-ttu-id="67c80-137">EventName</span><span class="sxs-lookup"><span data-stu-id="67c80-137">EventName</span></span> | <span data-ttu-id="67c80-138">Nome operazione</span><span class="sxs-lookup"><span data-stu-id="67c80-138">Operation name</span></span>           
<span data-ttu-id="67c80-139">resourceId</span><span class="sxs-lookup"><span data-stu-id="67c80-139">resourceId</span></span> | <span data-ttu-id="67c80-140">ID della risorsa Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="67c80-140">Azure Resource Manager resource ID</span></span>
<span data-ttu-id="67c80-141">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="67c80-141">SubscriptionId</span></span> | <span data-ttu-id="67c80-142">ID sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="67c80-142">Subscription ID</span></span>
<span data-ttu-id="67c80-143">EventTimeString</span><span class="sxs-lookup"><span data-stu-id="67c80-143">EventTimeString</span></span> | <span data-ttu-id="67c80-144">Durata dell'operazione</span><span class="sxs-lookup"><span data-stu-id="67c80-144">Operation time</span></span>
<span data-ttu-id="67c80-145">EventProperties</span><span class="sxs-lookup"><span data-stu-id="67c80-145">EventProperties</span></span> | <span data-ttu-id="67c80-146">Proprietà dell'operazione</span><span class="sxs-lookup"><span data-stu-id="67c80-146">Operation properties</span></span>
<span data-ttu-id="67c80-147">Status</span><span class="sxs-lookup"><span data-stu-id="67c80-147">Status</span></span> | <span data-ttu-id="67c80-148">Stato dell'operazione</span><span class="sxs-lookup"><span data-stu-id="67c80-148">Operation status</span></span>
<span data-ttu-id="67c80-149">Chiamante</span><span class="sxs-lookup"><span data-stu-id="67c80-149">Caller</span></span> | <span data-ttu-id="67c80-150">Chiamante dell'operazione (Portale di Azure o client di gestione)</span><span class="sxs-lookup"><span data-stu-id="67c80-150">Caller of operation (Azure portal or management client)</span></span>
<span data-ttu-id="67c80-151">category</span><span class="sxs-lookup"><span data-stu-id="67c80-151">category</span></span> | <span data-ttu-id="67c80-152">OperationalLogs</span><span class="sxs-lookup"><span data-stu-id="67c80-152">OperationalLogs</span></span>

<span data-ttu-id="67c80-153">Di seguito è riportato un esempio di stringa JSON di log operativo:</span><span class="sxs-lookup"><span data-stu-id="67c80-153">Here's an example of an operational log JSON string:</span></span>

```json
{
  "ActivityId": "6aa994ac-b56e-4292-8448-0767a5657cc7",
  "EventName": "Create Queue",
  "resourceId": "/SUBSCRIPTIONS/1A2109E3-9DA0-455B-B937-E35E36C1163C/RESOURCEGROUPS/DEFAULT-SERVICEBUS-CENTRALUS/PROVIDERS/MICROSOFT.SERVICEBUS/NAMESPACES/SHOEBOXEHNS-CY4001",
  "SubscriptionId": "1a2109e3-9da0-455b-b937-e35e36c1163c",
  "EventTimeString": "9/28/2016 8:40:06 PM +00:00",
  "EventProperties": "{\"SubscriptionId\":\"1a2109e3-9da0-455b-b937-e35e36c1163c\",\"Namespace\":\"shoeboxehns-cy4001\",\"Via\":\"https://shoeboxehns-cy4001.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",
  "Status": "Succeeded",
  "Caller": "ServiceBus Client",
  "category": "OperationalLogs"
}
```

## <a name="next-steps"></a><span data-ttu-id="67c80-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="67c80-154">Next steps</span></span>

<span data-ttu-id="67c80-155">Visitare hello toolearn collegamenti più sul Bus di servizio seguente:</span><span class="sxs-lookup"><span data-stu-id="67c80-155">Visit hello following links toolearn more about Service Bus:</span></span>

* [<span data-ttu-id="67c80-156">Introduzione tooService Bus</span><span class="sxs-lookup"><span data-stu-id="67c80-156">Introduction tooService Bus</span></span>](service-bus-messaging-overview.md)
* [<span data-ttu-id="67c80-157">Introduzione al bus di servizio</span><span class="sxs-lookup"><span data-stu-id="67c80-157">Get started with Service Bus</span></span>](service-bus-dotnet-get-started-with-queues.md)
