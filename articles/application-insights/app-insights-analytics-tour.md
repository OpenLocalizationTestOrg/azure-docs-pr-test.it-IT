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
# <a name="a-tour-of-analytics-in-application-insights"></a>Presentazione dello strumento Analisi in Application Insights
[Analitica](app-insights-analytics.md) è hello ricerca potenti funzionalità di [Application Insights](app-insights-overview.md). Queste pagine descrivono il linguaggio di query di Log Analytics.

* **[Guardare video introduttivo hello](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.
* **[Test unità Analitica dei dati simulati](https://analytics.applicationinsights.io/demo)**  se l'applicazione non invia dati tooApplication Insights ancora.
* **[SQL utenti schede di riferimento rapido](https://aka.ms/sql-analytics)**  traduce idiomi comuni hello.

Di seguito è una procedura tooget alcune query di base che è stato avviato.

## <a name="connect-tooyour-application-insights-data"></a>Connettere i dati di Application Insights tooyour
Aprire Analisi dal [pannello Panoramica](app-insights-dashboards.md) dell'app in Application Insights:

![In portal.azure.com, aprire la risorsa di Application Insights e selezionare Analytics.](./media/app-insights-analytics-tour/001.png)

## <a name="takehttpsdocsloganalyticsioquerylanguagequerylanguagetakeoperatorhtml-show-me-n-rows"></a>[Take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): visualizzare n righe
I punti dati che registrano le operazioni degli utenti (in genere richieste HTTP ricevute dall'app Web) vengono archiviati in una tabella denominata `requests`. Ogni riga è un punto dati di telemetria ricevuto da hello Application Insights SDK nell'applicazione.

Per iniziare, esaminare alcune righe di esempio di tabella hello:

![results](./media/app-insights-analytics-tour/010.png)

> [!NOTE]
> Inserire un punto qualsiasi cursore hello nell'istruzione hello prima di fare clic. È possibile suddividere un'istruzione su più righe, ma non inserire righe vuote in un'istruzione. Le righe vuote sono un modo pratico di tookeep diversi separare le query nella finestra di hello.
>
>

Scegliere le colonne, trascinarle, creare gruppi in base alle colonne e applicare filtri:

![Fare clic sulla selezione di colonna in alto a destra dei risultati](./media/app-insights-analytics-tour/030.png)

Espandere i dettagli hello toosee qualsiasi articolo:

![Scegliere Tabella e usare Configura colonne](./media/app-insights-analytics-tour/040.png)

> [!NOTE]
> Fare clic sull'intestazione hello risultati una colonna toore ordine hello disponibile nel browser hello. Tuttavia, tenere presente che per un set di risultati di grandi dimensioni, hello numero di righe scaricate toohello browser è limitato. In questo modo di ordinamento non viene visualizzato sempre si hello effettiva più alta o più basso degli elementi. gli elementi di toosort usano in modo affidabile, hello `top` o `sort` operatore.
>
>

## <a name="tophttpsdocsloganalyticsioquerylanguagequerylanguagetopoperatorhtml-and-sorthttpsdocsloganalyticsioquerylanguagequerylanguagesortoperatorhtml"></a>[Top](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) e [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)
`take`è utile tooget un rapido esempio di un risultato, ma sono visualizzate le righe dalla tabella hello in nessun ordine particolare. utilizzare una visualizzazione ordinata, tooget `top` (per un esempio) o `sort` (su hello intera tabella).

Mostra hello prime n righe, ordinate in base a una colonna specifica:

```AIQL

    requests | top 10 by timestamp desc
```

* *Sintassi:* la maggior parte degli operatori ha parametri di tipo parola chiave, ad esempio `by`.
* `desc` = ordine decrescente, `asc` = ordine crescente.

![](./media/app-insights-analytics-tour/260.png)

`top...` è più efficiente di `sort ... | take...`. Si sarebbe potuto scrivere:

```AIQL

    requests | sort by timestamp desc | take 10
```

il risultato di Hello sarebbe hello stesso, ma verrà eseguito un po' più lentamente. Sarebbe stato anche possibile scrivere `order`, che è un alias di `sort`.

le intestazioni di colonna Hello nella visualizzazione tabella hello possono inoltre essere utilizzati toosort hello risultati sullo schermo hello. Ma ovviamente, se è stato usato `take` o `top` tooretrieve solo parte di una tabella, sarà possibile solo modificare l'ordine hello record è stato recuperato.

## <a name="wherehttpsdocsloganalyticsioquerylanguagequerylanguagewhereoperatorhtml-filtering-on-a-condition"></a>[Where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): filtrare in base a una condizione

Di seguito sono illustrate solo le richieste che hanno restituito un particolare codice di risultato:

```AIQL

    requests
    | where resultCode  == "404"
    | take 10
```

![](./media/app-insights-analytics-tour/250.png)

Hello `where` l'operatore accetta un'espressione booleana. Tenere presente i punti chiave seguenti:

* `and`, `or`: operatori booleani
* `==`, `<>`, `!=`: uguale a e non uguale a
* `=~`, `!~`: stringa senza distinzione tra maiuscole e minuscole uguale a e non uguale a. Sono disponibili numerosi altri operatori di confronto delle stringhe.

<!---Read all about [scalar expressions]().--->

### <a name="getting-hello-right-type"></a>Recupero di tipo corretto di hello
Individuare le richieste non riuscite:

```AIQL

    requests
    | where isnotempty(resultCode) and toint(resultCode) >= 400
```
<!---
`resultCode` has type string, so we must cast it app-insights-analytics-reference.md#casts for a numeric comparison.
--->

## <a name="time"></a>Tempo

Per impostazione predefinita, le query sono limitato toohello ultime 24 ore. Questo intervallo, però, può essere modificato:

![](./media/app-insights-analytics-tour/change-time-range.png)

Eseguire l'override di intervallo di tempo hello scrivendo una query che include la `timestamp` in una clausola where. ad esempio:

```AIQL

    // What were hello slowest requests over hello past 3 days?
    requests
    | where timestamp > ago(3d)  // Override hello time range
    | top 5 by duration
```

funzionalità di intervallo di tempo Hello è equivalente tooa 'where' clausola inserita dopo ogni indicazione di una delle tabelle di origine hello.

`ago(3d)` significa 'tre giorni fa'. Le altre unità di tempo includono ore (`2h`, `2.5h`), minuti (`25m`) e secondi (`10s`).

Altri esempi:

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

[Riferimento su date e ore](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).


## <a name="projecthttpsdocsloganalyticsioquerylanguagequerylanguageprojectoperatorhtml-select-rename-and-compute-columns"></a>[Project](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): selezionare, rinominare e calcolare le colonne
Utilizzare [ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) toopick out solo le colonne hello desiderate:

```AIQL

    requests | top 10 by timestamp desc
             | project timestamp, name, resultCode
```

![](./media/app-insights-analytics-tour/240.png)

È inoltre possibile rinominare le colonne e definire nuove colonne:

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

* I nomi di colonna possono includere spazi o simboli se sono racchiusi tra parentesi quadre, ad esempio: `['...']` o `["..."]`
* `%`è normale operatore modulo hello.
* `1d` (la cifra uno seguita da "d") è il valore letterale di un intervallo di tempo che indica un giorno. Ecco altri valori letterali di intervallo di tempo: `12h`, `30m`, `10s`, `0.01s`.
* `floor`(alias `bin`) Arrotonda un valore basso toohello multiplo del valore di base hello è fornire più vicino. Pertanto `floor(aTime, 1s)` Arrotonda volta verso il basso toohello più vicino al secondo.

Le espressioni possono includere tutti gli operatori di solito hello (`+`, `-`,...), ed è presente una gamma di funzioni utili.

## <a name="extend"></a>Extend
Se si desidera tooadd colonne toohello quelli esistenti, utilizzare [ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):

```AIQL

    requests
    | top 10 by timestamp desc
    | extend timeOfDay = floor(timestamp % 1d, 1s)
```

Utilizzando [ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) risulta meno dettagliata [ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) se si desidera tookeep tutti hello colonne esistenti.

### <a name="convert-toolocal-time"></a>Converte l'ora toolocal

I timestamp sono sempre espressi in formato UTC. Pertanto se è l'inverno costa ci Pacifico hello, si potrebbe essere come segue:

```AIQL

    requests
    | top 10 by timestamp desc
    | extend localTime = timestamp - 8h
```


## <a name="summarizehttpsdocsloganalyticsioquerylanguagequerylanguagesummarizeoperatorhtml-aggregate-groups-of-rows"></a>[Summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): aggregare gruppi di righe
`Summarize` applica una *funzione di aggregazione* specificata a gruppi di righe.

Ad esempio, in cui viene segnalato hello tempo app web toorespond tooa richiesta nel campo hello `duration`. Vediamo medio di risposta hello ora tooall richieste:

![](./media/app-insights-analytics-tour/410.png)

In alternativa, è possibile separare il risultato di hello in richieste di nomi diversi:

![](./media/app-insights-analytics-tour/420.png)

`Summarize`raccoglie hello punti dati nel flusso hello in gruppi per cui hello `by` clausola restituisce in modo uniforme. Ogni valore in hello `by` espressione - ogni nome di operazione in hello sopra riportato, restituisce una riga nella tabella risultati hello.

È anche possibile raggruppare i risultati per ora del giorno:

![](./media/app-insights-analytics-tour/430.png)

Si noti come utilizziamo hello `bin` funzione (noto anche come `floor`). Se si usasse solo `by timestamp`, ogni riga di input finirebbe in un piccolo gruppo distinto. Per qualsiasi scalari continua volte like o numeri, abbiamo toobreak intervallo continuo di hello in un numero gestibile di valori discreti. `bin`-che è appena hello familiarità di arrotondamento a discesa `floor` funzione - è toodo modo più semplice hello che.

È possibile utilizzare hello stessa tecnica tooreduce gli intervalli di stringhe:

![](./media/app-insights-analytics-tour/440.png)

Si noti che è possibile utilizzare `name=` nome hello tooset di una colonna di risultati, in espressioni di aggregazione hello o hello-clausola by.

## <a name="counting-sampled-data"></a>Conteggio dei dati campionati
`sum(itemCount)`è consigliato in hello aggregazione toocount eventi. In molti casi, itemCount = = 1, pertanto la funzione hello semplicemente conta il numero di hello di righe nel gruppo di hello. Ma quando [campionamento](app-insights-sampling.md) è nell'operazione, solo una frazione di eventi di hello originale vengono mantenute come punti dati di Application Insights, in modo che per ogni punto dati viene visualizzato, esistono `itemCount` eventi.

Ad esempio, se il campionamento Elimina 75% di eventi di hello originale, quindi itemCount = = 4 in record hello mantenuto -, ovvero per ogni record conservate, sono disponibili quattro record originale.

Campionamento adattivo causa itemCount toobe superiore durante i periodi di quando l'applicazione viene utilizzato.

Riepilogando itemCount fornisce pertanto una buona stima del numero originale di hello di eventi.

![](./media/app-insights-analytics-tour/510.png)

È inoltre disponibile un `count()` casi in cui si vuole numero hello toocount di righe in un gruppo di aggregazione (e un'operazione count).

Esiste un intervallo di [funzioni di aggregazione](https://docs.loganalytics.io/learn/tutorials/aggregations.html).

## <a name="charting-hello-results"></a>Creazione di grafici di risultati hello
```AIQL

    exceptions
       | summarize count=sum(itemCount)  
         by bin(timestamp, 1h)
```

Per impostazione predefinita, i risultati vengono visualizzati sotto forma di tabella:

![](./media/app-insights-analytics-tour/225.png)

Possiamo migliori rispetto alla visualizzazione tabella hello. Con l'opzione di barra verticale hello diamo un'occhiata risultati hello nella visualizzazione grafico hello:

![Fare clic su Grafico, quindi scegliere Grafico a barre verticali e assegnare gli assi x e y](./media/app-insights-analytics-tour/230.png)

Si noti che anche se è non Ordina risultati hello base all'ora (come si può vedere nella visualizzazione tabella hello), visualizzazione del grafico hello valori DateTime vengono sempre visualizzati nell'ordine corretto.


## <a name="timecharts"></a>Grafici di tempo
Visualizzare il numero di eventi presenti in ogni ora:

```AIQL

    requests
      | summarize event_count=sum(itemCount)
        by bin(timestamp, 1h)
```

Selezionare l'opzione di visualizzazione grafico hello:

![timechart](./media/app-insights-analytics-tour/080.png)

## <a name="multiple-series"></a>Serie multiple
Più espressioni di hello `summarize` clausola crea più colonne.

Più espressioni di hello `by` clausola crea più righe, uno per ogni combinazione di valori.

```AIQL

    requests
    | summarize count_=sum(itemCount), avg(duration)
      by bin(timestamp, 1h), client_StateOrProvince, client_City
    | order by timestamp asc, client_StateOrProvince, client_City
```

![Tabella delle richieste in base a ora e località](./media/app-insights-analytics-tour/090.png)

### <a name="segment-a-chart-by-dimensions"></a>Segmentare un grafico in base alle dimensioni
Se si grafico una tabella con una colonna stringa e una colonna numerica, la stringa hello può essere utilizzato toosplit dati numerici di hello in serie separate di punti. Se è presente più di una colonna stringa, è possibile scegliere quali toouse colonna come discriminatore hello.

![Segmentare un grafico di analisi](./media/app-insights-analytics-tour/100.png)

#### <a name="bounce-rate"></a>Frequenza di mancati recapiti

Convertire un toouse stringa booleana tooa come un discriminatore:

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

### <a name="display-multiple-metrics"></a>Visualizzare più metriche
Se un grafico di una tabella con più di una colonna numerica, in aggiunta toohello timestamp, è possibile visualizzare qualsiasi combinazione di essi.

![Segmentare un grafico di analisi](./media/app-insights-analytics-tour/110.png)

È necessario selezionare **Don't Split** (Non dividere) prima di poter selezionare più colonne numeriche. Non è possibile dividere da una colonna stringa hello stesso tempo alla visualizzazione di più di una colonna numerica.

## <a name="daily-average-cycle"></a>Ciclo della media giornaliera
Come l'utilizzo variare su giornata Media hello?

Richieste di conteggio per il tempo di hello modulo un giorno, suddivisi in ore:

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
> Notare che è attualmente tooconvert ora durate toodatetimes in ordine toodisplay in un grafico a linee.
>
>

## <a name="compare-multiple-daily-series"></a>Confrontare più serie giornaliere
La modalità utilizzo variare nel tempo hello del giorno in paesi diversi?

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

## <a name="plot-a-distribution"></a>Tracciare una distribuzione
Quante sessioni esistono di lunghezze diverse?

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

ultima riga Hello è toodatetime tooconvert obbligatorio. Attualmente asse hello x di un grafico viene visualizzato come un valore scalare solo se è un valore datetime.

Hello `where` clausola esclude le sessioni monofase (sessionDuration = = 0) e set hello lunghezza dell'asse x hello.

![](./media/app-insights-analytics-tour/290.png)

## <a name="percentileshttpsdocsloganalyticsioquerylanguagequerylanguagepercentilesaggfunctionhtml"></a>[Percentili](https://docs.loganalytics.io/queryLanguage/query_language_percentiles_aggfunction.html)
Quali intervalli di durate coprono le diverse percentuali delle sessioni?

Usare hello di sopra di query, ma sostituire l'ultima riga hello:

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

È inoltre rimosso il limite di hello hello in clausola, nell'ordine tooget correggere figure incluse tutte le sessioni con più di una richiesta:

![risultato](./media/app-insights-analytics-tour/180.png)

È possibile osservare che:

* Il 5% delle sessioni ha una durata inferiore a 3 minuti e 34 secondi;
* Il 50% delle sessioni dura meno di 36 minuti;
* Il 5% delle sessioni dura più di 7 giorni

tooget una suddivisione separata per ogni paese, semplicemente abbiamo colonna client_CountryOrRegion di hello toobring separatamente tramite entrambi riepilogare operatori:

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

## <a name="join"></a>Join
Avere accesso tooseveral tabelle, incluse le richieste e le eccezioni.

toofind hello eccezioni correlate tooa richiesta che ha restituito una risposta di errore, è possibile creare un join tabelle hello in `session_Id`:

```AIQL

    requests
    | where toint(resultCode) >= 500
    | join (exceptions) on operation_Id
    | take 30
```


È buona norma toouse `project` colonne hello solo tooselect è necessario prima di eseguire hello join.
In hello stesse clausole, viene rinominata una colonna timestamp hello.

## <a name="lethttpsdocsloganalyticsioquerylanguagequerylanguageletstatementhtml-assign-a-result-tooa-variable"></a>[Consentire](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): assegnare una variabile di risultato tooa

Utilizzare `let` tooseparate parti hello dell'espressione precedente hello. risultati Hello sono identiche:

```AIQL

    let bad_requests =
      requests
        | where  toint(resultCode) >= 500  ;
    bad_requests
    | join (exceptions) on session_Id
    | take 30
```

> [!Tip] 
> Nel client Analitica hello, non inserire le righe vuote tra le parti della query hello hello. Verificare che tooexecute tutti di esso.
>

Utilizzare `toscalar` tooconvert valore tooa di una cella di tabella:

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


### <a name="functions"></a>Funzioni

Utilizzare *Let* toodefine una funzione:

```AIQL

    let usdate = (t:datetime)
    {
      strcat(getmonth(t), "/", dayofmonth(t),"/", getyear(t), " ",
      bin((t-1h)%12h+1h,1s), iff(t%24h<12h, "AM", "PM"))
    };
    requests  
    | extend PST = usdate(timestamp-8h)
```

## <a name="accessing-nested-objects"></a>Accesso a oggetti annidati
È facile accedere agli oggetti annidati. Nel flusso di eccezioni hello, ad esempio, è possibile visualizzare oggetti strutturati come segue:

![risultato](./media/app-insights-analytics-tour/520.png)

È possibile convertirla scegliendo Proprietà hello che si è interessati:

```AIQL

    exceptions | take 10
    | extend method1 = tostring(details[0].parsedStack[1].method)
```

Si noti che è necessario tipo appropriato toohello toocast hello risultato.


## <a name="custom-properties-and-measurements"></a>Proprietà e misure personalizzate
Se l'applicazione associa [(proprietà) di dimensioni personalizzate e le misure personalizzate](app-insights-api-custom-events-metrics.md#properties) tooevents, quindi verranno visualizzate in hello `customDimensions` e `customMeasurements` oggetti.

Ad esempio, se l'applicazione include:

```C#

    var dimensions = new Dictionary<string, string>
                     {{"p1", "v1"},{"p2", "v2"}};
    var measurements = new Dictionary<string, double>
                     {{"m1", 42.0}, {"m2", 43.2}};
    telemetryClient.TrackEvent("myEvent", dimensions, measurements);
```

tooextract questi valori in Analitica:

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      m1 = todouble(customMeasurements.m1) // cast tooexpected type

```

tooverify se una dimensione personalizzata è un tipo specifico:

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      iff(notnull(todouble(customMeasurements.m1)), ...
```

## <a name="dashboards"></a>Dashboard
È possibile aggiungere il dashboard di tooa risultati in ordine toobring insieme tutti i grafici e tabelle più importanti.

* [Dashboard condiviso Azure](app-insights-dashboards.md#share-dashboards): fare clic sull'icona di hello pin. Per poterlo fare, è necessario disporre di un dashboard condiviso. Nel portale di Azure hello, aprire o creare un dashboard e fare clic su Condividi.
* [Dashboard di Power BI](app-insights-export-power-bi.md): fare clic su Esporta, Power BI Query (Query Power BI). Un vantaggio di questa alternativa consiste nel fatto che è possibile visualizzare la query insieme ad altri risultati da un'ampia gamma di origini.

## <a name="combine-with-imported-data"></a>Combinare con dati importati

Aspetto Analitica report nel dashboard di hello, ma talvolta si desidera tootranslate hello dati tooa più form semplice. Si supponga, ad esempio, che gli utenti autenticati sono identificati nei dati di telemetria hello da un alias. Si vuole tooshow reale nomi nei risultati. toodo, è necessario un file CSV che esegue il mapping dai nomi di hello alias toohello reale.

È possibile importare un file di dati e utilizzarlo come qualsiasi tabella hello standard (richieste, eccezioni e così via). Eseguire una query sulla propria tabella oppure aggiungerla ad altre tabelle. Ad esempio, se si dispone di una tabella denominata usermap, e sono presenti colonne `realName` e `userId`, è possibile utilizzare hello tootranslate `user_AuthenticatedId` campo nei dati di telemetria di hello richiesta:

```AIQL

    requests
    | where notempty(user_AuthenticatedId)
    | project userId = user_AuthenticatedId
      // get hello realName field from hello usermap table:
    | join kind=leftouter ( usermap ) on userId
      // count transactions by name:
    | summarize count() by realName
```

una tabella, nel Pannello di Schema hello, tooimport in **altre origini dati**, seguire le istruzioni di hello tooadd una nuova origine dati, caricando un campione di dati. È quindi possibile utilizzare le tabelle tooupload questa definizione.

funzionalità di importazione Hello è attualmente in anteprima, in modo inizialmente verrà visualizzato un collegamento "Contattaci" in "Altre origini dati." Utilizzare questo toosign un programma di anteprima toohello collegamento hello verrà sostituito da un pulsante "Aggiungi nuova origine dati".


## <a name="tables"></a>Tabelle
flusso di dati di telemetria ricevuti dall'app di Hello è accessibile tramite diverse tabelle. schema di Hello delle proprietà disponibili per ogni tabella è visibile in a sinistra della finestra hello hello.

### <a name="requests-table"></a>Tabella di richieste
Conteggio HTTP richieste tooyour web app e segmento in base al nome di pagina:

![Richieste di conteggio segmentate per nome](./media/app-insights-analytics-tour/analytics-count-requests.png)

Trova le richieste di hello che non soddisfano la maggior parte:

![Richieste di conteggio segmentate per nome](./media/app-insights-analytics-tour/analytics-failed-requests.png)

### <a name="custom-events-table"></a>Tabella di eventi personalizzati
Se si utilizza [Trackevent](app-insights-api-custom-events-metrics.md#trackevent) toosend gli eventi personalizzati, è possibile leggerli da questa tabella.

Esaminiamo un esempio in cui il codice dell'app contiene le righe seguenti:

```C#

    telemetry.TrackEvent("Query",
       new Dictionary<string,string> {{"query", sqlCmd}},
       new Dictionary<string,double> {
           {"retry", retryCount},
           {"querytime", totalTime}})
```

Frequenza di hello visualizzazione di questi eventi:

![Frequenza di visualizzazione degli eventi personalizzati](./media/app-insights-analytics-tour/analytics-custom-events-rate.png)

Estrarre le misure e dimensioni da eventi hello:

![Frequenza di visualizzazione degli eventi personalizzati](./media/app-insights-analytics-tour/analytics-custom-events-dimensions.png)

### <a name="custom-metrics-table"></a>Tabella delle metriche personalizzate
Se si utilizza [trackmetric ()](app-insights-api-custom-events-metrics.md#trackmetric) toosend metrica valori personalizzati, sono disponibili i risultati in hello **customMetrics** flusso. ad esempio:  

![Metriche personalizzate in Application Insights - Analisi](./media/app-insights-analytics-tour/analytics-custom-metrics.png)

> [!NOTE]
> In [Esplora metriche](app-insights-metrics-explorer.md), tutte le misure personalizzate tooany collegato di tipo di dati di telemetria vengono incluse nel pannello metriche hello insieme metriche inviate utilizzando `TrackMetric()`. Ma in Analitica, misure personalizzate sono ancora collegato toowhichever tipo di dati di telemetria sono stati riportati nella - eventi o le richieste e così via, mentre nel proprio flusso inviate dal TrackMetric metriche.
>
>

### <a name="performance-counters-table"></a>Tabella dei contatori delle prestazioni
[I contatori delle prestazioni](app-insights-performance-counters.md) mostrano le metriche base del sistema per l'applicazione, ad esempio CPU, memoria e uso della rete. È possibile configurare hello SDK toosend contatori aggiuntivi, inclusi i contatori personalizzati.

Hello **performanceCounters** schema espone hello `category`, `counter` nome, e `instance` nome di ogni contatore delle prestazioni. I nomi delle istanze di contatore sono applicabili toosome solo i contatori delle prestazioni e indicano in genere si riferisce il nome di hello di hello processo toowhich hello count. Nei dati di telemetria hello per ogni applicazione, verrà visualizzato solo i contatori di hello per tale applicazione. Ad esempio, toosee i contatori sono disponibili:

![Contatori delle prestazioni in Application Insights - Analisi](./media/app-insights-analytics-tour/analytics-performance-counters.png)

un grafico di memoria disponibile su hello tooget periodo selezionato:

![Timechart delle metriche in Application Insights - Analisi](./media/app-insights-analytics-tour/analytics-available-memory.png)

Come altri dati di telemetria, **performanceCounters** contiene anche una colonna `cloud_RoleInstance` che indica l'identità di hello del computer host hello in cui l'app è in esecuzione. Ad esempio, toocompare hello prestazioni dell'app in computer diversi hello:

![Prestazioni segmentate per istanze del ruolo in Application Insights - Analisi](./media/app-insights-analytics-tour/analytics-metrics-role-instance.png)

### <a name="exceptions-table"></a>Tabelle delle eccezioni
[Le eccezioni segnalate dall'app](app-insights-asp-net-exceptions.md) sono disponibili in questa tabella.

toofind hello richiesta HTTP che stava gestendo l'app quando è stata generata l'eccezione di hello, creare un join in operation_Id:

![Creare un join delle eccezioni con le richieste in operation_Id](./media/app-insights-analytics-tour/analytics-exception-request.png)

### <a name="browser-timings-table"></a>Tabella delle tempistiche del browser
`browserTimings` mostra i dati di caricamento della pagina raccolti nel browser degli utenti.

[Configurare l'app per i dati di telemetria sul lato client](app-insights-javascript.md) in ordine toosee queste metriche.

schema Hello include [metriche che indica di lunghezze hello delle diverse fasi del processo di caricamento della pagina hello](app-insights-javascript.md#page-load-performance). (Non indicano hello tempo che agli utenti di leggere una pagina).  

Mostra popularities hello di diverse pagine e caricare volte per ogni pagina:

![Tempistiche di caricamento delle pagine in Analisi](./media/app-insights-analytics-tour/analytics-page-load.png)

### <a name="availability-results-table"></a>Tabella dei risultati di disponibilità
`availabilityResults`Mostra hello risultati del [test web](app-insights-monitor-web-app-availability.md). Ogni esecuzione di test da ogni posizione di test viene segnalata separatamente.

![Tempistiche di caricamento delle pagine in Analisi](./media/app-insights-analytics-tour/analytics-availability.png)

### <a name="dependencies-table"></a>Tabella delle dipendenze
Contiene i risultati delle chiamate che applicazione rende toodatabases e le API REST e altro chiama tooTrackDependency(). Include anche le chiamate AJAX eseguite da browser hello.

Chiamate AJAX dal browser hello:

```AIQL

    dependencies | where client_Type == "Browser"
    | take 10
```

Chiamate a dipendenze dal server hello:

```AIQL

    dependencies | where client_Type == "PC"
    | take 10
```

Mostrano sempre risultati sul lato server dipendenza `success==False` se hello agente di Application Insights non è installato. Tuttavia, hello altri dati siano corretti.

### <a name="traces-table"></a>Tabella delle tracce
Contiene i dati di telemetria hello inviato da un'applicazione con tracktrace () presenti, o [altri framework di registrazione](app-insights-asp-net-trace-logs.md).

## <a name="video"></a>Video 

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

Query avanzate:

> [!VIDEO https://channel9.msdn.com/Events/Build/2016/P591/player]


## <a name="next-steps"></a>Passaggi successivi
* [Informazioni di riferimento sul linguaggio di Analisi](app-insights-analytics-reference.md)
* [SQL utenti schede di riferimento rapido](https://aka.ms/sql-analytics) traduce idiomi comuni hello.

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]
