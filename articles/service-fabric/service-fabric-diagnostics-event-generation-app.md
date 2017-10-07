---
title: Monitoraggio livello di applicazione di servizio dell'infrastruttura aaaAzure | Documenti Microsoft
description: Informazioni sull'applicazione e i registri e gli eventi a livello di servizio utilizzato toomonitor e diagnosticare i cluster di Azure Service Fabric.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/26/2017
ms.author: dekapur
ms.openlocfilehash: 4f4da1eaad4b88428eaa3a2100ac25c8a285a727
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-and-service-level-event-and-log-generation"></a>Generazione di eventi e log a livello di applicazione e servizio

## <a name="instrumenting-hello-code-with-custom-events"></a>La strumentazione di codice hello con eventi personalizzati

La strumentazione di codice hello è base hello per la maggior parte degli altri aspetti dei servizi di monitoraggio. La strumentazione è unico modo hello che sanno che qualcosa non vada e toodiagnose cosa toobe fissa. Sebbene sia tecnicamente possibile tooconnect un servizio di produzione tooa debugger, non è una pratica comune. I dati dettagliati di strumentazione sono quindi importanti.

Alcuni prodotti instrumentano automaticamente il codice. Benché queste soluzioni siano efficaci, è quasi sempre necessaria una strumentazione manuale. Fine hello, è necessario disporre di sufficiente tooforensically informazioni eseguire il debug di un'applicazione hello. Questo documento descrive diversi approcci tooinstrumenting del codice, e quando toochoose un approccio rispetto a un altro.

## <a name="eventsource"></a>EventSource
Quando si crea una soluzione di Azure Service Fabric da un modello in Visual Studio, viene generata una classe derivata da **EventSource** (**ServiceEventSource** o **ActorEventSource**). Viene creato un modello in cui è possibile aggiungere eventi per l'applicazione o il servizio. Hello **EventSource** nome **deve** essere univoco e deve essere rinominato dalla stringa di modello predefinito di hello MyCompany -&lt;soluzione&gt; - &lt; progetto&gt;. Più **EventSource** definizioni che usano hello stesso cause nome un problema in fase di esecuzione. Ogni evento definito deve avere un identificatore univoco. Se un identificatore non è univoco, si verificherà un errore di runtime. Alcune organizzazioni preassegnare intervalli di valori per i conflitti tooavoid identificatori tra i team di sviluppo separati. Per ulteriori informazioni, vedere [blog di Vance](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) o hello [documentazione MSDN](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).

### <a name="using-structured-eventsource-events"></a>Uso di eventi EventSource strutturati

Ciascuno di hello eventi negli esempi di codice hello in questa sezione vengono definiti per un caso specifico, ad esempio, quando viene registrato un tipo di servizio. Quando si definiscono i messaggi dal caso d'uso, possono essere incluso nel pacchetto dati testo hello di errore di hello e sarà possibile più facilmente la ricerca e filtro in base a nomi hello o valori di hello specificate proprietà. Strutturazione di output della strumentazione hello rende più facile tooconsume, ma richiede maggiore attenzione e l'ora toodefine un nuovo evento per ogni caso d'uso. Alcune definizioni di evento possono essere condivise tra l'intera applicazione hello. Un evento di avvio o arresto di un metodo, ad esempio, può essere riutilizzato in molti servizi in un'applicazione. Un servizio specifico per un dominio, ad esempio un sistema di ordine, può avere un evento **CreateOrder**, che ha un proprio evento univoco. Questo approccio può generare un numero elevato di eventi e può potenzialmente richiedere il coordinamento degli identificatori tra i team di progetto. 

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // hello instance constructor is private tooenforce singleton semantics.
        private ServiceEventSource() : base() { }

        ...

        // hello ServiceTypeRegistered event contains a unique identifier, an event attribute that defined hello event, and hello code implementation of hello event.
        private const int ServiceTypeRegisteredEventId = 3;
        [Event(ServiceTypeRegisteredEventId, Level = EventLevel.Informational, Message = "Service host process {0} registered service type {1}", Keywords = Keywords.ServiceInitialization)]
        public void ServiceTypeRegistered(int hostProcessId, string serviceType)
        {
            WriteEvent(ServiceTypeRegisteredEventId, hostProcessId, serviceType);
        }

        // hello ServiceHostInitializationFailed event contains a unique identifier, an event attribute that defined hello event, and hello code implementation of hello event.
        private const int ServiceHostInitializationFailedEventId = 4;
        [Event(ServiceHostInitializationFailedEventId, Level = EventLevel.Error, Message = "Service host initialization failed", Keywords = Keywords.ServiceInitialization)]
        public void ServiceHostInitializationFailed(string exception)
        {
            WriteEvent(ServiceHostInitializationFailedEventId, exception);
        }
```

### <a name="using-eventsource-generically"></a>Uso generico di EventSource

Poiché può essere difficile definire eventi specifici, molti utenti ne definiscono pochi con un set di parametri in comune che generalmente genera le informazioni sotto forma di stringa. Gran parte dell'aspetto di hello strutturato viene persa, ed è più difficili toosearch e filtro hello i risultati. In questo approccio, vengono definiti alcuni eventi che corrispondono in genere i livelli di registrazione toohello. Hello frammento di codice seguente definisce un messaggio di errore e di debug:

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // hello Instance constructor is private, tooenforce singleton semantics.
        private ServiceEventSource() : base() { }

        ...

        private const int DebugEventId = 10;
        [Event(DebugEventId, Level = EventLevel.Verbose, Message = "{0}")]
        public void Debug(string msg)
        {
            WriteEvent(DebugEventId, msg);
        }

        private const int ErrorEventId = 11;
        [Event(ErrorEventId, Level = EventLevel.Error, Message = "Error: {0} - {1}")]
        public void Error(string error, string msg)
        {
            WriteEvent(ErrorEventId, error, msg);
        }
```

Anche un ibrido di strumentazione strutturata e generica può essere una soluzione ideale. La strumentazione strutturata viene usata per la segnalazione degli errori e per le metriche. Eventi generici possono essere usati per hello dettagliata registrazione ovvero utilizzati dai tecnici per la risoluzione dei problemi.

## <a name="aspnet-core-logging"></a>Registrazione di ASP.NET Core

È importante toocarefully pianificare come instrumentare il codice. piano di Hello strumentazione destra consente di evitare potenzialmente destabilizzare il codice di base e quindi la necessità di codice hello tooreinstrument. tooreduce rischio, è possibile scegliere come una libreria di strumentazione [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), che fa parte di Microsoft ASP.NET Core. ASP.NET Core è un [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) interfaccia che è possibile utilizzare con il provider di hello di propria scelta, riducendo l'effetto di hello sul codice esistente. È possibile utilizzare il codice hello in ASP.NET Core in Windows e Linux e in hello completa di .NET Framework, in modo standardizzato il codice di strumentazione. Ciò viene approfondito di seguito:

### <a name="using-microsoftextensionslogging-in-service-fabric"></a>Uso di Microsoft.Extensions.Logging in Service Fabric

1. Aggiungi progetto di toohello pacchetto Microsoft.Extensions.Logging NuGet da tooinstrument hello. Inoltre, aggiungere tutti i pacchetti di provider (per un pacchetto di terze parti, vedere hello di esempio seguente). Per altre informazioni, vedere [Logging in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging) (Registrazione in ASP.NET Core).
2. Aggiungere un **utilizzando** direttiva Microsoft.Extensions.Logging tooyour file di servizio.
3. Definire una variabile privata all'interno della classe di servizio.

  ```csharp
  private ILogger _logger = null;

  ```
4. Nel costruttore hello della classe del servizio, aggiungere questo codice:

  ```csharp
  _logger = new LoggerFactory().CreateLogger<Stateless>();

  ```
5. Avviare la strumentazione del codice nei metodi. Ecco alcuni esempi:

  ```csharp
  _logger.LogDebug("Debug-level event from Microsoft.Logging");
  _logger.LogInformation("Informational-level event from Microsoft.Logging");

  // In this variant, we're adding structured properties RequestName and Duration, which have values MyRequest and hello duration of hello request.
  // Later in hello article, we discuss why this step is useful.
  _logger.LogInformation("{RequestName} {Duration}", "MyRequest", requestDuration);

  ```

## <a name="using-other-logging-providers"></a>Uso di altri provider di registrazione

Alcuni provider di terze parti utilizzano approccio hello descritto nella precedente sezione hello inclusi [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), e [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging). È possibile inserirli tutti nella registrazione ASP.NET Core oppure usarli separatamente. Serilog offre una funzionalità che arricchisce tutti i messaggi inviati da un logger. Questa funzionalità può essere utile toooutput hello servizio nome, tipo e le informazioni di partizione. toouse questa funzionalità in hello infrastruttura ASP.NET Core, eseguire questi passaggi:

1. Aggiungere Serilog, Serilog.Extensions.Logging, hello e pacchetti di Serilog.Sinks.Observable NuGet toohello progetto. Ad esempio successivo hello, è necessario aggiungere anche Serilog.Sinks.Literate. Un approccio migliore viene illustrato più avanti in questo articolo.
2. In Serilog, creare un'istanza di logger LoggerConfiguration e hello.

  ```csharp
  Log.Logger = new LoggerConfiguration().WriteTo.LiterateConsole().CreateLogger();
  ```

3. Aggiungere un costruttore di servizio Serilog.ILogger toohello argomento e passare hello appena creata del logger.

  ```csharp
  ServiceRuntime.RegisterServiceAsync("StatelessType", context => new Stateless(context, Log.Logger)).GetAwaiter().GetResult();
  ```

4. Nel costruttore servizio hello, aggiungere hello seguente di codice che crea hello enrichers di proprietà per hello **ServiceTypeName**, **ServiceName**, **PartitionId**e  **InstanceId** proprietà del servizio hello. Aggiunge inoltre una toohello enricher proprietà factory di registrazione di ASP.NET Core, pertanto è possibile utilizzare Microsoft.Extensions.Logging.ILogger nel codice.

  ```csharp
  public Stateless(StatelessServiceContext context, Serilog.ILogger serilog)
      : base(context)
  {
      PropertyEnricher[] properties = new PropertyEnricher[]
      {
          new PropertyEnricher("ServiceTypeName", context.ServiceTypeName),
          new PropertyEnricher("ServiceName", context.ServiceName),
          new PropertyEnricher("PartitionId", context.PartitionId),
          new PropertyEnricher("InstanceId", context.ReplicaOrInstanceId),
      };

      serilog.ForContext(properties);

      _logger = new LoggerFactory().AddSerilog(serilog.ForContext(properties)).CreateLogger<Stateless>();
  }
  ```

5. Instrumentare il codice di hello hello stesso come se si utilizza ASP.NET Core senza Serilog.

  >[!NOTE]
  >È consigliabile non utilizzare hello statico Log.Logger con hello sopra riportato. Service Fabric può ospitare più istanze di hello stesso tipo all'interno di un singolo processo del servizio. Se si utilizza hello Log.Logger statico, ultimo writer di hello di enrichers proprietà hello verranno visualizzati i valori per tutte le istanze in esecuzione. Si tratta di uno dei motivi per cui hello _logger variabile è una variabile membro privato della classe di servizio hello. Inoltre, è necessario apportare codice disponibile toocommon _logger di hello, che può essere utilizzato in tutti i servizi.

## <a name="choosing-a-logging-provider"></a>Scelta di un provider di registrazione

Se l'applicazione si basa sulle prestazioni elevate, **EventSource** è in genere l'approccio ottimale. **EventSource** *in genere* Usa meno risorse e più efficace rispetto alla registrazione di ASP.NET Core o una qualsiasi delle soluzioni di terze parti disponibili hello.  Non è un problema per molti servizi, ma se il servizio è orientato alle prestazioni **EventSource** si rivela la scelta più indicata. Tuttavia, tooget questi vantaggi di strutturato registrazione, **EventSource** richiede un investimento maggiore dal team di progettazione. Se possibile, eseguire un rapido prototipo di alcune opzioni di registrazione e quindi scegliere hello che meglio soddisfa le esigenze.

## <a name="next-steps"></a>Passaggi successivi

Dopo avere scelto il tooinstrument di provider di registrazione, le applicazioni e servizi, eventi e i registri delle necessario toobe aggregati prima di inviarli tooany piattaforma di analisi. Conoscenza [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) e [WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter comprendere alcuni dei hello opzioni consigliata.
