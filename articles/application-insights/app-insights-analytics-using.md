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
# <a name="using-analytics-in-application-insights"></a>Uso di Analytics in Application Insights
[Analitica](app-insights-analytics.md) è hello ricerca potenti funzionalità di [Application Insights](app-insights-overview.md). Queste pagine descrivono il linguaggio di query di Log Analytics.

* **[Guardare video introduttivo hello](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.
* **[Test unità Analitica dei dati simulati](https://analytics.applicationinsights.io/demo)**  se l'applicazione non invia dati tooApplication Insights ancora.

## <a name="open-analytics"></a>Aprire Analytics
Nella home page dell'app in Application Insights fare clic su Analytics.

![In portal.azure.com, aprire la risorsa di Application Insights e selezionare Analytics.](./media/app-insights-analytics-using/001.png)

esercitazione inline Hello fornisce alcune informazioni su ciò che è possibile eseguire.

È disponibile una [panoramica più ampia qui](app-insights-analytics-tour.md).

## <a name="query-your-telemetry"></a>Eseguire query sui dati di telemetria
### <a name="write-a-query"></a>Scrivere una query
![Visualizzazione schema](./media/app-insights-analytics-using/150.png)

Iniziare con i nomi di hello delle tabelle di hello elencate a sinistra di hello (o hello [intervallo](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) o [unione](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) operatori). Utilizzare `|` toocreate una pipeline di [operatori](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html). 

Viene richiesto con operatori hello e gli elementi di espressione hello che è possibile utilizzare. Fare clic sull'icona informazioni hello (o premere CTRL + BARRA SPAZIATRICE) tooget una descrizione più dettagliata ed esempi su come toouse ogni elemento.

Vedere hello [Introduzione al linguaggio Analitica](app-insights-analytics-tour.md) e [riferimenti al linguaggio](app-insights-analytics-reference.md).

### <a name="run-a-query"></a>Eseguire una query
![Esecuzione di una query](./media/app-insights-analytics-using/130.png)

1. Nelle query è possibile usare interruzioni di riga.
2. Posizionare hello cursore all'interno o alla fine della query hello desiderati toorun hello.
3. Controllare l'intervallo di tempo hello della query. È possibile modificarlo o ignorarlo inserendo la propria clausola [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) nella query.
3. Fare clic su Vai toorun hello.
4. Non inserire righe vuote nella query. È possibile mantenere più query separate in un'unica scheda di query, separandole con righe vuote. Solo query hello con cursore hello viene eseguita.

### <a name="save-a-query"></a>Salvare una query
![Salvataggio di una query](./media/app-insights-analytics-using/140.png)

1. Salvare il file di query corrente hello.
2. Aprire un file di query salvato.
3. Creare un nuovo file di query.

## <a name="see-hello-details"></a>Visualizzare i dettagli di hello
Espandere il relativo elenco completo delle proprietà di qualsiasi riga hello risultati toosee. È inoltre possibile espandere qualsiasi proprietà che è un valore strutturato - ad esempio, le dimensioni personalizzate o stack hello elenco un'eccezione.

![Espandere una riga](./media/app-insights-analytics-using/070.png)

## <a name="arrange-hello-results"></a>Consente di ordinare i risultati di hello
È possibile ordinare, filtrare, impaginare e raggruppare i risultati di hello restituiti dalla query.

> [!NOTE]
> Ordinamento, raggruppamento e applicazione di filtri nel browser hello non rieseguire la query. Essi ridisporre solo risultati hello che sono stati restituiti dalla query ultimo. 
> 
> tooperform queste attività in server hello prima vengono restituiti risultati hello, scrivere la query con hello [ordinamento](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [riepilogare](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) e [dove](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) operatori.
> 
> 

Selezionare le colonne di hello è ad esempio toosee, trascinare toorearrange intestazioni di colonna e ridimensionamento colonne trascinandone i bordi.

![Disporre le colonne](./media/app-insights-analytics-using/030.png)

### <a name="sort-and-filter-items"></a>Ordinare e filtrare elementi
Ordinare i risultati facendo head hello di una colonna. Fare clic su Nuovo hello toosort altro modo, e fare clic su una terza volta toorevert toohello ordine originale restituiti dalla query.

Utilizzare la ricerca di hello filtro icona toonarrow.

![Ordinare e filtrare le colonne](./media/app-insights-analytics-using/040.png)

### <a name="group-items"></a>Raggruppare elementi
toosort da più di una colonna, utilizzare il raggruppamento. Prima di abilitarlo e quindi trascinare le intestazioni di colonna nello spazio di hello sopra la tabella hello.

![Gruppo](./media/app-insights-analytics-using/060.png)

### <a name="missing-some-results"></a>Mancano alcuni risultati?

Se si ritiene che non vengono visualizzati tutti i risultati di hello che previsto, esistono due motivi possibili.

* **Filtro intervallo di tempo**. Per impostazione predefinita, viene visualizzata solo risultati di hello ultime 24 ore. È un filtro automatico che limita l'intervallo di hello dei risultati che vengono recuperate dalle tabelle di origine hello. 

    Tuttavia, è possibile modificare l'intervallo di tempo hello filtro utilizzando il menu di scelta rapida hello.

    Oppure è possibile eseguire l'override di intervallo automatico hello includendo la propria [ `where  ... timestamp ...` clausola](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) nella query. ad esempio:

    `requests | where timestamp > ago('2d')`

* **Limite dei risultati**. È previsto un limite di 10 righe k hello risultati restituiti dal portale hello. Un messaggio di avviso Mostra se è passare supera il limite di hello. In tal caso, ordinare i risultati nella tabella hello non Mostra sempre si tutti hello primo o ultimi risultati effettivi. 

    È di buona norma tooavoid che colpisce hello limite. Utilizzare filtro di intervallo di tempo hello oppure utilizzare gli operatori, ad esempio:

  * [timestamp top 100 by](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) 
  * [take 100](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html)
  * [summarize ](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) 
  * [where timestamp > ago(3d)](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html)

Per visualizzare più di 10.000 righe, è consigliabile usare [Esportazione continua](app-insights-export-telemetry.md). Analytics è progettato per l'analisi e non per il recupero di dati non elaborati.

## <a name="diagrams"></a>Diagrammi
Selezionare il tipo di hello di diagramma che si desidera:

![Selezionare un tipo di diagramma](./media/app-insights-analytics-using/230.png)

Se si dispone di diverse colonne di tipi di destra hello, è possibile scegliere hello x e gli assi y e una colonna di dimensioni toosplit hello risultati.

Per impostazione predefinita, risultati vengono inizialmente visualizzati in una tabella e si seleziona il diagramma hello manualmente. Ma è possibile utilizzare hello [rendering direttiva](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) alla fine hello tooselect una query un diagramma.

### <a name="analytics-diagnostics"></a>Diagnostica di Analytics


In un timechart, se è presente un improvviso picco o un passaggio nei dati, si può vedere un punto evidenziato nella riga hello. Ciò indica che una combinazione di proprietà che filtrano tutte le modifiche improvvise hello è identificato da diagnostica Analitica. Fare clic su hello punto tooget per ulteriori dettagli sul filtro hello e toosee hello filtrato versione. Questo può consentire di identificare quale modifica hello causato. 

[Altre informazioni sulla Diagnostica di Analytics](app-insights-analytics-diagnostics.md)


![Diagnostica di Analytics](./media/app-insights-analytics-using/analytics-diagnostics.png)

## <a name="pin-toodashboard"></a>PIN toodashboard
È possibile aggiungere una tabella o diagramma tooone del [dashboard condiviso](app-insights-dashboards.md) -sufficiente fare clic su Aggiungi hello. (Potrebbe essere troppo[aggiornamento applicazione del pacchetto di prezzi](app-insights-pricing.md) tooturn su questa funzionalità.) 

![Fare clic su hello pin](./media/app-insights-analytics-using/pin-01.png)

Ciò significa che, quando si crea un dashboard toohelp è monitorare le prestazioni di hello o utilizzo dei servizi web, è possibile includere piuttosto complessa analisi insieme hello altre metriche. 

È possibile aggiungere un dashboard toohello tabella, se sono presenti un massimo di quattro colonne. Vengono visualizzate solo hello prime sette righe.

### <a name="dashboard-refresh"></a>Aggiornamento del dashboard
Hello grafico aggiunto toohello dashboard vengono aggiornati automaticamente eseguendo di nuovo la query hello ogni ore circa. È anche possibile fare clic su pulsante Aggiorna hello.

### <a name="automatic-simplifications"></a>Semplificazioni automatiche

Certi semplificazione grafico tooa applicato quando si aggiunge il dashboard tooa.

**Limitazione di tempo:** le query sono automaticamente limitato toohello negli ultimi 14 giorni. Hello effetto è hello stesso come se la query include `where timestamp > ago(14d)`.

**Restrizione del conteggio di bin:** se si visualizza un grafico che dispone di molti bin discreti (in genere un grafico a barre) hello meno bin popolati automaticamente sono raggruppati in un singolo "altri" bin. Ad esempio, questa query:

    requests | summarize count_search = count() by client_CountryOrRegion

ha questo aspetto in Analisi:

![Grafico con una lunga coda](./media/app-insights-analytics-using/pin-07.png)

Tuttavia, quando si aggiunge tooa dashboard, simile al seguente:

![Grafico con bin limitati](./media/app-insights-analytics-using/pin-08.png)

## <a name="export-tooexcel"></a>Esportazione tooExcel
Dopo aver eseguito una query, è possibile scaricare un file con estensione csv. Fare clic su **Esporta in Excel**.

## <a name="export-toopower-bi"></a>Esportazione tooPower BI
Posizionare il cursore di hello in una query e scegliere **esportare, Power BI**.

![Esportazione da Analitica tooPower BI](./media/app-insights-analytics-using/240.png)

Eseguire query hello in Power BI. È possibile impostare toorefresh su una pianificazione.

Con Power BI, è possibile creare i dashboard per raggruppare i dati da un'ampia gamma di origini.

[Ulteriori informazioni sull'esportazione tooPower BI](app-insights-export-power-bi.md)

## <a name="deep-link"></a>Collegamento diretto

Ottenere un collegamento in **esportazione, il collegamento di condivisione** che è possibile inviare tooanother utente. Fornito contiene utente hello [gruppo di risorse di accesso tooyour](app-insights-resources-roles-access-control.md), hello query verrà aperta in hello UI Analitica.

(Collegamento hello, viene visualizzato il testo della query hello dopo "? q =", la compressione gzip e con codifica base 64. È possibile scrivere i collegamenti diretti di codice toogenerate fornire toousers. Tuttavia, hello consigliato modo toorun Analitica dal codice consiste nell'utilizzare hello [API REST](https://dev.applicationinsights.io/).)


## <a name="automation"></a>Automazione

Hello utilizzare [API REST di accesso ai dati](https://dev.applicationinsights.io/) query Analitica toorun. [Ad esempio](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (con PowerShell):

```PS
curl "https://api.applicationinsights.io/beta/apps/DEMO_APP/query?query=requests%7C%20where%20timestamp%20%3E%3D%20ago(24h)%7C%20count" -H "x-api-key: DEMO_KEY"
```

A differenza dell'interfaccia utente Analitica hello, hello API REST non aggiunge automaticamente tutte le query tooyour limitazione di timestamp. Tenere presente che tooadd la propria clausola where, tooavoid ottenere le risposte di grandi dimensioni.



## <a name="import-data"></a>Importa dati

È possibile importare i dati da un file CSV. Un utilizzo tipico è tooimport i dati statici che è possibile unire le tabelle di dati di telemetria. 

Ad esempio, se gli utenti autenticati vengono rilevati nei dati di telemetria da un alias o un id offuscato, è possibile importare una tabella che mappa i nomi di alias tooreal. Eseguendo un join su dati di telemetria di hello richiesta, è possibile identificare gli utenti con i relativi nomi reali nei report Analitica hello.

### <a name="define-your-data-schema"></a>Definire lo schema dei dati

1. Fare clic su **Impostazioni** (in alto a sinistra) e quindi su **Origini dati**. 
2. Aggiungere un'origine dati, attenendosi alle istruzioni hello. Si è richiesto toosupply un campione di dati di hello, che devono includere almeno dieci righe. È quindi possibile correggere schema hello.

Definisce un'origine dati, che è possibile quindi utilizzare tooimport singole tabelle.

### <a name="import-a-table"></a>Importare una tabella

1. Aprire la definizione dell'origine dati dall'elenco di hello.
2. Fare clic su "Carica" e seguono hello istruzioni tooupload hello tabella. Ciò comporta un tooa chiamata API REST e pertanto, è facile tooautomate. 

La tabella è ora disponibile per l'utilizzo nelle query di Analytics. Verrà visualizzata in Analytics 

### <a name="use-hello-table"></a>Utilizzare tabella hello

Si supponga che la definizione dell'origine dati sia denominata `usermap` e che abbia due campi, `realName` e `user_AuthenticatedId`. Hello `requests` tabella include anche un campo denominato `user_AuthenticatedId`, pertanto è facile toojoin loro:

```AIQL

    requests
    | where notempty(user_AuthenticatedId) | take 10
    | join kind=leftouter ( usermap ) on user_AuthenticatedId 
```
la tabella risultante di richieste Hello è una colonna aggiuntiva, `realName`.

### <a name="import-from-logstash"></a>Importare da LogStash

Se si utilizza [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), è possibile utilizzare i log tooquery Analitica. Hello utilizzare [plug-in che invia i dati in Analitica](https://github.com/Microsoft/logstash-output-application-insights). 

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

