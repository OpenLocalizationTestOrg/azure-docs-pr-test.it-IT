---
title: gli avvisi di tooset Powershell aaaUse in Application Insights | Documenti Microsoft
description: Automatizzare la configurazione di messaggi di posta elettronica tooget Application Insights sulle modifiche di metrica.
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
ms.openlocfilehash: d68e5f9511bb4015f59175724bc1a4a04ecf43e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooset-alerts-in-application-insights"></a><span data-ttu-id="23bfc-103">Utilizzare PowerShell tooset avvisi in Application Insights</span><span class="sxs-lookup"><span data-stu-id="23bfc-103">Use PowerShell tooset alerts in Application Insights</span></span>
<span data-ttu-id="23bfc-104">È possibile automatizzare la configurazione di hello di [avvisi](app-insights-alerts.md) in [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="23bfc-104">You can automate hello configuration of [alerts](app-insights-alerts.md) in [Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="23bfc-105">È inoltre possibile [impostare tooautomate webhook l'avviso tooan risposta](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="23bfc-105">In addition, you can [set webhooks tooautomate your response tooan alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

> [!NOTE]
> <span data-ttu-id="23bfc-106">Se si desidera toocreate risorse e gli avvisi a hello stesso tempo, prendere in considerazione [utilizzando un modello di gestione risorse di Azure](app-insights-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="23bfc-106">If you want toocreate resources and alerts at hello same time, consider [using an Azure Resource Manager template](app-insights-powershell.md).</span></span>
>
>

## <a name="one-time-setup"></a><span data-ttu-id="23bfc-107">Installazione singola</span><span class="sxs-lookup"><span data-stu-id="23bfc-107">One-time setup</span></span>
<span data-ttu-id="23bfc-108">Se non si è mai usato PowerShell con la sottoscrizione di Azure:</span><span class="sxs-lookup"><span data-stu-id="23bfc-108">If you haven't used PowerShell with your Azure subscription before:</span></span>

<span data-ttu-id="23bfc-109">Installare il modulo di Azure Powershell hello computer hello in cui si desidera script hello toorun.</span><span class="sxs-lookup"><span data-stu-id="23bfc-109">Install hello Azure Powershell module on hello machine where you want toorun hello scripts.</span></span>

* <span data-ttu-id="23bfc-110">Installare [Installazione guidata piattaforma Web Microsoft (v5 o versione successiva)](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="23bfc-110">Install [Microsoft Web Platform Installer (v5 or higher)](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="23bfc-111">Utilizzarlo tooinstall Microsoft Azure Powershell</span><span class="sxs-lookup"><span data-stu-id="23bfc-111">Use it tooinstall Microsoft Azure Powershell</span></span>

## <a name="connect-tooazure"></a><span data-ttu-id="23bfc-112">Connettersi tooAzure</span><span class="sxs-lookup"><span data-stu-id="23bfc-112">Connect tooAzure</span></span>
<span data-ttu-id="23bfc-113">Avviare PowerShell di Azure e [connettere sottoscrizione tooyour](/powershell/azure/overview):</span><span class="sxs-lookup"><span data-stu-id="23bfc-113">Start Azure PowerShell and [connect tooyour subscription](/powershell/azure/overview):</span></span>

```PowerShell

    Add-AzureAccount
```


## <a name="get-alerts"></a><span data-ttu-id="23bfc-114">Ottenere gli avvisi</span><span class="sxs-lookup"><span data-stu-id="23bfc-114">Get alerts</span></span>
    Get-AzureAlertRmRule -ResourceGroup "Fabrikam" [-Name "My rule"] [-DetailedOutput]

## <a name="add-alert"></a><span data-ttu-id="23bfc-115">Aggiungere un avviso</span><span class="sxs-lookup"><span data-stu-id="23bfc-115">Add alert</span></span>
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



## <a name="example-1"></a><span data-ttu-id="23bfc-116">Esempio 1</span><span class="sxs-lookup"><span data-stu-id="23bfc-116">Example 1</span></span>
<span data-ttu-id="23bfc-117">Invia messaggio se le richieste tooHTTP risposta del server di hello, calcolare la media di 5 minuti, è inferiore a 1 secondo.</span><span class="sxs-lookup"><span data-stu-id="23bfc-117">Email me if hello server's response tooHTTP requests, averaged over 5 minutes, is slower than 1 second.</span></span> <span data-ttu-id="23bfc-118">La risorsa di Application Insights è denominata IceCreamWebApp e si trova nel gruppo di risorse Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="23bfc-118">My Application Insights resource is called IceCreamWebApp, and it is in resource group Fabrikam.</span></span> <span data-ttu-id="23bfc-119">Sto proprietario hello di hello sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="23bfc-119">I am hello owner of hello Azure subscription.</span></span>

<span data-ttu-id="23bfc-120">Hello GUID è l'ID sottoscrizione hello (non hello chiave di strumentazione di un'applicazione hello).</span><span class="sxs-lookup"><span data-stu-id="23bfc-120">hello GUID is hello subscription ID (not hello instrumentation key of hello application).</span></span>

    Add-AlertRule -Name "slow responses" `
     -Description "email me if hello server responds slowly" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "request.duration" `
     -Operator GreaterThan `
     -Threshold 1 `
     -WindowSize 00:05:00 `
     -SendEmailToServiceOwners `
     -Location "East US" -RuleType Metric

## <a name="example-2"></a><span data-ttu-id="23bfc-121">Esempio 2</span><span class="sxs-lookup"><span data-stu-id="23bfc-121">Example 2</span></span>
<span data-ttu-id="23bfc-122">Un'applicazione in cui usare [trackmetric ()](app-insights-api-custom-events-metrics.md#trackmetric) tooreport una metrica denominata "salesPerHour".</span><span class="sxs-lookup"><span data-stu-id="23bfc-122">I have an application in which I use [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) tooreport a metric named "salesPerHour."</span></span> <span data-ttu-id="23bfc-123">Inviare un messaggio di posta elettronica toomy colleghi se "salesPerHour" scende di sotto di 100, calcolare la media di più di 24 ore.</span><span class="sxs-lookup"><span data-stu-id="23bfc-123">Send an email toomy colleagues if "salesPerHour" drops below 100, averaged over 24 hours.</span></span>

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

<span data-ttu-id="23bfc-124">Hello stessa regola può essere utilizzato per metrica hello segnalato tramite hello [parametro misura](app-insights-api-custom-events-metrics.md#properties) di rilevamento di un'altra chiamata, ad esempio TrackEvent o trackPageView.</span><span class="sxs-lookup"><span data-stu-id="23bfc-124">hello same rule can be used for hello metric reported by using hello [measurement parameter](app-insights-api-custom-events-metrics.md#properties) of another tracking call such as TrackEvent or trackPageView.</span></span>

## <a name="metric-names"></a><span data-ttu-id="23bfc-125">Nomi delle metriche</span><span class="sxs-lookup"><span data-stu-id="23bfc-125">Metric names</span></span>
| <span data-ttu-id="23bfc-126">Nome metrica</span><span class="sxs-lookup"><span data-stu-id="23bfc-126">Metric name</span></span> | <span data-ttu-id="23bfc-127">Nome schermata</span><span class="sxs-lookup"><span data-stu-id="23bfc-127">Screen name</span></span> | <span data-ttu-id="23bfc-128">Descrizione</span><span class="sxs-lookup"><span data-stu-id="23bfc-128">Description</span></span> |
| --- | --- | --- |
| `basicExceptionBrowser.count` |<span data-ttu-id="23bfc-129">Eccezioni del browser</span><span class="sxs-lookup"><span data-stu-id="23bfc-129">Browser exceptions</span></span> |<span data-ttu-id="23bfc-130">Numero di eccezioni non rilevate generate nel browser hello.</span><span class="sxs-lookup"><span data-stu-id="23bfc-130">Count of uncaught exceptions thrown in hello browser.</span></span> |
| `basicExceptionServer.count` |<span data-ttu-id="23bfc-131">Eccezioni del server</span><span class="sxs-lookup"><span data-stu-id="23bfc-131">Server exceptions</span></span> |<span data-ttu-id="23bfc-132">Numero di eccezioni non gestite generate da app hello</span><span class="sxs-lookup"><span data-stu-id="23bfc-132">Count of unhandled exceptions thrown by hello app</span></span> |
| `clientPerformance.clientProcess.value` |<span data-ttu-id="23bfc-133">Tempo di elaborazione client</span><span class="sxs-lookup"><span data-stu-id="23bfc-133">Client processing time</span></span> |<span data-ttu-id="23bfc-134">Tempo trascorso tra la ricezione ultimo byte di hello di un documento fino a quando non viene caricato hello DOM.</span><span class="sxs-lookup"><span data-stu-id="23bfc-134">Time between receiving hello last byte of a document until hello DOM is loaded.</span></span> <span data-ttu-id="23bfc-135">Le richieste asincrone potrebbero essere ancora in fase di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="23bfc-135">Async requests may still be processing.</span></span> |
| `clientPerformance.networkConnection.value` |<span data-ttu-id="23bfc-136">Tempo di connessione alla rete per il caricamento della pagina</span><span class="sxs-lookup"><span data-stu-id="23bfc-136">Page load network connect time</span></span> |<span data-ttu-id="23bfc-137">Browser hello ora accetta tooconnect toohello rete.</span><span class="sxs-lookup"><span data-stu-id="23bfc-137">Time hello browser takes tooconnect toohello network.</span></span> <span data-ttu-id="23bfc-138">Può essere 0 se memorizzato nella cache.</span><span class="sxs-lookup"><span data-stu-id="23bfc-138">Can be 0 if cached.</span></span> |
| `clientPerformance.receiveRequest.value` |<span data-ttu-id="23bfc-139">Tempo per la ricezione della risposta</span><span class="sxs-lookup"><span data-stu-id="23bfc-139">Receiving response time</span></span> |<span data-ttu-id="23bfc-140">Tempo trascorso tra l'invio richiesta toostarting tooreceive risposta browser.</span><span class="sxs-lookup"><span data-stu-id="23bfc-140">Time between browser sending request toostarting tooreceive response.</span></span> |
| `clientPerformance.sendRequest.value` |<span data-ttu-id="23bfc-141">Tempo per l'invio della richiesta</span><span class="sxs-lookup"><span data-stu-id="23bfc-141">Send request time</span></span> |<span data-ttu-id="23bfc-142">Tempo impiegato dal toosend richiesta del browser.</span><span class="sxs-lookup"><span data-stu-id="23bfc-142">Time taken by browser toosend request.</span></span> |
| `clientPerformance.total.value` |<span data-ttu-id="23bfc-143">Tempo di caricamento della pagina del browser</span><span class="sxs-lookup"><span data-stu-id="23bfc-143">Browser page load time</span></span> |<span data-ttu-id="23bfc-144">Tempo compreso tra la richiesta utente e il caricamento di DOM, fogli di stile, script e immagini.</span><span class="sxs-lookup"><span data-stu-id="23bfc-144">Time from user request until DOM, stylesheets, scripts and images are loaded.</span></span> |
| `performanceCounter.available_bytes.value` |<span data-ttu-id="23bfc-145">Memoria disponibile</span><span class="sxs-lookup"><span data-stu-id="23bfc-145">Available memory</span></span> |<span data-ttu-id="23bfc-146">Memoria fisica immediatamente disponibile per l'allocazione a un processo o utilizzabile dal sistema.</span><span class="sxs-lookup"><span data-stu-id="23bfc-146">Physical memory immediately available for a process or for system use.</span></span> |
| `performanceCounter.io_data_bytes_per_sec.value` |<span data-ttu-id="23bfc-147">Velocità di elaborazione I/O</span><span class="sxs-lookup"><span data-stu-id="23bfc-147">Process IO Rate</span></span> |<span data-ttu-id="23bfc-148">Totale byte al secondo lette e scritte toofiles, rete e dispositivi.</span><span class="sxs-lookup"><span data-stu-id="23bfc-148">Total bytes per second read and written toofiles, network and devices.</span></span> |
| `performanceCounter.number_of_exceps_thrown_per_sec.value` |<span data-ttu-id="23bfc-149">Frequenza di eccezioni</span><span class="sxs-lookup"><span data-stu-id="23bfc-149">exception rate</span></span> |<span data-ttu-id="23bfc-150">Eccezioni generate al secondo.</span><span class="sxs-lookup"><span data-stu-id="23bfc-150">Exceptions thrown per second.</span></span> |
| `performanceCounter.percentage_processor_time.value` |<span data-ttu-id="23bfc-151">CPU processo</span><span class="sxs-lookup"><span data-stu-id="23bfc-151">Process CPU</span></span> |<span data-ttu-id="23bfc-152">Hello percentuale di tempo di tutti i thread di processo utilizzato da istruzioni del tooexecution hello processore per processo dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="23bfc-152">hello percentage of elapsed time of all process threads used by hello processor tooexecution instructions for hello applications process.</span></span> |
| `performanceCounter.percentage_processor_total.value` |<span data-ttu-id="23bfc-153">Tempo processore</span><span class="sxs-lookup"><span data-stu-id="23bfc-153">Processor time</span></span> |<span data-ttu-id="23bfc-154">Percentuale tempo processore hello Hello trascorre in thread non inattivo.</span><span class="sxs-lookup"><span data-stu-id="23bfc-154">hello percentage of time that hello processor spends in non-Idle threads.</span></span> |
| `performanceCounter.process_private_bytes.value` |<span data-ttu-id="23bfc-155">Byte privati processo</span><span class="sxs-lookup"><span data-stu-id="23bfc-155">Process private bytes</span></span> |<span data-ttu-id="23bfc-156">Memoria assegnata in modo esclusivo toohello monitorati i processi dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="23bfc-156">Memory exclusively assigned toohello monitored application's processes.</span></span> |
| `performanceCounter.request_execution_time.value` |<span data-ttu-id="23bfc-157">Tempo di esecuzione della richiesta di ASP.NET</span><span class="sxs-lookup"><span data-stu-id="23bfc-157">ASP.NET request execution time</span></span> |<span data-ttu-id="23bfc-158">Tempo di esecuzione della richiesta più recente di hello.</span><span class="sxs-lookup"><span data-stu-id="23bfc-158">Execution time of hello most recent request.</span></span> |
| `performanceCounter.requests_in_application_queue.value` |<span data-ttu-id="23bfc-159">Richieste ASP.NET nella coda di esecuzione</span><span class="sxs-lookup"><span data-stu-id="23bfc-159">ASP.NET requests in execution queue</span></span> |<span data-ttu-id="23bfc-160">Lunghezza della coda di richieste applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="23bfc-160">Length of hello application request queue.</span></span> |
| `performanceCounter.requests_per_sec.value` |<span data-ttu-id="23bfc-161">Percentuale di richieste ASP.NET</span><span class="sxs-lookup"><span data-stu-id="23bfc-161">ASP.NET request rate</span></span> |<span data-ttu-id="23bfc-162">Frequenza di tutti richieste applicazione toohello al secondo da ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="23bfc-162">Rate of all requests toohello application per second from ASP.NET.</span></span> |
| `remoteDependencyFailed.durationMetric.count` |<span data-ttu-id="23bfc-163">Errori di dipendenze</span><span class="sxs-lookup"><span data-stu-id="23bfc-163">Dependency failures</span></span> |<span data-ttu-id="23bfc-164">Numero di chiamate non riuscite effettuate dalle risorse di tooexternal hello server applicazioni.</span><span class="sxs-lookup"><span data-stu-id="23bfc-164">Count of failed calls made by hello server application tooexternal resources.</span></span> |
| `request.duration` |<span data-ttu-id="23bfc-165">Tempo di risposta del server</span><span class="sxs-lookup"><span data-stu-id="23bfc-165">Server response time</span></span> |<span data-ttu-id="23bfc-166">Tempo tra la ricezione di una richiesta HTTP e il completamento dell'invio risposta hello.</span><span class="sxs-lookup"><span data-stu-id="23bfc-166">Time between receiving an HTTP request and finishing sending hello response.</span></span> |
| `request.rate` |<span data-ttu-id="23bfc-167">Frequenza di richieste</span><span class="sxs-lookup"><span data-stu-id="23bfc-167">Request rate</span></span> |<span data-ttu-id="23bfc-168">Frequenza di applicazione di toohello tutte le richieste al secondo.</span><span class="sxs-lookup"><span data-stu-id="23bfc-168">Rate of all requests toohello application per second.</span></span> |
| `requestFailed.count` |<span data-ttu-id="23bfc-169">Richieste non riuscite</span><span class="sxs-lookup"><span data-stu-id="23bfc-169">Failed requests</span></span> |<span data-ttu-id="23bfc-170">Conteggio delle richieste HTTP per cui è stato restituito un codice di risposta maggiore o uguale a 400</span><span class="sxs-lookup"><span data-stu-id="23bfc-170">Count of HTTP requests that resulted in a response code >= 400</span></span> |
| `view.count` |<span data-ttu-id="23bfc-171">Visualizzazioni pagina</span><span class="sxs-lookup"><span data-stu-id="23bfc-171">Page views</span></span> |<span data-ttu-id="23bfc-172">Conteggio delle richieste utente del client per una pagina Web.</span><span class="sxs-lookup"><span data-stu-id="23bfc-172">Count of client user requests for a web page.</span></span> <span data-ttu-id="23bfc-173">Il traffico sintetico è filtrato.</span><span class="sxs-lookup"><span data-stu-id="23bfc-173">Synthetic traffic is filtered out.</span></span> |
| <span data-ttu-id="23bfc-174">{nome metrica personalizzato}</span><span class="sxs-lookup"><span data-stu-id="23bfc-174">{your custom metric name}</span></span> |<span data-ttu-id="23bfc-175">{nome metrica}</span><span class="sxs-lookup"><span data-stu-id="23bfc-175">{Your metric name}</span></span> |<span data-ttu-id="23bfc-176">Il valore della metrica segnalati da [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) o hello [parametro misurazioni di una chiamata di rilevamento](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="23bfc-176">Your metric value reported by [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) or in hello [measurements parameter of a tracking call](app-insights-api-custom-events-metrics.md#properties).</span></span> |

<span data-ttu-id="23bfc-177">le metriche Hello vengono inviate da moduli diversi dati di telemetria:</span><span class="sxs-lookup"><span data-stu-id="23bfc-177">hello metrics are sent by different telemetry modules:</span></span>

| <span data-ttu-id="23bfc-178">Gruppo metrica</span><span class="sxs-lookup"><span data-stu-id="23bfc-178">Metric group</span></span> | <span data-ttu-id="23bfc-179">Modulo dell'agente di raccolta</span><span class="sxs-lookup"><span data-stu-id="23bfc-179">Collector module</span></span> |
| --- | --- |
| <span data-ttu-id="23bfc-180">basicExceptionBrowser,</span><span class="sxs-lookup"><span data-stu-id="23bfc-180">basicExceptionBrowser,</span></span><br/><span data-ttu-id="23bfc-181">clientPerformance,</span><span class="sxs-lookup"><span data-stu-id="23bfc-181">clientPerformance,</span></span><br/><span data-ttu-id="23bfc-182">view</span><span class="sxs-lookup"><span data-stu-id="23bfc-182">view</span></span> |[<span data-ttu-id="23bfc-183">JavaScript browser</span><span class="sxs-lookup"><span data-stu-id="23bfc-183">Browser JavaScript</span></span>](app-insights-javascript.md) |
| <span data-ttu-id="23bfc-184">performanceCounter</span><span class="sxs-lookup"><span data-stu-id="23bfc-184">performanceCounter</span></span> |[<span data-ttu-id="23bfc-185">Prestazioni</span><span class="sxs-lookup"><span data-stu-id="23bfc-185">Performance</span></span>](app-insights-configuration-with-applicationinsights-config.md) |
| <span data-ttu-id="23bfc-186">remoteDependencyFailed</span><span class="sxs-lookup"><span data-stu-id="23bfc-186">remoteDependencyFailed</span></span> |[<span data-ttu-id="23bfc-187">Dipendenza</span><span class="sxs-lookup"><span data-stu-id="23bfc-187">Dependency</span></span>](app-insights-configuration-with-applicationinsights-config.md) |
| <span data-ttu-id="23bfc-188">request,</span><span class="sxs-lookup"><span data-stu-id="23bfc-188">request,</span></span><br/><span data-ttu-id="23bfc-189">requestFailed</span><span class="sxs-lookup"><span data-stu-id="23bfc-189">requestFailed</span></span> |[<span data-ttu-id="23bfc-190">Richiesta server</span><span class="sxs-lookup"><span data-stu-id="23bfc-190">Server request</span></span>](app-insights-configuration-with-applicationinsights-config.md) |

## <a name="webhooks"></a><span data-ttu-id="23bfc-191">Webhook</span><span class="sxs-lookup"><span data-stu-id="23bfc-191">Webhooks</span></span>
<span data-ttu-id="23bfc-192">È possibile [automatizzare l'avviso tooan risposta](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="23bfc-192">You can [automate your response tooan alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span> <span data-ttu-id="23bfc-193">Azure richiamerà l'indirizzo Web specificato quando viene generato un avviso.</span><span class="sxs-lookup"><span data-stu-id="23bfc-193">Azure will call a web address of your choice when an alert is raised.</span></span>

## <a name="see-also"></a><span data-ttu-id="23bfc-194">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="23bfc-194">See also</span></span>
* [<span data-ttu-id="23bfc-195">Script tooconfigure Application Insights</span><span class="sxs-lookup"><span data-stu-id="23bfc-195">Script tooconfigure Application Insights</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="23bfc-196">Creare risorse Application Insights e test web da modelli</span><span class="sxs-lookup"><span data-stu-id="23bfc-196">Create Application Insights and web test resources from templates</span></span>](app-insights-powershell.md)
* [<span data-ttu-id="23bfc-197">Automatizzare l'accoppiamento tra Microsoft Azure Diagnostics tooApplication Insights</span><span class="sxs-lookup"><span data-stu-id="23bfc-197">Automate coupling Microsoft Azure Diagnostics tooApplication Insights</span></span>](app-insights-powershell-azure-diagnostics.md)
* [<span data-ttu-id="23bfc-198">Automatizzare l'avviso tooan risposta</span><span class="sxs-lookup"><span data-stu-id="23bfc-198">Automate your response tooan alert</span></span>](../monitoring-and-diagnostics/insights-webhooks-alerts.md)
