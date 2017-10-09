---
title: aaaSet backup analitica di app web per ASP.NET con Azure Application Insights | Documenti Microsoft
description: "Configurare l'analisi delle prestazioni, della disponibilità e dell'utilizzo per un sito Web ASP.NET, ospitato in locale o in Azure."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d0eee3c0-b328-448f-8123-f478052751db
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: 61a3cdce68da48bfb9450b1d296acc1535f50a38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-application-insights-for-your-aspnet-website"></a>Installare Application Insights per un sito Web ASP.NET

Questa procedura consente di configurare i dati di telemetria toohello ASP.NET web app toosend [Azure Application Insights](app-insights-overview.md) servizio. Funziona per le applicazioni ASP.NET che sono ospitate nel server IIS o nel Cloud hello. Verrà visualizzato grafici e un linguaggio di query potenti che consentono di comprendere le prestazioni di hello dell'app e modalità di utilizzo di più avvisi automatici in caso di problemi di prestazioni. Molti sviluppatori trovano queste funzionalità eccellenti come sono, ma è anche possibile estendere e personalizzare i dati di telemetria hello se è necessario.

Il programma di installazione richiede pochi clic in Visual Studio. È necessario addebiti di hello opzione tooavoid limitando volume hello di telemetria. In questo modo si tooexperiment e di debug o toomonitor un sito con non molti utenti. Quando si decide si desidera toogo-ahead e monitorare il sito di produzione, è il limite di hello tooraise semplice in un secondo momento.

## <a name="before-you-start"></a>Prima di iniziare
Sono necessari:

* Visual Studio 2013 Update 3 o versioni successive. È preferibile una versione successiva.
* Una sottoscrizione troppo[Microsoft Azure](http://azure.com). Se il team o l'organizzazione dispone di una sottoscrizione di Azure, il proprietario di hello possibile aggiungere è tooit, utilizzando il [account Microsoft](http://live.com).

Sono disponibili argomenti alternativo toolook in se si è interessati:

* [Strumentazione di un'app Web in fase di esecuzione](app-insights-monitor-performance-live-website-now.md)
* [Servizi cloud di Azure](app-insights-cloudservices.md)

## <a name="ide"></a>Passaggio 1: Aggiungere hello Application Insights SDK

Fare clic con il pulsante destro del mouse sul progetto dell'app Web in Esplora soluzioni e scegliere **Aggiungi** > **Application Insights Telemetry** oppure **Configura Application Insights**.

![Screenshot di Esplora soluzioni con le opzioni Aggiungi e Application Insights Telemetry evidenziate](./media/app-insights-asp-net/appinsights-03-addExisting.png)

(In Visual Studio 2015, è inoltre disponibile un'opzione tooadd Application Insights, nella finestra di dialogo Nuovo progetto hello.)

Continuare toohello pagina di configurazione di Application Insights:

![Screenshot della pagina Registra l'app con Application Insights](./media/app-insights-asp-net/visual-studio-register-dialog.png)

**a.** Selezionare l'account hello e sottoscrizione utilizzare tooaccess Azure.

**b.** Selezionare la risorsa hello in Azure in cui si desidera dati hello toosee dall'app. In genere:

* Usare un'[unica risorsa per diversi componenti](app-insights-monitor-multi-role-apps.md) di una singola applicazione. 
* Creare risorse separate per applicazioni non correlate.
 
Se si desidera tooset hello risorse gruppo o hello percorso in cui sono memorizzati i dati, fare clic su **configurare le impostazioni**. Gruppi di risorse sono utilizzati toocontrol toodata di accesso. Ad esempio, se si dispone di più App che fanno parte di hello stesso sistema, si potrebbero inserire i dati di Application Insights in hello stesso gruppo di risorse.

**c.** Impostare un limite al limite di volume di dati gratuito hello, tooavoid addebiti. Application Insights è liberare tooa certo volume di dati di telemetria. Dopo aver creata la risorsa hello, è possibile modificare la selezione nel portale di hello aprendo **funzionalità + prezzi** > **gestione di volumi di dati** > **giornaliero estremità di volume**.

**d.** Fare clic su **registrare** toogo-ahead e configurare Application Insights per l'app web. Dati di telemetria verranno inviati toohello [portale di Azure](https://portal.azure.com), sia durante il debug e dopo aver pubblicato l'applicazione.

**e.** Se non si desidera portale toohello di telemetria toosend durante il debug, aggiungere app tooyour di Application Insights SDK hello ma non si configura una risorsa nel portale di hello. Sarà in grado di toosee telemetria in Visual Studio durante il debug. In un secondo momento, è possibile restituire la pagina di configurazione toothis oppure è possibile attendere fino a dopo aver distribuito l'app e [passare telemetria in fase di esecuzione](app-insights-monitor-performance-live-website-now.md).


## <a name="run"></a>Passaggio 2: Eseguire l'app
Eseguire l'app con F5. Aprire pagine diverse toogenerate alcuni dati di telemetria.

In Visual Studio, viene visualizzato un conteggio di eventi di hello che sono stati registrati.

![Screenshot di Visual Studio. pulsante di Application Insights Hello Mostra durante il debug.](./media/app-insights-asp-net/54.png)

## <a name="step-3-see-your-telemetry"></a>Passaggio 3: Visualizzare i dati di telemetria
È possibile visualizzare i dati di telemetria in Visual Studio o nel portale web di Application Insights hello. Ricerca di dati di telemetria in Visual Studio toohelp si esegue il debug dell'app. Monitoraggio delle prestazioni e l'utilizzo nel portale web di hello quando il sistema è in tempo reale. 

### <a name="see-your-telemetry-in-visual-studio"></a>Visualizzare i dati di telemetria in Visual Studio

In Visual Studio, aprire finestra di Application Insights hello. Fare clic su hello **Application Insights** pulsante o destro del mouse sul progetto in Esplora soluzioni, scegliere **Application Insights**, quindi fare clic su **ricerca Live telemetria**.

Nella finestra di ricerca di Visual Studio Application Insights hello, vedere hello **dati da una sessione di Debug** visualizzazione di dati di telemetria generato sul lato server hello dell'app. Sperimentare filtri hello e fare clic su qualsiasi toosee evento maggiori dettagli.

![Schermata di hello consente di visualizzare dati da una sessione di debug nella finestra di Application Insights hello.](./media/app-insights-asp-net/55.png)

> [!NOTE]
> Se tutti i dati non viene visualizzato, verificare che sia corretto, intervallo di tempo hello e fare clic sull'icona di ricerca hello.

[Uso di Application Insights in Visual Studio](app-insights-visual-studio.md).

<a name="monitor"></a>
### <a name="see-telemetry-in-web-portal"></a>Visualizzare i dati di telemetria nel portale Web

È inoltre possibile visualizzare i dati di telemetria nel portale web di Application Insights hello (a meno che non si è scelto di hello solo tooinstall SDK). portale di Hello dispone di più grafici, strumenti di analisi e visualizzazioni tra componenti di Visual Studio. portale di Hello offre anche gli avvisi.

Aprire la risorsa Application Insights. Firmare in toohello [portale di Azure](https://portal.azure.com/) disponibili in tale posizione o il pulsante destro del mouse hello progetto in Visual Studio e lasciare che consentono di accedere non esiste.

![Schermata di Visual Studio, che mostra come tooopen hello portale Application Insights](./media/app-insights-asp-net/appinsights-04-openPortal.png)

> [!NOTE]
> Se si verifica un errore di accesso: si dispone più di un set di credenziali di Microsoft, e eseguito l'accesso con il set corretto di hello? Nel portale di hello, disconnettersi e accedere di nuovo.

viene visualizzato il portale di Hello su una vista di telemetria hello dall'app.

![Screenshot della pagina Panoramica di Application Insights](./media/app-insights-asp-net/66.png)

Nel portale di hello, fare clic su qualsiasi riquadro o un grafico di toosee maggiori dettagli.

[Ulteriori informazioni sull'utilizzo di Application Insights nel portale di Azure hello](app-insights-dashboards.md).

## <a name="step-4-publish-your-app"></a>Passaggio 4: Pubblicare l'app
Pubblicare il server IIS di app tooyour o tooAzure. Espressioni di controllo [flusso metriche in tempo reale](app-insights-metrics-explorer.md#live-metrics-stream) toomake che tutto sia in esecuzione senza problemi.

Dati di telemetria a crescere nel portale Application Insights hello, in cui è possibile monitorare le metriche, cercare i dati di telemetria e impostare [dashboard](app-insights-dashboards.md). È inoltre possibile utilizzare hello potente [il linguaggio di query Log Analitica](https://docs.loganalytics.io/) tooanalyze utilizzo e prestazioni o toofind eventi specifici.

È anche possibile continuare tooanalyze dati di telemetria in [Visual Studio](app-insights-visual-studio.md), con strumenti quali ricerca diagnostica e [tendenze](app-insights-visual-studio-trends.md).

> [!NOTE]
> Se l'app invia sufficiente hello tooapproach telemetria [limitazioni](app-insights-pricing.md#limits-summary)automatico [campionamento](app-insights-sampling.md) attiva. Campionamento riduce la quantità hello di telemetria inviato dall'app, mantenendo i dati correlati per scopi diagnostici.
>
>

## <a name="land"></a> Le impostazioni sono state completate.

Congratulazioni. È installato il pacchetto di Application Insights hello nell'app e configurato il servizio di Application Insights toohello toosend telemetria in Azure.

![Diagramma dello spostamento dei dati di telemetria](./media/app-insights-asp-net/01-scheme.png)

risorse di Azure che riceve i dati di telemetria dell'applicazione Hello è identificato da un *chiave di strumentazione*. Questa chiave sono disponibili nel file Applicationinsights config hello.


## <a name="upgrade-toofuture-sdk-versions"></a>Aggiornare le versioni SDK toofuture
tooupgrade tooa [nuova versione di hello SDK](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases)aprire hello **Gestione pacchetti NuGet** nuovamente e filtrare i pacchetti installati. Selezionare **Microsoft.ApplicationInsights.Web** e scegliere **Aggiorna**.

Se sono state tooApplicationInsights.config eventuali personalizzazioni, salvare una copia prima dell'aggiornamento. Quindi, inserire le modifiche nella nuova versione di hello.

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Passaggi successivi

### <a name="more-telemetry"></a>Altri dati di telemetria

* **[Dati sul browser e sul caricamento di pagine](app-insights-javascript.md)**: inserire un frammento di codice nelle pagine Web.
* **[Ottenere un monitoraggio più dettagliato di dipendenze ed eccezioni](app-insights-monitor-performance-live-website-now.md)**: installare Status Monitor nel server.
* **[Codice di eventi personalizzati](app-insights-api-custom-events-metrics.md)**  toocount, ora, o una misura delle azioni dell'utente.
* **[Ottenere dati di log](app-insights-asp-net-trace-logs.md)**: correlare i dati di log con i dati di telemetria.

### <a name="analysis"></a>Analisi

* **[Uso di Application Insights in Visual Studio](app-insights-visual-studio.md)**<br/>Include informazioni sul debug con dati di telemetria, ricerca di diagnostica e drill-through toocode.
* **[Utilizzo di portale Application Insights hello](app-insights-dashboards.md)**<br/> Include informazioni su dashboard, strumenti avanzati di diagnostica e di analisi, avvisi, mappa attiva delle dipendenze dell'applicazione ed esportazione dei dati di telemetria.
* **[Analitica](app-insights-analytics-tour.md)**  -hello linguaggio di query efficace.

### <a name="alerts"></a>Avvisi

* [Test disponibilità](app-insights-monitor-web-app-availability.md): creazione di test che il sito sia visibile sul web hello toomake.
* [Smart diagnostica](app-insights-proactive-diagnostics.md): questi test viene eseguito automaticamente, non vi è toodo nulla tooset tali backup. Se l'app ha una frequenza insolita di richieste non riuscite, verrà comunicato automaticamente.
* [Metrici avvisi](app-insights-alerts.md): impostare questi toowarn se una metrica supera una soglia. È possibile impostarli nelle metriche personalizzate di cui si scrive il codice nell'app.

### <a name="automation"></a>Automazione

* [Automatizzare la creazione di risorse di Application Insights](app-insights-powershell.md)
