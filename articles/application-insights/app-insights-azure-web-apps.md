---
title: prestazioni dell'applicazione web di Azure aaaMonitor | Documenti Microsoft
description: Monitoraggio delle prestazioni applicative per le app Web di Azure. Tempo di caricamento e risposta del grafico, informazioni sulle dipendenze e impostazione di avvisi sulle prestazioni.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0b2deb30-6ea8-4bc4-8ed0-26765b85149f
ms.service: azure-portal
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: d1083254e5c504b18f2ac5ae2368610dc2790436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-web-app-performance"></a>Monitoraggio delle prestazioni dell'applicazione web di Azure
In hello [portale Azure](https://portal.azure.com) è possibile impostare il monitoraggio delle prestazioni dell'applicazione per il [App web di Azure](../app-service-web/app-service-web-overview.md). [Azure Application Insights](app-insights-overview.md) Instrumenta la telemetria dell'app toosend sui relativi toohello attività servizio di Application Insights, in cui sono stati archiviato e analizzato. Non esiste, metrica grafici e strumenti di ricerca possono essere utilizzati toohelp diagnosticare i problemi, migliorare le prestazioni e valutare l'utilizzo.

## <a name="run-time-or-build-time"></a>Fase di esecuzione o fase di compilazione
È possibile configurare il monitoraggio tramite la strumentazione dell'applicazione hello in uno dei due modi:

* **Fase di esecuzione** : è possibile selezionare un'estensione di monitoraggio delle prestazioni quando l'app Web è già attiva. Non è necessario toorebuild oppure reinstallare l'app. Si ottiene un set di pacchetti standard che monitorano i tempi di risposta, le percentuali di riuscita, le eccezioni, le dipendenze e così via. 
* **Fase di compilazione** : è possibile installare un pacchetto nell'app durante lo sviluppo. Questa opzione è più versatile. In aggiunta toohello stessi pacchetti standard, è possibile scrivere dati di telemetria hello codice toocustomize o toosend propri dati di telemetria. È possibile registrare le attività specifiche o registrare gli eventi in base toohello semantica del dominio applicazione. 

## <a name="run-time-instrumentation-with-application-insights"></a>Strumentazione della fase di esecuzione con Application Insights
Se si esegue già un'App Web in Azure, vengono già visualizzati alcuni dati di monitoraggio, cioè la frequenza di esecuzione con errori e la frequenza delle richieste. Aggiungere altre, ad esempio tempi di risposta, monitoraggio chiamate toodependencies, rilevamento intelligente e potente linguaggio di query Log Analitica hello tooget di Application Insights. 

1. **Selezionare Application Insights** nel Pannello di controllo Azure hello per le app web.
   
    ![In Monitoraggio scegliere Application Insights](./media/app-insights-azure-web-apps/05-extend.png)
   
   * Scegliere toocreate una nuova risorsa, a meno che non è già stata configurata una risorsa di Application Insights per l'app da un'altra route.
2. **Instrumentare l'App Web** dopo l'installazione di Application Insights. 
   
    ![Instrumentazione dell'App Web](./media/app-insights-azure-web-apps/restart-web-app-for-insights.png)

   **Abilitare il monitoraggio lato client** per la visualizzazione delle pagine e la telemetria utente.

   * Selezionare Impostazioni > Impostazioni applicazione
   * In Impostazioni app aggiungere una nuova coppia chiave-valore: 
   
    Chiave: `APPINSIGHTS_JAVASCRIPT_ENABLED` 
    
    Valore: `true`
   * **Salvare** hello impostazioni e **riavviare** l'app.
3. **Monitorare l'app**.  [Dati hello Expore](#explore-the-data).

In un secondo momento, è possibile compilare app hello con Application Insights, se si desidera.

*Come rimuovere Application Insights, o passare toosending tooanother risorse?*

* In Azure, pannello di controllo aprire hello web app e in strumenti di sviluppo, aprire **estensioni**. Eliminare l'estensione Application Insights hello. Quindi sotto monitoraggio, scegliere Application Insights e creare o selezionare hello risorsa desiderata.

## <a name="build-hello-app-with-application-insights"></a>Compilare l'applicazione hello con Application Insights
Application Insights può fornire ulteriori dati di telemetria installando un SDK nell'applicazione. In particolare, è possibile raccogliere i log di traccia, [scrivere dati di telemetria personalizzati](app-insights-api-custom-events-metrics.md) e ottenere report di eccezione più dettagliati.

1. **In Visual Studio** 2013 Update 2 o versione successiva configurare Application Insights per il progetto.

    Progetto web hello e scegliere **Aggiungi > Application Insights** o **Configura Application Insights**.
   
    ![Fare clic sul progetto web hello e scegliere di aggiungere o configurare Application Insights](./media/app-insights-azure-web-apps/03-add.png)
   
    Se viene chiesto toosign in, utilizzare le credenziali di hello per l'account di Azure.
   
    operazione Hello ha due effetti:
   
   1. Crea una risorsa di Application Insights in Azure, in cui vengono archiviati, analizzati e visualizzati i dati di telemetria.
   2. Aggiunge hello NuGet di Application Insights tooyour codice di pacchetto (se non è presente già) e lo configura toosend telemetria toohello risorse di Azure.
2. **Verificare i dati di telemetria hello** da app di hello in esecuzione nel computer di sviluppo (F5).
3. **Pubblicare l'applicazione hello** tooAzure in hello come di consueto. 

*Come passare risorsa di Application Insights toosending tooa diversi?*

* In Visual Studio, progetto hello pulsante destro del mouse, scegliere **Configura Application Insights** e scegliere hello risorsa desiderata. È possibile ottenere hello opzione toocreate una nuova risorsa. Ricompilare e ridistribuire.

## <a name="explore-hello-data"></a>Esplorare i dati di hello
1. Nel Pannello di Application Insights hello del Pannello di controllo di app web, consente di visualizzare metriche in tempo reale, che mostra le richieste e gli errori all'interno di un secondo o due di essi in corso. È molto utile visualizzare questi dati quando si esegue di nuovo la pubblicazione di un'app, perché eventuali problemi sono immediatamente visibili.
2. Fare clic sulle toohello completo della risorsa Application Insights.

    ![Fare clic](./media/app-insights-azure-web-apps/view-in-application-insights.png)

    È anche possibile accedervi direttamente dal riquadro di esplorazione delle risorse di Azure.

1. Fare clic sulle tooget qualsiasi grafico dettaglio:
   
    ![Nel pannello della panoramica hello Application Insights, fare clic su un grafico](./media/app-insights-azure-web-apps/07-dependency.png)
   
    È possibile [personalizzare i pannelli delle metriche](app-insights-metrics-explorer.md).
2. Fare clic sulle altre toosee singoli eventi e le relative proprietà:
   
    ![Fare clic su una ricerca filtrata su tale tipo di un tooopen di tipo evento](./media/app-insights-azure-web-apps/08-requests.png)
   
    Si noti hello "..." tooopen collegamento tutte le proprietà.
   
    È possibile [personalizzare le ricerche](app-insights-diagnostic-search.md).

Per le ricerche più potenti su dati di telemetria, utilizzare hello [il linguaggio di query Log Analitica](app-insights-analytics-tour.md).

## <a name="more-telemetry"></a>Altri dati di telemetria

* [Dati di caricamento della pagina Web](app-insights-javascript.md)
* [Telemetria personalizzata](app-insights-api-custom-events-metrics.md)

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Passaggi successivi
* [Eseguire il profiler di hello nella tua app in tempo reale](app-insights-profiler.md).
* [Funzioni di Azure](https://github.com/christopheranderson/azure-functions-app-insights-sample): monitorare Funzioni di Azure con Application Insights
* [Abilitare diagnostica di Azure](app-insights-azure-diagnostics.md) tooApplication toobe inviate informazioni dettagliate.
* [Monitorare le metriche di integrità servizio](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) toomake che il servizio sia disponibile e reattiva.
* [Ricevere notifiche di avviso](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) ogni volta che si verificano eventi operativi o le metriche superano una soglia.
* Utilizzare [Application Insights per le app JavaScript e pagine web](app-insights-javascript.md) telemetria client tooget dai browser hello che visita una pagina web.
* [Configurare i test web disponibilità](app-insights-monitor-web-app-availability.md) toobe ricevere un avviso se il sito è inattivo.

