---
title: aaaHow posso... in Azure Application Insights | Documenti Microsoft
description: Domande frequenti in Application Insights
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 48b2b644-92e4-44c3-bc14-068f1bbedd22
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: bwren
ms.openlocfilehash: 89294c3583b7c4e7998143be6d359f2deb3c8f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-i--in-application-insights"></a>Cosa fare in Application Insights?
## <a name="get-an-email-when-"></a>Per ricevere un messaggio di posta elettronica quando...
### <a name="email-if-my-site-goes-down"></a>Inviare un messaggio di posta elettronica se il sito non è disponibile
Impostare un [test web di disponibilità](app-insights-monitor-web-app-availability.md).

### <a name="email-if-my-site-is-overloaded"></a>Inviare un messaggio di posta elettronica se il sito è sovraccarico
Impostare un [avviso](app-insights-alerts.md) per il **tempo di risposta del server**. Una soglia compresa tra 1 e 2 secondi dovrebbe risolvere il problema.

![](./media/app-insights-how-do-i/030-server.png)

L'applicazione potrebbe inoltre dare segni di difficoltà tramite la restituzione di codici di errore. Impostare un avviso per le **richieste non riuscite**.

Se si desidera un avviso tooset **eccezioni Server**, potrebbe essere toodo [alcune impostazioni aggiuntive](app-insights-asp-net-exceptions.md) dati toosee degli ordini.

### <a name="email-on-exceptions"></a>Inviare un messaggio di posta elettronica in caso di eccezioni
1. [Configurare il monitoraggio delle eccezioni](app-insights-asp-net-exceptions.md)
2. [Impostare un avviso](app-insights-alerts.md) su hello eccezione conteggio metrica

### <a name="email-on-an-event-in-my-app"></a>Inviare un messaggio di posta elettronica per un evento generato dall'app
Si supponga che desideri tooget un messaggio di posta elettronica quando si verifica un evento specifico. Application Insights non fornisce direttamente questa funzionalità, ma è possibile [inviare un avviso quando una metrica supera una soglia](app-insights-alerts.md).

Gli avvisi possono essere impostati per [metriche personalizzate](app-insights-api-custom-events-metrics.md#trackmetric), anche se non per gli eventi personalizzati. Scrivere alcuni tooincrease codice una metrica, quando si verifica l'evento hello:

    telemetry.TrackMetric("Alarm", 10);

oppure:

    var measurements = new Dictionary<string,double>();
    measurements ["Alarm"] = 10;
    telemetry.TrackEvent("status", null, measurements);

Poiché gli avvisi hanno due stati, occorre toosend un valore basso quando si considera l'avviso hello toohave terminato:

    telemetry.TrackMetric("Alarm", 0.5);

Creare un grafico in [Esplora metrica](app-insights-metrics-explorer.md) toosee l'allarme:

![](./media/app-insights-how-do-i/010-alarm.png)

Impostare ora toofire un avviso quando la metrica hello supera un valore medio per un breve periodo:

![](./media/app-insights-how-do-i/020-threshold.png)

Impostare hello toohello periodo minimo di una Media.

Messaggi di posta elettronica viene visualizzato quando la metrica hello supera il numero sia inferiore alla soglia hello.

Tooconsider alcuni punti:

* Un avviso dispone di due stati: "Avviso" e "Integro". stato Hello viene valutato solo quando viene ricevuta una metrica.
* Un messaggio di posta elettronica viene inviato solo quando cambia lo stato di hello. È per questo motivo è toosend metriche sia alte e basso valore.
* avviso hello tooevaluate, Media hello viene eseguito di valori hello ricevuto su hello precedente. Ciò si verifica ogni volta che viene ricevuta una metrica, in modo da messaggi di posta elettronica possono essere inviati più frequentemente rispetto al periodo di hello che è impostato.
* Poiché i messaggi di posta elettronica vengono inviati "avviso" e "Integro", è opportuno tooconsider pensiero nuovamente l'evento monofase come una condizione di due stati. Ad esempio, anziché un evento "processo completato", avere una condizione "processo in corso", in cui si ricevono messaggi di posta elettronica nella hello iniziale e finale di un processo.

### <a name="set-up-alerts-automatically"></a>Impostare automaticamente gli avvisi
[Utilizzare PowerShell toocreate nuovi avvisi](app-insights-alerts.md#automation)

## <a name="use-powershell-toomanage-application-insights"></a>Usare PowerShell tooManage Application Insights
* [Creare nuove risorse](app-insights-powershell-script-create-resource.md)
* [Creare nuovi avvisi](app-insights-alerts.md#automation)

## <a name="separate-telemetry-from-different-versions"></a>Separare la telemetria da diverse versioni

* Più ruoli in un'app: usare una singola risorsa di Application Insights e filtrare su cloud_Rolename. [Altre informazioni](app-insights-monitor-multi-role-apps.md)
* Separazione di sviluppo, test e versioni di rilascio: usare diverse risorse di Application Insights. Selezionare le chiavi di strumentazione hello da Web. config. [Altre informazioni](app-insights-separate-resources.md)
* Creazione di rapporti sulle versioni di compilazione: aggiungere una proprietà usando un inizializzatore di telemetria. [Altre informazioni](app-insights-separate-resources.md)

## <a name="monitor-backend-servers-and-desktop-apps"></a>Monitorare i server back-end e le app desktop
[Modulo di Windows Server SDK hello utilizzare](app-insights-windows-desktop.md).

## <a name="visualize-data"></a>Visualizzare i dati
#### <a name="dashboard-with-metrics-from-multiple-apps"></a>Dashboard con metriche da più app
* In [Esplora metriche](app-insights-metrics-explorer.md)personalizzare il grafico e salvarlo come preferito. Aggiungerlo toohello dashboard di Azure.

#### <a name="dashboard-with-data-from-other-sources-and-application-insights"></a>Dashboard con dati provenienti da altre fonti e Application Insights
* [Esportare i dati di telemetria tooPower BI](app-insights-export-power-bi.md).

Or

* Usare SharePoint come dashboard, dove i dati vengono visualizzati in Web part di SharePoint. [Utilizzare l'esportazione continua e Analitica flusso tooexport tooSQL](app-insights-code-sample-export-sql-stream-analytics.md).  Utilizzare PowerView tooexamine hello database e creare una web part di SharePoint per PowerView.

<a name="search-specific-users"></a>

### <a name="filter-out-anonymous-or-authenticated-users"></a>Filtrare gli utenti anonimi o autenticati
Se gli utenti ad accedere, è possibile impostare hello [id utente autenticato](app-insights-api-custom-events-metrics.md#authenticated-users). Questa operazione non viene eseguita automaticamente.

È quindi possibile:

* Eseguire ricerche in base a ID utente specifici

![](./media/app-insights-how-do-i/110-search.png)

* Filtrare gli utenti anonimi e autenticati tooeither metriche

![](./media/app-insights-how-do-i/115-metrics.png)

## <a name="modify-property-names-or-values"></a>Modificare i nomi della proprietà o i valori
Creare un [filtro](app-insights-api-filtering-sampling.md#filtering). Ciò consente di modificare o filtrare i dati di telemetria prima che venga inviato dal tooApplication app Insights.

## <a name="list-specific-users-and-their-usage"></a>Elencare utenti specifici e il relativo uso
Se si desidera troppo[cercare utenti specifici](#search-specific-users), è possibile impostare hello [id utente autenticato](app-insights-api-custom-events-metrics.md#authenticated-users).

Se si desidera un elenco di utenti con i dati quali, ad esempio, le pagine visualizzate o la frequenza di accesso, sono disponibili due opzioni:

* [Id dell'utente autenticato insieme](app-insights-api-custom-events-metrics.md#authenticated-users), [esportare database tooa](app-insights-code-sample-export-sql-stream-analytics.md) e utilizzare adatto strumenti tooanalyze sono i dati utente.
* Se si dispone solo di un numero ridotto di utenti, è possibile inviare eventi personalizzati o metriche, usando i dati di hello di interesse come hello valore metrico o nome dell'evento e l'id utente hello impostazione come proprietà. visualizzazioni di pagina tooanalyze, sostituire hello standard JavaScript trackPageView chiamata. dati di telemetria di tooanalyze sul lato server, utilizzare una telemetria inizializzatore tooadd hello utente id tooall telemetria server. È quindi possibile metriche di filtro e di segmento e ricerche basate sull'id utente hello.

## <a name="reduce-traffic-from-my-app-tooapplication-insights"></a>Ridurre il traffico da my tooApplication app Insights
* In [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md), disabilitare tutti i moduli non è necessario, tale agente di raccolta hello contatore delle prestazioni.
* Utilizzare [campionamento e il filtraggio](app-insights-api-filtering-sampling.md) in hello SDK.
* Nelle pagine web, limitare il numero di hello di chiamate Ajax segnalati per ogni pagina. Nel frammento di script hello dopo `instrumentationKey:...` , inserire: `,maxAjaxCallsPerView:3` (o un numero).
* Se si utilizza [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), calcolo di aggregazione hello di batch di valori della metrica prima di inviare i risultati di hello. Un overload di TrackMetric() esegue questa operazione.

Altre informazioni su [prezzi e quote](app-insights-pricing.md).

## <a name="disable-telemetry"></a>Disabilitare telemetria
troppo**dinamicamente arrestare e avviare** hello raccolta e la trasmissione di dati di telemetria da server hello:

```

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```



troppo**disabilitare gli agenti di raccolta standard selezionati** : ad esempio, i contatori delle prestazioni, le richieste HTTP o dipendenze, eliminare o impostare come commento le righe rilevanti hello in [Applicationinsights](app-insights-api-custom-events-metrics.md). È possibile farlo, ad esempio, se si desidera toosend TrackRequest dati personalizzati.

## <a name="view-system-performance-counters"></a>Visualizzare i contatori delle prestazioni di sistema
Tra hello metriche è possibile visualizzare in Esplora metriche sono un set di contatori delle prestazioni di sistema. Esiste un pannello predefinito denominato **Server** in cui sono visualizzati alcuni set.

![Aprire la risorsa Application Insights e fare clic su Server.](./media/app-insights-how-do-i/121-servers.png)

### <a name="if-you-see-no-performance-counter-data"></a>Se non vengono visualizzati dati dei contatori delle prestazioni
* **Server IIS** sul proprio computer o in una macchina virtuale. [Installare Status Monitor](app-insights-monitor-performance-live-website-now.md).
* **Sito Web di Azure** - i contatori delle prestazioni non sono ancora supportati. Esistono alcune metriche è possibile ottenere come una parte standard del Pannello di controllo sito web di Azure hello.
* **Server Unix** - [Installare collectd](app-insights-java-collectd.md)

### <a name="toodisplay-more-performance-counters"></a>toodisplay più contatori delle prestazioni
* Prima di tutto, [aggiungere un nuovo grafico](app-insights-metrics-explorer.md) e visualizzare se il contatore hello in hello base impostato da offrire.
* In caso contrario, [aggiungere hello contatore toohello set raccolti dal modulo del contatore delle prestazioni hello](app-insights-performance-counters.md).
