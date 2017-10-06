---
title: aaaDependency rilevamento in Azure Application Insights | Documenti Microsoft
description: "Analizzare l'uso, la disponibilità e le prestazioni dell'applicazione locale o Web di Microsoft Azure con Application Insights."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d15c4ca8-4c1a-47ab-a03d-c322b4bb2a9e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: bwren
ms.openlocfilehash: e72f5465462ae8e64363cbbaa62911aff636c504
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-application-insights-dependency-tracking"></a>Impostare Application Insights: tenere traccia delle dipendenze
Una *dipendenza* è un componente esterno chiamato dall'app. In genere è un servizio chiamato con il protocollo HTTP, oppure un database o un file system. [Application Insights](app-insights-overview.md) misura per quanto tempo l'applicazione attende le dipendenze e la frequenza con la quale una chiamata alle dipendenze non riesce. È possibile provare a utilizzare chiamate specifiche e correlarle toorequests ed eccezioni.

![grafici di esempio](./media/app-insights-asp-net-dependencies/10-intro.png)

attualmente, il monitoraggio delle dipendenze di casella Hello segnala chiamate toothese tipi di dipendenze:

* Server
  * Database SQL
  * Servizi Web ASP.NET e WCF che usano i binding basati su HTTP
  * Chiamate HTTP locali o remote
  * Azure Cosmos DB, tabelle, archiviazione BLOB e coda
* Pagina Web
  * Chiamate AJAX

Il monitoraggio funziona tramite l'uso di [strumentazione con codice byte](https://msdn.microsoft.com/library/z9z62c29.aspx) basata su determinati metodo. L'overhead delle prestazioni è minimo.

È anche possibile scrivere un proprio SDK chiama toomonitor altre dipendenze, sia nel codice client e server hello utilizzando hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).

## <a name="set-up-dependency-monitoring"></a>Configurare il monitoraggio delle dipendenze
Dipendenza parziale vengono raccolti automaticamente mediante hello [Application Insights SDK](app-insights-asp-net.md). tooget completo dei dati, installare l'agente appropriato di hello per server host hello.

| Piattaforma | Installa |
| --- | --- |
| Server IIS |Entrambi [installa Status Monitor nel server](app-insights-monitor-performance-live-website-now.md) o [l'aggiornamento del framework dell'applicazione too.NET 4.6 o versione successivo](http://go.microsoft.com/fwlink/?LinkId=528259) e installare hello [Application Insights SDK](app-insights-asp-net.md) nell'app. |
| App Web di Azure |Nel Pannello di controllo per l'app web, [blade di Application Insights hello aperti nel Pannello di controllo di app web](app-insights-azure-web-apps.md) e scegliere Installa, se richiesto. |
| Servizio cloud di Azure |[Usare l'attività di avvio](app-insights-cloudservices.md) oppure [installare .NET Framework 4.6+](../cloud-services/cloud-services-dotnet-install-dotnet.md). |

## <a name="where-toofind-dependency-data"></a>In dati sulle dipendenze toofind
* La [mappa delle applicazioni](#application-map) visualizza le dipendenze tra l'app e i componenti adiacenti.
* I [pannelli Prestazioni, Browser ed Errori](#performance-and-blades) visualizzano i dati sulle dipendenze del server.
* Il [pannello Browser](#ajax-calls) visualizza le chiamate AJAX dai browser degli utenti.
* [Fare clic su tramite richieste lente o non riuscite](#diagnose-slow-requests) chiama la relativa dipendenza toocheck.
* [Analitica](#analytics) possono essere utilizzati tooquery dipendenza dati.

## <a name="application-map"></a>Mappa delle applicazioni
Mappa delle applicazioni agisce come delle dipendenze toodiscovering visivo tra hello dei componenti dell'applicazione. Viene generato automaticamente da dati di telemetria hello dall'app. Questo esempio mostra le chiamate AJAX dagli script browser hello e le chiamate REST dal server hello servizi esterni tootwo di app.

![Mappa delle applicazioni](./media/app-insights-asp-net-dependencies/08.png)

* **Passare dalle caselle hello** toorelevant dipendenza e altri grafici.
* **Mappa di hello pin** toohello [dashboard](app-insights-dashboards.md), dove sarà completamente funzionale.

[Altre informazioni](app-insights-app-map.md)

## <a name="performance-and-failure-blades"></a>Pannelli Prestazioni ed Errori
Pannello prestazioni Hello Mostra la durata di hello delle chiamate di dipendenza effettuate dall'applicazione server hello. Sono presenti un grafico di riepilogo e una tabella segmentata per chiamata.

![Grafici delle dipendenze nel pannello Prestazioni](./media/app-insights-asp-net-dependencies/dependencies-in-performance-blade.png)

Fare clic sui grafici di riepilogo hello o hello tabella elementi toosearch non elaborato le occorrenze di queste chiamate.

![Istanze delle chiamate alle dipendenze](./media/app-insights-asp-net-dependencies/dependency-call-instance.png)

**Numero di errori nei** vengono visualizzati nella hello **errori** blade. Qualsiasi codice restituito non è in hello intervallo 200-399, o sconosciuto è un errore.

> [!NOTE]
> Il **100% di errori** indica probabilmente che si stanno ricevendo solo dati parziali sulle dipendenze. È necessario troppo[impostare dipendenza monitoraggio piattaforma appropriata tooyour](#set-up-dependency-monitoring).
>
>

## <a name="ajax-calls"></a>Chiamate AJAX
Pannello browser Hello Mostra la durata di hello e percentuale di errori di AJAX chiamate dal [JavaScript nelle pagine web](app-insights-javascript.md). Sono visualizzate come dipendenze.

## <a name="diagnosis"></a> Diagnosticare le richieste lente
Ogni evento di richiesta è associata a chiamate a dipendenze hello, eccezioni e altri eventi che vengono rilevati durante l'elaborazione dell'applicazione hello richiesta. Se alcune richieste esegue in modo errato, trovare, è possibile definire se si trova a causa di una risposta tooslow da una dipendenza.

Di seguito è illustrato un esempio.

### <a name="tracing-from-requests-toodependencies"></a>Esecuzione della traccia da toodependencies richieste
Aprire il pannello di prestazioni hello ed esaminare griglia hello di richieste:

![Elenco di richieste con conteggi e medie](./media/app-insights-asp-net-dependencies/02-reqs.png)

inizio Hello uno sta richiedendo molto tempo. Vediamo se è possibile scoprire dove viene impiegato il tempo di hello.

Fare clic sulla riga toosee singola richiesta gli eventi:

![Elenco di occorrenze di richiesta](./media/app-insights-asp-net-dependencies/03-instances.png)

Fare clic su qualsiasi istanza di a esecuzione prolungata tooinspect ulteriormente e scorrere verso il basso toohello dipendenza remoto chiamate toothis correlati richiesta:

![Trovare le dipendenze tooRemote chiamate, identificare insolita durata](./media/app-insights-asp-net-dependencies/04-dependencies.png)

Sembra che la maggior parte delle hello ora manutenzione impiegato per la richiesta in un servizio locale tooa di chiamata.

Selezionare tale tooget riga per ulteriori informazioni:

![Fare clic su a causa di hello tooidentify tale dipendenza remoto](./media/app-insights-asp-net-dependencies/05-detail.png)

Sembra che qui viene ospitata problema hello. È stato individuare il problema di hello, pertanto ora è necessario toofind out perché la chiamata richiede molto tempo.

### <a name="request-timeline"></a>Sequenza temporale della richiesta
In un altro caso non ci sono chiamate a dipendenze particolarmente lunghe, Tuttavia, passando alla visualizzazione cronologia toohello, possiamo vedere dove si è verificato il ritardo di hello l'elaborazione interna:

![Trovare le dipendenze tooRemote chiamate, identificare insolita durata](./media/app-insights-asp-net-dependencies/04-1.png)

Ci toobe un grande spazio dopo la chiamata della dipendenza prima hello, in modo da esaminare toosee il nostro codice motivo che è.

### <a name="profile-your-live-site"></a>Profilatura del sito live

Non è chiaro quale passare del tempo di hello? Hello [profiler Application Insights](app-insights-profiler.md) tracce HTTP chiama sito attivo tooyour e illustra le funzioni nel codice richiede tempo più lungo di hello.

## <a name="failed-requests"></a>Richieste non riuscite
Richieste non riuscite potrebbero inoltre essere associate a toodependencies chiamate non riuscite. Nuovamente, è possibile scorrere tootrack problema hello.

![Fare clic sul grafico di hello richieste non riuscite](./media/app-insights-asp-net-dependencies/06-fail.png)

Fare clic sulle tooan occorrenza di una richiesta non riuscita ed esaminare gli eventi associati.

![Fare clic su un tipo di richiesta, fare clic su hello istanza tooget tooa vista diversa della stessa istanza di hello, selezionarlo tooget i dettagli dell'eccezione.](./media/app-insights-asp-net-dependencies/07-faildetail.png)

## <a name="analytics"></a>Analytics
È possibile tenere traccia delle dipendenze in hello [il linguaggio di query Log Analitica](https://docs.loganalytics.io/). Di seguito sono riportati alcuni esempi.

* Trovare eventuali chiamate alle dipendenze non riuscite:

```

    dependencies | where success != "True" | take 10
```

* Trovare le chiamate AJAX:

```

    dependencies | where client_Type == "Browser" | take 10
```

* Trovare le chiamate alle dipendenze associate alle richieste:

```

    dependencies
    | where timestamp > ago(1d) and  client_Type != "Browser"
    | join (requests | where timestamp > ago(1d))
      on operation_Id  
```


* Trovare le chiamate AJAX associate alle visualizzazioni di pagina:

```

    dependencies
    | where timestamp > ago(1d) and  client_Type == "Browser"
    | join (browserTimings | where timestamp > ago(1d))
      on operation_Id
```



## <a name="custom-dependency-tracking"></a>Rilevamento personalizzato delle dipendenze
modulo di rilevamento delle dipendenze standard Hello individua automaticamente le dipendenze esterne quali database e le API REST. Ma è possibile che alcuni componenti aggiuntivi di toobe trattate hello stesso modo.

È possibile scrivere codice che invia le informazioni sulle dipendenze, utilizzando hello stesso [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) utilizzato dai moduli standard hello.

Ad esempio, se si compila il codice con un assembly che non scritto personalmente, è possibile ora tutti hello chiamate tooit, toofind out il contributo che rende la risposta tooyour volte. toohave dati visualizzati nei grafici dipendenza hello in Application Insights, inviarlo tramite `TrackDependency`.

```C#

            var startTime = DateTime.UtcNow;
            var timer = System.Diagnostics.Stopwatch.StartNew();
            try
            {
                success = dependency.Call();
            }
            finally
            {
                timer.Stop();
                telemetry.TrackDependency("myDependency", "myCall", startTime, timer.Elapsed, success);
            }
```

Se si desidera tooswitch off modulo di rilevamento di hello dipendenza standard, rimuovere hello riferimento tooDependencyTrackingTelemetryModule in [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md).

## <a name="troubleshooting"></a>Risoluzione dei problemi
*Il flag di operazione riuscita della dipendenza visualizza sempre true o false.*

*Query SQL no visualizzate completamente.*

* Eseguire l'aggiornamento più recente di hello SDK toohello. Se la versione di .NET è precedente alla 4.6:
  * Host IIS: installare [agente di Application Insights](app-insights-monitor-performance-live-website-now.md) nei server host hello.
  * App web di Azure: Apri Application Insights scheda nel Pannello di controllo di hello web app e installare Application Insights.

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Passaggi successivi
* [Eccezioni](app-insights-asp-net-exceptions.md)
* [Dati utente e di pagina](app-insights-javascript.md)
* [Disponibilità](app-insights-monitor-web-app-availability.md)
