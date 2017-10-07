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
# <a name="analytics-in-application-insights"></a>Analytics in Application Insights
[Analitica](app-insights-analytics.md) è hello ricerca potenti funzionalità di [Application Insights](app-insights-overview.md). Queste pagine descrivono il linguaggio di query di Log Analytics. 

* **[Guardare video introduttivo hello](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.
* **[Test unità Analitica dei dati simulati](https://analytics.applicationinsights.io/demo)**  se l'applicazione non invia dati tooApplication Insights ancora.
* **[SQL utenti schede di riferimento rapido](https://aka.ms/sql-analytics)**  traduce idiomi comuni hello.
* **[Riferimenti al linguaggio](app-insights-analytics-reference.md)**  informazioni su come toouse tutti hello potenti funzionalità di linguaggio di query Log Analitica hello.


## <a name="queries-in-analytics"></a>Query in Analytics
Una query tipica è costituita da una tabella di *origine* seguita da una serie di *operatori* separati da `|`. 

Ad esempio, possibile scoprire l'orario di cittadini hello di giorno di Hyderabad provare l'app web. E mentre siamo, esaminare i codici di risultato vengono restituiti le richieste HTTP tootheir. 

```AIQL
requests
| where timestamp > ago(30d)
| summarize ClientCount = dcount(client_IP) by bin(timestamp, 1h), resultCode
| extend LocalTime = timestamp - 4h
| order by LocalTime desc
| render barchart
```

Abbiamo conteggio indirizzi IP client distinti, raggruppandoli in base all'ora di hello del giorno hello su hello ultimi 7 giorni. 

> [!NOTE]
> risultati tooget di fuori di hello 24 ore precedenti, includere 'timestamp' in modo esplicito nella query o utilizzare i menu a discesa intervallo tempo hello.
>

Verranno visualizzati risultati hello con hello barra presentazione grafico, la selezione toostack hello dai codici di risposta diversi:

![Scegliere il grafico a barre, gli assi X e Y, quindi la segmentazione](./media/app-insights-analytics/020.png)

L'app sembra riscuotere molto successo a Hyderabad all'ora di pranzo e prima di andare a dormire. (Si dovrebbe anche esaminare quei 500 codici).

Sono inoltre disponibili operazioni statistiche avanzate:

![Risultati della query statistica](./media/app-insights-analytics/025.png)

linguaggio Hello presenta molte funzionalità interessanti:


* [Filtrare](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) i dati di telemetria app non elaborati in base a qualsiasi campo, comprese proprietà personalizzate e metriche.
* [Unire](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) più tabelle: correlare le richieste a visualizzazioni di pagina, chiamate a dipendenze, eccezioni e tracce di log.
* [Aggregazioni](https://docs.loganalytics.io/learn/tutorials/aggregations.html)statistiche avanzate.
* Efficienti quanto SQL, ma è molto più semplice per le query complesse: invece di nidificazione di istruzioni, si invia tramite pipe dati hello da un'operazione elementari toohello successivamente.
* Visualizzazioni immediate e avanzate.
* [PIN grafici dashboard tooAzure](app-insights-analytics-using.md#pin-to-dashboard).
* [Esportare le query tooPower BI](app-insights-analytics-using.md#export-to-power-bi).
* È presente un [API REST](https://dev.applicationinsights.io/) che è possibile utilizzare toorun query a livello di codice, ad esempio da Powershell.


## <a name="connect-tooyour-application-insights-data"></a>Connettere i dati di Application Insights tooyour
Aprire Analisi dal [pannello Panoramica](app-insights-dashboards.md) dell'app in Application Insights: 

![In portal.azure.com, aprire la risorsa di Application Insights e selezionare Analytics.](./media/app-insights-analytics/001.png)


## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]



## <a name="query-examples"></a>Esempi di query

Provare questi power hello tooillustrate di procedure dettagliate dell'uso Analitica:

 *  [Diagnostica automatica di picchi e salti procedurali nella durata delle richieste](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Automatic%20diagnostics%20of%20sudden%20spikes%20or%20step%20jumps%20in%20requests%20duration&shared=true)
 *  [Analisi delle riduzioni delle prestazioni con l'analisi delle serie temporali](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20performance%20degradations%20with%20time%20series%20analysis&shared=true)
 *  [Analisi degli errori delle applicazioni con autocluster e diffpatterns](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20application%20failures%20with%20autocluster%20and%20diffpatterns&shared=true)
 *  [Rilevamenti forma avanzati con l'analisi delle serie temporali](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Advanced%20shape%20detection%20with%20time%20series%20analysis&shared=true)
 *  [Utilizzando la finestra operazioni tooanalyze utilizzo dell'applicazione (in sequenza e così via MAU/DAU)](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Using%20sliding%20window%20calculations%20to%20analyze%20usage%20metrics:%20rolling%20MAU~2FDAU%20and%20cohorts&shared=true)
 *  [Rilevamento di interruzioni del servizio in base all'analisi dei registri di debug](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) e post di blog corrispondente [qui](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).
 *  [Profilatura delle prestazioni delle applicazioni tramite log di debug semplici](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) e post di blog corrispondente [qui](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)
 *  [Misurazione della durata di hello per ogni passaggio nel flusso di codice utilizzando i registri di debug semplice](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) e un post di blog corrispondente [qui](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)
 *  [Analisi della concorrenza tramite log di debug semplici](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) e post di blog corrispondente [qui](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)



## <a name="next-steps"></a>Passaggi successivi
* È consigliabile iniziare con hello [Introduzione al linguaggio](app-insights-analytics-tour.md). 
* Altre informazioni sull'[uso di Analytics](app-insights-analytics-using.md). 
* [Informazioni di riferimento sul linguaggio](app-insights-analytics-reference.md). 
