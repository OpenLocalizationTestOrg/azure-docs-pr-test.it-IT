---
title: aaaTrack operazioni personalizzate con Azure Application Insights .NET SDK | Documenti Microsoft
description: Verifica delle operazioni personalizzate con Azure Application Insights .NET SDK
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 06/31/2017
ms.author: sergkanz
ms.openlocfilehash: fe338d3e2b17a3dae43c96c60a19f57b3f46f0a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="track-custom-operations-with-application-insights-net-sdk"></a><span data-ttu-id="fd387-103">Verifica delle operazioni personalizzate con Application Insights .NET SDK</span><span class="sxs-lookup"><span data-stu-id="fd387-103">Track custom operations with Application Insights .NET SDK</span></span>

<span data-ttu-id="fd387-104">Azure Application Insights SDK automaticamente traccia in cui le richieste HTTP in ingresso e chiama toodependent servizi, ad esempio le richieste HTTP e query SQL.</span><span class="sxs-lookup"><span data-stu-id="fd387-104">Azure Application Insights SDKs automatically track incoming HTTP requests and calls toodependent services, such as HTTP requests and SQL queries.</span></span> <span data-ttu-id="fd387-105">Rilevamento e la correlazione delle richieste e le dipendenze ottenere visibilità in tempi di risposta e l'affidabilità hello intera applicazione in tutti i microservizi che combinano l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="fd387-105">Tracking and correlation of requests and dependencies give you visibility into hello whole application's responsiveness and reliability across all microservices that combine this application.</span></span> 

<span data-ttu-id="fd387-106">Esiste una classe di modelli di applicazione che non può essere supportata in modo generico.</span><span class="sxs-lookup"><span data-stu-id="fd387-106">There is a class of application patterns that can't be supported generically.</span></span> <span data-ttu-id="fd387-107">Per il corretto monitoraggio di tali modelli, è necessaria la strumentazione manuale del codice.</span><span class="sxs-lookup"><span data-stu-id="fd387-107">Proper monitoring of such patterns requires manual code instrumentation.</span></span> <span data-ttu-id="fd387-108">Questo articolo descrive alcuni criteri che potrebbero richiedere una strumentazione manuale, ad esempio per l’elaborazione di code personalizzate e l'esecuzione prolungata di attività in background.</span><span class="sxs-lookup"><span data-stu-id="fd387-108">This article covers a few patterns that might require manual instrumentation, such as custom queue processing and running long-running background tasks.</span></span>

<span data-ttu-id="fd387-109">Questo documento fornisce istruzioni su come tootrack operazioni personalizzate con hello Application Insights SDK.</span><span class="sxs-lookup"><span data-stu-id="fd387-109">This document provides guidance on how tootrack custom operations with hello Application Insights SDK.</span></span> <span data-ttu-id="fd387-110">Questa documentazione è relativa a:</span><span class="sxs-lookup"><span data-stu-id="fd387-110">This documentation is relevant for:</span></span>

- <span data-ttu-id="fd387-111">Application Insights per .NET (noto anche come Base SDK) versione 2.4+.</span><span class="sxs-lookup"><span data-stu-id="fd387-111">Application Insights for .NET (also known as Base SDK) version 2.4+.</span></span>
- <span data-ttu-id="fd387-112">Application Insights per applicazioni Web (che esegue ASP.NET) versione 2.4+.</span><span class="sxs-lookup"><span data-stu-id="fd387-112">Application Insights for web applications (running ASP.NET) version 2.4+.</span></span>
- <span data-ttu-id="fd387-113">Application Insights per ASP.NET Core versione 2.1+.</span><span class="sxs-lookup"><span data-stu-id="fd387-113">Application Insights for ASP.NET Core version 2.1+.</span></span>

## <a name="overview"></a><span data-ttu-id="fd387-114">Panoramica</span><span class="sxs-lookup"><span data-stu-id="fd387-114">Overview</span></span>
<span data-ttu-id="fd387-115">Un'operazione è un lavoro logico eseguito da un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="fd387-115">An operation is a logical piece of work run by an application.</span></span> <span data-ttu-id="fd387-116">Sono indicati nome, ora di avvio, durata, risultato e contesto dell'esecuzione, ad esempio nome utente, proprietà e risultato.</span><span class="sxs-lookup"><span data-stu-id="fd387-116">It has a name, start time, duration, result, and a context of execution like user name, properties, and result.</span></span> <span data-ttu-id="fd387-117">Se l'operazione A è stata avviata dall'operazione B, l'operazione B è impostata come elemento padre per A. Un'operazione può avere un solo padre, ma può avere molte operazioni figlio.</span><span class="sxs-lookup"><span data-stu-id="fd387-117">If operation A was initiated by operation B, then operation B is set as a parent for A. An operation can have only one parent, but it can have many child operations.</span></span> <span data-ttu-id="fd387-118">Per ulteriori informazioni sulle operazioni e la correlazione dei dati di telemetria, vedere [Correlazione dei dati di telemetria di Azure Application Insights](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="fd387-118">For more information on operations and telemetry correlation, see [Azure Application Insights telemetry correlation](application-insights-correlation.md).</span></span>

<span data-ttu-id="fd387-119">In Application Insights .NET SDK hello, hello operazione è descritta dalla classe astratta hello [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) e dei relativi discendenti [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) e [DependencyTelemetry ](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).</span><span class="sxs-lookup"><span data-stu-id="fd387-119">In hello Application Insights .NET SDK, hello operation is described by hello abstract class [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) and its descendants [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) and [DependencyTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).</span></span>

## <a name="incoming-operations-tracking"></a><span data-ttu-id="fd387-120">Verifica delle operazioni in ingresso</span><span class="sxs-lookup"><span data-stu-id="fd387-120">Incoming operations tracking</span></span> 
<span data-ttu-id="fd387-121">Hello web Application Insights che SDK raccoglie automaticamente le richieste HTTP per le applicazioni in esecuzione in una pipeline IIS e tutte le applicazioni ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="fd387-121">hello Application Insights web SDK automatically collects HTTP requests for ASP.NET applications that run in an IIS pipeline and all ASP.NET Core applications.</span></span> <span data-ttu-id="fd387-122">Sono disponibili soluzioni supportate dalla community per altre piattaforme e altri framework.</span><span class="sxs-lookup"><span data-stu-id="fd387-122">There are community-supported solutions for other platforms and frameworks.</span></span> <span data-ttu-id="fd387-123">Tuttavia, se un'applicazione hello non è supportata da alcun standard hello o soluzioni supportate community, è possibile instrumentare il manualmente.</span><span class="sxs-lookup"><span data-stu-id="fd387-123">However, if hello application isn't supported by any of hello standard or community-supported solutions, you can instrument it manually.</span></span>

<span data-ttu-id="fd387-124">Un altro esempio che richiede di rilevamento personalizzato è lavoro hello che riceve gli elementi dalla coda hello.</span><span class="sxs-lookup"><span data-stu-id="fd387-124">Another example that requires custom tracking is hello worker that receives items from hello queue.</span></span> <span data-ttu-id="fd387-125">Per alcuni le code, hello chiamare tooadd un messaggio toothis coda viene registrata come una dipendenza.</span><span class="sxs-lookup"><span data-stu-id="fd387-125">For some queues, hello call tooadd a message toothis queue is tracked as a dependency.</span></span> <span data-ttu-id="fd387-126">Tuttavia, operazioni di livello elevato di hello che descrive l'elaborazione dei messaggi non vengono raccolti automaticamente.</span><span class="sxs-lookup"><span data-stu-id="fd387-126">However, hello high-level operation that describes message processing is not automatically collected.</span></span>

<span data-ttu-id="fd387-127">Di seguito viene illustrato come è possibile tenere traccia di tali operazioni.</span><span class="sxs-lookup"><span data-stu-id="fd387-127">Let's see how we can track such operations.</span></span>

<span data-ttu-id="fd387-128">In un livello elevato, l'attività hello è toocreate `RequestTelemetry` e impostare le proprietà di note.</span><span class="sxs-lookup"><span data-stu-id="fd387-128">On a high level, hello task is toocreate `RequestTelemetry` and set known properties.</span></span> <span data-ttu-id="fd387-129">Al termine dell'operazione di hello, controllare la telemetria hello.</span><span class="sxs-lookup"><span data-stu-id="fd387-129">After hello operation is finished, you track hello telemetry.</span></span> <span data-ttu-id="fd387-130">Hello di esempio seguente è illustrata questa attività.</span><span class="sxs-lookup"><span data-stu-id="fd387-130">hello following example demonstrates this task.</span></span>

### <a name="http-request-in-owin-self-hosted-app"></a><span data-ttu-id="fd387-131">Richiesta HTTP nell'app con self-hosting Owin</span><span class="sxs-lookup"><span data-stu-id="fd387-131">HTTP request in Owin self-hosted app</span></span>
<span data-ttu-id="fd387-132">In questo esempio, si seguirà hello [il protocollo HTTP per la correlazione](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md).</span><span class="sxs-lookup"><span data-stu-id="fd387-132">In this example, we follow hello [HTTP Protocol for Correlation](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md).</span></span> <span data-ttu-id="fd387-133">È possibile aspettarsi intestazioni tooreceive descritte non esiste.</span><span class="sxs-lookup"><span data-stu-id="fd387-133">You should expect tooreceive headers that are described there.</span></span>

``` C#
public class ApplicationInsightsMiddleware : OwinMiddleware
{
    private readonly TelemetryClient telemetryClient = new TelemetryClient(TelemetryConfiguration.Active);
    
    public ApplicationInsightsMiddleware(OwinMiddleware next) : base(next) {}

    public override async Task Invoke(IOwinContext context)
    {
        // Let's create and start RequestTelemetry.
        var requestTelemetry = new RequestTelemetry
        {
            Name = $"{context.Request.Method} {context.Request.Uri.GetLeftPart(UriPartial.Path)}"
        };

        // If there is a Request-Id received from hello upstream service, set hello telemetry context accordingly.
        if (context.Request.Headers.ContainsKey("Request-Id"))
        {
            var requestId = context.Request.Headers.Get("Request-Id");
            // Get hello operation ID from hello Request-Id (if you follow hello HTTP Protocol for Correlation).
            requestTelemetry.Context.Operation.Id = GetOperationId(requestId);
            requestTelemetry.Context.Operation.ParentId = requestId;
        }

        // StartOperation is a helper method that allows correlation of 
        // current operations with nested operations/telemetry
        // and initializes start time and duration on telemetry items.
        var operation = telemetryClient.StartOperation(requestTelemetry);

        // Process hello request.
        try
        {
            await Next.Invoke(context);
        }
        catch (Exception e)
        {
            requestTelemetry.Success = false;
            telemetryClient.TrackException(e);
            throw;
        }
        finally
        {
            // Update status code and success as appropriate.
            if (context.Response != null)
            {
                requestTelemetry.ResponseCode = context.Response.StatusCode.ToString();
                requestTelemetry.Success = context.Response.StatusCode >= 200 && context.Response.StatusCode <= 299;
            }
            else
            {
                requestTelemetry.Success = false;
            }

            // Now it's time toostop hello operation (and track telemetry).
            telemetryClient.StopOperation(operation);
        }
    }
    
    public static string GetOperationId(string id)
    {
        // Returns hello root ID from hello '|' toohello first '.' if any.
        int rootEnd = id.IndexOf('.');
        if (rootEnd < 0)
            rootEnd = id.Length;

        int rootStart = id[0] == '|' ? 1 : 0;
        return id.Substring(rootStart, rootEnd - rootStart);
    }
}
```

<span data-ttu-id="fd387-134">il protocollo HTTP per la correlazione Hello dichiara inoltre hello `Correlation-Context` intestazione.</span><span class="sxs-lookup"><span data-stu-id="fd387-134">hello HTTP Protocol for Correlation also declares hello `Correlation-Context` header.</span></span> <span data-ttu-id="fd387-135">Tuttavia, è omesso qui per motivi di semplicità.</span><span class="sxs-lookup"><span data-stu-id="fd387-135">However, it's omitted here for simplicity.</span></span>

## <a name="queue-instrumentation"></a><span data-ttu-id="fd387-136">Strumentazione della coda</span><span class="sxs-lookup"><span data-stu-id="fd387-136">Queue instrumentation</span></span>
<span data-ttu-id="fd387-137">Per le comunicazioni HTTP, un protocollo abbiamo creato i dettagli di correlazione toopass.</span><span class="sxs-lookup"><span data-stu-id="fd387-137">For HTTP communication, we've created a protocol toopass correlation details.</span></span> <span data-ttu-id="fd387-138">Con i protocolli di alcune delle code, è possibile passare i metadati aggiuntivi con il messaggio hello e con altri utenti che non è possibile.</span><span class="sxs-lookup"><span data-stu-id="fd387-138">With some queues' protocols, you can pass additional metadata along with hello message, and with others you can't.</span></span>

### <a name="service-bus-queue"></a><span data-ttu-id="fd387-139">Coda del bus di servizio</span><span class="sxs-lookup"><span data-stu-id="fd387-139">Service Bus queue</span></span>
<span data-ttu-id="fd387-140">Con hello Azure [coda di Service Bus](../service-bus-messaging/index.md), è possibile passare un contenitore di proprietà con il messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="fd387-140">With hello Azure [Service Bus queue](../service-bus-messaging/index.md), you can pass a property bag along with hello message.</span></span> <span data-ttu-id="fd387-141">Usato da ID di correlazione toopass hello.</span><span class="sxs-lookup"><span data-stu-id="fd387-141">We use it toopass hello correlation ID.</span></span>

<span data-ttu-id="fd387-142">coda di Service Bus Hello Usa i protocolli basati su TCP.</span><span class="sxs-lookup"><span data-stu-id="fd387-142">hello Service Bus queue uses TCP-based protocols.</span></span> <span data-ttu-id="fd387-143">Application Insights non tiene traccia automaticamente delle operazioni della coda, quindi ne viene tenuta traccia manualmente.</span><span class="sxs-lookup"><span data-stu-id="fd387-143">Application Insights doesn't automatically track queue operations, so we track them manually.</span></span> <span data-ttu-id="fd387-144">rimozione dalla coda Hello operazione è un'API di tipo push e siamo tootrack non è possibile.</span><span class="sxs-lookup"><span data-stu-id="fd387-144">hello dequeue operation is a push-style API, and we're unable tootrack it.</span></span>

#### <a name="enqueue"></a><span data-ttu-id="fd387-145">Accodare</span><span class="sxs-lookup"><span data-stu-id="fd387-145">Enqueue</span></span>

```C#
public async Task Enqueue(string payload)
{
    // StartOperation is a helper method that initializes hello telemetry item
    // and allows correlation of this operation with its parent and children.
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("enqueue " + queueName);
    operation.Telemetry.Type = "Queue";
    operation.Telemetry.Data = "Enqueue " + queueName;

    var message = new BrokeredMessage(payload);
    // Service Bus queue allows hello property bag toopass along with hello message.
    // We will use them toopass our correlation identifiers (and other context)
    // toohello consumer.
    message.Properties.Add("ParentId", operation.Telemetry.Id);
    message.Properties.Add("RootId", operation.Telemetry.Context.Operation.Id);

    try
    {
        await queue.SendAsync(message);
        
        // Set operation.Telemetry Success and ResponseCode here.
        operation.Telemetry.Success = true;
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        // Set operation.Telemetry Success and ResponseCode here.
        operation.Telemetry.Success = false;
        throw;
    }
    finally
    {
        telemetryClient.StopOperation(operation);
    }
}
```

#### <a name="process"></a><span data-ttu-id="fd387-146">Process</span><span class="sxs-lookup"><span data-stu-id="fd387-146">Process</span></span>
```C#
public async Task Process(BrokeredMessage message)
{
    // After hello message is taken from hello queue, create RequestTelemetry tootrack its processing.
    // It might also make sense tooget hello name from hello message.
    RequestTelemetry requestTelemetry = new RequestTelemetry { Name = "Dequeue " + queueName };

    var rootId = message.Properties["RootId"].ToString();
    var parentId = message.Properties["ParentId"].ToString();
    // Get hello operation ID from hello Request-Id (if you follow hello HTTP Protocol for Correlation).
    requestTelemetry.Context.Operation.Id = rootId;
    requestTelemetry.Context.Operation.ParentId = parentId;

    var operation = telemetryClient.StartOperation(requestTelemetry);

    try
    {
        await ProcessMessage();
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        throw;
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetryClient.StopOperation(operation);
    }
}
```

### <a name="azure-storage-queue"></a><span data-ttu-id="fd387-147">Coda di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="fd387-147">Azure Storage queue</span></span>
<span data-ttu-id="fd387-148">Hello seguente esempio viene illustrato come hello tootrack [coda di archiviazione di Azure](../storage/queues/storage-dotnet-how-to-use-queues.md) operazioni e correlare dati di telemetria tra producer hello, consumer hello e archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="fd387-148">hello following example shows how tootrack hello [Azure Storage queue](../storage/queues/storage-dotnet-how-to-use-queues.md) operations and correlate telemetry between hello producer, hello consumer, and Azure Storage.</span></span> 

<span data-ttu-id="fd387-149">coda di archiviazione Hello ha un'API HTTP.</span><span class="sxs-lookup"><span data-stu-id="fd387-149">hello Storage queue has an HTTP API.</span></span> <span data-ttu-id="fd387-150">Coda di toohello tutte le chiamate vengono rilevate dall'agente di raccolta di Application Insights dipendenza di hello per le richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="fd387-150">All calls toohello queue are tracked by hello Application Insights Dependency Collector for HTTP requests.</span></span>
<span data-ttu-id="fd387-151">Assicurarsi di avere `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer` in `applicationInsights.config`.</span><span class="sxs-lookup"><span data-stu-id="fd387-151">Make sure you have `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer` in `applicationInsights.config`.</span></span> <span data-ttu-id="fd387-152">Se non lo è disponibile, aggiungerlo a livello di programmazione come descritto in [il filtraggio e la pre-elaborazione in hello Azure Application Insights SDK](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="fd387-152">If you don't have it, add it programmatically as described in [Filtering and Preprocessing in hello Azure Application Insights SDK](app-insights-api-filtering-sampling.md).</span></span>

<span data-ttu-id="fd387-153">Se si configura Application Insights manualmente, creare e inizializzare `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` in modo simile a:</span><span class="sxs-lookup"><span data-stu-id="fd387-153">If you configure Application Insights manually, make sure you create and initialize `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` similarly to:</span></span>
 
``` C#
DependencyTrackingTelemetryModule module = new DependencyTrackingTelemetryModule();

// You can prevent correlation header injection toosome domains by adding it toohello excluded list.
// Make sure you add a Storage endpoint. Otherwise, you might experience request signature validation issues on hello Storage service side.
module.ExcludeComponentCorrelationHttpHeadersOnDomains.Add("core.windows.net");
module.Initialize(TelemetryConfiguration.Active);

// Do not forget toodispose of hello module during application shutdown.
```

<span data-ttu-id="fd387-154">È anche consigliabile ID operazione di Application Insights toocorrelate hello con ID di hello archiviazione richiesta.</span><span class="sxs-lookup"><span data-stu-id="fd387-154">You also might want toocorrelate hello Application Insights operation ID with hello Storage request ID.</span></span> <span data-ttu-id="fd387-155">Per informazioni su come tooset e ottenere una risorsa di archiviazione richiesta client e un ID richiesta server, vedere [Monitor, diagnosticare e risolvere i problemi di archiviazione di Azure](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).</span><span class="sxs-lookup"><span data-stu-id="fd387-155">For information on how tooset and get a Storage request client and a server request ID, see [Monitor, diagnose, and troubleshoot Azure Storage](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).</span></span>

#### <a name="enqueue"></a><span data-ttu-id="fd387-156">Accodare</span><span class="sxs-lookup"><span data-stu-id="fd387-156">Enqueue</span></span>
<span data-ttu-id="fd387-157">Poiché le code di archiviazione supportano hello API HTTP, tutte le operazioni con coda hello vengono rilevate automaticamente da Application Insights.</span><span class="sxs-lookup"><span data-stu-id="fd387-157">Because Storage queues support hello HTTP API, all operations with hello queue are automatically tracked by Application Insights.</span></span> <span data-ttu-id="fd387-158">In molti casi, questa strumentazione dovrebbe essere sufficiente.</span><span class="sxs-lookup"><span data-stu-id="fd387-158">In many cases, this instrumentation should be enough.</span></span> <span data-ttu-id="fd387-159">Tuttavia, toocorrelate esegue la traccia sul lato consumer hello con tracce produttori, è necessario passare un contesto di correlazione in modo analogo toohow si procede in hello protocollo HTTP per la correlazione.</span><span class="sxs-lookup"><span data-stu-id="fd387-159">However, toocorrelate traces on hello consumer side with producer traces, you must pass some correlation context similarly toohow we do it in hello HTTP Protocol for Correlation.</span></span> 

<span data-ttu-id="fd387-160">In questo esempio, si traccia hello facoltativo `Enqueue` operazione.</span><span class="sxs-lookup"><span data-stu-id="fd387-160">In this example, we track hello optional `Enqueue` operation.</span></span> <span data-ttu-id="fd387-161">È possibile:</span><span class="sxs-lookup"><span data-stu-id="fd387-161">You can:</span></span>

 - <span data-ttu-id="fd387-162">**Correlare i tentativi (se presente)**: hanno un elemento padre comune che è hello `Enqueue` operazione.</span><span class="sxs-lookup"><span data-stu-id="fd387-162">**Correlate retries (if any)**: They all have one common parent that's hello `Enqueue` operation.</span></span> <span data-ttu-id="fd387-163">In caso contrario, se si tiene traccia come elementi figlio della richiesta in ingresso hello.</span><span class="sxs-lookup"><span data-stu-id="fd387-163">Otherwise, they're tracked as children of hello incoming request.</span></span> <span data-ttu-id="fd387-164">Se sono presenti più code di toohello richieste logico, potrebbe essere difficile toofind quale la chiamata ha prodotto tentativi.</span><span class="sxs-lookup"><span data-stu-id="fd387-164">If there are multiple logical requests toohello queue, it might be difficult toofind which call resulted in retries.</span></span>
 - <span data-ttu-id="fd387-165">**Correlare i log di archiviazione (se e quando necessario)** con i dati di telemetria di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="fd387-165">**Correlate Storage logs (if and when needed)**: They're correlated with Application Insights telemetry.</span></span>

<span data-ttu-id="fd387-166">Hello `Enqueue` l'operazione è figlio di hello di un'operazione padre (ad esempio, una richiesta HTTP in ingresso).</span><span class="sxs-lookup"><span data-stu-id="fd387-166">hello `Enqueue` operation is hello child of a parent operation (for example, an incoming HTTP request).</span></span> <span data-ttu-id="fd387-167">chiamata della dipendenza Hello HTTP è figlio di hello di hello `Enqueue` nipote hello e di operazione di richiesta in ingresso hello:</span><span class="sxs-lookup"><span data-stu-id="fd387-167">hello HTTP dependency call is hello child of hello `Enqueue` operation and hello grandchild of hello incoming request:</span></span>

```C#
public async Task Enqueue(CloudQueue queue, string message)
{
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("enqueue " + queue.Name);
    operation.Telemetry.Type = "Queue";
    operation.Telemetry.Data = "Enqueue " + queue.Name;

    // MessagePayload represents your custom message and also serializes correlation identifiers into payload.
    // For example, if you choose toopass payload serialized tooJSON, it might look like
    // {'RootId' : 'some-id', 'ParentId' : '|some-id.1.2.3.', 'message' : 'your message tooprocess'}
    var jsonPayload = JsonConvert.SerializeObject(new MessagePayload
    {
        RootId = operation.Telemetry.Context.Operation.Id,
        ParentId = operation.Telemetry.Id,
        Payload = message
    });
    
    CloudQueueMessage queueMessage = new CloudQueueMessage(jsonPayload);

    // Add operation.Telemetry.Id toohello OperationContext toocorrelate Storage logs and Application Insights telemetry.
    OperationContext context = new OperationContext { ClientRequestID = operation.Telemetry.Id};

    try
    {
        await queue.AddMessageAsync(queueMessage, null, null, new QueueRequestOptions(), context);
    }
    catch (StorageException e)
    {
        operation.Telemetry.Properties.Add("AzureServiceRequestID", e.RequestInformation.ServiceRequestID);
        operation.Telemetry.Success = false;
        operation.Telemetry.ResultCode = e.RequestInformation.HttpStatusCode.ToString();
        telemetryClient.TrackException(e);
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetryClient.StopOperation(operation);
    }
}  
```

<span data-ttu-id="fd387-168">quantità di hello tooreduce di telemetria dell'applicazione report o se non si desidera hello tootrack `Enqueue` operazione per altri motivi, utilizzare hello `Activity` direttamente l'API:</span><span class="sxs-lookup"><span data-stu-id="fd387-168">tooreduce hello amount of telemetry your application reports or if you don't want tootrack hello `Enqueue` operation for other reasons, use hello `Activity` API directly:</span></span>

- <span data-ttu-id="fd387-169">Creazione (e avviare) un nuovo `Activity` anziché iniziare l'operazione di Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="fd387-169">Create (and start) a new `Activity` instead of starting hello Application Insights operation.</span></span> <span data-ttu-id="fd387-170">Si *non* necessario tooassign qualsiasi proprietà, tranne che il nome di operazione hello.</span><span class="sxs-lookup"><span data-stu-id="fd387-170">You do *not* need tooassign any properties on it except hello operation name.</span></span>
- <span data-ttu-id="fd387-171">Serializzare `yourActivity.Id` nel payload del messaggio hello anziché `operation.Telemetry.Id`.</span><span class="sxs-lookup"><span data-stu-id="fd387-171">Serialize `yourActivity.Id` into hello message payload instead of `operation.Telemetry.Id`.</span></span> <span data-ttu-id="fd387-172">È anche possibile usare `Activity.Current.Id`.</span><span class="sxs-lookup"><span data-stu-id="fd387-172">You can also use `Activity.Current.Id`.</span></span>


#### <a name="dequeue"></a><span data-ttu-id="fd387-173">Rimuovere dalla coda</span><span class="sxs-lookup"><span data-stu-id="fd387-173">Dequeue</span></span>
<span data-ttu-id="fd387-174">Allo stesso modo troppo`Enqueue`, una coda di archiviazione toohello di richiesta HTTP effettiva viene automaticamente rilevata da Application Insights.</span><span class="sxs-lookup"><span data-stu-id="fd387-174">Similarly too`Enqueue`, an actual HTTP request toohello Storage queue is automatically tracked by Application Insights.</span></span> <span data-ttu-id="fd387-175">Tuttavia, hello `Enqueue` operazione presumibilmente viene eseguita nel contesto padre hello, ad esempio un contesto di richiesta in ingresso.</span><span class="sxs-lookup"><span data-stu-id="fd387-175">However, hello `Enqueue` operation presumably happens in hello parent context, such as an incoming request context.</span></span> <span data-ttu-id="fd387-176">Application Insights SDK correlare automaticamente tale operazione (e la parte HTTP) con richiesta padre hello e altri dati di telemetria segnalati in hello stesso ambito.</span><span class="sxs-lookup"><span data-stu-id="fd387-176">Application Insights SDKs automatically correlate such an operation (and its HTTP part) with hello parent request and other telemetry reported in hello same scope.</span></span>

<span data-ttu-id="fd387-177">Hello `Dequeue` operazione è un'operazione complessa.</span><span class="sxs-lookup"><span data-stu-id="fd387-177">hello `Dequeue` operation is tricky.</span></span> <span data-ttu-id="fd387-178">Hello Application Insights SDK tiene automaticamente traccia delle richieste HTTP.</span><span class="sxs-lookup"><span data-stu-id="fd387-178">hello Application Insights SDK automatically tracks HTTP requests.</span></span> <span data-ttu-id="fd387-179">Tuttavia, non conoscere il contesto di correlazione hello fino a quando non viene analizzato il messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="fd387-179">However, it doesn't know hello correlation context until hello message is parsed.</span></span> <span data-ttu-id="fd387-180">Non è messaggio hello tooget toocorrelate possibili hello HTTP richiesta con rest hello di telemetria hello.</span><span class="sxs-lookup"><span data-stu-id="fd387-180">It's not possible toocorrelate hello HTTP request tooget hello message with hello rest of hello telemetry.</span></span>

<span data-ttu-id="fd387-181">In molti casi, potrebbe essere utile toocorrelate hello HTTP richiesta toohello coda nonché altre tracce.</span><span class="sxs-lookup"><span data-stu-id="fd387-181">In many cases, it might be useful toocorrelate hello HTTP request toohello queue with other traces as well.</span></span> <span data-ttu-id="fd387-182">Hello esempio seguente viene illustrato come toodo è:</span><span class="sxs-lookup"><span data-stu-id="fd387-182">hello following example demonstrates how toodo it:</span></span>

``` C#
public async Task<MessagePayload> Dequeue(CloudQueue queue)
{
    var telemetry = new DependencyTelemetry
    {
        Type = "Queue",
        Name = "Dequeue " + queue.Name
    };

    telemetry.Start();

    try
    {
        var message = await queue.GetMessageAsync();

        if (message != null)
        {
            var payload = JsonConvert.DeserializeObject<MessagePayload>(message.AsString);

            // If there is a message, we want toocorrelate hello Dequeue operation with processing.
            // However, we will only know what correlation ID toouse after we get it from hello message,
            // so we will report telemetry after we know hello IDs.
            telemetry.Context.Operation.Id = payload.RootId;
            telemetry.Context.Operation.ParentId = payload.ParentId;

            // Delete hello message.
            return payload;
        }
    }
    catch (StorageException e)
    {
        telemetry.Properties.Add("AzureServiceRequestID", e.RequestInformation.ServiceRequestID);
        telemetry.Success = false;
        telemetry.ResultCode = e.RequestInformation.HttpStatusCode.ToString();
        telemetryClient.TrackException(e);
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetry.Stop();
        telemetryClient.Track(telemetry);
    }

    return null;
}
```

#### <a name="process"></a><span data-ttu-id="fd387-183">Process</span><span class="sxs-lookup"><span data-stu-id="fd387-183">Process</span></span>

<span data-ttu-id="fd387-184">Nell'esempio seguente di hello, si traccia un messaggio in arrivo in modo simile toohow si traccia HTTP in ingresso richiesta:</span><span class="sxs-lookup"><span data-stu-id="fd387-184">In hello following example, we trace an incoming message in a manner similarly toohow we trace an incoming HTTP request:</span></span>

```C#
public async Task Process(MessagePayload message)
{
    // After hello message is dequeued from hello queue, create RequestTelemetry tootrack its processing.
    RequestTelemetry requestTelemetry = new RequestTelemetry { Name = "Dequeue " + queueName };
    // It might also make sense tooget hello name from hello message.
    requestTelemetry.Context.Operation.Id = message.RootId;
    requestTelemetry.Context.Operation.ParentId = message.ParentId;

    var operation = telemetryClient.StartOperation(requestTelemetry);

    try
    {
        await ProcessMessage();
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        throw;
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetryClient.StopOperation(operation);
    }
}
```

<span data-ttu-id="fd387-185">Analogamente, è possibile instrumentare le altre operazioni della coda.</span><span class="sxs-lookup"><span data-stu-id="fd387-185">Similarly, other queue operations can be instrumented.</span></span> <span data-ttu-id="fd387-186">L'operazione di visualizzazione deve essere instrumentata in modo simile a quella di rimozione dalla coda.</span><span class="sxs-lookup"><span data-stu-id="fd387-186">A peek operation should be instrumented in a similar way as a dequeue operation.</span></span> <span data-ttu-id="fd387-187">Non è necessario instrumentare operazioni di gestione della coda.</span><span class="sxs-lookup"><span data-stu-id="fd387-187">Instrumenting queue management operations isn't necessary.</span></span> <span data-ttu-id="fd387-188">Application Insights tiene traccia di operazioni come HTTP e nella maggior parte dei casi è sufficiente.</span><span class="sxs-lookup"><span data-stu-id="fd387-188">Application Insights tracks operations such as HTTP, and in most cases, it's enough.</span></span>

<span data-ttu-id="fd387-189">Quando si esegue la strumentazione di eliminazione dei messaggi, assicurarsi di impostare operazione hello identificatori (correlazione).</span><span class="sxs-lookup"><span data-stu-id="fd387-189">When you instrument message deletion, make sure you set hello operation (correlation) identifiers.</span></span> <span data-ttu-id="fd387-190">In alternativa, è possibile utilizzare hello `Activity` API.</span><span class="sxs-lookup"><span data-stu-id="fd387-190">Alternatively, you can use hello `Activity` API.</span></span> <span data-ttu-id="fd387-191">Quindi non è necessario tooset gli identificatori di operazione su elementi di dati di telemetria hello perché tale operazione Application Insights per l'utente:</span><span class="sxs-lookup"><span data-stu-id="fd387-191">Then you don't need tooset operation identifiers on hello telemetry items because Application Insights does it for you:</span></span>

- <span data-ttu-id="fd387-192">Creare un nuovo `Activity` dopo aver ottenuto un elemento dalla coda hello.</span><span class="sxs-lookup"><span data-stu-id="fd387-192">Create a new `Activity` after you've got an item from hello queue.</span></span>
- <span data-ttu-id="fd387-193">Utilizzare `Activity.SetParentId(message.ParentId)` toocorrelate consumer e producer registri.</span><span class="sxs-lookup"><span data-stu-id="fd387-193">Use `Activity.SetParentId(message.ParentId)` toocorrelate consumer and producer logs.</span></span>
- <span data-ttu-id="fd387-194">Avviare hello `Activity`.</span><span class="sxs-lookup"><span data-stu-id="fd387-194">Start hello `Activity`.</span></span>
- <span data-ttu-id="fd387-195">Tenere traccia delle operazioni di rimozione dalla coda, elaborazione ed eliminazione usando gli helper `Start/StopOperation`.</span><span class="sxs-lookup"><span data-stu-id="fd387-195">Track dequeue, process, and delete operations by using `Start/StopOperation` helpers.</span></span> <span data-ttu-id="fd387-196">Eseguire l'operazione da hello stesso asincrona controllare il flusso (contesto di esecuzione).</span><span class="sxs-lookup"><span data-stu-id="fd387-196">Do it from hello same asynchronous control flow (execution context).</span></span> <span data-ttu-id="fd387-197">In questo modo la correlazione sarà corretta.</span><span class="sxs-lookup"><span data-stu-id="fd387-197">In this way, they're correlated properly.</span></span>
- <span data-ttu-id="fd387-198">Arresto hello `Activity`.</span><span class="sxs-lookup"><span data-stu-id="fd387-198">Stop hello `Activity`.</span></span>
- <span data-ttu-id="fd387-199">Usare `Start/StopOperation` o chiamare `Track` telemetry manualmente.</span><span class="sxs-lookup"><span data-stu-id="fd387-199">Use `Start/StopOperation`, or call `Track` telemetry manually.</span></span>

### <a name="batch-processing"></a><span data-ttu-id="fd387-200">Elaborazione batch</span><span class="sxs-lookup"><span data-stu-id="fd387-200">Batch processing</span></span>
<span data-ttu-id="fd387-201">Per alcune code, è possibile una rimozione dalla coda di più messaggi con una singola richiesta.</span><span class="sxs-lookup"><span data-stu-id="fd387-201">With some queues, you can dequeue multiple messages with one request.</span></span> <span data-ttu-id="fd387-202">L'elaborazione di tali messaggi è presumibilmente indipendente e appartiene toohello diverse operazioni logiche.</span><span class="sxs-lookup"><span data-stu-id="fd387-202">Processing such messages is presumably independent and belongs toohello different logical operations.</span></span> <span data-ttu-id="fd387-203">In questo caso, non è possibile toocorrelate hello `Dequeue` l'elaborazione dei messaggi di operazione tooparticular.</span><span class="sxs-lookup"><span data-stu-id="fd387-203">In this case, it's not possible toocorrelate hello `Dequeue` operation tooparticular message processing.</span></span>

<span data-ttu-id="fd387-204">Ogni elaborazione dei messaggi deve essere eseguita nel proprio flusso di controllo asincrono.</span><span class="sxs-lookup"><span data-stu-id="fd387-204">Each message should be processed in its own asynchronous control flow.</span></span> <span data-ttu-id="fd387-205">Per ulteriori informazioni, vedere hello [dipendenze in uscita rilevamento](#outgoing-dependencies-tracking) sezione.</span><span class="sxs-lookup"><span data-stu-id="fd387-205">For more information, see hello [Outgoing dependencies tracking](#outgoing-dependencies-tracking) section.</span></span>

## <a name="long-running-background-tasks"></a><span data-ttu-id="fd387-206">Attività in background a esecuzione prolungata</span><span class="sxs-lookup"><span data-stu-id="fd387-206">Long-running background tasks</span></span>
<span data-ttu-id="fd387-207">Alcune applicazioni avviano operazioni a esecuzione prolungata che possono essere causate dalle richieste degli utenti.</span><span class="sxs-lookup"><span data-stu-id="fd387-207">Some applications start long-running operations that might be caused by user requests.</span></span> <span data-ttu-id="fd387-208">Dalla prospettiva di strumentazione di traccia/hello, non è diverso dalla richiesta o la dipendenza di strumentazione:</span><span class="sxs-lookup"><span data-stu-id="fd387-208">From hello tracing/instrumentation perspective, it's not different from request or dependency instrumentation:</span></span> 

``` C#
async Task BackgroundTask()
{
    var operation = telemetryClient.StartOperation<RequestTelemetry>(taskName);
    operation.Telemetry.Type = "Background";
    try
    {
        int progress = 0;
        while (progress < 100)
        {
            // Process hello task.
            telemetryClient.TrackTrace($"done {progress++}%");
        }
        // Update status code and success as appropriate.
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        // Update status code and success as appropriate.
        throw;
    }
    finally
    {
        telemetryClient.StopOperation(operation);
    }
}
```

<span data-ttu-id="fd387-209">In questo esempio, si usa `telemetryClient.StartOperation` toocreate `RequestTelemetry` e il contesto di correlazione hello riempimento.</span><span class="sxs-lookup"><span data-stu-id="fd387-209">In this example, we use `telemetryClient.StartOperation` toocreate `RequestTelemetry` and fill hello correlation context.</span></span> <span data-ttu-id="fd387-210">Si supponga che si dispone di un'operazione padre che è stata creata da richieste in ingresso che hello operazione pianificata.</span><span class="sxs-lookup"><span data-stu-id="fd387-210">Let's say you have a parent operation that was created by incoming requests that scheduled hello operation.</span></span> <span data-ttu-id="fd387-211">Purché `BackgroundTask` avviato hello stesso flusso di controllo asincrono come una richiesta in ingresso, è correlato a tale operazione padre.</span><span class="sxs-lookup"><span data-stu-id="fd387-211">As long as `BackgroundTask` starts in hello same asynchronous control flow as an incoming request, it's correlated with that parent operation.</span></span> <span data-ttu-id="fd387-212">`BackgroundTask`e tutti gli elementi di telemetria nidificata automaticamente sono correlati con richiesta di hello che lo ha causato, anche dopo il termine richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="fd387-212">`BackgroundTask` and all nested telemetry items are automatically correlated with hello request that caused it, even after hello request ends.</span></span>

<span data-ttu-id="fd387-213">Avvio dell'attività hello da thread in background hello privo di qualsiasi operazione (`Activity`) associati, `BackgroundTask` non dispone di qualsiasi elemento padre.</span><span class="sxs-lookup"><span data-stu-id="fd387-213">When hello task starts from hello background thread that doesn't have any operation (`Activity`) associated with it, `BackgroundTask` doesn't have any parent.</span></span> <span data-ttu-id="fd387-214">Tuttavia, può avere operazioni annidate.</span><span class="sxs-lookup"><span data-stu-id="fd387-214">However, it can have nested operations.</span></span> <span data-ttu-id="fd387-215">Tutti gli elementi di dati di telemetria segnalati dall'attività hello sono correlato toohello `RequestTelemetry` creato in `BackgroundTask`.</span><span class="sxs-lookup"><span data-stu-id="fd387-215">All telemetry items reported from hello task are correlated toohello `RequestTelemetry` created in `BackgroundTask`.</span></span>

## <a name="outgoing-dependencies-tracking"></a><span data-ttu-id="fd387-216">Verifica delle dipendenze in uscita</span><span class="sxs-lookup"><span data-stu-id="fd387-216">Outgoing dependencies tracking</span></span>
<span data-ttu-id="fd387-217">È possibile tenere traccia della propria tipologia di dipendenza o di operazioni non supportate da Application Insights.</span><span class="sxs-lookup"><span data-stu-id="fd387-217">You can track your own dependency kind or an operation that's not supported by Application Insights.</span></span>

<span data-ttu-id="fd387-218">Hello `Enqueue` metodo nella coda di Service Bus hello o coda di archiviazione hello può essere utilizzato come esempi per tale rilevamento personalizzato.</span><span class="sxs-lookup"><span data-stu-id="fd387-218">hello `Enqueue` method in hello Service Bus queue or hello Storage queue can serve as examples for such custom tracking.</span></span>

<span data-ttu-id="fd387-219">Hello approccio generale per tenere traccia delle dipendenze personalizzato consiste nel:</span><span class="sxs-lookup"><span data-stu-id="fd387-219">hello general approach for custom dependency tracking is to:</span></span>

- <span data-ttu-id="fd387-220">Chiamare hello `TelemetryClient.StartOperation` (metodo) (estensione) che riempie hello `DependencyTelemetry` proprietà necessarie per la correlazione e altre proprietà (ora di inizio stamp, durata).</span><span class="sxs-lookup"><span data-stu-id="fd387-220">Call hello `TelemetryClient.StartOperation` (extension) method that fills hello `DependencyTelemetry` properties that are needed for correlation and some other properties (start  time stamp, duration).</span></span>
- <span data-ttu-id="fd387-221">Impostare altre proprietà personalizzata hello `DependencyTelemetry`, ad esempio nome hello e qualsiasi altro contesto, è necessario.</span><span class="sxs-lookup"><span data-stu-id="fd387-221">Set other custom properties on hello `DependencyTelemetry`, such as hello name and any other context you need.</span></span>
- <span data-ttu-id="fd387-222">Effettuare una chiamata di dipendenza e attendere.</span><span class="sxs-lookup"><span data-stu-id="fd387-222">Make a dependency call and wait for it.</span></span>
- <span data-ttu-id="fd387-223">Arrestare l'operazione di hello con `StopOperation` al termine.</span><span class="sxs-lookup"><span data-stu-id="fd387-223">Stop hello operation with `StopOperation` when it's finished.</span></span>
- <span data-ttu-id="fd387-224">Gestire le eccezioni.</span><span class="sxs-lookup"><span data-stu-id="fd387-224">Handle exceptions.</span></span>

<span data-ttu-id="fd387-225">`StopOperation`Arresta solo l'operazione di hello che è stato avviato.</span><span class="sxs-lookup"><span data-stu-id="fd387-225">`StopOperation` only stops hello operation that was started.</span></span> <span data-ttu-id="fd387-226">Se l'operazione corrente in esecuzione hello non corrisponde a hello uno desiderato toostop, `StopOperation` non esegue alcuna operazione.</span><span class="sxs-lookup"><span data-stu-id="fd387-226">If hello current running operation doesn't match hello one you want toostop, `StopOperation` does nothing.</span></span> <span data-ttu-id="fd387-227">Questa situazione potrebbe verificarsi se si avvia più operazioni in parallelo in hello stesso contesto di esecuzione:</span><span class="sxs-lookup"><span data-stu-id="fd387-227">This situation might happen if you start multiple operations in parallel in hello same execution context:</span></span>

```C#
var firstOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
var firstOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
var firstTask = RunMyTaskAsync();

var secondOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 2");
var secondTask = RunMyTaskAsync();

await firstTask;

// This will do nothing and will not report telemetry for hello first operation
// as currently secondOperation is active.
telemetryClient.StopOperation(firstOperation); 

await secondTask;
```

<span data-ttu-id="fd387-228">È quindi necessario assicurarsi di chiamare sempre `StartOperation` e di eseguire l'attività nel contesto corretto:</span><span class="sxs-lookup"><span data-stu-id="fd387-228">Make sure you always call `StartOperation` and run your task in its own context:</span></span>
```C#
public async Task RunMyTaskAsync()
{
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
    try 
    {
        var myTask = await StartMyTaskAsync();
        // Update status code and success as appropriate.
    }
    catch(...) 
    {
        // Update status code and success as appropriate.
    }
    finally 
    {
        telemetryClient.StopOperation(operation);
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="fd387-229">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fd387-229">Next steps</span></span>

- <span data-ttu-id="fd387-230">Nozioni di base hello di [correlazione telemetria](application-insights-correlation.md) in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="fd387-230">Learn hello basics of [telemetry correlation](application-insights-correlation.md) in Application Insights.</span></span>
- <span data-ttu-id="fd387-231">Vedere hello [modello di dati](application-insights-data-model.md) per un modello di tipi e i dati di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="fd387-231">See hello [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="fd387-232">Report personalizzati [eventi e metriche](app-insights-api-custom-events-metrics.md) tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="fd387-232">Report custom [events and metrics](app-insights-api-custom-events-metrics.md) tooApplication Insights.</span></span>
- <span data-ttu-id="fd387-233">Estrarre la [configurazione](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) standard di una raccolta di proprietà di contesto.</span><span class="sxs-lookup"><span data-stu-id="fd387-233">Check out standard [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) for context properties collection.</span></span>
- <span data-ttu-id="fd387-234">Controllare hello [manuale dell'utente System.Diagnostics.Activity](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) toosee come vengono messi in correlazione telemetria.</span><span class="sxs-lookup"><span data-stu-id="fd387-234">Check hello [System.Diagnostics.Activity User Guide](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) toosee how we correlate telemetry.</span></span>
