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
# <a name="azure-functions-service-bus-bindings"></a><span data-ttu-id="93582-104">Associazioni del bus di servizio di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="93582-104">Azure Functions Service Bus bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="93582-105">Questo articolo viene illustrato come tooconfigure e di lavoro con le associazioni di Azure Service Bus in funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="93582-105">This article explains how tooconfigure and work with Azure Service Bus bindings in Azure Functions.</span></span> 

<span data-ttu-id="93582-106">Funzioni di Azure supporta il trigger e le associazioni di output per le code e gli argomenti del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="93582-106">Azure Functions supports trigger and output bindings for Service Bus queues and topics.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="service-bus-trigger"></a><span data-ttu-id="93582-107">Trigger di bus di servizio</span><span class="sxs-lookup"><span data-stu-id="93582-107">Service Bus trigger</span></span>
<span data-ttu-id="93582-108">Utilizzare hello Bus di servizio trigger toorespond toomessages da una coda del Bus di servizio o un argomento.</span><span class="sxs-lookup"><span data-stu-id="93582-108">Use hello Service Bus trigger toorespond toomessages from a Service Bus queue or topic.</span></span> 

<span data-ttu-id="93582-109">Hello Bus di servizio della coda e argomento sono definiti trigger da hello seguendo gli oggetti JSON in hello `bindings` matrice function.json:</span><span class="sxs-lookup"><span data-stu-id="93582-109">hello Service Bus queue and topic triggers are defined by hello following JSON objects in hello `bindings` array of function.json:</span></span>

* <span data-ttu-id="93582-110">trigger della *coda*:</span><span class="sxs-lookup"><span data-stu-id="93582-110">*queue* trigger:</span></span>

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

* <span data-ttu-id="93582-111">trigger dell'*argomento*:</span><span class="sxs-lookup"><span data-stu-id="93582-111">*topic* trigger:</span></span>

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

<span data-ttu-id="93582-112">Si noti hello segue:</span><span class="sxs-lookup"><span data-stu-id="93582-112">Note hello following:</span></span>

* <span data-ttu-id="93582-113">Per `connection`, [creare un'impostazione dell'app nell'app funzione](functions-how-to-use-azure-function-app-settings.md) che include spazio dei nomi Service Bus tooyour hello connessione stringa, quindi specificare il nome di hello di impostazione dell'app hello in hello `connection` proprietà del trigger.</span><span class="sxs-lookup"><span data-stu-id="93582-113">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains hello connection string tooyour Service Bus namespace, then specify hello name of hello app setting in hello `connection` property in your trigger.</span></span> <span data-ttu-id="93582-114">Stringa di connessione hello è ottenere seguendo i passaggi di hello mostrati al [ottenere le credenziali di gestione di hello](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span><span class="sxs-lookup"><span data-stu-id="93582-114">You obtain hello connection string by following hello steps shown at [Obtain hello management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="93582-115">stringa di connessione Hello deve essere per lo spazio dei nomi Service Bus, coda specifica tooa non limitato o argomento.</span><span class="sxs-lookup"><span data-stu-id="93582-115">hello connection string must be for a Service Bus namespace, not limited tooa specific queue or topic.</span></span>
  <span data-ttu-id="93582-116">Se si lascia `connection` vuoto, il trigger hello presuppone che una stringa di connessione del Bus di servizio predefinito è specificata in un'app impostazione denominata `AzureWebJobsServiceBus`.</span><span class="sxs-lookup"><span data-stu-id="93582-116">If you leave `connection` empty, hello trigger assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="93582-117">Per `accessRights`, i valori disponibili sono `manage` e `listen`.</span><span class="sxs-lookup"><span data-stu-id="93582-117">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="93582-118">valore predefinito di Hello è `manage`, che indica che hello `connection` è hello **Gestisci** autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="93582-118">hello default is `manage`, which indicates that hello `connection` has hello **Manage** permission.</span></span> <span data-ttu-id="93582-119">Se si usa una stringa di connessione che non dispone di hello **Gestisci** set di autorizzazioni, `accessRights` troppo`listen`.</span><span class="sxs-lookup"><span data-stu-id="93582-119">If you use a connection string that does not have hello **Manage** permission, set `accessRights` too`listen`.</span></span> <span data-ttu-id="93582-120">In caso contrario, le funzioni hello runtime potrebbe non riuscire durante le operazioni di toodo che richiedono i diritti di gestione.</span><span class="sxs-lookup"><span data-stu-id="93582-120">Otherwise, hello Functions runtime might fail trying toodo operations that require manage rights.</span></span>

## <a name="trigger-behavior"></a><span data-ttu-id="93582-121">Comportamento di trigger</span><span class="sxs-lookup"><span data-stu-id="93582-121">Trigger behavior</span></span>
* <span data-ttu-id="93582-122">**Il threading singolo** : per impostazione predefinita, i processi del runtime di funzioni hello più messaggi contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="93582-122">**Single-threading** - By default, hello Functions runtime processes multiple messages concurrently.</span></span> <span data-ttu-id="93582-123">toodirect hello runtime tooprocess un solo argomento o coda messaggio alla volta, impostare `serviceBus.maxConcurrentCalls` too1 in *host.json*.</span><span class="sxs-lookup"><span data-stu-id="93582-123">toodirect hello runtime tooprocess only a single queue or topic message at a time, set `serviceBus.maxConcurrentCalls` too1 in *host.json*.</span></span> 
  <span data-ttu-id="93582-124">Per informazioni su *host.json*, vedere la [Struttura di cartelle](functions-reference.md#folder-structure) e [host.json](https://github .com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="93582-124">For information about *host.json*, see [Folder Structure](functions-reference.md#folder-structure) and [host.json](https://github .com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>
* <span data-ttu-id="93582-125">**Gestione dei messaggi non elaborabili**: il bus di servizio esegue la gestione dei messaggi non elaborabili in modo autonomo, non controllabile o modificabile nella configurazione o nel codice di Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="93582-125">**Poison message handling** - Service Bus does its own poison message handling, which can't be controlled or configured in Azure Functions configuration or code.</span></span> 
* <span data-ttu-id="93582-126">**Comportamento di PeekLock** -hello funzioni runtime riceve un messaggio in [ `PeekLock` modalità](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) e chiama `Complete` messaggio hello se la funzione hello viene completata correttamente o chiamate `Abandon` se hello funzione ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="93582-126">**PeekLock behavior** - hello Functions runtime receives a message in [`PeekLock` mode](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) and calls `Complete` on hello message if hello function finishes successfully, or calls `Abandon` if hello function fails.</span></span> 
  <span data-ttu-id="93582-127">Se la funzione hello viene eseguito più di hello `PeekLock` timeout blocco hello viene rinnovato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="93582-127">If hello function runs longer than hello `PeekLock` timeout, hello lock is automatically renewed.</span></span>

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="93582-128">Uso dei trigger</span><span class="sxs-lookup"><span data-stu-id="93582-128">Trigger usage</span></span>
<span data-ttu-id="93582-129">In questa sezione viene illustrato come toouse attivare il Bus di servizio nel codice di funzione.</span><span class="sxs-lookup"><span data-stu-id="93582-129">This section shows you how toouse your Service Bus trigger in your function code.</span></span> 

<span data-ttu-id="93582-130">In c# e F #, hello Bus di servizio trigger può essere deserializzato tooany di hello seguenti tipi di input:</span><span class="sxs-lookup"><span data-stu-id="93582-130">In C# and F#, hello Service Bus trigger message can be deserialized tooany of hello following input types:</span></span>

* <span data-ttu-id="93582-131">`string`: utile per i messaggi di stringa</span><span class="sxs-lookup"><span data-stu-id="93582-131">`string` - useful for string messages</span></span>
* <span data-ttu-id="93582-132">`byte[]`: utile per i dati binari</span><span class="sxs-lookup"><span data-stu-id="93582-132">`byte[]` - useful for binary data</span></span>
* <span data-ttu-id="93582-133">Qualsiasi [oggetto](https://msdn.microsoft.com/library/system.object.aspx): utile per i dati serializzati con JSON.</span><span class="sxs-lookup"><span data-stu-id="93582-133">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized data.</span></span>
  <span data-ttu-id="93582-134">Se si dichiara un tipo di input personalizzato, ad esempio `CustomType`, le funzioni di Azure tenta i dati JSON hello toodeserialize nel tipo specificato.</span><span class="sxs-lookup"><span data-stu-id="93582-134">If you declare a custom input type, such as `CustomType`, Azure Functions tries toodeserialize hello JSON data into your specified type.</span></span>
* <span data-ttu-id="93582-135">`BrokeredMessage`-consente hello deserializzato messaggio hello [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) metodo.</span><span class="sxs-lookup"><span data-stu-id="93582-135">`BrokeredMessage` - gives you hello deserialized message with hello [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) method.</span></span>

<span data-ttu-id="93582-136">In Node.js, messaggio di attivazione di Service Bus hello viene passato nella funzione hello sotto forma di stringa o oggetto JSON.</span><span class="sxs-lookup"><span data-stu-id="93582-136">In Node.js, hello Service Bus trigger message is passed into hello function as either a string or JSON object.</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="93582-137">Esempio di trigger</span><span class="sxs-lookup"><span data-stu-id="93582-137">Trigger sample</span></span>
<span data-ttu-id="93582-138">Si supponga di avere hello function.json seguenti:</span><span class="sxs-lookup"><span data-stu-id="93582-138">Suppose you have hello following function.json:</span></span>

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

<span data-ttu-id="93582-139">Vedere l'esempio specifico del linguaggio hello che elabora un messaggio nella coda Service Bus.</span><span class="sxs-lookup"><span data-stu-id="93582-139">See hello language-specific sample that processes a Service Bus queue message.</span></span>

* [<span data-ttu-id="93582-140">C#</span><span class="sxs-lookup"><span data-stu-id="93582-140">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="93582-141">F#</span><span class="sxs-lookup"><span data-stu-id="93582-141">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="93582-142">Node.JS</span><span class="sxs-lookup"><span data-stu-id="93582-142">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="93582-143">Esempio di trigger in C#</span><span class="sxs-lookup"><span data-stu-id="93582-143">Trigger sample in C#</span></span> #

```cs
public static void Run(string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a><span data-ttu-id="93582-144">Esempio di trigger in F#</span><span class="sxs-lookup"><span data-stu-id="93582-144">Trigger sample in F#</span></span> #

```fsharp
let Run(myQueueItem: string, log: TraceWriter) =
    log.Info(sprintf "F# ServiceBus queue trigger function processed message: %s" myQueueItem)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="93582-145">Esempio di trigger in Node.js</span><span class="sxs-lookup"><span data-stu-id="93582-145">Trigger sample in Node.js</span></span>

```javascript
module.exports = function(context, myQueueItem) {
    context.log('Node.js ServiceBus queue trigger function processed message', myQueueItem);
    context.done();
};
```

<a name="output"></a>

## <a name="service-bus-output-binding"></a><span data-ttu-id="93582-146">Associazione di output di bus di servizio</span><span class="sxs-lookup"><span data-stu-id="93582-146">Service Bus output binding</span></span>
<span data-ttu-id="93582-147">output di coda e argomento Bus di servizio per una funzione Hello utilizzare hello seguendo gli oggetti JSON in hello `bindings` matrice function.json:</span><span class="sxs-lookup"><span data-stu-id="93582-147">hello Service Bus queue and topic output for a function use hello following JSON objects in hello `bindings` array of function.json:</span></span>

* <span data-ttu-id="93582-148">output di *coda*:</span><span class="sxs-lookup"><span data-stu-id="93582-148">*queue* output:</span></span>

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
* <span data-ttu-id="93582-149">output di *argomento*:</span><span class="sxs-lookup"><span data-stu-id="93582-149">*topic* output:</span></span>

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

<span data-ttu-id="93582-150">Si noti hello segue:</span><span class="sxs-lookup"><span data-stu-id="93582-150">Note hello following:</span></span>

* <span data-ttu-id="93582-151">Per `connection`, [creare un'impostazione dell'app nell'app funzione](functions-how-to-use-azure-function-app-settings.md) che include spazio dei nomi Service Bus tooyour hello connessione stringa, quindi specificare il nome di hello di impostazione dell'app hello in hello `connection` proprietà nell'output associazione.</span><span class="sxs-lookup"><span data-stu-id="93582-151">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains hello connection string tooyour Service Bus namespace, then specify hello name of hello app setting in hello `connection` property in your output binding.</span></span> <span data-ttu-id="93582-152">Stringa di connessione hello è ottenere seguendo i passaggi di hello mostrati al [ottenere le credenziali di gestione di hello](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span><span class="sxs-lookup"><span data-stu-id="93582-152">You obtain hello connection string by following hello steps shown at [Obtain hello management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="93582-153">stringa di connessione Hello deve essere per lo spazio dei nomi Service Bus, coda specifica tooa non limitato o argomento.</span><span class="sxs-lookup"><span data-stu-id="93582-153">hello connection string must be for a Service Bus namespace, not limited tooa specific queue or topic.</span></span>
  <span data-ttu-id="93582-154">Se si lascia `connection` vuoto, hello associazione di output si presuppone che una stringa di connessione del Bus di servizio predefinito è specificata in un'app impostazione denominata `AzureWebJobsServiceBus`.</span><span class="sxs-lookup"><span data-stu-id="93582-154">If you leave `connection` empty, hello output binding assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="93582-155">Per `accessRights`, i valori disponibili sono `manage` e `listen`.</span><span class="sxs-lookup"><span data-stu-id="93582-155">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="93582-156">valore predefinito di Hello è `manage`, che indica che hello `connection` è hello **Gestisci** autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="93582-156">hello default is `manage`, which indicates that hello `connection` has hello **Manage** permission.</span></span> <span data-ttu-id="93582-157">Se si usa una stringa di connessione che non dispone di hello **Gestisci** set di autorizzazioni, `accessRights` troppo`listen`.</span><span class="sxs-lookup"><span data-stu-id="93582-157">If you use a connection string that does not have hello **Manage** permission, set `accessRights` too`listen`.</span></span> <span data-ttu-id="93582-158">In caso contrario, le funzioni hello runtime potrebbe non riuscire durante le operazioni di toodo che richiedono i diritti di gestione.</span><span class="sxs-lookup"><span data-stu-id="93582-158">Otherwise, hello Functions runtime might fail trying toodo operations that require manage rights.</span></span>

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="93582-159">Uso dell'output</span><span class="sxs-lookup"><span data-stu-id="93582-159">Output usage</span></span>
<span data-ttu-id="93582-160">In c# e F #, le funzioni di Azure è possibile creare un messaggio nella coda Service Bus da uno qualsiasi dei seguenti tipi di hello:</span><span class="sxs-lookup"><span data-stu-id="93582-160">In C# and F#, Azure Functions can create a Service Bus queue message from any of hello following types:</span></span>

* <span data-ttu-id="93582-161">Qualsiasi [oggetto](https://msdn.microsoft.com/library/system.object.aspx): la definizione dei parametri è simile a `out T paramName` (C#).</span><span class="sxs-lookup"><span data-stu-id="93582-161">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - Parameter definition looks like `out T paramName` (C#).</span></span>
  <span data-ttu-id="93582-162">Funzioni deserializza l'oggetto hello in un messaggio JSON.</span><span class="sxs-lookup"><span data-stu-id="93582-162">Functions deserializes hello object into a JSON message.</span></span> <span data-ttu-id="93582-163">Se il valore di output di hello è null quando si esce dalla funzione hello, funzioni Crea messaggio hello con un oggetto null.</span><span class="sxs-lookup"><span data-stu-id="93582-163">If hello output value is null when hello function exits, Functions creates hello message with a null object.</span></span>
* <span data-ttu-id="93582-164">`string`: la definizione dei parametri è simile a `out string paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="93582-164">`string` - Parameter definition looks like `out string paraName` (C#).</span></span> <span data-ttu-id="93582-165">Se il valore di parametro hello è non null quando si esce dalla funzione hello, funzioni di crea un messaggio.</span><span class="sxs-lookup"><span data-stu-id="93582-165">If hello parameter value is non-null when hello function exits, Functions creates a message.</span></span>
* <span data-ttu-id="93582-166">`byte[]`: la definizione dei parametri è simile a `out byte[] paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="93582-166">`byte[]` - Parameter definition looks like `out byte[] paraName` (C#).</span></span> <span data-ttu-id="93582-167">Se il valore di parametro hello è non null quando si esce dalla funzione hello, funzioni di crea un messaggio.</span><span class="sxs-lookup"><span data-stu-id="93582-167">If hello parameter value is non-null when hello function exits, Functions creates a message.</span></span>
* <span data-ttu-id="93582-168">`BrokeredMessage`: la definizione dei parametri è simile a `out BrokeredMessage paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="93582-168">`BrokeredMessage` Parameter definition looks like `out BrokeredMessage paraName` (C#).</span></span> <span data-ttu-id="93582-169">Se il valore di parametro hello è non null quando si esce dalla funzione hello, funzioni di crea un messaggio.</span><span class="sxs-lookup"><span data-stu-id="93582-169">If hello parameter value is non-null when hello function exits, Functions creates a message.</span></span>

<span data-ttu-id="93582-170">Per la creazione di più messaggi in una funzione C# è possibile usare `ICollector<T>` o `IAsyncCollector<T>`.</span><span class="sxs-lookup"><span data-stu-id="93582-170">For creating multiple messages in a C# function, you can use `ICollector<T>` or `IAsyncCollector<T>`.</span></span> <span data-ttu-id="93582-171">Viene creato un messaggio quando si chiama hello `Add` metodo.</span><span class="sxs-lookup"><span data-stu-id="93582-171">A message is created when you call hello `Add` method.</span></span>

<span data-ttu-id="93582-172">In Node.js, è possibile assegnare una stringa, una matrice di byte o un oggetto Javascript (deserializzato in JSON) troppo`context.binding.<paramName>`.</span><span class="sxs-lookup"><span data-stu-id="93582-172">In Node.js, you can assign a string, a byte array, or a Javascript object (deserialized into JSON) too`context.binding.<paramName>`.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="93582-173">Esempio di output</span><span class="sxs-lookup"><span data-stu-id="93582-173">Output sample</span></span>
<span data-ttu-id="93582-174">Si supponga di avere seguito function.json hello, che definisce un output di coda del Bus di servizio:</span><span class="sxs-lookup"><span data-stu-id="93582-174">Suppose you have hello following function.json, that defines a Service Bus queue output:</span></span>

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

<span data-ttu-id="93582-175">Vedere l'esempio specifico del linguaggio hello che invia la coda di messaggi toohello service bus.</span><span class="sxs-lookup"><span data-stu-id="93582-175">See hello language-specific sample that sends a message toohello service bus queue.</span></span>

* [<span data-ttu-id="93582-176">C#</span><span class="sxs-lookup"><span data-stu-id="93582-176">C#</span></span>](#outcsharp)
* [<span data-ttu-id="93582-177">F#</span><span class="sxs-lookup"><span data-stu-id="93582-177">F#</span></span>](#outfsharp)
* [<span data-ttu-id="93582-178">Node.JS</span><span class="sxs-lookup"><span data-stu-id="93582-178">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="93582-179">Esempio di output in C#</span><span class="sxs-lookup"><span data-stu-id="93582-179">Output sample in C#</span></span> #

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, out string outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue = message;
}
```

<span data-ttu-id="93582-180">In alternativa, toocreate più messaggi:</span><span class="sxs-lookup"><span data-stu-id="93582-180">Or, toocreate multiple messages:</span></span>

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

### <a name="output-sample-in-f"></a><span data-ttu-id="93582-181">Esempio di output in F#</span><span class="sxs-lookup"><span data-stu-id="93582-181">Output sample in F#</span></span> #

```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter, outputSbQueue: byref<string>) =
    let message = sprintf "Service Bus queue message created at: %s" (DateTime.Now.ToString())
    log.Info(message)
    outputSbQueue = message
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="93582-182">Esempio di output in Node.js</span><span class="sxs-lookup"><span data-stu-id="93582-182">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = message;
    context.done();
};
```

<span data-ttu-id="93582-183">In alternativa, toocreate più messaggi:</span><span class="sxs-lookup"><span data-stu-id="93582-183">Or, toocreate multiple messages:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="93582-184">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="93582-184">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

