---
title: riferimento aaaApplicationInsights.config - Azure | Documenti Microsoft
description: Abilitare o disabilitare i moduli di raccolta dati e aggiungere i contatori delle prestazioni e altri parametri.
services: application-insights
documentationcenter: 
author: OlegAnaniev-MSFT
editor: alancameronwills
manager: carmonm
ms.assetid: 6e397752-c086-46e9-8648-a1196e8078c2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 76cb11349d87dfc508ec8b1c454259a0b079c48a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-hello-application-insights-sdk-with-applicationinsightsconfig-or-xml"></a>Configurazione di Application Insights SDK hello con Applicationinsights o. Xml
Hello Application Insights .NET SDK è costituito da un numero di pacchetti NuGet. Il [pacchetto core](http://www.nuget.org/packages/Microsoft.ApplicationInsights) fornisce hello API per l'invio di dati di telemetria relativi a messaggi hello Application Insights. [Altri pacchetti](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) forniscono *moduli* e *inizializzatori* di telemetria per il rilevamento automatico dei dati di telemetria dall'applicazione e dal rispettivo contesto. Modificando il file di configurazione di hello, è possibile abilitare o disabilitare inizializzatori e i moduli di telemetria e impostare i parametri per alcune di esse.

file di configurazione Hello `ApplicationInsights.config` o `ApplicationInsights.xml`, a seconda del tipo di hello dell'applicazione. Viene aggiunta automaticamente tooyour progetto quando si [installare la maggior parte delle versioni di hello SDK][start]. Viene inoltre aggiunto app web tooa da [Status Monitor in un server IIS][redfield], o quando si seleziona hello termini Insights [estensione per una macchina virtuale o un sito Web di Azure](app-insights-azure-web-apps.md).

Non è un hello toocontrol file equivalente [SDK in una pagina web][client].

Questo documento descrive le sezioni di hello che vedere nella configurazione di hello, file, come controllano componenti hello del SDK, hello e i pacchetti NuGet caricare tali componenti.

## <a name="telemetry-modules-aspnet"></a>Moduli di telemetria (ASP.NET)
Ogni modulo di telemetria raccoglie un tipo specifico di dati e le Usa core hello dati hello toosend di API. i moduli di Hello vengono installati per diversi pacchetti NuGet, aggiungere anche i file con estensione config toohello hello righe richieste.

È presente un nodo nel file di configurazione hello per ogni modulo. un modulo, toodisable Elimina nodo hello o impostarlo come commento.

### <a name="dependency-tracking"></a>Rilevamento delle dipendenze
[Rilevamento delle dipendenze](app-insights-asp-net-dependencies.md) raccoglie dati di telemetria sulle chiamate l'app invia toodatabases e i servizi esterni e database. tooallow toowork questo modulo in un server IIS, è necessario troppo[installa Status Monitor][redfield]. toouse in App web di Azure o le macchine virtuali, [selezionare l'estensione Application Insights hello](app-insights-azure-web-apps.md).

È anche possibile scrivere la propria dipendenza rilevamento codice utilizzando hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).

* `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule`
* [Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) .

### <a name="performance-collector"></a>Agente di raccolta dati delle prestazioni
[Raccoglie contatori delle prestazioni di sistema](app-insights-performance-counters.md) come CPU, memoria e rete caricate dalle istallazioni IIS. È possibile specificare quali toocollect contatori, inclusi i contatori delle prestazioni che è stato configurato manualmente.

* `Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule`
* [Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) .

### <a name="application-insights-diagnostics-telemetry"></a>Telemetria delle diagnostiche Application Insights
Hello `DiagnosticsTelemetryModule` segnala gli errori nel codice di strumentazione di Application Insights stesso hello. Ad esempio, se i contatori delle prestazioni non è possibile accedere a codice hello o un `ITelemetryInitializer` genera un'eccezione. Dati di telemetria di traccia rilevati da questo modulo viene visualizzata in hello [ricerca diagnostica][diagnostic]. Invia dati di diagnostica toodc.services.vsallin.net.

* `Microsoft.ApplicationInsights.Extensibility.Implementation.Tracing.DiagnosticsTelemetryModule`
* [Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) . Se si installa solo questo pacchetto, il file Applicationinsights config hello non viene creato automaticamente.

### <a name="developer-mode"></a>Modalità di sviluppo
`DeveloperModeWithDebuggerAttachedTelemetryModule`forza hello Application Insights `TelemetryChannel` toosend dati immediatamente, elemento dati di uno telemetria alla volta, quando un debugger è collegato toohello processo dell'applicazione. Questo riduce hello periodo di tempo tra il momento di hello quando l'applicazione tiene traccia di telemetria e quando viene visualizzato nel portale Application Insights hello. Questo causa un costo significativo per la CPU e la larghezza di banda di rete.

* `Microsoft.ApplicationInsights.WindowsServer.DeveloperModeWithDebuggerAttachedTelemetryModule`
* [Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/)

### <a name="web-request-tracking"></a>Rilevamento delle richieste web
Hello report [codice di tempo e il risultato della risposta](app-insights-asp-net.md) di richieste HTTP.

* `Microsoft.ApplicationInsights.Web.RequestTrackingTelemetryModule`
* [Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web)

### <a name="exception-tracking"></a>Rilevamento delle eccezioni
`ExceptionTrackingTelemetryModule` rileva le eccezioni non gestite nell'app Web. Vedere [Errori ed eccezioni][exceptions].

* `Microsoft.ApplicationInsights.Web.ExceptionTrackingTelemetryModule`
* [Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web)
* `Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` - rileva le [eccezioni delle attività non notate](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).
* `Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` - rileva le eccezioni non gestite per i ruoli di lavoro, servizi windows, e applicazioni della console.
* [Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) .

### <a name="eventsource-tracking"></a>Rilevamento EventSource
`EventSourceTelemetryModule`Consente di tooconfigure toobe eventi EventSource inviato tooApplication informazioni come le tracce. Per informazioni su eventi EventSource di rilevamento, vedere [Using EventSource Events](app-insights-asp-net-trace-logs.md#using-eventsource-events) (uso degli eventi EventSource).

* `Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule`
* [Microsoft.ApplicationInsights.EventSourceListener](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EventSourceListener) 

### <a name="etw-event-tracking"></a>Registrazione degli eventi ETW
`EtwCollectorTelemetryModule`consente eventi tooconfigure toobe provider ETW inviato tooApplication informazioni come le tracce. Per informazioni sul rilevamento di eventi ETW, vedere [Using ETW Events](app-insights-asp-net-trace-logs.md#using-etw-events) (Uso di eventi ETW).

* `Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule`
* [Microsoft.ApplicationInsights.EtwCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EtwCollector) 

### <a name="microsoftapplicationinsights"></a>Microsoft.ApplicationInsights
pacchetto di Microsoft. applicationinsights Hello fornisce hello [core API](https://msdn.microsoft.com/library/mt420197.aspx) di hello SDK. è anche possibile e Hello altri moduli di telemetria utilizzano questo [usarlo toodefine propria telemetria](app-insights-api-custom-events-metrics.md).

* Non ci sono voci in ApplicationInsights.config.
* [Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) . Se si installa questo NuGet, non viene generato nessun file .config.

## <a name="telemetry-channel"></a>Canale di telemetria
canale dati di telemetria Hello gestisce il buffer e la trasmissione di dati di telemetria toohello servizio Application Insights.

* `Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel`è il canale predefinito hello per i servizi. Esegue il buffering dei dati in memoria.
* `Microsoft.ApplicationInsights.PersistenceChannel` è un’alternativa per le applicazioni della console. Consente di risparmiare spazio di archiviazione toopersistent unflushed dati quando si chiude l'app e verrà inviato quando l'applicazione hello viene riavviata.

## <a name="telemetry-initializers-aspnet"></a>Inizializzatori di telemetria (ASP.NET)
Gli inizializzatori di telemetria impostano proprietà di contesto che vengono inviate insieme ad ogni elemento di telemetria.

È possibile [scrivere il propria inizializzatori](app-insights-api-filtering-sampling.md#add-properties) tooset le proprietà di contesto.

gli inizializzatori di Hello standard sono impostati tramite hello Web o WindowsServer NuGet pacchetti:

* `AccountIdTelemetryInitializer`Imposta proprietà AccountId hello.
* `AuthenticatedUserIdTelemetryInitializer`Imposta proprietà AuthenticatedUserId hello come set da hello SDK per JavaScript.
* `AzureRoleEnvironmentTelemetryInitializer`hello aggiornamenti `RoleName` e `RoleInstance` le proprietà di hello `Device` contesto per tutti gli elementi di dati di telemetria con le informazioni estratte dall'ambiente di runtime di Azure hello.
* `BuildInfoConfigComponentVersionTelemetryInitializer`hello aggiornamenti `Version` proprietà di hello `Component` contesto per tutti gli elementi di dati di telemetria con valore hello estratto dalla hello `BuildInfo.config` file prodotto da Microsoft Build.
* `ClientIpHeaderTelemetryInitializer`aggiornamenti `Ip` proprietà di hello `Location` basata sul contesto di tutti gli elementi di dati di telemetria su hello `X-Forwarded-For` intestazione HTTP della richiesta di hello.
* `DeviceTelemetryInitializer`hello gli aggiornamenti seguenti proprietà di hello `Device` contesto per tutti gli elementi di dati di telemetria.
  * `Type`è stato impostato troppo "PC"
  * `Id`è impostato toohello nome di dominio hello computer in cui è in esecuzione un'applicazione web hello.
  * `OemName`è impostato un valore toohello estratto da hello `Win32_ComputerSystem.Manufacturer` campo tramite WMI.
  * `Model`è impostato un valore toohello estratto da hello `Win32_ComputerSystem.Model` campo tramite WMI.
  * `NetworkType`è impostato un valore toohello estratto da hello `NetworkInterface`.
  * `Language`è impostato il nome toohello di hello `CurrentCulture`.
* `DomainNameRoleInstanceTelemetryInitializer`hello aggiornamenti `RoleInstance` proprietà di hello `Device` contesto per tutti gli elementi di dati di telemetria con il nome di dominio di hello del computer hello in cui è in esecuzione un'applicazione web hello.
* `OperationNameTelemetryInitializer`hello aggiornamenti `Name` proprietà di hello `RequestTelemetry` hello e `Name` proprietà di hello `Operation` basata sul contesto di tutti gli elementi di dati di telemetria nel metodo hello HTTP, nonché i nomi di hello tooprocess richiamato azione e del controller di ASP.NET MVC richiesta.
* `OperationIdTelemetryInitializer`o `OperationCorrelationTelemetryInitializer` hello aggiornamenti `Operation.Id` proprietà di contesto di tutti gli elementi di dati di telemetria rilevati durante la gestione di una richiesta con hello generato automaticamente `RequestTelemetry.Id`.
* `SessionTelemetryInitializer`hello aggiornamenti `Id` proprietà di hello `Session` contesto per tutti gli elementi di dati di telemetria con valore estratto dalla hello `ai_session` cookie generati da hello codice strumentazione ApplicationInsights JavaScript in esecuzione nel browser dell'utente hello.
* `SyntheticTelemetryInitializer`o `SyntheticUserAgentTelemetryInitializer` hello aggiornamenti `User`, `Session` e `Operation` proprietà di contesti di tutti gli elementi di dati di telemetria rilevate quando si gestisce una richiesta da un'origine sintetica, ad esempio una disponibilità test o un bot motore di ricerca. Per impostazione predefinita, [Esplora metriche](app-insights-metrics-explorer.md) non mostra la telemetria sintetica.

    Hello `<Filters>` impostare proprietà delle richieste di hello di identificazione.
* `UserAgentTelemetryInitializer`hello aggiornamenti `UserAgent` proprietà di hello `User` basata sul contesto di tutti gli elementi di dati di telemetria su hello `User-Agent` intestazione HTTP della richiesta di hello.
* `UserTelemetryInitializer`hello aggiornamenti `Id` e `AcquisitionDate` le proprietà di `User` contesto per tutti gli elementi di dati di telemetria con i valori estratti da hello `ai_user` cookie generati dal codice di strumentazione di Application Insights JavaScript hello in esecuzione in hello browser dell'utente.
* `WebTestTelemetryInitializer`set di hello user id, id di sessione e le proprietà dell'origine sintetiche per HTTP richieste che provengono da [disponibilità test](app-insights-monitor-web-app-availability.md).
  Hello `<Filters>` impostare proprietà delle richieste di hello di identificazione.

Per le applicazioni .NET in esecuzione nell'infrastruttura del servizio, è possibile includere hello `Microsoft.ApplicationInsights.ServiceFabric` pacchetto NuGet. Il pacchetto include un `FabricTelemetryInitializer`, che aggiunge gli elementi tootelemetry di proprietà di Service Fabric. Per ulteriori informazioni, vedere hello [pagina GitHub](https://go.microsoft.com/fwlink/?linkid=848457) sulle proprietà hello aggiunte dal pacchetto NuGet.

## <a name="telemetry-processors-aspnet"></a>Processori di telemetria (ASP.NET)
Processori di telemetria è possono filtrare e modificare ogni elemento di dati di telemetria appena prima che venga inviata dal portale di toohello hello SDK.

E’ possibile [scrivere i propri processori di telemetria](app-insights-api-filtering-sampling.md#filtering).

#### <a name="adaptive-sampling-telemetry-processor-from-200-beta3"></a>Processore di telemetria di campionamento adattivo (da 2.0.0-beta3)
Questa opzione è abilitata per impostazione predefinita. Se l'app invia molti dati di telemetria, questo processore rimuove alcune di esse.

```xml

    <TelemetryProcessors>
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    </TelemetryProcessors>

```

il parametro Hello fornisce destinazione hello hello algoritmo tenta tooachieve. Ogni istanza di hello SDK funziona in modo indipendente, quindi se il server è un cluster di più computer, volume hello dei dati di telemetria verrà moltiplicati conseguenza.

[Altre informazioni sul campionamento](app-insights-sampling.md).

#### <a name="fixed-rate-sampling-telemetry-processor-from-200-beta1"></a>Processore di telemetria di campionamento adattivo (da 2.0.0-beta1)
È inoltre disponibile un [processore di telemetria di campionamento](app-insights-api-filtering-sampling.md) standard (da 2.0.1):

```XML

    <TelemetryProcessors>
     <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">

     <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
     <SamplingPercentage>10</SamplingPercentage>
     </Add>
   </TelemetryProcessors>

```



## <a name="channel-parameters-java"></a>Parametri del canale (Java)
Questi parametri influiscono sulle modalità hello SDK per Java deve archiviare e scaricare i dati di telemetria hello da esso raccolti.

#### <a name="maxtelemetrybuffercapacity"></a>MaxTelemetryBufferCapacity
numero di Hello di elementi di dati di telemetria che possono essere archiviati in archiviazione in memoria hello del SDK. Quando viene raggiunto il numero, viene svuotato il buffer di dati di telemetria hello:, ovvero gli elementi di dati di telemetria hello vengono inviati i server di Application Insights toohello.

* Min: 1
* Max: 1000
* Valore predefinito: 500

```

  <ApplicationInsights>
      ...
      <Channel>
       <MaxTelemetryBufferCapacity>100</MaxTelemetryBufferCapacity>
      </Channel>
      ...
  </ApplicationInsights>
```

#### <a name="flushintervalinseconds"></a>FlushIntervalInSeconds
Determina la frequenza con cui hello dati archiviati nel servizio di archiviazione in memoria hello devono essere scaricato (inviato tooApplication Insights).

* Min: 1
* Max: 300
* Valore predefinito: 5

```

    <ApplicationInsights>
      ...
      <Channel>
        <FlushIntervalInSeconds>100</FlushIntervalInSeconds>
      </Channel>
      ...
    </ApplicationInsights>
```

#### <a name="maxtransmissionstoragecapacityinmb"></a>MaxTransmissionStorageCapacityInMB
Determina hello la dimensione massima in MB assegnato toohello nell'archivio permanente sul disco locale hello. Questa risorsa di archiviazione viene utilizzato per salvare in modo permanente gli elementi di telemetria non è stato possibile toobe trasmesso toohello Application Insights endpoint. Quando sono stato raggiunto dimensioni di archiviazione hello, nuovi elementi di dati di telemetria verranno eliminati.

* Min: 1
* Max: 100
* Valore predefinito: 10

```

   <ApplicationInsights>
      ...
      <Channel>
        <MaxTransmissionStorageCapacityInMB>50</MaxTransmissionStorageCapacityInMB>
      </Channel>
      ...
   </ApplicationInsights>
```



## <a name="instrumentationkey"></a>InstrumentationKey
Ciò determina la risorsa di Application Insights hello in cui i dati verranno visualizzati. In genere, viene creata una risorsa separata, con una chiave separata, per ognuna delle applicazioni.

Se si desidera chiave hello tooset in modo dinamico, ad esempio se si desidera che i risultati di toosend dalle risorse dell'applicazione - toodifferent omettere chiave hello dal file di configurazione hello e impostarlo nel codice.

chiave di hello tooset per tutte le istanze di TelemetryClient, inclusi i moduli di telemetria standard, imposta la chiave hello TelemetryConfiguration.Active. Eseguire questa operazione in un metodo di inizializzazione, ad esempio global.aspx.cs in un servizio ASP.NET:

```C#

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      //...
```

Se si desidera toosend un set specifico di risorse diverso tooa di eventi, è possibile impostare chiave hello per un TelemetryClient specifico:

```C#

    var tc = new TelemetryClient();
    tc.Context.InstrumentationKey = "----- my key ----";
    tc.TrackEvent("myEvent");
    // ...

```

una nuova chiave, tooget [creare una nuova risorsa nel portale Application Insights hello][new].

## <a name="next-steps"></a>Passaggi successivi
[Altre informazioni sulle API hello][api].

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[netlogs]: app-insights-asp-net-trace-logs.md
[new]: app-insights-create-new-resource.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
