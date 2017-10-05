---
title: Monitoraggio dell'applicazione Azure Service Fabric | Microsoft Docs
description: Informazioni su log ed eventi a livello di servizio e applicazione usati per monitorare e diagnosticare i cluster di Azure Service Fabric.
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
ms.openlocfilehash: 3c472904641108b7383cd0f1416c47460f8de11a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="application-and-service-level-event-and-log-generation"></a><span data-ttu-id="8f7eb-103">Generazione di eventi e log a livello di applicazione e servizio</span><span class="sxs-lookup"><span data-stu-id="8f7eb-103">Application and service level event and log generation</span></span>

## <a name="instrumenting-the-code-with-custom-events"></a><span data-ttu-id="8f7eb-104">Strumentazione del codice con eventi personalizzati</span><span class="sxs-lookup"><span data-stu-id="8f7eb-104">Instrumenting the code with custom events</span></span>

<span data-ttu-id="8f7eb-105">La strumentazione del codice è la base di molti altri aspetti di monitoraggio dei servizi.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-105">Instrumenting the code is the basis for most other aspects of monitoring your services.</span></span> <span data-ttu-id="8f7eb-106">La strumentazione è l'unico modo per rilevare eventuali problemi e individuare le correzioni necessarie.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-106">Instrumentation is the only way you can know that something is wrong, and to diagnose what needs to be fixed.</span></span> <span data-ttu-id="8f7eb-107">Anche se è tecnicamente possibile connettere un debugger a un servizio di produzione, questa non è una procedura comune.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-107">Although technically it's possible to connect a debugger to a production service, it's not a common practice.</span></span> <span data-ttu-id="8f7eb-108">I dati dettagliati di strumentazione sono quindi importanti.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-108">So, having detailed instrumentation data is important.</span></span>

<span data-ttu-id="8f7eb-109">Alcuni prodotti instrumentano automaticamente il codice.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-109">Some products automatically instrument your code.</span></span> <span data-ttu-id="8f7eb-110">Benché queste soluzioni siano efficaci, è quasi sempre necessaria una strumentazione manuale.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-110">Although these solutions can work well, manual instrumentation is almost always required.</span></span> <span data-ttu-id="8f7eb-111">Alla fine, è necessario disporre di informazioni sufficienti per eseguire un debug accurato dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-111">In the end, you must have enough information to forensically debug the application.</span></span> <span data-ttu-id="8f7eb-112">Questo documento illustra diversi approcci alla strumentazione del codice e indicano quando è consigliabile scegliere un approccio rispetto a un altro.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-112">This document describes different approaches to instrumenting your code, and when to choose one approach over another.</span></span>

## <a name="eventsource"></a><span data-ttu-id="8f7eb-113">EventSource</span><span class="sxs-lookup"><span data-stu-id="8f7eb-113">EventSource</span></span>
<span data-ttu-id="8f7eb-114">Quando si crea una soluzione di Azure Service Fabric da un modello in Visual Studio, viene generata una classe derivata da **EventSource** (**ServiceEventSource** o **ActorEventSource**).</span><span class="sxs-lookup"><span data-stu-id="8f7eb-114">When you create a Service Fabric solution from a template in Visual Studio, an **EventSource**-derived class (**ServiceEventSource** or **ActorEventSource**) is generated.</span></span> <span data-ttu-id="8f7eb-115">Viene creato un modello in cui è possibile aggiungere eventi per l'applicazione o il servizio.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-115">A template is created, in which you can add events for your application or service.</span></span> <span data-ttu-id="8f7eb-116">Il nome di **EventSource** **deve** essere univoco e deve essere rinominato dalla stringa del modello predefinito MyCompany-&lt;soluzione&gt;-&lt;progetto&gt;.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-116">The **EventSource** name **must** be unique, and should be renamed from the default template string MyCompany-&lt;solution&gt;-&lt;project&gt;.</span></span> <span data-ttu-id="8f7eb-117">Se esistono più definizioni di **EventSource** con lo stesso nome, potranno verificarsi errori di runtime.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-117">Having multiple **EventSource** definitions that use the same name causes an issue at run time.</span></span> <span data-ttu-id="8f7eb-118">Ogni evento definito deve avere un identificatore univoco.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-118">Each defined event must have a unique identifier.</span></span> <span data-ttu-id="8f7eb-119">Se un identificatore non è univoco, si verificherà un errore di runtime.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-119">If an identifier is not unique, a runtime failure occurs.</span></span> <span data-ttu-id="8f7eb-120">Alcune organizzazioni preassegnano intervalli di valori per gli identificatori, in modo da evitare conflitti tra team di sviluppo separati.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-120">Some organizations preassign ranges of values for identifiers to avoid conflicts between separate development teams.</span></span> <span data-ttu-id="8f7eb-121">Per altre informazioni, vedere il [blog di Vance](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) o la [documentazione di MSDN](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).</span><span class="sxs-lookup"><span data-stu-id="8f7eb-121">For more information, see [Vance's blog](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) or the [MSDN documentation](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).</span></span>

### <a name="using-structured-eventsource-events"></a><span data-ttu-id="8f7eb-122">Uso di eventi EventSource strutturati</span><span class="sxs-lookup"><span data-stu-id="8f7eb-122">Using structured EventSource events</span></span>

<span data-ttu-id="8f7eb-123">Ogni evento negli esempi di codice di questa sezione è definito per un caso specifico, ad esempio, quando viene registrato un tipo di servizio.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-123">Each of the events in the code examples in this section are defined for a specific case, for example, when a service type is registered.</span></span> <span data-ttu-id="8f7eb-124">Quando si definiscono i messaggi in base al caso di utilizzo, è possibile creare pacchetti dei dati e con il testo dell'errore, quindi eseguire ricerche e applicare filtri con maggiore facilità in base ai nomi o ai valori delle proprietà specificate.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-124">When you define messages by use case, data can be packaged with the text of the error, and you can more easily search and filter based on the names or values of the specified properties.</span></span> <span data-ttu-id="8f7eb-125">Strutturando l'output della strumentazione è possibile usarlo con più facilità, ma ciò richiede sforzi maggiori per definire un nuovo evento per ciascun caso d'uso.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-125">Structuring the instrumentation output makes it easier to consume, but requires more thought and time to define a new event for each use case.</span></span> <span data-ttu-id="8f7eb-126">Alcune definizioni di evento possono essere condivise nell'intera applicazione.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-126">Some event definitions can be shared across the entire application.</span></span> <span data-ttu-id="8f7eb-127">Un evento di avvio o arresto di un metodo, ad esempio, può essere riutilizzato in molti servizi in un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-127">For example, a method start or stop event would be reused across many services within an application.</span></span> <span data-ttu-id="8f7eb-128">Un servizio specifico per un dominio, ad esempio un sistema di ordine, può avere un evento **CreateOrder**, che ha un proprio evento univoco.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-128">A domain-specific service, like an order system, might have a **CreateOrder** event, which has its own unique event.</span></span> <span data-ttu-id="8f7eb-129">Questo approccio può generare un numero elevato di eventi e può potenzialmente richiedere il coordinamento degli identificatori tra i team di progetto.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-129">This approach might generate many events, and potentially require coordination of identifiers across project teams.</span></span> 

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // The instance constructor is private to enforce singleton semantics.
        private ServiceEventSource() : base() { }

        ...

        // The ServiceTypeRegistered event contains a unique identifier, an event attribute that defined the event, and the code implementation of the event.
        private const int ServiceTypeRegisteredEventId = 3;
        [Event(ServiceTypeRegisteredEventId, Level = EventLevel.Informational, Message = "Service host process {0} registered service type {1}", Keywords = Keywords.ServiceInitialization)]
        public void ServiceTypeRegistered(int hostProcessId, string serviceType)
        {
            WriteEvent(ServiceTypeRegisteredEventId, hostProcessId, serviceType);
        }

        // The ServiceHostInitializationFailed event contains a unique identifier, an event attribute that defined the event, and the code implementation of the event.
        private const int ServiceHostInitializationFailedEventId = 4;
        [Event(ServiceHostInitializationFailedEventId, Level = EventLevel.Error, Message = "Service host initialization failed", Keywords = Keywords.ServiceInitialization)]
        public void ServiceHostInitializationFailed(string exception)
        {
            WriteEvent(ServiceHostInitializationFailedEventId, exception);
        }
```

### <a name="using-eventsource-generically"></a><span data-ttu-id="8f7eb-130">Uso generico di EventSource</span><span class="sxs-lookup"><span data-stu-id="8f7eb-130">Using EventSource generically</span></span>

<span data-ttu-id="8f7eb-131">Poiché può essere difficile definire eventi specifici, molti utenti ne definiscono pochi con un set di parametri in comune che generalmente genera le informazioni sotto forma di stringa.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-131">Because defining specific events can be difficult, many people define a few events with a common set of parameters that generally output their information as a string.</span></span> <span data-ttu-id="8f7eb-132">Gran parte dell'aspetto strutturato viene persa, rendendo più difficili le ricerche e i filtri dei risultati.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-132">Much of the structured aspect is lost, and it's more difficult to search and filter the results.</span></span> <span data-ttu-id="8f7eb-133">In questo approccio vengono definiti alcuni eventi, in genere corrispondenti ai livelli di registrazione.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-133">In this approach, a few events that usually correspond to the logging levels are defined.</span></span> <span data-ttu-id="8f7eb-134">Il frammento seguente definisce un messaggio di debug e di errore:</span><span class="sxs-lookup"><span data-stu-id="8f7eb-134">The following snippet defines a debug and error message:</span></span>

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // The Instance constructor is private, to enforce singleton semantics.
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

<span data-ttu-id="8f7eb-135">Anche un ibrido di strumentazione strutturata e generica può essere una soluzione ideale.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-135">Using a hybrid of structured and generic instrumentation also can work well.</span></span> <span data-ttu-id="8f7eb-136">La strumentazione strutturata viene usata per la segnalazione degli errori e per le metriche.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-136">Structured instrumentation is used for reporting errors and metrics.</span></span> <span data-ttu-id="8f7eb-137">Gli eventi generici possono essere usati per la registrazione dettagliata utilizzata dai tecnici per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-137">Generic events can be used for the detailed logging that is consumed by engineers for troubleshooting.</span></span>

## <a name="aspnet-core-logging"></a><span data-ttu-id="8f7eb-138">Registrazione di ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="8f7eb-138">ASP.NET Core logging</span></span>

<span data-ttu-id="8f7eb-139">È importante pianificare con attenzione la strumentazione del codice.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-139">It's important to carefully plan how you will instrument your code.</span></span> <span data-ttu-id="8f7eb-140">Il piano di strumentazione corretto può consentire di evitare la potenziale destabilizzazione della codebase e la conseguente necessità di ripetere la strumentazione del codice.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-140">The right instrumentation plan can help you avoid potentially destabilizing your code base, and then needing to reinstrument the code.</span></span> <span data-ttu-id="8f7eb-141">Per ridurre il rischio, è possibile scegliere una libreria di strumentazione come [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), inclusa in Microsoft ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-141">To reduce risk, you can choose an instrumentation library like [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), which is part of Microsoft ASP.NET Core.</span></span> <span data-ttu-id="8f7eb-142">ASP.NET Core ha un'interfaccia [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) che può essere usata con il provider preferito, riducendo al minimo l'effetto sul codice esistente.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-142">ASP.NET Core has an [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) interface that you can use with the provider of your choice, while minimizing the effect on existing code.</span></span> <span data-ttu-id="8f7eb-143">È possibile usare il codice in ASP.NET Core in Windows e Linux e in .NET Framework completo, in modo da standardizzare la strumentazione del codice.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-143">You can use the code in ASP.NET Core on Windows and Linux, and in the full .NET Framework, so your instrumentation code is standardized.</span></span> <span data-ttu-id="8f7eb-144">Ciò viene approfondito di seguito:</span><span class="sxs-lookup"><span data-stu-id="8f7eb-144">This is further explored below:</span></span>

### <a name="using-microsoftextensionslogging-in-service-fabric"></a><span data-ttu-id="8f7eb-145">Uso di Microsoft.Extensions.Logging in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8f7eb-145">Using Microsoft.Extensions.Logging in Service Fabric</span></span>

1. <span data-ttu-id="8f7eb-146">Aggiungere il pacchetto Microsoft.Extensions.Logging NuGet al progetto da strumentare.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-146">Add the Microsoft.Extensions.Logging NuGet package to the project you want to instrument.</span></span> <span data-ttu-id="8f7eb-147">Aggiungere anche eventuali pacchetti del provider. Per un pacchetto di terze parti, vedere l'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-147">Also, add any provider packages (for a third-party package, see the following example).</span></span> <span data-ttu-id="8f7eb-148">Per altre informazioni, vedere [Logging in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging) (Registrazione in ASP.NET Core).</span><span class="sxs-lookup"><span data-stu-id="8f7eb-148">For more information, see [Logging in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging).</span></span>
2. <span data-ttu-id="8f7eb-149">Aggiungere una direttiva **using** per Microsoft.Extensions.Logging al file del servizio.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-149">Add a **using** directive for Microsoft.Extensions.Logging to your service file.</span></span>
3. <span data-ttu-id="8f7eb-150">Definire una variabile privata all'interno della classe di servizio.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-150">Define a private variable within your service class.</span></span>

  ```csharp
  private ILogger _logger = null;

  ```
4. <span data-ttu-id="8f7eb-151">Nel costruttore della classe del servizio aggiungere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="8f7eb-151">In the constructor of your service class, add this code:</span></span>

  ```csharp
  _logger = new LoggerFactory().CreateLogger<Stateless>();

  ```
5. <span data-ttu-id="8f7eb-152">Avviare la strumentazione del codice nei metodi.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-152">Start instrumenting your code in your methods.</span></span> <span data-ttu-id="8f7eb-153">Ecco alcuni esempi:</span><span class="sxs-lookup"><span data-stu-id="8f7eb-153">Here are a few samples:</span></span>

  ```csharp
  _logger.LogDebug("Debug-level event from Microsoft.Logging");
  _logger.LogInformation("Informational-level event from Microsoft.Logging");

  // In this variant, we're adding structured properties RequestName and Duration, which have values MyRequest and the duration of the request.
  // Later in the article, we discuss why this step is useful.
  _logger.LogInformation("{RequestName} {Duration}", "MyRequest", requestDuration);

  ```

## <a name="using-other-logging-providers"></a><span data-ttu-id="8f7eb-154">Uso di altri provider di registrazione</span><span class="sxs-lookup"><span data-stu-id="8f7eb-154">Using other logging providers</span></span>

<span data-ttu-id="8f7eb-155">Alcuni provider di terze parti usano l'approccio descritto nella sezione precedente, inclusi [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/) e [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging).</span><span class="sxs-lookup"><span data-stu-id="8f7eb-155">Some third-party providers use the approach described in the preceding section, including [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), and [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging).</span></span> <span data-ttu-id="8f7eb-156">È possibile inserirli tutti nella registrazione ASP.NET Core oppure usarli separatamente.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-156">You can plug each of these into ASP.NET Core logging, or you can use them separately.</span></span> <span data-ttu-id="8f7eb-157">Serilog offre una funzionalità che arricchisce tutti i messaggi inviati da un logger.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-157">Serilog has a feature that enriches all messages sent from a logger.</span></span> <span data-ttu-id="8f7eb-158">Questa funzionalità può essere utile per restituire il nome del servizio, il tipo e le informazioni sulla partizione.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-158">This feature can be useful to output the service name, type, and partition information.</span></span> <span data-ttu-id="8f7eb-159">Per usare questa funzionalità nell'infrastruttura di ASP.NET Core, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="8f7eb-159">To use this capability in the ASP.NET Core infrastructure, do these steps:</span></span>

1. <span data-ttu-id="8f7eb-160">Aggiungere i pacchetti NuGet Serilog, Serilog.Extensions.Logging e Serilog.Sinks.Observable al progetto.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-160">Add the Serilog, Serilog.Extensions.Logging, and Serilog.Sinks.Observable NuGet packages to the project.</span></span> <span data-ttu-id="8f7eb-161">Per l'esempio successivo aggiungere anche Serilog.Sinks.Literate.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-161">For the next example, also add Serilog.Sinks.Literate.</span></span> <span data-ttu-id="8f7eb-162">Un approccio migliore viene illustrato più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-162">A better approach is shown later in this article.</span></span>
2. <span data-ttu-id="8f7eb-163">In Serilog creare LoggerConfiguration e l'istanza del logger.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-163">In Serilog, create a LoggerConfiguration and the logger instance.</span></span>

  ```csharp
  Log.Logger = new LoggerConfiguration().WriteTo.LiterateConsole().CreateLogger();
  ```

3. <span data-ttu-id="8f7eb-164">Aggiungere un argomento SeriLog.ILogger al costruttore del servizio e passare il logger appena creato.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-164">Add a Serilog.ILogger argument to the service constructor, and pass the newly created logger.</span></span>

  ```csharp
  ServiceRuntime.RegisterServiceAsync("StatelessType", context => new Stateless(context, Log.Logger)).GetAwaiter().GetResult();
  ```

4. <span data-ttu-id="8f7eb-165">Nel costruttore del servizio aggiungere il codice seguente che crea il necessario per arricchire le proprietà **ServiceTypeName**, **ServiceName**, **PartitionId** e **InstanceId** del servizio.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-165">In the service constructor, add the following code, which creates the property enrichers for the **ServiceTypeName**, **ServiceName**, **PartitionId**, and **InstanceId** properties of the service.</span></span> <span data-ttu-id="8f7eb-166">Aggiunge anche un enricher delle proprietà alla struttura di registrazione di ASP.NET Core, per consentire di usare Microsoft.Extensions.Logging.ILogger nel codice.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-166">It also adds a property enricher to the ASP.NET Core logging factory, so you can use Microsoft.Extensions.Logging.ILogger in your code.</span></span>

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

5. <span data-ttu-id="8f7eb-167">Instrumentare il codice come se si stesse usando ASP.NET Core senza Serilog.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-167">Instrument the code the same as if you were using ASP.NET Core without Serilog.</span></span>

  >[!NOTE]
  ><span data-ttu-id="8f7eb-168">È consigliabile non usare Log.Logger statico con l'esempio precedente.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-168">We recommend that you don't use the static Log.Logger with the preceding example.</span></span> <span data-ttu-id="8f7eb-169">Service Fabric può ospitare più istanze dello stesso tipo di servizio in un singolo processo.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-169">Service Fabric can host multiple instances of the same service type within a single process.</span></span> <span data-ttu-id="8f7eb-170">Se si usa Log.Logger statico, l'ultimo writer degli enricher delle proprietà mostrerà i valori per tutte le istanze in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-170">If you use the static Log.Logger, the last writer of the property enrichers will show values for all instances that are running.</span></span> <span data-ttu-id="8f7eb-171">Questo è un motivo per cui la variabile _logger è una variabile di membro privata della classe di servizio.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-171">This is one reason why the _logger variable is a private member variable of the service class.</span></span> <span data-ttu-id="8f7eb-172">È anche necessario rendere disponibile _logger al codice comune, che potrebbe essere usato nei servizi.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-172">Also, you must make the _logger available to common code, which might be used across services.</span></span>

## <a name="choosing-a-logging-provider"></a><span data-ttu-id="8f7eb-173">Scelta di un provider di registrazione</span><span class="sxs-lookup"><span data-stu-id="8f7eb-173">Choosing a logging provider</span></span>

<span data-ttu-id="8f7eb-174">Se l'applicazione si basa sulle prestazioni elevate, **EventSource** è in genere l'approccio ottimale.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-174">If your application relies on high performance, **EventSource** is usually a good approach.</span></span> <span data-ttu-id="8f7eb-175">**EventSource** usa *in genere* un numero minore di risorse e offre prestazioni migliori rispetto alla registrazione di ASP.NET Core o di eventuali soluzioni di terze parti disponibili.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-175">**EventSource** *generally* uses fewer resources and performs better than ASP.NET Core logging or any of the available third-party solutions.</span></span>  <span data-ttu-id="8f7eb-176">Non è un problema per molti servizi, ma se il servizio è orientato alle prestazioni **EventSource** si rivela la scelta più indicata.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-176">This isn't an issue for many services, but if your service is performance-oriented, using **EventSource** might be a better choice.</span></span> <span data-ttu-id="8f7eb-177">Tuttavia per ottenere questi vantaggi della registrazione strutturata, **EventSource** richiede un investimento maggiore da parte del team tecnico.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-177">However, to get these benefits of structured logging, **EventSource** requires a larger investment from your engineering team.</span></span> <span data-ttu-id="8f7eb-178">Se possibile, effettuare un rapido prototipo di alcune opzioni di registrazione e quindi scegliere quello che meglio soddisfa le esigenze dell'utente.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-178">If possible, do a quick prototype of a few logging options, and then choose the one that best meets your needs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f7eb-179">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8f7eb-179">Next steps</span></span>

<span data-ttu-id="8f7eb-180">Dopo aver scelto il provider di accesso per instrumentare le applicazioni e i servizi, è necessario aggregare i log e gli eventi prima di inviarli a una piattaforma.</span><span class="sxs-lookup"><span data-stu-id="8f7eb-180">Once you have chosen your logging provider to instrument your applications and services, your logs and events need to be aggregated before they can be sent to any analysis platform.</span></span> <span data-ttu-id="8f7eb-181">Per meglio comprendere alcune delle opzioni consigliate leggere altre informazioni su [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) e [WAD](service-fabric-diagnostics-event-aggregation-wad.md).</span><span class="sxs-lookup"><span data-stu-id="8f7eb-181">Read about [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) and [WAD](service-fabric-diagnostics-event-aggregation-wad.md) to better understand some of the recommended options.</span></span>
