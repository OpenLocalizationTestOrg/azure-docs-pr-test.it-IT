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
# <a name="application-and-service-level-event-and-log-generation"></a><span data-ttu-id="d5808-103">Generazione di eventi e log a livello di applicazione e servizio</span><span class="sxs-lookup"><span data-stu-id="d5808-103">Application and service level event and log generation</span></span>

## <a name="instrumenting-hello-code-with-custom-events"></a><span data-ttu-id="d5808-104">La strumentazione di codice hello con eventi personalizzati</span><span class="sxs-lookup"><span data-stu-id="d5808-104">Instrumenting hello code with custom events</span></span>

<span data-ttu-id="d5808-105">La strumentazione di codice hello è base hello per la maggior parte degli altri aspetti dei servizi di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="d5808-105">Instrumenting hello code is hello basis for most other aspects of monitoring your services.</span></span> <span data-ttu-id="d5808-106">La strumentazione è unico modo hello che sanno che qualcosa non vada e toodiagnose cosa toobe fissa.</span><span class="sxs-lookup"><span data-stu-id="d5808-106">Instrumentation is hello only way you can know that something is wrong, and toodiagnose what needs toobe fixed.</span></span> <span data-ttu-id="d5808-107">Sebbene sia tecnicamente possibile tooconnect un servizio di produzione tooa debugger, non è una pratica comune.</span><span class="sxs-lookup"><span data-stu-id="d5808-107">Although technically it's possible tooconnect a debugger tooa production service, it's not a common practice.</span></span> <span data-ttu-id="d5808-108">I dati dettagliati di strumentazione sono quindi importanti.</span><span class="sxs-lookup"><span data-stu-id="d5808-108">So, having detailed instrumentation data is important.</span></span>

<span data-ttu-id="d5808-109">Alcuni prodotti instrumentano automaticamente il codice.</span><span class="sxs-lookup"><span data-stu-id="d5808-109">Some products automatically instrument your code.</span></span> <span data-ttu-id="d5808-110">Benché queste soluzioni siano efficaci, è quasi sempre necessaria una strumentazione manuale.</span><span class="sxs-lookup"><span data-stu-id="d5808-110">Although these solutions can work well, manual instrumentation is almost always required.</span></span> <span data-ttu-id="d5808-111">Fine hello, è necessario disporre di sufficiente tooforensically informazioni eseguire il debug di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="d5808-111">In hello end, you must have enough information tooforensically debug hello application.</span></span> <span data-ttu-id="d5808-112">Questo documento descrive diversi approcci tooinstrumenting del codice, e quando toochoose un approccio rispetto a un altro.</span><span class="sxs-lookup"><span data-stu-id="d5808-112">This document describes different approaches tooinstrumenting your code, and when toochoose one approach over another.</span></span>

## <a name="eventsource"></a><span data-ttu-id="d5808-113">EventSource</span><span class="sxs-lookup"><span data-stu-id="d5808-113">EventSource</span></span>
<span data-ttu-id="d5808-114">Quando si crea una soluzione di Azure Service Fabric da un modello in Visual Studio, viene generata una classe derivata da **EventSource** (**ServiceEventSource** o **ActorEventSource**).</span><span class="sxs-lookup"><span data-stu-id="d5808-114">When you create a Service Fabric solution from a template in Visual Studio, an **EventSource**-derived class (**ServiceEventSource** or **ActorEventSource**) is generated.</span></span> <span data-ttu-id="d5808-115">Viene creato un modello in cui è possibile aggiungere eventi per l'applicazione o il servizio.</span><span class="sxs-lookup"><span data-stu-id="d5808-115">A template is created, in which you can add events for your application or service.</span></span> <span data-ttu-id="d5808-116">Hello **EventSource** nome **deve** essere univoco e deve essere rinominato dalla stringa di modello predefinito di hello MyCompany -&lt;soluzione&gt; - &lt; progetto&gt;.</span><span class="sxs-lookup"><span data-stu-id="d5808-116">hello **EventSource** name **must** be unique, and should be renamed from hello default template string MyCompany-&lt;solution&gt;-&lt;project&gt;.</span></span> <span data-ttu-id="d5808-117">Più **EventSource** definizioni che usano hello stesso cause nome un problema in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="d5808-117">Having multiple **EventSource** definitions that use hello same name causes an issue at run time.</span></span> <span data-ttu-id="d5808-118">Ogni evento definito deve avere un identificatore univoco.</span><span class="sxs-lookup"><span data-stu-id="d5808-118">Each defined event must have a unique identifier.</span></span> <span data-ttu-id="d5808-119">Se un identificatore non è univoco, si verificherà un errore di runtime.</span><span class="sxs-lookup"><span data-stu-id="d5808-119">If an identifier is not unique, a runtime failure occurs.</span></span> <span data-ttu-id="d5808-120">Alcune organizzazioni preassegnare intervalli di valori per i conflitti tooavoid identificatori tra i team di sviluppo separati.</span><span class="sxs-lookup"><span data-stu-id="d5808-120">Some organizations preassign ranges of values for identifiers tooavoid conflicts between separate development teams.</span></span> <span data-ttu-id="d5808-121">Per ulteriori informazioni, vedere [blog di Vance](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) o hello [documentazione MSDN](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).</span><span class="sxs-lookup"><span data-stu-id="d5808-121">For more information, see [Vance's blog](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) or hello [MSDN documentation](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).</span></span>

### <a name="using-structured-eventsource-events"></a><span data-ttu-id="d5808-122">Uso di eventi EventSource strutturati</span><span class="sxs-lookup"><span data-stu-id="d5808-122">Using structured EventSource events</span></span>

<span data-ttu-id="d5808-123">Ciascuno di hello eventi negli esempi di codice hello in questa sezione vengono definiti per un caso specifico, ad esempio, quando viene registrato un tipo di servizio.</span><span class="sxs-lookup"><span data-stu-id="d5808-123">Each of hello events in hello code examples in this section are defined for a specific case, for example, when a service type is registered.</span></span> <span data-ttu-id="d5808-124">Quando si definiscono i messaggi dal caso d'uso, possono essere incluso nel pacchetto dati testo hello di errore di hello e sarà possibile più facilmente la ricerca e filtro in base a nomi hello o valori di hello specificate proprietà.</span><span class="sxs-lookup"><span data-stu-id="d5808-124">When you define messages by use case, data can be packaged with hello text of hello error, and you can more easily search and filter based on hello names or values of hello specified properties.</span></span> <span data-ttu-id="d5808-125">Strutturazione di output della strumentazione hello rende più facile tooconsume, ma richiede maggiore attenzione e l'ora toodefine un nuovo evento per ogni caso d'uso.</span><span class="sxs-lookup"><span data-stu-id="d5808-125">Structuring hello instrumentation output makes it easier tooconsume, but requires more thought and time toodefine a new event for each use case.</span></span> <span data-ttu-id="d5808-126">Alcune definizioni di evento possono essere condivise tra l'intera applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="d5808-126">Some event definitions can be shared across hello entire application.</span></span> <span data-ttu-id="d5808-127">Un evento di avvio o arresto di un metodo, ad esempio, può essere riutilizzato in molti servizi in un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d5808-127">For example, a method start or stop event would be reused across many services within an application.</span></span> <span data-ttu-id="d5808-128">Un servizio specifico per un dominio, ad esempio un sistema di ordine, può avere un evento **CreateOrder**, che ha un proprio evento univoco.</span><span class="sxs-lookup"><span data-stu-id="d5808-128">A domain-specific service, like an order system, might have a **CreateOrder** event, which has its own unique event.</span></span> <span data-ttu-id="d5808-129">Questo approccio può generare un numero elevato di eventi e può potenzialmente richiedere il coordinamento degli identificatori tra i team di progetto.</span><span class="sxs-lookup"><span data-stu-id="d5808-129">This approach might generate many events, and potentially require coordination of identifiers across project teams.</span></span> 

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

### <a name="using-eventsource-generically"></a><span data-ttu-id="d5808-130">Uso generico di EventSource</span><span class="sxs-lookup"><span data-stu-id="d5808-130">Using EventSource generically</span></span>

<span data-ttu-id="d5808-131">Poiché può essere difficile definire eventi specifici, molti utenti ne definiscono pochi con un set di parametri in comune che generalmente genera le informazioni sotto forma di stringa.</span><span class="sxs-lookup"><span data-stu-id="d5808-131">Because defining specific events can be difficult, many people define a few events with a common set of parameters that generally output their information as a string.</span></span> <span data-ttu-id="d5808-132">Gran parte dell'aspetto di hello strutturato viene persa, ed è più difficili toosearch e filtro hello i risultati.</span><span class="sxs-lookup"><span data-stu-id="d5808-132">Much of hello structured aspect is lost, and it's more difficult toosearch and filter hello results.</span></span> <span data-ttu-id="d5808-133">In questo approccio, vengono definiti alcuni eventi che corrispondono in genere i livelli di registrazione toohello.</span><span class="sxs-lookup"><span data-stu-id="d5808-133">In this approach, a few events that usually correspond toohello logging levels are defined.</span></span> <span data-ttu-id="d5808-134">Hello frammento di codice seguente definisce un messaggio di errore e di debug:</span><span class="sxs-lookup"><span data-stu-id="d5808-134">hello following snippet defines a debug and error message:</span></span>

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

<span data-ttu-id="d5808-135">Anche un ibrido di strumentazione strutturata e generica può essere una soluzione ideale.</span><span class="sxs-lookup"><span data-stu-id="d5808-135">Using a hybrid of structured and generic instrumentation also can work well.</span></span> <span data-ttu-id="d5808-136">La strumentazione strutturata viene usata per la segnalazione degli errori e per le metriche.</span><span class="sxs-lookup"><span data-stu-id="d5808-136">Structured instrumentation is used for reporting errors and metrics.</span></span> <span data-ttu-id="d5808-137">Eventi generici possono essere usati per hello dettagliata registrazione ovvero utilizzati dai tecnici per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="d5808-137">Generic events can be used for hello detailed logging that is consumed by engineers for troubleshooting.</span></span>

## <a name="aspnet-core-logging"></a><span data-ttu-id="d5808-138">Registrazione di ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="d5808-138">ASP.NET Core logging</span></span>

<span data-ttu-id="d5808-139">È importante toocarefully pianificare come instrumentare il codice.</span><span class="sxs-lookup"><span data-stu-id="d5808-139">It's important toocarefully plan how you will instrument your code.</span></span> <span data-ttu-id="d5808-140">piano di Hello strumentazione destra consente di evitare potenzialmente destabilizzare il codice di base e quindi la necessità di codice hello tooreinstrument.</span><span class="sxs-lookup"><span data-stu-id="d5808-140">hello right instrumentation plan can help you avoid potentially destabilizing your code base, and then needing tooreinstrument hello code.</span></span> <span data-ttu-id="d5808-141">tooreduce rischio, è possibile scegliere come una libreria di strumentazione [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), che fa parte di Microsoft ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="d5808-141">tooreduce risk, you can choose an instrumentation library like [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), which is part of Microsoft ASP.NET Core.</span></span> <span data-ttu-id="d5808-142">ASP.NET Core è un [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) interfaccia che è possibile utilizzare con il provider di hello di propria scelta, riducendo l'effetto di hello sul codice esistente.</span><span class="sxs-lookup"><span data-stu-id="d5808-142">ASP.NET Core has an [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) interface that you can use with hello provider of your choice, while minimizing hello effect on existing code.</span></span> <span data-ttu-id="d5808-143">È possibile utilizzare il codice hello in ASP.NET Core in Windows e Linux e in hello completa di .NET Framework, in modo standardizzato il codice di strumentazione.</span><span class="sxs-lookup"><span data-stu-id="d5808-143">You can use hello code in ASP.NET Core on Windows and Linux, and in hello full .NET Framework, so your instrumentation code is standardized.</span></span> <span data-ttu-id="d5808-144">Ciò viene approfondito di seguito:</span><span class="sxs-lookup"><span data-stu-id="d5808-144">This is further explored below:</span></span>

### <a name="using-microsoftextensionslogging-in-service-fabric"></a><span data-ttu-id="d5808-145">Uso di Microsoft.Extensions.Logging in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d5808-145">Using Microsoft.Extensions.Logging in Service Fabric</span></span>

1. <span data-ttu-id="d5808-146">Aggiungi progetto di toohello pacchetto Microsoft.Extensions.Logging NuGet da tooinstrument hello.</span><span class="sxs-lookup"><span data-stu-id="d5808-146">Add hello Microsoft.Extensions.Logging NuGet package toohello project you want tooinstrument.</span></span> <span data-ttu-id="d5808-147">Inoltre, aggiungere tutti i pacchetti di provider (per un pacchetto di terze parti, vedere hello di esempio seguente).</span><span class="sxs-lookup"><span data-stu-id="d5808-147">Also, add any provider packages (for a third-party package, see hello following example).</span></span> <span data-ttu-id="d5808-148">Per altre informazioni, vedere [Logging in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging) (Registrazione in ASP.NET Core).</span><span class="sxs-lookup"><span data-stu-id="d5808-148">For more information, see [Logging in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging).</span></span>
2. <span data-ttu-id="d5808-149">Aggiungere un **utilizzando** direttiva Microsoft.Extensions.Logging tooyour file di servizio.</span><span class="sxs-lookup"><span data-stu-id="d5808-149">Add a **using** directive for Microsoft.Extensions.Logging tooyour service file.</span></span>
3. <span data-ttu-id="d5808-150">Definire una variabile privata all'interno della classe di servizio.</span><span class="sxs-lookup"><span data-stu-id="d5808-150">Define a private variable within your service class.</span></span>

  ```csharp
  private ILogger _logger = null;

  ```
4. <span data-ttu-id="d5808-151">Nel costruttore hello della classe del servizio, aggiungere questo codice:</span><span class="sxs-lookup"><span data-stu-id="d5808-151">In hello constructor of your service class, add this code:</span></span>

  ```csharp
  _logger = new LoggerFactory().CreateLogger<Stateless>();

  ```
5. <span data-ttu-id="d5808-152">Avviare la strumentazione del codice nei metodi.</span><span class="sxs-lookup"><span data-stu-id="d5808-152">Start instrumenting your code in your methods.</span></span> <span data-ttu-id="d5808-153">Ecco alcuni esempi:</span><span class="sxs-lookup"><span data-stu-id="d5808-153">Here are a few samples:</span></span>

  ```csharp
  _logger.LogDebug("Debug-level event from Microsoft.Logging");
  _logger.LogInformation("Informational-level event from Microsoft.Logging");

  // In this variant, we're adding structured properties RequestName and Duration, which have values MyRequest and hello duration of hello request.
  // Later in hello article, we discuss why this step is useful.
  _logger.LogInformation("{RequestName} {Duration}", "MyRequest", requestDuration);

  ```

## <a name="using-other-logging-providers"></a><span data-ttu-id="d5808-154">Uso di altri provider di registrazione</span><span class="sxs-lookup"><span data-stu-id="d5808-154">Using other logging providers</span></span>

<span data-ttu-id="d5808-155">Alcuni provider di terze parti utilizzano approccio hello descritto nella precedente sezione hello inclusi [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), e [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging).</span><span class="sxs-lookup"><span data-stu-id="d5808-155">Some third-party providers use hello approach described in hello preceding section, including [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), and [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging).</span></span> <span data-ttu-id="d5808-156">È possibile inserirli tutti nella registrazione ASP.NET Core oppure usarli separatamente.</span><span class="sxs-lookup"><span data-stu-id="d5808-156">You can plug each of these into ASP.NET Core logging, or you can use them separately.</span></span> <span data-ttu-id="d5808-157">Serilog offre una funzionalità che arricchisce tutti i messaggi inviati da un logger.</span><span class="sxs-lookup"><span data-stu-id="d5808-157">Serilog has a feature that enriches all messages sent from a logger.</span></span> <span data-ttu-id="d5808-158">Questa funzionalità può essere utile toooutput hello servizio nome, tipo e le informazioni di partizione.</span><span class="sxs-lookup"><span data-stu-id="d5808-158">This feature can be useful toooutput hello service name, type, and partition information.</span></span> <span data-ttu-id="d5808-159">toouse questa funzionalità in hello infrastruttura ASP.NET Core, eseguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="d5808-159">toouse this capability in hello ASP.NET Core infrastructure, do these steps:</span></span>

1. <span data-ttu-id="d5808-160">Aggiungere Serilog, Serilog.Extensions.Logging, hello e pacchetti di Serilog.Sinks.Observable NuGet toohello progetto.</span><span class="sxs-lookup"><span data-stu-id="d5808-160">Add hello Serilog, Serilog.Extensions.Logging, and Serilog.Sinks.Observable NuGet packages toohello project.</span></span> <span data-ttu-id="d5808-161">Ad esempio successivo hello, è necessario aggiungere anche Serilog.Sinks.Literate.</span><span class="sxs-lookup"><span data-stu-id="d5808-161">For hello next example, also add Serilog.Sinks.Literate.</span></span> <span data-ttu-id="d5808-162">Un approccio migliore viene illustrato più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="d5808-162">A better approach is shown later in this article.</span></span>
2. <span data-ttu-id="d5808-163">In Serilog, creare un'istanza di logger LoggerConfiguration e hello.</span><span class="sxs-lookup"><span data-stu-id="d5808-163">In Serilog, create a LoggerConfiguration and hello logger instance.</span></span>

  ```csharp
  Log.Logger = new LoggerConfiguration().WriteTo.LiterateConsole().CreateLogger();
  ```

3. <span data-ttu-id="d5808-164">Aggiungere un costruttore di servizio Serilog.ILogger toohello argomento e passare hello appena creata del logger.</span><span class="sxs-lookup"><span data-stu-id="d5808-164">Add a Serilog.ILogger argument toohello service constructor, and pass hello newly created logger.</span></span>

  ```csharp
  ServiceRuntime.RegisterServiceAsync("StatelessType", context => new Stateless(context, Log.Logger)).GetAwaiter().GetResult();
  ```

4. <span data-ttu-id="d5808-165">Nel costruttore servizio hello, aggiungere hello seguente di codice che crea hello enrichers di proprietà per hello **ServiceTypeName**, **ServiceName**, **PartitionId**e  **InstanceId** proprietà del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="d5808-165">In hello service constructor, add hello following code, which creates hello property enrichers for hello **ServiceTypeName**, **ServiceName**, **PartitionId**, and **InstanceId** properties of hello service.</span></span> <span data-ttu-id="d5808-166">Aggiunge inoltre una toohello enricher proprietà factory di registrazione di ASP.NET Core, pertanto è possibile utilizzare Microsoft.Extensions.Logging.ILogger nel codice.</span><span class="sxs-lookup"><span data-stu-id="d5808-166">It also adds a property enricher toohello ASP.NET Core logging factory, so you can use Microsoft.Extensions.Logging.ILogger in your code.</span></span>

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

5. <span data-ttu-id="d5808-167">Instrumentare il codice di hello hello stesso come se si utilizza ASP.NET Core senza Serilog.</span><span class="sxs-lookup"><span data-stu-id="d5808-167">Instrument hello code hello same as if you were using ASP.NET Core without Serilog.</span></span>

  >[!NOTE]
  ><span data-ttu-id="d5808-168">È consigliabile non utilizzare hello statico Log.Logger con hello sopra riportato.</span><span class="sxs-lookup"><span data-stu-id="d5808-168">We recommend that you don't use hello static Log.Logger with hello preceding example.</span></span> <span data-ttu-id="d5808-169">Service Fabric può ospitare più istanze di hello stesso tipo all'interno di un singolo processo del servizio.</span><span class="sxs-lookup"><span data-stu-id="d5808-169">Service Fabric can host multiple instances of hello same service type within a single process.</span></span> <span data-ttu-id="d5808-170">Se si utilizza hello Log.Logger statico, ultimo writer di hello di enrichers proprietà hello verranno visualizzati i valori per tutte le istanze in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="d5808-170">If you use hello static Log.Logger, hello last writer of hello property enrichers will show values for all instances that are running.</span></span> <span data-ttu-id="d5808-171">Si tratta di uno dei motivi per cui hello _logger variabile è una variabile membro privato della classe di servizio hello.</span><span class="sxs-lookup"><span data-stu-id="d5808-171">This is one reason why hello _logger variable is a private member variable of hello service class.</span></span> <span data-ttu-id="d5808-172">Inoltre, è necessario apportare codice disponibile toocommon _logger di hello, che può essere utilizzato in tutti i servizi.</span><span class="sxs-lookup"><span data-stu-id="d5808-172">Also, you must make hello _logger available toocommon code, which might be used across services.</span></span>

## <a name="choosing-a-logging-provider"></a><span data-ttu-id="d5808-173">Scelta di un provider di registrazione</span><span class="sxs-lookup"><span data-stu-id="d5808-173">Choosing a logging provider</span></span>

<span data-ttu-id="d5808-174">Se l'applicazione si basa sulle prestazioni elevate, **EventSource** è in genere l'approccio ottimale.</span><span class="sxs-lookup"><span data-stu-id="d5808-174">If your application relies on high performance, **EventSource** is usually a good approach.</span></span> <span data-ttu-id="d5808-175">**EventSource** *in genere* Usa meno risorse e più efficace rispetto alla registrazione di ASP.NET Core o una qualsiasi delle soluzioni di terze parti disponibili hello.</span><span class="sxs-lookup"><span data-stu-id="d5808-175">**EventSource** *generally* uses fewer resources and performs better than ASP.NET Core logging or any of hello available third-party solutions.</span></span>  <span data-ttu-id="d5808-176">Non è un problema per molti servizi, ma se il servizio è orientato alle prestazioni **EventSource** si rivela la scelta più indicata.</span><span class="sxs-lookup"><span data-stu-id="d5808-176">This isn't an issue for many services, but if your service is performance-oriented, using **EventSource** might be a better choice.</span></span> <span data-ttu-id="d5808-177">Tuttavia, tooget questi vantaggi di strutturato registrazione, **EventSource** richiede un investimento maggiore dal team di progettazione.</span><span class="sxs-lookup"><span data-stu-id="d5808-177">However, tooget these benefits of structured logging, **EventSource** requires a larger investment from your engineering team.</span></span> <span data-ttu-id="d5808-178">Se possibile, eseguire un rapido prototipo di alcune opzioni di registrazione e quindi scegliere hello che meglio soddisfa le esigenze.</span><span class="sxs-lookup"><span data-stu-id="d5808-178">If possible, do a quick prototype of a few logging options, and then choose hello one that best meets your needs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5808-179">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d5808-179">Next steps</span></span>

<span data-ttu-id="d5808-180">Dopo avere scelto il tooinstrument di provider di registrazione, le applicazioni e servizi, eventi e i registri delle necessario toobe aggregati prima di inviarli tooany piattaforma di analisi.</span><span class="sxs-lookup"><span data-stu-id="d5808-180">Once you have chosen your logging provider tooinstrument your applications and services, your logs and events need toobe aggregated before they can be sent tooany analysis platform.</span></span> <span data-ttu-id="d5808-181">Conoscenza [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) e [WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter comprendere alcuni dei hello opzioni consigliata.</span><span class="sxs-lookup"><span data-stu-id="d5808-181">Read about [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) and [WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter understand some of hello recommended options.</span></span>
