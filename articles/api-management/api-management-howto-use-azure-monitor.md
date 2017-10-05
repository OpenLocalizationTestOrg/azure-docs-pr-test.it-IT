---
title: Monitorare Gestione API con Monitoraggio di Azure | Microsoft Docs
description: Informazioni su come monitorare il servizio Gestione API di Azure usando Monitoraggio di Azure.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2fa193cd-ea71-4b33-a5ca-1f55e5351e23
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 0f64947755c79739bb6f15325929bd074cfd7210
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-api-management-with-azure-monitor"></a><span data-ttu-id="67762-103">Monitorare Gestione API con Monitoraggio di Azure</span><span class="sxs-lookup"><span data-stu-id="67762-103">Monitor API Management with Azure Monitor</span></span>
<span data-ttu-id="67762-104">Monitoraggio di Azure è un servizio di Azure che offre un'unica origine per il monitoraggio di tutte le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="67762-104">Azure Monitor is an Azure service that provides a single source for monitoring all your Azure resources.</span></span> <span data-ttu-id="67762-105">Con Monitoraggio di Azure è possibile visualizzare, eseguire query, indirizzare, archiviare ed effettuare operazioni sulle metriche e sui log provenienti dalle risorse di Azure, tra cui Gestione API.</span><span class="sxs-lookup"><span data-stu-id="67762-105">With Azure Monitor, you can visualize, query, route, archive, and take actions on the metrics and logs coming from Azure resources such as API Management.</span></span> 

<span data-ttu-id="67762-106">Il video seguente illustra come monitorare Gestione API usando Monitoraggio di Azure.</span><span class="sxs-lookup"><span data-stu-id="67762-106">The following video shows how to monitor API Management using Azure Monitor.</span></span> <span data-ttu-id="67762-107">Per altre informazioni su Monitoraggio di Azure, vedere l'[introduzione a Monitoraggio di Azure].</span><span class="sxs-lookup"><span data-stu-id="67762-107">For more information about Azure Monitor, see [Get Started with Azure Monitor].</span></span> 


> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Monitor-API-Management-with-Azure-Monitor/player]
>
>
 
## <a name="metrics"></a><span data-ttu-id="67762-108">Metrica</span><span class="sxs-lookup"><span data-stu-id="67762-108">Metrics</span></span>
<span data-ttu-id="67762-109">Gestione API attualmente genera cinque metriche e si prevede di aggiungerne altre in futuro.</span><span class="sxs-lookup"><span data-stu-id="67762-109">API Management currently emits five metrics and we plan to add more in the future.</span></span> <span data-ttu-id="67762-110">Le metriche vengono generate ogni minuto in modo da ottenere una visibilità quasi in tempo reale dello stato e dell'integrità delle API.</span><span class="sxs-lookup"><span data-stu-id="67762-110">These metrics are emitted every minute, giving you near real-time visibility into the state and health of your APIs.</span></span> <span data-ttu-id="67762-111">Di seguito è riportato un riepilogo delle metriche:</span><span class="sxs-lookup"><span data-stu-id="67762-111">Following is a summary of the metrics:</span></span>
* <span data-ttu-id="67762-112">Totale richieste gateway: numero di richieste di API nel periodo.</span><span class="sxs-lookup"><span data-stu-id="67762-112">Total Gateway Requests: the number of API requests in the period.</span></span> 
* <span data-ttu-id="67762-113">Richieste gateway riuscite: numero di richieste di API che hanno ricevuto codici di risposta HTTP corretta, tra cui 304, 307 e qualsiasi valore inferiore a 301, ad esempio, 200.</span><span class="sxs-lookup"><span data-stu-id="67762-113">Successful Gateway Requests: the number of API requests that received successful HTTP response codes including 304, 307 and anything smaller than 301 (for example, 200).</span></span> 
* <span data-ttu-id="67762-114">Richieste gateway non riuscite: numero di richieste di API che hanno ricevuto codici di risposta HTTP errata, tra cui 400 e qualsiasi valore superiore a 500.</span><span class="sxs-lookup"><span data-stu-id="67762-114">Failed Gateway Requests: the number of API requests that received erroneous HTTP response codes including 400 and anything larger than 500.</span></span>
* <span data-ttu-id="67762-115">Richieste gateway non autorizzate: numero di richieste di API che hanno ricevuto codici di risposta HTTP tra cui 401, 403 e 429.</span><span class="sxs-lookup"><span data-stu-id="67762-115">Unauthorized Gateway Requests: the number of API requests that received HTTP response codes including 401, 403, and 429.</span></span> 
* <span data-ttu-id="67762-116">Altre richieste gateway: numero di richieste di API che hanno ricevuto codici di risposta HTTP che non appartengono a una delle categorie precedenti, ad esempio, 418.</span><span class="sxs-lookup"><span data-stu-id="67762-116">Other Gateway Requests: the number of API requests that received HTTP response codes that do not belong to any of the preceding categories (for example, 418).</span></span>

<span data-ttu-id="67762-117">È possibile accedere alle metriche del servizio Gestione API o alle metriche di tutte le risorse di Azure in Monitoraggio di Azure.</span><span class="sxs-lookup"><span data-stu-id="67762-117">You can access metrics in your API Management service, or access metrics of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="67762-118">Per visualizzare le metriche del servizio Gestione API:</span><span class="sxs-lookup"><span data-stu-id="67762-118">To view metrics in your API Management service:</span></span>
1. <span data-ttu-id="67762-119">Aprire il Portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="67762-119">Open the Azure portal.</span></span>
2. <span data-ttu-id="67762-120">Accedere al servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="67762-120">Go to your API Management service.</span></span>
3. <span data-ttu-id="67762-121">Fare clic su **Metrica**.</span><span class="sxs-lookup"><span data-stu-id="67762-121">Click **Metrics**.</span></span>

![Pannello delle metriche][metrics-blade]

<span data-ttu-id="67762-123">Per altre informazioni sull'uso delle metriche, vedere [Panoramica delle metriche].</span><span class="sxs-lookup"><span data-stu-id="67762-123">For more information about how to use Metrics, see [Overview of Metrics].</span></span>

## <a name="activity-logs"></a><span data-ttu-id="67762-124">Log attività</span><span class="sxs-lookup"><span data-stu-id="67762-124">Activity Logs</span></span>
<span data-ttu-id="67762-125">I log attività offrono informazioni dettagliate sulle operazioni eseguite nei servizi Gestione API.</span><span class="sxs-lookup"><span data-stu-id="67762-125">Activity logs provide insight into the operations that were performed on your API Management services.</span></span> <span data-ttu-id="67762-126">In precedenza erano noti come "log di controllo" o "log operativi".</span><span class="sxs-lookup"><span data-stu-id="67762-126">It was previously known as "audit logs" or "operational logs".</span></span> <span data-ttu-id="67762-127">L'uso del log attività consente di acquisire informazioni dettagliate su qualsiasi operazione di scrittura (PUT, POST, DELETE) eseguita sui servizi Gestione API.</span><span class="sxs-lookup"><span data-stu-id="67762-127">Using activity logs, you can determine the "what, who, and when" for any write operations (PUT, POST, DELETE) taken on your API Management services.</span></span> 

> [!NOTE]
> <span data-ttu-id="67762-128">I log attività non includono le operazioni di lettura (GET) né le operazioni eseguite nel portale di pubblicazione classico o usando le API di gestione originali.</span><span class="sxs-lookup"><span data-stu-id="67762-128">Activity logs do not include read (GET) operations or operations performed in the classic Publisher Portal or using the original Management APIs.</span></span>

<span data-ttu-id="67762-129">È possibile accedere ai log attività del servizio Gestione API o ai log di tutte le risorse di Azure in Monitoraggio di Azure.</span><span class="sxs-lookup"><span data-stu-id="67762-129">You can access activity logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="67762-130">Per visualizzare i log attività del servizio Gestione API:</span><span class="sxs-lookup"><span data-stu-id="67762-130">To view activity logs in your API Management service:</span></span>
1. <span data-ttu-id="67762-131">Aprire il Portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="67762-131">Open the Azure portal.</span></span>
2. <span data-ttu-id="67762-132">Accedere al servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="67762-132">Go to your API Management service.</span></span>
3. <span data-ttu-id="67762-133">Fare clic su **Log attività**.</span><span class="sxs-lookup"><span data-stu-id="67762-133">Click **Activity log**.</span></span>

![Pannello dei log attività][activity-logs-blade]

<span data-ttu-id="67762-135">Per altre informazioni sull'uso dei log attività, vedere [Panoramica del log attività di Azure].</span><span class="sxs-lookup"><span data-stu-id="67762-135">For more information about how to use Metrics, see [Overview of Activity Logs].</span></span>

## <a name="alerts"></a><span data-ttu-id="67762-136">Avvisi</span><span class="sxs-lookup"><span data-stu-id="67762-136">Alerts</span></span>
<span data-ttu-id="67762-137">È possibile configurare un avviso basato sulle metriche e sui log attività.</span><span class="sxs-lookup"><span data-stu-id="67762-137">You can configure to receive alerts based on metrics and activity logs.</span></span> <span data-ttu-id="67762-138">Monitoraggio di Azure consente di configurare un avviso in modo che, se attivato, esegua queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="67762-138">Azure Monitor allows you to configure an alert to do the following when it triggers:</span></span>

* <span data-ttu-id="67762-139">Inviare una notifica via posta elettronica</span><span class="sxs-lookup"><span data-stu-id="67762-139">Send an email notification</span></span>
* <span data-ttu-id="67762-140">Chiamare un webhook</span><span class="sxs-lookup"><span data-stu-id="67762-140">Call a webhook</span></span>
* <span data-ttu-id="67762-141">Richiamare un'app per la logica di Azure</span><span class="sxs-lookup"><span data-stu-id="67762-141">Invoke an Azure Logic App</span></span>

<span data-ttu-id="67762-142">È possibile configurare regole per gli avvisi nel servizio Gestione API o in Monitoraggio di Azure.</span><span class="sxs-lookup"><span data-stu-id="67762-142">You can configure alert rules in your API Management service, or in Azure Monitor.</span></span> <span data-ttu-id="67762-143">Per configurarle in Gestione API:</span><span class="sxs-lookup"><span data-stu-id="67762-143">To configure them in API Management:</span></span> 
1. <span data-ttu-id="67762-144">Aprire il Portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="67762-144">Open the Azure portal.</span></span>
2. <span data-ttu-id="67762-145">Accedere al servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="67762-145">Go to your API Management service.</span></span>
3. <span data-ttu-id="67762-146">Fare clic su **Regole di avviso**.</span><span class="sxs-lookup"><span data-stu-id="67762-146">Click **Alert rules**.</span></span>

![Pannello Regole di avviso][alert-rules-blade]

<span data-ttu-id="67762-148">Per altre informazioni sull'uso degli avvisi, vedere [Panoramica degli avvisi].</span><span class="sxs-lookup"><span data-stu-id="67762-148">For more information about using Alerts, see [Overview of Alerts].</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="67762-149">Log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="67762-149">Diagnostic Logs</span></span>
<span data-ttu-id="67762-150">I log di diagnostica offrono informazioni dettagliate sulle operazioni e gli errori importanti per il controllo e per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="67762-150">Diagnostic logs provide rich information about operations and errors that are important for auditing as well as troubleshooting purposes.</span></span> <span data-ttu-id="67762-151">I log di diagnostica differiscono dai log attività.</span><span class="sxs-lookup"><span data-stu-id="67762-151">Diagnostics logs differ from activity logs.</span></span> <span data-ttu-id="67762-152">I log attività offrono informazioni approfondite sulle operazioni eseguite nelle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="67762-152">Activity logs provide insights into the operations that were performed on your Azure resources.</span></span> <span data-ttu-id="67762-153">I log di diagnostica forniscono informazioni approfondite sulle operazioni che la risorsa esegue automaticamente.</span><span class="sxs-lookup"><span data-stu-id="67762-153">Diagnostics logs provide insight into operations that your resource performed itself.</span></span>

<span data-ttu-id="67762-154">Attualmente Gestione API offre ogni ora log di diagnostica in batch sulla singola richiesta API con ogni voce con la struttura seguente:</span><span class="sxs-lookup"><span data-stu-id="67762-154">API Management currently provides diagnostics logs (batched hourly) about individual API request with each entry having the following structure:</span></span>

```
{
    "Tenant": "",
      "DeploymentName": "",
      "time": "",
      "resourceId": "",
      "category": "GatewayLogs",
      "operationName": "Microsoft.ApiManagement/GatewayLogs",
      "durationMs": ,
      "Level": ,
      "properties": "{
          "ApiId": "",
          "OperationId": "",
          "ProductId": "",
          "SubscriptionId": "",
          "Method": "",
          "Url": "",
          "RequestSize": ,
          "ServiceTime": "",
          "BackendMethod": "",
          "BackendUrl": "",
          "BackendResponseCode": ,
          "ResponseCode": ,
          "ResponseSize": ,
          "Cache": "",
          "UserId"
      }"
 }
```

<span data-ttu-id="67762-155">È possibile accedere ai log di diagnostica del servizio Gestione API o ai log di tutte le risorse di Azure in Monitoraggio di Azure.</span><span class="sxs-lookup"><span data-stu-id="67762-155">You can access diagnostic logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="67762-156">Per visualizzare i log di diagnostica del servizio Gestione API:</span><span class="sxs-lookup"><span data-stu-id="67762-156">To view diagnostic logs in your API Management service:</span></span>
1. <span data-ttu-id="67762-157">Aprire il Portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="67762-157">Open the Azure portal.</span></span>
2. <span data-ttu-id="67762-158">Accedere al servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="67762-158">Go to your API Management service.</span></span>
3. <span data-ttu-id="67762-159">Fare clic su **Log di diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="67762-159">Click **Diagnostic log**.</span></span>

![Pannello Log di diagnostica][diagnostic-logs-blade]

<span data-ttu-id="67762-161">Per altre informazioni sull'uso dei log di diagnostica, vedere [Raccogliere e usare i dati di diagnostica dalle risorse di Azure].</span><span class="sxs-lookup"><span data-stu-id="67762-161">For more information about how to use Metrics, see [Overview of Diagnostic Logs].</span></span>

## <a name="next-step"></a><span data-ttu-id="67762-162">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="67762-162">Next Step</span></span>

* <span data-ttu-id="67762-163">[introduzione a Monitoraggio di Azure]</span><span class="sxs-lookup"><span data-stu-id="67762-163">[Get Started with Azure Monitor]</span></span>
* <span data-ttu-id="67762-164">[Panoramica delle metriche]</span><span class="sxs-lookup"><span data-stu-id="67762-164">[Overview of Metrics]</span></span>
* <span data-ttu-id="67762-165">[Panoramica del log attività di Azure]</span><span class="sxs-lookup"><span data-stu-id="67762-165">[Overview of Activity Logs]</span></span>
* <span data-ttu-id="67762-166">[Raccogliere e usare i dati di diagnostica dalle risorse di Azure]</span><span class="sxs-lookup"><span data-stu-id="67762-166">[Overview of Diagnostic Logs]</span></span>
* <span data-ttu-id="67762-167">[Panoramica degli avvisi]</span><span class="sxs-lookup"><span data-stu-id="67762-167">[Overview of Alerts]</span></span>

<span data-ttu-id="67762-168">[introduzione a Monitoraggio di Azure]: ../monitoring-and-diagnostics/monitoring-get-started.md</span><span class="sxs-lookup"><span data-stu-id="67762-168">[Get Started with Azure Monitor]: ../monitoring-and-diagnostics/monitoring-get-started.md</span></span>
<span data-ttu-id="67762-169">[Panoramica delle metriche]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md</span><span class="sxs-lookup"><span data-stu-id="67762-169">[Overview of Metrics]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md</span></span>
<span data-ttu-id="67762-170">[Panoramica del log attività di Azure]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md</span><span class="sxs-lookup"><span data-stu-id="67762-170">[Overview of Activity Logs]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md</span></span>
<span data-ttu-id="67762-171">[Raccogliere e usare i dati di diagnostica dalle risorse di Azure]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md</span><span class="sxs-lookup"><span data-stu-id="67762-171">[Overview of Diagnostic Logs]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md</span></span>
<span data-ttu-id="67762-172">[Panoramica degli avvisi]: ../monitoring-and-diagnostics/insights-alerts-portal.md</span><span class="sxs-lookup"><span data-stu-id="67762-172">[Overview of Alerts]: ../monitoring-and-diagnostics/insights-alerts-portal.md</span></span>



[metrics-blade]: ./media/api-management-azure-monitor/api-management-metrics-blade.png
[activity-logs-blade]: ./media/api-management-azure-monitor/api-management-activity-logs-blade.png
[alert-rules-blade]: ./media/api-management-azure-monitor/api-management-alert-rules-blade.png
[diagnostic-logs-blade]: ./media/api-management-azure-monitor/api-management-diagnostic-logs-blade.png
