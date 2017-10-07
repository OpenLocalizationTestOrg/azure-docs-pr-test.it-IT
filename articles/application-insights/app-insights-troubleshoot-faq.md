---
title: domande frequenti di Application Insights aaaAzure | Documenti Microsoft
description: Domande frequenti su Application Insights.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0e3b103c-6e2a-4634-9e8c-8b85cf5e9c84
ms.service: application-insights
ms.workload: mobile
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: bwren
ms.openlocfilehash: e27ee9b7d040a04828a9892865a6681b83f94326
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-frequently-asked-questions"></a>Application Insights: domande frequenti

## <a name="configuration-problems"></a>Problemi di configurazione
*Problemi nella configurazione di:*

* [App .NET](app-insights-asp-net-troubleshoot-no-data.md)
* [Monitoraggio di un'applicazione già in esecuzione](app-insights-monitor-performance-live-website-now.md#troubleshooting-runtime-configuration-of-application-insights)
* [Diagnostica di Azure](app-insights-azure-diagnostics.md)
* [App Web Java](app-insights-java-troubleshoot.md)

*Non sono disponibili dati dal server*

* [Impostare le eccezioni del firewall](app-insights-ip-addresses.md)
* [Configurare un server ASP.NET](app-insights-monitor-performance-live-website-now.md)
* [Configurare un server Java](app-insights-java-agent.md)

## <a name="can-i-use-application-insights-with-"></a>Si può usare Application Insights con ...?

* [App Web in un server IIS locale o in una macchina virtuale](app-insights-asp-net.md)
* [App Web Java](app-insights-java-get-started.md)
* [App Node.js](app-insights-nodejs.md)
* [App Web in Azure](app-insights-azure-web-apps.md)
* [Servizi cloud in Azure](app-insights-cloudservices.md)
* [Server app eseguiti in Docker](app-insights-docker.md)
* [App Web a pagina singola](app-insights-javascript.md)
* [SharePoint](app-insights-sharepoint.md)
* [App desktop Windows](app-insights-windows-desktop.md)
* [Altre piattaforme](app-insights-platforms.md)

## <a name="is-it-free"></a>È gratuito?

Sì, per l'uso sperimentale. In hello prezzi piano basic, l'applicazione può inviare una determinata indennità dei dati ogni mese gratuitamente. Hello disponibile sia sufficiente toocover sviluppo e pubblicazione di un'app per un numero ridotto di utenti. È possibile impostare un limite tooprevent più di una quantità di dati specificata dall'elaborazione.

Volumi più elevati di dati di telemetria vengono addebitati mediante hello Gb. Vengono forniti alcuni suggerimenti sul troppo[limitare gli addebiti](app-insights-pricing.md).

piano dell'organizzazione Hello comporta un addebito per ogni giorno in cui ogni nodo del server web invia dati di telemetria. È adatta se si desidera toouse esportazione continua su larga scala.

[Hello lettura prezzi piano](https://azure.microsoft.com/pricing/details/application-insights/).

## <a name="how-much-is-it-costing"></a>Quanto costa?

* Aprire hello **funzionalità + prezzi** pagina in una risorsa di Application Insights. È incluso un grafico dell'utilizzo recente. Se si vuole, è possibile impostare un limite di volume di dati.
* Aprire hello [pannello fatturazione di Azure](https://portal.azure.com/#blade/Microsoft_Azure_Billing/BillingBlade/Overview) toosee gli effetti di tutte le risorse.

## <a name="q14"></a>Quali modifiche apporta Application Insights al progetto?
Dettagli Hello dipendono dal tipo di hello del progetto. Per un'applicazione Web:

* Aggiunge i file di progetto tooyour:

  * ApplicationInsights.config.
  * ai.js
* Installa i pacchetti NuGet seguenti:

  * *Application Insights API* : hello API di base
  * *Application Insights API per le applicazioni Web* -utilizzato telemetria toosend dal server hello
  * *Application Insights API per applicazioni JavaScript* -utilizzato telemetria toosend da client hello

    i pacchetti Hello includono questi assembly:
  * Microsoft.ApplicationInsights
  * Microsoft.ApplicationInsights.Platform
* Inserire elementi in:

  * Web.config
  * packages.config
* (Nuovo progetti only - se si [Aggiungi progetto esistente di Application Insights tooan][start], è stato toodo manualmente.) Inserisce i frammenti di codice tooinitialize di codice hello client e server con ID risorsa di Application Insights hello. Ad esempio, in un'applicazione MVC, codice viene inserito in una pagina master hello Views/Shared/_Layout.cshtml

## <a name="how-do-i-upgrade-from-older-sdk-versions"></a>In che modo è possibile effettuare l'aggiornamento da versioni dell'SDK meno recenti?
Vedere hello [note sulla versione](app-insights-release-notes.md) per hello SDK appropriati tooyour tipo di applicazione.

## <a name="update"></a>In che modo è possibile modificare la risorsa di Azure che riceve i dati del progetto?
In Esplora soluzioni fare clic con il pulsante destro del mouse su `ApplicationInsights.config` e scegliere **Aggiorna Application Insights**. È possibile inviare hello tooan esistente o nuova risorsa di dati in Azure. Modifica aggiornamento Hello hello chiave di strumentazione di Applicationinsights, che determina a quale server hello SDK invia i dati. A meno che non si deseleziona "Aggiorna tutto", verrà modificato anche chiave hello in cui viene visualizzato nelle pagine web.

## <a name="what-is-status-monitor"></a>Che cos'è Status Monitor?

Un'applicazione desktop che consente il toohelp di server web IIS configurare Application Insights nelle App web. Non raccoglie dati di telemetria: è possibile interromperlo se non si sta configurando un'app. 

[Altre informazioni](app-insights-monitor-performance-live-website-now.md#questions).

## <a name="what-telemetry-is-collected-by-application-insights"></a>Quali dati di telemetria vengono raccolti da Application Insights?

Da app Web del server:

* Richieste HTTP
* [Dipendenze](app-insights-asp-net-dependencies.md). Le chiamate a: database SQL. HTTP chiama servizi tooexternal; Azure Cosmos DB, tabella, nell'archiviazione blob e coda. 
* [Eccezioni](app-insights-asp-net-exceptions.md) e analisi dello stack.
* [I contatori delle prestazioni](app-insights-performance-counters.md) : se si utilizza [Status Monitor](app-insights-monitor-performance-live-website-now.md), Azure monitoring(app-insights-azure-web-apps.md) o hello [writer collectd Application Insights](app-insights-java-collectd.md).
* [Metrica ed eventi personalizzati](app-insights-api-custom-events-metrics.md) codificati.
* [I log di traccia](app-insights-asp-net-trace-logs.md) se si configura l'agente di raccolta dati appropriata hello.

Da [pagine Web dei client](app-insights-javascript.md):

* [Conteggi delle visualizzazioni pagina](app-insights-web-track-usage.md)
* [Chiamate AJAX](app-insights-asp-net-dependencies.md): richieste effettuate da uno script in esecuzione.
* Dati di carico della visualizzazione pagina
* Conteggi di utenti e sessioni
* [ID utente autenticato](app-insights-api-custom-events-metrics.md#authenticated-users)

Da altre origini, se sono configurate:

* [Diagnostica di Azure](app-insights-azure-diagnostics.md)
* [Contenitori Docker](app-insights-docker.md)
* [Importazione di tabelle tooAnalytics](app-insights-analytics-import.md)
* [OMS (Log Analytics)](https://azure.microsoft.com/blog/omssolutionforappinsightspublicpreview/)
* [Logstash](app-insights-analytics-import.md)

## <a name="can-i-filter-out-or-modify-some-telemetry"></a>È possibile filtrare o modificare alcuni dati di telemetria?

In server hello Sì, è possibile scrivere:

* Dati di telemetria processore toofilter o aggiungere elementi di dati di telemetria tooselected proprietà prima che vengano inviati dall'app.
* Dati di telemetria inizializzatore tooadd proprietà tooall degli elementi di dati di telemetria.

Vedere altre informazioni per [ASP.NET](app-insights-api-filtering-sampling.md) o [Java](app-insights-java-filter-telemetry.md).

## <a name="how-are-city-country-and-other-geo-location-data-calculated"></a>Come vengono calcolati i dati su città, paesi e altre aree geografiche?

Saremo indirizzo hello IP (IPv4 o IPv6) del client web hello utilizzando [GeoLite2](http://dev.maxmind.com/geoip/geoip2/geolite2/).

* Dati di telemetria browser: indirizzo IP del mittente hello raccolte.
* Dati di telemetria server: il modulo di Application Insights hello raccoglie l'indirizzo IP del client hello. L'indirizzo non viene raccolto se è impostato `X-Forwarded-For`.

È possibile configurare hello `ClientIpHeaderTelemetryInitializer` indirizzo IP di hello tootake da un'intestazione diversa. In alcuni sistemi, ad esempio, lo spostamento da un proxy, il carico troppo di bilanciamento del carico o della rete CDN`X-Originating-IP`. [Altre informazioni](http://apmtips.com/blog/2016/07/05/client-ip-address/)

È possibile [usare Power BI](app-insights-export-power-bi.md) toodisplay dati di telemetria richiesta su una mappa.


## <a name="data"></a>Quanto tempo i dati verranno mantenuti nel portale di hello? Tale conservazione è sicura?
Vedere l'argomento relativo a [conservazione dei dati e privacy][data].

## <a name="might-personally-identifiable-information-pii-be-sent-in-hello-telemetry"></a>Informazioni personali (PII) è possibile inviare nei dati di telemetria hello?

Ciò si verifica se il codice invia tali dati. E può verificarsi anche se le variabili dell'analisi dello stack includono informazioni personali. Il team di sviluppo deve eseguire tooensure valutazioni dei rischi che informazioni personali viene gestita correttamente. Vedere [altre informazioni sulla conservazione e privacy dei dati](app-insights-data-retention-privacy.md).

ottetti di ultima Hello dell'indirizzo web del client hello sono sempre impostato too0 dopo l'inserimento dal portale hello.

## <a name="my-ikey-is-visible-in-my-web-page-source"></a>L'iKey dell'utente è visibile nell'origine della pagina Web. 

* Questo è una pratica comune nelle soluzioni di monitoraggio.
* Non può essere utilizzato toosteal i dati.
* Può essere utilizzato tooskew gli avvisi dati o del trigger.
* Nessun cliente ha segnalato tali problemi.

È possibile:

* Usare due valori iKey separati, ovvero due risorse separate di Application Insights, per i dati del client e del server. Or
* Scrivere un proxy che viene eseguito nel server e che i client web hello a invii i dati tramite tale proxy.

## <a name="post"></a>Come visualizzare dati POST in Ricerca diagnostica?
È non registra i dati POST automaticamente, ma è possibile utilizzare una chiamata a TrackTrace: inserire dati hello nel parametro messaggio hello. Questo è un limite di dimensioni più tempo rispetto a limiti di hello per le proprietà della stringa, anche se non è possibile filtrare su di esso.

## <a name="should-i-use-single-or-multiple-application-insights-resources"></a>È preferibile usare una o più risorse di Application Insights?

Utilizzare una singola risorsa per tutti i componenti di hello o i ruoli in un sistema di business. Usare risorse separate per sviluppo, test e versioni di rilascio e per applicazioni indipendenti.

* [Vedere hello discussione qui](app-insights-separate-resources.md)
* [Esempio: servizio cloud con ruoli di lavoro e Web](app-insights-cloudservices.md)

## <a name="how-do-i-dynamically-change-hello-instrumentation-key"></a>Come si modifica in modo dinamico i chiave di strumentazione hello?

* [Vedere questo articolo](app-insights-separate-resources.md)
* [Esempio: servizio cloud con ruoli di lavoro e Web](app-insights-cloudservices.md)

## <a name="what-are-hello-user-and-session-counts"></a>Quali sono hello utente e sessione conta?

* Hello JavaScript SDK viene impostato un cookie di utente nel client web hello tooidentify degli utenti e delle attività toogroup cookie della sessione.
* Se non è presente alcun script sul lato client, è possibile [impostare cookie server hello](http://apmtips.com/blog/2016/07/09/tracking-users-in-api-apps/).
* Se un utente reale usa il sito in browser diversi o esegue una navigazione privata o in incognito oppure usa computer diversi, viene inclusi più di una volta nei conteggi.
* tooidentify un utente connesso in macchine e i browser, aggiungere una chiamata troppo[setAuthenticatedUserContect()](app-insights-api-custom-events-metrics.md#authenticated-users).

## <a name="q17"></a> In Application Insights sono state abilitate tutte le funzionalità?
| Elementi che dovrebbero essere visualizzati | Come tooget, | Perché si vuole ottenerli |
| --- | --- | --- |
| Grafici di disponibilità |[Test Web](app-insights-monitor-web-app-availability.md) |Stabilire se l'app Web è attiva |
| Prestazioni dell'app server: tempi di risposta, ... |[Aggiungere Application Insights tooyour progetto](app-insights-asp-net.md) o [installare AI Status Monitor nel server](app-insights-monitor-performance-live-website-now.md) (o scrivere codice personalizzato troppo[tenere traccia delle dipendenze](app-insights-api-custom-events-metrics.md#trackdependency)) |Rilevare i problemi di prestazioni |
| Telemetria di dipendenza |[Installare Status Monitor di Application Insights nel server](app-insights-monitor-performance-live-website-now.md) |Diagnosticare i problemi relativi a database o altri componenti esterni |
| Ricavare analisi dello stack dalle eccezioni |[Inserire chiamate TrackException nel codice](app-insights-asp-net-exceptions.md) (ma alcune sono segnalate automaticamente) |Rilevare e diagnosticare le eccezioni |
| Eseguire la ricerca di tracce dei log |[Aggiungere un adattatore di registrazione](app-insights-asp-net-trace-logs.md) |Diagnosticare le eccezioni, problemi di prestazioni |
| Nozioni di base dell'utilizzo del client: visualizzazioni pagina, sessioni, ... |[Inizializzatore JavaScript nelle pagine Web](app-insights-javascript.md) |Analisi dell'utilizzo |
| Metriche personalizzate client |[Rilevamento delle chiamate nelle pagine Web](app-insights-api-custom-events-metrics.md) |Migliorare l'esperienza utente |
| Metriche personalizzate server |[Rilevamento delle chiamate nel server](app-insights-api-custom-events-metrics.md) |Business intelligence |

## <a name="why-are-hello-counts-in-search-and-metrics-charts-unequal"></a>Perché sono hello conta nei grafici di ricerca e metriche diverso?

[Campionamento](app-insights-sampling.md) riduce il numero di hello di elementi di dati di telemetria (richieste, gli eventi personalizzati e così via) che vengono effettivamente inviato dal portale toohello app. Nella ricerca, si visualizza il numero di hello di elementi effettivamente ricevuto. Nei grafici di metriche che consentono di visualizzare un conteggio di eventi, si visualizza il numero di hello di originali eventi che si è verificato. 

Ogni elemento trasmesso include una proprietà `itemCount` che visualizza quanti eventi originali rappresenta tale elemento. tooobserve campionamento nell'operazione, è possibile eseguire questa query in Analitica:

```
    requests | summarize original_events = sum(itemCount), transmitted_events = count()
```


## <a name="automation"></a>Automazione

### <a name="configuring-application-insights"></a>Configurazione di Application Insights

È possibile [scrivere script di PowerShell](app-insights-powershell.md) tramite Monitoraggio risorse di Azure per:

* Creare e aggiornare risorse di Application Insights.
* Impostare hello prezzi piano.
* Ottenere la chiave di strumentazione hello.
* Aggiungere un avviso di metrica.
* Aggiungere un test di disponibilità.

Non è possibile impostare un report di esplorazione delle metriche o impostare un'esportazione continua.

### <a name="querying-hello-telemetry"></a>Esecuzione di query su dati di telemetria hello

Hello utilizzare [API REST](https://dev.applicationinsights.io/) toorun [Analitica](app-insights-analytics.md) query.

## <a name="how-can-i-set-an-alert-on-an-event"></a>Come è possibile impostare un avviso per un evento?

Gli avvisi di Azure si applicano solo alle metriche. Creare una metrica personalizzata che supera una soglia di valori ogni volta che si verifica l'evento. Impostare quindi un avviso per la metrica hello. Si noti che: si riceverà una notifica ogni volta che metrica hello supera la soglia hello in entrambe le direzioni; non si otterrà una notifica fino al primo passaggio, indipendentemente dal valore iniziale di hello sia alta o bassa; hello è sempre una latenza di pochi minuti.

## <a name="are-there-data-transfer-charges-between-an-azure-web-app-and-application-insights"></a>Ci sono costi per il trasferimento dati tra un'app Web di Azure e Application Insights?

* Se l'app Web di Azure è ospitata in un data center in cui è presente un endpoint di raccolta di Application Insights, non è previsto alcun addebito. 
* Se non c'è nessun endpoint nel data center host, la telemetria dell'app sarà soggetta agli [addebiti in uscita di Azure](https://azure.microsoft.com/pricing/details/bandwidth/).

Ciò non dipende da dove è ospitata la risorsa di Application Insights. Solo dipende dalla distribuzione hello di questo endpoint.

## <a name="can-i-send-telemetry-toohello-application-insights-portal"></a>È possibile inviare portale Application Insights toohello di telemetria?

È consigliabile usare il SDK e di usare hello API SDK (app-insights-api-custom-events-metrics.md). Sono disponibili scenari di hello SDK per vari [piattaforme](app-insights-platforms.md). Gli SDK gestiscono bufferring, compressione, limitazione, tentativi e così via. Tuttavia, hello [dello schema di inserimento](https://github.com/Microsoft/ApplicationInsights-dotnet/tree/develop/Schema/PublicSchema) e [protocollo dell'endpoint](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/EndpointSpecs/ENDPOINT-PROTOCOL.md) sono pubblici.

## <a name="can-i-monitor-an-intranet-web-server"></a>È possibile monitorare un server Web Intranet?

Di seguito vengono illustrati due metodi:

### <a name="firewall-door"></a>Porta firewall

Consenti il web server toosend telemetria tooour endpoint https://dc.services.visualstudio.com:443 e https://rt.services.visualstudio.com:443. 

### <a name="proxy"></a>Proxy

Instradare il traffico dal gateway della rete intranet, per impostare questa proprietà in Applicationinsights tooa server:

```XML
<TelemetryChannel>
    <EndpointAddress>your gateway endpoint</EndpointAddress>
</TelemetryChannel>
```

Il gateway deve indirizzare toohttps://dc.services.visualstudio.com:443/v2/traccia il traffico di hello

## <a name="can-i-run-availability-web-tests-on-an-intranet-server"></a>È possibile eseguire test Web di disponibilità in un server Intranet?

Il nostro [test web](app-insights-monitor-web-app-availability.md) eseguiti nei punti di presenza che vengono distribuiti in tutto il mondo hello. Sono disponibili due soluzioni:

* Porta del firewall: Consenti richieste server tooyour da [hello lungo ed elenco modificabile di web gli agenti di test](app-insights-ip-addresses.md).
* Scrivere il proprio codice toosend richieste periodiche tooyour server all'interno della rete intranet. A tale scopo è anche possibile eseguire test Web di Visual Studio. tester Hello Impossibile inviare i risultati di hello Insights tooApplication utilizzando hello TrackAvailability() API.

## <a name="more-answers"></a>Altre risposte
* [Forum di Application Insights](https://social.msdn.microsoft.com/Forums/vstudio/en-US/home?forum=ApplicationInsights)

<!--Link references-->

[data]: app-insights-data-retention-privacy.md
[platforms]: app-insights-platforms.md
[start]: app-insights-overview.md
[windows]: app-insights-windows-get-started.md
