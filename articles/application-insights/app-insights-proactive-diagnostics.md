---
title: Rilevamento in Azure Application Insights aaaSmart | Documenti Microsoft
description: Application Insights esegue automaticamente un'analisi approfondita dei dati di telemetria dell'app e segnala potenziali problemi.
services: application-insights
documentationcenter: windows
author: rakefetj
manager: carmonm
ms.assetid: 2eeb4a35-c7a1-49f7-9b68-4f4b860938b2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: f794476088fc69154eda2077b7a5cdc769fab3a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="smart-detection-in-application-insights"></a>Rilevamento intelligente in Application Insights
 Il rilevamento intelligente segnala automaticamente i potenziali problemi di prestazioni nell'applicazione Web. Esegue l'analisi proattiva dei dati di telemetria hello che l'app invia troppo[Application Insights](app-insights-overview.md). Se si verifica un improvviso aumento della percentuale di errori o in caso di modelli anomali delle prestazioni di client o server, viene generato un avviso. Questa funzionalità non richiede alcuna configurazione. Funziona se l'applicazione invia dati di telemetria sufficienti.

È possibile accedere gli avvisi di rilevamento intelligente da messaggi di posta elettronica hello che viene visualizzato sia dal pannello Smart rilevamento hello.

## <a name="review-your-smart-detections"></a>Esaminare i rilevamenti intelligenti
È possibile individuare i rilevamenti in due modi:

* **Viene visualizzato un messaggio di posta elettronica** da Application Insights. Ecco un esempio tipico:
  
    ![Avviso di posta elettronica](./media/app-insights-proactive-diagnostics/03.png)
  
    Fare clic su hello pulsante grande tooopen più dettagliatamente nel portale di hello.
* **riquadro rilevamento intelligente Hello** panoramica dell'app pannello Visualizza il numero di avvisi recenti. Fare clic su hello riquadro toosee un elenco degli avvisi recenti.

![Visualizzare rilevamenti recenti](./media/app-insights-proactive-diagnostics/04.png)

Selezionare un avviso toosee i dettagli.

## <a name="what-problems-are-detected"></a>Tipi di problemi rilevati
Esistono tre tipologie di rilevamento:

* [Rilevamento intelligente: anomalie negli errori](app-insights-proactive-failure-diagnostics.md). Si usa machine learning frequenza hello previsto tooset delle richieste non riuscite per l'app, correlazione con carico e di altri fattori. Se la percentuale di errori hello passa all'esterno di busta previsto hello, si invia un avviso.
* [Rilevamento intelligente: anomalie nelle prestazioni](app-insights-proactive-performance-diagnostics.md). Ricevere le notifiche se il tempo di risposta di un'operazione o la dipendenza di durata rallentamento toohistorical confrontati della linea di base o se si stabilisce un modello anomalo in fase di caricamento pagina o di tempi di risposta.   
* [Rilevamento intelligente: problemi del servizio cloud di Azure](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/). Vengono inviati avvisi all'utente se l'app è ospitata in Servizi cloud di Azure e un'istanza del ruolo presenta errori di avvio, ricicli frequenti o arresti anomali del sistema in fase di esecuzione.

(i collegamenti della Guida hello in ogni notifica visualizzano articoli pertinenti toohello.)

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Passaggi successivi
Questi strumenti di diagnostica consentono di controllare la telemetria hello dall'app:

* [Esplora metriche](app-insights-metrics-explorer.md)
* [Esplora ricerche](app-insights-diagnostic-search.md)
* [Linguaggio avanzato di query di Analisi](app-insights-analytics-tour.md)

Il rilevamento intelligente è completamente automatico, Ma forse si vogliono tooset di alcune ulteriori avvisi?

* [Configurare manualmente gli avvisi relativi alle metriche](app-insights-alerts.md)
* [Test Web di disponibilità](app-insights-monitor-web-app-availability.md) 

