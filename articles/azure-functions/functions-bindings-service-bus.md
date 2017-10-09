---
title: Funzioni di Service Bus aaaAzure trigger e le associazioni | Documenti Microsoft
description: Comprendere come toouse Service Bus di Azure attiva e le associazioni in funzioni di Azure.
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: Funzioni di Azure, Funzioni, elaborazione eventi, calcolo dinamico, architettura senza server
ms.assetid: daedacf0-6546-4355-a65c-50873e74f66b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/01/2017
ms.author: glenga
ms.openlocfilehash: dff9e89bd3840b8c11f91cae41e13502afc7aa60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-service-bus-bindings"></a>Associazioni del bus di servizio di Funzioni di Azure
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Questo articolo viene illustrato come tooconfigure e di lavoro con le associazioni di Azure Service Bus in funzioni di Azure. 

Funzioni di Azure supporta il trigger e le associazioni di output per le code e gli argomenti del bus di servizio.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="service-bus-trigger"></a>Trigger di bus di servizio
Utilizzare hello Bus di servizio trigger toorespond toomessages da una coda del Bus di servizio o un argomento. 

Hello Bus di servizio della coda e argomento sono definiti trigger da hello seguendo gli oggetti JSON in hello `bindings` matrice function.json:

* trigger della *coda*:

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "queueName" : "<Name of hello queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

* trigger dell'*argomento*:

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "topicName" : "<Name of hello topic>",
        "subscriptionName" : "<Name of hello subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

Si noti hello segue:

* Per `connection`, [creare un'impostazione dell'app nell'app funzione](functions-how-to-use-azure-function-app-settings.md) che include spazio dei nomi Service Bus tooyour hello connessione stringa, quindi specificare il nome di hello di impostazione dell'app hello in hello `connection` proprietà del trigger. Stringa di connessione hello è ottenere seguendo i passaggi di hello mostrati al [ottenere le credenziali di gestione di hello](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).
  stringa di connessione Hello deve essere per lo spazio dei nomi Service Bus, coda specifica tooa non limitato o argomento.
  Se si lascia `connection` vuoto, il trigger hello presuppone che una stringa di connessione del Bus di servizio predefinito è specificata in un'app impostazione denominata `AzureWebJobsServiceBus`.
* Per `accessRights`, i valori disponibili sono `manage` e `listen`. valore predefinito di Hello è `manage`, che indica che hello `connection` è hello **Gestisci** autorizzazione. Se si usa una stringa di connessione che non dispone di hello **Gestisci** set di autorizzazioni, `accessRights` troppo`listen`. In caso contrario, le funzioni hello runtime potrebbe non riuscire durante le operazioni di toodo che richiedono i diritti di gestione.

## <a name="trigger-behavior"></a>Comportamento di trigger
* **Il threading singolo** : per impostazione predefinita, i processi del runtime di funzioni hello più messaggi contemporaneamente. toodirect hello runtime tooprocess un solo argomento o coda messaggio alla volta, impostare `serviceBus.maxConcurrentCalls` too1 in *host.json*. 
  Per informazioni su *host.json*, vedere la [Struttura di cartelle](functions-reference.md#folder-structure) e [host.json](https://github .com/Azure/azure-webjobs-sdk-script/wiki/host.json).
* **Gestione dei messaggi non elaborabili**: il bus di servizio esegue la gestione dei messaggi non elaborabili in modo autonomo, non controllabile o modificabile nella configurazione o nel codice di Funzioni di Azure. 
* **Comportamento di PeekLock** -hello funzioni runtime riceve un messaggio in [ `PeekLock` modalità](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) e chiama `Complete` messaggio hello se la funzione hello viene completata correttamente o chiamate `Abandon` se hello funzione ha esito negativo. 
  Se la funzione hello viene eseguito più di hello `PeekLock` timeout blocco hello viene rinnovato automaticamente.

<a name="triggerusage"></a>

## <a name="trigger-usage"></a>Uso dei trigger
In questa sezione viene illustrato come toouse attivare il Bus di servizio nel codice di funzione. 

In c# e F #, hello Bus di servizio trigger può essere deserializzato tooany di hello seguenti tipi di input:

* `string`: utile per i messaggi di stringa
* `byte[]`: utile per i dati binari
* Qualsiasi [oggetto](https://msdn.microsoft.com/library/system.object.aspx): utile per i dati serializzati con JSON.
  Se si dichiara un tipo di input personalizzato, ad esempio `CustomType`, le funzioni di Azure tenta i dati JSON hello toodeserialize nel tipo specificato.
* `BrokeredMessage`-consente hello deserializzato messaggio hello [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) metodo.

In Node.js, messaggio di attivazione di Service Bus hello viene passato nella funzione hello sotto forma di stringa o oggetto JSON.

<a name="triggersample"></a>

## <a name="trigger-sample"></a>Esempio di trigger
Si supponga di avere hello function.json seguenti:

```json
{
"bindings": [
    {
    "queueName": "testqueue",
    "connection": "MyServiceBusConnection",
    "name": "myQueueItem",
    "type": "serviceBusTrigger",
    "direction": "in"
    }
],
"disabled": false
}
```

Vedere l'esempio specifico del linguaggio hello che elabora un messaggio nella coda Service Bus.

* [C#](#triggercsharp)
* [F#](#triggerfsharp)
* [Node.JS](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>Esempio di trigger in C# #

```cs
public static void Run(string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a>Esempio di trigger in F# #

```fsharp
let Run(myQueueItem: string, log: TraceWriter) =
    log.Info(sprintf "F# ServiceBus queue trigger function processed message: %s" myQueueItem)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a>Esempio di trigger in Node.js

```javascript
module.exports = function(context, myQueueItem) {
    context.log('Node.js ServiceBus queue trigger function processed message', myQueueItem);
    context.done();
};
```

<a name="output"></a>

## <a name="service-bus-output-binding"></a>Associazione di output di bus di servizio
output di coda e argomento Bus di servizio per una funzione Hello utilizzare hello seguendo gli oggetti JSON in hello `bindings` matrice function.json:

* output di *coda*:

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "queueName" : "<Name of hello queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```
* output di *argomento*:

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "topicName" : "<Name of hello topic>",
        "subscriptionName" : "<Name of hello subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```

Si noti hello segue:

* Per `connection`, [creare un'impostazione dell'app nell'app funzione](functions-how-to-use-azure-function-app-settings.md) che include spazio dei nomi Service Bus tooyour hello connessione stringa, quindi specificare il nome di hello di impostazione dell'app hello in hello `connection` proprietà nell'output associazione. Stringa di connessione hello è ottenere seguendo i passaggi di hello mostrati al [ottenere le credenziali di gestione di hello](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).
  stringa di connessione Hello deve essere per lo spazio dei nomi Service Bus, coda specifica tooa non limitato o argomento.
  Se si lascia `connection` vuoto, hello associazione di output si presuppone che una stringa di connessione del Bus di servizio predefinito è specificata in un'app impostazione denominata `AzureWebJobsServiceBus`.
* Per `accessRights`, i valori disponibili sono `manage` e `listen`. valore predefinito di Hello è `manage`, che indica che hello `connection` è hello **Gestisci** autorizzazione. Se si usa una stringa di connessione che non dispone di hello **Gestisci** set di autorizzazioni, `accessRights` troppo`listen`. In caso contrario, le funzioni hello runtime potrebbe non riuscire durante le operazioni di toodo che richiedono i diritti di gestione.

<a name="outputusage"></a>

## <a name="output-usage"></a>Uso dell'output
In c# e F #, le funzioni di Azure è possibile creare un messaggio nella coda Service Bus da uno qualsiasi dei seguenti tipi di hello:

* Qualsiasi [oggetto](https://msdn.microsoft.com/library/system.object.aspx): la definizione dei parametri è simile a `out T paramName` (C#).
  Funzioni deserializza l'oggetto hello in un messaggio JSON. Se il valore di output di hello è null quando si esce dalla funzione hello, funzioni Crea messaggio hello con un oggetto null.
* `string`: la definizione dei parametri è simile a `out string paraName` (C#). Se il valore di parametro hello è non null quando si esce dalla funzione hello, funzioni di crea un messaggio.
* `byte[]`: la definizione dei parametri è simile a `out byte[] paraName` (C#). Se il valore di parametro hello è non null quando si esce dalla funzione hello, funzioni di crea un messaggio.
* `BrokeredMessage`: la definizione dei parametri è simile a `out BrokeredMessage paraName` (C#). Se il valore di parametro hello è non null quando si esce dalla funzione hello, funzioni di crea un messaggio.

Per la creazione di più messaggi in una funzione C# è possibile usare `ICollector<T>` o `IAsyncCollector<T>`. Viene creato un messaggio quando si chiama hello `Add` metodo.

In Node.js, è possibile assegnare una stringa, una matrice di byte o un oggetto Javascript (deserializzato in JSON) troppo`context.binding.<paramName>`.

<a name="outputsample"></a>

## <a name="output-sample"></a>Esempio di output
Si supponga di avere seguito function.json hello, che definisce un output di coda del Bus di servizio:

```json
{
    "bindings": [
        {
            "schedule": "0/15 * * * * *",
            "name": "myTimer",
            "runsOnStartup": true,
            "type": "timerTrigger",
            "direction": "in"
        },
        {
            "name": "outputSbQueue",
            "type": "serviceBus",
            "queueName": "testqueue",
            "connection": "MyServiceBusConnection",
            "direction": "out"
        }
    ],
    "disabled": false
}
```

Vedere l'esempio specifico del linguaggio hello che invia la coda di messaggi toohello service bus.

* [C#](#outcsharp)
* [F#](#outfsharp)
* [Node.JS](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>Esempio di output in C# #

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, out string outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue = message;
}
```

In alternativa, toocreate più messaggi:

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, ICollector<string> outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue.Add("1 " + message);
    outputSbQueue.Add("2 " + message);
}
```

<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a>Esempio di output in F# #

```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter, outputSbQueue: byref<string>) =
    let message = sprintf "Service Bus queue message created at: %s" (DateTime.Now.ToString())
    log.Info(message)
    outputSbQueue = message
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a>Esempio di output in Node.js

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = message;
    context.done();
};
```

In alternativa, toocreate più messaggi:

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = [];
    context.bindings.outputSbQueueMsg.push("1 " + message);
    context.bindings.outputSbQueueMsg.push("2 " + message);
    context.done();
};
```

## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

