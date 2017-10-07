---
title: aaaUsing Analitica - hello potente strumento di ricerca di Azure Application Insights | Documenti Microsoft
description: 'Utilizzo di hello Analitica, hello potente diagnostica strumento di ricerca di Application Insights. '
services: application-insights
documentationcenter: 
author: danhadari
manager: carmonm
ms.assetid: c3b34430-f592-4c32-b900-e9f50ca096b3
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 6e0246848457db368c57d08c47b5bf73f4e5e3a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-analytics-in-application-insights"></a><span data-ttu-id="0cb05-103">Uso di Analytics in Application Insights</span><span class="sxs-lookup"><span data-stu-id="0cb05-103">Using Analytics in Application Insights</span></span>
<span data-ttu-id="0cb05-104">[Analitica](app-insights-analytics.md) è hello ricerca potenti funzionalità di [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0cb05-104">[Analytics](app-insights-analytics.md) is hello powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="0cb05-105">Queste pagine descrivono il linguaggio di query di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="0cb05-105">These pages describe the Log Analytics query language.</span></span>

* <span data-ttu-id="0cb05-106">**[Guardare video introduttivo hello](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="0cb05-106">**[Watch hello introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="0cb05-107">**[Test unità Analitica dei dati simulati](https://analytics.applicationinsights.io/demo)**  se l'applicazione non invia dati tooApplication Insights ancora.</span><span class="sxs-lookup"><span data-stu-id="0cb05-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data tooApplication Insights yet.</span></span>

## <a name="open-analytics"></a><span data-ttu-id="0cb05-108">Aprire Analytics</span><span class="sxs-lookup"><span data-stu-id="0cb05-108">Open Analytics</span></span>
<span data-ttu-id="0cb05-109">Nella home page dell'app in Application Insights fare clic su Analytics.</span><span class="sxs-lookup"><span data-stu-id="0cb05-109">From your app's home resource in Application Insights, click Analytics.</span></span>

![In portal.azure.com, aprire la risorsa di Application Insights e selezionare Analytics.](./media/app-insights-analytics-using/001.png)

<span data-ttu-id="0cb05-111">esercitazione inline Hello fornisce alcune informazioni su ciò che è possibile eseguire.</span><span class="sxs-lookup"><span data-stu-id="0cb05-111">hello inline tutorial gives you some ideas about what you can do.</span></span>

<span data-ttu-id="0cb05-112">È disponibile una [panoramica più ampia qui](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="0cb05-112">There's a [more extensive tour here](app-insights-analytics-tour.md).</span></span>

## <a name="query-your-telemetry"></a><span data-ttu-id="0cb05-113">Eseguire query sui dati di telemetria</span><span class="sxs-lookup"><span data-stu-id="0cb05-113">Query your telemetry</span></span>
### <a name="write-a-query"></a><span data-ttu-id="0cb05-114">Scrivere una query</span><span class="sxs-lookup"><span data-stu-id="0cb05-114">Write a query</span></span>
![Visualizzazione schema](./media/app-insights-analytics-using/150.png)

<span data-ttu-id="0cb05-116">Iniziare con i nomi di hello delle tabelle di hello elencate a sinistra di hello (o hello [intervallo](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) o [unione](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) operatori).</span><span class="sxs-lookup"><span data-stu-id="0cb05-116">Begin with hello names of any of hello tables listed on hello left (or hello [range](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) or [union](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) operators).</span></span> <span data-ttu-id="0cb05-117">Utilizzare `|` toocreate una pipeline di [operatori](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html).</span><span class="sxs-lookup"><span data-stu-id="0cb05-117">Use `|` toocreate a pipeline of [operators](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html).</span></span> 

<span data-ttu-id="0cb05-118">Viene richiesto con operatori hello e gli elementi di espressione hello che è possibile utilizzare.</span><span class="sxs-lookup"><span data-stu-id="0cb05-118">IntelliSense prompts you with hello operators and hello expression elements that you can use.</span></span> <span data-ttu-id="0cb05-119">Fare clic sull'icona informazioni hello (o premere CTRL + BARRA SPAZIATRICE) tooget una descrizione più dettagliata ed esempi su come toouse ogni elemento.</span><span class="sxs-lookup"><span data-stu-id="0cb05-119">Click hello information icon (or press CTRL+Space) tooget a longer description and examples of how toouse each element.</span></span>

<span data-ttu-id="0cb05-120">Vedere hello [Introduzione al linguaggio Analitica](app-insights-analytics-tour.md) e [riferimenti al linguaggio](app-insights-analytics-reference.md).</span><span class="sxs-lookup"><span data-stu-id="0cb05-120">See hello [Analytics language tour](app-insights-analytics-tour.md) and [language reference](app-insights-analytics-reference.md).</span></span>

### <a name="run-a-query"></a><span data-ttu-id="0cb05-121">Eseguire una query</span><span class="sxs-lookup"><span data-stu-id="0cb05-121">Run a query</span></span>
![Esecuzione di una query](./media/app-insights-analytics-using/130.png)

1. <span data-ttu-id="0cb05-123">Nelle query è possibile usare interruzioni di riga.</span><span class="sxs-lookup"><span data-stu-id="0cb05-123">You can use single line breaks in a query.</span></span>
2. <span data-ttu-id="0cb05-124">Posizionare hello cursore all'interno o alla fine della query hello desiderati toorun hello.</span><span class="sxs-lookup"><span data-stu-id="0cb05-124">Put hello cursor inside or at hello end of hello query you want toorun.</span></span>
3. <span data-ttu-id="0cb05-125">Controllare l'intervallo di tempo hello della query.</span><span class="sxs-lookup"><span data-stu-id="0cb05-125">Check hello time range of your query.</span></span> <span data-ttu-id="0cb05-126">È possibile modificarlo o ignorarlo inserendo la propria clausola [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) nella query.</span><span class="sxs-lookup"><span data-stu-id="0cb05-126">(You can change it, or override it by including your own [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) clause in your query.)</span></span>
3. <span data-ttu-id="0cb05-127">Fare clic su Vai toorun hello.</span><span class="sxs-lookup"><span data-stu-id="0cb05-127">Click Go toorun hello query.</span></span>
4. <span data-ttu-id="0cb05-128">Non inserire righe vuote nella query.</span><span class="sxs-lookup"><span data-stu-id="0cb05-128">Don't put blank lines in your query.</span></span> <span data-ttu-id="0cb05-129">È possibile mantenere più query separate in un'unica scheda di query, separandole con righe vuote.</span><span class="sxs-lookup"><span data-stu-id="0cb05-129">You can keep several separated queries in one query tab by separating them with blank lines.</span></span> <span data-ttu-id="0cb05-130">Solo query hello con cursore hello viene eseguita.</span><span class="sxs-lookup"><span data-stu-id="0cb05-130">Only hello query that has hello cursor runs.</span></span>

### <a name="save-a-query"></a><span data-ttu-id="0cb05-131">Salvare una query</span><span class="sxs-lookup"><span data-stu-id="0cb05-131">Save a query</span></span>
![Salvataggio di una query](./media/app-insights-analytics-using/140.png)

1. <span data-ttu-id="0cb05-133">Salvare il file di query corrente hello.</span><span class="sxs-lookup"><span data-stu-id="0cb05-133">Save hello current query file.</span></span>
2. <span data-ttu-id="0cb05-134">Aprire un file di query salvato.</span><span class="sxs-lookup"><span data-stu-id="0cb05-134">Open a saved query file.</span></span>
3. <span data-ttu-id="0cb05-135">Creare un nuovo file di query.</span><span class="sxs-lookup"><span data-stu-id="0cb05-135">Create a new query file.</span></span>

## <a name="see-hello-details"></a><span data-ttu-id="0cb05-136">Visualizzare i dettagli di hello</span><span class="sxs-lookup"><span data-stu-id="0cb05-136">See hello details</span></span>
<span data-ttu-id="0cb05-137">Espandere il relativo elenco completo delle proprietà di qualsiasi riga hello risultati toosee.</span><span class="sxs-lookup"><span data-stu-id="0cb05-137">Expand any row in hello results toosee its complete list of properties.</span></span> <span data-ttu-id="0cb05-138">È inoltre possibile espandere qualsiasi proprietà che è un valore strutturato - ad esempio, le dimensioni personalizzate o stack hello elenco un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="0cb05-138">You can further expand any property that is a structured value - for example, custom dimensions, or hello stack listing in an exception.</span></span>

![Espandere una riga](./media/app-insights-analytics-using/070.png)

## <a name="arrange-hello-results"></a><span data-ttu-id="0cb05-140">Consente di ordinare i risultati di hello</span><span class="sxs-lookup"><span data-stu-id="0cb05-140">Arrange hello results</span></span>
<span data-ttu-id="0cb05-141">È possibile ordinare, filtrare, impaginare e raggruppare i risultati di hello restituiti dalla query.</span><span class="sxs-lookup"><span data-stu-id="0cb05-141">You can sort, filter, paginate, and group hello results returned from your query.</span></span>

> [!NOTE]
> <span data-ttu-id="0cb05-142">Ordinamento, raggruppamento e applicazione di filtri nel browser hello non rieseguire la query.</span><span class="sxs-lookup"><span data-stu-id="0cb05-142">Sorting, grouping, and filtering in hello browser don't re-run your query.</span></span> <span data-ttu-id="0cb05-143">Essi ridisporre solo risultati hello che sono stati restituiti dalla query ultimo.</span><span class="sxs-lookup"><span data-stu-id="0cb05-143">They only rearrange hello results that were returned by your last query.</span></span> 
> 
> <span data-ttu-id="0cb05-144">tooperform queste attività in server hello prima vengono restituiti risultati hello, scrivere la query con hello [ordinamento](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [riepilogare](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) e [dove](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) operatori.</span><span class="sxs-lookup"><span data-stu-id="0cb05-144">tooperform these tasks in hello server before hello results are returned, write your query with hello [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) and [where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) operators.</span></span>
> 
> 

<span data-ttu-id="0cb05-145">Selezionare le colonne di hello è ad esempio toosee, trascinare toorearrange intestazioni di colonna e ridimensionamento colonne trascinandone i bordi.</span><span class="sxs-lookup"><span data-stu-id="0cb05-145">Pick hello columns you'd like toosee, drag column headers toorearrange them, and resize columns by dragging their borders.</span></span>

![Disporre le colonne](./media/app-insights-analytics-using/030.png)

### <a name="sort-and-filter-items"></a><span data-ttu-id="0cb05-147">Ordinare e filtrare elementi</span><span class="sxs-lookup"><span data-stu-id="0cb05-147">Sort and filter items</span></span>
<span data-ttu-id="0cb05-148">Ordinare i risultati facendo head hello di una colonna.</span><span class="sxs-lookup"><span data-stu-id="0cb05-148">Sort your results by clicking hello head of a column.</span></span> <span data-ttu-id="0cb05-149">Fare clic su Nuovo hello toosort altro modo, e fare clic su una terza volta toorevert toohello ordine originale restituiti dalla query.</span><span class="sxs-lookup"><span data-stu-id="0cb05-149">Click again toosort hello other way, and click a third time toorevert toohello original ordering returned by your query.</span></span>

<span data-ttu-id="0cb05-150">Utilizzare la ricerca di hello filtro icona toonarrow.</span><span class="sxs-lookup"><span data-stu-id="0cb05-150">Use hello filter icon toonarrow your search.</span></span>

![Ordinare e filtrare le colonne](./media/app-insights-analytics-using/040.png)

### <a name="group-items"></a><span data-ttu-id="0cb05-152">Raggruppare elementi</span><span class="sxs-lookup"><span data-stu-id="0cb05-152">Group items</span></span>
<span data-ttu-id="0cb05-153">toosort da più di una colonna, utilizzare il raggruppamento.</span><span class="sxs-lookup"><span data-stu-id="0cb05-153">toosort by more than one column, use grouping.</span></span> <span data-ttu-id="0cb05-154">Prima di abilitarlo e quindi trascinare le intestazioni di colonna nello spazio di hello sopra la tabella hello.</span><span class="sxs-lookup"><span data-stu-id="0cb05-154">First enable it, and then drag column headers into hello space above hello table.</span></span>

![Gruppo](./media/app-insights-analytics-using/060.png)

### <a name="missing-some-results"></a><span data-ttu-id="0cb05-156">Mancano alcuni risultati?</span><span class="sxs-lookup"><span data-stu-id="0cb05-156">Missing some results?</span></span>

<span data-ttu-id="0cb05-157">Se si ritiene che non vengono visualizzati tutti i risultati di hello che previsto, esistono due motivi possibili.</span><span class="sxs-lookup"><span data-stu-id="0cb05-157">If you think you're not seeing all hello results you expected, there are a couple of possible reasons.</span></span>

* <span data-ttu-id="0cb05-158">**Filtro intervallo di tempo**.</span><span class="sxs-lookup"><span data-stu-id="0cb05-158">**Time range filter**.</span></span> <span data-ttu-id="0cb05-159">Per impostazione predefinita, viene visualizzata solo risultati di hello ultime 24 ore.</span><span class="sxs-lookup"><span data-stu-id="0cb05-159">By default, you will only see results from hello last 24 hours.</span></span> <span data-ttu-id="0cb05-160">È un filtro automatico che limita l'intervallo di hello dei risultati che vengono recuperate dalle tabelle di origine hello.</span><span class="sxs-lookup"><span data-stu-id="0cb05-160">There is an automatic filter that limits hello range of results that are retrieved from hello source tables.</span></span> 

    <span data-ttu-id="0cb05-161">Tuttavia, è possibile modificare l'intervallo di tempo hello filtro utilizzando il menu di scelta rapida hello.</span><span class="sxs-lookup"><span data-stu-id="0cb05-161">However, you can change hello time range filter by using hello drop-down menu.</span></span>

    <span data-ttu-id="0cb05-162">Oppure è possibile eseguire l'override di intervallo automatico hello includendo la propria [ `where  ... timestamp ...` clausola](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) nella query.</span><span class="sxs-lookup"><span data-stu-id="0cb05-162">Or you can override hello automatic range by including your own [`where  ... timestamp ...` clause](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) into your query.</span></span> <span data-ttu-id="0cb05-163">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="0cb05-163">For example:</span></span>

    `requests | where timestamp > ago('2d')`

* <span data-ttu-id="0cb05-164">**Limite dei risultati**.</span><span class="sxs-lookup"><span data-stu-id="0cb05-164">**Results limit**.</span></span> <span data-ttu-id="0cb05-165">È previsto un limite di 10 righe k hello risultati restituiti dal portale hello.</span><span class="sxs-lookup"><span data-stu-id="0cb05-165">There's a limit of about 10k rows on hello results returned from hello portal.</span></span> <span data-ttu-id="0cb05-166">Un messaggio di avviso Mostra se è passare supera il limite di hello.</span><span class="sxs-lookup"><span data-stu-id="0cb05-166">A warning shows if you go over hello limit.</span></span> <span data-ttu-id="0cb05-167">In tal caso, ordinare i risultati nella tabella hello non Mostra sempre si tutti hello primo o ultimi risultati effettivi.</span><span class="sxs-lookup"><span data-stu-id="0cb05-167">If that happens, sorting your results in hello table won't always show you all hello actual first or last results.</span></span> 

    <span data-ttu-id="0cb05-168">È di buona norma tooavoid che colpisce hello limite.</span><span class="sxs-lookup"><span data-stu-id="0cb05-168">It's good practice tooavoid hitting hello limit.</span></span> <span data-ttu-id="0cb05-169">Utilizzare filtro di intervallo di tempo hello oppure utilizzare gli operatori, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="0cb05-169">Use hello time range filter, or use operators such as:</span></span>

  * [<span data-ttu-id="0cb05-170">timestamp top 100 by</span><span class="sxs-lookup"><span data-stu-id="0cb05-170">top 100 by timestamp</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) 
  * [<span data-ttu-id="0cb05-171">take 100</span><span class="sxs-lookup"><span data-stu-id="0cb05-171">take 100</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html)
  * [<span data-ttu-id="0cb05-172">summarize </span><span class="sxs-lookup"><span data-stu-id="0cb05-172">summarize </span></span>](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) 
  * [<span data-ttu-id="0cb05-173">where timestamp > ago(3d)</span><span class="sxs-lookup"><span data-stu-id="0cb05-173">where timestamp > ago(3d)</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html)

<span data-ttu-id="0cb05-174">Per visualizzare più di 10.000 righe,</span><span class="sxs-lookup"><span data-stu-id="0cb05-174">(Want more than 10k rows?</span></span> <span data-ttu-id="0cb05-175">è consigliabile usare [Esportazione continua](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="0cb05-175">Consider using [Continuous Export](app-insights-export-telemetry.md) instead.</span></span> <span data-ttu-id="0cb05-176">Analytics è progettato per l'analisi e non per il recupero di dati non elaborati.</span><span class="sxs-lookup"><span data-stu-id="0cb05-176">Analytics is designed for analysis, rather than retrieving raw data.)</span></span>

## <a name="diagrams"></a><span data-ttu-id="0cb05-177">Diagrammi</span><span class="sxs-lookup"><span data-stu-id="0cb05-177">Diagrams</span></span>
<span data-ttu-id="0cb05-178">Selezionare il tipo di hello di diagramma che si desidera:</span><span class="sxs-lookup"><span data-stu-id="0cb05-178">Select hello type of diagram you'd like:</span></span>

![Selezionare un tipo di diagramma](./media/app-insights-analytics-using/230.png)

<span data-ttu-id="0cb05-180">Se si dispone di diverse colonne di tipi di destra hello, è possibile scegliere hello x e gli assi y e una colonna di dimensioni toosplit hello risultati.</span><span class="sxs-lookup"><span data-stu-id="0cb05-180">If you have several columns of hello right types, you can choose hello x and y axes, and a column of dimensions toosplit hello results by.</span></span>

<span data-ttu-id="0cb05-181">Per impostazione predefinita, risultati vengono inizialmente visualizzati in una tabella e si seleziona il diagramma hello manualmente.</span><span class="sxs-lookup"><span data-stu-id="0cb05-181">By default, results are initially displayed as a table, and you select hello diagram manually.</span></span> <span data-ttu-id="0cb05-182">Ma è possibile utilizzare hello [rendering direttiva](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) alla fine hello tooselect una query un diagramma.</span><span class="sxs-lookup"><span data-stu-id="0cb05-182">But you can use hello [render directive](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) at hello end of a query tooselect a diagram.</span></span>

### <a name="analytics-diagnostics"></a><span data-ttu-id="0cb05-183">Diagnostica di Analytics</span><span class="sxs-lookup"><span data-stu-id="0cb05-183">Analytics diagnostics</span></span>


<span data-ttu-id="0cb05-184">In un timechart, se è presente un improvviso picco o un passaggio nei dati, si può vedere un punto evidenziato nella riga hello.</span><span class="sxs-lookup"><span data-stu-id="0cb05-184">On a timechart, if there is a sudden spike or step in your data, you may see a highlighted point on hello line.</span></span> <span data-ttu-id="0cb05-185">Ciò indica che una combinazione di proprietà che filtrano tutte le modifiche improvvise hello è identificato da diagnostica Analitica.</span><span class="sxs-lookup"><span data-stu-id="0cb05-185">This indicates that Analytics Diagnostics has identified a combination of properties that filter out hello sudden change.</span></span> <span data-ttu-id="0cb05-186">Fare clic su hello punto tooget per ulteriori dettagli sul filtro hello e toosee hello filtrato versione.</span><span class="sxs-lookup"><span data-stu-id="0cb05-186">Click hello point tooget more detail on hello filter, and toosee hello filtered version.</span></span> <span data-ttu-id="0cb05-187">Questo può consentire di identificare quale modifica hello causato.</span><span class="sxs-lookup"><span data-stu-id="0cb05-187">This may help you identify what caused hello change.</span></span> 

[<span data-ttu-id="0cb05-188">Altre informazioni sulla Diagnostica di Analytics</span><span class="sxs-lookup"><span data-stu-id="0cb05-188">Learn more about Analytics Diagnostics</span></span>](app-insights-analytics-diagnostics.md)


![Diagnostica di Analytics](./media/app-insights-analytics-using/analytics-diagnostics.png)

## <a name="pin-toodashboard"></a><span data-ttu-id="0cb05-190">PIN toodashboard</span><span class="sxs-lookup"><span data-stu-id="0cb05-190">Pin toodashboard</span></span>
<span data-ttu-id="0cb05-191">È possibile aggiungere una tabella o diagramma tooone del [dashboard condiviso](app-insights-dashboards.md) -sufficiente fare clic su Aggiungi hello.</span><span class="sxs-lookup"><span data-stu-id="0cb05-191">You can pin a diagram or table tooone of your [shared dashboards](app-insights-dashboards.md) - just click hello pin.</span></span> <span data-ttu-id="0cb05-192">(Potrebbe essere troppo[aggiornamento applicazione del pacchetto di prezzi](app-insights-pricing.md) tooturn su questa funzionalità.)</span><span class="sxs-lookup"><span data-stu-id="0cb05-192">(You might need too[upgrade your app's pricing package](app-insights-pricing.md) tooturn on this feature.)</span></span> 

![Fare clic su hello pin](./media/app-insights-analytics-using/pin-01.png)

<span data-ttu-id="0cb05-194">Ciò significa che, quando si crea un dashboard toohelp è monitorare le prestazioni di hello o utilizzo dei servizi web, è possibile includere piuttosto complessa analisi insieme hello altre metriche.</span><span class="sxs-lookup"><span data-stu-id="0cb05-194">This means that, when you put together a dashboard toohelp you monitor hello performance or usage of your web services, you can include quite complex analysis alongside hello other metrics.</span></span> 

<span data-ttu-id="0cb05-195">È possibile aggiungere un dashboard toohello tabella, se sono presenti un massimo di quattro colonne.</span><span class="sxs-lookup"><span data-stu-id="0cb05-195">You can pin a table toohello dashboard, if it has four or fewer columns.</span></span> <span data-ttu-id="0cb05-196">Vengono visualizzate solo hello prime sette righe.</span><span class="sxs-lookup"><span data-stu-id="0cb05-196">Only hello top seven rows are displayed.</span></span>

### <a name="dashboard-refresh"></a><span data-ttu-id="0cb05-197">Aggiornamento del dashboard</span><span class="sxs-lookup"><span data-stu-id="0cb05-197">Dashboard refresh</span></span>
<span data-ttu-id="0cb05-198">Hello grafico aggiunto toohello dashboard vengono aggiornati automaticamente eseguendo di nuovo la query hello ogni ore circa.</span><span class="sxs-lookup"><span data-stu-id="0cb05-198">hello chart pinned toohello dashboard is refreshed automatically by re-running hello query approximately every hours.</span></span> <span data-ttu-id="0cb05-199">È anche possibile fare clic su pulsante Aggiorna hello.</span><span class="sxs-lookup"><span data-stu-id="0cb05-199">You can also click hello Refresh button.</span></span>

### <a name="automatic-simplifications"></a><span data-ttu-id="0cb05-200">Semplificazioni automatiche</span><span class="sxs-lookup"><span data-stu-id="0cb05-200">Automatic simplifications</span></span>

<span data-ttu-id="0cb05-201">Certi semplificazione grafico tooa applicato quando si aggiunge il dashboard tooa.</span><span class="sxs-lookup"><span data-stu-id="0cb05-201">Certain simplifications are applied tooa chart when you pin it tooa dashboard.</span></span>

<span data-ttu-id="0cb05-202">**Limitazione di tempo:** le query sono automaticamente limitato toohello negli ultimi 14 giorni.</span><span class="sxs-lookup"><span data-stu-id="0cb05-202">**Time restriction:** Queries are automatically limited toohello past 14 days.</span></span> <span data-ttu-id="0cb05-203">Hello effetto è hello stesso come se la query include `where timestamp > ago(14d)`.</span><span class="sxs-lookup"><span data-stu-id="0cb05-203">hello effect is hello same as if your query includes `where timestamp > ago(14d)`.</span></span>

<span data-ttu-id="0cb05-204">**Restrizione del conteggio di bin:** se si visualizza un grafico che dispone di molti bin discreti (in genere un grafico a barre) hello meno bin popolati automaticamente sono raggruppati in un singolo "altri" bin.</span><span class="sxs-lookup"><span data-stu-id="0cb05-204">**Bin count restriction:** If you display a chart that has a lot of discrete bins (typically a bar chart), hello less populated bins are automatically grouped into a single "others" bin.</span></span> <span data-ttu-id="0cb05-205">Ad esempio, questa query:</span><span class="sxs-lookup"><span data-stu-id="0cb05-205">For example, this query:</span></span>

    requests | summarize count_search = count() by client_CountryOrRegion

<span data-ttu-id="0cb05-206">ha questo aspetto in Analisi:</span><span class="sxs-lookup"><span data-stu-id="0cb05-206">looks like this in Analytics:</span></span>

![Grafico con una lunga coda](./media/app-insights-analytics-using/pin-07.png)

<span data-ttu-id="0cb05-208">Tuttavia, quando si aggiunge tooa dashboard, simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="0cb05-208">but when you pin it tooa dashboard, it looks like this:</span></span>

![Grafico con bin limitati](./media/app-insights-analytics-using/pin-08.png)

## <a name="export-tooexcel"></a><span data-ttu-id="0cb05-210">Esportazione tooExcel</span><span class="sxs-lookup"><span data-stu-id="0cb05-210">Export tooExcel</span></span>
<span data-ttu-id="0cb05-211">Dopo aver eseguito una query, è possibile scaricare un file con estensione csv.</span><span class="sxs-lookup"><span data-stu-id="0cb05-211">After you've run a query, you can download a .csv file.</span></span> <span data-ttu-id="0cb05-212">Fare clic su **Esporta in Excel**.</span><span class="sxs-lookup"><span data-stu-id="0cb05-212">Click **Export,  Excel**.</span></span>

## <a name="export-toopower-bi"></a><span data-ttu-id="0cb05-213">Esportazione tooPower BI</span><span class="sxs-lookup"><span data-stu-id="0cb05-213">Export tooPower BI</span></span>
<span data-ttu-id="0cb05-214">Posizionare il cursore di hello in una query e scegliere **esportare, Power BI**.</span><span class="sxs-lookup"><span data-stu-id="0cb05-214">Put hello cursor in a query and choose **Export, Power BI**.</span></span>

![Esportazione da Analitica tooPower BI](./media/app-insights-analytics-using/240.png)

<span data-ttu-id="0cb05-216">Eseguire query hello in Power BI.</span><span class="sxs-lookup"><span data-stu-id="0cb05-216">You run hello query in Power BI.</span></span> <span data-ttu-id="0cb05-217">È possibile impostare toorefresh su una pianificazione.</span><span class="sxs-lookup"><span data-stu-id="0cb05-217">You can set it toorefresh on a schedule.</span></span>

<span data-ttu-id="0cb05-218">Con Power BI, è possibile creare i dashboard per raggruppare i dati da un'ampia gamma di origini.</span><span class="sxs-lookup"><span data-stu-id="0cb05-218">With Power BI, you can create dashboards that bring together data from a wide variety of sources.</span></span>

[<span data-ttu-id="0cb05-219">Ulteriori informazioni sull'esportazione tooPower BI</span><span class="sxs-lookup"><span data-stu-id="0cb05-219">Learn more about export tooPower BI</span></span>](app-insights-export-power-bi.md)

## <a name="deep-link"></a><span data-ttu-id="0cb05-220">Collegamento diretto</span><span class="sxs-lookup"><span data-stu-id="0cb05-220">Deep link</span></span>

<span data-ttu-id="0cb05-221">Ottenere un collegamento in **esportazione, il collegamento di condivisione** che è possibile inviare tooanother utente.</span><span class="sxs-lookup"><span data-stu-id="0cb05-221">Get a link under **Export, Share link** that you can send tooanother user.</span></span> <span data-ttu-id="0cb05-222">Fornito contiene utente hello [gruppo di risorse di accesso tooyour](app-insights-resources-roles-access-control.md), hello query verrà aperta in hello UI Analitica.</span><span class="sxs-lookup"><span data-stu-id="0cb05-222">Provided hello user has [access tooyour resource group](app-insights-resources-roles-access-control.md), hello query will open in hello Analytics UI.</span></span>

<span data-ttu-id="0cb05-223">(Collegamento hello, viene visualizzato il testo della query hello dopo "? q =", la compressione gzip e con codifica base 64.</span><span class="sxs-lookup"><span data-stu-id="0cb05-223">(In hello link, hello query text appears after "?q=", gzip compressed and base-64 encoded.</span></span> <span data-ttu-id="0cb05-224">È possibile scrivere i collegamenti diretti di codice toogenerate fornire toousers.</span><span class="sxs-lookup"><span data-stu-id="0cb05-224">You could write code toogenerate deep links that you provide toousers.</span></span> <span data-ttu-id="0cb05-225">Tuttavia, hello consigliato modo toorun Analitica dal codice consiste nell'utilizzare hello [API REST](https://dev.applicationinsights.io/).)</span><span class="sxs-lookup"><span data-stu-id="0cb05-225">However, hello recommended way toorun Analytics from code is by using hello [REST API](https://dev.applicationinsights.io/).)</span></span>


## <a name="automation"></a><span data-ttu-id="0cb05-226">Automazione</span><span class="sxs-lookup"><span data-stu-id="0cb05-226">Automation</span></span>

<span data-ttu-id="0cb05-227">Hello utilizzare [API REST di accesso ai dati](https://dev.applicationinsights.io/) query Analitica toorun.</span><span class="sxs-lookup"><span data-stu-id="0cb05-227">Use hello  [Data Access REST API](https://dev.applicationinsights.io/) toorun Analytics queries.</span></span> <span data-ttu-id="0cb05-228">[Ad esempio](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (con PowerShell):</span><span class="sxs-lookup"><span data-stu-id="0cb05-228">[For example](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (using PowerShell):</span></span>

```PS
curl "https://api.applicationinsights.io/beta/apps/DEMO_APP/query?query=requests%7C%20where%20timestamp%20%3E%3D%20ago(24h)%7C%20count" -H "x-api-key: DEMO_KEY"
```

<span data-ttu-id="0cb05-229">A differenza dell'interfaccia utente Analitica hello, hello API REST non aggiunge automaticamente tutte le query tooyour limitazione di timestamp.</span><span class="sxs-lookup"><span data-stu-id="0cb05-229">Unlike hello Analytics UI, hello REST API does not automatically add any timestamp limitation tooyour queries.</span></span> <span data-ttu-id="0cb05-230">Tenere presente che tooadd la propria clausola where, tooavoid ottenere le risposte di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="0cb05-230">Remember tooadd your own where-clause, tooavoid getting huge responses.</span></span>



## <a name="import-data"></a><span data-ttu-id="0cb05-231">Importa dati</span><span class="sxs-lookup"><span data-stu-id="0cb05-231">Import data</span></span>

<span data-ttu-id="0cb05-232">È possibile importare i dati da un file CSV.</span><span class="sxs-lookup"><span data-stu-id="0cb05-232">You can import data from a CSV file.</span></span> <span data-ttu-id="0cb05-233">Un utilizzo tipico è tooimport i dati statici che è possibile unire le tabelle di dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="0cb05-233">A typical usage is tooimport static data that you can join with tables from your telemetry.</span></span> 

<span data-ttu-id="0cb05-234">Ad esempio, se gli utenti autenticati vengono rilevati nei dati di telemetria da un alias o un id offuscato, è possibile importare una tabella che mappa i nomi di alias tooreal.</span><span class="sxs-lookup"><span data-stu-id="0cb05-234">For example, if authenticated users are identified in your telemetry by an alias or obfuscated id, you could import a table that maps aliases tooreal names.</span></span> <span data-ttu-id="0cb05-235">Eseguendo un join su dati di telemetria di hello richiesta, è possibile identificare gli utenti con i relativi nomi reali nei report Analitica hello.</span><span class="sxs-lookup"><span data-stu-id="0cb05-235">By performing a join on hello request telemetry, you can identify users by their real names in hello Analytics reports.</span></span>

### <a name="define-your-data-schema"></a><span data-ttu-id="0cb05-236">Definire lo schema dei dati</span><span class="sxs-lookup"><span data-stu-id="0cb05-236">Define your data schema</span></span>

1. <span data-ttu-id="0cb05-237">Fare clic su **Impostazioni** (in alto a sinistra) e quindi su **Origini dati**.</span><span class="sxs-lookup"><span data-stu-id="0cb05-237">Click **Settings** (at top left) and then **Data Sources**.</span></span> 
2. <span data-ttu-id="0cb05-238">Aggiungere un'origine dati, attenendosi alle istruzioni hello.</span><span class="sxs-lookup"><span data-stu-id="0cb05-238">Add a data source, following hello instructions.</span></span> <span data-ttu-id="0cb05-239">Si è richiesto toosupply un campione di dati di hello, che devono includere almeno dieci righe.</span><span class="sxs-lookup"><span data-stu-id="0cb05-239">You are asked toosupply a sample of hello data, which should include at least ten rows.</span></span> <span data-ttu-id="0cb05-240">È quindi possibile correggere schema hello.</span><span class="sxs-lookup"><span data-stu-id="0cb05-240">You then correct hello schema.</span></span>

<span data-ttu-id="0cb05-241">Definisce un'origine dati, che è possibile quindi utilizzare tooimport singole tabelle.</span><span class="sxs-lookup"><span data-stu-id="0cb05-241">This defines a data source, which you can then use tooimport individual tables.</span></span>

### <a name="import-a-table"></a><span data-ttu-id="0cb05-242">Importare una tabella</span><span class="sxs-lookup"><span data-stu-id="0cb05-242">Import a table</span></span>

1. <span data-ttu-id="0cb05-243">Aprire la definizione dell'origine dati dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="0cb05-243">Open your data source definition from hello list.</span></span>
2. <span data-ttu-id="0cb05-244">Fare clic su "Carica" e seguono hello istruzioni tooupload hello tabella.</span><span class="sxs-lookup"><span data-stu-id="0cb05-244">Click "Upload" and follow hello instructions tooupload hello table.</span></span> <span data-ttu-id="0cb05-245">Ciò comporta un tooa chiamata API REST e pertanto, è facile tooautomate.</span><span class="sxs-lookup"><span data-stu-id="0cb05-245">This involves a call tooa REST API, and so it is easy tooautomate.</span></span> 

<span data-ttu-id="0cb05-246">La tabella è ora disponibile per l'utilizzo nelle query di Analytics.</span><span class="sxs-lookup"><span data-stu-id="0cb05-246">Your table is now available for use in Analytics queries.</span></span> <span data-ttu-id="0cb05-247">Verrà visualizzata in Analytics</span><span class="sxs-lookup"><span data-stu-id="0cb05-247">It will appear in Analytics</span></span> 

### <a name="use-hello-table"></a><span data-ttu-id="0cb05-248">Utilizzare tabella hello</span><span class="sxs-lookup"><span data-stu-id="0cb05-248">Use hello table</span></span>

<span data-ttu-id="0cb05-249">Si supponga che la definizione dell'origine dati sia denominata `usermap` e che abbia due campi, `realName` e `user_AuthenticatedId`.</span><span class="sxs-lookup"><span data-stu-id="0cb05-249">Let's suppose your data source definition is called `usermap`, and that it has two fields, `realName` and `user_AuthenticatedId`.</span></span> <span data-ttu-id="0cb05-250">Hello `requests` tabella include anche un campo denominato `user_AuthenticatedId`, pertanto è facile toojoin loro:</span><span class="sxs-lookup"><span data-stu-id="0cb05-250">hello `requests` table also has a field named `user_AuthenticatedId`, so it's easy toojoin them:</span></span>

```AIQL

    requests
    | where notempty(user_AuthenticatedId) | take 10
    | join kind=leftouter ( usermap ) on user_AuthenticatedId 
```
<span data-ttu-id="0cb05-251">la tabella risultante di richieste Hello è una colonna aggiuntiva, `realName`.</span><span class="sxs-lookup"><span data-stu-id="0cb05-251">hello resulting table of requests has an additional column, `realName`.</span></span>

### <a name="import-from-logstash"></a><span data-ttu-id="0cb05-252">Importare da LogStash</span><span class="sxs-lookup"><span data-stu-id="0cb05-252">Import from LogStash</span></span>

<span data-ttu-id="0cb05-253">Se si utilizza [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), è possibile utilizzare i log tooquery Analitica.</span><span class="sxs-lookup"><span data-stu-id="0cb05-253">If you use [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), you can use Analytics tooquery your logs.</span></span> <span data-ttu-id="0cb05-254">Hello utilizzare [plug-in che invia i dati in Analitica](https://github.com/Microsoft/logstash-output-application-insights).</span><span class="sxs-lookup"><span data-stu-id="0cb05-254">Use hello [plugin that pipes data into Analytics](https://github.com/Microsoft/logstash-output-application-insights).</span></span> 

## <a name="video"></a><span data-ttu-id="0cb05-255">Video</span><span class="sxs-lookup"><span data-stu-id="0cb05-255">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

