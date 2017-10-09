---
title: Panoramica aaaA Analitica in Azure Application Insights | Documenti Microsoft
description: Brevi esempi di tutte le query principale hello in Analitica, hello potente strumento di ricerca di Application Insights.
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
ms.openlocfilehash: c268e26c6bf93ac2ee2a9d5e83613150dcf90b04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="a-tour-of-analytics-in-application-insights"></a><span data-ttu-id="a8a0f-103">Presentazione dello strumento Analisi in Application Insights</span><span class="sxs-lookup"><span data-stu-id="a8a0f-103">A tour of Analytics in Application Insights</span></span>
<span data-ttu-id="a8a0f-104">[Analitica](app-insights-analytics.md) è hello ricerca potenti funzionalità di [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a8a0f-104">[Analytics](app-insights-analytics.md) is hello powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="a8a0f-105">Queste pagine descrivono il linguaggio di query di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-105">These pages describe the Log Analytics query language.</span></span>

* <span data-ttu-id="a8a0f-106">**[Guardare video introduttivo hello](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-106">**[Watch hello introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="a8a0f-107">**[Test unità Analitica dei dati simulati](https://analytics.applicationinsights.io/demo)**  se l'applicazione non invia dati tooApplication Insights ancora.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data tooApplication Insights yet.</span></span>
* <span data-ttu-id="a8a0f-108">**[SQL utenti schede di riferimento rapido](https://aka.ms/sql-analytics)**  traduce idiomi comuni hello.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-108">**[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates hello most common idioms.</span></span>

<span data-ttu-id="a8a0f-109">Di seguito è una procedura tooget alcune query di base che è stato avviato.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-109">Let's take a walk through some basic queries tooget you started.</span></span>

## <a name="connect-tooyour-application-insights-data"></a><span data-ttu-id="a8a0f-110">Connettere i dati di Application Insights tooyour</span><span class="sxs-lookup"><span data-stu-id="a8a0f-110">Connect tooyour Application Insights data</span></span>
<span data-ttu-id="a8a0f-111">Aprire Analisi dal [pannello Panoramica](app-insights-dashboards.md) dell'app in Application Insights:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-111">Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights:</span></span>

![In portal.azure.com, aprire la risorsa di Application Insights e selezionare Analytics.](./media/app-insights-analytics-tour/001.png)

## <a name="takehttpsdocsloganalyticsioquerylanguagequerylanguagetakeoperatorhtml-show-me-n-rows"></a><span data-ttu-id="a8a0f-113">[Take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): visualizzare n righe</span><span class="sxs-lookup"><span data-stu-id="a8a0f-113">[Take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): show me n rows</span></span>
<span data-ttu-id="a8a0f-114">I punti dati che registrano le operazioni degli utenti (in genere richieste HTTP ricevute dall'app Web) vengono archiviati in una tabella denominata `requests`.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-114">Data points that log user operations (typically HTTP requests received by your web app) are stored in a table called `requests`.</span></span> <span data-ttu-id="a8a0f-115">Ogni riga è un punto dati di telemetria ricevuto da hello Application Insights SDK nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-115">Each row is a telemetry data point received from hello Application Insights SDK in your app.</span></span>

<span data-ttu-id="a8a0f-116">Per iniziare, esaminare alcune righe di esempio di tabella hello:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-116">Let's start by examining a few sample rows of hello table:</span></span>

![results](./media/app-insights-analytics-tour/010.png)

> [!NOTE]
> <span data-ttu-id="a8a0f-118">Inserire un punto qualsiasi cursore hello nell'istruzione hello prima di fare clic.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-118">Put hello cursor somewhere in hello statement before you click Go.</span></span> <span data-ttu-id="a8a0f-119">È possibile suddividere un'istruzione su più righe, ma non inserire righe vuote in un'istruzione.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-119">You can split a statement over more than one line, but don't put blank lines in a statement.</span></span> <span data-ttu-id="a8a0f-120">Le righe vuote sono un modo pratico di tookeep diversi separare le query nella finestra di hello.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-120">Blank lines are a convenient way tookeep several separate queries in hello window.</span></span>
>
>

<span data-ttu-id="a8a0f-121">Scegliere le colonne, trascinarle, creare gruppi in base alle colonne e applicare filtri:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-121">Choose columns, drag them, group by columns, and filter:</span></span>

![Fare clic sulla selezione di colonna in alto a destra dei risultati](./media/app-insights-analytics-tour/030.png)

<span data-ttu-id="a8a0f-123">Espandere i dettagli hello toosee qualsiasi articolo:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-123">Expand any item toosee hello detail:</span></span>

![Scegliere Tabella e usare Configura colonne](./media/app-insights-analytics-tour/040.png)

> [!NOTE]
> <span data-ttu-id="a8a0f-125">Fare clic sull'intestazione hello risultati una colonna toore ordine hello disponibile nel browser hello.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-125">Click hello head of a column toore-order hello results available in hello web browser.</span></span> <span data-ttu-id="a8a0f-126">Tuttavia, tenere presente che per un set di risultati di grandi dimensioni, hello numero di righe scaricate toohello browser è limitato.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-126">But be aware that for a large result set, hello number of rows downloaded toohello browser is limited.</span></span> <span data-ttu-id="a8a0f-127">In questo modo di ordinamento non viene visualizzato sempre si hello effettiva più alta o più basso degli elementi.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-127">Sorting this way doesn't always show you hello actual highest or lowest items.</span></span> <span data-ttu-id="a8a0f-128">gli elementi di toosort usano in modo affidabile, hello `top` o `sort` operatore.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-128">toosort items reliably, use hello `top` or `sort` operator.</span></span>
>
>

## <a name="tophttpsdocsloganalyticsioquerylanguagequerylanguagetopoperatorhtml-and-sorthttpsdocsloganalyticsioquerylanguagequerylanguagesortoperatorhtml"></a><span data-ttu-id="a8a0f-129">[Top](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) e [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)</span><span class="sxs-lookup"><span data-stu-id="a8a0f-129">[Top](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) and [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)</span></span>
<span data-ttu-id="a8a0f-130">`take`è utile tooget un rapido esempio di un risultato, ma sono visualizzate le righe dalla tabella hello in nessun ordine particolare.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-130">`take` is useful tooget a quick sample of a result, but it shows rows from hello table in no particular order.</span></span> <span data-ttu-id="a8a0f-131">utilizzare una visualizzazione ordinata, tooget `top` (per un esempio) o `sort` (su hello intera tabella).</span><span class="sxs-lookup"><span data-stu-id="a8a0f-131">tooget an ordered view, use `top` (for a sample) or `sort` (over hello whole table).</span></span>

<span data-ttu-id="a8a0f-132">Mostra hello prime n righe, ordinate in base a una colonna specifica:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-132">Show me hello first n rows, ordered by a particular column:</span></span>

```AIQL

    requests | top 10 by timestamp desc
```

* <span data-ttu-id="a8a0f-133">*Sintassi:* la maggior parte degli operatori ha parametri di tipo parola chiave, ad esempio `by`.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-133">*Syntax:* Most operators have keyword parameters such as `by`.</span></span>
* <span data-ttu-id="a8a0f-134">`desc` = ordine decrescente, `asc` = ordine crescente.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-134">`desc` = descending order, `asc` = ascending.</span></span>

![](./media/app-insights-analytics-tour/260.png)

<span data-ttu-id="a8a0f-135">`top...` è più efficiente di `sort ... | take...`.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-135">`top...` is a more performant way of saying `sort ... | take...`.</span></span> <span data-ttu-id="a8a0f-136">Si sarebbe potuto scrivere:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-136">We could have written:</span></span>

```AIQL

    requests | sort by timestamp desc | take 10
```

<span data-ttu-id="a8a0f-137">il risultato di Hello sarebbe hello stesso, ma verrà eseguito un po' più lentamente.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-137">hello result would be hello same, but it would run a bit more slowly.</span></span> <span data-ttu-id="a8a0f-138">Sarebbe stato anche possibile scrivere `order`, che è un alias di `sort`.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-138">(You could also write `order`, which is an alias of `sort`.)</span></span>

<span data-ttu-id="a8a0f-139">le intestazioni di colonna Hello nella visualizzazione tabella hello possono inoltre essere utilizzati toosort hello risultati sullo schermo hello.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-139">hello column headers in hello table view can also be used toosort hello results on hello screen.</span></span> <span data-ttu-id="a8a0f-140">Ma ovviamente, se è stato usato `take` o `top` tooretrieve solo parte di una tabella, sarà possibile solo modificare l'ordine hello record è stato recuperato.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-140">But of course, if you've used `take` or `top` tooretrieve just part of a table, you'll only re-order hello records you've retrieved.</span></span>

## <a name="wherehttpsdocsloganalyticsioquerylanguagequerylanguagewhereoperatorhtml-filtering-on-a-condition"></a><span data-ttu-id="a8a0f-141">[Where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): filtrare in base a una condizione</span><span class="sxs-lookup"><span data-stu-id="a8a0f-141">[Where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): filtering on a condition</span></span>

<span data-ttu-id="a8a0f-142">Di seguito sono illustrate solo le richieste che hanno restituito un particolare codice di risultato:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-142">Let's see just requests that returned a particular result code:</span></span>

```AIQL

    requests
    | where resultCode  == "404"
    | take 10
```

![](./media/app-insights-analytics-tour/250.png)

<span data-ttu-id="a8a0f-143">Hello `where` l'operatore accetta un'espressione booleana.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-143">hello `where` operator takes a Boolean expression.</span></span> <span data-ttu-id="a8a0f-144">Tenere presente i punti chiave seguenti:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-144">Here are some key points about them:</span></span>

* <span data-ttu-id="a8a0f-145">`and`, `or`: operatori booleani</span><span class="sxs-lookup"><span data-stu-id="a8a0f-145">`and`, `or`: Boolean operators</span></span>
* <span data-ttu-id="a8a0f-146">`==`, `<>`, `!=`: uguale a e non uguale a</span><span class="sxs-lookup"><span data-stu-id="a8a0f-146">`==`, `<>`, `!=` : equal and not equal</span></span>
* <span data-ttu-id="a8a0f-147">`=~`, `!~`: stringa senza distinzione tra maiuscole e minuscole uguale a e non uguale a.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-147">`=~`, `!~` : case-insensitive string equal and not equal.</span></span> <span data-ttu-id="a8a0f-148">Sono disponibili numerosi altri operatori di confronto delle stringhe.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-148">There are lots more string comparison operators.</span></span>

<!---Read all about [scalar expressions]().--->

### <a name="getting-hello-right-type"></a><span data-ttu-id="a8a0f-149">Recupero di tipo corretto di hello</span><span class="sxs-lookup"><span data-stu-id="a8a0f-149">Getting hello right type</span></span>
<span data-ttu-id="a8a0f-150">Individuare le richieste non riuscite:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-150">Find unsuccessful requests:</span></span>

```AIQL

    requests
    | where isnotempty(resultCode) and toint(resultCode) >= 400
```
<!---
`resultCode` has type string, so we must cast it app-insights-analytics-reference.md#casts for a numeric comparison.
--->

## <a name="time"></a><span data-ttu-id="a8a0f-151">Tempo</span><span class="sxs-lookup"><span data-stu-id="a8a0f-151">Time</span></span>

<span data-ttu-id="a8a0f-152">Per impostazione predefinita, le query sono limitato toohello ultime 24 ore.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-152">By default, your queries are restricted toohello last 24 hours.</span></span> <span data-ttu-id="a8a0f-153">Questo intervallo, però, può essere modificato:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-153">But you can change this range:</span></span>

![](./media/app-insights-analytics-tour/change-time-range.png)

<span data-ttu-id="a8a0f-154">Eseguire l'override di intervallo di tempo hello scrivendo una query che include la `timestamp` in una clausola where.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-154">Override hello time range by writing any query that mentions `timestamp` in a where-clause.</span></span> <span data-ttu-id="a8a0f-155">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-155">For example:</span></span>

```AIQL

    // What were hello slowest requests over hello past 3 days?
    requests
    | where timestamp > ago(3d)  // Override hello time range
    | top 5 by duration
```

<span data-ttu-id="a8a0f-156">funzionalità di intervallo di tempo Hello è equivalente tooa 'where' clausola inserita dopo ogni indicazione di una delle tabelle di origine hello.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-156">hello time range feature is equivalent tooa 'where' clause inserted after each mention of one of hello source tables.</span></span>

<span data-ttu-id="a8a0f-157">`ago(3d)` significa 'tre giorni fa'.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-157">`ago(3d)` means 'three days ago'.</span></span> <span data-ttu-id="a8a0f-158">Le altre unità di tempo includono ore (`2h`, `2.5h`), minuti (`25m`) e secondi (`10s`).</span><span class="sxs-lookup"><span data-stu-id="a8a0f-158">Other units of time include hours (`2h`, `2.5h`), minutes (`25m`), and seconds (`10s`).</span></span>

<span data-ttu-id="a8a0f-159">Altri esempi:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-159">Other examples:</span></span>

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

<span data-ttu-id="a8a0f-160">[Riferimento su date e ore](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).</span><span class="sxs-lookup"><span data-stu-id="a8a0f-160">[Dates and times reference](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).</span></span>


## <a name="projecthttpsdocsloganalyticsioquerylanguagequerylanguageprojectoperatorhtml-select-rename-and-compute-columns"></a><span data-ttu-id="a8a0f-161">[Project](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): selezionare, rinominare e calcolare le colonne</span><span class="sxs-lookup"><span data-stu-id="a8a0f-161">[Project](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): select, rename, and compute columns</span></span>
<span data-ttu-id="a8a0f-162">Utilizzare [ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) toopick out solo le colonne hello desiderate:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-162">Use [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) toopick out just hello columns you want:</span></span>

```AIQL

    requests | top 10 by timestamp desc
             | project timestamp, name, resultCode
```

![](./media/app-insights-analytics-tour/240.png)

<span data-ttu-id="a8a0f-163">È inoltre possibile rinominare le colonne e definire nuove colonne:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-163">You can also rename columns and define new ones:</span></span>

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

* <span data-ttu-id="a8a0f-165">I nomi di colonna possono includere spazi o simboli se sono racchiusi tra parentesi quadre, ad esempio: `['...']` o `["..."]`</span><span class="sxs-lookup"><span data-stu-id="a8a0f-165">Column names can include spaces or symbols if they are bracketed like this: `['...']` or `["..."]`</span></span>
* <span data-ttu-id="a8a0f-166">`%`è normale operatore modulo hello.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-166">`%` is hello usual modulo operator.</span></span>
* <span data-ttu-id="a8a0f-167">`1d` (la cifra uno seguita da "d") è il valore letterale di un intervallo di tempo che indica un giorno.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-167">`1d` (that's a digit one, then a 'd') is a timespan literal meaning one day.</span></span> <span data-ttu-id="a8a0f-168">Ecco altri valori letterali di intervallo di tempo: `12h`, `30m`, `10s`, `0.01s`.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-168">Here are some more timespan literals: `12h`, `30m`, `10s`, `0.01s`.</span></span>
* <span data-ttu-id="a8a0f-169">`floor`(alias `bin`) Arrotonda un valore basso toohello multiplo del valore di base hello è fornire più vicino.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-169">`floor` (alias `bin`) rounds a value down toohello nearest multiple of hello base value you provide.</span></span> <span data-ttu-id="a8a0f-170">Pertanto `floor(aTime, 1s)` Arrotonda volta verso il basso toohello più vicino al secondo.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-170">So `floor(aTime, 1s)` rounds a time down toohello nearest second.</span></span>

<span data-ttu-id="a8a0f-171">Le espressioni possono includere tutti gli operatori di solito hello (`+`, `-`,...), ed è presente una gamma di funzioni utili.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-171">Expressions can include all hello usual operators (`+`, `-`, ...), and there's a range of useful functions.</span></span>

## <a name="extend"></a><span data-ttu-id="a8a0f-172">Extend</span><span class="sxs-lookup"><span data-stu-id="a8a0f-172">Extend</span></span>
<span data-ttu-id="a8a0f-173">Se si desidera tooadd colonne toohello quelli esistenti, utilizzare [ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):</span><span class="sxs-lookup"><span data-stu-id="a8a0f-173">If you just want tooadd columns toohello existing ones, use [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | extend timeOfDay = floor(timestamp % 1d, 1s)
```

<span data-ttu-id="a8a0f-174">Utilizzando [ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) risulta meno dettagliata [ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) se si desidera tookeep tutti hello colonne esistenti.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-174">Using [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) is less verbose than [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) if you want tookeep all hello existing columns.</span></span>

### <a name="convert-toolocal-time"></a><span data-ttu-id="a8a0f-175">Converte l'ora toolocal</span><span class="sxs-lookup"><span data-stu-id="a8a0f-175">Convert toolocal time</span></span>

<span data-ttu-id="a8a0f-176">I timestamp sono sempre espressi in formato UTC.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-176">Timestamps are always in UTC.</span></span> <span data-ttu-id="a8a0f-177">Pertanto se è l'inverno costa ci Pacifico hello, si potrebbe essere come segue:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-177">So if you're on hello US Pacific coast and it's winter, you might like this:</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | extend localTime = timestamp - 8h
```


## <a name="summarizehttpsdocsloganalyticsioquerylanguagequerylanguagesummarizeoperatorhtml-aggregate-groups-of-rows"></a><span data-ttu-id="a8a0f-178">[Summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): aggregare gruppi di righe</span><span class="sxs-lookup"><span data-stu-id="a8a0f-178">[Summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): aggregate groups of rows</span></span>
<span data-ttu-id="a8a0f-179">`Summarize` applica una *funzione di aggregazione* specificata a gruppi di righe.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-179">`Summarize` applies a specified *aggregation function* over groups of rows.</span></span>

<span data-ttu-id="a8a0f-180">Ad esempio, in cui viene segnalato hello tempo app web toorespond tooa richiesta nel campo hello `duration`.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-180">For example, hello time your web app takes toorespond tooa request is reported in hello field `duration`.</span></span> <span data-ttu-id="a8a0f-181">Vediamo medio di risposta hello ora tooall richieste:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-181">Let's see hello average response time tooall requests:</span></span>

![](./media/app-insights-analytics-tour/410.png)

<span data-ttu-id="a8a0f-182">In alternativa, è possibile separare il risultato di hello in richieste di nomi diversi:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-182">Or we could separate hello result into requests of different names:</span></span>

![](./media/app-insights-analytics-tour/420.png)

<span data-ttu-id="a8a0f-183">`Summarize`raccoglie hello punti dati nel flusso hello in gruppi per cui hello `by` clausola restituisce in modo uniforme.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-183">`Summarize` collects hello data points in hello stream into groups for which hello `by` clause evaluates equally.</span></span> <span data-ttu-id="a8a0f-184">Ogni valore in hello `by` espressione - ogni nome di operazione in hello sopra riportato, restituisce una riga nella tabella risultati hello.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-184">Each value in hello `by` expression - each operation name in hello above example - results in a row in hello result table.</span></span>

<span data-ttu-id="a8a0f-185">È anche possibile raggruppare i risultati per ora del giorno:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-185">Or we could group results by time of day:</span></span>

![](./media/app-insights-analytics-tour/430.png)

<span data-ttu-id="a8a0f-186">Si noti come utilizziamo hello `bin` funzione (noto anche come `floor`).</span><span class="sxs-lookup"><span data-stu-id="a8a0f-186">Notice how we're using hello `bin` function (aka `floor`).</span></span> <span data-ttu-id="a8a0f-187">Se si usasse solo `by timestamp`, ogni riga di input finirebbe in un piccolo gruppo distinto.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-187">If we just used `by timestamp`, every input row would end up in its own little group.</span></span> <span data-ttu-id="a8a0f-188">Per qualsiasi scalari continua volte like o numeri, abbiamo toobreak intervallo continuo di hello in un numero gestibile di valori discreti.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-188">For any continuous scalar like times or numbers, we have toobreak hello continuous range into a manageable number of discrete values.</span></span> <span data-ttu-id="a8a0f-189">`bin`-che è appena hello familiarità di arrotondamento a discesa `floor` funzione - è toodo modo più semplice hello che.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-189">`bin` - which is just hello familiar rounding-down `floor` function - is hello easiest way toodo that.</span></span>

<span data-ttu-id="a8a0f-190">È possibile utilizzare hello stessa tecnica tooreduce gli intervalli di stringhe:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-190">We can use hello same technique tooreduce ranges of strings:</span></span>

![](./media/app-insights-analytics-tour/440.png)

<span data-ttu-id="a8a0f-191">Si noti che è possibile utilizzare `name=` nome hello tooset di una colonna di risultati, in espressioni di aggregazione hello o hello-clausola by.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-191">Notice that you can use `name=` tooset hello name of a result column, either in hello aggregation expressions or hello by-clause.</span></span>

## <a name="counting-sampled-data"></a><span data-ttu-id="a8a0f-192">Conteggio dei dati campionati</span><span class="sxs-lookup"><span data-stu-id="a8a0f-192">Counting sampled data</span></span>
<span data-ttu-id="a8a0f-193">`sum(itemCount)`è consigliato in hello aggregazione toocount eventi.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-193">`sum(itemCount)` is hello recommended aggregation toocount events.</span></span> <span data-ttu-id="a8a0f-194">In molti casi, itemCount = = 1, pertanto la funzione hello semplicemente conta il numero di hello di righe nel gruppo di hello.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-194">In many cases, itemCount==1, so hello function simply counts up hello number of rows in hello group.</span></span> <span data-ttu-id="a8a0f-195">Ma quando [campionamento](app-insights-sampling.md) è nell'operazione, solo una frazione di eventi di hello originale vengono mantenute come punti dati di Application Insights, in modo che per ogni punto dati viene visualizzato, esistono `itemCount` eventi.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-195">But when [sampling](app-insights-sampling.md) is in operation, only a fraction of hello original events are retained as data points in Application Insights, so that for each data point you see, there are `itemCount` events.</span></span>

<span data-ttu-id="a8a0f-196">Ad esempio, se il campionamento Elimina 75% di eventi di hello originale, quindi itemCount = = 4 in record hello mantenuto -, ovvero per ogni record conservate, sono disponibili quattro record originale.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-196">For example, if sampling discards 75% of hello original events, then itemCount==4 in hello retained records - that is, for every retained record, there were four original records.</span></span>

<span data-ttu-id="a8a0f-197">Campionamento adattivo causa itemCount toobe superiore durante i periodi di quando l'applicazione viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-197">Adaptive sampling causes itemCount toobe higher during periods when your application is being heavily used.</span></span>

<span data-ttu-id="a8a0f-198">Riepilogando itemCount fornisce pertanto una buona stima del numero originale di hello di eventi.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-198">Summing up itemCount therefore gives a good estimate of hello original number of events.</span></span>

![](./media/app-insights-analytics-tour/510.png)

<span data-ttu-id="a8a0f-199">È inoltre disponibile un `count()` casi in cui si vuole numero hello toocount di righe in un gruppo di aggregazione (e un'operazione count).</span><span class="sxs-lookup"><span data-stu-id="a8a0f-199">There's also a `count()` aggregation (and a count operation), for cases where you really do want toocount hello number of rows in a group.</span></span>

<span data-ttu-id="a8a0f-200">Esiste un intervallo di [funzioni di aggregazione](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span><span class="sxs-lookup"><span data-stu-id="a8a0f-200">There's a range of [aggregation functions](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span></span>

## <a name="charting-hello-results"></a><span data-ttu-id="a8a0f-201">Creazione di grafici di risultati hello</span><span class="sxs-lookup"><span data-stu-id="a8a0f-201">Charting hello results</span></span>
```AIQL

    exceptions
       | summarize count=sum(itemCount)  
         by bin(timestamp, 1h)
```

<span data-ttu-id="a8a0f-202">Per impostazione predefinita, i risultati vengono visualizzati sotto forma di tabella:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-202">By default, results display as a table:</span></span>

![](./media/app-insights-analytics-tour/225.png)

<span data-ttu-id="a8a0f-203">Possiamo migliori rispetto alla visualizzazione tabella hello.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-203">We can do better than hello table view.</span></span> <span data-ttu-id="a8a0f-204">Con l'opzione di barra verticale hello diamo un'occhiata risultati hello nella visualizzazione grafico hello:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-204">Let's look at hello results in hello chart view with hello vertical bar option:</span></span>

![Fare clic su Grafico, quindi scegliere Grafico a barre verticali e assegnare gli assi x e y](./media/app-insights-analytics-tour/230.png)

<span data-ttu-id="a8a0f-206">Si noti che anche se è non Ordina risultati hello base all'ora (come si può vedere nella visualizzazione tabella hello), visualizzazione del grafico hello valori DateTime vengono sempre visualizzati nell'ordine corretto.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-206">Notice that although we didn't sort hello results by time (as you can see in hello table display), hello chart display always shows datetimes in correct order.</span></span>


## <a name="timecharts"></a><span data-ttu-id="a8a0f-207">Grafici di tempo</span><span class="sxs-lookup"><span data-stu-id="a8a0f-207">Timecharts</span></span>
<span data-ttu-id="a8a0f-208">Visualizzare il numero di eventi presenti in ogni ora:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-208">Show how many events there are each hour:</span></span>

```AIQL

    requests
      | summarize event_count=sum(itemCount)
        by bin(timestamp, 1h)
```

<span data-ttu-id="a8a0f-209">Selezionare l'opzione di visualizzazione grafico hello:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-209">Select hello Chart display option:</span></span>

![timechart](./media/app-insights-analytics-tour/080.png)

## <a name="multiple-series"></a><span data-ttu-id="a8a0f-211">Serie multiple</span><span class="sxs-lookup"><span data-stu-id="a8a0f-211">Multiple series</span></span>
<span data-ttu-id="a8a0f-212">Più espressioni di hello `summarize` clausola crea più colonne.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-212">Multiple expressions in hello `summarize` clause creates multiple columns.</span></span>

<span data-ttu-id="a8a0f-213">Più espressioni di hello `by` clausola crea più righe, uno per ogni combinazione di valori.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-213">Multiple expressions in hello `by` clause creates multiple rows, one for each combination of values.</span></span>

```AIQL

    requests
    | summarize count_=sum(itemCount), avg(duration)
      by bin(timestamp, 1h), client_StateOrProvince, client_City
    | order by timestamp asc, client_StateOrProvince, client_City
```

![Tabella delle richieste in base a ora e località](./media/app-insights-analytics-tour/090.png)

### <a name="segment-a-chart-by-dimensions"></a><span data-ttu-id="a8a0f-215">Segmentare un grafico in base alle dimensioni</span><span class="sxs-lookup"><span data-stu-id="a8a0f-215">Segment a chart by dimensions</span></span>
<span data-ttu-id="a8a0f-216">Se si grafico una tabella con una colonna stringa e una colonna numerica, la stringa hello può essere utilizzato toosplit dati numerici di hello in serie separate di punti.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-216">If you chart a table that has a string column and a numeric column, hello string can be used toosplit hello numeric data into separate series of points.</span></span> <span data-ttu-id="a8a0f-217">Se è presente più di una colonna stringa, è possibile scegliere quali toouse colonna come discriminatore hello.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-217">If there's more than one string column, you can choose which column toouse as hello discriminator.</span></span>

![Segmentare un grafico di analisi](./media/app-insights-analytics-tour/100.png)

#### <a name="bounce-rate"></a><span data-ttu-id="a8a0f-219">Frequenza di mancati recapiti</span><span class="sxs-lookup"><span data-stu-id="a8a0f-219">Bounce rate</span></span>

<span data-ttu-id="a8a0f-220">Convertire un toouse stringa booleana tooa come un discriminatore:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-220">Convert a boolean tooa string toouse it as a discriminator:</span></span>

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

### <a name="display-multiple-metrics"></a><span data-ttu-id="a8a0f-221">Visualizzare più metriche</span><span class="sxs-lookup"><span data-stu-id="a8a0f-221">Display multiple metrics</span></span>
<span data-ttu-id="a8a0f-222">Se un grafico di una tabella con più di una colonna numerica, in aggiunta toohello timestamp, è possibile visualizzare qualsiasi combinazione di essi.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-222">If you chart a table that has more than one numeric column, in addition toohello timestamp, you can display any combination of them.</span></span>

![Segmentare un grafico di analisi](./media/app-insights-analytics-tour/110.png)

<span data-ttu-id="a8a0f-224">È necessario selezionare **Don't Split** (Non dividere) prima di poter selezionare più colonne numeriche.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-224">You must select **Don't Split** before you can select multiple numeric columns.</span></span> <span data-ttu-id="a8a0f-225">Non è possibile dividere da una colonna stringa hello stesso tempo alla visualizzazione di più di una colonna numerica.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-225">You can't split by a string column at hello same time as displaying more than one numeric column.</span></span>

## <a name="daily-average-cycle"></a><span data-ttu-id="a8a0f-226">Ciclo della media giornaliera</span><span class="sxs-lookup"><span data-stu-id="a8a0f-226">Daily average cycle</span></span>
<span data-ttu-id="a8a0f-227">Come l'utilizzo variare su giornata Media hello?</span><span class="sxs-lookup"><span data-stu-id="a8a0f-227">How does usage vary over hello average day?</span></span>

<span data-ttu-id="a8a0f-228">Richieste di conteggio per il tempo di hello modulo un giorno, suddivisi in ore:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-228">Count requests by hello time modulo one day, binned into hours:</span></span>

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
> <span data-ttu-id="a8a0f-230">Notare che è attualmente tooconvert ora durate toodatetimes in ordine toodisplay in un grafico a linee.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-230">Notice that we currently have tooconvert time durations toodatetimes in order toodisplay on a line chart.</span></span>
>
>

## <a name="compare-multiple-daily-series"></a><span data-ttu-id="a8a0f-231">Confrontare più serie giornaliere</span><span class="sxs-lookup"><span data-stu-id="a8a0f-231">Compare multiple daily series</span></span>
<span data-ttu-id="a8a0f-232">La modalità utilizzo variare nel tempo hello del giorno in paesi diversi?</span><span class="sxs-lookup"><span data-stu-id="a8a0f-232">How does usage vary over hello time of day in different countries?</span></span>

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

## <a name="plot-a-distribution"></a><span data-ttu-id="a8a0f-234">Tracciare una distribuzione</span><span class="sxs-lookup"><span data-stu-id="a8a0f-234">Plot a distribution</span></span>
<span data-ttu-id="a8a0f-235">Quante sessioni esistono di lunghezze diverse?</span><span class="sxs-lookup"><span data-stu-id="a8a0f-235">How many sessions are there of different lengths?</span></span>

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

<span data-ttu-id="a8a0f-236">ultima riga Hello è toodatetime tooconvert obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-236">hello last line is required tooconvert toodatetime.</span></span> <span data-ttu-id="a8a0f-237">Attualmente asse hello x di un grafico viene visualizzato come un valore scalare solo se è un valore datetime.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-237">Currently hello x axis of a chart is displayed as a scalar only if it is a datetime.</span></span>

<span data-ttu-id="a8a0f-238">Hello `where` clausola esclude le sessioni monofase (sessionDuration = = 0) e set hello lunghezza dell'asse x hello.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-238">hello `where` clause excludes one-shot sessions (sessionDuration==0) and sets hello length of hello x-axis.</span></span>

![](./media/app-insights-analytics-tour/290.png)

## <a name="percentileshttpsdocsloganalyticsioquerylanguagequerylanguagepercentilesaggfunctionhtml"></a>[<span data-ttu-id="a8a0f-239">Percentili</span><span class="sxs-lookup"><span data-stu-id="a8a0f-239">Percentiles</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_percentiles_aggfunction.html)
<span data-ttu-id="a8a0f-240">Quali intervalli di durate coprono le diverse percentuali delle sessioni?</span><span class="sxs-lookup"><span data-stu-id="a8a0f-240">What ranges of durations cover different percentages of sessions?</span></span>

<span data-ttu-id="a8a0f-241">Usare hello di sopra di query, ma sostituire l'ultima riga hello:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-241">Use hello above query, but replace hello last line:</span></span>

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

<span data-ttu-id="a8a0f-242">È inoltre rimosso il limite di hello hello in clausola, nell'ordine tooget correggere figure incluse tutte le sessioni con più di una richiesta:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-242">We also removed hello upper limit in hello where clause, in order tooget correct figures including all sessions with more than one request:</span></span>

![risultato](./media/app-insights-analytics-tour/180.png)

<span data-ttu-id="a8a0f-244">È possibile osservare che:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-244">From which we can see that:</span></span>

* <span data-ttu-id="a8a0f-245">Il 5% delle sessioni ha una durata inferiore a 3 minuti e 34 secondi;</span><span class="sxs-lookup"><span data-stu-id="a8a0f-245">5% of sessions have a duration of less than 3 minutes 34s;</span></span>
* <span data-ttu-id="a8a0f-246">Il 50% delle sessioni dura meno di 36 minuti;</span><span class="sxs-lookup"><span data-stu-id="a8a0f-246">50% of sessions last less than 36 minutes;</span></span>
* <span data-ttu-id="a8a0f-247">Il 5% delle sessioni dura più di 7 giorni</span><span class="sxs-lookup"><span data-stu-id="a8a0f-247">5% of sessions last more than 7 days</span></span>

<span data-ttu-id="a8a0f-248">tooget una suddivisione separata per ogni paese, semplicemente abbiamo colonna client_CountryOrRegion di hello toobring separatamente tramite entrambi riepilogare operatori:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-248">tooget a separate breakdown for each country, we just have toobring hello client_CountryOrRegion column separately through both summarize operators:</span></span>

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

## <a name="join"></a><span data-ttu-id="a8a0f-249">Join</span><span class="sxs-lookup"><span data-stu-id="a8a0f-249">Join</span></span>
<span data-ttu-id="a8a0f-250">Avere accesso tooseveral tabelle, incluse le richieste e le eccezioni.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-250">We have access tooseveral tables, including requests and exceptions.</span></span>

<span data-ttu-id="a8a0f-251">toofind hello eccezioni correlate tooa richiesta che ha restituito una risposta di errore, è possibile creare un join tabelle hello in `session_Id`:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-251">toofind hello exceptions related tooa request that returned a failure response, we can join hello tables on `session_Id`:</span></span>

```AIQL

    requests
    | where toint(resultCode) >= 500
    | join (exceptions) on operation_Id
    | take 30
```


<span data-ttu-id="a8a0f-252">È buona norma toouse `project` colonne hello solo tooselect è necessario prima di eseguire hello join.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-252">It's good practice toouse `project` tooselect just hello columns we need before performing hello join.</span></span>
<span data-ttu-id="a8a0f-253">In hello stesse clausole, viene rinominata una colonna timestamp hello.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-253">In hello same clauses, we rename hello timestamp column.</span></span>

## <a name="lethttpsdocsloganalyticsioquerylanguagequerylanguageletstatementhtml-assign-a-result-tooa-variable"></a><span data-ttu-id="a8a0f-254">[Consentire](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): assegnare una variabile di risultato tooa</span><span class="sxs-lookup"><span data-stu-id="a8a0f-254">[Let](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): Assign a result tooa variable</span></span>

<span data-ttu-id="a8a0f-255">Utilizzare `let` tooseparate parti hello dell'espressione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-255">Use `let` tooseparate out hello parts of hello previous expression.</span></span> <span data-ttu-id="a8a0f-256">risultati Hello sono identiche:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-256">hello results are unchanged:</span></span>

```AIQL

    let bad_requests =
      requests
        | where  toint(resultCode) >= 500  ;
    bad_requests
    | join (exceptions) on session_Id
    | take 30
```

> [!Tip] 
> <span data-ttu-id="a8a0f-257">Nel client Analitica hello, non inserire le righe vuote tra le parti della query hello hello.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-257">In hello Analytics client, don't put blank lines between hello parts of hello query.</span></span> <span data-ttu-id="a8a0f-258">Verificare che tooexecute tutti di esso.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-258">Make sure tooexecute all of it.</span></span>
>

<span data-ttu-id="a8a0f-259">Utilizzare `toscalar` tooconvert valore tooa di una cella di tabella:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-259">Use `toscalar` tooconvert a single table cell tooa value:</span></span>

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


### <a name="functions"></a><span data-ttu-id="a8a0f-260">Funzioni</span><span class="sxs-lookup"><span data-stu-id="a8a0f-260">Functions</span></span>

<span data-ttu-id="a8a0f-261">Utilizzare *Let* toodefine una funzione:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-261">Use *Let* toodefine a function:</span></span>

```AIQL

    let usdate = (t:datetime)
    {
      strcat(getmonth(t), "/", dayofmonth(t),"/", getyear(t), " ",
      bin((t-1h)%12h+1h,1s), iff(t%24h<12h, "AM", "PM"))
    };
    requests  
    | extend PST = usdate(timestamp-8h)
```

## <a name="accessing-nested-objects"></a><span data-ttu-id="a8a0f-262">Accesso a oggetti annidati</span><span class="sxs-lookup"><span data-stu-id="a8a0f-262">Accessing nested objects</span></span>
<span data-ttu-id="a8a0f-263">È facile accedere agli oggetti annidati.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-263">Nested objects can be accessed easily.</span></span> <span data-ttu-id="a8a0f-264">Nel flusso di eccezioni hello, ad esempio, è possibile visualizzare oggetti strutturati come segue:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-264">For example, in hello exceptions stream you can see structured objects like this:</span></span>

![risultato](./media/app-insights-analytics-tour/520.png)

<span data-ttu-id="a8a0f-266">È possibile convertirla scegliendo Proprietà hello che si è interessati:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-266">You can flatten it by choosing hello properties you're interested in:</span></span>

```AIQL

    exceptions | take 10
    | extend method1 = tostring(details[0].parsedStack[1].method)
```

<span data-ttu-id="a8a0f-267">Si noti che è necessario tipo appropriato toohello toocast hello risultato.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-267">Note that you need toocast hello result toohello appropriate type.</span></span>


## <a name="custom-properties-and-measurements"></a><span data-ttu-id="a8a0f-268">Proprietà e misure personalizzate</span><span class="sxs-lookup"><span data-stu-id="a8a0f-268">Custom properties and measurements</span></span>
<span data-ttu-id="a8a0f-269">Se l'applicazione associa [(proprietà) di dimensioni personalizzate e le misure personalizzate](app-insights-api-custom-events-metrics.md#properties) tooevents, quindi verranno visualizzate in hello `customDimensions` e `customMeasurements` oggetti.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-269">If your application attaches [custom dimensions (properties) and custom measurements](app-insights-api-custom-events-metrics.md#properties) tooevents, then you will see them in hello `customDimensions` and `customMeasurements` objects.</span></span>

<span data-ttu-id="a8a0f-270">Ad esempio, se l'applicazione include:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-270">For example, if your app includes:</span></span>

```C#

    var dimensions = new Dictionary<string, string>
                     {{"p1", "v1"},{"p2", "v2"}};
    var measurements = new Dictionary<string, double>
                     {{"m1", 42.0}, {"m2", 43.2}};
    telemetryClient.TrackEvent("myEvent", dimensions, measurements);
```

<span data-ttu-id="a8a0f-271">tooextract questi valori in Analitica:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-271">tooextract these values in Analytics:</span></span>

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      m1 = todouble(customMeasurements.m1) // cast tooexpected type

```

<span data-ttu-id="a8a0f-272">tooverify se una dimensione personalizzata è un tipo specifico:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-272">tooverify whether a custom dimension is of a particular type:</span></span>

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      iff(notnull(todouble(customMeasurements.m1)), ...
```

## <a name="dashboards"></a><span data-ttu-id="a8a0f-273">Dashboard</span><span class="sxs-lookup"><span data-stu-id="a8a0f-273">Dashboards</span></span>
<span data-ttu-id="a8a0f-274">È possibile aggiungere il dashboard di tooa risultati in ordine toobring insieme tutti i grafici e tabelle più importanti.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-274">You can pin your results tooa dashboard in order toobring together all your most important charts and tables.</span></span>

* <span data-ttu-id="a8a0f-275">[Dashboard condiviso Azure](app-insights-dashboards.md#share-dashboards): fare clic sull'icona di hello pin.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-275">[Azure shared dashboard](app-insights-dashboards.md#share-dashboards): Click hello pin icon.</span></span> <span data-ttu-id="a8a0f-276">Per poterlo fare, è necessario disporre di un dashboard condiviso.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-276">Before you do this, you must have a shared dashboard.</span></span> <span data-ttu-id="a8a0f-277">Nel portale di Azure hello, aprire o creare un dashboard e fare clic su Condividi.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-277">In hello Azure portal, open or create a dashboard and click Share.</span></span>
* <span data-ttu-id="a8a0f-278">[Dashboard di Power BI](app-insights-export-power-bi.md): fare clic su Esporta, Power BI Query (Query Power BI).</span><span class="sxs-lookup"><span data-stu-id="a8a0f-278">[Power BI dashboard](app-insights-export-power-bi.md): Click Export, Power BI Query.</span></span> <span data-ttu-id="a8a0f-279">Un vantaggio di questa alternativa consiste nel fatto che è possibile visualizzare la query insieme ad altri risultati da un'ampia gamma di origini.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-279">An advantage of this alternative is that you can display your query alongside other results from a wide range of sources.</span></span>

## <a name="combine-with-imported-data"></a><span data-ttu-id="a8a0f-280">Combinare con dati importati</span><span class="sxs-lookup"><span data-stu-id="a8a0f-280">Combine with imported data</span></span>

<span data-ttu-id="a8a0f-281">Aspetto Analitica report nel dashboard di hello, ma talvolta si desidera tootranslate hello dati tooa più form semplice.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-281">Analytics reports look great on hello dashboard, but sometimes you want tootranslate hello data tooa more digestible form.</span></span> <span data-ttu-id="a8a0f-282">Si supponga, ad esempio, che gli utenti autenticati sono identificati nei dati di telemetria hello da un alias.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-282">For example, suppose your authenticated users are identified in hello telemetry by an alias.</span></span> <span data-ttu-id="a8a0f-283">Si vuole tooshow reale nomi nei risultati.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-283">You'd like tooshow their real names in your results.</span></span> <span data-ttu-id="a8a0f-284">toodo, è necessario un file CSV che esegue il mapping dai nomi di hello alias toohello reale.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-284">toodo this, you need a CSV file that maps from hello aliases toohello real names.</span></span>

<span data-ttu-id="a8a0f-285">È possibile importare un file di dati e utilizzarlo come qualsiasi tabella hello standard (richieste, eccezioni e così via).</span><span class="sxs-lookup"><span data-stu-id="a8a0f-285">You can import a data file and use it just like any of hello standard tables (requests, exceptions, and so on).</span></span> <span data-ttu-id="a8a0f-286">Eseguire una query sulla propria tabella oppure aggiungerla ad altre tabelle.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-286">Either query it on its own, or join it with other tables.</span></span> <span data-ttu-id="a8a0f-287">Ad esempio, se si dispone di una tabella denominata usermap, e sono presenti colonne `realName` e `userId`, è possibile utilizzare hello tootranslate `user_AuthenticatedId` campo nei dati di telemetria di hello richiesta:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-287">For example, if you have a table named usermap, and it has columns `realName` and `userId`, then you can use it tootranslate hello `user_AuthenticatedId` field in hello request telemetry:</span></span>

```AIQL

    requests
    | where notempty(user_AuthenticatedId)
    | project userId = user_AuthenticatedId
      // get hello realName field from hello usermap table:
    | join kind=leftouter ( usermap ) on userId
      // count transactions by name:
    | summarize count() by realName
```

<span data-ttu-id="a8a0f-288">una tabella, nel Pannello di Schema hello, tooimport in **altre origini dati**, seguire le istruzioni di hello tooadd una nuova origine dati, caricando un campione di dati.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-288">tooimport a table, in hello Schema blade, under **Other Data Sources**, follow hello instructions tooadd a new data source, by uploading a sample of your data.</span></span> <span data-ttu-id="a8a0f-289">È quindi possibile utilizzare le tabelle tooupload questa definizione.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-289">Then you can use this definition tooupload tables.</span></span>

<span data-ttu-id="a8a0f-290">funzionalità di importazione Hello è attualmente in anteprima, in modo inizialmente verrà visualizzato un collegamento "Contattaci" in "Altre origini dati."</span><span class="sxs-lookup"><span data-stu-id="a8a0f-290">hello import feature is currently in preview, so you will initially see a "Contact us" link under "Other data sources."</span></span> <span data-ttu-id="a8a0f-291">Utilizzare questo toosign un programma di anteprima toohello collegamento hello verrà sostituito da un pulsante "Aggiungi nuova origine dati".</span><span class="sxs-lookup"><span data-stu-id="a8a0f-291">Use this toosign up toohello preview program, and hello link will then be replaced by an "Add new data source" button.</span></span>


## <a name="tables"></a><span data-ttu-id="a8a0f-292">Tabelle</span><span class="sxs-lookup"><span data-stu-id="a8a0f-292">Tables</span></span>
<span data-ttu-id="a8a0f-293">flusso di dati di telemetria ricevuti dall'app di Hello è accessibile tramite diverse tabelle.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-293">hello stream of telemetry received from your app is accessible through several tables.</span></span> <span data-ttu-id="a8a0f-294">schema di Hello delle proprietà disponibili per ogni tabella è visibile in a sinistra della finestra hello hello.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-294">hello schema of properties available for each table is visible at hello left of hello window.</span></span>

### <a name="requests-table"></a><span data-ttu-id="a8a0f-295">Tabella di richieste</span><span class="sxs-lookup"><span data-stu-id="a8a0f-295">Requests table</span></span>
<span data-ttu-id="a8a0f-296">Conteggio HTTP richieste tooyour web app e segmento in base al nome di pagina:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-296">Count HTTP requests tooyour web app and segment by page name:</span></span>

![Richieste di conteggio segmentate per nome](./media/app-insights-analytics-tour/analytics-count-requests.png)

<span data-ttu-id="a8a0f-298">Trova le richieste di hello che non soddisfano la maggior parte:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-298">Find hello requests that fail most:</span></span>

![Richieste di conteggio segmentate per nome](./media/app-insights-analytics-tour/analytics-failed-requests.png)

### <a name="custom-events-table"></a><span data-ttu-id="a8a0f-300">Tabella di eventi personalizzati</span><span class="sxs-lookup"><span data-stu-id="a8a0f-300">Custom events table</span></span>
<span data-ttu-id="a8a0f-301">Se si utilizza [Trackevent](app-insights-api-custom-events-metrics.md#trackevent) toosend gli eventi personalizzati, è possibile leggerli da questa tabella.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-301">If you use [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) toosend your own events, you can read them from this table.</span></span>

<span data-ttu-id="a8a0f-302">Esaminiamo un esempio in cui il codice dell'app contiene le righe seguenti:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-302">Let's take an example where your app code contains these lines:</span></span>

```C#

    telemetry.TrackEvent("Query",
       new Dictionary<string,string> {{"query", sqlCmd}},
       new Dictionary<string,double> {
           {"retry", retryCount},
           {"querytime", totalTime}})
```

<span data-ttu-id="a8a0f-303">Frequenza di hello visualizzazione di questi eventi:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-303">Display hello frequency of these events:</span></span>

![Frequenza di visualizzazione degli eventi personalizzati](./media/app-insights-analytics-tour/analytics-custom-events-rate.png)

<span data-ttu-id="a8a0f-305">Estrarre le misure e dimensioni da eventi hello:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-305">Extract measurements and dimensions from hello events:</span></span>

![Frequenza di visualizzazione degli eventi personalizzati](./media/app-insights-analytics-tour/analytics-custom-events-dimensions.png)

### <a name="custom-metrics-table"></a><span data-ttu-id="a8a0f-307">Tabella delle metriche personalizzate</span><span class="sxs-lookup"><span data-stu-id="a8a0f-307">Custom metrics table</span></span>
<span data-ttu-id="a8a0f-308">Se si utilizza [trackmetric ()](app-insights-api-custom-events-metrics.md#trackmetric) toosend metrica valori personalizzati, sono disponibili i risultati in hello **customMetrics** flusso.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-308">If you are using [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) toosend your own metric values, you’ll find its results in hello **customMetrics** stream.</span></span> <span data-ttu-id="a8a0f-309">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-309">For example:</span></span>  

![Metriche personalizzate in Application Insights - Analisi](./media/app-insights-analytics-tour/analytics-custom-metrics.png)

> [!NOTE]
> <span data-ttu-id="a8a0f-311">In [Esplora metriche](app-insights-metrics-explorer.md), tutte le misure personalizzate tooany collegato di tipo di dati di telemetria vengono incluse nel pannello metriche hello insieme metriche inviate utilizzando `TrackMetric()`.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-311">In [Metrics Explorer](app-insights-metrics-explorer.md), all custom measurements attached tooany type of telemetry appear together in hello metrics blade along with metrics sent using `TrackMetric()`.</span></span> <span data-ttu-id="a8a0f-312">Ma in Analitica, misure personalizzate sono ancora collegato toowhichever tipo di dati di telemetria sono stati riportati nella - eventi o le richieste e così via, mentre nel proprio flusso inviate dal TrackMetric metriche.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-312">But in Analytics, custom measurements are still attached toowhichever type of telemetry they were carried on - events or requests, and so on - while metrics sent by TrackMetric appear in their own stream.</span></span>
>
>

### <a name="performance-counters-table"></a><span data-ttu-id="a8a0f-313">Tabella dei contatori delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="a8a0f-313">Performance counters table</span></span>
<span data-ttu-id="a8a0f-314">[I contatori delle prestazioni](app-insights-performance-counters.md) mostrano le metriche base del sistema per l'applicazione, ad esempio CPU, memoria e uso della rete.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-314">[Performance counters](app-insights-performance-counters.md) show you basic system metrics for your app, such as CPU, memory, and network utilization.</span></span> <span data-ttu-id="a8a0f-315">È possibile configurare hello SDK toosend contatori aggiuntivi, inclusi i contatori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-315">You can configure hello SDK toosend additional counters, including your own custom counters.</span></span>

<span data-ttu-id="a8a0f-316">Hello **performanceCounters** schema espone hello `category`, `counter` nome, e `instance` nome di ogni contatore delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-316">hello **performanceCounters** schema exposes hello `category`, `counter` name, and `instance` name of each performance counter.</span></span> <span data-ttu-id="a8a0f-317">I nomi delle istanze di contatore sono applicabili toosome solo i contatori delle prestazioni e indicano in genere si riferisce il nome di hello di hello processo toowhich hello count.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-317">Counter instance names are only applicable toosome performance counters, and typically indicate hello name of hello process toowhich hello count relates.</span></span> <span data-ttu-id="a8a0f-318">Nei dati di telemetria hello per ogni applicazione, verrà visualizzato solo i contatori di hello per tale applicazione.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-318">In hello telemetry for each application, you’ll see only hello counters for that application.</span></span> <span data-ttu-id="a8a0f-319">Ad esempio, toosee i contatori sono disponibili:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-319">For example, toosee what counters are available:</span></span>

![Contatori delle prestazioni in Application Insights - Analisi](./media/app-insights-analytics-tour/analytics-performance-counters.png)

<span data-ttu-id="a8a0f-321">un grafico di memoria disponibile su hello tooget periodo selezionato:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-321">tooget a chart of available memory over hello selected period:</span></span>

![Timechart delle metriche in Application Insights - Analisi](./media/app-insights-analytics-tour/analytics-available-memory.png)

<span data-ttu-id="a8a0f-323">Come altri dati di telemetria, **performanceCounters** contiene anche una colonna `cloud_RoleInstance` che indica l'identità di hello del computer host hello in cui l'app è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-323">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates hello identity of hello host machine on which your app is running.</span></span> <span data-ttu-id="a8a0f-324">Ad esempio, toocompare hello prestazioni dell'app in computer diversi hello:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-324">For example, toocompare hello performance of your app on hello different machines:</span></span>

![Prestazioni segmentate per istanze del ruolo in Application Insights - Analisi](./media/app-insights-analytics-tour/analytics-metrics-role-instance.png)

### <a name="exceptions-table"></a><span data-ttu-id="a8a0f-326">Tabelle delle eccezioni</span><span class="sxs-lookup"><span data-stu-id="a8a0f-326">Exceptions table</span></span>
<span data-ttu-id="a8a0f-327">[Le eccezioni segnalate dall'app](app-insights-asp-net-exceptions.md) sono disponibili in questa tabella.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-327">[Exceptions reported by your app](app-insights-asp-net-exceptions.md) are available in this table.</span></span>

<span data-ttu-id="a8a0f-328">toofind hello richiesta HTTP che stava gestendo l'app quando è stata generata l'eccezione di hello, creare un join in operation_Id:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-328">toofind hello HTTP request that your app was handling when hello exception was raised, join on operation_Id:</span></span>

![Creare un join delle eccezioni con le richieste in operation_Id](./media/app-insights-analytics-tour/analytics-exception-request.png)

### <a name="browser-timings-table"></a><span data-ttu-id="a8a0f-330">Tabella delle tempistiche del browser</span><span class="sxs-lookup"><span data-stu-id="a8a0f-330">Browser timings table</span></span>
<span data-ttu-id="a8a0f-331">`browserTimings` mostra i dati di caricamento della pagina raccolti nel browser degli utenti.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-331">`browserTimings` shows page load data collected in your users' browsers.</span></span>

<span data-ttu-id="a8a0f-332">[Configurare l'app per i dati di telemetria sul lato client](app-insights-javascript.md) in ordine toosee queste metriche.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-332">[Set up your app for client-side telemetry](app-insights-javascript.md) in order toosee these metrics.</span></span>

<span data-ttu-id="a8a0f-333">schema Hello include [metriche che indica di lunghezze hello delle diverse fasi del processo di caricamento della pagina hello](app-insights-javascript.md#page-load-performance).</span><span class="sxs-lookup"><span data-stu-id="a8a0f-333">hello schema includes [metrics indicating hello lengths of different stages of hello page loading process](app-insights-javascript.md#page-load-performance).</span></span> <span data-ttu-id="a8a0f-334">(Non indicano hello tempo che agli utenti di leggere una pagina).</span><span class="sxs-lookup"><span data-stu-id="a8a0f-334">(They don’t indicate hello length of time your users read a page.)</span></span>  

<span data-ttu-id="a8a0f-335">Mostra popularities hello di diverse pagine e caricare volte per ogni pagina:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-335">Show hello popularities of different pages, and load times for each page:</span></span>

![Tempistiche di caricamento delle pagine in Analisi](./media/app-insights-analytics-tour/analytics-page-load.png)

### <a name="availability-results-table"></a><span data-ttu-id="a8a0f-337">Tabella dei risultati di disponibilità</span><span class="sxs-lookup"><span data-stu-id="a8a0f-337">Availability results table</span></span>
<span data-ttu-id="a8a0f-338">`availabilityResults`Mostra hello risultati del [test web](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="a8a0f-338">`availabilityResults` shows hello results of your [web tests](app-insights-monitor-web-app-availability.md).</span></span> <span data-ttu-id="a8a0f-339">Ogni esecuzione di test da ogni posizione di test viene segnalata separatamente.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-339">Each run of your tests from each test location is reported separately.</span></span>

![Tempistiche di caricamento delle pagine in Analisi](./media/app-insights-analytics-tour/analytics-availability.png)

### <a name="dependencies-table"></a><span data-ttu-id="a8a0f-341">Tabella delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="a8a0f-341">Dependencies table</span></span>
<span data-ttu-id="a8a0f-342">Contiene i risultati delle chiamate che applicazione rende toodatabases e le API REST e altro chiama tooTrackDependency().</span><span class="sxs-lookup"><span data-stu-id="a8a0f-342">Contains results of calls that your app makes toodatabases and REST APIs, and other calls tooTrackDependency().</span></span> <span data-ttu-id="a8a0f-343">Include anche le chiamate AJAX eseguite da browser hello.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-343">Also includes AJAX calls made from hello browser.</span></span>

<span data-ttu-id="a8a0f-344">Chiamate AJAX dal browser hello:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-344">AJAX calls from hello browser:</span></span>

```AIQL

    dependencies | where client_Type == "Browser"
    | take 10
```

<span data-ttu-id="a8a0f-345">Chiamate a dipendenze dal server hello:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-345">Dependency calls from hello server:</span></span>

```AIQL

    dependencies | where client_Type == "PC"
    | take 10
```

<span data-ttu-id="a8a0f-346">Mostrano sempre risultati sul lato server dipendenza `success==False` se hello agente di Application Insights non è installato.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-346">Server-side dependency results always show `success==False` if hello Application Insights Agent is not installed.</span></span> <span data-ttu-id="a8a0f-347">Tuttavia, hello altri dati siano corretti.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-347">However, hello other data are correct.</span></span>

### <a name="traces-table"></a><span data-ttu-id="a8a0f-348">Tabella delle tracce</span><span class="sxs-lookup"><span data-stu-id="a8a0f-348">Traces table</span></span>
<span data-ttu-id="a8a0f-349">Contiene i dati di telemetria hello inviato da un'applicazione con tracktrace () presenti, o [altri framework di registrazione](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="a8a0f-349">Contains hello telemetry sent by your app using TrackTrace(), or [other logging frameworks](app-insights-asp-net-trace-logs.md).</span></span>

## <a name="video"></a><span data-ttu-id="a8a0f-350">Video</span><span class="sxs-lookup"><span data-stu-id="a8a0f-350">Video</span></span> 

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

<span data-ttu-id="a8a0f-351">Query avanzate:</span><span class="sxs-lookup"><span data-stu-id="a8a0f-351">Advanced queries:</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Build/2016/P591/player]


## <a name="next-steps"></a><span data-ttu-id="a8a0f-352">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a8a0f-352">Next steps</span></span>
* [<span data-ttu-id="a8a0f-353">Informazioni di riferimento sul linguaggio di Analisi</span><span class="sxs-lookup"><span data-stu-id="a8a0f-353">Analytics language reference</span></span>](app-insights-analytics-reference.md)
* <span data-ttu-id="a8a0f-354">[SQL utenti schede di riferimento rapido](https://aka.ms/sql-analytics) traduce idiomi comuni hello.</span><span class="sxs-lookup"><span data-stu-id="a8a0f-354">[SQL-users' cheat sheet](https://aka.ms/sql-analytics) translates hello most common idioms.</span></span>

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]
