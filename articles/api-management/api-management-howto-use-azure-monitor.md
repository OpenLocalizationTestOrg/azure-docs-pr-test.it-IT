---
title: API di gestione con Azure Monitor aaaMonitor | Documenti Microsoft
description: Informazioni su come toomonitor gestione API di Azure del servizio tramite il monitoraggio di Azure.
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
ms.openlocfilehash: 5012d8ed57ea4f94ea6bc1b7c4e1102516ec4414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-api-management-with-azure-monitor"></a><span data-ttu-id="9fca5-103">Monitorare Gestione API con Monitoraggio di Azure</span><span class="sxs-lookup"><span data-stu-id="9fca5-103">Monitor API Management with Azure Monitor</span></span>
<span data-ttu-id="9fca5-104">Monitoraggio di Azure è un servizio di Azure che offre un'unica origine per il monitoraggio di tutte le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="9fca5-104">Azure Monitor is an Azure service that provides a single source for monitoring all your Azure resources.</span></span> <span data-ttu-id="9fca5-105">Con Monitor di Azure, è possibile visualizzare, richiedere, route, archiviare e intraprendere azioni metriche hello e log provenienti dalle risorse di Azure, ad esempio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="9fca5-105">With Azure Monitor, you can visualize, query, route, archive, and take actions on hello metrics and logs coming from Azure resources such as API Management.</span></span> 

<span data-ttu-id="9fca5-106">Hello seguente video viene illustrato come toomonitor gestione API tramite il monitoraggio di Azure.</span><span class="sxs-lookup"><span data-stu-id="9fca5-106">hello following video shows how toomonitor API Management using Azure Monitor.</span></span> <span data-ttu-id="9fca5-107">Per altre informazioni su Monitoraggio di Azure, vedere l'[introduzione a Monitoraggio di Azure].</span><span class="sxs-lookup"><span data-stu-id="9fca5-107">For more information about Azure Monitor, see [Get Started with Azure Monitor].</span></span> 


> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Monitor-API-Management-with-Azure-Monitor/player]
>
>
 
## <a name="metrics"></a><span data-ttu-id="9fca5-108">Metrica</span><span class="sxs-lookup"><span data-stu-id="9fca5-108">Metrics</span></span>
<span data-ttu-id="9fca5-109">Gestione API attualmente genera cinque metriche e contiamo tooadd più hello future.</span><span class="sxs-lookup"><span data-stu-id="9fca5-109">API Management currently emits five metrics and we plan tooadd more in hello future.</span></span> <span data-ttu-id="9fca5-110">Queste metriche vengono create ogni minuto, fornendo quasi in tempo reale visibilità nello stato di hello e integrità delle API.</span><span class="sxs-lookup"><span data-stu-id="9fca5-110">These metrics are emitted every minute, giving you near real-time visibility into hello state and health of your APIs.</span></span> <span data-ttu-id="9fca5-111">Ecco un riepilogo delle metriche hello:</span><span class="sxs-lookup"><span data-stu-id="9fca5-111">Following is a summary of hello metrics:</span></span>
* <span data-ttu-id="9fca5-112">Totale richieste Gateway: hello numero di API richieste nel periodo di hello.</span><span class="sxs-lookup"><span data-stu-id="9fca5-112">Total Gateway Requests: hello number of API requests in hello period.</span></span> 
* <span data-ttu-id="9fca5-113">Richieste riuscite Gateway: numero hello di richieste di API che ha ricevuto i codici di risposta HTTP ha esito positivo inclusi 304, 307 e qualsiasi valore inferiore rispetto a 301 (ad esempio, 200).</span><span class="sxs-lookup"><span data-stu-id="9fca5-113">Successful Gateway Requests: hello number of API requests that received successful HTTP response codes including 304, 307 and anything smaller than 301 (for example, 200).</span></span> 
* <span data-ttu-id="9fca5-114">Gateway richieste non riuscite: numero di hello di richieste di API che ha ricevuto i codici di risposta HTTP errati tra 400 e qualsiasi valore maggiore di 500.</span><span class="sxs-lookup"><span data-stu-id="9fca5-114">Failed Gateway Requests: hello number of API requests that received erroneous HTTP response codes including 400 and anything larger than 500.</span></span>
* <span data-ttu-id="9fca5-115">Richieste non autorizzate di Gateway: numero hello di richieste di API che ha ricevuto i codici di risposta HTTP inclusi 401, 403 e 429.</span><span class="sxs-lookup"><span data-stu-id="9fca5-115">Unauthorized Gateway Requests: hello number of API requests that received HTTP response codes including 401, 403, and 429.</span></span> 
* <span data-ttu-id="9fca5-116">Altre richieste Gateway: numero hello di richieste di API che ha ricevuto i codici di risposta HTTP che non appartengono tooany di hello precedente categorie (ad esempio, 418).</span><span class="sxs-lookup"><span data-stu-id="9fca5-116">Other Gateway Requests: hello number of API requests that received HTTP response codes that do not belong tooany of hello preceding categories (for example, 418).</span></span>

<span data-ttu-id="9fca5-117">È possibile accedere alle metriche del servizio Gestione API o alle metriche di tutte le risorse di Azure in Monitoraggio di Azure.</span><span class="sxs-lookup"><span data-stu-id="9fca5-117">You can access metrics in your API Management service, or access metrics of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="9fca5-118">metrica tooview nel servizio Gestione API:</span><span class="sxs-lookup"><span data-stu-id="9fca5-118">tooview metrics in your API Management service:</span></span>
1. <span data-ttu-id="9fca5-119">Hello aprirlo portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9fca5-119">Open hello Azure portal.</span></span>
2. <span data-ttu-id="9fca5-120">Passare il servizio di gestione API tooyour.</span><span class="sxs-lookup"><span data-stu-id="9fca5-120">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="9fca5-121">Fare clic su **Metrica**.</span><span class="sxs-lookup"><span data-stu-id="9fca5-121">Click **Metrics**.</span></span>

![Pannello delle metriche][metrics-blade]

<span data-ttu-id="9fca5-123">Per ulteriori informazioni su come toouse metriche, vedere [Panoramica di metriche].</span><span class="sxs-lookup"><span data-stu-id="9fca5-123">For more information about how toouse Metrics, see [Overview of Metrics].</span></span>

## <a name="activity-logs"></a><span data-ttu-id="9fca5-124">Log attività</span><span class="sxs-lookup"><span data-stu-id="9fca5-124">Activity Logs</span></span>
<span data-ttu-id="9fca5-125">Log attività forniscono informazioni sulle operazioni di hello che sono stati eseguiti i servizi gestione API.</span><span class="sxs-lookup"><span data-stu-id="9fca5-125">Activity logs provide insight into hello operations that were performed on your API Management services.</span></span> <span data-ttu-id="9fca5-126">In precedenza erano noti come "log di controllo" o "log operativi".</span><span class="sxs-lookup"><span data-stu-id="9fca5-126">It was previously known as "audit logs" or "operational logs".</span></span> <span data-ttu-id="9fca5-127">Utilizzo di log di attività, è possibile determinare hello "cosa, chi e quando" per le operazioni (PUT, POST, DELETE) eseguite nei servizi gestione API di scrittura.</span><span class="sxs-lookup"><span data-stu-id="9fca5-127">Using activity logs, you can determine hello "what, who, and when" for any write operations (PUT, POST, DELETE) taken on your API Management services.</span></span> 

> [!NOTE]
> <span data-ttu-id="9fca5-128">Log attività non includono le operazioni di lettura (GET) o sulle operazioni eseguite hello portale classico di server di pubblicazione o utilizzando hello originale le API di gestione.</span><span class="sxs-lookup"><span data-stu-id="9fca5-128">Activity logs do not include read (GET) operations or operations performed in hello classic Publisher Portal or using hello original Management APIs.</span></span>

<span data-ttu-id="9fca5-129">È possibile accedere ai log attività del servizio Gestione API o ai log di tutte le risorse di Azure in Monitoraggio di Azure.</span><span class="sxs-lookup"><span data-stu-id="9fca5-129">You can access activity logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="9fca5-130">attività tooview accede al servizio Gestione API:</span><span class="sxs-lookup"><span data-stu-id="9fca5-130">tooview activity logs in your API Management service:</span></span>
1. <span data-ttu-id="9fca5-131">Hello aprirlo portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9fca5-131">Open hello Azure portal.</span></span>
2. <span data-ttu-id="9fca5-132">Passare il servizio di gestione API tooyour.</span><span class="sxs-lookup"><span data-stu-id="9fca5-132">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="9fca5-133">Fare clic su **Log attività**.</span><span class="sxs-lookup"><span data-stu-id="9fca5-133">Click **Activity log**.</span></span>

![Pannello dei log attività][activity-logs-blade]

<span data-ttu-id="9fca5-135">Per ulteriori informazioni su come toouse metriche, vedere [Panoramica del log attività].</span><span class="sxs-lookup"><span data-stu-id="9fca5-135">For more information about how toouse Metrics, see [Overview of Activity Logs].</span></span>

## <a name="alerts"></a><span data-ttu-id="9fca5-136">Avvisi</span><span class="sxs-lookup"><span data-stu-id="9fca5-136">Alerts</span></span>
<span data-ttu-id="9fca5-137">È possibile configurare avvisi tooreceive in base alle metriche e attività di log.</span><span class="sxs-lookup"><span data-stu-id="9fca5-137">You can configure tooreceive alerts based on metrics and activity logs.</span></span> <span data-ttu-id="9fca5-138">Monitoraggio di Azure consente tooconfigure un avviso toodo hello seguenti attiva:</span><span class="sxs-lookup"><span data-stu-id="9fca5-138">Azure Monitor allows you tooconfigure an alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="9fca5-139">Inviare una notifica via posta elettronica</span><span class="sxs-lookup"><span data-stu-id="9fca5-139">Send an email notification</span></span>
* <span data-ttu-id="9fca5-140">Chiamare un webhook</span><span class="sxs-lookup"><span data-stu-id="9fca5-140">Call a webhook</span></span>
* <span data-ttu-id="9fca5-141">Richiamare un'app per la logica di Azure</span><span class="sxs-lookup"><span data-stu-id="9fca5-141">Invoke an Azure Logic App</span></span>

<span data-ttu-id="9fca5-142">È possibile configurare regole per gli avvisi nel servizio Gestione API o in Monitoraggio di Azure.</span><span class="sxs-lookup"><span data-stu-id="9fca5-142">You can configure alert rules in your API Management service, or in Azure Monitor.</span></span> <span data-ttu-id="9fca5-143">tooconfigure usarle in Gestione API:</span><span class="sxs-lookup"><span data-stu-id="9fca5-143">tooconfigure them in API Management:</span></span> 
1. <span data-ttu-id="9fca5-144">Hello aprirlo portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9fca5-144">Open hello Azure portal.</span></span>
2. <span data-ttu-id="9fca5-145">Passare il servizio di gestione API tooyour.</span><span class="sxs-lookup"><span data-stu-id="9fca5-145">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="9fca5-146">Fare clic su **Regole di avviso**.</span><span class="sxs-lookup"><span data-stu-id="9fca5-146">Click **Alert rules**.</span></span>

![Pannello Regole di avviso][alert-rules-blade]

<span data-ttu-id="9fca5-148">Per altre informazioni sull'uso degli avvisi, vedere [Panoramica degli avvisi].</span><span class="sxs-lookup"><span data-stu-id="9fca5-148">For more information about using Alerts, see [Overview of Alerts].</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="9fca5-149">Log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="9fca5-149">Diagnostic Logs</span></span>
<span data-ttu-id="9fca5-150">I log di diagnostica offrono informazioni dettagliate sulle operazioni e gli errori importanti per il controllo e per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="9fca5-150">Diagnostic logs provide rich information about operations and errors that are important for auditing as well as troubleshooting purposes.</span></span> <span data-ttu-id="9fca5-151">I log di diagnostica differiscono dai log attività.</span><span class="sxs-lookup"><span data-stu-id="9fca5-151">Diagnostics logs differ from activity logs.</span></span> <span data-ttu-id="9fca5-152">Log attività forniscono informazioni dettagliate sui operazioni hello che sono state eseguite in risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="9fca5-152">Activity logs provide insights into hello operations that were performed on your Azure resources.</span></span> <span data-ttu-id="9fca5-153">I log di diagnostica forniscono informazioni approfondite sulle operazioni che la risorsa esegue automaticamente.</span><span class="sxs-lookup"><span data-stu-id="9fca5-153">Diagnostics logs provide insight into operations that your resource performed itself.</span></span>

<span data-ttu-id="9fca5-154">Gestione API fornisce attualmente la diagnostica di log (in batch ogni ora) sull'API singoli richiesta con ogni voce con hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="9fca5-154">API Management currently provides diagnostics logs (batched hourly) about individual API request with each entry having hello following structure:</span></span>

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

<span data-ttu-id="9fca5-155">È possibile accedere ai log di diagnostica del servizio Gestione API o ai log di tutte le risorse di Azure in Monitoraggio di Azure.</span><span class="sxs-lookup"><span data-stu-id="9fca5-155">You can access diagnostic logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="9fca5-156">tooview i log di diagnostica nel servizio Gestione API:</span><span class="sxs-lookup"><span data-stu-id="9fca5-156">tooview diagnostic logs in your API Management service:</span></span>
1. <span data-ttu-id="9fca5-157">Hello aprirlo portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9fca5-157">Open hello Azure portal.</span></span>
2. <span data-ttu-id="9fca5-158">Passare il servizio di gestione API tooyour.</span><span class="sxs-lookup"><span data-stu-id="9fca5-158">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="9fca5-159">Fare clic su **Log di diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="9fca5-159">Click **Diagnostic log**.</span></span>

![Pannello Log di diagnostica][diagnostic-logs-blade]

<span data-ttu-id="9fca5-161">Per ulteriori informazioni su come toouse metriche, vedere [Panoramica del log di diagnostica].</span><span class="sxs-lookup"><span data-stu-id="9fca5-161">For more information about how toouse Metrics, see [Overview of Diagnostic Logs].</span></span>

## <a name="next-step"></a><span data-ttu-id="9fca5-162">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="9fca5-162">Next Step</span></span>

* <span data-ttu-id="9fca5-163">[introduzione a Monitoraggio di Azure]</span><span class="sxs-lookup"><span data-stu-id="9fca5-163">[Get Started with Azure Monitor]</span></span>
* <span data-ttu-id="9fca5-164">[Panoramica di metriche]</span><span class="sxs-lookup"><span data-stu-id="9fca5-164">[Overview of Metrics]</span></span>
* <span data-ttu-id="9fca5-165">[Panoramica del log attività]</span><span class="sxs-lookup"><span data-stu-id="9fca5-165">[Overview of Activity Logs]</span></span>
* <span data-ttu-id="9fca5-166">[Panoramica del log di diagnostica]</span><span class="sxs-lookup"><span data-stu-id="9fca5-166">[Overview of Diagnostic Logs]</span></span>
* <span data-ttu-id="9fca5-167">[Panoramica degli avvisi]</span><span class="sxs-lookup"><span data-stu-id="9fca5-167">[Overview of Alerts]</span></span>

[introduzione a Monitoraggio di Azure]: ../monitoring-and-diagnostics/monitoring-get-started.md
[Panoramica di metriche]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md
[Panoramica del log attività]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md
[Panoramica del log di diagnostica]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md
[Panoramica degli avvisi]: ../monitoring-and-diagnostics/insights-alerts-portal.md



[metrics-blade]: ./media/api-management-azure-monitor/api-management-metrics-blade.png
[activity-logs-blade]: ./media/api-management-azure-monitor/api-management-activity-logs-blade.png
[alert-rules-blade]: ./media/api-management-azure-monitor/api-management-alert-rules-blade.png
[diagnostic-logs-blade]: ./media/api-management-azure-monitor/api-management-diagnostic-logs-blade.png
