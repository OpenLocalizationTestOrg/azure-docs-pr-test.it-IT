---
title: 'Uso di Analytics: il potente strumento di ricerca di Azure Application Insights | Microsoft Docs'
description: 'Utilizzare Analytics: lo strumento di ricerca diagnostica incluso in Application Insights '
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
ms.openlocfilehash: 9f7c1744db52b1c2f374fd5655e2c66b5f61bacf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="using-analytics-in-application-insights"></a><span data-ttu-id="fb31a-103">Uso di Analytics in Application Insights</span><span class="sxs-lookup"><span data-stu-id="fb31a-103">Using Analytics in Application Insights</span></span>
<span data-ttu-id="fb31a-104">L'[analisi](app-insights-analytics.md) è lo strumento di ricerca avanzato incluso in [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fb31a-104">[Analytics](app-insights-analytics.md) is the powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="fb31a-105">Queste pagine descrivono il linguaggio di query di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="fb31a-105">These pages describe the Log Analytics query language.</span></span>

* <span data-ttu-id="fb31a-106">**[Guardare il video introduttivo](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="fb31a-106">**[Watch the introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="fb31a-107">**[Eseguire la versione di test di Analisi sui dati simulati](https://analytics.applicationinsights.io/demo)** se l'app non invia ancora i dati ad Application Insights.</span><span class="sxs-lookup"><span data-stu-id="fb31a-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data to Application Insights yet.</span></span>

## <a name="open-analytics"></a><span data-ttu-id="fb31a-108">Aprire Analytics</span><span class="sxs-lookup"><span data-stu-id="fb31a-108">Open Analytics</span></span>
<span data-ttu-id="fb31a-109">Nella home page dell'app in Application Insights fare clic su Analytics.</span><span class="sxs-lookup"><span data-stu-id="fb31a-109">From your app's home resource in Application Insights, click Analytics.</span></span>

![In portal.azure.com, aprire la risorsa di Application Insights e selezionare Analytics.](./media/app-insights-analytics-using/001.png)

<span data-ttu-id="fb31a-111">L'esercitazione inline fornisce alcune informazioni su come procedere.</span><span class="sxs-lookup"><span data-stu-id="fb31a-111">The inline tutorial gives you some ideas about what you can do.</span></span>

<span data-ttu-id="fb31a-112">È disponibile una [panoramica più ampia qui](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="fb31a-112">There's a [more extensive tour here](app-insights-analytics-tour.md).</span></span>

## <a name="query-your-telemetry"></a><span data-ttu-id="fb31a-113">Eseguire query sui dati di telemetria</span><span class="sxs-lookup"><span data-stu-id="fb31a-113">Query your telemetry</span></span>
### <a name="write-a-query"></a><span data-ttu-id="fb31a-114">Scrivere una query</span><span class="sxs-lookup"><span data-stu-id="fb31a-114">Write a query</span></span>
![Visualizzazione schema](./media/app-insights-analytics-using/150.png)

<span data-ttu-id="fb31a-116">Iniziare con i nomi delle tabelle elencate a sinistra oppure con l'operatore [range](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) o [union](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html).</span><span class="sxs-lookup"><span data-stu-id="fb31a-116">Begin with the names of any of the tables listed on the left (or the [range](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) or [union](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) operators).</span></span> <span data-ttu-id="fb31a-117">Usare `|` per creare una pipeline di [operatori](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html).</span><span class="sxs-lookup"><span data-stu-id="fb31a-117">Use `|` to create a pipeline of [operators](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html).</span></span> 

<span data-ttu-id="fb31a-118">IntelliSense suggerisce gli operatori e gli elementi delle espressioni che è possibile usare.</span><span class="sxs-lookup"><span data-stu-id="fb31a-118">IntelliSense prompts you with the operators and the expression elements that you can use.</span></span> <span data-ttu-id="fb31a-119">Fare clic sull'icona informazioni o premere CTRL+BARRA SPAZIATRICE per una descrizione più dettagliata ed esempi di utilizzo di ogni elemento.</span><span class="sxs-lookup"><span data-stu-id="fb31a-119">Click the information icon (or press CTRL+Space) to get a longer description and examples of how to use each element.</span></span>

<span data-ttu-id="fb31a-120">Vedere la [panoramica del linguaggio di Analytics](app-insights-analytics-tour.md) e le [informazioni di riferimento sul linguaggio](app-insights-analytics-reference.md).</span><span class="sxs-lookup"><span data-stu-id="fb31a-120">See the [Analytics language tour](app-insights-analytics-tour.md) and [language reference](app-insights-analytics-reference.md).</span></span>

### <a name="run-a-query"></a><span data-ttu-id="fb31a-121">Eseguire una query</span><span class="sxs-lookup"><span data-stu-id="fb31a-121">Run a query</span></span>
![Esecuzione di una query](./media/app-insights-analytics-using/130.png)

1. <span data-ttu-id="fb31a-123">Nelle query è possibile usare interruzioni di riga.</span><span class="sxs-lookup"><span data-stu-id="fb31a-123">You can use single line breaks in a query.</span></span>
2. <span data-ttu-id="fb31a-124">Posizionare il cursore all'interno o alla fine della query da eseguire.</span><span class="sxs-lookup"><span data-stu-id="fb31a-124">Put the cursor inside or at the end of the query you want to run.</span></span>
3. <span data-ttu-id="fb31a-125">Controllare l'intervallo di tempo della query.</span><span class="sxs-lookup"><span data-stu-id="fb31a-125">Check the time range of your query.</span></span> <span data-ttu-id="fb31a-126">È possibile modificarlo o ignorarlo inserendo la propria clausola [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) nella query.</span><span class="sxs-lookup"><span data-stu-id="fb31a-126">(You can change it, or override it by including your own [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) clause in your query.)</span></span>
3. <span data-ttu-id="fb31a-127">Fare clic su Vai per eseguire la query.</span><span class="sxs-lookup"><span data-stu-id="fb31a-127">Click Go to run the query.</span></span>
4. <span data-ttu-id="fb31a-128">Non inserire righe vuote nella query.</span><span class="sxs-lookup"><span data-stu-id="fb31a-128">Don't put blank lines in your query.</span></span> <span data-ttu-id="fb31a-129">È possibile mantenere più query separate in un'unica scheda di query, separandole con righe vuote.</span><span class="sxs-lookup"><span data-stu-id="fb31a-129">You can keep several separated queries in one query tab by separating them with blank lines.</span></span> <span data-ttu-id="fb31a-130">Viene eseguita solo la query con il cursore.</span><span class="sxs-lookup"><span data-stu-id="fb31a-130">Only the query that has the cursor runs.</span></span>

### <a name="save-a-query"></a><span data-ttu-id="fb31a-131">Salvare una query</span><span class="sxs-lookup"><span data-stu-id="fb31a-131">Save a query</span></span>
![Salvataggio di una query](./media/app-insights-analytics-using/140.png)

1. <span data-ttu-id="fb31a-133">Salvare il file di query corrente.</span><span class="sxs-lookup"><span data-stu-id="fb31a-133">Save the current query file.</span></span>
2. <span data-ttu-id="fb31a-134">Aprire un file di query salvato.</span><span class="sxs-lookup"><span data-stu-id="fb31a-134">Open a saved query file.</span></span>
3. <span data-ttu-id="fb31a-135">Creare un nuovo file di query.</span><span class="sxs-lookup"><span data-stu-id="fb31a-135">Create a new query file.</span></span>

## <a name="see-the-details"></a><span data-ttu-id="fb31a-136">Visualizzare i dettagli</span><span class="sxs-lookup"><span data-stu-id="fb31a-136">See the details</span></span>
<span data-ttu-id="fb31a-137">Espandere una riga dei risultati per visualizzarne l'elenco completo delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="fb31a-137">Expand any row in the results to see its complete list of properties.</span></span> <span data-ttu-id="fb31a-138">È possibile espandere ulteriormente qualsiasi proprietà che sia un valore strutturato, ad esempio le dimensioni personalizzate o l'elenco in pila di un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="fb31a-138">You can further expand any property that is a structured value - for example, custom dimensions, or the stack listing in an exception.</span></span>

![Espandere una riga](./media/app-insights-analytics-using/070.png)

## <a name="arrange-the-results"></a><span data-ttu-id="fb31a-140">Disporre i risultati</span><span class="sxs-lookup"><span data-stu-id="fb31a-140">Arrange the results</span></span>
<span data-ttu-id="fb31a-141">È possibile ordinare, filtrare, impaginare e raggruppare i risultati restituiti dalla query.</span><span class="sxs-lookup"><span data-stu-id="fb31a-141">You can sort, filter, paginate, and group the results returned from your query.</span></span>

> [!NOTE]
> <span data-ttu-id="fb31a-142">Le operazioni di ordinamento, raggruppamento e filtro nel browser non eseguono nuovamente la query,</span><span class="sxs-lookup"><span data-stu-id="fb31a-142">Sorting, grouping, and filtering in the browser don't re-run your query.</span></span> <span data-ttu-id="fb31a-143">ma riorganizzano i risultati restituiti dall'ultima query.</span><span class="sxs-lookup"><span data-stu-id="fb31a-143">They only rearrange the results that were returned by your last query.</span></span> 
> 
> <span data-ttu-id="fb31a-144">Per eseguire queste attività nel server prima che vengano restituiti i risultati, scrivere la query usando gli operatori [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) e [where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html).</span><span class="sxs-lookup"><span data-stu-id="fb31a-144">To perform these tasks in the server before the results are returned, write your query with the [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) and [where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) operators.</span></span>
> 
> 

<span data-ttu-id="fb31a-145">Selezionare le colonne da visualizzare, trascinare le intestazioni di colonna per ridisporle e ridimensionare le colonne trascinandone i bordi.</span><span class="sxs-lookup"><span data-stu-id="fb31a-145">Pick the columns you'd like to see, drag column headers to rearrange them, and resize columns by dragging their borders.</span></span>

![Disporre le colonne](./media/app-insights-analytics-using/030.png)

### <a name="sort-and-filter-items"></a><span data-ttu-id="fb31a-147">Ordinare e filtrare elementi</span><span class="sxs-lookup"><span data-stu-id="fb31a-147">Sort and filter items</span></span>
<span data-ttu-id="fb31a-148">Ordinare i risultati facendo clic sull'intestazione di una colonna.</span><span class="sxs-lookup"><span data-stu-id="fb31a-148">Sort your results by clicking the head of a column.</span></span> <span data-ttu-id="fb31a-149">Fare clic di nuovo per applicare l'ordinamento opposto. Fare clic una terza volta per ripristinare l'ordine originale restituito dalla query.</span><span class="sxs-lookup"><span data-stu-id="fb31a-149">Click again to sort the other way, and click a third time to revert to the original ordering returned by your query.</span></span>

<span data-ttu-id="fb31a-150">Usare l'icona del filtro per perfezionare la ricerca.</span><span class="sxs-lookup"><span data-stu-id="fb31a-150">Use the filter icon to narrow your search.</span></span>

![Ordinare e filtrare le colonne](./media/app-insights-analytics-using/040.png)

### <a name="group-items"></a><span data-ttu-id="fb31a-152">Raggruppare elementi</span><span class="sxs-lookup"><span data-stu-id="fb31a-152">Group items</span></span>
<span data-ttu-id="fb31a-153">Per ordinare più di una colonna, usare il raggruppamento.</span><span class="sxs-lookup"><span data-stu-id="fb31a-153">To sort by more than one column, use grouping.</span></span> <span data-ttu-id="fb31a-154">Abilitare il raggruppamento e quindi trascinare le intestazioni di colonna nello spazio sopra la tabella.</span><span class="sxs-lookup"><span data-stu-id="fb31a-154">First enable it, and then drag column headers into the space above the table.</span></span>

![Gruppo](./media/app-insights-analytics-using/060.png)

### <a name="missing-some-results"></a><span data-ttu-id="fb31a-156">Mancano alcuni risultati?</span><span class="sxs-lookup"><span data-stu-id="fb31a-156">Missing some results?</span></span>

<span data-ttu-id="fb31a-157">Se si ritiene che non siano visualizzati tutti i risultati previsti, esistono un paio di possibili motivi.</span><span class="sxs-lookup"><span data-stu-id="fb31a-157">If you think you're not seeing all the results you expected, there are a couple of possible reasons.</span></span>

* <span data-ttu-id="fb31a-158">**Filtro intervallo di tempo**.</span><span class="sxs-lookup"><span data-stu-id="fb31a-158">**Time range filter**.</span></span> <span data-ttu-id="fb31a-159">Per impostazione predefinita, vengono visualizzati solo i risultati delle ultime 24 ore.</span><span class="sxs-lookup"><span data-stu-id="fb31a-159">By default, you will only see results from the last 24 hours.</span></span> <span data-ttu-id="fb31a-160">È presente un filtro automatico che limita l'intervallo dei risultati recuperati dalle tabelle di origine.</span><span class="sxs-lookup"><span data-stu-id="fb31a-160">There is an automatic filter that limits the range of results that are retrieved from the source tables.</span></span> 

    <span data-ttu-id="fb31a-161">È possibile tuttavia modificare il filtro intervallo di tempo usando il menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="fb31a-161">However, you can change the time range filter by using the drop-down menu.</span></span>

    <span data-ttu-id="fb31a-162">In alternativa, è possibile ignorare l'intervallo automatico inserendo la propria clausola [`where  ... timestamp ...` ](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) nella query.</span><span class="sxs-lookup"><span data-stu-id="fb31a-162">Or you can override the automatic range by including your own [`where  ... timestamp ...` clause](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) into your query.</span></span> <span data-ttu-id="fb31a-163">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="fb31a-163">For example:</span></span>

    `requests | where timestamp > ago('2d')`

* <span data-ttu-id="fb31a-164">**Limite dei risultati**.</span><span class="sxs-lookup"><span data-stu-id="fb31a-164">**Results limit**.</span></span> <span data-ttu-id="fb31a-165">È previsto un limite di 10.000 righe di risultati restituiti dal portale.</span><span class="sxs-lookup"><span data-stu-id="fb31a-165">There's a limit of about 10k rows on the results returned from the portal.</span></span> <span data-ttu-id="fb31a-166">Se il numero di risultati supera il limite, verrà visualizzato un avviso.</span><span class="sxs-lookup"><span data-stu-id="fb31a-166">A warning shows if you go over the limit.</span></span> <span data-ttu-id="fb31a-167">In tal caso, l'ordinamento dei risultati nella tabella non permette sempre di visualizzare i primo o gli ultimi risultati effettivi.</span><span class="sxs-lookup"><span data-stu-id="fb31a-167">If that happens, sorting your results in the table won't always show you all the actual first or last results.</span></span> 

    <span data-ttu-id="fb31a-168">È consigliabile evitare di raggiungere il limite.</span><span class="sxs-lookup"><span data-stu-id="fb31a-168">It's good practice to avoid hitting the limit.</span></span> <span data-ttu-id="fb31a-169">Usare il filtro intervallo di tempo oppure usare gli operatori, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="fb31a-169">Use the time range filter, or use operators such as:</span></span>

  * [<span data-ttu-id="fb31a-170">timestamp top 100 by</span><span class="sxs-lookup"><span data-stu-id="fb31a-170">top 100 by timestamp</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) 
  * [<span data-ttu-id="fb31a-171">take 100</span><span class="sxs-lookup"><span data-stu-id="fb31a-171">take 100</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html)
  * [<span data-ttu-id="fb31a-172">summarize </span><span class="sxs-lookup"><span data-stu-id="fb31a-172">summarize </span></span>](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) 
  * [<span data-ttu-id="fb31a-173">where timestamp > ago(3d)</span><span class="sxs-lookup"><span data-stu-id="fb31a-173">where timestamp > ago(3d)</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html)

<span data-ttu-id="fb31a-174">Per visualizzare più di 10.000 righe,</span><span class="sxs-lookup"><span data-stu-id="fb31a-174">(Want more than 10k rows?</span></span> <span data-ttu-id="fb31a-175">è consigliabile usare [Esportazione continua](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="fb31a-175">Consider using [Continuous Export](app-insights-export-telemetry.md) instead.</span></span> <span data-ttu-id="fb31a-176">Analytics è progettato per l'analisi e non per il recupero di dati non elaborati.</span><span class="sxs-lookup"><span data-stu-id="fb31a-176">Analytics is designed for analysis, rather than retrieving raw data.)</span></span>

## <a name="diagrams"></a><span data-ttu-id="fb31a-177">Diagrammi</span><span class="sxs-lookup"><span data-stu-id="fb31a-177">Diagrams</span></span>
<span data-ttu-id="fb31a-178">Selezionare il tipo di diagramma desiderato:</span><span class="sxs-lookup"><span data-stu-id="fb31a-178">Select the type of diagram you'd like:</span></span>

![Selezionare un tipo di diagramma](./media/app-insights-analytics-using/230.png)

<span data-ttu-id="fb31a-180">Se sono presenti più colonne dei tipi corretti, è possibile scegliere gli assi X e Y e una colonna di dimensioni in base alla quale dividere i risultati.</span><span class="sxs-lookup"><span data-stu-id="fb31a-180">If you have several columns of the right types, you can choose the x and y axes, and a column of dimensions to split the results by.</span></span>

<span data-ttu-id="fb31a-181">Per impostazione predefinita, i risultati vengono inizialmente visualizzati in una tabella e si seleziona il diagramma manualmente.</span><span class="sxs-lookup"><span data-stu-id="fb31a-181">By default, results are initially displayed as a table, and you select the diagram manually.</span></span> <span data-ttu-id="fb31a-182">Per selezionare il diagramma, è possibile usare la [direttiva render](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) alla fine di una query.</span><span class="sxs-lookup"><span data-stu-id="fb31a-182">But you can use the [render directive](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) at the end of a query to select a diagram.</span></span>

### <a name="analytics-diagnostics"></a><span data-ttu-id="fb31a-183">Diagnostica di Analytics</span><span class="sxs-lookup"><span data-stu-id="fb31a-183">Analytics diagnostics</span></span>


<span data-ttu-id="fb31a-184">In un grafico del tempo, se si verifica un picco o una variazione improvvisa dei dati, sulla linea viene evidenziato un punto.</span><span class="sxs-lookup"><span data-stu-id="fb31a-184">On a timechart, if there is a sudden spike or step in your data, you may see a highlighted point on the line.</span></span> <span data-ttu-id="fb31a-185">Ciò indica che Diagnostica di Analytics ha identificato una combinazione di proprietà che filtrano le variazioni improvvise.</span><span class="sxs-lookup"><span data-stu-id="fb31a-185">This indicates that Analytics Diagnostics has identified a combination of properties that filter out the sudden change.</span></span> <span data-ttu-id="fb31a-186">Fare clic sul punto per ottenere maggiori dettagli sul filtro e per visualizzare la versione filtrata.</span><span class="sxs-lookup"><span data-stu-id="fb31a-186">Click the point to get more detail on the filter, and to see the filtered version.</span></span> <span data-ttu-id="fb31a-187">Questa opzione consente di identificare la causa della variazione.</span><span class="sxs-lookup"><span data-stu-id="fb31a-187">This may help you identify what caused the change.</span></span> 

[<span data-ttu-id="fb31a-188">Altre informazioni sulla Diagnostica di Analytics</span><span class="sxs-lookup"><span data-stu-id="fb31a-188">Learn more about Analytics Diagnostics</span></span>](app-insights-analytics-diagnostics.md)


![Diagnostica di Analytics](./media/app-insights-analytics-using/analytics-diagnostics.png)

## <a name="pin-to-dashboard"></a><span data-ttu-id="fb31a-190">Aggiungi al dashboard</span><span class="sxs-lookup"><span data-stu-id="fb31a-190">Pin to dashboard</span></span>
<span data-ttu-id="fb31a-191">Per aggiungere un diagramma o una tabella a uno dei [dashboard condivisi](app-insights-dashboards.md) , è sufficiente fare clic sulla puntina.</span><span class="sxs-lookup"><span data-stu-id="fb31a-191">You can pin a diagram or table to one of your [shared dashboards](app-insights-dashboards.md) - just click the pin.</span></span> <span data-ttu-id="fb31a-192">Potrebbe essere necessario [aggiornare il pacchetto dei prezzi dell'app](app-insights-pricing.md) per attivare questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="fb31a-192">(You might need to [upgrade your app's pricing package](app-insights-pricing.md) to turn on this feature.)</span></span> 

![Fare clic sulla puntina](./media/app-insights-analytics-using/pin-01.png)

<span data-ttu-id="fb31a-194">Ciò significa che, quando si crea un dashboard per monitorare le prestazioni o l'utilizzo dei servizi Web, è possibile includere analisi piuttosto complesse insieme ad altre metriche.</span><span class="sxs-lookup"><span data-stu-id="fb31a-194">This means that, when you put together a dashboard to help you monitor the performance or usage of your web services, you can include quite complex analysis alongside the other metrics.</span></span> 

<span data-ttu-id="fb31a-195">È possibile aggiungere una tabella al dashboard se contiene un massimo di quattro colonne.</span><span class="sxs-lookup"><span data-stu-id="fb31a-195">You can pin a table to the dashboard, if it has four or fewer columns.</span></span> <span data-ttu-id="fb31a-196">Verranno visualizzate solo le prime sette righe.</span><span class="sxs-lookup"><span data-stu-id="fb31a-196">Only the top seven rows are displayed.</span></span>

### <a name="dashboard-refresh"></a><span data-ttu-id="fb31a-197">Aggiornamento del dashboard</span><span class="sxs-lookup"><span data-stu-id="fb31a-197">Dashboard refresh</span></span>
<span data-ttu-id="fb31a-198">Il grafico aggiunto al dashboard viene aggiornato automaticamente rieseguendo la query ogni due ore circa.</span><span class="sxs-lookup"><span data-stu-id="fb31a-198">The chart pinned to the dashboard is refreshed automatically by re-running the query approximately every hours.</span></span> <span data-ttu-id="fb31a-199">È possibile anche fare clic sul pulsante Aggiorna.</span><span class="sxs-lookup"><span data-stu-id="fb31a-199">You can also click the Refresh button.</span></span>

### <a name="automatic-simplifications"></a><span data-ttu-id="fb31a-200">Semplificazioni automatiche</span><span class="sxs-lookup"><span data-stu-id="fb31a-200">Automatic simplifications</span></span>

<span data-ttu-id="fb31a-201">Quando si aggiunge a un grafico al dashboard, vengono applicate al grafico determinate semplificazioni.</span><span class="sxs-lookup"><span data-stu-id="fb31a-201">Certain simplifications are applied to a chart when you pin it to a dashboard.</span></span>

<span data-ttu-id="fb31a-202">**Restrizione di orario:** le query vengono automaticamente limitate agli ultimi 14 giorni.</span><span class="sxs-lookup"><span data-stu-id="fb31a-202">**Time restriction:** Queries are automatically limited to the past 14 days.</span></span> <span data-ttu-id="fb31a-203">Si tratta dello stesso effetto che si ottiene quando la query include `where timestamp > ago(14d)`.</span><span class="sxs-lookup"><span data-stu-id="fb31a-203">The effect is the same as if your query includes `where timestamp > ago(14d)`.</span></span>

<span data-ttu-id="fb31a-204">**Restrizione al numero di bin:** se si visualizza un grafico con numerosi bin discreti, in genere un grafico a barre, i bin meno popolati vengono automaticamente raggruppati in un unico bin "altri".</span><span class="sxs-lookup"><span data-stu-id="fb31a-204">**Bin count restriction:** If you display a chart that has a lot of discrete bins (typically a bar chart), the less populated bins are automatically grouped into a single "others" bin.</span></span> <span data-ttu-id="fb31a-205">Ad esempio, questa query:</span><span class="sxs-lookup"><span data-stu-id="fb31a-205">For example, this query:</span></span>

    requests | summarize count_search = count() by client_CountryOrRegion

<span data-ttu-id="fb31a-206">ha questo aspetto in Analisi:</span><span class="sxs-lookup"><span data-stu-id="fb31a-206">looks like this in Analytics:</span></span>

![Grafico con una lunga coda](./media/app-insights-analytics-using/pin-07.png)

<span data-ttu-id="fb31a-208">ma quando la si aggiunge un dashboard, è simile alla figura seguente:</span><span class="sxs-lookup"><span data-stu-id="fb31a-208">but when you pin it to a dashboard, it looks like this:</span></span>

![Grafico con bin limitati](./media/app-insights-analytics-using/pin-08.png)

## <a name="export-to-excel"></a><span data-ttu-id="fb31a-210">Eseguire l'esportazione in Excel</span><span class="sxs-lookup"><span data-stu-id="fb31a-210">Export to Excel</span></span>
<span data-ttu-id="fb31a-211">Dopo aver eseguito una query, è possibile scaricare un file con estensione csv.</span><span class="sxs-lookup"><span data-stu-id="fb31a-211">After you've run a query, you can download a .csv file.</span></span> <span data-ttu-id="fb31a-212">Fare clic su **Esporta in Excel**.</span><span class="sxs-lookup"><span data-stu-id="fb31a-212">Click **Export,  Excel**.</span></span>

## <a name="export-to-power-bi"></a><span data-ttu-id="fb31a-213">Esportare in Power BI</span><span class="sxs-lookup"><span data-stu-id="fb31a-213">Export to Power BI</span></span>
<span data-ttu-id="fb31a-214">Posizionare il cursore in una query e scegliere **Esporta in Power BI**.</span><span class="sxs-lookup"><span data-stu-id="fb31a-214">Put the cursor in a query and choose **Export, Power BI**.</span></span>

![Esportazione da Analisi a Power BI](./media/app-insights-analytics-using/240.png)

<span data-ttu-id="fb31a-216">Si esegue la query in Power BI.</span><span class="sxs-lookup"><span data-stu-id="fb31a-216">You run the query in Power BI.</span></span> <span data-ttu-id="fb31a-217">È possibile impostarla in modo che venga aggiornata secondo una pianificazione.</span><span class="sxs-lookup"><span data-stu-id="fb31a-217">You can set it to refresh on a schedule.</span></span>

<span data-ttu-id="fb31a-218">Con Power BI, è possibile creare i dashboard per raggruppare i dati da un'ampia gamma di origini.</span><span class="sxs-lookup"><span data-stu-id="fb31a-218">With Power BI, you can create dashboards that bring together data from a wide variety of sources.</span></span>

[<span data-ttu-id="fb31a-219">Altre informazioni sull'esportazione in Power BI</span><span class="sxs-lookup"><span data-stu-id="fb31a-219">Learn more about export to Power BI</span></span>](app-insights-export-power-bi.md)

## <a name="deep-link"></a><span data-ttu-id="fb31a-220">Collegamento diretto</span><span class="sxs-lookup"><span data-stu-id="fb31a-220">Deep link</span></span>

<span data-ttu-id="fb31a-221">Ottenere un collegamento in **Esporta, Condividi collegamento** che è possibile inviare a un altro utente.</span><span class="sxs-lookup"><span data-stu-id="fb31a-221">Get a link under **Export, Share link** that you can send to another user.</span></span> <span data-ttu-id="fb31a-222">Purché l'utente abbia [accesso al gruppo di risorse](app-insights-resources-roles-access-control.md), la query verrà aperta nell'interfaccia utente di Analytics.</span><span class="sxs-lookup"><span data-stu-id="fb31a-222">Provided the user has [access to your resource group](app-insights-resources-roles-access-control.md), the query will open in the Analytics UI.</span></span>

<span data-ttu-id="fb31a-223">Nel collegamento, il testo della query appare dopo "?q=", con compressione gzip e codifica in base 64.</span><span class="sxs-lookup"><span data-stu-id="fb31a-223">(In the link, the query text appears after "?q=", gzip compressed and base-64 encoded.</span></span> <span data-ttu-id="fb31a-224">È possibile scrivere codice per generare collegamenti diretti da fornire agli utenti.</span><span class="sxs-lookup"><span data-stu-id="fb31a-224">You could write code to generate deep links that you provide to users.</span></span> <span data-ttu-id="fb31a-225">Tuttavia il modo consigliato per eseguire Analytics dal codice è tramite l'uso dell'[API REST](https://dev.applicationinsights.io/).</span><span class="sxs-lookup"><span data-stu-id="fb31a-225">However, the recommended way to run Analytics from code is by using the [REST API](https://dev.applicationinsights.io/).)</span></span>


## <a name="automation"></a><span data-ttu-id="fb31a-226">Automazione</span><span class="sxs-lookup"><span data-stu-id="fb31a-226">Automation</span></span>

<span data-ttu-id="fb31a-227">Usare l'[API  REST di accesso ai dati](https://dev.applicationinsights.io/) per eseguire le query di Analytics.</span><span class="sxs-lookup"><span data-stu-id="fb31a-227">Use the  [Data Access REST API](https://dev.applicationinsights.io/) to run Analytics queries.</span></span> <span data-ttu-id="fb31a-228">[Ad esempio](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (con PowerShell):</span><span class="sxs-lookup"><span data-stu-id="fb31a-228">[For example](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (using PowerShell):</span></span>

```PS
curl "https://api.applicationinsights.io/beta/apps/DEMO_APP/query?query=requests%7C%20where%20timestamp%20%3E%3D%20ago(24h)%7C%20count" -H "x-api-key: DEMO_KEY"
```

<span data-ttu-id="fb31a-229">A differenza dell'interfaccia utente di Analytics, l'API REST non aggiunge automaticamente limitazioni di timestamp alle query.</span><span class="sxs-lookup"><span data-stu-id="fb31a-229">Unlike the Analytics UI, the REST API does not automatically add any timestamp limitation to your queries.</span></span> <span data-ttu-id="fb31a-230">Ricordarsi di aggiungere la propria clausola where per evitare di ricevere le risposte di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="fb31a-230">Remember to add your own where-clause, to avoid getting huge responses.</span></span>



## <a name="import-data"></a><span data-ttu-id="fb31a-231">Importa dati</span><span class="sxs-lookup"><span data-stu-id="fb31a-231">Import data</span></span>

<span data-ttu-id="fb31a-232">È possibile importare i dati da un file CSV.</span><span class="sxs-lookup"><span data-stu-id="fb31a-232">You can import data from a CSV file.</span></span> <span data-ttu-id="fb31a-233">Un utilizzo tipico consiste nell'importare i dati statici che è possibile unire alle tabelle dei dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="fb31a-233">A typical usage is to import static data that you can join with tables from your telemetry.</span></span> 

<span data-ttu-id="fb31a-234">Ad esempio, se nei dati di telemetria vengono identificati utenti autenticati tramite un alias o un ID offuscato, è possibile importare una tabella che esegue il mapping degli alias sui nomi reali.</span><span class="sxs-lookup"><span data-stu-id="fb31a-234">For example, if authenticated users are identified in your telemetry by an alias or obfuscated id, you could import a table that maps aliases to real names.</span></span> <span data-ttu-id="fb31a-235">Eseguendo un join nei dati di telemetria della richiesta, è possibile identificare gli utenti in base ai nomi reali nei report di Analytics.</span><span class="sxs-lookup"><span data-stu-id="fb31a-235">By performing a join on the request telemetry, you can identify users by their real names in the Analytics reports.</span></span>

### <a name="define-your-data-schema"></a><span data-ttu-id="fb31a-236">Definire lo schema dei dati</span><span class="sxs-lookup"><span data-stu-id="fb31a-236">Define your data schema</span></span>

1. <span data-ttu-id="fb31a-237">Fare clic su **Impostazioni** (in alto a sinistra) e quindi su **Origini dati**.</span><span class="sxs-lookup"><span data-stu-id="fb31a-237">Click **Settings** (at top left) and then **Data Sources**.</span></span> 
2. <span data-ttu-id="fb31a-238">Aggiungere un'origine dati, seguendo le istruzioni.</span><span class="sxs-lookup"><span data-stu-id="fb31a-238">Add a data source, following the instructions.</span></span> <span data-ttu-id="fb31a-239">Viene chiesto di fornire un esempio dei dati che deve includere almeno dieci righe.</span><span class="sxs-lookup"><span data-stu-id="fb31a-239">You are asked to supply a sample of the data, which should include at least ten rows.</span></span> <span data-ttu-id="fb31a-240">È quindi possibile correggere lo schema.</span><span class="sxs-lookup"><span data-stu-id="fb31a-240">You then correct the schema.</span></span>

<span data-ttu-id="fb31a-241">Lo schema definisce un'origine dati che sarà possibile usare per importare le singole tabelle.</span><span class="sxs-lookup"><span data-stu-id="fb31a-241">This defines a data source, which you can then use to import individual tables.</span></span>

### <a name="import-a-table"></a><span data-ttu-id="fb31a-242">Importare una tabella</span><span class="sxs-lookup"><span data-stu-id="fb31a-242">Import a table</span></span>

1. <span data-ttu-id="fb31a-243">Aprire la definizione dell'origine dati dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="fb31a-243">Open your data source definition from the list.</span></span>
2. <span data-ttu-id="fb31a-244">Fare clic su "Carica" e seguire le istruzioni per caricare la tabella.</span><span class="sxs-lookup"><span data-stu-id="fb31a-244">Click "Upload" and follow the instructions to upload the table.</span></span> <span data-ttu-id="fb31a-245">Poiché l'operazione prevede una chiamata a un'API REST risulterà facile da automatizzare.</span><span class="sxs-lookup"><span data-stu-id="fb31a-245">This involves a call to a REST API, and so it is easy to automate.</span></span> 

<span data-ttu-id="fb31a-246">La tabella è ora disponibile per l'utilizzo nelle query di Analytics.</span><span class="sxs-lookup"><span data-stu-id="fb31a-246">Your table is now available for use in Analytics queries.</span></span> <span data-ttu-id="fb31a-247">Verrà visualizzata in Analytics</span><span class="sxs-lookup"><span data-stu-id="fb31a-247">It will appear in Analytics</span></span> 

### <a name="use-the-table"></a><span data-ttu-id="fb31a-248">Usare la tabella</span><span class="sxs-lookup"><span data-stu-id="fb31a-248">Use the table</span></span>

<span data-ttu-id="fb31a-249">Si supponga che la definizione dell'origine dati sia denominata `usermap` e che abbia due campi, `realName` e `user_AuthenticatedId`.</span><span class="sxs-lookup"><span data-stu-id="fb31a-249">Let's suppose your data source definition is called `usermap`, and that it has two fields, `realName` and `user_AuthenticatedId`.</span></span> <span data-ttu-id="fb31a-250">Poiché la tabella `requests` contiene anche un campo denominato `user_AuthenticatedId`, creare un join risulterà facile:</span><span class="sxs-lookup"><span data-stu-id="fb31a-250">The `requests` table also has a field named `user_AuthenticatedId`, so it's easy to join them:</span></span>

```AIQL

    requests
    | where notempty(user_AuthenticatedId) | take 10
    | join kind=leftouter ( usermap ) on user_AuthenticatedId 
```
<span data-ttu-id="fb31a-251">La tabella di richieste risultante ha una colonna aggiuntiva, `realName`.</span><span class="sxs-lookup"><span data-stu-id="fb31a-251">The resulting table of requests has an additional column, `realName`.</span></span>

### <a name="import-from-logstash"></a><span data-ttu-id="fb31a-252">Importare da LogStash</span><span class="sxs-lookup"><span data-stu-id="fb31a-252">Import from LogStash</span></span>

<span data-ttu-id="fb31a-253">Se si usa [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), è possibile usare Analytics per eseguire query nei log.</span><span class="sxs-lookup"><span data-stu-id="fb31a-253">If you use [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), you can use Analytics to query your logs.</span></span> <span data-ttu-id="fb31a-254">Usare il [plug-in che invia pipe dei dati in Analytics](https://github.com/Microsoft/logstash-output-application-insights).</span><span class="sxs-lookup"><span data-stu-id="fb31a-254">Use the [plugin that pipes data into Analytics](https://github.com/Microsoft/logstash-output-application-insights).</span></span> 

## <a name="video"></a><span data-ttu-id="fb31a-255">Video</span><span class="sxs-lookup"><span data-stu-id="fb31a-255">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

