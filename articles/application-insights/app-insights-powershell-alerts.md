---
title: Usare PowerShell per impostare gli avvisi in Application Insights | Microsoft Docs
description: Automatizzare la configurazione di Application Insights per ricevere messaggi di posta elettronica sulle modifiche delle metriche.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 05d6a9e0-77a2-4a35-9052-a7768d23a196
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: 64675c51abf80daa3a55220f910aa8fdee1042ca
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="use-powershell-to-set-alerts-in-application-insights"></a><span data-ttu-id="e0f2b-103">Usare PowerShell per impostare gli avvisi in Application Insights</span><span class="sxs-lookup"><span data-stu-id="e0f2b-103">Use PowerShell to set alerts in Application Insights</span></span>
<span data-ttu-id="e0f2b-104">È possibile automatizzare la configurazione degli [avvisi](app-insights-alerts.md) in [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e0f2b-104">You can automate the configuration of [alerts](app-insights-alerts.md) in [Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="e0f2b-105">È inoltre possibile [impostare webhook per automatizzare la risposta a un avviso](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="e0f2b-105">In addition, you can [set webhooks to automate your response to an alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

> [!NOTE]
> <span data-ttu-id="e0f2b-106">Se si vuole creare risorse e avvisi allo stesso tempo, considerare l'[uso di un modello di Azure Resource Manager](app-insights-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e0f2b-106">If you want to create resources and alerts at the same time, consider [using an Azure Resource Manager template](app-insights-powershell.md).</span></span>
>
>

## <a name="one-time-setup"></a><span data-ttu-id="e0f2b-107">Installazione singola</span><span class="sxs-lookup"><span data-stu-id="e0f2b-107">One-time setup</span></span>
<span data-ttu-id="e0f2b-108">Se non si è mai usato PowerShell con la sottoscrizione di Azure:</span><span class="sxs-lookup"><span data-stu-id="e0f2b-108">If you haven't used PowerShell with your Azure subscription before:</span></span>

<span data-ttu-id="e0f2b-109">Installare il modulo Azure Powershell nel computer in cui verranno eseguiti gli script.</span><span class="sxs-lookup"><span data-stu-id="e0f2b-109">Install the Azure Powershell module on the machine where you want to run the scripts.</span></span>

* <span data-ttu-id="e0f2b-110">Installare [Installazione guidata piattaforma Web Microsoft (v5 o versione successiva)](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0f2b-110">Install [Microsoft Web Platform Installer (v5 or higher)](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="e0f2b-111">Usarla per installare Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e0f2b-111">Use it to install Microsoft Azure Powershell</span></span>

## <a name="connect-to-azure"></a><span data-ttu-id="e0f2b-112">Connettersi ad Azure</span><span class="sxs-lookup"><span data-stu-id="e0f2b-112">Connect to Azure</span></span>
<span data-ttu-id="e0f2b-113">Avviare Azure PowerShell e [connettersi alla sottoscrizione](/powershell/azure/overview):</span><span class="sxs-lookup"><span data-stu-id="e0f2b-113">Start Azure PowerShell and [connect to your subscription](/powershell/azure/overview):</span></span>

```PowerShell

    Add-AzureAccount
```


## <a name="get-alerts"></a><span data-ttu-id="e0f2b-114">Ottenere gli avvisi</span><span class="sxs-lookup"><span data-stu-id="e0f2b-114">Get alerts</span></span>
    Get-AzureAlertRmRule -ResourceGroup "Fabrikam" [-Name "My rule"] [-DetailedOutput]

## <a name="add-alert"></a><span data-ttu-id="e0f2b-115">Aggiungere un avviso</span><span class="sxs-lookup"><span data-stu-id="e0f2b-115">Add alert</span></span>
    Add-AlertRule  -Name "{ALERT NAME}" -Description "{TEXT}" `
     -ResourceGroup "{GROUP NAME}" `
     -ResourceId "/subscriptions/{SUBSCRIPTION ID}/resourcegroups/{GROUP NAME}/providers/microsoft.insights/components/{APP RESOURCE NAME}" `
     -MetricName "{METRIC NAME}" `
     -Operator GreaterThan  `
     -Threshold {NUMBER}   `
     -WindowSize {HH:MM:SS}  `
     [-SendEmailToServiceOwners] `
     [-CustomEmails "EMAIL1@X.COM","EMAIL2@Y.COM" ] `
     -Location "East US" // must be East US at present
     -RuleType Metric



## <a name="example-1"></a><span data-ttu-id="e0f2b-116">Esempio 1</span><span class="sxs-lookup"><span data-stu-id="e0f2b-116">Example 1</span></span>
<span data-ttu-id="e0f2b-117">Invia un messaggio di posta elettronica se la risposta del server alle richieste HTTP, calcolate su una media di 5 minuti, richiede più di 1 secondo.</span><span class="sxs-lookup"><span data-stu-id="e0f2b-117">Email me if the server's response to HTTP requests, averaged over 5 minutes, is slower than 1 second.</span></span> <span data-ttu-id="e0f2b-118">La risorsa di Application Insights è denominata IceCreamWebApp e si trova nel gruppo di risorse Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="e0f2b-118">My Application Insights resource is called IceCreamWebApp, and it is in resource group Fabrikam.</span></span> <span data-ttu-id="e0f2b-119">Sono il proprietario della sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e0f2b-119">I am the owner of the Azure subscription.</span></span>

<span data-ttu-id="e0f2b-120">Il GUID è l'ID sottoscrizione (non la chiave di strumentazione dell'applicazione).</span><span class="sxs-lookup"><span data-stu-id="e0f2b-120">The GUID is the subscription ID (not the instrumentation key of the application).</span></span>

    Add-AlertRule -Name "slow responses" `
     -Description "email me if the server responds slowly" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "request.duration" `
     -Operator GreaterThan `
     -Threshold 1 `
     -WindowSize 00:05:00 `
     -SendEmailToServiceOwners `
     -Location "East US" -RuleType Metric

## <a name="example-2"></a><span data-ttu-id="e0f2b-121">Esempio 2</span><span class="sxs-lookup"><span data-stu-id="e0f2b-121">Example 2</span></span>
<span data-ttu-id="e0f2b-122">Ho un'applicazione in cui uso [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) per segnalare una metrica denominata "salesPerHour".</span><span class="sxs-lookup"><span data-stu-id="e0f2b-122">I have an application in which I use [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) to report a metric named "salesPerHour."</span></span> <span data-ttu-id="e0f2b-123">Invia un messaggio di posta elettronica ai miei colleghi, se "salesPerHour" scende sotto il valore 100, calcolato su una media di 24 ore.</span><span class="sxs-lookup"><span data-stu-id="e0f2b-123">Send an email to my colleagues if "salesPerHour" drops below 100, averaged over 24 hours.</span></span>

    Add-AlertRule -Name "poor sales" `
     -Description "slow sales alert" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "salesPerHour" `
     -Operator LessThan `
     -Threshold 100 `
     -WindowSize 24:00:00 `
     -CustomEmails "satish@fabrikam.com","lei@fabrikam.com" `
     -Location "East US" -RuleType Metric

<span data-ttu-id="e0f2b-124">La stessa regola può essere utilizzata per la metrica riportata utilizzando il [parametro misura](app-insights-api-custom-events-metrics.md#properties) di un altra chiamata di rilevamento come ad esempio TrackEvent o trackPageView.</span><span class="sxs-lookup"><span data-stu-id="e0f2b-124">The same rule can be used for the metric reported by using the [measurement parameter](app-insights-api-custom-events-metrics.md#properties) of another tracking call such as TrackEvent or trackPageView.</span></span>

## <a name="metric-names"></a><span data-ttu-id="e0f2b-125">Nomi delle metriche</span><span class="sxs-lookup"><span data-stu-id="e0f2b-125">Metric names</span></span>
| <span data-ttu-id="e0f2b-126">Nome metrica</span><span class="sxs-lookup"><span data-stu-id="e0f2b-126">Metric name</span></span> | <span data-ttu-id="e0f2b-127">Nome schermata</span><span class="sxs-lookup"><span data-stu-id="e0f2b-127">Screen name</span></span> | <span data-ttu-id="e0f2b-128">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e0f2b-128">Description</span></span> |
| --- | --- | --- |
| `basicExceptionBrowser.count` |<span data-ttu-id="e0f2b-129">Eccezioni del browser</span><span class="sxs-lookup"><span data-stu-id="e0f2b-129">Browser exceptions</span></span> |<span data-ttu-id="e0f2b-130">Conteggio delle eccezioni non rilevate generate nel browser.</span><span class="sxs-lookup"><span data-stu-id="e0f2b-130">Count of uncaught exceptions thrown in the browser.</span></span> |
| `basicExceptionServer.count` |<span data-ttu-id="e0f2b-131">Eccezioni del server</span><span class="sxs-lookup"><span data-stu-id="e0f2b-131">Server exceptions</span></span> |<span data-ttu-id="e0f2b-132">Conteggio delle eccezioni non gestite generate dall'applicazione</span><span class="sxs-lookup"><span data-stu-id="e0f2b-132">Count of unhandled exceptions thrown by the app</span></span> |
| `clientPerformance.clientProcess.value` |<span data-ttu-id="e0f2b-133">Tempo di elaborazione client</span><span class="sxs-lookup"><span data-stu-id="e0f2b-133">Client processing time</span></span> |<span data-ttu-id="e0f2b-134">Tempo compreso tra la ricezione dell'ultimo byte di un documento e il caricamento del DOM.</span><span class="sxs-lookup"><span data-stu-id="e0f2b-134">Time between receiving the last byte of a document until the DOM is loaded.</span></span> <span data-ttu-id="e0f2b-135">Le richieste asincrone potrebbero essere ancora in fase di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="e0f2b-135">Async requests may still be processing.</span></span> |
| `clientPerformance.networkConnection.value` |<span data-ttu-id="e0f2b-136">Tempo di connessione alla rete per il caricamento della pagina</span><span class="sxs-lookup"><span data-stu-id="e0f2b-136">Page load network connect time</span></span> |<span data-ttu-id="e0f2b-137">Tempo impiegato dal browser per connettersi alla rete.</span><span class="sxs-lookup"><span data-stu-id="e0f2b-137">Time the browser takes to connect to the network.</span></span> <span data-ttu-id="e0f2b-138">Può essere 0 se memorizzato nella cache.</span><span class="sxs-lookup"><span data-stu-id="e0f2b-138">Can be 0 if cached.</span></span> |
| `clientPerformance.receiveRequest.value` |<span data-ttu-id="e0f2b-139">Tempo per la ricezione della risposta</span><span class="sxs-lookup"><span data-stu-id="e0f2b-139">Receiving response time</span></span> |<span data-ttu-id="e0f2b-140">Tempo tra l'invio di richiesta del browser e l'inizio della ricezione della risposta.</span><span class="sxs-lookup"><span data-stu-id="e0f2b-140">Time between browser sending request to starting to receive response.</span></span> |
| `clientPerformance.sendRequest.value` |<span data-ttu-id="e0f2b-141">Tempo per l'invio della richiesta</span><span class="sxs-lookup"><span data-stu-id="e0f2b-141">Send request time</span></span> |<span data-ttu-id="e0f2b-142">Tempo impiegato dal browser per inviare la richiesta.</span><span class="sxs-lookup"><span data-stu-id="e0f2b-142">Time taken by browser to send request.</span></span> |
| `clientPerformance.total.value` |<span data-ttu-id="e0f2b-143">Tempo di caricamento della pagina del browser</span><span class="sxs-lookup"><span data-stu-id="e0f2b-143">Browser page load time</span></span> |<span data-ttu-id="e0f2b-144">Tempo compreso tra la richiesta utente e il caricamento di DOM, fogli di stile, script e immagini.</span><span class="sxs-lookup"><span data-stu-id="e0f2b-144">Time from user request until DOM, stylesheets, scripts and images are loaded.</span></span> |
| `performanceCounter.available_bytes.value` |<span data-ttu-id="e0f2b-145">Memoria disponibile</span><span class="sxs-lookup"><span data-stu-id="e0f2b-145">Available memory</span></span> |<span data-ttu-id="e0f2b-146">Memoria fisica immediatamente disponibile per l'allocazione a un processo o utilizzabile dal sistema.</span><span class="sxs-lookup"><span data-stu-id="e0f2b-146">Physical memory immediately available for a process or for system use.</span></span> |
| `performanceCounter.io_data_bytes_per_sec.value` |<span data-ttu-id="e0f2b-147">Velocità di elaborazione I/O</span><span class="sxs-lookup"><span data-stu-id="e0f2b-147">Process IO Rate</span></span> |<span data-ttu-id="e0f2b-148">Numero totale di byte al secondo letti e scritti in file, rete e dispositivi.</span><span class="sxs-lookup"><span data-stu-id="e0f2b-148">Total bytes per second read and written to files, network and devices.</span></span> |
| `performanceCounter.number_of_exceps_thrown_per_sec.value` |<span data-ttu-id="e0f2b-149">Frequenza di eccezioni</span><span class="sxs-lookup"><span data-stu-id="e0f2b-149">exception rate</span></span> |<span data-ttu-id="e0f2b-150">Eccezioni generate al secondo.</span><span class="sxs-lookup"><span data-stu-id="e0f2b-150">Exceptions thrown per second.</span></span> |
| `performanceCounter.percentage_processor_time.value` |<span data-ttu-id="e0f2b-151">CPU processo</span><span class="sxs-lookup"><span data-stu-id="e0f2b-151">Process CPU</span></span> |<span data-ttu-id="e0f2b-152">Percentuale di tempo trascorso di tutti i thread di processo usati dal processore per le istruzioni di esecuzione relative al processo dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e0f2b-152">The percentage of elapsed time of all process threads used by the processor to execution instructions for the applications process.</span></span> |
| `performanceCounter.percentage_processor_total.value` |<span data-ttu-id="e0f2b-153">Tempo processore</span><span class="sxs-lookup"><span data-stu-id="e0f2b-153">Processor time</span></span> |<span data-ttu-id="e0f2b-154">Percentuale di tempo che il processore dedica a thread non inattivi.</span><span class="sxs-lookup"><span data-stu-id="e0f2b-154">The percentage of time that the processor spends in non-Idle threads.</span></span> |
| `performanceCounter.process_private_bytes.value` |<span data-ttu-id="e0f2b-155">Byte privati processo</span><span class="sxs-lookup"><span data-stu-id="e0f2b-155">Process private bytes</span></span> |<span data-ttu-id="e0f2b-156">Memoria assegnata in modo esclusivo ai processi dell'applicazione monitorata.</span><span class="sxs-lookup"><span data-stu-id="e0f2b-156">Memory exclusively assigned to the monitored application's processes.</span></span> |
| `performanceCounter.request_execution_time.value` |<span data-ttu-id="e0f2b-157">Tempo di esecuzione della richiesta di ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e0f2b-157">ASP.NET request execution time</span></span> |<span data-ttu-id="e0f2b-158">Tempo di esecuzione della richiesta più recente.</span><span class="sxs-lookup"><span data-stu-id="e0f2b-158">Execution time of the most recent request.</span></span> |
| `performanceCounter.requests_in_application_queue.value` |<span data-ttu-id="e0f2b-159">Richieste ASP.NET nella coda di esecuzione</span><span class="sxs-lookup"><span data-stu-id="e0f2b-159">ASP.NET requests in execution queue</span></span> |<span data-ttu-id="e0f2b-160">Lunghezza della coda di richieste dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e0f2b-160">Length of the application request queue.</span></span> |
| `performanceCounter.requests_per_sec.value` |<span data-ttu-id="e0f2b-161">Percentuale di richieste ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e0f2b-161">ASP.NET request rate</span></span> |<span data-ttu-id="e0f2b-162">Percentuale di tutte le richieste effettuate all'applicazione da ASP.NET in un secondo.</span><span class="sxs-lookup"><span data-stu-id="e0f2b-162">Rate of all requests to the application per second from ASP.NET.</span></span> |
| `remoteDependencyFailed.durationMetric.count` |<span data-ttu-id="e0f2b-163">Errori di dipendenze</span><span class="sxs-lookup"><span data-stu-id="e0f2b-163">Dependency failures</span></span> |<span data-ttu-id="e0f2b-164">Conteggio delle chiamate non riuscite effettuate dall'applicazione server alle risorse esterne.</span><span class="sxs-lookup"><span data-stu-id="e0f2b-164">Count of failed calls made by the server application to external resources.</span></span> |
| `request.duration` |<span data-ttu-id="e0f2b-165">Tempo di risposta del server</span><span class="sxs-lookup"><span data-stu-id="e0f2b-165">Server response time</span></span> |<span data-ttu-id="e0f2b-166">Tempo compreso tra la ricezione di una richiesta HTTP e il completamento dell'invio della risposta.</span><span class="sxs-lookup"><span data-stu-id="e0f2b-166">Time between receiving an HTTP request and finishing sending the response.</span></span> |
| `request.rate` |<span data-ttu-id="e0f2b-167">Frequenza di richieste</span><span class="sxs-lookup"><span data-stu-id="e0f2b-167">Request rate</span></span> |<span data-ttu-id="e0f2b-168">Percentuale di tutte le richieste effettuate all'applicazione in un secondo.</span><span class="sxs-lookup"><span data-stu-id="e0f2b-168">Rate of all requests to the application per second.</span></span> |
| `requestFailed.count` |<span data-ttu-id="e0f2b-169">Richieste non riuscite</span><span class="sxs-lookup"><span data-stu-id="e0f2b-169">Failed requests</span></span> |<span data-ttu-id="e0f2b-170">Conteggio delle richieste HTTP per cui è stato restituito un codice di risposta maggiore o uguale a 400</span><span class="sxs-lookup"><span data-stu-id="e0f2b-170">Count of HTTP requests that resulted in a response code >= 400</span></span> |
| `view.count` |<span data-ttu-id="e0f2b-171">Visualizzazioni pagina</span><span class="sxs-lookup"><span data-stu-id="e0f2b-171">Page views</span></span> |<span data-ttu-id="e0f2b-172">Conteggio delle richieste utente del client per una pagina Web.</span><span class="sxs-lookup"><span data-stu-id="e0f2b-172">Count of client user requests for a web page.</span></span> <span data-ttu-id="e0f2b-173">Il traffico sintetico è filtrato.</span><span class="sxs-lookup"><span data-stu-id="e0f2b-173">Synthetic traffic is filtered out.</span></span> |
| <span data-ttu-id="e0f2b-174">{nome metrica personalizzato}</span><span class="sxs-lookup"><span data-stu-id="e0f2b-174">{your custom metric name}</span></span> |<span data-ttu-id="e0f2b-175">{nome metrica}</span><span class="sxs-lookup"><span data-stu-id="e0f2b-175">{Your metric name}</span></span> |<span data-ttu-id="e0f2b-176">Il valore della metrica segnalato da [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) o il [parametro delle misurazioni di una chiamata di rilevamento](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="e0f2b-176">Your metric value reported by [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) or in the [measurements parameter of a tracking call](app-insights-api-custom-events-metrics.md#properties).</span></span> |

<span data-ttu-id="e0f2b-177">Le metriche vengono inviate da moduli di telemetria diversi:</span><span class="sxs-lookup"><span data-stu-id="e0f2b-177">The metrics are sent by different telemetry modules:</span></span>

| <span data-ttu-id="e0f2b-178">Gruppo metrica</span><span class="sxs-lookup"><span data-stu-id="e0f2b-178">Metric group</span></span> | <span data-ttu-id="e0f2b-179">Modulo dell'agente di raccolta</span><span class="sxs-lookup"><span data-stu-id="e0f2b-179">Collector module</span></span> |
| --- | --- |
| <span data-ttu-id="e0f2b-180">basicExceptionBrowser,</span><span class="sxs-lookup"><span data-stu-id="e0f2b-180">basicExceptionBrowser,</span></span><br/><span data-ttu-id="e0f2b-181">clientPerformance,</span><span class="sxs-lookup"><span data-stu-id="e0f2b-181">clientPerformance,</span></span><br/><span data-ttu-id="e0f2b-182">view</span><span class="sxs-lookup"><span data-stu-id="e0f2b-182">view</span></span> |[<span data-ttu-id="e0f2b-183">JavaScript browser</span><span class="sxs-lookup"><span data-stu-id="e0f2b-183">Browser JavaScript</span></span>](app-insights-javascript.md) |
| <span data-ttu-id="e0f2b-184">performanceCounter</span><span class="sxs-lookup"><span data-stu-id="e0f2b-184">performanceCounter</span></span> |[<span data-ttu-id="e0f2b-185">Prestazioni</span><span class="sxs-lookup"><span data-stu-id="e0f2b-185">Performance</span></span>](app-insights-configuration-with-applicationinsights-config.md) |
| <span data-ttu-id="e0f2b-186">remoteDependencyFailed</span><span class="sxs-lookup"><span data-stu-id="e0f2b-186">remoteDependencyFailed</span></span> |[<span data-ttu-id="e0f2b-187">Dipendenza</span><span class="sxs-lookup"><span data-stu-id="e0f2b-187">Dependency</span></span>](app-insights-configuration-with-applicationinsights-config.md) |
| <span data-ttu-id="e0f2b-188">request,</span><span class="sxs-lookup"><span data-stu-id="e0f2b-188">request,</span></span><br/><span data-ttu-id="e0f2b-189">requestFailed</span><span class="sxs-lookup"><span data-stu-id="e0f2b-189">requestFailed</span></span> |[<span data-ttu-id="e0f2b-190">Richiesta server</span><span class="sxs-lookup"><span data-stu-id="e0f2b-190">Server request</span></span>](app-insights-configuration-with-applicationinsights-config.md) |

## <a name="webhooks"></a><span data-ttu-id="e0f2b-191">Webhook</span><span class="sxs-lookup"><span data-stu-id="e0f2b-191">Webhooks</span></span>
<span data-ttu-id="e0f2b-192">È possibile [automatizzare la risposta a un avviso](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="e0f2b-192">You can [automate your response to an alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span> <span data-ttu-id="e0f2b-193">Azure richiamerà l'indirizzo Web specificato quando viene generato un avviso.</span><span class="sxs-lookup"><span data-stu-id="e0f2b-193">Azure will call a web address of your choice when an alert is raised.</span></span>

## <a name="see-also"></a><span data-ttu-id="e0f2b-194">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="e0f2b-194">See also</span></span>
* [<span data-ttu-id="e0f2b-195">Script per configurare Application Insights</span><span class="sxs-lookup"><span data-stu-id="e0f2b-195">Script to configure Application Insights</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="e0f2b-196">Creare risorse Application Insights e test web da modelli</span><span class="sxs-lookup"><span data-stu-id="e0f2b-196">Create Application Insights and web test resources from templates</span></span>](app-insights-powershell.md)
* [<span data-ttu-id="e0f2b-197">Automatizzare l'accoppiamento tra Diagnostica di Microsoft Azure e Application Insights</span><span class="sxs-lookup"><span data-stu-id="e0f2b-197">Automate coupling Microsoft Azure Diagnostics to Application Insights</span></span>](app-insights-powershell-azure-diagnostics.md)
* [<span data-ttu-id="e0f2b-198">Automatizzare la risposta a un avviso</span><span class="sxs-lookup"><span data-stu-id="e0f2b-198">Automate your response to an alert</span></span>](../monitoring-and-diagnostics/insights-webhooks-alerts.md)
