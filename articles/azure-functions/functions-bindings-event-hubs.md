---
title: associazioni di hub di eventi di funzioni aaaAzure | Documenti Microsoft
description: Comprendere come le associazioni di hub eventi di Azure toouse nelle funzioni di Azure.
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: Funzioni di Azure, Funzioni, elaborazione eventi, calcolo dinamico, architettura senza server
ms.assetid: daf81798-7acc-419a-bc32-b5a41c6db56b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/20/2017
ms.author: wesmc
ms.openlocfilehash: e864f032ad5ac58d318c9843c3844b5642733a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-event-hubs-bindings"></a><span data-ttu-id="40575-104">Associazioni di Hub eventi in Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="40575-104">Azure Functions Event Hubs bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="40575-105">Questo articolo viene illustrato come tooconfigure e utilizzare [hub eventi di Azure](../event-hubs/event-hubs-what-is-event-hubs.md) associazioni per le funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="40575-105">This article explains how tooconfigure and use [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) bindings for Azure Functions.</span></span>
<span data-ttu-id="40575-106">Funzioni di Azure supporta il trigger e le associazioni di output per Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="40575-106">Azure Functions supports trigger and output bindings for Event Hubs.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="40575-107">Nel caso di nuovo hub di eventi tooAzure, vedere hello [Panoramica di hub eventi](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="40575-107">If you are new tooAzure Event Hubs, see hello [Event Hubs overview](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

<a name="trigger"></a>

## <a name="event-hub-trigger"></a><span data-ttu-id="40575-108">Trigger di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="40575-108">Event hub trigger</span></span>
<span data-ttu-id="40575-109">Utilizzare gli hub di eventi hello attivare toorespond tooan evento flusso di eventi di hub eventi tooan inviato.</span><span class="sxs-lookup"><span data-stu-id="40575-109">Use hello Event Hubs trigger toorespond tooan event sent tooan event hub event stream.</span></span> <span data-ttu-id="40575-110">È necessario disporre dell'accesso in lettura toohello evento hub tooset dei trigger hello.</span><span class="sxs-lookup"><span data-stu-id="40575-110">You must have read access toohello event hub tooset up hello trigger.</span></span>

<span data-ttu-id="40575-111">trigger di funzione Hello hub eventi Usa hello seguente oggetto JSON nella hello `bindings` matrice function.json:</span><span class="sxs-lookup"><span data-stu-id="40575-111">hello Event Hubs function trigger uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHubTrigger",
    "name": "<Name of trigger parameter in function signature>",
    "direction": "in",
    "path": "<Name of hello event hub>",
    "consumerGroup": "Consumer group toouse - see below",
    "connection": "<Name of app setting with connection string - see below>"
}
```

<span data-ttu-id="40575-112">`consumerGroup`è un hello tooset proprietà facoltativa utilizzata [gruppo di consumer](../event-hubs/event-hubs-features.md#event-consumers) utilizzato toosubscribe tooevents nell'hub hello.</span><span class="sxs-lookup"><span data-stu-id="40575-112">`consumerGroup` is an optional property used tooset hello [consumer group](../event-hubs/event-hubs-features.md#event-consumers) used toosubscribe tooevents in hello hub.</span></span> <span data-ttu-id="40575-113">Se omesso, hello `$Default` viene utilizzato il gruppo di consumer.</span><span class="sxs-lookup"><span data-stu-id="40575-113">If omitted, hello `$Default` consumer group is used.</span></span>  
<span data-ttu-id="40575-114">`connection`deve essere hello nome di un'impostazione di app che contiene lo spazio dei nomi hello connessione stringa toohello dell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="40575-114">`connection` must be hello name of an app setting that contains hello connection string toohello event hub's namespace.</span></span>
<span data-ttu-id="40575-115">Copiare la stringa di connessione, fare clic su hello **informazioni di connessione** pulsante per hello *dello spazio dei nomi*, non hello hub di eventi stesso.</span><span class="sxs-lookup"><span data-stu-id="40575-115">Copy this connection string by clicking hello **Connection Information** button for hello *namespace*, not hello event hub itself.</span></span> <span data-ttu-id="40575-116">La stringa di connessione deve disporre almeno di lettura trigger hello tooactivate di autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="40575-116">This connection string must have at least read permissions tooactivate hello trigger.</span></span>

<span data-ttu-id="40575-117">[Impostazioni aggiuntive](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) può essere fornito in un host.json toofurther file fine ottimizzare gli hub di eventi trigger.</span><span class="sxs-lookup"><span data-stu-id="40575-117">[Additional settings](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) can be provided in a host.json file toofurther fine tune Event Hubs triggers.</span></span>  

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="40575-118">Uso dei trigger</span><span class="sxs-lookup"><span data-stu-id="40575-118">Trigger usage</span></span>
<span data-ttu-id="40575-119">Quando una funzione di hub di eventi trigger viene attivata, il messaggio hello che lo attiva viene passato alla funzione hello sotto forma di stringa.</span><span class="sxs-lookup"><span data-stu-id="40575-119">When an Event Hubs trigger function is triggered, hello message that triggers it is passed into hello function as a string.</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="40575-120">Esempio di trigger</span><span class="sxs-lookup"><span data-stu-id="40575-120">Trigger sample</span></span>
<span data-ttu-id="40575-121">Si supponga di avere hello seguenti hub di eventi trigger hello `bindings` matrice function.json:</span><span class="sxs-lookup"><span data-stu-id="40575-121">Suppose you have hello following Event Hubs trigger in hello `bindings` array of function.json:</span></span>

```json
{
  "type": "eventHubTrigger",
  "name": "myEventHubMessage",
  "direction": "in",
  "path": "MyEventHub",
  "connection": "myEventHubReadConnectionString"
}
```

<span data-ttu-id="40575-122">Vedere l'esempio specifico del linguaggio hello che registra corpo del messaggio hello del trigger di hub eventi hello.</span><span class="sxs-lookup"><span data-stu-id="40575-122">See hello language-specific sample that logs hello message body of hello event hub trigger.</span></span>

* [<span data-ttu-id="40575-123">C#</span><span class="sxs-lookup"><span data-stu-id="40575-123">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="40575-124">F#</span><span class="sxs-lookup"><span data-stu-id="40575-124">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="40575-125">Node.JS</span><span class="sxs-lookup"><span data-stu-id="40575-125">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="40575-126">Esempio di trigger in C#</span><span class="sxs-lookup"><span data-stu-id="40575-126">Trigger sample in C#</span></span> #

```cs
using System;

public static void Run(string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

<span data-ttu-id="40575-127">È inoltre possibile ricevere eventi hello come un [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) oggetto, che consente di accedere ai metadati di evento toohello.</span><span class="sxs-lookup"><span data-stu-id="40575-127">You can also receive hello event as an [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) object, which gives you access toohello event metadata.</span></span>

```cs
#r "Microsoft.ServiceBus"
using System.Text;
using Microsoft.ServiceBus.Messaging;

public static void Run(EventData myEventHubMessage, TraceWriter log)
{
    log.Info($"{Encoding.UTF8.GetString(myEventHubMessage.GetBytes())}");
}
```

<span data-ttu-id="40575-128">tooreceive eventi in un batch, modificare la firma del metodo hello troppo`string[]` o `EventData[]`.</span><span class="sxs-lookup"><span data-stu-id="40575-128">tooreceive events in a batch, change hello method signature too`string[]` or `EventData[]`.</span></span>

```cs
public static void Run(string[] eventHubMessages, TraceWriter log)
{
    foreach (var message in eventHubMessages)
    {
        log.Info($"C# Event Hub trigger function processed a message: {message}");
    }
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a><span data-ttu-id="40575-129">Esempio di trigger in F#</span><span class="sxs-lookup"><span data-stu-id="40575-129">Trigger sample in F#</span></span> #

```fsharp
let Run(myEventHubMessage: string, log: TraceWriter) =
    log.Info(sprintf "F# eventhub trigger function processed work item: %s" myEventHubMessage)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="40575-130">Esempio di trigger in Node.js</span><span class="sxs-lookup"><span data-stu-id="40575-130">Trigger sample in Node.js</span></span>

```javascript
module.exports = function (context, myEventHubMessage) {
    context.log('Node.js eventhub trigger function processed work item', myEventHubMessage);    
    context.done();
};
```

<a name="output"></a>

## <a name="event-hubs-output-binding"></a><span data-ttu-id="40575-131">Associazione di output di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="40575-131">Event Hubs output binding</span></span>
<span data-ttu-id="40575-132">Associazione toowrite eventi tooan evento hub eventi flusso di output di hello utilizzare gli hub di eventi.</span><span class="sxs-lookup"><span data-stu-id="40575-132">Use hello Event Hubs output binding toowrite events tooan event hub event stream.</span></span> <span data-ttu-id="40575-133">È necessario disporre di trasmissione autorizzazione tooan evento hub toowrite eventi tooit.</span><span class="sxs-lookup"><span data-stu-id="40575-133">You must have send permission tooan event hub toowrite events tooit.</span></span>

<span data-ttu-id="40575-134">associazione di output Hello utilizza hello seguente oggetto JSON nella hello `bindings` matrice function.json:</span><span class="sxs-lookup"><span data-stu-id="40575-134">hello output binding uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHub",
    "name": "<Name of output parameter in function signature>",
    "path": "<Name of event hub>",
    "connection": "<Name of app setting with connection string - see below>"
    "direction": "out"
}
```

<span data-ttu-id="40575-135">`connection`deve essere hello nome di un'impostazione di app che contiene lo spazio dei nomi hello connessione stringa toohello dell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="40575-135">`connection` must be hello name of an app setting that contains hello connection string toohello event hub's namespace.</span></span>
<span data-ttu-id="40575-136">Copiare la stringa di connessione, fare clic su hello **informazioni di connessione** pulsante per hello *dello spazio dei nomi*, non hello hub di eventi stesso.</span><span class="sxs-lookup"><span data-stu-id="40575-136">Copy this connection string by clicking hello **Connection Information** button for hello *namespace*, not hello event hub itself.</span></span> <span data-ttu-id="40575-137">Questa stringa di connessione deve avere flusso di eventi di trasmissione autorizzazioni toosend hello messaggio toohello.</span><span class="sxs-lookup"><span data-stu-id="40575-137">This connection string must have send permissions toosend hello message toohello event stream.</span></span>

## <a name="output-usage"></a><span data-ttu-id="40575-138">Uso dell'output</span><span class="sxs-lookup"><span data-stu-id="40575-138">Output usage</span></span>
<span data-ttu-id="40575-139">In questa sezione viene illustrato come toouse gli hub di eventi di output di associazione nel codice di funzione.</span><span class="sxs-lookup"><span data-stu-id="40575-139">This section shows you how toouse your Event Hubs output binding in your function code.</span></span>

<span data-ttu-id="40575-140">È possibile creare hub di eventi di messaggi toohello configurato con i seguenti tipi di parametro hello:</span><span class="sxs-lookup"><span data-stu-id="40575-140">You can output messages toohello configured event hub with hello following parameter types:</span></span>

* `out string`
* <span data-ttu-id="40575-141">`ICollector<string>`(toooutput più messaggi)</span><span class="sxs-lookup"><span data-stu-id="40575-141">`ICollector<string>` (toooutput multiple messages)</span></span>
* <span data-ttu-id="40575-142">`IAsyncCollector<string>` (versione asincrona di `ICollector<T>`)</span><span class="sxs-lookup"><span data-stu-id="40575-142">`IAsyncCollector<string>` (async version of `ICollector<T>`)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="40575-143">Esempio di output</span><span class="sxs-lookup"><span data-stu-id="40575-143">Output sample</span></span>
<span data-ttu-id="40575-144">Si supponga di avere seguito hello hub eventi di output dell'associazione in hello `bindings` matrice function.json:</span><span class="sxs-lookup"><span data-stu-id="40575-144">Suppose you have hello following Event Hubs output binding in hello `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHub",
    "name": "outputEventHubMessage",
    "path": "myeventhub",
    "connection": "MyEventHubSend",
    "direction": "out"
}
```

<span data-ttu-id="40575-145">Vedere l'esempio specifico del linguaggio hello che scrive un flusso di eventi toohello anche.</span><span class="sxs-lookup"><span data-stu-id="40575-145">See hello language-specific sample that writes an event toohello even stream.</span></span>

* [<span data-ttu-id="40575-146">C#</span><span class="sxs-lookup"><span data-stu-id="40575-146">C#</span></span>](#outcsharp)
* [<span data-ttu-id="40575-147">F#</span><span class="sxs-lookup"><span data-stu-id="40575-147">F#</span></span>](#outfsharp)
* [<span data-ttu-id="40575-148">Node.JS</span><span class="sxs-lookup"><span data-stu-id="40575-148">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="40575-149">Esempio di output in C#</span><span class="sxs-lookup"><span data-stu-id="40575-149">Output sample in C#</span></span> #

```cs
using System;

public static void Run(TimerInfo myTimer, out string outputEventHubMessage, TraceWriter log)
{
    String msg = $"TimerTriggerCSharp1 executed at: {DateTime.Now}";
    log.Verbose(msg);   
    outputEventHubMessage = msg;
}
```

<span data-ttu-id="40575-150">In alternativa, toocreate più messaggi:</span><span class="sxs-lookup"><span data-stu-id="40575-150">Or, toocreate multiple messages:</span></span>

```cs
public static void Run(TimerInfo myTimer, ICollector<string> outputEventHubMessage, TraceWriter log)
{
    string message = $"Event Hub message created at: {DateTime.Now}";
    log.Info(message);
    outputEventHubMessage.Add("1 " + message);
    outputEventHubMessage.Add("2 " + message);
}
```

<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a><span data-ttu-id="40575-151">Esempio di output in F#</span><span class="sxs-lookup"><span data-stu-id="40575-151">Output sample in F#</span></span> #

```fsharp
let Run(myTimer: TimerInfo, outputEventHubMessage: byref<string>, log: TraceWriter) =
    let msg = sprintf "TimerTriggerFSharp1 executed at: %s" DateTime.Now.ToString()
    log.Verbose(msg);
    outputEventHubMessage <- msg;
```

<a name="outnodejs"></a>

### <a name="output-sample-for-nodejs"></a><span data-ttu-id="40575-152">Esempio di output in Node.js</span><span class="sxs-lookup"><span data-stu-id="40575-152">Output sample for Node.js</span></span>

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();
    context.log('Event Hub message created at: ', timeStamp);   
    context.bindings.outputEventHubMessage = "Event Hub message created at: " + timeStamp;
    context.done();
};
```

<span data-ttu-id="40575-153">In alternativa, toosend più messaggi,</span><span class="sxs-lookup"><span data-stu-id="40575-153">Or, toosend multiple messages,</span></span>

```javascript
module.exports = function(context) {
    var timeStamp = new Date().toISOString();
    var message = 'Event Hub message created at: ' + timeStamp;

    context.bindings.outputEventHubMessage = [];

    context.bindings.outputEventHubMessage.push("1 " + message);
    context.bindings.outputEventHubMessage.push("2 " + message);
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="40575-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="40575-154">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
