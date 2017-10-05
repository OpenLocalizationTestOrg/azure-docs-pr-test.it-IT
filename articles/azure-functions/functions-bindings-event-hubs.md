---
title: Associazioni di Hub eventi in Funzioni di Azure | Microsoft Docs
description: Informazioni su come usare le associazioni di Hub eventi di Azure in Funzioni di Azure.
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
ms.openlocfilehash: 19021bef8b7156b3049f43b0275c0ed0c6b22514
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-event-hubs-bindings"></a><span data-ttu-id="d08ea-104">Associazioni di Hub eventi in Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="d08ea-104">Azure Functions Event Hubs bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="d08ea-105">Questo articolo illustra come configurare e usare le associazioni di [Hub eventi di Azure](../event-hubs/event-hubs-what-is-event-hubs.md) in Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="d08ea-105">This article explains how to configure and use [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) bindings for Azure Functions.</span></span>
<span data-ttu-id="d08ea-106">Funzioni di Azure supporta il trigger e le associazioni di output per Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="d08ea-106">Azure Functions supports trigger and output bindings for Event Hubs.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="d08ea-107">Se non si ha familiarità con Hub eventi di Azure, vedere la [panoramica di Hub eventi](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="d08ea-107">If you are new to Azure Event Hubs, see the [Event Hubs overview](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

<a name="trigger"></a>

## <a name="event-hub-trigger"></a><span data-ttu-id="d08ea-108">Trigger di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="d08ea-108">Event hub trigger</span></span>
<span data-ttu-id="d08ea-109">È possibile usare il trigger di Hub eventi per rispondere a un evento inviato a un flusso di eventi di Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="d08ea-109">Use the Event Hubs trigger to respond to an event sent to an event hub event stream.</span></span> <span data-ttu-id="d08ea-110">Per configurare il trigger è necessario avere accesso in lettura ad Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="d08ea-110">You must have read access to the event hub to set up the trigger.</span></span>

<span data-ttu-id="d08ea-111">Il trigger di funzione di Hub eventi usa l'oggetto JSON seguente nella matrice `bindings` di function.json:</span><span class="sxs-lookup"><span data-stu-id="d08ea-111">The Event Hubs function trigger uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHubTrigger",
    "name": "<Name of trigger parameter in function signature>",
    "direction": "in",
    "path": "<Name of the event hub>",
    "consumerGroup": "Consumer group to use - see below",
    "connection": "<Name of app setting with connection string - see below>"
}
```

<span data-ttu-id="d08ea-112">`consumerGroup`: proprietà facoltativa usata per impostare il [gruppo di consumer](../event-hubs/event-hubs-features.md#event-consumers) usato per effettuare la sottoscrizione agli eventi nell'hub.</span><span class="sxs-lookup"><span data-stu-id="d08ea-112">`consumerGroup` is an optional property used to set the [consumer group](../event-hubs/event-hubs-features.md#event-consumers) used to subscribe to events in the hub.</span></span> <span data-ttu-id="d08ea-113">Se omessa, al suo posto viene usato il gruppo di consumer `$Default`.</span><span class="sxs-lookup"><span data-stu-id="d08ea-113">If omitted, the `$Default` consumer group is used.</span></span>  
<span data-ttu-id="d08ea-114">`connection` deve essere il nome di un'impostazione dell'app che contiene la stringa di connessione per lo spazio dei nomi di Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="d08ea-114">`connection` must be the name of an app setting that contains the connection string to the event hub's namespace.</span></span>
<span data-ttu-id="d08ea-115">Copiare questa stringa di connessione facendo clic sul pulsante **Informazioni di connessione** per lo *spazio dei nomi*, non per lo stesso Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="d08ea-115">Copy this connection string by clicking the **Connection Information** button for the *namespace*, not the event hub itself.</span></span> <span data-ttu-id="d08ea-116">Per attivare il trigger, questa stringa di connessione deve disporre almeno delle autorizzazioni Read.</span><span class="sxs-lookup"><span data-stu-id="d08ea-116">This connection string must have at least read permissions to activate the trigger.</span></span>

<span data-ttu-id="d08ea-117">È possibile specificare [Impostazioni aggiuntive](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) in un file host.json per ottimizzare i trigger di Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="d08ea-117">[Additional settings](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) can be provided in a host.json file to further fine tune Event Hubs triggers.</span></span>  

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="d08ea-118">Utilizzo dei trigger</span><span class="sxs-lookup"><span data-stu-id="d08ea-118">Trigger usage</span></span>
<span data-ttu-id="d08ea-119">Quando viene attivata una funzione trigger di Hub eventi, il messaggio che la attiva viene passato alla funzione sotto forma di stringa.</span><span class="sxs-lookup"><span data-stu-id="d08ea-119">When an Event Hubs trigger function is triggered, the message that triggers it is passed into the function as a string.</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="d08ea-120">Esempio di trigger</span><span class="sxs-lookup"><span data-stu-id="d08ea-120">Trigger sample</span></span>
<span data-ttu-id="d08ea-121">Si supponga che il trigger di Hub eventi seguente sia presente nella matrice `bindings` di function.json:</span><span class="sxs-lookup"><span data-stu-id="d08ea-121">Suppose you have the following Event Hubs trigger in the `bindings` array of function.json:</span></span>

```json
{
  "type": "eventHubTrigger",
  "name": "myEventHubMessage",
  "direction": "in",
  "path": "MyEventHub",
  "connection": "myEventHubReadConnectionString"
}
```

<span data-ttu-id="d08ea-122">Vedere l'esempio specifico del linguaggio che registra il corpo del messaggio del trigger di Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="d08ea-122">See the language-specific sample that logs the message body of the event hub trigger.</span></span>

* [<span data-ttu-id="d08ea-123">C#</span><span class="sxs-lookup"><span data-stu-id="d08ea-123">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="d08ea-124">F#</span><span class="sxs-lookup"><span data-stu-id="d08ea-124">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="d08ea-125">Node.JS</span><span class="sxs-lookup"><span data-stu-id="d08ea-125">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="d08ea-126">Esempio di trigger in C#</span><span class="sxs-lookup"><span data-stu-id="d08ea-126">Trigger sample in C#</span></span> #

```cs
using System;

public static void Run(string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

<span data-ttu-id="d08ea-127">È anche possibile ricevere l'evento come un oggetto [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata), che consente di accedere ai metadati dell'evento.</span><span class="sxs-lookup"><span data-stu-id="d08ea-127">You can also receive the event as an [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) object, which gives you access to the event metadata.</span></span>

```cs
#r "Microsoft.ServiceBus"
using System.Text;
using Microsoft.ServiceBus.Messaging;

public static void Run(EventData myEventHubMessage, TraceWriter log)
{
    log.Info($"{Encoding.UTF8.GetString(myEventHubMessage.GetBytes())}");
}
```

<span data-ttu-id="d08ea-128">Per ricevere gli eventi in un batch, impostare la firma del metodo su `string[]` o `EventData[]`.</span><span class="sxs-lookup"><span data-stu-id="d08ea-128">To receive events in a batch, change the method signature to `string[]` or `EventData[]`.</span></span>

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

### <a name="trigger-sample-in-f"></a><span data-ttu-id="d08ea-129">Esempio di trigger in F#</span><span class="sxs-lookup"><span data-stu-id="d08ea-129">Trigger sample in F#</span></span> #

```fsharp
let Run(myEventHubMessage: string, log: TraceWriter) =
    log.Info(sprintf "F# eventhub trigger function processed work item: %s" myEventHubMessage)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="d08ea-130">Esempio di trigger in Node.js</span><span class="sxs-lookup"><span data-stu-id="d08ea-130">Trigger sample in Node.js</span></span>

```javascript
module.exports = function (context, myEventHubMessage) {
    context.log('Node.js eventhub trigger function processed work item', myEventHubMessage);    
    context.done();
};
```

<a name="output"></a>

## <a name="event-hubs-output-binding"></a><span data-ttu-id="d08ea-131">Associazione di output di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="d08ea-131">Event Hubs output binding</span></span>
<span data-ttu-id="d08ea-132">È possibile usare l'associazione di output di Hub eventi per scrivere eventi in un flusso di eventi di Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="d08ea-132">Use the Event Hubs output binding to write events to an event hub event stream.</span></span> <span data-ttu-id="d08ea-133">Per scrivervi eventi, è necessario disporre dell'autorizzazione Send verso un Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="d08ea-133">You must have send permission to an event hub to write events to it.</span></span>

<span data-ttu-id="d08ea-134">L'associazione di output usa l'oggetto JSON seguente nella matrice `bindings` di function.json:</span><span class="sxs-lookup"><span data-stu-id="d08ea-134">The output binding uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHub",
    "name": "<Name of output parameter in function signature>",
    "path": "<Name of event hub>",
    "connection": "<Name of app setting with connection string - see below>"
    "direction": "out"
}
```

<span data-ttu-id="d08ea-135">`connection` deve essere il nome di un'impostazione dell'app che contiene la stringa di connessione per lo spazio dei nomi di Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="d08ea-135">`connection` must be the name of an app setting that contains the connection string to the event hub's namespace.</span></span>
<span data-ttu-id="d08ea-136">Copiare questa stringa di connessione facendo clic sul pulsante **Informazioni di connessione** per lo *spazio dei nomi*, non per lo stesso Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="d08ea-136">Copy this connection string by clicking the **Connection Information** button for the *namespace*, not the event hub itself.</span></span> <span data-ttu-id="d08ea-137">Per inviare il messaggio al flusso di eventi, questa stringa di connessione deve disporre di autorizzazioni Send.</span><span class="sxs-lookup"><span data-stu-id="d08ea-137">This connection string must have send permissions to send the message to the event stream.</span></span>

## <a name="output-usage"></a><span data-ttu-id="d08ea-138">Uso dell'output</span><span class="sxs-lookup"><span data-stu-id="d08ea-138">Output usage</span></span>
<span data-ttu-id="d08ea-139">Questa sezione illustra come usare l'associazione di output di Hub eventi nel codice della funzione.</span><span class="sxs-lookup"><span data-stu-id="d08ea-139">This section shows you how to use your Event Hubs output binding in your function code.</span></span>

<span data-ttu-id="d08ea-140">È possibile inviare i messaggi all'hub eventi configurato con i tipi di parametro seguenti:</span><span class="sxs-lookup"><span data-stu-id="d08ea-140">You can output messages to the configured event hub with the following parameter types:</span></span>

* `out string`
* <span data-ttu-id="d08ea-141">`ICollector<string>` (per restituire più messaggi)</span><span class="sxs-lookup"><span data-stu-id="d08ea-141">`ICollector<string>` (to output multiple messages)</span></span>
* <span data-ttu-id="d08ea-142">`IAsyncCollector<string>` (versione asincrona di `ICollector<T>`)</span><span class="sxs-lookup"><span data-stu-id="d08ea-142">`IAsyncCollector<string>` (async version of `ICollector<T>`)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="d08ea-143">Esempio di output</span><span class="sxs-lookup"><span data-stu-id="d08ea-143">Output sample</span></span>
<span data-ttu-id="d08ea-144">Si supponga che l'associazione di output di Hub eventi seguente sia presente nella matrice `bindings` di function.json:</span><span class="sxs-lookup"><span data-stu-id="d08ea-144">Suppose you have the following Event Hubs output binding in the `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHub",
    "name": "outputEventHubMessage",
    "path": "myeventhub",
    "connection": "MyEventHubSend",
    "direction": "out"
}
```

<span data-ttu-id="d08ea-145">Vedere l'esempio specifico del linguaggio che scrive un evento nel flusso di eventi.</span><span class="sxs-lookup"><span data-stu-id="d08ea-145">See the language-specific sample that writes an event to the even stream.</span></span>

* [<span data-ttu-id="d08ea-146">C#</span><span class="sxs-lookup"><span data-stu-id="d08ea-146">C#</span></span>](#outcsharp)
* [<span data-ttu-id="d08ea-147">F#</span><span class="sxs-lookup"><span data-stu-id="d08ea-147">F#</span></span>](#outfsharp)
* [<span data-ttu-id="d08ea-148">Node.JS</span><span class="sxs-lookup"><span data-stu-id="d08ea-148">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="d08ea-149">Esempio di output in C#</span><span class="sxs-lookup"><span data-stu-id="d08ea-149">Output sample in C#</span></span> #

```cs
using System;

public static void Run(TimerInfo myTimer, out string outputEventHubMessage, TraceWriter log)
{
    String msg = $"TimerTriggerCSharp1 executed at: {DateTime.Now}";
    log.Verbose(msg);   
    outputEventHubMessage = msg;
}
```

<span data-ttu-id="d08ea-150">Oppure per creare più messaggi:</span><span class="sxs-lookup"><span data-stu-id="d08ea-150">Or, to create multiple messages:</span></span>

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

### <a name="output-sample-in-f"></a><span data-ttu-id="d08ea-151">Esempio di output in F#</span><span class="sxs-lookup"><span data-stu-id="d08ea-151">Output sample in F#</span></span> #

```fsharp
let Run(myTimer: TimerInfo, outputEventHubMessage: byref<string>, log: TraceWriter) =
    let msg = sprintf "TimerTriggerFSharp1 executed at: %s" DateTime.Now.ToString()
    log.Verbose(msg);
    outputEventHubMessage <- msg;
```

<a name="outnodejs"></a>

### <a name="output-sample-for-nodejs"></a><span data-ttu-id="d08ea-152">Esempio di output in Node.js</span><span class="sxs-lookup"><span data-stu-id="d08ea-152">Output sample for Node.js</span></span>

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();
    context.log('Event Hub message created at: ', timeStamp);   
    context.bindings.outputEventHubMessage = "Event Hub message created at: " + timeStamp;
    context.done();
};
```

<span data-ttu-id="d08ea-153">Oppure, per inviare più messaggi,</span><span class="sxs-lookup"><span data-stu-id="d08ea-153">Or, to send multiple messages,</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="d08ea-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d08ea-154">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
