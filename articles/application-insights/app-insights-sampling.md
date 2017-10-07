---
title: campionamento aaaTelemetry in Azure Application Insights | Documenti Microsoft
description: Tookeep hello come volume di dati di telemetria nel controllo.
services: application-insights
documentationcenter: windows
author: vgorbenko
manager: carmonm
ms.assetid: 015ab744-d514-42c0-8553-8410eef00368
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bwren
ms.openlocfilehash: e19c350d0a5f16736c100322a9922fcfbf5d7b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sampling-in-application-insights"></a>Campionamento in Application Insights


Il campionamento è una funzionalità di [Azure Application Insights](app-insights-overview.md). È il traffico dati di telemetria in senso tooreduce e archiviazione, hello consigliati mantenendo una corretta analisi dei dati dell'applicazione. filtro Hello seleziona gli elementi correlati, in modo che è possibile spostarsi tra gli elementi quando si esegue l'analisi diagnostica.
Quando i conteggi di metrica vengono presentati tooyou nel portale di hello, essi vengono rinormalizzati account tootake di campionamento, toominimize qualsiasi effetto sulle statistiche di hello hello.

Il campionamento riduce i costi del traffico e dei dati e consente di evitare la limitazione.

## <a name="in-brief"></a>In breve:
* Campionamento mantiene 1 in  *n*  registra ed Elimina rest hello. Ad esempio, potrebbe mantenere 1 un evento su 5, corrispondente a una frequenza di campionamento del 20%. 
* Nelle app server Web ASP.NET, il campionamento viene eseguito automaticamente se l'applicazione invia molti dati di telemetria.
* È inoltre possibile impostare manualmente, campionamento entrambi hello in portale su hello dei prezzi di pagina. oppure in hello SDK ASP.NET nel file config hello, tooalso ridurre il traffico di rete hello.
* Se si accede a eventi personalizzati e si desidera toomake assicurarsi che un set di eventi viene mantenuto o eliminato insieme, assicurarsi che essi hanno hello stesso valore di ID operazione.
* divisore di campionamento Hello  *n*  viene segnalato in ogni record nella proprietà hello `itemCount`, che nella ricerca viene visualizzata sotto hello nome descrittivo "numero di richieste" o "conteggio eventi". Quando il campionamento non è in esecuzione, `itemCount==1`.
* Se si scrivono query di Dati di analisi, è necessario [tener conto del campionamento](app-insights-analytics-tour.md#counting-sampled-data). In particolare, anziché eseguire semplicemente il conteggio dei record, è necessario usare `summarize sum(itemCount)`.

## <a name="types-of-sampling"></a>Tipi di campionamento
Esistono tre diversi metodi di campionamento:

* **Campionamento adattivo** regola automaticamente il volume di hello di telemetria inviato da hello SDK nell'applicazione ASP.NET. Si tratta di un'opzione predefinita dell'SDK versione 2.0.0-beta3. Attualmente disponibile solo per la telemetria lato server di ASP.NET. 
* **Campionamento tasso fisso** ridurre hello volume di dati di telemetria inviati da entrambi i server ASP.NET e i browser degli utenti. Impostare la frequenza di hello. Hello client e server eseguirà la sincronizzazione loro campionamento in modo che, nella ricerca, è possibile spostarsi tra le visualizzazioni pagina correlati e richieste.
* **Campionamento inserimento** funziona in hello portale di Azure. Vengono rimossi alcuni dei dati di telemetria hello in arrivo dall'app, a una velocità è impostata. Non riduce il traffico di telemetria, ma consente all'utente di rispettare la quota mensile. Hello grande vantaggio offerto dal campionamento di inserimento è che è possibile impostarlo senza ridistribuire l'applicazione e funziona in modo uniforme per tutti i server e client. 

Se è in esecuzione il campionamento adattivo o a frequenza fissa, il campionamento per inserimento è disabilitato.

## <a name="ingestion-sampling"></a>Campionamento per inserimento
Questo modulo di campionamento opera a punto hello in dati di telemetria hello dal server web, browser e dispositivi raggiunge l'endpoint del servizio Application Insights hello. Anche se non ridurre il traffico di dati di telemetria hello inviato dall'app, riduce la quantità hello elaborati e mantenuti (e addebitato) da Application Insights.

Se l'app passa spesso superamento della quota mensile e non è necessario scegliere hello di utilizzare uno dei tipi di base SDK hello di campionamento, utilizzare questo tipo di campionamento. 

Impostare la frequenza di campionamento hello in hello quote e prezzi pannello:

![Dal pannello della panoramica applicazione hello, fare clic su impostazioni di Quota, esempi, quindi selezionare una frequenza di campionamento e fare clic su Aggiorna.](./media/app-insights-sampling/04.png)

Gli altri tipi di campionamento di algoritmo hello mantiene gli elementi di dati di telemetria correlati. Ad esempio, quando si sta controllando telemetria hello nella ricerca, sarà possibile richiesta hello toofind correlati tooa particolare eccezione. I conteggi di metrica, ad esempio la frequenza delle richieste e delle eccezioni, vengono mantenuti correttamente.

I punti dati che vengono rimossi dal campionamento non sono disponibili in alcuna funzionalità di Application Insights, ad esempio nell' [esportazione continua](app-insights-export-telemetry.md).

Il campionamento per inserimento non funziona mentre è attivo il campionamento a frequenza fissa o adattivo basato sull'SDK. Se la frequenza di campionamento hello in hello SDK è inferiore al 100%, quindi hello frequenza di campionamento inserimento impostate viene ignorato.

> [!WARNING]
> valore Hello visualizzato sul riquadro hello indica i valori hello impostati per il campionamento di inserimento. Non ha una frequenza di campionamento effettivo hello se campionamento SDK è in esecuzione.
> 
> 

## <a name="adaptive-sampling-at-your-web-server"></a>Campionamento adattivo nel server Web
Campionamento adattivo è disponibile per hello Application Insights SDK per ASP.NET v 2.0.0-beta3 e versioni successive ed è abilitato per impostazione predefinita. 

Campionamento adattivo influisce sul volume hello di telemetria inviato da toohello di app del server web del servizio Application Insights. Hello volume viene regolato automaticamente tookeep all'interno di una frequenza massima specificata del traffico.

Non opera a bassi volumi di dati di telemetria, pertanto un'app per eseguire il debug o un sito Web con un basso utilizzo non saranno interessate.

volume di destinazione hello tooachieve, alcuni dei dati di telemetria hello generato viene eliminato. Ma gli altri tipi di campionamento di algoritmo hello mantiene gli elementi di dati di telemetria correlati. Ad esempio, quando si sta controllando telemetria hello nella ricerca, sarà possibile richiesta hello toofind correlati tooa particolare eccezione. 

Consente di contare metrica, ad esempio tasso di richiesta e il tasso di eccezione sono toocompensate adattata per hello, frequenza di campionamento in modo che siano visualizzati valori circa corretti in Esplora metriche.

**Aggiornamento NuGet del progetto** pacchetti toohello più recente *pre-release* versione di Application Insights: fare clic sul progetto hello in Esplora soluzioni, scegliere Gestisci pacchetti NuGet controllare **inclusione versione non definitiva** e cercare Microsoft.ApplicationInsights.Web. 

In [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md), è possibile modificare vari parametri in hello `AdaptiveSamplingTelemetryProcessor` nodo. cifre Hello indicate sono valori predefiniti di hello:

* `<MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>`
  
    Hello velocità di destinazione che hello algoritmo adattivo ha come obiettivo **in ogni host server**. Se l'app web viene eseguito il numero di host, è possibile ridurre in modo da tooremain entro la frequenza di destinazione del traffico nel portale Application Insights hello questo valore.
* `<EvaluationInterval>00:00:15</EvaluationInterval>` 
  
    intervallo di Hello in cui hello viene rivalutato quantità attuale di telemetria. La valutazione viene eseguita come media mobile. È possibile tooshorten questo intervallo se i dati di telemetria è ritenuta toosudden picchi.
* `<SamplingPercentageDecreaseTimeout>00:02:00</SamplingPercentageDecreaseTimeout>`
  
    Quando le modifiche valore percentuale di campionamento, dopo quanto tempo dopo che sono è consentito il campionamento percentuale nuovamente toolower toocapture meno dati.
* `<SamplingPercentageIncreaseTimeout>00:15:00</SamplingPercentageIncreaseTimeout>`
  
    Quando le modifiche valore percentuale di campionamento, dopo quanto tempo dopo che sono è consentito il campionamento percentuale nuovamente tooincrease toocapture più dati.
* `<MinSamplingPercentage>0.1</MinSamplingPercentage>`
  
    Campionamento percentuale in base alla variazione, che cos'è il valore minimo di hello ci stiamo consentiti tooset.
* `<MaxSamplingPercentage>100.0</MaxSamplingPercentage>`
  
    Campionamento percentuale in base alla variazione, che cos'è il valore massimo di hello ci stiamo consentiti tooset.
* `<MovingAverageRatio>0.25</MovingAverageRatio>` 
  
    Nel calcolo della media mobile hello hello peso hello assegnato toohello il valore più recente. Utilizzare un tooor uguale valore minore di 1. I valori minori modificare algoritmo hello meno reattivi toosudden.
* `<InitialSamplingPercentage>100</InitialSamplingPercentage>`
  
    valore di Hello assegnato quando l'applicazione hello ha iniziato. Non ridurlo durante il debug. 

* `<ExcludedTypes>Trace;Exception</ExcludedTypes>`
  
    Elenco di tipi che non si desidera toobe campionate delimitate da un punto e virgola. I tipi riconosciuti sono: dipendenza, evento, eccezione, pageview, richiesta, traccia. Tutte le istanze di hello specificato vengono trasmessi tipi; tipi di Hello non specificati vengono campionati.

* `<IncludedTypes>Request;Dependency</IncludedTypes>`
  
    Elenco di tipi che si desidera toobe campionate delimitate da un punto e virgola. I tipi riconosciuti sono: dipendenza, evento, eccezione, pageview, richiesta, traccia. Hello specificato vengono campionati tipi; tutte le istanze di hello sempre da trasmettere altri tipi.


**tooswitch off** campionamento adattivo, Rimuovi hello AdaptiveSamplingTelemetryProcessor nodo dalla configurazione di applicationinsights.

### <a name="alternative-configure-adaptive-sampling-in-code"></a>Alternativa: configurare il campionamento adattivo nel codice
Anziché regolare campionamento nel file hello. config, è possibile utilizzare codice. In questo modo è una funzione di callback che viene richiamata ogni volta che la frequenza di campionamento hello viene rivalutata toospecify. Si può usare, ad esempio, viene utilizzato toofind out la frequenza di campionamento.

Rimuovere hello `AdaptiveSamplingTelemetryProcessor` nodo da file hello. config.

*C#*

```C#

    using Microsoft.ApplicationInsights;
    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.Channel.Implementation;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var adaptiveSamplingSettings = new SamplingPercentageEstimatorSettings();

    // Optional: here you can adjust hello settings from their defaults.

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;

    builder.UseAdaptiveSampling(
         adaptiveSamplingSettings,

        // Callback on rate re-evaluation:
        (double afterSamplingTelemetryItemRatePerSecond,
         double currentSamplingPercentage,
         double newSamplingPercentage,
         bool isSamplingPercentageChanged,
         SamplingPercentageEstimatorSettings s
        ) =>
        {
          if (isSamplingPercentageChanged)
          {
             // Report hello sampling rate.
             telemetryClient.TrackMetric("samplingPercentage", newSamplingPercentage);
          }
      });

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

([Informazioni sui processori di telemetria](app-insights-api-filtering-sampling.md#filtering).)

<a name="other-web-pages"></a>

## <a name="sampling-for-web-pages-with-javascript"></a>Campionamento per pagine Web con JavaScript
È possibile configurare le pagine Web per il campionamento a frequenza fissa da qualsiasi server. 

Quando si [configurare le pagine web hello per Application Insights](app-insights-javascript.md), modificare il frammento hello che vengono recuperate dal portale Application Insights hello. (In applicazioni ASP.NET, frammento di codice hello in genere viene inserito in layout. cshtml.)  Inserire una riga simile `samplingPercentage: 10,` prima chiave di strumentazione hello:

    <script>
    var appInsights= ... 
    }({ 


    // Value must be 100/N where N is an integer.
    // Valid examples: 50, 25, 20, 10, 5, 1, 0.1, ...
    samplingPercentage: 10, 

    instrumentationKey:...
    }); 

    window.appInsights=appInsights; 
    appInsights.trackPageView(); 
    </script> 

Per percentuale di campionamento hello, scegliere una percentuale Chiudi too100/N dove N è un numero intero.  Il campionamento attualmente non supporta altri valori.

È inoltre possibile abilitare il campionamento tasso fisso nel server di hello, server e client hello verranno sincronizzate in modo che, nella ricerca, è possibile spostarsi tra le visualizzazioni pagina correlati e richieste.

## <a name="fixed-rate-sampling-for-aspnet-web-sites"></a>Campionamento a frequenza fissa per siti Web ASP.NET
Tasso fisso campionamento riduce il traffico di hello inviato dal server web e i browser web. A differenza del campionamento adattivo, riduce i dati di telemetria a una frequenza fissa definita dall'utente. Sincronizza inoltre hello client e il campionamento di server in modo che vengono mantenuti gli elementi correlati, ad esempio, in modo che se si esamina una visualizzazione di pagina nella ricerca, è possibile trovare la richiesta correlata.

algoritmo di campionamento Hello mantiene gli elementi correlati. Per ciascun evento di richiesta HTTP, l'algoritmo e gli eventi correlati vengono eliminati o trasmessi. 

In Esplora metriche, velocità, ad esempio conteggi di richiesta e l'eccezione sono moltiplicato per toocompensate un fattore per la frequenza di campionamento di hello, in modo che siano circa corretti.

1. **Aggiornare i pacchetti NuGet del progetto** toohello più recente *definitive* versione di Application Insights. Fare clic sul progetto hello in Esplora soluzioni, scegliere Gestisci pacchetti NuGet, controllare **Includi versione preliminare** e cercare Microsoft.ApplicationInsights.Web. 
2. **Disabilitare il campionamento adattivo**: In [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md), rimuovere o impostare come commento hello `AdaptiveSamplingTelemetryProcessor` nodo.
   
    ```xml
   
    <TelemetryProcessors>
   
    <!-- Disabled adaptive sampling:
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    -->

    ```

1. **Abilita il modulo di campionamento tasso fisso hello.** Aggiungere questo frammento troppo[Applicationinsights](app-insights-configuration-with-applicationinsights-config.md):
   
    ```XML
   
    <TelemetryProcessors>
     <Add  Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
   
      <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
      <SamplingPercentage>10</SamplingPercentage>
      </Add>
    </TelemetryProcessors>
   
    ```

> [!NOTE]
> Per percentuale di campionamento hello, scegliere una percentuale Chiudi too100/N dove N è un numero intero.  Il campionamento attualmente non supporta altri valori.
> 
> 

### <a name="alternative-enable-fixed-rate-sampling-in-your-server-code"></a>Alternativa: abilitare il campionamento a frequenza fissa nel codice del server locale
Anziché impostare il parametro di campionamento hello nel file hello. config, è possibile utilizzare codice. 

*C#*

```C#

    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var builder = TelemetryConfiguration.Active.GetTelemetryProcessorChainBuilder();
    builder.UseSampling(10.0); // percentage

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

([Informazioni sui processori di telemetria](app-insights-api-filtering-sampling.md#filtering).)

## <a name="when-toouse-sampling"></a>Quando il campionamento toouse?
Campionamento adattivo è abilitato automaticamente se si utilizza hello 2.0.0-beta3 versione ASP.NET SDK o versione successiva. Nel server Microsoft è possibile usare il campionamento per inserimento indipendentemente dalla versione dell'SDK in uso.

Per la maggior parte delle applicazioni di piccole e medie dimensioni, il campionamento non è necessario. raccogliendo i dati in tutte le attività utente si ottengono informazioni di diagnostica utili Hello e statistiche più accurate. 

vantaggi principali di Hello di campionamento sono:

* Il servizio Application Insights rimuove ("limita") i punti dati quando l'app invia una frequenza di telemetria molto elevata in un breve intervallo di tempo. 
* tookeep all'interno di hello [quota](app-insights-pricing.md) di punti dati per il piano tariffario. 
* traffico di rete tooreduce dalla raccolta hello di telemetria. 

### <a name="which-type-of-sampling-should-i-use"></a>Quale tipo di campionamento è opportuno usare?
**Usare il campionamento per inserimento se:**

* Si supera spesso la quota mensile dei dati di telemetria.
* Si utilizza una versione di hello SDK che non supporta il campionamento - ad esempio, hello SDK per Java o nelle versioni ASP.NET precedenti a 2.
* Si ricevono grandi quantità di dati di telemetria dal Web browser degli utenti.

**Usare il campionamento a frequenza fissa se:**

* Si usa hello Application Insights SDK per la versione di servizi web ASP.NET 2.0.0 o versioni successive, e
* Si desidera campionamento sincronizzato tra client e server, in modo che, quando si sta verificando gli eventi in [ricerca](app-insights-diagnostic-search.md), è possibile spostarsi tra gli eventi correlati nel client hello e server, ad esempio le visualizzazioni di pagina e le richieste http.
* Si è certi della percentuale di hello campionamento appropriato per l'app. Deve essere sufficientemente alto tooget metriche precise, ma di seguito hello frequenza che supera la quota di determinazione dei prezzi e hello limitazioni. 

**Usare il campionamento adattivo:**

In caso contrario, è consigliabile il campionamento adattivo. Questa opzione è abilitata per impostazione predefinita nel server ASP.NET hello SDK, versione 2.0.0-beta3 o versione successiva. Non riduce il traffico fino a una determinata frequenza minima, in modo da non avere effetto su un sito poco usato.

## <a name="how-do-i-know-whether-sampling-is-in-operation"></a>Come è possibile sapere se il campionamento è in esecuzione?
hello toodiscover effettivo campionamento frequenza indipendentemente da dove è stato applicato, usare un [query Analitica](app-insights-analytics.md) simile al seguente:

    requests | where timestamp > ago(1d)
    | summarize 100/avg(itemCount) by bin(timestamp, 1h) 
    | render areachart 

In ogni mantenuti record, `itemCount` indica il numero di hello di record originali che esso rappresenta, too1 uguale + il numero di hello di record scartati precedente. 

## <a name="how-does-sampling-work"></a>Come funziona il campionamento?
Tasso fisso e campionamento adattivo sono una funzionalità di hello SDK nelle versioni ASP.NET da partire 2.0.0. Campionamento di inserimento è una funzionalità del servizio di Application Insights hello e può essere attivo se hello SDK non sta eseguendo il campionamento. 

algoritmo di campionamento Hello decide quali toodrop di elementi di dati di telemetria e quali tookeep quelli (se è in hello SDK o nel servizio di Application Insights hello). decisione di campionamento Hello è basata su diverse regole finalizzate toopreserve tutti i punti dati correlati tra loro intatto, gestione di un'esperienza di diagnostica in Application Insights affidabile anche con un set di dati ridotto e utilizzabili. Se, ad esempio, per una richiesta non riuscita l'app invia elementi di telemetria aggiuntivi (come eccezioni e tracce registrate da questa richiesta), il campionamento non dividerà la richiesta e il resto della telemetria, ma conserverà o rimuoverà gli elementi tutti insieme. Di conseguenza, quando si esamina i dettagli della richiesta hello in Application Insights, è possibile visualizzare sempre richiesta hello insieme ai relativi elementi di telemetria associati. 

Per le applicazioni che definiscono "user" (ovvero, applicazioni web più comuni), decisione di campionamento hello è basata su hash hello dell'id utente di hello, che significa che tutti i dati di telemetria per un determinato utente è mantenuta o eliminata. Per i tipi di applicazioni che non definiscono gli utenti (ad esempio servizi web) hello decisione di campionamento hello è basata su id operazione hello della richiesta di hello. Infine, per gli elementi di dati di telemetria hello che non dispongono di id utente né operazione impostato (ad esempio elementi di dati di telemetria segnalati dal thread asincroni senza alcun contesto http) campionamento acquisisce semplicemente una percentuale di elementi di dati di telemetria di ogni tipo. 

Per la presentazione di dati di telemetria indietro tooyou hello Application Insights servizio regola metriche hello da hello stessa percentuale di campionamento che è stato utilizzato in fase di hello della raccolta, toocompensate per hello punti dati mancanti. Di conseguenza, quando si esaminano i dati di telemetria hello in Application Insights, gli utenti di hello sono quelli statisticamente corretto delle approssimazioni di numeri reali toohello molto simile.

accuratezza Hello di approssimazione hello dipende in larga misura dalla percentuale di campionamento hello configurato. Inoltre, l'accuratezza di hello aumenta per le applicazioni che gestiscono un volume elevato di richieste simili in genere da un numero elevato di utenti. In hello invece, per le applicazioni che non funzionano con un carico significativo, campionamento non è necessaria perché queste applicazioni possono inviare in genere tutti i relativi dati di telemetria rimanendo entro la quota di hello, senza perdita di dati dalla limitazione delle richieste. 

Si noti che Application Insights non di esempio i tipi di dati di telemetria metriche e le sessioni, poiché per questi tipi di riduzione della precisione hello può risultare estremamente indesiderata. 

### <a name="adaptive-sampling"></a>Campionamento adattivo
Campionamento adattivo aggiunge un componente di tale monitor hello velocità di trasmissione corrente dal hello SDK e modifica hello campionamento percentuale tootry toostay all'interno di velocità massima di hello destinazione. regolazione Hello viene ricalcolata a intervalli regolari e si basa su una media mobile di hello velocità di trasmissione in uscita.

## <a name="sampling-and-hello-javascript-sdk"></a>Campionamento e hello SDK per JavaScript
Hello sul lato client (JavaScript) SDK fa parte di campionamento tasso fisso in combinazione con hello sul lato server SDK. pagine Hello instrumentato invierà telemetria sul lato client da hello agli stessi utenti per la quale hello sul lato server effettuata decisione troppo "di esempio in." Questa logica è progettato toomaintain integrità della sessione utente tra lato client e server. Di conseguenza, da un particolare elemento della telemetria in Application Insights è possibile trovare tutti gli altri elementi della telemetria per questa sessione utente. 

*La telemetria lato e client e server non mostra i campioni coordinati, come descritto sopra.*

* Verificare di avere abilitato il campionamento a frequenza fissa sia sul server che sul client.
* Assicurarsi che la versione SDK hello è 2.0 o versione successiva.
* Verificare che si imposta hello stesso campionamento percentuale in hello client e server.

## <a name="frequently-asked-questions"></a>Domande frequenti
*Perché il campionamento non è una semplice "raccolta di percentuale X di ogni tipo di telemetria"?*

* Durante questo metodo di campionamento fornisce con una precisione molto elevata in approssimazioni metrica, causa l'interruzione dati di diagnostica toocorrelate possibilità per utente, sessione e la richiesta, è fondamentale per la diagnostica. Il campionamento quindi funziona meglio come logica di "raccolta di tutti gli elementi della telemetria per una percentuale X di utenti dell'app" o di "raccolta di tutta la telemetria per una percentuale X di richieste app". Per gli elementi di dati di telemetria hello non associati alle richieste di hello (ad esempio, l'elaborazione asincrona in background), hello rientrano il backup è troppo "collect X % di tutti gli elementi per ogni tipo di dati di telemetria." 

*Percentuale di campionamento hello può cambiare nel tempo?*

* Sì, adattivo campionando gradualmente la percentuale di campionamento di hello, in base a hello attualmente osservata volume di dati di telemetria hello.

*Se si utilizza il campionamento tasso fisso, come si capisce quali campionamento percentuale funzionerà hello migliore per la mia applicazione?*

* È toostart con campionamento adattivo, scoprire cosa valutarlo liquida in (vedere hello sopra domanda), e quindi commutatore toofixed-velocità di campionamento con tale tasso. 
  
    In caso contrario, è necessario tooguess. Analizzare l'utilizzo di dati di telemetria corrente nel AI, osservare qualsiasi limitazione delle richieste che è in corso e stima hello volume di dati di telemetria raccolti hello. Questi tre input, nonché il piano tariffario selezionato, è consigliabile quanto desiderato volume hello tooreduce di telemetria raccolti hello. Tuttavia, un aumento nel numero hello degli utenti o alcuni altri MAIUSC volume hello di telemetria potrebbe invalidare la stima.

*Cosa accade se si configura una percentuale di campionamento troppo bassa?*

* Percentuale di campionamento eccessivamente basso (campionamento over-aggressive) riduce accuratezza hello delle approssimazioni di hello, quando si tenta di Application Insights visualizzazione hello toocompensate dei dati di hello per riduce il volume di dati hello. Inoltre, diagnostica esperienza potrebbe influire negativamente, come alcuni dei hello raramente errori o richieste lente possono essere campionate.

*Cosa accade se si configura una percentuale di campionamento troppo alta?*

* Configurazione troppo elevato di campionamento percentuale (non aggressiva sufficientemente) comporta una riduzione insufficiente nel volume di hello di hello raccolti dati di telemetria. Possono comunque verificarsi telemetria perdita di dati correlati potrebbe essere superiore è pianificato a causa delle spese toooverage toothrottling e hello costo dell'utilizzo di Application Insights.

*Su quali piattaforme è possibile usare il campionamento?*

* Campionamento di inserimento può avvenire automaticamente per qualsiasi telemetria di sopra di un determinato volume, se non sta eseguendo il campionamento hello SDK. Questo funzionerà, ad esempio, se l'app Usa un server Java o se si utilizza una versione precedente di hello SDK di ASP.NET.
* Se si sta utilizzando versioni SDK ASP.NET 2.0.0 e versioni successive (ospitato in Azure o nel proprio server), si ottiene adattivo di campionamento per impostazione predefinita, ma è possibile passare toofixed velocità, come descritto in precedenza. Campionamento tasso fisso, il browser hello SDK consente di sincronizzare automaticamente toosample eventi correlati. 

*Esistono alcuni eventi rari voglio sempre toosee. Come è possibile ottenere tali oltre il modulo di campionamento hello?*

* Inizializza un'istanza separata di TelemetryClient con un nuovo TelemetryConfiguration (non hello Active quello predefinito). Utilizzare tale toosend gli eventi rari.

## <a name="next-steps"></a>Passaggi successivi
* [applicazione di filtri](app-insights-api-filtering-sampling.md) può garantire un controllo più rigoroso sui dati inviati dall'SDK.

