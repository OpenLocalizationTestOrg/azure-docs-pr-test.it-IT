---
title: Log di diagnostica del bus di servizio di Azure | Microsoft Docs
description: Informazioni su come configurare i log di diagnostica per il bus di servizio in Azure.
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
ms.openlocfilehash: 72e18444c83b84c5191a0aab3dc6983517167dd1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="service-bus-diagnostic-logs"></a><span data-ttu-id="63cc5-103">Log di diagnostica del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="63cc5-103">Service Bus diagnostic logs</span></span>

<span data-ttu-id="63cc5-104">È possibile visualizzare due tipi di log per il bus di servizio di Azure:</span><span class="sxs-lookup"><span data-stu-id="63cc5-104">You can view two types of logs for Azure Service Bus:</span></span>
* <span data-ttu-id="63cc5-105">**[Log attività](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="63cc5-105">**[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span></span> <span data-ttu-id="63cc5-106">Questi log contengono informazioni sulle operazioni eseguite in un processo.</span><span class="sxs-lookup"><span data-stu-id="63cc5-106">These logs contain information about operations performed on a job.</span></span> <span data-ttu-id="63cc5-107">I log sono sempre attivati.</span><span class="sxs-lookup"><span data-stu-id="63cc5-107">The logs are always enabled.</span></span>
* <span data-ttu-id="63cc5-108">**[Log di diagnostica](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="63cc5-108">**[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span></span> <span data-ttu-id="63cc5-109">È possibile configurare i log di diagnostica per informazioni più complete su tutto ciò che accade in un processo.</span><span class="sxs-lookup"><span data-stu-id="63cc5-109">You can configure diagnostic logs for richer information about everything that happens within a job.</span></span> <span data-ttu-id="63cc5-110">I log di diagnostica coprono le attività che si verificano dal momento della creazione del processo fino alla sua eliminazione, inclusi gli aggiornamenti e le attività che si verificano durante l'esecuzione del processo.</span><span class="sxs-lookup"><span data-stu-id="63cc5-110">Diagnostic logs cover activities from the time the job is created until the job is deleted, including updates and activities that occur while the job is running.</span></span>

## <a name="turn-on-diagnostic-logs"></a><span data-ttu-id="63cc5-111">Attivare i log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="63cc5-111">Turn on diagnostic logs</span></span>

<span data-ttu-id="63cc5-112">I log di diagnostica sono disabilitati per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="63cc5-112">Diagnostics logs are disabled by default.</span></span> <span data-ttu-id="63cc5-113">Per abilitare i log di diagnostica, eseguire la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="63cc5-113">To enable diagnostic logs, perform the following steps:</span></span>

1.  <span data-ttu-id="63cc5-114">Nel [portale di Azure](https://portal.azure.com) in **Monitoraggio + Gestione** fare clic su **Log di diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="63cc5-114">In the [Azure portal](https://portal.azure.com), under **Monitoring + Management**, click **Diagnostics logs**.</span></span>

    ![navigazione al pannello dei log di diagnostica](./media/service-bus-diagnostic-logs/image1.png)

2. <span data-ttu-id="63cc5-116">Fare clic sulla risorsa da monitorare.</span><span class="sxs-lookup"><span data-stu-id="63cc5-116">Click the resource you want to monitor.</span></span>  

3.  <span data-ttu-id="63cc5-117">Fare clic su **Attiva diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="63cc5-117">Click **Turn on diagnostics**.</span></span>

    ![attivazione dei log di diagnostica](./media/service-bus-diagnostic-logs/image2.png)

4.  <span data-ttu-id="63cc5-119">Per **Stato** fare clic su **Attivato**.</span><span class="sxs-lookup"><span data-stu-id="63cc5-119">For **Status**, click **On**.</span></span>

    ![modifica dello stato dei log di diagnostica](./media/service-bus-diagnostic-logs/image3.png)

5.  <span data-ttu-id="63cc5-121">Impostare la destinazione di archiviazione desiderata, ad esempio un account di archiviazione, un hub eventi o Azure Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="63cc5-121">Set the archive target that you want; for example, a storage account, an Event Hub, or Azure Log Analytics.</span></span>

6.  <span data-ttu-id="63cc5-122">Salvare le nuove impostazioni di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="63cc5-122">Save the new diagnostics settings.</span></span>

<span data-ttu-id="63cc5-123">Le nuove impostazioni diventano effettive in circa 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="63cc5-123">New settings take effect in about 10 minutes.</span></span> <span data-ttu-id="63cc5-124">Trascorso questo tempo, i log vengono visualizzati nella destinazione di archiviazione configurata, all'interno del pannello **Log di diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="63cc5-124">After that, logs appear in the configured archival target, on the **Diagnostics logs** blade.</span></span>

<span data-ttu-id="63cc5-125">Per altre informazioni sulla configurazione della diagnostica, vedere la [panoramica dei log di diagnostica di Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="63cc5-125">For more information about configuring diagnostics, see the [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="diagnostic-logs-schema"></a><span data-ttu-id="63cc5-126">Schema dei log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="63cc5-126">Diagnostic logs schema</span></span>

<span data-ttu-id="63cc5-127">Tutti i log vengono archiviati in formato JavaScript Object Notation (JSON).</span><span class="sxs-lookup"><span data-stu-id="63cc5-127">All logs are stored in JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="63cc5-128">Ogni voce presenta campi stringa che usano il formato descritto nella sezione seguente.</span><span class="sxs-lookup"><span data-stu-id="63cc5-128">Each entry has string fields that use the format described in the following section.</span></span>

## <a name="operational-logs-schema"></a><span data-ttu-id="63cc5-129">Schema di log operativi</span><span class="sxs-lookup"><span data-stu-id="63cc5-129">Operational logs schema</span></span>

<span data-ttu-id="63cc5-130">I log nella categoria **OperationalLogs** acquisiscono i dati relativi al funzionamento del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="63cc5-130">Logs in the **OperationalLogs** category capture what happens during Service Bus operations.</span></span> <span data-ttu-id="63cc5-131">In particolare, questi log acquisiscono il tipo di operazione, tra cui la creazione delle code, le risorse usate e lo stato dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="63cc5-131">Specifically, these logs capture the operation type, including queue creation, resources used, and the status of the operation.</span></span>

<span data-ttu-id="63cc5-132">Le stringhe JSON dei log operativi includono gli elementi elencati nella seguente tabella:</span><span class="sxs-lookup"><span data-stu-id="63cc5-132">Operational log JSON strings include elements listed in the following table:</span></span>

<span data-ttu-id="63cc5-133">Nome</span><span class="sxs-lookup"><span data-stu-id="63cc5-133">Name</span></span> | <span data-ttu-id="63cc5-134">Descrizione</span><span class="sxs-lookup"><span data-stu-id="63cc5-134">Description</span></span>
------- | -------
<span data-ttu-id="63cc5-135">ActivityId</span><span class="sxs-lookup"><span data-stu-id="63cc5-135">ActivityId</span></span> | <span data-ttu-id="63cc5-136">ID interno, usato a scopo di rilevamento</span><span class="sxs-lookup"><span data-stu-id="63cc5-136">Internal ID, used for tracking</span></span>
<span data-ttu-id="63cc5-137">EventName</span><span class="sxs-lookup"><span data-stu-id="63cc5-137">EventName</span></span> | <span data-ttu-id="63cc5-138">Nome operazione</span><span class="sxs-lookup"><span data-stu-id="63cc5-138">Operation name</span></span>           
<span data-ttu-id="63cc5-139">resourceId</span><span class="sxs-lookup"><span data-stu-id="63cc5-139">resourceId</span></span> | <span data-ttu-id="63cc5-140">ID della risorsa Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="63cc5-140">Azure Resource Manager resource ID</span></span>
<span data-ttu-id="63cc5-141">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="63cc5-141">SubscriptionId</span></span> | <span data-ttu-id="63cc5-142">ID sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="63cc5-142">Subscription ID</span></span>
<span data-ttu-id="63cc5-143">EventTimeString</span><span class="sxs-lookup"><span data-stu-id="63cc5-143">EventTimeString</span></span> | <span data-ttu-id="63cc5-144">Durata dell'operazione</span><span class="sxs-lookup"><span data-stu-id="63cc5-144">Operation time</span></span>
<span data-ttu-id="63cc5-145">EventProperties</span><span class="sxs-lookup"><span data-stu-id="63cc5-145">EventProperties</span></span> | <span data-ttu-id="63cc5-146">Proprietà dell'operazione</span><span class="sxs-lookup"><span data-stu-id="63cc5-146">Operation properties</span></span>
<span data-ttu-id="63cc5-147">Status</span><span class="sxs-lookup"><span data-stu-id="63cc5-147">Status</span></span> | <span data-ttu-id="63cc5-148">Stato dell'operazione</span><span class="sxs-lookup"><span data-stu-id="63cc5-148">Operation status</span></span>
<span data-ttu-id="63cc5-149">Chiamante</span><span class="sxs-lookup"><span data-stu-id="63cc5-149">Caller</span></span> | <span data-ttu-id="63cc5-150">Chiamante dell'operazione (Portale di Azure o client di gestione)</span><span class="sxs-lookup"><span data-stu-id="63cc5-150">Caller of operation (Azure portal or management client)</span></span>
<span data-ttu-id="63cc5-151">category</span><span class="sxs-lookup"><span data-stu-id="63cc5-151">category</span></span> | <span data-ttu-id="63cc5-152">OperationalLogs</span><span class="sxs-lookup"><span data-stu-id="63cc5-152">OperationalLogs</span></span>

<span data-ttu-id="63cc5-153">Di seguito è riportato un esempio di stringa JSON di log operativo:</span><span class="sxs-lookup"><span data-stu-id="63cc5-153">Here's an example of an operational log JSON string:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="63cc5-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="63cc5-154">Next steps</span></span>

<span data-ttu-id="63cc5-155">Visitare i collegamenti seguenti per altre informazioni sul bus di servizio:</span><span class="sxs-lookup"><span data-stu-id="63cc5-155">Visit the following links to learn more about Service Bus:</span></span>

* [<span data-ttu-id="63cc5-156">Introduzione al bus di servizio</span><span class="sxs-lookup"><span data-stu-id="63cc5-156">Introduction to Service Bus</span></span>](service-bus-messaging-overview.md)
* [<span data-ttu-id="63cc5-157">Introduzione al bus di servizio</span><span class="sxs-lookup"><span data-stu-id="63cc5-157">Get started with Service Bus</span></span>](service-bus-dotnet-get-started-with-queues.md)
