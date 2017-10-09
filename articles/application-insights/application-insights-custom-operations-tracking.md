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
# <a name="track-custom-operations-with-application-insights-net-sdk"></a>Verifica delle operazioni personalizzate con Application Insights .NET SDK

Azure Application Insights SDK automaticamente traccia in cui le richieste HTTP in ingresso e chiama toodependent servizi, ad esempio le richieste HTTP e query SQL. Rilevamento e la correlazione delle richieste e le dipendenze ottenere visibilità in tempi di risposta e l'affidabilità hello intera applicazione in tutti i microservizi che combinano l'applicazione. 

Esiste una classe di modelli di applicazione che non può essere supportata in modo generico. Per il corretto monitoraggio di tali modelli, è necessaria la strumentazione manuale del codice. Questo articolo descrive alcuni criteri che potrebbero richiedere una strumentazione manuale, ad esempio per l’elaborazione di code personalizzate e l'esecuzione prolungata di attività in background.

Questo documento fornisce istruzioni su come tootrack operazioni personalizzate con hello Application Insights SDK. Questa documentazione è relativa a:

- Application Insights per .NET (noto anche come Base SDK) versione 2.4+.
- Application Insights per applicazioni Web (che esegue ASP.NET) versione 2.4+.
- Application Insights per ASP.NET Core versione 2.1+.

## <a name="overview"></a>Panoramica
Un'operazione è un lavoro logico eseguito da un'applicazione. Sono indicati nome, ora di avvio, durata, risultato e contesto dell'esecuzione, ad esempio nome utente, proprietà e risultato. Se l'operazione A è stata avviata dall'operazione B, l'operazione B è impostata come elemento padre per A. Un'operazione può avere un solo padre, ma può avere molte operazioni figlio. Per ulteriori informazioni sulle operazioni e la correlazione dei dati di telemetria, vedere [Correlazione dei dati di telemetria di Azure Application Insights](application-insights-correlation.md).

In Application Insights .NET SDK hello, hello operazione è descritta dalla classe astratta hello [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) e dei relativi discendenti [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) e [DependencyTelemetry ](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).

## <a name="incoming-operations-tracking"></a>Verifica delle operazioni in ingresso 
Hello web Application Insights che SDK raccoglie automaticamente le richieste HTTP per le applicazioni in esecuzione in una pipeline IIS e tutte le applicazioni ASP.NET Core. Sono disponibili soluzioni supportate dalla community per altre piattaforme e altri framework. Tuttavia, se un'applicazione hello non è supportata da alcun standard hello o soluzioni supportate community, è possibile instrumentare il manualmente.

Un altro esempio che richiede di rilevamento personalizzato è lavoro hello che riceve gli elementi dalla coda hello. Per alcuni le code, hello chiamare tooadd un messaggio toothis coda viene registrata come una dipendenza. Tuttavia, operazioni di livello elevato di hello che descrive l'elaborazione dei messaggi non vengono raccolti automaticamente.

Di seguito viene illustrato come è possibile tenere traccia di tali operazioni.

In un livello elevato, l'attività hello è toocreate `RequestTelemetry` e impostare le proprietà di note. Al termine dell'operazione di hello, controllare la telemetria hello. Hello di esempio seguente è illustrata questa attività.

### <a name="http-request-in-owin-self-hosted-app"></a>Richiesta HTTP nell'app con self-hosting Owin
In questo esempio, si seguirà hello [il protocollo HTTP per la correlazione](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md). È possibile aspettarsi intestazioni tooreceive descritte non esiste.

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

il protocollo HTTP per la correlazione Hello dichiara inoltre hello `Correlation-Context` intestazione. Tuttavia, è omesso qui per motivi di semplicità.

## <a name="queue-instrumentation"></a>Strumentazione della coda
Per le comunicazioni HTTP, un protocollo abbiamo creato i dettagli di correlazione toopass. Con i protocolli di alcune delle code, è possibile passare i metadati aggiuntivi con il messaggio hello e con altri utenti che non è possibile.

### <a name="service-bus-queue"></a>Coda del bus di servizio
Con hello Azure [coda di Service Bus](../service-bus-messaging/index.md), è possibile passare un contenitore di proprietà con il messaggio hello. Usato da ID di correlazione toopass hello.

coda di Service Bus Hello Usa i protocolli basati su TCP. Application Insights non tiene traccia automaticamente delle operazioni della coda, quindi ne viene tenuta traccia manualmente. rimozione dalla coda Hello operazione è un'API di tipo push e siamo tootrack non è possibile.

#### <a name="enqueue"></a>Accodare

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

#### <a name="process"></a>Process
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

### <a name="azure-storage-queue"></a>Coda di archiviazione di Azure
Hello seguente esempio viene illustrato come hello tootrack [coda di archiviazione di Azure](../storage/queues/storage-dotnet-how-to-use-queues.md) operazioni e correlare dati di telemetria tra producer hello, consumer hello e archiviazione di Azure. 

coda di archiviazione Hello ha un'API HTTP. Coda di toohello tutte le chiamate vengono rilevate dall'agente di raccolta di Application Insights dipendenza di hello per le richieste HTTP.
Assicurarsi di avere `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer` in `applicationInsights.config`. Se non lo è disponibile, aggiungerlo a livello di programmazione come descritto in [il filtraggio e la pre-elaborazione in hello Azure Application Insights SDK](app-insights-api-filtering-sampling.md).

Se si configura Application Insights manualmente, creare e inizializzare `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` in modo simile a:
 
``` C#
DependencyTrackingTelemetryModule module = new DependencyTrackingTelemetryModule();

// You can prevent correlation header injection toosome domains by adding it toohello excluded list.
// Make sure you add a Storage endpoint. Otherwise, you might experience request signature validation issues on hello Storage service side.
module.ExcludeComponentCorrelationHttpHeadersOnDomains.Add("core.windows.net");
module.Initialize(TelemetryConfiguration.Active);

// Do not forget toodispose of hello module during application shutdown.
```

È anche consigliabile ID operazione di Application Insights toocorrelate hello con ID di hello archiviazione richiesta. Per informazioni su come tooset e ottenere una risorsa di archiviazione richiesta client e un ID richiesta server, vedere [Monitor, diagnosticare e risolvere i problemi di archiviazione di Azure](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).

#### <a name="enqueue"></a>Accodare
Poiché le code di archiviazione supportano hello API HTTP, tutte le operazioni con coda hello vengono rilevate automaticamente da Application Insights. In molti casi, questa strumentazione dovrebbe essere sufficiente. Tuttavia, toocorrelate esegue la traccia sul lato consumer hello con tracce produttori, è necessario passare un contesto di correlazione in modo analogo toohow si procede in hello protocollo HTTP per la correlazione. 

In questo esempio, si traccia hello facoltativo `Enqueue` operazione. È possibile:

 - **Correlare i tentativi (se presente)**: hanno un elemento padre comune che è hello `Enqueue` operazione. In caso contrario, se si tiene traccia come elementi figlio della richiesta in ingresso hello. Se sono presenti più code di toohello richieste logico, potrebbe essere difficile toofind quale la chiamata ha prodotto tentativi.
 - **Correlare i log di archiviazione (se e quando necessario)** con i dati di telemetria di Application Insights.

Hello `Enqueue` l'operazione è figlio di hello di un'operazione padre (ad esempio, una richiesta HTTP in ingresso). chiamata della dipendenza Hello HTTP è figlio di hello di hello `Enqueue` nipote hello e di operazione di richiesta in ingresso hello:

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

quantità di hello tooreduce di telemetria dell'applicazione report o se non si desidera hello tootrack `Enqueue` operazione per altri motivi, utilizzare hello `Activity` direttamente l'API:

- Creazione (e avviare) un nuovo `Activity` anziché iniziare l'operazione di Application Insights hello. Si *non* necessario tooassign qualsiasi proprietà, tranne che il nome di operazione hello.
- Serializzare `yourActivity.Id` nel payload del messaggio hello anziché `operation.Telemetry.Id`. È anche possibile usare `Activity.Current.Id`.


#### <a name="dequeue"></a>Rimuovere dalla coda
Allo stesso modo troppo`Enqueue`, una coda di archiviazione toohello di richiesta HTTP effettiva viene automaticamente rilevata da Application Insights. Tuttavia, hello `Enqueue` operazione presumibilmente viene eseguita nel contesto padre hello, ad esempio un contesto di richiesta in ingresso. Application Insights SDK correlare automaticamente tale operazione (e la parte HTTP) con richiesta padre hello e altri dati di telemetria segnalati in hello stesso ambito.

Hello `Dequeue` operazione è un'operazione complessa. Hello Application Insights SDK tiene automaticamente traccia delle richieste HTTP. Tuttavia, non conoscere il contesto di correlazione hello fino a quando non viene analizzato il messaggio hello. Non è messaggio hello tooget toocorrelate possibili hello HTTP richiesta con rest hello di telemetria hello.

In molti casi, potrebbe essere utile toocorrelate hello HTTP richiesta toohello coda nonché altre tracce. Hello esempio seguente viene illustrato come toodo è:

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

#### <a name="process"></a>Process

Nell'esempio seguente di hello, si traccia un messaggio in arrivo in modo simile toohow si traccia HTTP in ingresso richiesta:

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

Analogamente, è possibile instrumentare le altre operazioni della coda. L'operazione di visualizzazione deve essere instrumentata in modo simile a quella di rimozione dalla coda. Non è necessario instrumentare operazioni di gestione della coda. Application Insights tiene traccia di operazioni come HTTP e nella maggior parte dei casi è sufficiente.

Quando si esegue la strumentazione di eliminazione dei messaggi, assicurarsi di impostare operazione hello identificatori (correlazione). In alternativa, è possibile utilizzare hello `Activity` API. Quindi non è necessario tooset gli identificatori di operazione su elementi di dati di telemetria hello perché tale operazione Application Insights per l'utente:

- Creare un nuovo `Activity` dopo aver ottenuto un elemento dalla coda hello.
- Utilizzare `Activity.SetParentId(message.ParentId)` toocorrelate consumer e producer registri.
- Avviare hello `Activity`.
- Tenere traccia delle operazioni di rimozione dalla coda, elaborazione ed eliminazione usando gli helper `Start/StopOperation`. Eseguire l'operazione da hello stesso asincrona controllare il flusso (contesto di esecuzione). In questo modo la correlazione sarà corretta.
- Arresto hello `Activity`.
- Usare `Start/StopOperation` o chiamare `Track` telemetry manualmente.

### <a name="batch-processing"></a>Elaborazione batch
Per alcune code, è possibile una rimozione dalla coda di più messaggi con una singola richiesta. L'elaborazione di tali messaggi è presumibilmente indipendente e appartiene toohello diverse operazioni logiche. In questo caso, non è possibile toocorrelate hello `Dequeue` l'elaborazione dei messaggi di operazione tooparticular.

Ogni elaborazione dei messaggi deve essere eseguita nel proprio flusso di controllo asincrono. Per ulteriori informazioni, vedere hello [dipendenze in uscita rilevamento](#outgoing-dependencies-tracking) sezione.

## <a name="long-running-background-tasks"></a>Attività in background a esecuzione prolungata
Alcune applicazioni avviano operazioni a esecuzione prolungata che possono essere causate dalle richieste degli utenti. Dalla prospettiva di strumentazione di traccia/hello, non è diverso dalla richiesta o la dipendenza di strumentazione: 

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

In questo esempio, si usa `telemetryClient.StartOperation` toocreate `RequestTelemetry` e il contesto di correlazione hello riempimento. Si supponga che si dispone di un'operazione padre che è stata creata da richieste in ingresso che hello operazione pianificata. Purché `BackgroundTask` avviato hello stesso flusso di controllo asincrono come una richiesta in ingresso, è correlato a tale operazione padre. `BackgroundTask`e tutti gli elementi di telemetria nidificata automaticamente sono correlati con richiesta di hello che lo ha causato, anche dopo il termine richiesta hello.

Avvio dell'attività hello da thread in background hello privo di qualsiasi operazione (`Activity`) associati, `BackgroundTask` non dispone di qualsiasi elemento padre. Tuttavia, può avere operazioni annidate. Tutti gli elementi di dati di telemetria segnalati dall'attività hello sono correlato toohello `RequestTelemetry` creato in `BackgroundTask`.

## <a name="outgoing-dependencies-tracking"></a>Verifica delle dipendenze in uscita
È possibile tenere traccia della propria tipologia di dipendenza o di operazioni non supportate da Application Insights.

Hello `Enqueue` metodo nella coda di Service Bus hello o coda di archiviazione hello può essere utilizzato come esempi per tale rilevamento personalizzato.

Hello approccio generale per tenere traccia delle dipendenze personalizzato consiste nel:

- Chiamare hello `TelemetryClient.StartOperation` (metodo) (estensione) che riempie hello `DependencyTelemetry` proprietà necessarie per la correlazione e altre proprietà (ora di inizio stamp, durata).
- Impostare altre proprietà personalizzata hello `DependencyTelemetry`, ad esempio nome hello e qualsiasi altro contesto, è necessario.
- Effettuare una chiamata di dipendenza e attendere.
- Arrestare l'operazione di hello con `StopOperation` al termine.
- Gestire le eccezioni.

`StopOperation`Arresta solo l'operazione di hello che è stato avviato. Se l'operazione corrente in esecuzione hello non corrisponde a hello uno desiderato toostop, `StopOperation` non esegue alcuna operazione. Questa situazione potrebbe verificarsi se si avvia più operazioni in parallelo in hello stesso contesto di esecuzione:

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

È quindi necessario assicurarsi di chiamare sempre `StartOperation` e di eseguire l'attività nel contesto corretto:
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

## <a name="next-steps"></a>Passaggi successivi

- Nozioni di base hello di [correlazione telemetria](application-insights-correlation.md) in Application Insights.
- Vedere hello [modello di dati](application-insights-data-model.md) per un modello di tipi e i dati di Application Insights.
- Report personalizzati [eventi e metriche](app-insights-api-custom-events-metrics.md) tooApplication Insights.
- Estrarre la [configurazione](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) standard di una raccolta di proprietà di contesto.
- Controllare hello [manuale dell'utente System.Diagnostics.Activity](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) toosee come vengono messi in correlazione telemetria.
