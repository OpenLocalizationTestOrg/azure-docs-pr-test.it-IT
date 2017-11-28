---
title: Presentazione di Analisi in Azure Application Insights | Microsoft Docs
description: Brevi esempi di tutte le principali query in Analisi, lo strumento di ricerca avanzato di Application Insights.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: bddf4a6d-ea8d-4607-8531-1fe197cc57ad
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/06/2017
ms.author: bwren
ms.openlocfilehash: f5650d212eb2f8c460f062b3c11ae14c1e026ba6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="a-tour-of-analytics-in-application-insights"></a><span data-ttu-id="7c116-103">Presentazione dello strumento Analisi in Application Insights</span><span class="sxs-lookup"><span data-stu-id="7c116-103">A tour of Analytics in Application Insights</span></span>
<span data-ttu-id="7c116-104">L'[analisi](app-insights-analytics.md) è lo strumento di ricerca avanzato incluso in [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7c116-104">[Analytics](app-insights-analytics.md) is the powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="7c116-105">Queste pagine descrivono il linguaggio di query di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="7c116-105">These pages describe the Log Analytics query language.</span></span>

* <span data-ttu-id="7c116-106">**[Guardare il video introduttivo](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="7c116-106">**[Watch the introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="7c116-107">**[Eseguire la versione di test di Analisi sui dati simulati](https://analytics.applicationinsights.io/demo)** se l'app non invia ancora i dati ad Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7c116-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data to Application Insights yet.</span></span>
* <span data-ttu-id="7c116-108">Il **[foglio informativo sugli utenti SQL](https://aka.ms/sql-analytics)** traduce i linguaggi più comuni.</span><span class="sxs-lookup"><span data-stu-id="7c116-108">**[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates the most common idioms.</span></span>

<span data-ttu-id="7c116-109">Di seguito sono descritte alcune query di base utili per iniziare.</span><span class="sxs-lookup"><span data-stu-id="7c116-109">Let's take a walk through some basic queries to get you started.</span></span>

## <a name="connect-to-your-application-insights-data"></a><span data-ttu-id="7c116-110">Connettersi ai dati di Application Insights</span><span class="sxs-lookup"><span data-stu-id="7c116-110">Connect to your Application Insights data</span></span>
<span data-ttu-id="7c116-111">Aprire Analisi dal [pannello Panoramica](app-insights-dashboards.md) dell'app in Application Insights:</span><span class="sxs-lookup"><span data-stu-id="7c116-111">Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights:</span></span>

![In portal.azure.com, aprire la risorsa di Application Insights e selezionare Analytics.](./media/app-insights-analytics-tour/001.png)

## <a name="takehttpsdocsloganalyticsioquerylanguagequerylanguagetakeoperatorhtml-show-me-n-rows"></a><span data-ttu-id="7c116-113">[Take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): visualizzare n righe</span><span class="sxs-lookup"><span data-stu-id="7c116-113">[Take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): show me n rows</span></span>
<span data-ttu-id="7c116-114">I punti dati che registrano le operazioni degli utenti (in genere richieste HTTP ricevute dall'app Web) vengono archiviati in una tabella denominata `requests`.</span><span class="sxs-lookup"><span data-stu-id="7c116-114">Data points that log user operations (typically HTTP requests received by your web app) are stored in a table called `requests`.</span></span> <span data-ttu-id="7c116-115">Ogni riga è un punto dati di telemetria ricevuto da Application Insights SDK nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7c116-115">Each row is a telemetry data point received from the Application Insights SDK in your app.</span></span>

<span data-ttu-id="7c116-116">Si inizierà ora a esaminare alcune righe di esempio della tabella:</span><span class="sxs-lookup"><span data-stu-id="7c116-116">Let's start by examining a few sample rows of the table:</span></span>

![results](./media/app-insights-analytics-tour/010.png)

> [!NOTE]
> <span data-ttu-id="7c116-118">Inserire il cursore in un punto nell'istruzione prima fare clic su Vai.</span><span class="sxs-lookup"><span data-stu-id="7c116-118">Put the cursor somewhere in the statement before you click Go.</span></span> <span data-ttu-id="7c116-119">È possibile suddividere un'istruzione su più righe, ma non inserire righe vuote in un'istruzione.</span><span class="sxs-lookup"><span data-stu-id="7c116-119">You can split a statement over more than one line, but don't put blank lines in a statement.</span></span> <span data-ttu-id="7c116-120">Le righe vuote sono un modo pratico per mantenere più query separate nella finestra.</span><span class="sxs-lookup"><span data-stu-id="7c116-120">Blank lines are a convenient way to keep several separate queries in the window.</span></span>
>
>

<span data-ttu-id="7c116-121">Scegliere le colonne, trascinarle, creare gruppi in base alle colonne e applicare filtri:</span><span class="sxs-lookup"><span data-stu-id="7c116-121">Choose columns, drag them, group by columns, and filter:</span></span>

![Fare clic sulla selezione di colonna in alto a destra dei risultati](./media/app-insights-analytics-tour/030.png)

<span data-ttu-id="7c116-123">Espandere un elemento per visualizzare i dettagli:</span><span class="sxs-lookup"><span data-stu-id="7c116-123">Expand any item to see the detail:</span></span>

![Scegliere Tabella e usare Configura colonne](./media/app-insights-analytics-tour/040.png)

> [!NOTE]
> <span data-ttu-id="7c116-125">Fare clic sull'intestazione di una colonna per riordinare i risultati disponibili nel Web browser.</span><span class="sxs-lookup"><span data-stu-id="7c116-125">Click the head of a column to re-order the results available in the web browser.</span></span> <span data-ttu-id="7c116-126">Tuttavia, tenere presente che per un set di risultati di grandi dimensioni, il numero di righe scaricate nel browser è limitato.</span><span class="sxs-lookup"><span data-stu-id="7c116-126">But be aware that for a large result set, the number of rows downloaded to the browser is limited.</span></span> <span data-ttu-id="7c116-127">Questa modalità di ordinamento non sempre illustra gli elementi effettivi massimi o minimi.</span><span class="sxs-lookup"><span data-stu-id="7c116-127">Sorting this way doesn't always show you the actual highest or lowest items.</span></span> <span data-ttu-id="7c116-128">Per ordinarli in modo affidabile, usare l'operatore `top` o `sort`.</span><span class="sxs-lookup"><span data-stu-id="7c116-128">To sort items reliably, use the `top` or `sort` operator.</span></span>
>
>

## <a name="tophttpsdocsloganalyticsioquerylanguagequerylanguagetopoperatorhtml-and-sorthttpsdocsloganalyticsioquerylanguagequerylanguagesortoperatorhtml"></a><span data-ttu-id="7c116-129">[Top](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) e [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)</span><span class="sxs-lookup"><span data-stu-id="7c116-129">[Top](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) and [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)</span></span>
<span data-ttu-id="7c116-130">`take` è utile per ottenere un rapido esempio di un risultato, ma mostra le righe della tabella senza un ordine particolare.</span><span class="sxs-lookup"><span data-stu-id="7c116-130">`take` is useful to get a quick sample of a result, but it shows rows from the table in no particular order.</span></span> <span data-ttu-id="7c116-131">Per ottenere una visualizzazione ordinata, usare `top` per un campione o `sort` per l'intera tabella.</span><span class="sxs-lookup"><span data-stu-id="7c116-131">To get an ordered view, use `top` (for a sample) or `sort` (over the whole table).</span></span>

<span data-ttu-id="7c116-132">Mostrare le prime n righe, ordinate in base a una colonna specifica:</span><span class="sxs-lookup"><span data-stu-id="7c116-132">Show me the first n rows, ordered by a particular column:</span></span>

```AIQL

    requests | top 10 by timestamp desc
```

* <span data-ttu-id="7c116-133">*Sintassi:* la maggior parte degli operatori ha parametri di tipo parola chiave, ad esempio `by`.</span><span class="sxs-lookup"><span data-stu-id="7c116-133">*Syntax:* Most operators have keyword parameters such as `by`.</span></span>
* <span data-ttu-id="7c116-134">`desc` = ordine decrescente, `asc` = ordine crescente.</span><span class="sxs-lookup"><span data-stu-id="7c116-134">`desc` = descending order, `asc` = ascending.</span></span>

![](./media/app-insights-analytics-tour/260.png)

<span data-ttu-id="7c116-135">`top...` è più efficiente di `sort ... | take...`.</span><span class="sxs-lookup"><span data-stu-id="7c116-135">`top...` is a more performant way of saying `sort ... | take...`.</span></span> <span data-ttu-id="7c116-136">Si sarebbe potuto scrivere:</span><span class="sxs-lookup"><span data-stu-id="7c116-136">We could have written:</span></span>

```AIQL

    requests | sort by timestamp desc | take 10
```

<span data-ttu-id="7c116-137">Il risultato sarebbe stato lo stesso, ma l'esecuzione sarebbe risultata più lenta.</span><span class="sxs-lookup"><span data-stu-id="7c116-137">The result would be the same, but it would run a bit more slowly.</span></span> <span data-ttu-id="7c116-138">Sarebbe stato anche possibile scrivere `order`, che è un alias di `sort`.</span><span class="sxs-lookup"><span data-stu-id="7c116-138">(You could also write `order`, which is an alias of `sort`.)</span></span>

<span data-ttu-id="7c116-139">Le intestazioni di colonna nella visualizzazione tabella possono essere usate anche per ordinare i risultati sullo schermo.</span><span class="sxs-lookup"><span data-stu-id="7c116-139">The column headers in the table view can also be used to sort the results on the screen.</span></span> <span data-ttu-id="7c116-140">Naturalmente, se è stato usato `take` o `top` per recuperare solo parte di una tabella, verranno riordinati solo i record recuperati.</span><span class="sxs-lookup"><span data-stu-id="7c116-140">But of course, if you've used `take` or `top` to retrieve just part of a table, you'll only re-order the records you've retrieved.</span></span>

## <a name="wherehttpsdocsloganalyticsioquerylanguagequerylanguagewhereoperatorhtml-filtering-on-a-condition"></a><span data-ttu-id="7c116-141">[Where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): filtrare in base a una condizione</span><span class="sxs-lookup"><span data-stu-id="7c116-141">[Where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): filtering on a condition</span></span>

<span data-ttu-id="7c116-142">Di seguito sono illustrate solo le richieste che hanno restituito un particolare codice di risultato:</span><span class="sxs-lookup"><span data-stu-id="7c116-142">Let's see just requests that returned a particular result code:</span></span>

```AIQL

    requests
    | where resultCode  == "404"
    | take 10
```

![](./media/app-insights-analytics-tour/250.png)

<span data-ttu-id="7c116-143">L'operatore `where` accetta un'espressione booleana.</span><span class="sxs-lookup"><span data-stu-id="7c116-143">The `where` operator takes a Boolean expression.</span></span> <span data-ttu-id="7c116-144">Tenere presente i punti chiave seguenti:</span><span class="sxs-lookup"><span data-stu-id="7c116-144">Here are some key points about them:</span></span>

* <span data-ttu-id="7c116-145">`and`, `or`: operatori booleani</span><span class="sxs-lookup"><span data-stu-id="7c116-145">`and`, `or`: Boolean operators</span></span>
* <span data-ttu-id="7c116-146">`==`, `<>`, `!=`: uguale a e non uguale a</span><span class="sxs-lookup"><span data-stu-id="7c116-146">`==`, `<>`, `!=` : equal and not equal</span></span>
* <span data-ttu-id="7c116-147">`=~`, `!~`: stringa senza distinzione tra maiuscole e minuscole uguale a e non uguale a.</span><span class="sxs-lookup"><span data-stu-id="7c116-147">`=~`, `!~` : case-insensitive string equal and not equal.</span></span> <span data-ttu-id="7c116-148">Sono disponibili numerosi altri operatori di confronto delle stringhe.</span><span class="sxs-lookup"><span data-stu-id="7c116-148">There are lots more string comparison operators.</span></span>

<!---Read all about [scalar expressions]().--->

### <a name="getting-the-right-type"></a><span data-ttu-id="7c116-149">Recupero del tipo corretto</span><span class="sxs-lookup"><span data-stu-id="7c116-149">Getting the right type</span></span>
<span data-ttu-id="7c116-150">Individuare le richieste non riuscite:</span><span class="sxs-lookup"><span data-stu-id="7c116-150">Find unsuccessful requests:</span></span>

```AIQL

    requests
    | where isnotempty(resultCode) and toint(resultCode) >= 400
```
<!---
`resultCode` has type string, so we must cast it app-insights-analytics-reference.md#casts for a numeric comparison.
--->

## <a name="time"></a><span data-ttu-id="7c116-151">Tempo</span><span class="sxs-lookup"><span data-stu-id="7c116-151">Time</span></span>

<span data-ttu-id="7c116-152">Per impostazione predefinita, le query sono limitate alle ultime 24 ore.</span><span class="sxs-lookup"><span data-stu-id="7c116-152">By default, your queries are restricted to the last 24 hours.</span></span> <span data-ttu-id="7c116-153">Questo intervallo, però, può essere modificato:</span><span class="sxs-lookup"><span data-stu-id="7c116-153">But you can change this range:</span></span>

![](./media/app-insights-analytics-tour/change-time-range.png)

<span data-ttu-id="7c116-154">Eseguire l'override dell'intervallo di tempo scrivendo una query che includa `timestamp` in una clausola where.</span><span class="sxs-lookup"><span data-stu-id="7c116-154">Override the time range by writing any query that mentions `timestamp` in a where-clause.</span></span> <span data-ttu-id="7c116-155">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="7c116-155">For example:</span></span>

```AIQL

    // What were the slowest requests over the past 3 days?
    requests
    | where timestamp > ago(3d)  // Override the time range
    | top 5 by duration
```

<span data-ttu-id="7c116-156">La funzionalità di intervallo di tempo è equivalente a una clausola 'where' inserita dopo ogni menzione di una delle tabelle di origine.</span><span class="sxs-lookup"><span data-stu-id="7c116-156">The time range feature is equivalent to a 'where' clause inserted after each mention of one of the source tables.</span></span>

<span data-ttu-id="7c116-157">`ago(3d)` significa 'tre giorni fa'.</span><span class="sxs-lookup"><span data-stu-id="7c116-157">`ago(3d)` means 'three days ago'.</span></span> <span data-ttu-id="7c116-158">Le altre unità di tempo includono ore (`2h`, `2.5h`), minuti (`25m`) e secondi (`10s`).</span><span class="sxs-lookup"><span data-stu-id="7c116-158">Other units of time include hours (`2h`, `2.5h`), minutes (`25m`), and seconds (`10s`).</span></span>

<span data-ttu-id="7c116-159">Altri esempi:</span><span class="sxs-lookup"><span data-stu-id="7c116-159">Other examples:</span></span>

```AIQL

    // Last calendar week:
    requests
    | where timestamp > startofweek(now()-7d)
        and timestamp < startofweek(now())
    | top 5 by duration

    // First hour of every day in past seven days:
    requests
    | where timestamp > ago(7d) and timestamp % 1d < 1h
    | top 5 by duration

    // Specific dates:
    requests
    | where timestamp > datetime(2016-11-19) and timestamp < datetime(2016-11-21)
    | top 5 by duration

```

<span data-ttu-id="7c116-160">[Riferimento su date e ore](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).</span><span class="sxs-lookup"><span data-stu-id="7c116-160">[Dates and times reference](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).</span></span>


## <a name="projecthttpsdocsloganalyticsioquerylanguagequerylanguageprojectoperatorhtml-select-rename-and-compute-columns"></a><span data-ttu-id="7c116-161">[Project](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): selezionare, rinominare e calcolare le colonne</span><span class="sxs-lookup"><span data-stu-id="7c116-161">[Project](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): select, rename, and compute columns</span></span>
<span data-ttu-id="7c116-162">Usare [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) per selezionare solo le colonne desiderate:</span><span class="sxs-lookup"><span data-stu-id="7c116-162">Use [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) to pick out just the columns you want:</span></span>

```AIQL

    requests | top 10 by timestamp desc
             | project timestamp, name, resultCode
```

![](./media/app-insights-analytics-tour/240.png)

<span data-ttu-id="7c116-163">È inoltre possibile rinominare le colonne e definire nuove colonne:</span><span class="sxs-lookup"><span data-stu-id="7c116-163">You can also rename columns and define new ones:</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | project  
            name,
            response = resultCode,
            timestamp,
            ['time of day'] = floor(timestamp % 1d, 1s)
```

![risultato](./media/app-insights-analytics-tour/270.png)

* <span data-ttu-id="7c116-165">I nomi di colonna possono includere spazi o simboli se sono racchiusi tra parentesi quadre, ad esempio: `['...']` o `["..."]`</span><span class="sxs-lookup"><span data-stu-id="7c116-165">Column names can include spaces or symbols if they are bracketed like this: `['...']` or `["..."]`</span></span>
* <span data-ttu-id="7c116-166">`%` è il consueto operatore modulo.</span><span class="sxs-lookup"><span data-stu-id="7c116-166">`%` is the usual modulo operator.</span></span>
* <span data-ttu-id="7c116-167">`1d` (la cifra uno seguita da "d") è il valore letterale di un intervallo di tempo che indica un giorno.</span><span class="sxs-lookup"><span data-stu-id="7c116-167">`1d` (that's a digit one, then a 'd') is a timespan literal meaning one day.</span></span> <span data-ttu-id="7c116-168">Ecco altri valori letterali di intervallo di tempo: `12h`, `30m`, `10s`, `0.01s`.</span><span class="sxs-lookup"><span data-stu-id="7c116-168">Here are some more timespan literals: `12h`, `30m`, `10s`, `0.01s`.</span></span>
* <span data-ttu-id="7c116-169">`floor` (alias `bin`) arrotonda un valore per difetto al multiplo più vicino del valore di base specificato.</span><span class="sxs-lookup"><span data-stu-id="7c116-169">`floor` (alias `bin`) rounds a value down to the nearest multiple of the base value you provide.</span></span> <span data-ttu-id="7c116-170">`floor(aTime, 1s)` arrotonda un'ora per difetto al secondo più vicino.</span><span class="sxs-lookup"><span data-stu-id="7c116-170">So `floor(aTime, 1s)` rounds a time down to the nearest second.</span></span>

<span data-ttu-id="7c116-171">Le espressioni possono includere tutti gli operatori consueti (`+`, `-`, ...) ed è disponibile una gamma di funzioni utili.</span><span class="sxs-lookup"><span data-stu-id="7c116-171">Expressions can include all the usual operators (`+`, `-`, ...), and there's a range of useful functions.</span></span>

## <a name="extend"></a><span data-ttu-id="7c116-172">Extend</span><span class="sxs-lookup"><span data-stu-id="7c116-172">Extend</span></span>
<span data-ttu-id="7c116-173">Per aggiungere colonne a quelle già esistenti, usare [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):</span><span class="sxs-lookup"><span data-stu-id="7c116-173">If you just want to add columns to the existing ones, use [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | extend timeOfDay = floor(timestamp % 1d, 1s)
```

<span data-ttu-id="7c116-174">Se si vogliono mantenere tutte le colonne esistenti, [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) è meno dettagliato di [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html).</span><span class="sxs-lookup"><span data-stu-id="7c116-174">Using [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) is less verbose than [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) if you want to keep all the existing columns.</span></span>

### <a name="convert-to-local-time"></a><span data-ttu-id="7c116-175">Convertire nell'ora locale</span><span class="sxs-lookup"><span data-stu-id="7c116-175">Convert to local time</span></span>

<span data-ttu-id="7c116-176">I timestamp sono sempre espressi in formato UTC.</span><span class="sxs-lookup"><span data-stu-id="7c116-176">Timestamps are always in UTC.</span></span> <span data-ttu-id="7c116-177">Pertanto, se ci si trova sulla costa del Pacifico ed è inverno, potrebbe essere utile quanto riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="7c116-177">So if you're on the US Pacific coast and it's winter, you might like this:</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | extend localTime = timestamp - 8h
```


## <a name="summarizehttpsdocsloganalyticsioquerylanguagequerylanguagesummarizeoperatorhtml-aggregate-groups-of-rows"></a><span data-ttu-id="7c116-178">[Summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): aggregare gruppi di righe</span><span class="sxs-lookup"><span data-stu-id="7c116-178">[Summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): aggregate groups of rows</span></span>
<span data-ttu-id="7c116-179">`Summarize` applica una *funzione di aggregazione* specificata a gruppi di righe.</span><span class="sxs-lookup"><span data-stu-id="7c116-179">`Summarize` applies a specified *aggregation function* over groups of rows.</span></span>

<span data-ttu-id="7c116-180">Ad esempio, il tempo che l'app Web impiega per rispondere a una richiesta viene indicato nel campo `duration`.</span><span class="sxs-lookup"><span data-stu-id="7c116-180">For example, the time your web app takes to respond to a request is reported in the field `duration`.</span></span> <span data-ttu-id="7c116-181">Verrà visualizzato il tempo medio di risposta a tutte le richieste:</span><span class="sxs-lookup"><span data-stu-id="7c116-181">Let's see the average response time to all requests:</span></span>

![](./media/app-insights-analytics-tour/410.png)

<span data-ttu-id="7c116-182">È anche possibile separare il risultato in richieste con nomi diversi:</span><span class="sxs-lookup"><span data-stu-id="7c116-182">Or we could separate the result into requests of different names:</span></span>

![](./media/app-insights-analytics-tour/420.png)

<span data-ttu-id="7c116-183">`Summarize` raccoglie i punti dati del flusso in gruppi che la clausola `by` valuta in ugual misura.</span><span class="sxs-lookup"><span data-stu-id="7c116-183">`Summarize` collects the data points in the stream into groups for which the `by` clause evaluates equally.</span></span> <span data-ttu-id="7c116-184">Ogni valore nell'espressione `by` , ovvero ogni nome di operazione nell'esempio precedente, restituisce una riga nella tabella dei risultati.</span><span class="sxs-lookup"><span data-stu-id="7c116-184">Each value in the `by` expression - each operation name in the above example - results in a row in the result table.</span></span>

<span data-ttu-id="7c116-185">È anche possibile raggruppare i risultati per ora del giorno:</span><span class="sxs-lookup"><span data-stu-id="7c116-185">Or we could group results by time of day:</span></span>

![](./media/app-insights-analytics-tour/430.png)

<span data-ttu-id="7c116-186">Si noti che si sta usando la funzione `bin`, detta anche `floor`.</span><span class="sxs-lookup"><span data-stu-id="7c116-186">Notice how we're using the `bin` function (aka `floor`).</span></span> <span data-ttu-id="7c116-187">Se si usasse solo `by timestamp`, ogni riga di input finirebbe in un piccolo gruppo distinto.</span><span class="sxs-lookup"><span data-stu-id="7c116-187">If we just used `by timestamp`, every input row would end up in its own little group.</span></span> <span data-ttu-id="7c116-188">Per i valori scalari continui, come le ore o i numeri, è necessario suddividere l'intervallo continuo in un numero gestibile di valori discreti.</span><span class="sxs-lookup"><span data-stu-id="7c116-188">For any continuous scalar like times or numbers, we have to break the continuous range into a manageable number of discrete values.</span></span> <span data-ttu-id="7c116-189">Il modo più semplice per eseguire questa operazione è usare `bin`, che è in realtà la nota funzione `floor` per l'arrotondamento per difetto.</span><span class="sxs-lookup"><span data-stu-id="7c116-189">`bin` - which is just the familiar rounding-down `floor` function - is the easiest way to do that.</span></span>

<span data-ttu-id="7c116-190">È possibile usare la stessa tecnica per ridurre gli intervalli di stringhe:</span><span class="sxs-lookup"><span data-stu-id="7c116-190">We can use the same technique to reduce ranges of strings:</span></span>

![](./media/app-insights-analytics-tour/440.png)

<span data-ttu-id="7c116-191">Si noti che è possibile usare `name=` per impostare il nome di una colonna di risultati, nelle espressioni di aggregazione o nella clausola by.</span><span class="sxs-lookup"><span data-stu-id="7c116-191">Notice that you can use `name=` to set the name of a result column, either in the aggregation expressions or the by-clause.</span></span>

## <a name="counting-sampled-data"></a><span data-ttu-id="7c116-192">Conteggio dei dati campionati</span><span class="sxs-lookup"><span data-stu-id="7c116-192">Counting sampled data</span></span>
<span data-ttu-id="7c116-193">`sum(itemCount)` è l'aggregazione consigliata per contare gli eventi.</span><span class="sxs-lookup"><span data-stu-id="7c116-193">`sum(itemCount)` is the recommended aggregation to count events.</span></span> <span data-ttu-id="7c116-194">In molti casi, itemCount==1, quindi la funzione somma semplicemente il numero di righe nel gruppo.</span><span class="sxs-lookup"><span data-stu-id="7c116-194">In many cases, itemCount==1, so the function simply counts up the number of rows in the group.</span></span> <span data-ttu-id="7c116-195">Ma, quando nell'operazione è previsto un [campionamento](app-insights-sampling.md), solo una frazione degli eventi originali viene conservata come punti dati in Application Insights, in modo che siano presenti eventi in numero pari a `itemCount` per ogni punto dati visualizzato.</span><span class="sxs-lookup"><span data-stu-id="7c116-195">But when [sampling](app-insights-sampling.md) is in operation, only a fraction of the original events are retained as data points in Application Insights, so that for each data point you see, there are `itemCount` events.</span></span>

<span data-ttu-id="7c116-196">Ad esempio, se il campionamento elimina il 75% degli eventi originali, allora itemCount==4 nei record mantenuti; ciò significa che per ogni record mantenuto erano presenti quattro record originali.</span><span class="sxs-lookup"><span data-stu-id="7c116-196">For example, if sampling discards 75% of the original events, then itemCount==4 in the retained records - that is, for every retained record, there were four original records.</span></span>

<span data-ttu-id="7c116-197">Il campionamento adattivo causa un valore itemCount più elevato durante i periodi in cui l'applicazione viene utilizzata di frequente.</span><span class="sxs-lookup"><span data-stu-id="7c116-197">Adaptive sampling causes itemCount to be higher during periods when your application is being heavily used.</span></span>

<span data-ttu-id="7c116-198">Il riepilogo di itemCount offre quindi una stima valida del numero di eventi originale.</span><span class="sxs-lookup"><span data-stu-id="7c116-198">Summing up itemCount therefore gives a good estimate of the original number of events.</span></span>

![](./media/app-insights-analytics-tour/510.png)

<span data-ttu-id="7c116-199">È disponibile anche un'aggregazione `count()` , oltre a un'operazione di conteggio, per i casi in cui si vuole effettivamente contare il numero di righe in un gruppo.</span><span class="sxs-lookup"><span data-stu-id="7c116-199">There's also a `count()` aggregation (and a count operation), for cases where you really do want to count the number of rows in a group.</span></span>

<span data-ttu-id="7c116-200">Esiste un intervallo di [funzioni di aggregazione](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span><span class="sxs-lookup"><span data-stu-id="7c116-200">There's a range of [aggregation functions](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span></span>

## <a name="charting-the-results"></a><span data-ttu-id="7c116-201">Disegnare i risultati</span><span class="sxs-lookup"><span data-stu-id="7c116-201">Charting the results</span></span>
```AIQL

    exceptions
       | summarize count=sum(itemCount)  
         by bin(timestamp, 1h)
```

<span data-ttu-id="7c116-202">Per impostazione predefinita, i risultati vengono visualizzati sotto forma di tabella:</span><span class="sxs-lookup"><span data-stu-id="7c116-202">By default, results display as a table:</span></span>

![](./media/app-insights-analytics-tour/225.png)

<span data-ttu-id="7c116-203">È possibile ottenere un risultato migliore della visualizzazione tabella.</span><span class="sxs-lookup"><span data-stu-id="7c116-203">We can do better than the table view.</span></span> <span data-ttu-id="7c116-204">Si osservino i risultati nella visualizzazione grafico con l'opzione delle barre verticali:</span><span class="sxs-lookup"><span data-stu-id="7c116-204">Let's look at the results in the chart view with the vertical bar option:</span></span>

![Fare clic su Grafico, quindi scegliere Grafico a barre verticali e assegnare gli assi x e y](./media/app-insights-analytics-tour/230.png)

<span data-ttu-id="7c116-206">Si noti che anche se i risultati non sono stati ordinati in base all'ora (come è possibile osservare nella visualizzazione tabella), la visualizzazione grafico mostra sempre i dati data/ora nell'ordine corretto.</span><span class="sxs-lookup"><span data-stu-id="7c116-206">Notice that although we didn't sort the results by time (as you can see in the table display), the chart display always shows datetimes in correct order.</span></span>


## <a name="timecharts"></a><span data-ttu-id="7c116-207">Grafici di tempo</span><span class="sxs-lookup"><span data-stu-id="7c116-207">Timecharts</span></span>
<span data-ttu-id="7c116-208">Visualizzare il numero di eventi presenti in ogni ora:</span><span class="sxs-lookup"><span data-stu-id="7c116-208">Show how many events there are each hour:</span></span>

```AIQL

    requests
      | summarize event_count=sum(itemCount)
        by bin(timestamp, 1h)
```

<span data-ttu-id="7c116-209">Selezionare l'opzione di visualizzazione grafico:</span><span class="sxs-lookup"><span data-stu-id="7c116-209">Select the Chart display option:</span></span>

![timechart](./media/app-insights-analytics-tour/080.png)

## <a name="multiple-series"></a><span data-ttu-id="7c116-211">Serie multiple</span><span class="sxs-lookup"><span data-stu-id="7c116-211">Multiple series</span></span>
<span data-ttu-id="7c116-212">La presenza di più espressioni nella clausola `summarize` determina la creazione di più colonne.</span><span class="sxs-lookup"><span data-stu-id="7c116-212">Multiple expressions in the `summarize` clause creates multiple columns.</span></span>

<span data-ttu-id="7c116-213">La presenza di più espressioni nella clausola `by` determina la creazione di più righe, una per ogni combinazione di valori.</span><span class="sxs-lookup"><span data-stu-id="7c116-213">Multiple expressions in the `by` clause creates multiple rows, one for each combination of values.</span></span>

```AIQL

    requests
    | summarize count_=sum(itemCount), avg(duration)
      by bin(timestamp, 1h), client_StateOrProvince, client_City
    | order by timestamp asc, client_StateOrProvince, client_City
```

![Tabella delle richieste in base a ora e località](./media/app-insights-analytics-tour/090.png)

### <a name="segment-a-chart-by-dimensions"></a><span data-ttu-id="7c116-215">Segmentare un grafico in base alle dimensioni</span><span class="sxs-lookup"><span data-stu-id="7c116-215">Segment a chart by dimensions</span></span>
<span data-ttu-id="7c116-216">Se si crea un grafico per una tabella contenente una colonna di stringhe e una colonna numerica, la stringa può essere usata per suddividere i dati numerici in serie separate di punti.</span><span class="sxs-lookup"><span data-stu-id="7c116-216">If you chart a table that has a string column and a numeric column, the string can be used to split the numeric data into separate series of points.</span></span> <span data-ttu-id="7c116-217">Se è presente più di una colonna di stringhe, è possibile scegliere la colonna da usare come discriminatore.</span><span class="sxs-lookup"><span data-stu-id="7c116-217">If there's more than one string column, you can choose which column to use as the discriminator.</span></span>

![Segmentare un grafico di analisi](./media/app-insights-analytics-tour/100.png)

#### <a name="bounce-rate"></a><span data-ttu-id="7c116-219">Frequenza di mancati recapiti</span><span class="sxs-lookup"><span data-stu-id="7c116-219">Bounce rate</span></span>

<span data-ttu-id="7c116-220">Convertire un valore booleano in una stringa per usarlo come discriminatore:</span><span class="sxs-lookup"><span data-stu-id="7c116-220">Convert a boolean to a string to use it as a discriminator:</span></span>

```AIQL

    // Bounce rate: sessions with only one page view
    requests
    | where notempty(session_Id)
    | where tostring(operation_SyntheticSource) == "" // real users
    | summarize pagesInSession=sum(itemCount), sessionEnd=max(timestamp)
               by session_Id
    | extend isbounce= pagesInSession == 1
    | summarize count()
               by tostring(isbounce), bin (sessionEnd, 1h)
    | render timechart
```

### <a name="display-multiple-metrics"></a><span data-ttu-id="7c116-221">Visualizzare più metriche</span><span class="sxs-lookup"><span data-stu-id="7c116-221">Display multiple metrics</span></span>
<span data-ttu-id="7c116-222">Se si crea un grafico per una tabella contenente più di una colonna numerica, oltre al timestamp, è possibile visualizzare qualsiasi combinazione di colonne.</span><span class="sxs-lookup"><span data-stu-id="7c116-222">If you chart a table that has more than one numeric column, in addition to the timestamp, you can display any combination of them.</span></span>

![Segmentare un grafico di analisi](./media/app-insights-analytics-tour/110.png)

<span data-ttu-id="7c116-224">È necessario selezionare **Don't Split** (Non dividere) prima di poter selezionare più colonne numeriche.</span><span class="sxs-lookup"><span data-stu-id="7c116-224">You must select **Don't Split** before you can select multiple numeric columns.</span></span> <span data-ttu-id="7c116-225">Non è possibile dividere in base a una colonna di stringhe e allo stesso tempo visualizzare più di una colonna numerica.</span><span class="sxs-lookup"><span data-stu-id="7c116-225">You can't split by a string column at the same time as displaying more than one numeric column.</span></span>

## <a name="daily-average-cycle"></a><span data-ttu-id="7c116-226">Ciclo della media giornaliera</span><span class="sxs-lookup"><span data-stu-id="7c116-226">Daily average cycle</span></span>
<span data-ttu-id="7c116-227">Come varia l'uso nella giornata media?</span><span class="sxs-lookup"><span data-stu-id="7c116-227">How does usage vary over the average day?</span></span>

<span data-ttu-id="7c116-228">Conteggiare le richieste per un modulo di un giorno, suddivise in ore:</span><span class="sxs-lookup"><span data-stu-id="7c116-228">Count requests by the time modulo one day, binned into hours:</span></span>

```AIQL

    requests
    | where timestamp > ago(30d)  // Override "Last 24h"
    | where tostring(operation_SyntheticSource) == "" // real users
    | extend hour = bin(timestamp % 1d , 1h)
          + datetime("2016-01-01") // Allow render on line chart
    | summarize event_count=sum(itemCount) by hour
```

![Grafico a linee delle ore di un giorno medio](./media/app-insights-analytics-tour/120.png)

> [!NOTE]
> <span data-ttu-id="7c116-230">Si noti che attualmente è necessario convertire le durate in valori datetime per visualizzarli in un grafico a linee.</span><span class="sxs-lookup"><span data-stu-id="7c116-230">Notice that we currently have to convert time durations to datetimes in order to display on a line chart.</span></span>
>
>

## <a name="compare-multiple-daily-series"></a><span data-ttu-id="7c116-231">Confrontare più serie giornaliere</span><span class="sxs-lookup"><span data-stu-id="7c116-231">Compare multiple daily series</span></span>
<span data-ttu-id="7c116-232">Come varia l'uso nelle ore del giorno nei diversi paesi?</span><span class="sxs-lookup"><span data-stu-id="7c116-232">How does usage vary over the time of day in different countries?</span></span>

```AIQL

     requests  
     | where timestamp > ago(30d)  // Override "Last 24h"
     | where tostring(operation_SyntheticSource) == "" // real users
     | extend hour= floor( timestamp % 1d , 1h)
           + datetime("2001-01-01")
     | summarize event_count=sum(itemCount)
       by hour, client_CountryOrRegion
     | render timechart
```

![Suddivisione in base a client_CountryOrRegion](./media/app-insights-analytics-tour/130.png)

## <a name="plot-a-distribution"></a><span data-ttu-id="7c116-234">Tracciare una distribuzione</span><span class="sxs-lookup"><span data-stu-id="7c116-234">Plot a distribution</span></span>
<span data-ttu-id="7c116-235">Quante sessioni esistono di lunghezze diverse?</span><span class="sxs-lookup"><span data-stu-id="7c116-235">How many sessions are there of different lengths?</span></span>

```AIQL

    requests
    | where timestamp > ago(30d) // override "Last 24h"
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id
    | extend sessionDuration = max_timestamp - min_timestamp
    | where sessionDuration > 1s and sessionDuration < 3m
    | summarize count() by floor(sessionDuration, 3s)
    | project d = sessionDuration + datetime("2016-01-01"), count_
```

<span data-ttu-id="7c116-236">L'ultima riga serve per convertire in formato datetime.</span><span class="sxs-lookup"><span data-stu-id="7c116-236">The last line is required to convert to datetime.</span></span> <span data-ttu-id="7c116-237">Attualmente l'asse x di un grafico viene visualizzato come valore scalare solo se è un valore datetime.</span><span class="sxs-lookup"><span data-stu-id="7c116-237">Currently the x axis of a chart is displayed as a scalar only if it is a datetime.</span></span>

<span data-ttu-id="7c116-238">La clausola `where` esclude le sessioni monofase (sessionDuration==0) e imposta la lunghezza dell'asse x.</span><span class="sxs-lookup"><span data-stu-id="7c116-238">The `where` clause excludes one-shot sessions (sessionDuration==0) and sets the length of the x-axis.</span></span>

![](./media/app-insights-analytics-tour/290.png)

## <a name="percentileshttpsdocsloganalyticsioquerylanguagequerylanguagepercentilesaggfunctionhtml"></a>[<span data-ttu-id="7c116-239">Percentili</span><span class="sxs-lookup"><span data-stu-id="7c116-239">Percentiles</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_percentiles_aggfunction.html)
<span data-ttu-id="7c116-240">Quali intervalli di durate coprono le diverse percentuali delle sessioni?</span><span class="sxs-lookup"><span data-stu-id="7c116-240">What ranges of durations cover different percentages of sessions?</span></span>

<span data-ttu-id="7c116-241">Usare la query precedente, ma sostituire l'ultima riga:</span><span class="sxs-lookup"><span data-stu-id="7c116-241">Use the above query, but replace the last line:</span></span>

```AIQL

    requests
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id
    | extend sesh = max_timestamp - min_timestamp
    | where sesh > 1s
    | summarize count() by floor(sesh, 3s)
    | summarize percentiles(sesh, 5, 20, 50, 80, 95)
```

<span data-ttu-id="7c116-242">Viene anche rimosso il limite superiore nella clausola where in modo da ottenere dati corretti che includono tutte le sessioni con più di una richiesta:</span><span class="sxs-lookup"><span data-stu-id="7c116-242">We also removed the upper limit in the where clause, in order to get correct figures including all sessions with more than one request:</span></span>

![risultato](./media/app-insights-analytics-tour/180.png)

<span data-ttu-id="7c116-244">È possibile osservare che:</span><span class="sxs-lookup"><span data-stu-id="7c116-244">From which we can see that:</span></span>

* <span data-ttu-id="7c116-245">Il 5% delle sessioni ha una durata inferiore a 3 minuti e 34 secondi;</span><span class="sxs-lookup"><span data-stu-id="7c116-245">5% of sessions have a duration of less than 3 minutes 34s;</span></span>
* <span data-ttu-id="7c116-246">Il 50% delle sessioni dura meno di 36 minuti;</span><span class="sxs-lookup"><span data-stu-id="7c116-246">50% of sessions last less than 36 minutes;</span></span>
* <span data-ttu-id="7c116-247">Il 5% delle sessioni dura più di 7 giorni</span><span class="sxs-lookup"><span data-stu-id="7c116-247">5% of sessions last more than 7 days</span></span>

<span data-ttu-id="7c116-248">Per ottenere una suddivisione separata per ogni paese, è sufficiente visualizzare la colonna client_CountryOrRegion separatamente attraverso entrambi gli operatori summarize:</span><span class="sxs-lookup"><span data-stu-id="7c116-248">To get a separate breakdown for each country, we just have to bring the client_CountryOrRegion column separately through both summarize operators:</span></span>

```AIQL

    requests
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id, client_CountryOrRegion
    | extend sesh = max_timestamp - min_timestamp
    | where sesh > 1s
    | summarize count() by floor(sesh, 3s), client_CountryOrRegion
    | summarize percentiles(sesh, 5, 20, 50, 80, 95)
      by client_CountryOrRegion
```

![](./media/app-insights-analytics-tour/190.png)

## <a name="join"></a><span data-ttu-id="7c116-249">Join</span><span class="sxs-lookup"><span data-stu-id="7c116-249">Join</span></span>
<span data-ttu-id="7c116-250">È possibile accedere a più tabelle, incluse le richieste e le eccezioni.</span><span class="sxs-lookup"><span data-stu-id="7c116-250">We have access to several tables, including requests and exceptions.</span></span>

<span data-ttu-id="7c116-251">Per trovare le eccezioni correlate a una richiesta che ha restituito una risposta di errore, è possibile creare un join delle tabelle in `session_Id`:</span><span class="sxs-lookup"><span data-stu-id="7c116-251">To find the exceptions related to a request that returned a failure response, we can join the tables on `session_Id`:</span></span>

```AIQL

    requests
    | where toint(resultCode) >= 500
    | join (exceptions) on operation_Id
    | take 30
```


<span data-ttu-id="7c116-252">È buona norma usare `project` per selezionare solo le colonne necessarie prima di eseguire il join.</span><span class="sxs-lookup"><span data-stu-id="7c116-252">It's good practice to use `project` to select just the columns we need before performing the join.</span></span>
<span data-ttu-id="7c116-253">Nelle stesse clausole, si rinomina la colonna timestamp.</span><span class="sxs-lookup"><span data-stu-id="7c116-253">In the same clauses, we rename the timestamp column.</span></span>

## <a name="lethttpsdocsloganalyticsioquerylanguagequerylanguageletstatementhtml-assign-a-result-to-a-variable"></a><span data-ttu-id="7c116-254">[Let](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): assegnare un risultato a una variabile</span><span class="sxs-lookup"><span data-stu-id="7c116-254">[Let](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): Assign a result to a variable</span></span>

<span data-ttu-id="7c116-255">Usare `let` per separare le parti dell'espressione precedente.</span><span class="sxs-lookup"><span data-stu-id="7c116-255">Use `let` to separate out the parts of the previous expression.</span></span> <span data-ttu-id="7c116-256">I risultati rimangono invariati:</span><span class="sxs-lookup"><span data-stu-id="7c116-256">The results are unchanged:</span></span>

```AIQL

    let bad_requests =
      requests
        | where  toint(resultCode) >= 500  ;
    bad_requests
    | join (exceptions) on session_Id
    | take 30
```

> [!Tip] 
> <span data-ttu-id="7c116-257">Nel client Analisi non inserire righe vuote tra le parti della query.</span><span class="sxs-lookup"><span data-stu-id="7c116-257">In the Analytics client, don't put blank lines between the parts of the query.</span></span> <span data-ttu-id="7c116-258">Verificare che vengano eseguiti tutti gli elementi.</span><span class="sxs-lookup"><span data-stu-id="7c116-258">Make sure to execute all of it.</span></span>
>

<span data-ttu-id="7c116-259">Usare `toscalar` per convertire una cella di tabella in un valore:</span><span class="sxs-lookup"><span data-stu-id="7c116-259">Use `toscalar` to convert a single table cell to a value:</span></span>

```AIQL
let topCities =  toscalar (
   requests
   | summarize count() by client_City 
   | top n by count_ 
   | summarize makeset(client_City));
requests
| where client_City in (topCities(3)) 
| summarize count() by client_City;
```


### <a name="functions"></a><span data-ttu-id="7c116-260">Funzioni</span><span class="sxs-lookup"><span data-stu-id="7c116-260">Functions</span></span>

<span data-ttu-id="7c116-261">Usare *Let* per definire una funzione:</span><span class="sxs-lookup"><span data-stu-id="7c116-261">Use *Let* to define a function:</span></span>

```AIQL

    let usdate = (t:datetime)
    {
      strcat(getmonth(t), "/", dayofmonth(t),"/", getyear(t), " ",
      bin((t-1h)%12h+1h,1s), iff(t%24h<12h, "AM", "PM"))
    };
    requests  
    | extend PST = usdate(timestamp-8h)
```

## <a name="accessing-nested-objects"></a><span data-ttu-id="7c116-262">Accesso a oggetti annidati</span><span class="sxs-lookup"><span data-stu-id="7c116-262">Accessing nested objects</span></span>
<span data-ttu-id="7c116-263">È facile accedere agli oggetti annidati.</span><span class="sxs-lookup"><span data-stu-id="7c116-263">Nested objects can be accessed easily.</span></span> <span data-ttu-id="7c116-264">Nel flusso exceptions, ad esempio, sono visibili oggetti strutturati come questo:</span><span class="sxs-lookup"><span data-stu-id="7c116-264">For example, in the exceptions stream you can see structured objects like this:</span></span>

![risultato](./media/app-insights-analytics-tour/520.png)

<span data-ttu-id="7c116-266">È possibile renderlo flat scegliendo le proprietà che interessano:</span><span class="sxs-lookup"><span data-stu-id="7c116-266">You can flatten it by choosing the properties you're interested in:</span></span>

```AIQL

    exceptions | take 10
    | extend method1 = tostring(details[0].parsedStack[1].method)
```

<span data-ttu-id="7c116-267">È necessario eseguire il cast del risultato per il tipo appropriato.</span><span class="sxs-lookup"><span data-stu-id="7c116-267">Note that you need to cast the result to the appropriate type.</span></span>


## <a name="custom-properties-and-measurements"></a><span data-ttu-id="7c116-268">Proprietà e misure personalizzate</span><span class="sxs-lookup"><span data-stu-id="7c116-268">Custom properties and measurements</span></span>
<span data-ttu-id="7c116-269">Se l'applicazione associa agli eventi [dimensioni (proprietà) e misure personalizzate](app-insights-api-custom-events-metrics.md#properties), queste saranno visibili negli oggetti `customDimensions` e `customMeasurements`.</span><span class="sxs-lookup"><span data-stu-id="7c116-269">If your application attaches [custom dimensions (properties) and custom measurements](app-insights-api-custom-events-metrics.md#properties) to events, then you will see them in the `customDimensions` and `customMeasurements` objects.</span></span>

<span data-ttu-id="7c116-270">Ad esempio, se l'applicazione include:</span><span class="sxs-lookup"><span data-stu-id="7c116-270">For example, if your app includes:</span></span>

```C#

    var dimensions = new Dictionary<string, string>
                     {{"p1", "v1"},{"p2", "v2"}};
    var measurements = new Dictionary<string, double>
                     {{"m1", 42.0}, {"m2", 43.2}};
    telemetryClient.TrackEvent("myEvent", dimensions, measurements);
```

<span data-ttu-id="7c116-271">Per estrarre questi valori in Dati di analisi:</span><span class="sxs-lookup"><span data-stu-id="7c116-271">To extract these values in Analytics:</span></span>

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      m1 = todouble(customMeasurements.m1) // cast to expected type

```

<span data-ttu-id="7c116-272">Per verificare se una dimensione personalizzata è di tipo specifico:</span><span class="sxs-lookup"><span data-stu-id="7c116-272">To verify whether a custom dimension is of a particular type:</span></span>

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      iff(notnull(todouble(customMeasurements.m1)), ...
```

## <a name="dashboards"></a><span data-ttu-id="7c116-273">Dashboard</span><span class="sxs-lookup"><span data-stu-id="7c116-273">Dashboards</span></span>
<span data-ttu-id="7c116-274">È possibile aggiungere i risultati a un dashboard in modo da riunire tutti i grafici e le tabelle più importanti.</span><span class="sxs-lookup"><span data-stu-id="7c116-274">You can pin your results to a dashboard in order to bring together all your most important charts and tables.</span></span>

* <span data-ttu-id="7c116-275">[Dashboard condiviso di Azure](app-insights-dashboards.md#share-dashboards): fare clic sull'icona di aggiunta.</span><span class="sxs-lookup"><span data-stu-id="7c116-275">[Azure shared dashboard](app-insights-dashboards.md#share-dashboards): Click the pin icon.</span></span> <span data-ttu-id="7c116-276">Per poterlo fare, è necessario disporre di un dashboard condiviso.</span><span class="sxs-lookup"><span data-stu-id="7c116-276">Before you do this, you must have a shared dashboard.</span></span> <span data-ttu-id="7c116-277">Nel portale di Azure, aprire o creare un dashboard e fare clic su Condividi.</span><span class="sxs-lookup"><span data-stu-id="7c116-277">In the Azure portal, open or create a dashboard and click Share.</span></span>
* <span data-ttu-id="7c116-278">[Dashboard di Power BI](app-insights-export-power-bi.md): fare clic su Esporta, Power BI Query (Query Power BI).</span><span class="sxs-lookup"><span data-stu-id="7c116-278">[Power BI dashboard](app-insights-export-power-bi.md): Click Export, Power BI Query.</span></span> <span data-ttu-id="7c116-279">Un vantaggio di questa alternativa consiste nel fatto che è possibile visualizzare la query insieme ad altri risultati da un'ampia gamma di origini.</span><span class="sxs-lookup"><span data-stu-id="7c116-279">An advantage of this alternative is that you can display your query alongside other results from a wide range of sources.</span></span>

## <a name="combine-with-imported-data"></a><span data-ttu-id="7c116-280">Combinare con dati importati</span><span class="sxs-lookup"><span data-stu-id="7c116-280">Combine with imported data</span></span>

<span data-ttu-id="7c116-281">I report di Analisi hanno un ottimo aspetto nel dashboard, tuttavia a volte si desidera convertire i dati in un formato più semplice.</span><span class="sxs-lookup"><span data-stu-id="7c116-281">Analytics reports look great on the dashboard, but sometimes you want to translate the data to a more digestible form.</span></span> <span data-ttu-id="7c116-282">Si supponga, ad esempio, che gli utenti autenticati siano identificati nei dati di telemetria da un alias.</span><span class="sxs-lookup"><span data-stu-id="7c116-282">For example, suppose your authenticated users are identified in the telemetry by an alias.</span></span> <span data-ttu-id="7c116-283">Si desidera visualizzarne i nomi reali nei risultati.</span><span class="sxs-lookup"><span data-stu-id="7c116-283">You'd like to show their real names in your results.</span></span> <span data-ttu-id="7c116-284">A tale scopo, è necessario un file CSV con il mapping dagli alias ai nomi reali.</span><span class="sxs-lookup"><span data-stu-id="7c116-284">To do this, you need a CSV file that maps from the aliases to the real names.</span></span>

<span data-ttu-id="7c116-285">È possibile importare un file di dati e usarlo come qualsiasi tabella standard (richieste, eccezioni e così via).</span><span class="sxs-lookup"><span data-stu-id="7c116-285">You can import a data file and use it just like any of the standard tables (requests, exceptions, and so on).</span></span> <span data-ttu-id="7c116-286">Eseguire una query sulla propria tabella oppure aggiungerla ad altre tabelle.</span><span class="sxs-lookup"><span data-stu-id="7c116-286">Either query it on its own, or join it with other tables.</span></span> <span data-ttu-id="7c116-287">Ad esempio, se si dispone di una tabella denominata usermap contenente le colonne `realName` e `userId`, è possibile usarla per convertire il campo `user_AuthenticatedId` nei dati di telemetria della richiesta:</span><span class="sxs-lookup"><span data-stu-id="7c116-287">For example, if you have a table named usermap, and it has columns `realName` and `userId`, then you can use it to translate the `user_AuthenticatedId` field in the request telemetry:</span></span>

```AIQL

    requests
    | where notempty(user_AuthenticatedId)
    | project userId = user_AuthenticatedId
      // get the realName field from the usermap table:
    | join kind=leftouter ( usermap ) on userId
      // count transactions by name:
    | summarize count() by realName
```

<span data-ttu-id="7c116-288">Per importare in una tabella, nel pannello Schema, in **Altre origini dati**, seguire le istruzioni per aggiungere una nuova origine dati, caricando un campione dei dati.</span><span class="sxs-lookup"><span data-stu-id="7c116-288">To import a table, in the Schema blade, under **Other Data Sources**, follow the instructions to add a new data source, by uploading a sample of your data.</span></span> <span data-ttu-id="7c116-289">È quindi possibile usare questa definizione per caricare le tabelle.</span><span class="sxs-lookup"><span data-stu-id="7c116-289">Then you can use this definition to upload tables.</span></span>

<span data-ttu-id="7c116-290">La funzionalità di importazione è attualmente in anteprima e sarà inizialmente visualizzato un collegamento "Contattaci" in "Altre origini dati."</span><span class="sxs-lookup"><span data-stu-id="7c116-290">The import feature is currently in preview, so you will initially see a "Contact us" link under "Other data sources."</span></span> <span data-ttu-id="7c116-291">Usare questo collegamento per iscriversi al programma di anteprima. Il collegamento verrà puoi sostituito da un pulsante "Aggiungi nuova origine dati".</span><span class="sxs-lookup"><span data-stu-id="7c116-291">Use this to sign up to the preview program, and the link will then be replaced by an "Add new data source" button.</span></span>


## <a name="tables"></a><span data-ttu-id="7c116-292">Tabelle</span><span class="sxs-lookup"><span data-stu-id="7c116-292">Tables</span></span>
<span data-ttu-id="7c116-293">Il flusso di dati di telemetria ricevuto dall'app è accessibile tramite più tabelle.</span><span class="sxs-lookup"><span data-stu-id="7c116-293">The stream of telemetry received from your app is accessible through several tables.</span></span> <span data-ttu-id="7c116-294">Lo schema delle proprietà disponibili per ogni tabella è situato nella parte sinistra della finestra.</span><span class="sxs-lookup"><span data-stu-id="7c116-294">The schema of properties available for each table is visible at the left of the window.</span></span>

### <a name="requests-table"></a><span data-ttu-id="7c116-295">Tabella di richieste</span><span class="sxs-lookup"><span data-stu-id="7c116-295">Requests table</span></span>
<span data-ttu-id="7c116-296">Contare le richieste HTTP all'applicazione Web e il segmento in base al nome della pagina:</span><span class="sxs-lookup"><span data-stu-id="7c116-296">Count HTTP requests to your web app and segment by page name:</span></span>

![Richieste di conteggio segmentate per nome](./media/app-insights-analytics-tour/analytics-count-requests.png)

<span data-ttu-id="7c116-298">Trovare le richieste con il maggior numero di esiti negativi:</span><span class="sxs-lookup"><span data-stu-id="7c116-298">Find the requests that fail most:</span></span>

![Richieste di conteggio segmentate per nome](./media/app-insights-analytics-tour/analytics-failed-requests.png)

### <a name="custom-events-table"></a><span data-ttu-id="7c116-300">Tabella di eventi personalizzati</span><span class="sxs-lookup"><span data-stu-id="7c116-300">Custom events table</span></span>
<span data-ttu-id="7c116-301">Se si usa [Trackevent()](app-insights-api-custom-events-metrics.md#trackevent) per inviare eventi personalizzati, è possibile leggerli da questa tabella.</span><span class="sxs-lookup"><span data-stu-id="7c116-301">If you use [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) to send your own events, you can read them from this table.</span></span>

<span data-ttu-id="7c116-302">Esaminiamo un esempio in cui il codice dell'app contiene le righe seguenti:</span><span class="sxs-lookup"><span data-stu-id="7c116-302">Let's take an example where your app code contains these lines:</span></span>

```C#

    telemetry.TrackEvent("Query",
       new Dictionary<string,string> {{"query", sqlCmd}},
       new Dictionary<string,double> {
           {"retry", retryCount},
           {"querytime", totalTime}})
```

<span data-ttu-id="7c116-303">Visualizzare la frequenza di questi eventi:</span><span class="sxs-lookup"><span data-stu-id="7c116-303">Display the frequency of these events:</span></span>

![Frequenza di visualizzazione degli eventi personalizzati](./media/app-insights-analytics-tour/analytics-custom-events-rate.png)

<span data-ttu-id="7c116-305">Estrarre le misure e le dimensioni degli eventi:</span><span class="sxs-lookup"><span data-stu-id="7c116-305">Extract measurements and dimensions from the events:</span></span>

![Frequenza di visualizzazione degli eventi personalizzati](./media/app-insights-analytics-tour/analytics-custom-events-dimensions.png)

### <a name="custom-metrics-table"></a><span data-ttu-id="7c116-307">Tabella delle metriche personalizzate</span><span class="sxs-lookup"><span data-stu-id="7c116-307">Custom metrics table</span></span>
<span data-ttu-id="7c116-308">Se si usa [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) per inviare i valori metrici, i risultati sono disponibili nel flusso **customMetrics**.</span><span class="sxs-lookup"><span data-stu-id="7c116-308">If you are using [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) to send your own metric values, you’ll find its results in the **customMetrics** stream.</span></span> <span data-ttu-id="7c116-309">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="7c116-309">For example:</span></span>  

![Metriche personalizzate in Application Insights - Analisi](./media/app-insights-analytics-tour/analytics-custom-metrics.png)

> [!NOTE]
> <span data-ttu-id="7c116-311">In [Esplora metriche](app-insights-metrics-explorer.md) tutte le misurazioni personalizzate associate a qualsiasi tipo di telemetria vengono visualizzate insieme nel pannello delle metriche, con le metriche inviate usando `TrackMetric()`.</span><span class="sxs-lookup"><span data-stu-id="7c116-311">In [Metrics Explorer](app-insights-metrics-explorer.md), all custom measurements attached to any type of telemetry appear together in the metrics blade along with metrics sent using `TrackMetric()`.</span></span> <span data-ttu-id="7c116-312">In Analisi, invece, le misure personalizzate sono ancora associate al tipo di telemetria su cui sono state rilevate, come eventi, richieste e così via, mentre le metriche inviate da TrackMetric vengono visualizzate all'interno del proprio flusso.</span><span class="sxs-lookup"><span data-stu-id="7c116-312">But in Analytics, custom measurements are still attached to whichever type of telemetry they were carried on - events or requests, and so on - while metrics sent by TrackMetric appear in their own stream.</span></span>
>
>

### <a name="performance-counters-table"></a><span data-ttu-id="7c116-313">Tabella dei contatori delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="7c116-313">Performance counters table</span></span>
<span data-ttu-id="7c116-314">[I contatori delle prestazioni](app-insights-performance-counters.md) mostrano le metriche base del sistema per l'applicazione, ad esempio CPU, memoria e uso della rete.</span><span class="sxs-lookup"><span data-stu-id="7c116-314">[Performance counters](app-insights-performance-counters.md) show you basic system metrics for your app, such as CPU, memory, and network utilization.</span></span> <span data-ttu-id="7c116-315">È possibile configurare l'SDK per inviare contatori aggiuntivi, tra cui contatori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="7c116-315">You can configure the SDK to send additional counters, including your own custom counters.</span></span>

<span data-ttu-id="7c116-316">Lo schema **performanceCounters** espone `category`, il nome `counter` e il nome `instance` per ogni contatore delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="7c116-316">The **performanceCounters** schema exposes the `category`, `counter` name, and `instance` name of each performance counter.</span></span> <span data-ttu-id="7c116-317">I nomi delle istanze di contatore sono applicabili solo ad alcuni contatori delle prestazioni e indicano in genere il nome del processo a cui il conteggio si riferisce.</span><span class="sxs-lookup"><span data-stu-id="7c116-317">Counter instance names are only applicable to some performance counters, and typically indicate the name of the process to which the count relates.</span></span> <span data-ttu-id="7c116-318">Nei dati di telemetria per ogni applicazione verranno visualizzati solo i contatori per l'applicazione specifica.</span><span class="sxs-lookup"><span data-stu-id="7c116-318">In the telemetry for each application, you’ll see only the counters for that application.</span></span> <span data-ttu-id="7c116-319">Ad esempio, per visualizzare quali contatori sono disponibili:</span><span class="sxs-lookup"><span data-stu-id="7c116-319">For example, to see what counters are available:</span></span>

![Contatori delle prestazioni in Application Insights - Analisi](./media/app-insights-analytics-tour/analytics-performance-counters.png)

<span data-ttu-id="7c116-321">Per ottenere un grafico della memoria disponibile nel periodo selezionato:</span><span class="sxs-lookup"><span data-stu-id="7c116-321">To get a chart of available memory over the selected period:</span></span>

![Timechart delle metriche in Application Insights - Analisi](./media/app-insights-analytics-tour/analytics-available-memory.png)

<span data-ttu-id="7c116-323">Come altri dati di telemetria, **performanceCounters** contiene anche una colonna `cloud_RoleInstance` che indica l'identità del computer host in cui è in esecuzione l'app.</span><span class="sxs-lookup"><span data-stu-id="7c116-323">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates the identity of the host machine on which your app is running.</span></span> <span data-ttu-id="7c116-324">Ad esempio, per confrontare le prestazioni dell'applicazione su computer diversi:</span><span class="sxs-lookup"><span data-stu-id="7c116-324">For example, to compare the performance of your app on the different machines:</span></span>

![Prestazioni segmentate per istanze del ruolo in Application Insights - Analisi](./media/app-insights-analytics-tour/analytics-metrics-role-instance.png)

### <a name="exceptions-table"></a><span data-ttu-id="7c116-326">Tabelle delle eccezioni</span><span class="sxs-lookup"><span data-stu-id="7c116-326">Exceptions table</span></span>
<span data-ttu-id="7c116-327">[Le eccezioni segnalate dall'app](app-insights-asp-net-exceptions.md) sono disponibili in questa tabella.</span><span class="sxs-lookup"><span data-stu-id="7c116-327">[Exceptions reported by your app](app-insights-asp-net-exceptions.md) are available in this table.</span></span>

<span data-ttu-id="7c116-328">Per trovare la richiesta HTTP che l'app gestiva al momento del rilevamento dell'eccezione, creare un join in operation_Id:</span><span class="sxs-lookup"><span data-stu-id="7c116-328">To find the HTTP request that your app was handling when the exception was raised, join on operation_Id:</span></span>

![Creare un join delle eccezioni con le richieste in operation_Id](./media/app-insights-analytics-tour/analytics-exception-request.png)

### <a name="browser-timings-table"></a><span data-ttu-id="7c116-330">Tabella delle tempistiche del browser</span><span class="sxs-lookup"><span data-stu-id="7c116-330">Browser timings table</span></span>
<span data-ttu-id="7c116-331">`browserTimings` mostra i dati di caricamento della pagina raccolti nel browser degli utenti.</span><span class="sxs-lookup"><span data-stu-id="7c116-331">`browserTimings` shows page load data collected in your users' browsers.</span></span>

<span data-ttu-id="7c116-332">[Configurare l'app per la telemetria sul lato client](app-insights-javascript.md) per visualizzare queste metriche.</span><span class="sxs-lookup"><span data-stu-id="7c116-332">[Set up your app for client-side telemetry](app-insights-javascript.md) in order to see these metrics.</span></span>

<span data-ttu-id="7c116-333">Lo schema include [metriche che indicano la lunghezza delle varie fasi del processo di caricamento della pagina](app-insights-javascript.md#page-load-performance).</span><span class="sxs-lookup"><span data-stu-id="7c116-333">The schema includes [metrics indicating the lengths of different stages of the page loading process](app-insights-javascript.md#page-load-performance).</span></span> <span data-ttu-id="7c116-334">Le metriche non indicano il tempo trascorso dagli utenti a leggere una pagina.</span><span class="sxs-lookup"><span data-stu-id="7c116-334">(They don’t indicate the length of time your users read a page.)</span></span>  

<span data-ttu-id="7c116-335">Le metriche mostrano la popolarità delle diverse pagine e i tempi di caricamento di ogni pagina:</span><span class="sxs-lookup"><span data-stu-id="7c116-335">Show the popularities of different pages, and load times for each page:</span></span>

![Tempistiche di caricamento delle pagine in Analisi](./media/app-insights-analytics-tour/analytics-page-load.png)

### <a name="availability-results-table"></a><span data-ttu-id="7c116-337">Tabella dei risultati di disponibilità</span><span class="sxs-lookup"><span data-stu-id="7c116-337">Availability results table</span></span>
<span data-ttu-id="7c116-338">`availabilityResults` mostra i risultati dei [test Web](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="7c116-338">`availabilityResults` shows the results of your [web tests](app-insights-monitor-web-app-availability.md).</span></span> <span data-ttu-id="7c116-339">Ogni esecuzione di test da ogni posizione di test viene segnalata separatamente.</span><span class="sxs-lookup"><span data-stu-id="7c116-339">Each run of your tests from each test location is reported separately.</span></span>

![Tempistiche di caricamento delle pagine in Analisi](./media/app-insights-analytics-tour/analytics-availability.png)

### <a name="dependencies-table"></a><span data-ttu-id="7c116-341">Tabella delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="7c116-341">Dependencies table</span></span>
<span data-ttu-id="7c116-342">Contiene i risultati delle chiamate che l'applicazione esegue sul database e sull'API REST e le chiamate a TrackDependency().</span><span class="sxs-lookup"><span data-stu-id="7c116-342">Contains results of calls that your app makes to databases and REST APIs, and other calls to TrackDependency().</span></span> <span data-ttu-id="7c116-343">Include inoltre le chiamate AJAX effettuate dal browser.</span><span class="sxs-lookup"><span data-stu-id="7c116-343">Also includes AJAX calls made from the browser.</span></span>

<span data-ttu-id="7c116-344">Chiamate AJAX dal browser:</span><span class="sxs-lookup"><span data-stu-id="7c116-344">AJAX calls from the browser:</span></span>

```AIQL

    dependencies | where client_Type == "Browser"
    | take 10
```

<span data-ttu-id="7c116-345">Chiamate di dipendenza dal server:</span><span class="sxs-lookup"><span data-stu-id="7c116-345">Dependency calls from the server:</span></span>

```AIQL

    dependencies | where client_Type == "PC"
    | take 10
```

<span data-ttu-id="7c116-346">I risultati della dipendenza lato server mostrano sempre `success==False` se l'agente Application Insights non è installato.</span><span class="sxs-lookup"><span data-stu-id="7c116-346">Server-side dependency results always show `success==False` if the Application Insights Agent is not installed.</span></span> <span data-ttu-id="7c116-347">Tuttavia, gli altri dati sono corretti.</span><span class="sxs-lookup"><span data-stu-id="7c116-347">However, the other data are correct.</span></span>

### <a name="traces-table"></a><span data-ttu-id="7c116-348">Tabella delle tracce</span><span class="sxs-lookup"><span data-stu-id="7c116-348">Traces table</span></span>
<span data-ttu-id="7c116-349">Contiene i dati di telemetria inviati dall'app tramite TrackTrace() o [altri framework di registrazione](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="7c116-349">Contains the telemetry sent by your app using TrackTrace(), or [other logging frameworks](app-insights-asp-net-trace-logs.md).</span></span>

## <a name="video"></a><span data-ttu-id="7c116-350">Video</span><span class="sxs-lookup"><span data-stu-id="7c116-350">Video</span></span> 

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

<span data-ttu-id="7c116-351">Query avanzate:</span><span class="sxs-lookup"><span data-stu-id="7c116-351">Advanced queries:</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Build/2016/P591/player]


## <a name="next-steps"></a><span data-ttu-id="7c116-352">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7c116-352">Next steps</span></span>
* [<span data-ttu-id="7c116-353">Informazioni di riferimento sul linguaggio di Analisi</span><span class="sxs-lookup"><span data-stu-id="7c116-353">Analytics language reference</span></span>](app-insights-analytics-reference.md)
* <span data-ttu-id="7c116-354">Il [foglio informativo sugli utenti SQL](https://aka.ms/sql-analytics) traduce i linguaggi più comuni.</span><span class="sxs-lookup"><span data-stu-id="7c116-354">[SQL-users' cheat sheet](https://aka.ms/sql-analytics) translates the most common idioms.</span></span>

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]
