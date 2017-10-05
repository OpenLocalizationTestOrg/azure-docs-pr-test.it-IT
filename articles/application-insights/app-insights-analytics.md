---
title: 'Analisi: il potente strumento di ricerca di Application Insights | Microsoft Docs'
description: 'Panoramica di Analytics: lo strumento di ricerca diagnostica avanzato incluso in Application Insights. '
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 0a2f6011-5bcf-47b7-8450-40f284274b24
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 8174745a00a107eea648b223a00466b6a7f37331
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="analytics-in-application-insights"></a><span data-ttu-id="9eaa1-103">Analytics in Application Insights</span><span class="sxs-lookup"><span data-stu-id="9eaa1-103">Analytics in Application Insights</span></span>
<span data-ttu-id="9eaa1-104">L'[analisi](app-insights-analytics.md) è lo strumento di ricerca avanzato incluso in [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9eaa1-104">[Analytics](app-insights-analytics.md) is the powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="9eaa1-105">Queste pagine descrivono il linguaggio di query di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="9eaa1-105">These pages describe the Log Analytics query language.</span></span> 

* <span data-ttu-id="9eaa1-106">**[Guardare il video introduttivo](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="9eaa1-106">**[Watch the introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="9eaa1-107">**[Eseguire la versione di test di Analisi sui dati simulati](https://analytics.applicationinsights.io/demo)** se l'app non invia ancora i dati ad Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9eaa1-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data to Application Insights yet.</span></span>
* <span data-ttu-id="9eaa1-108">Il **[foglio informativo sugli utenti SQL](https://aka.ms/sql-analytics)** traduce i linguaggi più comuni.</span><span class="sxs-lookup"><span data-stu-id="9eaa1-108">**[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates the most common idioms.</span></span>
* <span data-ttu-id="9eaa1-109">**[Informazioni di riferimento sul linguaggio](app-insights-analytics-reference.md)** Informazioni su come usare tutte le funzionalità avanzate del linguaggio di query di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="9eaa1-109">**[Language Reference](app-insights-analytics-reference.md)** Learn how to use all the powerful features of the Log Analytics query language.</span></span>


## <a name="queries-in-analytics"></a><span data-ttu-id="9eaa1-110">Query in Analytics</span><span class="sxs-lookup"><span data-stu-id="9eaa1-110">Queries in Analytics</span></span>
<span data-ttu-id="9eaa1-111">Una query tipica è costituita da una tabella di *origine* seguita da una serie di *operatori* separati da `|`.</span><span class="sxs-lookup"><span data-stu-id="9eaa1-111">A typical query is a *source* table followed by a series of *operators* separated by `|`.</span></span> 

<span data-ttu-id="9eaa1-112">Ad esempio, è possibile sapere a che ora del giorno gli abitanti di Hyderabad sperimentano l'app Web.</span><span class="sxs-lookup"><span data-stu-id="9eaa1-112">For example, let's find out what time of day the citizens of Hyderabad try our web app.</span></span> <span data-ttu-id="9eaa1-113">Inoltre, è possibile sapere quali codici di risultato sono restituiti per le richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="9eaa1-113">And while we're there, let's see what result codes are returned to their HTTP requests.</span></span> 

```AIQL
requests
| where timestamp > ago(30d)
| summarize ClientCount = dcount(client_IP) by bin(timestamp, 1h), resultCode
| extend LocalTime = timestamp - 4h
| order by LocalTime desc
| render barchart
```

<span data-ttu-id="9eaa1-114">Si contano indirizzi IP client distinti, raggruppandoli in base all'ora del giorno negli ultimi 7 giorni.</span><span class="sxs-lookup"><span data-stu-id="9eaa1-114">We count distinct client IP addresses, grouping them by the hour of the day over the past 7 days.</span></span> 

> [!NOTE]
> <span data-ttu-id="9eaa1-115">Per ottenere risultati oltre le 24 ore precedenti, includere "timestamp" in modo esplicito nella query o usare il menu a discesa per l'intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="9eaa1-115">To get results outside the previous 24h, either include 'timestamp' explicitly in your query, or use the time range drop-down menu.</span></span>
>

<span data-ttu-id="9eaa1-116">Verranno visualizzati i risultati in una presentazione con grafico a barre, con lo stack dei risultati ottenuti da codici di risposta diversi:</span><span class="sxs-lookup"><span data-stu-id="9eaa1-116">Let's display the results with the bar chart presentation, choosing to stack the results from different response codes:</span></span>

![Scegliere il grafico a barre, gli assi X e Y, quindi la segmentazione](./media/app-insights-analytics/020.png)

<span data-ttu-id="9eaa1-118">L'app sembra riscuotere molto successo a Hyderabad all'ora di pranzo e prima di andare a dormire.</span><span class="sxs-lookup"><span data-stu-id="9eaa1-118">Looks like our app is most popular at lunchtime and bed-time in Hyderabad.</span></span> <span data-ttu-id="9eaa1-119">(Si dovrebbe anche esaminare quei 500 codici).</span><span class="sxs-lookup"><span data-stu-id="9eaa1-119">(And we should investigate those 500 codes.)</span></span>

<span data-ttu-id="9eaa1-120">Sono inoltre disponibili operazioni statistiche avanzate:</span><span class="sxs-lookup"><span data-stu-id="9eaa1-120">There are also powerful statistical operations:</span></span>

![Risultati della query statistica](./media/app-insights-analytics/025.png)

<span data-ttu-id="9eaa1-122">Il linguaggio include diverse funzionalità utili, è possibile:</span><span class="sxs-lookup"><span data-stu-id="9eaa1-122">The language has many attractive features:</span></span>


* <span data-ttu-id="9eaa1-123">[Filtrare](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) i dati di telemetria app non elaborati in base a qualsiasi campo, comprese proprietà personalizzate e metriche.</span><span class="sxs-lookup"><span data-stu-id="9eaa1-123">[Filter](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) your raw app telemetry by any fields, including your custom properties and metrics.</span></span>
* <span data-ttu-id="9eaa1-124">[Unire](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) più tabelle: correlare le richieste a visualizzazioni di pagina, chiamate a dipendenze, eccezioni e tracce di log.</span><span class="sxs-lookup"><span data-stu-id="9eaa1-124">[Join](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) multiple tables – correlate requests with page views, dependency calls, exceptions and log traces.</span></span>
* <span data-ttu-id="9eaa1-125">[Aggregazioni](https://docs.loganalytics.io/learn/tutorials/aggregations.html)statistiche avanzate.</span><span class="sxs-lookup"><span data-stu-id="9eaa1-125">Powerful statistical [aggregations](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span></span>
* <span data-ttu-id="9eaa1-126">Altrettanto efficace come SQL, ma molto più semplice per le query complesse: anziché nidificare le istruzioni, i dati vengono inviati tramite pipe da un'operazione semplice alla successiva.</span><span class="sxs-lookup"><span data-stu-id="9eaa1-126">Just as powerful as SQL, but much easier for complex queries: instead of nesting statements, you pipe the data from one elementary operation to the next.</span></span>
* <span data-ttu-id="9eaa1-127">Visualizzazioni immediate e avanzate.</span><span class="sxs-lookup"><span data-stu-id="9eaa1-127">Immediate and powerful visualizations.</span></span>
* <span data-ttu-id="9eaa1-128">[Aggiungere grafici ai dashboard di Azure](app-insights-analytics-using.md#pin-to-dashboard).</span><span class="sxs-lookup"><span data-stu-id="9eaa1-128">[Pin charts to Azure dashboards](app-insights-analytics-using.md#pin-to-dashboard).</span></span>
* <span data-ttu-id="9eaa1-129">[Esportare le query in Power BI](app-insights-analytics-using.md#export-to-power-bi).</span><span class="sxs-lookup"><span data-stu-id="9eaa1-129">[Export queries to Power BI](app-insights-analytics-using.md#export-to-power-bi).</span></span>
* <span data-ttu-id="9eaa1-130">Esiste un'[API REST](https://dev.applicationinsights.io/) che è possibile usare per eseguire query in modo programmatico, ad esempio da PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9eaa1-130">There's a [REST API](https://dev.applicationinsights.io/) that you can use to run queries programmatically, for example from Powershell.</span></span>


## <a name="connect-to-your-application-insights-data"></a><span data-ttu-id="9eaa1-131">Connettersi ai dati di Application Insights</span><span class="sxs-lookup"><span data-stu-id="9eaa1-131">Connect to your Application Insights data</span></span>
<span data-ttu-id="9eaa1-132">Aprire Analisi dal [pannello Panoramica](app-insights-dashboards.md) dell'app in Application Insights:</span><span class="sxs-lookup"><span data-stu-id="9eaa1-132">Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights:</span></span> 

![In portal.azure.com, aprire la risorsa di Application Insights e selezionare Analytics.](./media/app-insights-analytics/001.png)


## <a name="video"></a><span data-ttu-id="9eaa1-134">Video</span><span class="sxs-lookup"><span data-stu-id="9eaa1-134">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]



## <a name="query-examples"></a><span data-ttu-id="9eaa1-135">Esempi di query</span><span class="sxs-lookup"><span data-stu-id="9eaa1-135">Query examples</span></span>

<span data-ttu-id="9eaa1-136">Provare a eseguire queste procedure dettagliate per illustrare le potenzialità di utilizzo di Analytics:</span><span class="sxs-lookup"><span data-stu-id="9eaa1-136">Try these walkthroughs to illustrate the power of using Analytics:</span></span>

 *  [<span data-ttu-id="9eaa1-137">Diagnostica automatica di picchi e salti procedurali nella durata delle richieste</span><span class="sxs-lookup"><span data-stu-id="9eaa1-137">Automatic diagnostics of spikes and step jumps in requests durations</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Automatic%20diagnostics%20of%20sudden%20spikes%20or%20step%20jumps%20in%20requests%20duration&shared=true)
 *  [<span data-ttu-id="9eaa1-138">Analisi delle riduzioni delle prestazioni con l'analisi delle serie temporali</span><span class="sxs-lookup"><span data-stu-id="9eaa1-138">Analyzing performance degradations with time series analysis</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20performance%20degradations%20with%20time%20series%20analysis&shared=true)
 *  [<span data-ttu-id="9eaa1-139">Analisi degli errori delle applicazioni con autocluster e diffpatterns</span><span class="sxs-lookup"><span data-stu-id="9eaa1-139">Analyzing application failures with autocluster and diffpatterns</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20application%20failures%20with%20autocluster%20and%20diffpatterns&shared=true)
 *  [<span data-ttu-id="9eaa1-140">Rilevamenti forma avanzati con l'analisi delle serie temporali</span><span class="sxs-lookup"><span data-stu-id="9eaa1-140">Advanced shape detections with time series analysis</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Advanced%20shape%20detection%20with%20time%20series%20analysis&shared=true)
 *  [<span data-ttu-id="9eaa1-141">Uso di operazioni della finestra temporale scorrevole per analizzare l'utilizzo dell'applicazione (come MAU/DAU in sequenza e così via)</span><span class="sxs-lookup"><span data-stu-id="9eaa1-141">Using sliding window operations to analyze application usage (rolling MAU/DAU etc)</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Using%20sliding%20window%20calculations%20to%20analyze%20usage%20metrics:%20rolling%20MAU~2FDAU%20and%20cohorts&shared=true)
 *  <span data-ttu-id="9eaa1-142">[Rilevamento di interruzioni del servizio in base all'analisi dei registri di debug](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) e post di blog corrispondente [qui](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).</span><span class="sxs-lookup"><span data-stu-id="9eaa1-142">[Detection of service disruptions based on analysis of debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) and a matching blog post [here](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).</span></span>
 *  <span data-ttu-id="9eaa1-143">[Profilatura delle prestazioni delle applicazioni tramite log di debug semplici](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) e post di blog corrispondente [qui](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)</span><span class="sxs-lookup"><span data-stu-id="9eaa1-143">[Profiling applications’ performance using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)</span></span>
 *  <span data-ttu-id="9eaa1-144">[Misurazione della durata per ogni passaggio nel flusso di codice tramite log di debug semplici](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) e post di blog corrispondente [qui](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)</span><span class="sxs-lookup"><span data-stu-id="9eaa1-144">[Measuring the duration for each step in your code flow using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)</span></span>
 *  <span data-ttu-id="9eaa1-145">[Analisi della concorrenza tramite log di debug semplici](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) e post di blog corrispondente [qui](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)</span><span class="sxs-lookup"><span data-stu-id="9eaa1-145">[Analyzing concurrency using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)</span></span>



## <a name="next-steps"></a><span data-ttu-id="9eaa1-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9eaa1-146">Next steps</span></span>
* <span data-ttu-id="9eaa1-147">È consigliabile iniziare con una [panoramica sul linguaggio](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="9eaa1-147">We recommend you start with the [language tour](app-insights-analytics-tour.md).</span></span> 
* <span data-ttu-id="9eaa1-148">Altre informazioni sull'[uso di Analytics](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="9eaa1-148">More about [using Analytics](app-insights-analytics-using.md).</span></span> 
* <span data-ttu-id="9eaa1-149">[Informazioni di riferimento sul linguaggio](app-insights-analytics-reference.md).</span><span class="sxs-lookup"><span data-stu-id="9eaa1-149">[Language reference](app-insights-analytics-reference.md).</span></span> 
