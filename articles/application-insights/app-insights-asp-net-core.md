---
title: Application Insights per ASP.NET Core aaaAzure | Documenti Microsoft
description: "Monitorare la disponibilità, le prestazioni e l'utilizzo delle applicazioni Web."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 3b722e47-38bd-4667-9ba4-65b7006c074c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: a7a27f9eef1daec5b0deae9fd88906e646980659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-aspnet-core"></a>Application Insights per ASP.NET Core
[Application Insights](app-insights-overview.md) consente di monitorare la disponibilità, le prestazioni e l'uso dell'applicazione Web. Con il feedback hello che è ottenere sulle prestazioni di hello e l'efficacia dell'app in hello wild, è possibile prendere decisioni informate sulla direzione hello della progettazione hello in ogni ciclo di vita di sviluppo.

![Esempio](./media/app-insights-asp-net-core/sample.png)

È necessaria una sottoscrizione con [Microsoft Azure](http://azure.com). È possibile accedere con un account Microsoft, che in genere si ottiene per Windows, XBox Live o altri servizi cloud Microsoft. Il team potrebbe avere un tooAzure sottoscrizione aziendale: chiedere hello proprietario tooadd tooit con l'account Microsoft.

## <a name="getting-started"></a>introduttiva

* In Esplora soluzioni di Visual Studio fare clic con il pulsante destro del mouse sul progetto e selezionare **Configura Application Insights** oppure **Aggiungi > Application Insights**. [Altre informazioni](app-insights-asp-net.md)
* Se i comandi di menu non viene visualizzata, seguire hello [manuale Guida introduttiva recupero](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started). Potrebbe essere necessario toodo questo se il progetto è stato creato con una versione di Visual Studio prima 2017.

## <a name="using-application-insights"></a>Utilizzo di Application Insights
Sign in hello [portale Microsoft Azure](https://portal.azure.com)selezionare **tutte le risorse** o **Application Insights**, quindi selezionare risorsa hello creato toomonitor l'app.

In una finestra separata dal browser, usare l'app per un periodo di tempo. Si noterà che i dati visualizzati nei grafici di Application Insights hello. (Potrebbe essere tooclick aggiornamento). Ci sarà solo una piccola quantità di dati al momento dello sviluppo, ma questi grafici si attiveranno davvero quando si pubblicherà l'app e si avranno numerosi utenti. 

pagina di panoramica Hello vengono visualizzati grafici di prestazioni chiave: tempo di risposta server, il tempo di caricamento pagina e il numero di richieste non riuscite. Fare clic su qualsiasi toosee grafico più grafici e dati.

Visualizzazioni nel portale di hello rientrano in tre categorie principali:

* [Esplora metriche](app-insights-metrics-explorer.md) Mostra grafici e tabelle di metrica e i conteggi, ad esempio tempi di risposta, percentuale degli errori o metriche personalizzate con hello [API](app-insights-api-custom-events-metrics.md). Filtro e segmento dati hello da tooget di valori di proprietà una comprensione migliore dell'app e i relativi utenti.
* [Ricerca di Esplora](app-insights-diagnostic-search.md) Elenca gli eventi singoli, ad esempio richieste specifiche, eccezioni, le tracce di log o eventi creato personalmente con hello [API](app-insights-api-custom-events-metrics.md). Filtrare e cercare gli eventi di hello e spostarsi tra i problemi di tooinvestigate eventi correlati.
* [Analisi](app-insights-analytics.md) consente di eseguire query simili a SQL sui dati di telemetria ed è un potente strumento di analisi e diagnostica.

## <a name="alerts"></a>Avvisi
* Si ottengono automaticamente [avvisi di diagnostica proattivi](app-insights-proactive-diagnostics.md) che informano su modifiche anomale alle frequenze di errori o ad altre metriche.
* Impostare [disponibilità test](app-insights-monitor-web-app-availability.md) tootest un sito Web continuamente da parte del mondo e si invia tramite posta elettronica non appena un test ha esito negativo.
* Impostare [metrici avvisi](app-insights-monitor-web-app-availability.md) tooknow se metriche, ad esempio tempi di risposta o tariffe eccezione compresa nei limiti accettabili.

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

## <a name="open-source"></a>Aprire origine
[Leggere e fornire codice toohello](https://github.com/Microsoft/ApplicationInsights-aspnetcore#recent-updates)


## <a name="next-steps"></a>Passaggi successivi
* [Aggiungere le pagine web di telemetria tooyour](app-insights-javascript.md) toomonitor pagina informazioni sull'utilizzo e prestazioni.
* [Monitoraggio dipendenze](app-insights-asp-net-dependencies.md) toosee se REST, SQL o altre risorse esterne rallentano è.
* [Utilizzare l'API di hello](app-insights-api-custom-events-metrics.md) toosend di eventi e le metriche per una visualizzazione più dettagliata dell'utilizzo e delle prestazioni dell'applicazione.
* [Test disponibilità](app-insights-monitor-web-app-availability.md) controllare app costantemente dal mondo hello. 

