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
# <a name="azure-functions-event-hubs-bindings"></a>Associazioni di Hub eventi in Funzioni di Azure
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Questo articolo viene illustrato come tooconfigure e utilizzare [hub eventi di Azure](../event-hubs/event-hubs-what-is-event-hubs.md) associazioni per le funzioni di Azure.
Funzioni di Azure supporta il trigger e le associazioni di output per Hub eventi.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

Nel caso di nuovo hub di eventi tooAzure, vedere hello [Panoramica di hub eventi](../event-hubs/event-hubs-what-is-event-hubs.md).

<a name="trigger"></a>

## <a name="event-hub-trigger"></a>Trigger di Hub eventi
Utilizzare gli hub di eventi hello attivare toorespond tooan evento flusso di eventi di hub eventi tooan inviato. È necessario disporre dell'accesso in lettura toohello evento hub tooset dei trigger hello.

trigger di funzione Hello hub eventi Usa hello seguente oggetto JSON nella hello `bindings` matrice function.json:

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

`consumerGroup`è un hello tooset proprietà facoltativa utilizzata [gruppo di consumer](../event-hubs/event-hubs-features.md#event-consumers) utilizzato toosubscribe tooevents nell'hub hello. Se omesso, hello `$Default` viene utilizzato il gruppo di consumer.  
`connection`deve essere hello nome di un'impostazione di app che contiene lo spazio dei nomi hello connessione stringa toohello dell'hub eventi.
Copiare la stringa di connessione, fare clic su hello **informazioni di connessione** pulsante per hello *dello spazio dei nomi*, non hello hub di eventi stesso. La stringa di connessione deve disporre almeno di lettura trigger hello tooactivate di autorizzazioni.

[Impostazioni aggiuntive](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) può essere fornito in un host.json toofurther file fine ottimizzare gli hub di eventi trigger.  

<a name="triggerusage"></a>

## <a name="trigger-usage"></a>Uso dei trigger
Quando una funzione di hub di eventi trigger viene attivata, il messaggio hello che lo attiva viene passato alla funzione hello sotto forma di stringa.

<a name="triggersample"></a>

## <a name="trigger-sample"></a>Esempio di trigger
Si supponga di avere hello seguenti hub di eventi trigger hello `bindings` matrice function.json:

```json
{
  "type": "eventHubTrigger",
  "name": "myEventHubMessage",
  "direction": "in",
  "path": "MyEventHub",
  "connection": "myEventHubReadConnectionString"
}
```

Vedere l'esempio specifico del linguaggio hello che registra corpo del messaggio hello del trigger di hub eventi hello.

* [C#](#triggercsharp)
* [F#](#triggerfsharp)
* [Node.JS](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>Esempio di trigger in C# #

```cs
using System;

public static void Run(string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

È inoltre possibile ricevere eventi hello come un [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) oggetto, che consente di accedere ai metadati di evento toohello.

```cs
#r "Microsoft.ServiceBus"
using System.Text;
using Microsoft.ServiceBus.Messaging;

public static void Run(EventData myEventHubMessage, TraceWriter log)
{
    log.Info($"{Encoding.UTF8.GetString(myEventHubMessage.GetBytes())}");
}
```

tooreceive eventi in un batch, modificare la firma del metodo hello troppo`string[]` o `EventData[]`.

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

### <a name="trigger-sample-in-f"></a>Esempio di trigger in F# #

```fsharp
let Run(myEventHubMessage: string, log: TraceWriter) =
    log.Info(sprintf "F# eventhub trigger function processed work item: %s" myEventHubMessage)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a>Esempio di trigger in Node.js

```javascript
module.exports = function (context, myEventHubMessage) {
    context.log('Node.js eventhub trigger function processed work item', myEventHubMessage);    
    context.done();
};
```

<a name="output"></a>

## <a name="event-hubs-output-binding"></a>Associazione di output di Hub eventi
Associazione toowrite eventi tooan evento hub eventi flusso di output di hello utilizzare gli hub di eventi. È necessario disporre di trasmissione autorizzazione tooan evento hub toowrite eventi tooit.

associazione di output Hello utilizza hello seguente oggetto JSON nella hello `bindings` matrice function.json:

```json
{
    "type": "eventHub",
    "name": "<Name of output parameter in function signature>",
    "path": "<Name of event hub>",
    "connection": "<Name of app setting with connection string - see below>"
    "direction": "out"
}
```

`connection`deve essere hello nome di un'impostazione di app che contiene lo spazio dei nomi hello connessione stringa toohello dell'hub eventi.
Copiare la stringa di connessione, fare clic su hello **informazioni di connessione** pulsante per hello *dello spazio dei nomi*, non hello hub di eventi stesso. Questa stringa di connessione deve avere flusso di eventi di trasmissione autorizzazioni toosend hello messaggio toohello.

## <a name="output-usage"></a>Uso dell'output
In questa sezione viene illustrato come toouse gli hub di eventi di output di associazione nel codice di funzione.

È possibile creare hub di eventi di messaggi toohello configurato con i seguenti tipi di parametro hello:

* `out string`
* `ICollector<string>`(toooutput più messaggi)
* `IAsyncCollector<string>` (versione asincrona di `ICollector<T>`)

<a name="outputsample"></a>

## <a name="output-sample"></a>Esempio di output
Si supponga di avere seguito hello hub eventi di output dell'associazione in hello `bindings` matrice function.json:

```json
{
    "type": "eventHub",
    "name": "outputEventHubMessage",
    "path": "myeventhub",
    "connection": "MyEventHubSend",
    "direction": "out"
}
```

Vedere l'esempio specifico del linguaggio hello che scrive un flusso di eventi toohello anche.

* [C#](#outcsharp)
* [F#](#outfsharp)
* [Node.JS](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>Esempio di output in C# #

```cs
using System;

public static void Run(TimerInfo myTimer, out string outputEventHubMessage, TraceWriter log)
{
    String msg = $"TimerTriggerCSharp1 executed at: {DateTime.Now}";
    log.Verbose(msg);   
    outputEventHubMessage = msg;
}
```

In alternativa, toocreate più messaggi:

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

### <a name="output-sample-in-f"></a>Esempio di output in F# #

```fsharp
let Run(myTimer: TimerInfo, outputEventHubMessage: byref<string>, log: TraceWriter) =
    let msg = sprintf "TimerTriggerFSharp1 executed at: %s" DateTime.Now.ToString()
    log.Verbose(msg);
    outputEventHubMessage <- msg;
```

<a name="outnodejs"></a>

### <a name="output-sample-for-nodejs"></a>Esempio di output in Node.js

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();
    context.log('Event Hub message created at: ', timeStamp);   
    context.bindings.outputEventHubMessage = "Event Hub message created at: " + timeStamp;
    context.done();
};
```

In alternativa, toosend più messaggi,

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

## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
