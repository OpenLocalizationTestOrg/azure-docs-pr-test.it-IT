---
title: ruoli di server e di lavoro di Application Insights per Windows aaaAzure | Documenti Microsoft
description: "Aggiungere manualmente le prestazioni, disponibilità e utilizzo di Application Insights SDK tooyour ASP.NET dell'applicazione tooanalyze hello."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 106ba99b-b57a-43b8-8866-e02f626c8190
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: 64643ef637195d10f87fc6020a77169bca66c1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manually-configure-application-insights-for-net-applications"></a>Configurare manualmente Application Insights per applicazioni .NET

È possibile configurare [Application Insights](app-insights-overview.md) toomonitor un'ampia gamma di applicazioni o i ruoli applicazione, componenti o microservizi. Per i servizi e le app Web, Visual Studio offre una [configurazione in un solo passaggio](app-insights-asp-net.md). Per altri tipi di applicazione .NET, come ruoli server back-end o applicazioni desktop, è possibile configurare Application Insights manualmente.

![Grafici di monitoraggio delle prestazioni di esempio](./media/app-insights-windows-services/10-perf.png)

#### <a name="before-you-start"></a>Prima di iniziare

Sono necessari:

* Una sottoscrizione troppo[Microsoft Azure](http://azure.com). Se il team o l'organizzazione dispone di una sottoscrizione di Azure, il proprietario di hello può aggiungere l'utente tooit, utilizzando il [account Microsoft](http://live.com).
* Visual Studio 2013 o versione successiva.

## <a name="add"></a>1. Scegliere una risorsa di Application Insights

risorsa' Hello' è in cui i dati vengono raccolti e visualizzati nel portale di Azure hello. È necessario se toodecide toocreate uno nuovo, o una condivisione esistente.

### <a name="part-of-a-larger-app-use-existing-resource"></a>Parte di un'app più grande: usare una risorsa esistente

Se l'applicazione web dispone di diversi componenti, ad esempio, un'applicazione web front-end e uno o più servizi back-end - quindi inviare i dati di telemetria da tutti i toohello componenti hello stessa risorsa. Verrà abilitarli toobe visualizzato in un singolo mapping di applicazioni e rendere possibili tootrace una richiesta da un componente tooanother.

In tal caso, se si sta già monitorando altri componenti di questa app, quindi utilizza solo hello stessa risorsa.

Aprire la risorsa hello in hello [portale di Azure](https://portal.azure.com/). 

### <a name="self-contained-app-create-a-new-resource"></a>App completa: creare una nuova risorsa

Se le applicazioni non correlate tooother hello nuova app, deve essere la propria risorsa.

Accedi toohello [portale di Azure](https://portal.azure.com/)e creare una nuova risorsa di Application Insights. Scegliere ASP.NET come tipo di applicazione hello.

![Fare clic su Nuovo, Application Insights](./media/app-insights-windows-services/01-new-asp.png)

tipo di applicazione scelto Hello imposta contenuto predefinito hello dei pannelli risorse hello.

## <a name="2-copy-hello-instrumentation-key"></a>2. Copiare hello chiave di strumentazione
chiave di Hello identifica risorse hello. Verrà installato appena in hello SDK, nella risorsa toohello dati toodirect di ordine.

![Fare clic su proprietà, selezionare la chiave hello e premere ctrl + C](./media/app-insights-windows-services/02-props-asp.png)

## <a name="sdk"></a>3. Installare il pacchetto Application Insights hello nell'applicazione
Installazione e configurazione di hello Application Insights pacchetto varia a seconda della piattaforma hello che stai lavorando. 

1. In Visual Studio fare clic con il pulsante destro del mouse sul progetto e scegliere **Gestisci pacchetti NuGet**.
   
    ![Fare clic sul progetto hello e scegliere Gestisci pacchetti Nuget](./media/app-insights-windows-services/03-nuget.png)
2. Installare il pacchetto Application Insights hello per le app di Windows server, "Microsoft.ApplicationInsights.WindowsServer".
   
    ![Cercare "Application Insights"](./media/app-insights-windows-services/04-ai-nuget.png)
   
    *Quale versione?*

    Controllare **Includi versione preliminare** se si desidera tootry funzionalità più recenti. documenti rilevanti Hello o blog Nota Se è necessaria una versione non definitiva.
    
    *È possibile usare altri pacchetti?*
   
    Sì. Se si desidera toouse hello API toosend propri dati di telemetria, scegliere "Microsoft. applicationinsights". pacchetto di Windows Server Hello include hello API più una serie di altri pacchetti, ad esempio la raccolta dei contatori delle prestazioni e il monitoraggio della dipendenza. 

### <a name="tooupgrade-toofuture-package-versions"></a>versioni del pacchetto toofuture tooupgrade
Microsoft rilasciare una nuova versione di hello SDK da tootime ora.

tooupgrade tooa [nuova versione del pacchetto di hello](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), riaprire Gestione pacchetti NuGet e filtrare i pacchetti installati. Selezionare **Microsoft.ApplicationInsights.WindowsServer** e scegliere **Aggiorna**.

Se sono state tooApplicationInsights.config eventuali personalizzazioni, salvare una copia prima di eseguire l'aggiornamento, nella nuova versione di hello in seguito il merge delle modifiche.

## <a name="4-send-telemetry"></a>4. Inviare dati di telemetria
**Se è installato solo il pacchetto hello API:**

* Impostare la chiave di strumentazione hello nel codice, ad esempio `main()`: 
  
    `TelemetryConfiguration.Active.InstrumentationKey = "`*nome della chiave*`";` 
* [Scrivere i propri dati di telemetria usando API hello](app-insights-api-custom-events-metrics.md#ikey).

**Se sono installati altri pacchetti di Application Insights,** è possibile utilizzare in se si preferisce, chiave di strumentazione hello tooset file config hello:

* Modificare Applicationinsights (che è stato aggiunto per installare NuGet hello). Inserire questa istruzione prima hello tag di chiusura:
  
    `<InstrumentationKey>`*chiave di strumentazione hello copiato*`</InstrumentationKey>`
* Verificare che la proprietà hello di Applicationinsights in Esplora soluzioni è impostata troppo**Build Action = il contenuto, copia tooOutput Directory = copia**.

È utile tooset hello strumentazione chiave nel codice se si desidera troppo[chiave hello commutatore per diverse configurazioni della build](app-insights-separate-resources.md). Se si imposta la chiave hello nel codice, non è necessario tooset in hello `.config` file.

## <a name="run"></a> Eseguire il progetto
Hello utilizzare **F5** toorun l'applicazione e per provarlo: Apri diverse pagine toogenerate alcuni dati di telemetria.

In Visual Studio, verrà visualizzato un conteggio di eventi di hello che sono stati inviati.

![Conteggio degli eventi in Visual Studio](./media/app-insights-windows-services/appinsights-09eventcount.png)

## <a name="monitor"></a> Visualizzare i dati di telemetria
Restituire toohello [portale di Azure](https://portal.azure.com/) e individuare la risorsa di Application Insights tooyour.

Cercare i dati nei grafici Panoramica hello. All'inizio si vedranno solo uno o due punti. ad esempio:

![Fare clic sui dati toomore](./media/app-insights-windows-services/12-first-perf.png)

Fare clic su tramite qualsiasi toosee grafico le metriche dettagliate. [Altre informazioni sulle metriche.](app-insights-web-monitor-performance.md)

### <a name="no-data"></a>Dati non visualizzati
* Utilizzare l'applicazione hello, apertura di pagine diverse in modo che generi alcuni dati di telemetria.
* Aprire hello [ricerca](app-insights-diagnostic-search.md) riquadro, toosee singoli eventi. In alcuni casi accetta eventi poco mentre più tooget tramite pipeline metriche hello.
* Attendere alcuni secondi e fare clic su **Aggiorna**. Grafici Aggiorna periodicamente se stessi, ma è possibile aggiornare manualmente, se in attesa per tooshow alcuni dati.
* Vedere [Domande su Application Insights per ASP.NET](app-insights-troubleshoot-faq.md).

## <a name="publish-your-app"></a>Pubblicare l'app
Ora di distribuire il server di applicazioni tooyour o accumulano dati hello tooAzure ed espressioni di controllo.

![Uso di Visual Studio toopublish dell'app](./media/app-insights-windows-services/15-publish.png)

Quando si esegue in modalità di debug, dati di telemetria viene avviata tramite pipeline hello, in modo che verranno visualizzati i dati visualizzati in pochi secondi. Quando si distribuisce l'applicazione nella configurazione Release, i dati si accumulano più lentamente.

### <a name="no-data-after-you-publish-tooyour-server"></a>Nessun dato dopo la pubblicazione tooyour server?
Aprire le porte per il traffico in uscita nel firewall del server. Vedere [questa pagina](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) per elenco hello di indirizzi richiesti 

### <a name="trouble-on-your-build-server"></a>Problemi del server di compilazione
Vedere [questa sezione sulla risoluzione dei problemi](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).

> [!NOTE]
> Se l'applicazione genera un grande quantità di dati di telemetria, modulo di campionamento adattivo hello ridurrà automaticamente volume hello inviato toohello portale inviando solo una frazione rappresentativa di eventi. Tuttavia, gli eventi che sono correlato toohello stessa richiesta verrà selezionata o deselezionata come gruppo, in modo che è possibile spostarsi tra gli eventi correlati. 
> [Informazioni sul campionamento](app-insights-sampling.md).
> 
> 

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Passaggi successivi
* [Aggiungere ulteriori dati di telemetria](app-insights-asp-net-more.md) tooget hello 360 gradi di visualizzazione dell'applicazione.

