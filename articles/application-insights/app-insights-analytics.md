---
title: aaaAnalytics - hello potente strumento di ricerca di Azure Application Insights | Documenti Microsoft
description: 'Panoramica di Analitica, hello potente diagnostica strumento di ricerca di Application Insights. '
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
ms.openlocfilehash: d2b41e2fff7cc786e11fa3dfe94fc46f1b86e9eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="analytics-in-application-insights"></a><span data-ttu-id="d4907-103">Analytics in Application Insights</span><span class="sxs-lookup"><span data-stu-id="d4907-103">Analytics in Application Insights</span></span>
<span data-ttu-id="d4907-104">[Analitica](app-insights-analytics.md) è hello ricerca potenti funzionalità di [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d4907-104">[Analytics](app-insights-analytics.md) is hello powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="d4907-105">Queste pagine descrivono il linguaggio di query di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="d4907-105">These pages describe the Log Analytics query language.</span></span> 

* <span data-ttu-id="d4907-106">**[Guardare video introduttivo hello](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="d4907-106">**[Watch hello introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="d4907-107">**[Test unità Analitica dei dati simulati](https://analytics.applicationinsights.io/demo)**  se l'applicazione non invia dati tooApplication Insights ancora.</span><span class="sxs-lookup"><span data-stu-id="d4907-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data tooApplication Insights yet.</span></span>
* <span data-ttu-id="d4907-108">**[SQL utenti schede di riferimento rapido](https://aka.ms/sql-analytics)**  traduce idiomi comuni hello.</span><span class="sxs-lookup"><span data-stu-id="d4907-108">**[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates hello most common idioms.</span></span>
* <span data-ttu-id="d4907-109">**[Riferimenti al linguaggio](app-insights-analytics-reference.md)**  informazioni su come toouse tutti hello potenti funzionalità di linguaggio di query Log Analitica hello.</span><span class="sxs-lookup"><span data-stu-id="d4907-109">**[Language Reference](app-insights-analytics-reference.md)** Learn how toouse all hello powerful features of hello Log Analytics query language.</span></span>


## <a name="queries-in-analytics"></a><span data-ttu-id="d4907-110">Query in Analytics</span><span class="sxs-lookup"><span data-stu-id="d4907-110">Queries in Analytics</span></span>
<span data-ttu-id="d4907-111">Una query tipica è costituita da una tabella di *origine* seguita da una serie di *operatori* separati da `|`.</span><span class="sxs-lookup"><span data-stu-id="d4907-111">A typical query is a *source* table followed by a series of *operators* separated by `|`.</span></span> 

<span data-ttu-id="d4907-112">Ad esempio, possibile scoprire l'orario di cittadini hello di giorno di Hyderabad provare l'app web.</span><span class="sxs-lookup"><span data-stu-id="d4907-112">For example, let's find out what time of day hello citizens of Hyderabad try our web app.</span></span> <span data-ttu-id="d4907-113">E mentre siamo, esaminare i codici di risultato vengono restituiti le richieste HTTP tootheir.</span><span class="sxs-lookup"><span data-stu-id="d4907-113">And while we're there, let's see what result codes are returned tootheir HTTP requests.</span></span> 

```AIQL
requests
| where timestamp > ago(30d)
| summarize ClientCount = dcount(client_IP) by bin(timestamp, 1h), resultCode
| extend LocalTime = timestamp - 4h
| order by LocalTime desc
| render barchart
```

<span data-ttu-id="d4907-114">Abbiamo conteggio indirizzi IP client distinti, raggruppandoli in base all'ora di hello del giorno hello su hello ultimi 7 giorni.</span><span class="sxs-lookup"><span data-stu-id="d4907-114">We count distinct client IP addresses, grouping them by hello hour of hello day over hello past 7 days.</span></span> 

> [!NOTE]
> <span data-ttu-id="d4907-115">risultati tooget di fuori di hello 24 ore precedenti, includere 'timestamp' in modo esplicito nella query o utilizzare i menu a discesa intervallo tempo hello.</span><span class="sxs-lookup"><span data-stu-id="d4907-115">tooget results outside hello previous 24h, either include 'timestamp' explicitly in your query, or use hello time range drop-down menu.</span></span>
>

<span data-ttu-id="d4907-116">Verranno visualizzati risultati hello con hello barra presentazione grafico, la selezione toostack hello dai codici di risposta diversi:</span><span class="sxs-lookup"><span data-stu-id="d4907-116">Let's display hello results with hello bar chart presentation, choosing toostack hello results from different response codes:</span></span>

![Scegliere il grafico a barre, gli assi X e Y, quindi la segmentazione](./media/app-insights-analytics/020.png)

<span data-ttu-id="d4907-118">L'app sembra riscuotere molto successo a Hyderabad all'ora di pranzo e prima di andare a dormire.</span><span class="sxs-lookup"><span data-stu-id="d4907-118">Looks like our app is most popular at lunchtime and bed-time in Hyderabad.</span></span> <span data-ttu-id="d4907-119">(Si dovrebbe anche esaminare quei 500 codici).</span><span class="sxs-lookup"><span data-stu-id="d4907-119">(And we should investigate those 500 codes.)</span></span>

<span data-ttu-id="d4907-120">Sono inoltre disponibili operazioni statistiche avanzate:</span><span class="sxs-lookup"><span data-stu-id="d4907-120">There are also powerful statistical operations:</span></span>

![Risultati della query statistica](./media/app-insights-analytics/025.png)

<span data-ttu-id="d4907-122">linguaggio Hello presenta molte funzionalità interessanti:</span><span class="sxs-lookup"><span data-stu-id="d4907-122">hello language has many attractive features:</span></span>


* <span data-ttu-id="d4907-123">[Filtrare](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) i dati di telemetria app non elaborati in base a qualsiasi campo, comprese proprietà personalizzate e metriche.</span><span class="sxs-lookup"><span data-stu-id="d4907-123">[Filter](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) your raw app telemetry by any fields, including your custom properties and metrics.</span></span>
* <span data-ttu-id="d4907-124">[Unire](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) più tabelle: correlare le richieste a visualizzazioni di pagina, chiamate a dipendenze, eccezioni e tracce di log.</span><span class="sxs-lookup"><span data-stu-id="d4907-124">[Join](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) multiple tables – correlate requests with page views, dependency calls, exceptions and log traces.</span></span>
* <span data-ttu-id="d4907-125">[Aggregazioni](https://docs.loganalytics.io/learn/tutorials/aggregations.html)statistiche avanzate.</span><span class="sxs-lookup"><span data-stu-id="d4907-125">Powerful statistical [aggregations](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span></span>
* <span data-ttu-id="d4907-126">Efficienti quanto SQL, ma è molto più semplice per le query complesse: invece di nidificazione di istruzioni, si invia tramite pipe dati hello da un'operazione elementari toohello successivamente.</span><span class="sxs-lookup"><span data-stu-id="d4907-126">Just as powerful as SQL, but much easier for complex queries: instead of nesting statements, you pipe hello data from one elementary operation toohello next.</span></span>
* <span data-ttu-id="d4907-127">Visualizzazioni immediate e avanzate.</span><span class="sxs-lookup"><span data-stu-id="d4907-127">Immediate and powerful visualizations.</span></span>
* <span data-ttu-id="d4907-128">[PIN grafici dashboard tooAzure](app-insights-analytics-using.md#pin-to-dashboard).</span><span class="sxs-lookup"><span data-stu-id="d4907-128">[Pin charts tooAzure dashboards](app-insights-analytics-using.md#pin-to-dashboard).</span></span>
* <span data-ttu-id="d4907-129">[Esportare le query tooPower BI](app-insights-analytics-using.md#export-to-power-bi).</span><span class="sxs-lookup"><span data-stu-id="d4907-129">[Export queries tooPower BI](app-insights-analytics-using.md#export-to-power-bi).</span></span>
* <span data-ttu-id="d4907-130">È presente un [API REST](https://dev.applicationinsights.io/) che è possibile utilizzare toorun query a livello di codice, ad esempio da Powershell.</span><span class="sxs-lookup"><span data-stu-id="d4907-130">There's a [REST API](https://dev.applicationinsights.io/) that you can use toorun queries programmatically, for example from Powershell.</span></span>


## <a name="connect-tooyour-application-insights-data"></a><span data-ttu-id="d4907-131">Connettere i dati di Application Insights tooyour</span><span class="sxs-lookup"><span data-stu-id="d4907-131">Connect tooyour Application Insights data</span></span>
<span data-ttu-id="d4907-132">Aprire Analisi dal [pannello Panoramica](app-insights-dashboards.md) dell'app in Application Insights:</span><span class="sxs-lookup"><span data-stu-id="d4907-132">Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights:</span></span> 

![In portal.azure.com, aprire la risorsa di Application Insights e selezionare Analytics.](./media/app-insights-analytics/001.png)


## <a name="video"></a><span data-ttu-id="d4907-134">Video</span><span class="sxs-lookup"><span data-stu-id="d4907-134">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]



## <a name="query-examples"></a><span data-ttu-id="d4907-135">Esempi di query</span><span class="sxs-lookup"><span data-stu-id="d4907-135">Query examples</span></span>

<span data-ttu-id="d4907-136">Provare questi power hello tooillustrate di procedure dettagliate dell'uso Analitica:</span><span class="sxs-lookup"><span data-stu-id="d4907-136">Try these walkthroughs tooillustrate hello power of using Analytics:</span></span>

 *  [<span data-ttu-id="d4907-137">Diagnostica automatica di picchi e salti procedurali nella durata delle richieste</span><span class="sxs-lookup"><span data-stu-id="d4907-137">Automatic diagnostics of spikes and step jumps in requests durations</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Automatic%20diagnostics%20of%20sudden%20spikes%20or%20step%20jumps%20in%20requests%20duration&shared=true)
 *  [<span data-ttu-id="d4907-138">Analisi delle riduzioni delle prestazioni con l'analisi delle serie temporali</span><span class="sxs-lookup"><span data-stu-id="d4907-138">Analyzing performance degradations with time series analysis</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20performance%20degradations%20with%20time%20series%20analysis&shared=true)
 *  [<span data-ttu-id="d4907-139">Analisi degli errori delle applicazioni con autocluster e diffpatterns</span><span class="sxs-lookup"><span data-stu-id="d4907-139">Analyzing application failures with autocluster and diffpatterns</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20application%20failures%20with%20autocluster%20and%20diffpatterns&shared=true)
 *  [<span data-ttu-id="d4907-140">Rilevamenti forma avanzati con l'analisi delle serie temporali</span><span class="sxs-lookup"><span data-stu-id="d4907-140">Advanced shape detections with time series analysis</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Advanced%20shape%20detection%20with%20time%20series%20analysis&shared=true)
 *  [<span data-ttu-id="d4907-141">Utilizzando la finestra operazioni tooanalyze utilizzo dell'applicazione (in sequenza e così via MAU/DAU)</span><span class="sxs-lookup"><span data-stu-id="d4907-141">Using sliding window operations tooanalyze application usage (rolling MAU/DAU etc)</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Using%20sliding%20window%20calculations%20to%20analyze%20usage%20metrics:%20rolling%20MAU~2FDAU%20and%20cohorts&shared=true)
 *  <span data-ttu-id="d4907-142">[Rilevamento di interruzioni del servizio in base all'analisi dei registri di debug](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) e post di blog corrispondente [qui](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).</span><span class="sxs-lookup"><span data-stu-id="d4907-142">[Detection of service disruptions based on analysis of debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) and a matching blog post [here](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).</span></span>
 *  <span data-ttu-id="d4907-143">[Profilatura delle prestazioni delle applicazioni tramite log di debug semplici](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) e post di blog corrispondente [qui](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)</span><span class="sxs-lookup"><span data-stu-id="d4907-143">[Profiling applications’ performance using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)</span></span>
 *  <span data-ttu-id="d4907-144">[Misurazione della durata di hello per ogni passaggio nel flusso di codice utilizzando i registri di debug semplice](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) e un post di blog corrispondente [qui](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)</span><span class="sxs-lookup"><span data-stu-id="d4907-144">[Measuring hello duration for each step in your code flow using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)</span></span>
 *  <span data-ttu-id="d4907-145">[Analisi della concorrenza tramite log di debug semplici](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) e post di blog corrispondente [qui](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)</span><span class="sxs-lookup"><span data-stu-id="d4907-145">[Analyzing concurrency using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)</span></span>



## <a name="next-steps"></a><span data-ttu-id="d4907-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d4907-146">Next steps</span></span>
* <span data-ttu-id="d4907-147">È consigliabile iniziare con hello [Introduzione al linguaggio](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="d4907-147">We recommend you start with hello [language tour](app-insights-analytics-tour.md).</span></span> 
* <span data-ttu-id="d4907-148">Altre informazioni sull'[uso di Analytics](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="d4907-148">More about [using Analytics](app-insights-analytics-using.md).</span></span> 
* <span data-ttu-id="d4907-149">[Informazioni di riferimento sul linguaggio](app-insights-analytics-reference.md).</span><span class="sxs-lookup"><span data-stu-id="d4907-149">[Language reference](app-insights-analytics-reference.md).</span></span> 
