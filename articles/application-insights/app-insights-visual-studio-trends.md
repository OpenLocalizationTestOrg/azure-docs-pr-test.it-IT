---
title: Tendenze aaaAnalyzing in Visual Studio | Documenti Microsoft
description: Analizzare, visualizzare ed esaminare le tendenze nei dati di telemetria di Application Insights in Visual Studio.
services: application-insights
documentationcenter: .net
author: numberbycolors
manager: carmonm
ms.assetid: 3150c6fc-2691-44f6-a290-fc5cd68e692a
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: 5c623ec040363f05e80ca927dc8855eb016adc99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="analyzing-trends-in-visual-studio"></a>Analisi delle tendenze in Visual Studio
strumento di tendenze di Application Insights Hello Visualizza gli eventi di telemetria importanti dell'applicazione web cambiano nel tempo, consentono di identificare rapidamente i problemi e anomalie. Collegando toomore dettagliate informazioni di diagnostica, le tendenze consentono di migliorare le prestazioni dell'applicazione, tenere traccia cause hello delle eccezioni e rilevare le informazioni dagli eventi personalizzati.

![Finestra Tendenze di esempio](./media/app-insights-visual-studio-trends/app-insights-trends-hero-750.png)

## <a name="configure-your-web-app-for-application-insights"></a>Configurare l'app Web per Application Insights

Se non è ancora stato fatto, [configurare l'app Web per Application Insights](app-insights-overview.md). In questo modo portale Application Insights toohello di telemetria toosend. strumento di tendenze Hello legge telemetria hello da qui.

Tendenze di Application Insights è disponibile in Visual Studio 2015 Update 3 e versioni successive.

## <a name="open-application-insights-trends"></a>Aprire Tendenze di Application Insights
finestra di tendenze di Application Insights tooopen hello:

* Pulsante della barra degli strumenti di Application Insights hello, scegliere **esplorare le tendenze di telemetria**, o
* Dal menu di scelta rapida hello progetto, scegliere **Application Insights > esplorare le tendenze di telemetria**, o
* Dalla barra dei menu di Visual Studio hello, scegliere **Vista > altre finestre > tendenze di Application Insights**.

È possibile visualizzare un prompt dei comandi tooselect una risorsa. Fare clic su **selezionare una risorsa**, accedere con una sottoscrizione di Azure, quindi scegliere una risorsa di Application Insights hello elenco per il quale si desidera tooanalyze le tendenze di telemetria.

## <a name="choose-a-trend-analysis"></a>Scegliere un'analisi delle tendenze
![Menu dei tipi comuni di analisi delle tendenze](./media/app-insights-visual-studio-trends/app-insights-trends-1-750.png)

Iniziare scegliendo una delle cinque analisi tendenza comuni, ogni analisi di dati da hello ultime 24 ore:

* **Analizzare i problemi di prestazioni con le richieste server** -servizio tooyour, raggruppato per tempi di risposta alle richieste.
* **Analizzare gli errori nelle richieste server** -richieste di servizio tooyour, raggruppato in base al codice di risposta HTTP
* **Esaminare le eccezioni di hello nell'applicazione** -eccezioni dal servizio, raggruppati per tipo di eccezione
* **Controllare le prestazioni di hello delle dipendenze dell'applicazione** -servizi chiamati dal servizio, raggruppati per tempi di risposta
* **Esame degli eventi personalizzati** : eventi personalizzati configurati per il servizio, raggruppati in base al tipo di evento

Queste analisi incorporati sono disponibili in un secondo momento da hello **visualizzare tipi comuni di analisi di dati di telemetria** pulsante hello nell'angolo superiore sinistro della finestra di tendenze hello.

## <a name="visualize-trends-in-your-application"></a>Visualizzare le tendenze nell'applicazione
Tendenze di Application Insights crea una visualizzazione basata su serie temporale dei dati di telemetria dell'app. Ogni visualizzazione basata su serie temporale contiene un tipo di dati di telemetria, raggruppati in base a una proprietà di tali dati, in un determinato intervallo di tempo. Ad esempio, è consigliabile richieste server tooview, raggruppate in base al paese hello da cui sono stati generati, su hello ultime 24 ore. In questo esempio, ogni bolla sulla visualizzazione hello rappresentano un numero di richieste di server hello per alcuni paese/area geografica durante un'ora.

Usare i controlli di hello nella parte superiore di hello di hello finestra tooadjust quali tipi di dati di telemetria visualizzare. In primo luogo, scegliere i tipi di dati di telemetria hello in cui si è interessati:

* **Tipo di telemetria** : richieste server, eccezioni, dipendenze o eventi personalizzati
* **Intervallo di tempo** - ovunque hello ultimi 30 minuti toohello ultimi 3 giorni
* **Raggruppa per** : tipo di eccezione, ID problema, paese/area geografica e altro ancora

Quindi, fare clic su **analisi telemetria** query hello toorun.

toonavigate tra bolle in visualizzazione hello:

* Fare clic su tooselect una bolla, che aggiorna i filtri di hello nella parte inferiore di hello della finestra hello, riepilogo eventi hello solo durante un periodo di tempo specifico
* Fare doppio clic su uno strumento di ricerca toohello toonavigate a bolle e visualizzare tutti gli eventi di telemetria singoli hello che si sono verificati durante tale periodo di tempo
* Fare clic tenendo premuto il tasto CTRL a bolle toode-select nella visualizzazione hello.

> [!TIP]
> Hello tendenze e ricerca strumenti interagiscono toohelp evidenziare le cause di hello di problemi del servizio tra migliaia di eventi di telemetria. Se in un pomeriggio i clienti notano che l'app ha una velocità di risposta inferiore, ad esempio, iniziare con Analisi. Analizzare le richieste effettuate servizio tooyour su hello ultime ore, raggruppati in base al tempo di risposta. e osservare se sono presenti gruppi insolitamente consistenti di richieste lente. Quindi fare doppio clic a bolle toogo toohello ricerca dello strumento, eventi di richiesta toothose filtrato. Ricerca, è possibile esplorare il contenuto di hello di tali richieste e spostarsi nel codice toohello problema hello tooresolve coinvolti.
> 
> 

## <a name="filter"></a>Filtro
Individuare le tendenze più specifiche con controlli del filtro nella parte inferiore di hello della finestra hello hello. tooapply un filtro, fare clic sul relativo nome. È possibile passare rapidamente tra le tendenze toodiscover filtri diversi che possono nascondere in una determinata dimensione dei dati di telemetria. Se si applica un filtro in una dimensione, ad esempio il tipo di eccezione, i filtri in altre dimensioni rimangono selezionabili anche se sono presenti inattivo. tooun-applicare un filtro, fare di nuovo clic. CTRL + clic tooselect più filtri in hello stessa dimensione.

![Filtri delle tendenze](./media/app-insights-visual-studio-trends/TrendsFiltering-750.png)

Cosa accade se si desidera tooapply più filtri? 

1. Applicare hello primo filtro. 
2. Fare clic su hello **applicare i filtri selezionati ed eseguire query nuovamente** pulsante in base al nome hello della dimensione hello del primo filtro. Questo richiederà nuovamente i dati di telemetria per solo gli eventi che corrispondono al filtro di primo hello. 
3. Applicare un secondo filtro. 
4. Ripetere le tendenze di toofind processo hello in subset specifici dei dati di telemetria. Ad esempio, nelle richieste server denominate "GET Home/Index" *e* provenienti dalla Germania *e* che hanno ricevuto un codice di risposta 500. 

tooun-applicare uno di questi filtri, fare clic su hello **rimuovere i filtri selezionati ed eseguire query nuovamente** pulsante per la dimensione di hello.

![Filtri multipli](./media/app-insights-visual-studio-trends/TrendsFiltering2-750.png)

## <a name="find-anomalies"></a>Trovare le anomalie
strumento di tendenze Hello possibile evidenziare bolle degli eventi anomali tooother confrontati bolle in hello la stessa ora di serie. Nell'elenco a discesa tipo di visualizzazione hello, scegliere **conteggi nell'intervallo di tempo (evidenziazione delle anomalie)** o **percentuali nell'intervallo di tempo (evidenziazione delle anomalie)**. Le bolle di colore rosso sono anomale. Le anomalie sono definite come bolle con conteggi le percentuali superiori ai 2.1 tempi hello deviazione standard dei conteggi hello/percentuali che si sono verificati in hello oltre due periodi di tempo (48 ore se si sta visualizzando hello last 24 ore, ecc.).

![I punti colorati indicano anomalie](./media/app-insights-visual-studio-trends/TrendsAnomalies-750.png)

> [!TIP]
> L'evidenziazione delle anomalie è particolarmente utile per trovare in una serie temporale di piccole bolle outlier che potrebbero altrimenti sembrare di dimensioni simili.  
> 
> 

## <a name="next"></a>Passaggi successivi
|  |  |
| --- | --- |
| **[Uso di Application Insights in Visual Studio](app-insights-visual-studio.md)**<br/>Ricerca sui dati di telemetria, visualizzazione dei dati in CodeLens e configurazione di Application Insights. Tutto in Visual Studio. |![Fare clic sul progetto hello e scegliere di Application Insights, ricerca](./media/app-insights-visual-studio-trends/34.png) |
| **[Aggiungere altri dati](app-insights-asp-net-more.md)**<br/>Monitorare l'utilizzo, la disponibilità, le dipendenze e le eccezioni, integrare le tracce dei framework di registrazione e scrivere telemetria personalizzata. |![Visual Studio](./media/app-insights-visual-studio-trends/64.png) |
| **[Utilizzo di portale Application Insights hello](app-insights-dashboards.md)**<br/>Dashboard, strumenti avanzati di diagnostica e di analisi, avvisi, mappa attiva delle dipendenze dell'applicazione ed esportazione dei dati di telemetria. |![Visual Studio](./media/app-insights-visual-studio-trends/62.png) |

