---
title: Trigger e associazioni del bus di servizio di Azure di Funzioni di Azure | Microsoft Docs
description: Informazioni su come usare trigger e associazioni del bus di servizio di Azure in Funzioni di Azure.
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
ms.openlocfilehash: b3ee306cd37ebf88dc9369ccc2dc6c670557fd5a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-service-bus-bindings"></a><span data-ttu-id="06db1-104">Associazioni del bus di servizio di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="06db1-104">Azure Functions Service Bus bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="06db1-105">Questo articolo illustra come configurare e operare con il codice per associazioni del bus di servizio di Azure in Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="06db1-105">This article explains how to configure and work with Azure Service Bus bindings in Azure Functions.</span></span> 

<span data-ttu-id="06db1-106">Funzioni di Azure supporta il trigger e le associazioni di output per le code e gli argomenti del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="06db1-106">Azure Functions supports trigger and output bindings for Service Bus queues and topics.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="service-bus-trigger"></a><span data-ttu-id="06db1-107">Trigger di bus di servizio</span><span class="sxs-lookup"><span data-stu-id="06db1-107">Service Bus trigger</span></span>
<span data-ttu-id="06db1-108">Usare il trigger di bus di servizio per rispondere a messaggi da una coda o da un argomento del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="06db1-108">Use the Service Bus trigger to respond to messages from a Service Bus queue or topic.</span></span> 

<span data-ttu-id="06db1-109">I trigger della coda e dell'argomento del bus di servizio sono definiti dagli oggetti JSON seguenti nella matrice `bindings` di function.json:</span><span class="sxs-lookup"><span data-stu-id="06db1-109">The Service Bus queue and topic triggers are defined by the following JSON objects in the `bindings` array of function.json:</span></span>

* <span data-ttu-id="06db1-110">trigger della *coda*:</span><span class="sxs-lookup"><span data-stu-id="06db1-110">*queue* trigger:</span></span>

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "queueName" : "<Name of the queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for the connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

* <span data-ttu-id="06db1-111">trigger dell'*argomento*:</span><span class="sxs-lookup"><span data-stu-id="06db1-111">*topic* trigger:</span></span>

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "topicName" : "<Name of the topic>",
        "subscriptionName" : "<Name of the subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for the connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

<span data-ttu-id="06db1-112">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="06db1-112">Note the following:</span></span>

* <span data-ttu-id="06db1-113">Per `connection`, [creare un'impostazione nell'app per le funzioni](functions-how-to-use-azure-function-app-settings.md) che contenga la stringa di connessione allo spazio dei nomi del bus di servizio, quindi specificare il nome dell'impostazione dell'app nella proprietà `connection` del trigger.</span><span class="sxs-lookup"><span data-stu-id="06db1-113">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains the connection string to your Service Bus namespace, then specify the name of the app setting in the `connection` property in your trigger.</span></span> <span data-ttu-id="06db1-114">Ottenere la stringa di connessione seguendo i passaggi illustrati in [Ottenere le credenziali di gestione](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span><span class="sxs-lookup"><span data-stu-id="06db1-114">You obtain the connection string by following the steps shown at [Obtain the management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="06db1-115">La stringa di connessione deve essere relativa a uno spazio dei nomi del bus di servizio e non limitata a una coda o un argomento specifico.</span><span class="sxs-lookup"><span data-stu-id="06db1-115">The connection string must be for a Service Bus namespace, not limited to a specific queue or topic.</span></span>
  <span data-ttu-id="06db1-116">Se si lascia `connection` vuoto, il trigger presuppone che una stringa di connessione del bus di servizio predefinito sia specificata nell'impostazione dell'app denominata `AzureWebJobsServiceBus`.</span><span class="sxs-lookup"><span data-stu-id="06db1-116">If you leave `connection` empty, the trigger assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="06db1-117">Per `accessRights`, i valori disponibili sono `manage` e `listen`.</span><span class="sxs-lookup"><span data-stu-id="06db1-117">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="06db1-118">Il valore predefinito è `manage`, che indica che `connection` dispone dell'autorizzazione **Gestisci**.</span><span class="sxs-lookup"><span data-stu-id="06db1-118">The default is `manage`, which indicates that the `connection` has the **Manage** permission.</span></span> <span data-ttu-id="06db1-119">Se si usa una stringa di connessione che non dispone dell'autorizzazione **Gestisci**, impostare `accessRights` su `listen`.</span><span class="sxs-lookup"><span data-stu-id="06db1-119">If you use a connection string that does not have the **Manage** permission, set `accessRights` to `listen`.</span></span> <span data-ttu-id="06db1-120">In caso contrario, il runtime di Funzioni potrebbe non riuscire a eseguire operazioni che richiedono diritti di gestione.</span><span class="sxs-lookup"><span data-stu-id="06db1-120">Otherwise, the Functions runtime might fail trying to do operations that require manage rights.</span></span>

## <a name="trigger-behavior"></a><span data-ttu-id="06db1-121">Comportamento di trigger</span><span class="sxs-lookup"><span data-stu-id="06db1-121">Trigger behavior</span></span>
* <span data-ttu-id="06db1-122">**Single threading**: per impostazione predefinita il runtime di Funzioni elabora più messaggi contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="06db1-122">**Single-threading** - By default, the Functions runtime processes multiple messages concurrently.</span></span> <span data-ttu-id="06db1-123">Per impostare il runtime in modo che elabori un solo messaggio della coda o dell'argomento alla volta, impostare `serviceBus.maxConcurrentCalls` su 1 in *host.json*.</span><span class="sxs-lookup"><span data-stu-id="06db1-123">To direct the runtime to process only a single queue or topic message at a time, set `serviceBus.maxConcurrentCalls` to 1 in *host.json*.</span></span> 
  <span data-ttu-id="06db1-124">Per informazioni su *host.json*, vedere la [Struttura di cartelle](functions-reference.md#folder-structure) e [host.json](https://github .com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="06db1-124">For information about *host.json*, see [Folder Structure](functions-reference.md#folder-structure) and [host.json](https://github .com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>
* <span data-ttu-id="06db1-125">**Gestione dei messaggi non elaborabili**: il bus di servizio esegue la gestione dei messaggi non elaborabili in modo autonomo, non controllabile o modificabile nella configurazione o nel codice di Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="06db1-125">**Poison message handling** - Service Bus does its own poison message handling, which can't be controlled or configured in Azure Functions configuration or code.</span></span> 
* <span data-ttu-id="06db1-126">**Comportamento di PeekLock**: il runtime di Funzioni riceve un messaggio in modalità [`PeekLock` ](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) e chiama `Complete` sul messaggio se la funzione viene completata correttamente oppure `Abandon` se la funzione ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="06db1-126">**PeekLock behavior** - The Functions runtime receives a message in [`PeekLock` mode](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) and calls `Complete` on the message if the function finishes successfully, or calls `Abandon` if the function fails.</span></span> 
  <span data-ttu-id="06db1-127">Se il tempo di esecuzione della funzione supera il timeout di `PeekLock` , il blocco viene rinnovato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="06db1-127">If the function runs longer than the `PeekLock` timeout, the lock is automatically renewed.</span></span>

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="06db1-128">Uso dei trigger</span><span class="sxs-lookup"><span data-stu-id="06db1-128">Trigger usage</span></span>
<span data-ttu-id="06db1-129">Questa sezione illustra come usare il trigger del bus di servizio nel codice di funzione.</span><span class="sxs-lookup"><span data-stu-id="06db1-129">This section shows you how to use your Service Bus trigger in your function code.</span></span> 

<span data-ttu-id="06db1-130">In C# ed F# il messaggio di trigger di bus di servizio può essere deserializzato in uno qualsiasi dei seguenti tipi:</span><span class="sxs-lookup"><span data-stu-id="06db1-130">In C# and F#, the Service Bus trigger message can be deserialized to any of the following input types:</span></span>

* <span data-ttu-id="06db1-131">`string`: utile per i messaggi di stringa</span><span class="sxs-lookup"><span data-stu-id="06db1-131">`string` - useful for string messages</span></span>
* <span data-ttu-id="06db1-132">`byte[]`: utile per i dati binari</span><span class="sxs-lookup"><span data-stu-id="06db1-132">`byte[]` - useful for binary data</span></span>
* <span data-ttu-id="06db1-133">Qualsiasi [oggetto](https://msdn.microsoft.com/library/system.object.aspx): utile per i dati serializzati con JSON.</span><span class="sxs-lookup"><span data-stu-id="06db1-133">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized data.</span></span>
  <span data-ttu-id="06db1-134">Se si dichiara un tipo di input personalizzato, ad esempio `CustomType`, Funzioni di Azure tenta di deserializzare i dati JSON nel tipo specificato.</span><span class="sxs-lookup"><span data-stu-id="06db1-134">If you declare a custom input type, such as `CustomType`, Azure Functions tries to deserialize the JSON data into your specified type.</span></span>
* <span data-ttu-id="06db1-135">`BrokeredMessage`: visualizza il messaggio deserializzato con il metodo [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx).</span><span class="sxs-lookup"><span data-stu-id="06db1-135">`BrokeredMessage` - gives you the deserialized message with the [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) method.</span></span>

<span data-ttu-id="06db1-136">In Node. js, il messaggio di trigger di bus di servizio viene passato alla funzione come stringa o come oggetto JSON.</span><span class="sxs-lookup"><span data-stu-id="06db1-136">In Node.js, the Service Bus trigger message is passed into the function as either a string or JSON object.</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="06db1-137">Esempio di trigger</span><span class="sxs-lookup"><span data-stu-id="06db1-137">Trigger sample</span></span>
<span data-ttu-id="06db1-138">Si supponga di disporre del file function.json seguente:</span><span class="sxs-lookup"><span data-stu-id="06db1-138">Suppose you have the following function.json:</span></span>

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

<span data-ttu-id="06db1-139">Vedere l'esempio specifico per la lingua che elabora un messaggio di coda del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="06db1-139">See the language-specific sample that processes a Service Bus queue message.</span></span>

* [<span data-ttu-id="06db1-140">C#</span><span class="sxs-lookup"><span data-stu-id="06db1-140">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="06db1-141">F#</span><span class="sxs-lookup"><span data-stu-id="06db1-141">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="06db1-142">Node.JS</span><span class="sxs-lookup"><span data-stu-id="06db1-142">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="06db1-143">Esempio di trigger in C#</span><span class="sxs-lookup"><span data-stu-id="06db1-143">Trigger sample in C#</span></span> #

```cs
public static void Run(string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a><span data-ttu-id="06db1-144">Esempio di trigger in F#</span><span class="sxs-lookup"><span data-stu-id="06db1-144">Trigger sample in F#</span></span> #

```fsharp
let Run(myQueueItem: string, log: TraceWriter) =
    log.Info(sprintf "F# ServiceBus queue trigger function processed message: %s" myQueueItem)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="06db1-145">Esempio di trigger in Node.js</span><span class="sxs-lookup"><span data-stu-id="06db1-145">Trigger sample in Node.js</span></span>

```javascript
module.exports = function(context, myQueueItem) {
    context.log('Node.js ServiceBus queue trigger function processed message', myQueueItem);
    context.done();
};
```

<a name="output"></a>

## <a name="service-bus-output-binding"></a><span data-ttu-id="06db1-146">Associazione di output di bus di servizio</span><span class="sxs-lookup"><span data-stu-id="06db1-146">Service Bus output binding</span></span>
<span data-ttu-id="06db1-147">Gli output della coda e dell'argomento del bus di servizio per una funzione usa gli oggetti JSON seguenti nella matrice `bindings` di function.json:</span><span class="sxs-lookup"><span data-stu-id="06db1-147">The Service Bus queue and topic output for a function use the following JSON objects in the `bindings` array of function.json:</span></span>

* <span data-ttu-id="06db1-148">output di *coda*:</span><span class="sxs-lookup"><span data-stu-id="06db1-148">*queue* output:</span></span>

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "queueName" : "<Name of the queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for the connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```
* <span data-ttu-id="06db1-149">output di *argomento*:</span><span class="sxs-lookup"><span data-stu-id="06db1-149">*topic* output:</span></span>

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "topicName" : "<Name of the topic>",
        "subscriptionName" : "<Name of the subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for the connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```

<span data-ttu-id="06db1-150">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="06db1-150">Note the following:</span></span>

* <span data-ttu-id="06db1-151">Per `connection`, [creare un'impostazione nell'app per le funzioni](functions-how-to-use-azure-function-app-settings.md) che contenga la stringa di connessione allo spazio dei nomi del bus di servizio, quindi specificare il nome dell'impostazione dell'app nella proprietà `connection` dell'associazione di output.</span><span class="sxs-lookup"><span data-stu-id="06db1-151">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains the connection string to your Service Bus namespace, then specify the name of the app setting in the `connection` property in your output binding.</span></span> <span data-ttu-id="06db1-152">Ottenere la stringa di connessione seguendo i passaggi illustrati in [Ottenere le credenziali di gestione](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span><span class="sxs-lookup"><span data-stu-id="06db1-152">You obtain the connection string by following the steps shown at [Obtain the management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="06db1-153">La stringa di connessione deve essere relativa a uno spazio dei nomi del bus di servizio e non limitata a una coda o un argomento specifico.</span><span class="sxs-lookup"><span data-stu-id="06db1-153">The connection string must be for a Service Bus namespace, not limited to a specific queue or topic.</span></span>
  <span data-ttu-id="06db1-154">Se si lascia `connection` vuoto, l'associazione di output presuppone che una stringa di connessione del bus di servizio predefinito sia specificata nell'impostazione dell'app denominata `AzureWebJobsServiceBus`.</span><span class="sxs-lookup"><span data-stu-id="06db1-154">If you leave `connection` empty, the output binding assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="06db1-155">Per `accessRights`, i valori disponibili sono `manage` e `listen`.</span><span class="sxs-lookup"><span data-stu-id="06db1-155">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="06db1-156">Il valore predefinito è `manage`, che indica che `connection` dispone dell'autorizzazione **Gestisci**.</span><span class="sxs-lookup"><span data-stu-id="06db1-156">The default is `manage`, which indicates that the `connection` has the **Manage** permission.</span></span> <span data-ttu-id="06db1-157">Se si usa una stringa di connessione che non dispone dell'autorizzazione **Gestisci**, impostare `accessRights` su `listen`.</span><span class="sxs-lookup"><span data-stu-id="06db1-157">If you use a connection string that does not have the **Manage** permission, set `accessRights` to `listen`.</span></span> <span data-ttu-id="06db1-158">In caso contrario, il runtime di Funzioni potrebbe non riuscire a eseguire operazioni che richiedono diritti di gestione.</span><span class="sxs-lookup"><span data-stu-id="06db1-158">Otherwise, the Functions runtime might fail trying to do operations that require manage rights.</span></span>

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="06db1-159">Uso dell'output</span><span class="sxs-lookup"><span data-stu-id="06db1-159">Output usage</span></span>
<span data-ttu-id="06db1-160">In C# e F#, Funzioni di Azure può creare un messaggio di coda del bus di servizio da uno qualsiasi dei tipi seguenti:</span><span class="sxs-lookup"><span data-stu-id="06db1-160">In C# and F#, Azure Functions can create a Service Bus queue message from any of the following types:</span></span>

* <span data-ttu-id="06db1-161">Qualsiasi [oggetto](https://msdn.microsoft.com/library/system.object.aspx): la definizione dei parametri è simile a `out T paramName` (C#).</span><span class="sxs-lookup"><span data-stu-id="06db1-161">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - Parameter definition looks like `out T paramName` (C#).</span></span>
  <span data-ttu-id="06db1-162">Funzioni deserializza l'oggetto in un messaggio JSON.</span><span class="sxs-lookup"><span data-stu-id="06db1-162">Functions deserializes the object into a JSON message.</span></span> <span data-ttu-id="06db1-163">Se il valore di output è null quando la funzione viene chiusa, Funzioni crea il messaggio con un oggetto null.</span><span class="sxs-lookup"><span data-stu-id="06db1-163">If the output value is null when the function exits, Functions creates the message with a null object.</span></span>
* <span data-ttu-id="06db1-164">`string`: la definizione dei parametri è simile a `out string paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="06db1-164">`string` - Parameter definition looks like `out string paraName` (C#).</span></span> <span data-ttu-id="06db1-165">Se il valore del parametro è diverso da null quando termina la funzione, Funzioni crea un messaggio.</span><span class="sxs-lookup"><span data-stu-id="06db1-165">If the parameter value is non-null when the function exits, Functions creates a message.</span></span>
* <span data-ttu-id="06db1-166">`byte[]`: la definizione dei parametri è simile a `out byte[] paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="06db1-166">`byte[]` - Parameter definition looks like `out byte[] paraName` (C#).</span></span> <span data-ttu-id="06db1-167">Se il valore del parametro è diverso da null quando termina la funzione, Funzioni crea un messaggio.</span><span class="sxs-lookup"><span data-stu-id="06db1-167">If the parameter value is non-null when the function exits, Functions creates a message.</span></span>
* <span data-ttu-id="06db1-168">`BrokeredMessage`: la definizione dei parametri è simile a `out BrokeredMessage paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="06db1-168">`BrokeredMessage` Parameter definition looks like `out BrokeredMessage paraName` (C#).</span></span> <span data-ttu-id="06db1-169">Se il valore del parametro è diverso da null quando termina la funzione, Funzioni crea un messaggio.</span><span class="sxs-lookup"><span data-stu-id="06db1-169">If the parameter value is non-null when the function exits, Functions creates a message.</span></span>

<span data-ttu-id="06db1-170">Per la creazione di più messaggi in una funzione C# è possibile usare `ICollector<T>` o `IAsyncCollector<T>`.</span><span class="sxs-lookup"><span data-stu-id="06db1-170">For creating multiple messages in a C# function, you can use `ICollector<T>` or `IAsyncCollector<T>`.</span></span> <span data-ttu-id="06db1-171">Quando si chiama il metodo `Add` viene creato un messaggio.</span><span class="sxs-lookup"><span data-stu-id="06db1-171">A message is created when you call the `Add` method.</span></span>

<span data-ttu-id="06db1-172">In Node. js, è possibile assegnare una stringa, una matrice di byte o un oggetto Javascript (deserializzato in JSON) a `context.binding.<paramName>`.</span><span class="sxs-lookup"><span data-stu-id="06db1-172">In Node.js, you can assign a string, a byte array, or a Javascript object (deserialized into JSON) to `context.binding.<paramName>`.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="06db1-173">Esempio di output</span><span class="sxs-lookup"><span data-stu-id="06db1-173">Output sample</span></span>
<span data-ttu-id="06db1-174">Si supponga di avere il seguente function.json, che definisce un output della coda di bus di servizio:</span><span class="sxs-lookup"><span data-stu-id="06db1-174">Suppose you have the following function.json, that defines a Service Bus queue output:</span></span>

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

<span data-ttu-id="06db1-175">Vedere l'esempio specifico per la lingua che invia un messaggio alla coda del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="06db1-175">See the language-specific sample that sends a message to the service bus queue.</span></span>

* [<span data-ttu-id="06db1-176">C#</span><span class="sxs-lookup"><span data-stu-id="06db1-176">C#</span></span>](#outcsharp)
* [<span data-ttu-id="06db1-177">F#</span><span class="sxs-lookup"><span data-stu-id="06db1-177">F#</span></span>](#outfsharp)
* [<span data-ttu-id="06db1-178">Node.JS</span><span class="sxs-lookup"><span data-stu-id="06db1-178">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="06db1-179">Esempio di output in C#</span><span class="sxs-lookup"><span data-stu-id="06db1-179">Output sample in C#</span></span> #

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, out string outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue = message;
}
```

<span data-ttu-id="06db1-180">Oppure per creare più messaggi:</span><span class="sxs-lookup"><span data-stu-id="06db1-180">Or, to create multiple messages:</span></span>

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

### <a name="output-sample-in-f"></a><span data-ttu-id="06db1-181">Esempio di output in F#</span><span class="sxs-lookup"><span data-stu-id="06db1-181">Output sample in F#</span></span> #

```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter, outputSbQueue: byref<string>) =
    let message = sprintf "Service Bus queue message created at: %s" (DateTime.Now.ToString())
    log.Info(message)
    outputSbQueue = message
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="06db1-182">Esempio di output in Node.js</span><span class="sxs-lookup"><span data-stu-id="06db1-182">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = message;
    context.done();
};
```

<span data-ttu-id="06db1-183">Oppure per creare più messaggi:</span><span class="sxs-lookup"><span data-stu-id="06db1-183">Or, to create multiple messages:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="06db1-184">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="06db1-184">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

