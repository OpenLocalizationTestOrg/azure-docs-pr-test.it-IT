---
title: Associazioni dell'archiviazione code di Funzioni di Azure | Microsoft Docs
description: Informazioni su come usare trigger e associazioni di Archiviazione di Azure in Funzioni di Azure.
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: Funzioni di Azure, Funzioni, elaborazione eventi, calcolo dinamico, architettura senza server
ms.assetid: 4e6a837d-e64f-45a0-87b7-aa02688a75f3
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: glenga
ms.openlocfilehash: e007acd75a2210d54f512e2c6698c90919f0fcd2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-queue-storage-bindings"></a><span data-ttu-id="2e1e4-104">Associazione dell'archiviazione code di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="2e1e4-104">Azure Functions Queue Storage bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="2e1e4-105">Questo articolo illustra come configurare e scrivere il codice delle associazioni archiviazione code di Azure in Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-105">This article describes how to configure and code Azure Queue storage bindings in Azure Functions.</span></span> <span data-ttu-id="2e1e4-106">Funzioni di Azure supporta il trigger e le associazioni di output per le code di Azure.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-106">Azure Functions supports trigger and output bindings for Azure queues.</span></span> <span data-ttu-id="2e1e4-107">Per le funzionalità disponibili in tutte le associazioni, vedere [Concetti di Trigger e associazioni di Funzioni di Azure](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="2e1e4-107">For features that are available in all bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="queue-storage-trigger"></a><span data-ttu-id="2e1e4-108">Trigger per l'archiviazione code</span><span class="sxs-lookup"><span data-stu-id="2e1e4-108">Queue storage trigger</span></span>
<span data-ttu-id="2e1e4-109">Il trigger dell'archiviazione code di Azure consente di monitorare l'archiviazione code di nuovi messaggi e di intraprendere le azioni necessarie.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-109">The Azure Queue storage trigger enables you to monitor a queue storage for new messages and react to them.</span></span> 

<span data-ttu-id="2e1e4-110">Definire un trigger di coda usando la scheda **Integrazione** nel portale Funzioni.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-110">Define a queue trigger using the **Integrate** tab in the Functions portal.</span></span> <span data-ttu-id="2e1e4-111">Il portale crea la definizione seguente nella sezione **associazioni** di *function.json*:</span><span class="sxs-lookup"><span data-stu-id="2e1e4-111">The portal creates the following definition in the  **bindings** section of *function.json*:</span></span>

```json
{
    "type": "queueTrigger",
    "direction": "in",
    "name": "<The name used to identify the trigger data in your code>",
    "queueName": "<Name of queue to poll>",
    "connection":"<Name of app setting - see below>"
}
```

* <span data-ttu-id="2e1e4-112">La proprietà `connection` deve contenere il nome di un'impostazione app che contiene una stringa di connessione alla risorsa di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-112">The `connection` property must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="2e1e4-113">Nel portale di Azure l'editor standard disponibile nella scheda **Integrazione** configura questa impostazione app quando si sceglie un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-113">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

<span data-ttu-id="2e1e4-114">È possibile specificare impostazioni aggiuntive in un [file host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) per ottimizzare i trigger dell'archiviazione code.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-114">Additional settings can be provided in a [host.json file](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) to further fine-tune queue storage triggers.</span></span> <span data-ttu-id="2e1e4-115">Ad esempio, è possibile modificare l'intervallo di polling della coda in host.json.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-115">For example, you can change the queue polling interval in host.json.</span></span>

<a name="triggerusage"></a>

## <a name="using-a-queue-trigger"></a><span data-ttu-id="2e1e4-116">Uso di un trigger della coda</span><span class="sxs-lookup"><span data-stu-id="2e1e4-116">Using a queue trigger</span></span>
<span data-ttu-id="2e1e4-117">Nelle funzioni Node.js si accede ai dati della coda usando `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-117">In Node.js functions, access the queue data using `context.bindings.<name>`.</span></span>


<span data-ttu-id="2e1e4-118">Nelle funzioni .NET è possibile accedere al payload della coda con un parametro del metodo, ad esempio `CloudQueueMessage paramName`.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-118">In .NET functions, access the queue payload using a method parameter such as `CloudQueueMessage paramName`.</span></span> <span data-ttu-id="2e1e4-119">In questo caso, `paramName` è il valore specificato nella [configurazione del trigger](#trigger).</span><span class="sxs-lookup"><span data-stu-id="2e1e4-119">Here, `paramName` is the value you specified in the [trigger configuration](#trigger).</span></span> <span data-ttu-id="2e1e4-120">Il messaggio della coda può essere deserializzato in uno qualsiasi dei seguenti tipi:</span><span class="sxs-lookup"><span data-stu-id="2e1e4-120">The queue message can be deserialized to any of the following types:</span></span>

* <span data-ttu-id="2e1e4-121">Oggetto POCO.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-121">POCO object.</span></span> <span data-ttu-id="2e1e4-122">Usare se il payload della coda è un oggetto JSON.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-122">Use if the queue payload is a JSON object.</span></span> <span data-ttu-id="2e1e4-123">Il runtime di Funzioni deserializza il payload nell'oggetto POCO.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-123">The Functions runtime deserializes the payload into the POCO object.</span></span> 
* `string`
* `byte[]`
* [`CloudQueueMessage`]

<a name="meta"></a>

### <a name="queue-trigger-metadata"></a><span data-ttu-id="2e1e4-124">Metadati del trigger della coda</span><span class="sxs-lookup"><span data-stu-id="2e1e4-124">Queue trigger metadata</span></span>
<span data-ttu-id="2e1e4-125">Il trigger della coda contiene diverse proprietà di metadati.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-125">The queue trigger provides several metadata properties.</span></span> <span data-ttu-id="2e1e4-126">Queste proprietà possono essere usate come parte delle espressioni di associazione in altre associazioni o come parametri nel codice.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-126">These properties can be used as part of binding expressions in other bindings or as parameters in your code.</span></span> <span data-ttu-id="2e1e4-127">I valori hanno la stessa semantica di [`CloudQueueMessage`].</span><span class="sxs-lookup"><span data-stu-id="2e1e4-127">The values have the same semantics as [`CloudQueueMessage`].</span></span>

* <span data-ttu-id="2e1e4-128">**QueueTrigger**: payload della coda, se si tratta di una stringa valida</span><span class="sxs-lookup"><span data-stu-id="2e1e4-128">**QueueTrigger** - queue payload (if a valid string)</span></span>
* <span data-ttu-id="2e1e4-129">**DequeueCount**: digitare `int`.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-129">**DequeueCount** - Type `int`.</span></span> <span data-ttu-id="2e1e4-130">Il numero di volte in cui questo messaggio è stato rimosso dalla coda.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-130">The number of times this message has been dequeued.</span></span>
* <span data-ttu-id="2e1e4-131">**ExpirationTime**: digitare `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-131">**ExpirationTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="2e1e4-132">Ora di scadenza del messaggio.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-132">The time that the message expires.</span></span>
* <span data-ttu-id="2e1e4-133">**Id**: digitare `string`.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-133">**Id** - Type `string`.</span></span> <span data-ttu-id="2e1e4-134">ID del messaggio in coda.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-134">Queue message ID.</span></span>
* <span data-ttu-id="2e1e4-135">**InsertionTime**: digitare `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-135">**InsertionTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="2e1e4-136">L'ora in cui il messaggio è stato aggiunto alla coda.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-136">The time that the message was added to the queue.</span></span>
* <span data-ttu-id="2e1e4-137">**NextVisibleTime** - Tipo `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-137">**NextVisibleTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="2e1e4-138">Ora in cui il messaggio sarà visibile.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-138">The time that the message will next be visible.</span></span>
* <span data-ttu-id="2e1e4-139">**PopReceipt**: digitare `string`.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-139">**PopReceipt** - Type `string`.</span></span> <span data-ttu-id="2e1e4-140">Ricezione del messaggio.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-140">The message's pop receipt.</span></span>

<span data-ttu-id="2e1e4-141">Per informazioni su come usare i metadati della coda, vedere l'[esempio di trigger](#triggersample).</span><span class="sxs-lookup"><span data-stu-id="2e1e4-141">See how to use the queue metadata in [Trigger sample](#triggersample).</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="2e1e4-142">Esempio di trigger</span><span class="sxs-lookup"><span data-stu-id="2e1e4-142">Trigger sample</span></span>
<span data-ttu-id="2e1e4-143">Si supponga di avere il seguente function.json, che definisce un trigger della coda:</span><span class="sxs-lookup"><span data-stu-id="2e1e4-143">Suppose you have the following function.json that defines a queue trigger:</span></span>

```json
{
    "disabled": false,
    "bindings": [
        {
            "type": "queueTrigger",
            "direction": "in",
            "name": "myQueueItem",
            "queueName": "myqueue-items",
            "connection":"MyStorageConnectionString"
        }
    ]
}
```

<span data-ttu-id="2e1e4-144">Vedere l'esempio specifico del linguaggio che recupera e registra i metadati della coda.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-144">See the language-specific sample that retrieves and logs queue metadata.</span></span>

* [<span data-ttu-id="2e1e4-145">C#</span><span class="sxs-lookup"><span data-stu-id="2e1e4-145">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="2e1e4-146">Node.js</span><span class="sxs-lookup"><span data-stu-id="2e1e4-146">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="2e1e4-147">Esempio di trigger in C#</span><span class="sxs-lookup"><span data-stu-id="2e1e4-147">Trigger sample in C#</span></span> #
```csharp
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Queue;
using System;

public static void Run(CloudQueueMessage myQueueItem, 
    DateTimeOffset expirationTime, 
    DateTimeOffset insertionTime, 
    DateTimeOffset nextVisibleTime,
    string queueTrigger,
    string id,
    string popReceipt,
    int dequeueCount,
    TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem.AsString}\n" +
        $"queueTrigger={queueTrigger}\n" +
        $"expirationTime={expirationTime}\n" +
        $"insertionTime={insertionTime}\n" +
        $"nextVisibleTime={nextVisibleTime}\n" +
        $"id={id}\n" +
        $"popReceipt={popReceipt}\n" + 
        $"dequeueCount={dequeueCount}");
}
```

<!--
<a name="triggerfsharp"></a>
### Trigger sample in F# ## 
```fsharp

```
-->

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="2e1e4-148">Esempio di trigger in Node.js</span><span class="sxs-lookup"><span data-stu-id="2e1e4-148">Trigger sample in Node.js</span></span>

```javascript
module.exports = function (context) {
    context.log('Node.js queue trigger function processed work item', context.bindings.myQueueItem);
    context.log('queueTrigger =', context.bindingData.queueTrigger);
    context.log('expirationTime =', context.bindingData.expirationTime);
    context.log('insertionTime =', context.bindingData.insertionTime);
    context.log('nextVisibleTime =', context.bindingData.nextVisibleTime);
    context.log('id=', context.bindingData.id);
    context.log('popReceipt =', context.bindingData.popReceipt);
    context.log('dequeueCount =', context.bindingData.dequeueCount);
    context.done();
};
```

### <a name="handling-poison-queue-messages"></a><span data-ttu-id="2e1e4-149">Gestione di messaggi della coda non elaborabili</span><span class="sxs-lookup"><span data-stu-id="2e1e4-149">Handling poison queue messages</span></span>
<span data-ttu-id="2e1e4-150">Quando una funzione di trigger della coda ha esito negativo, Funzioni di Azure ritenta l'esecuzione fino a cinque volte per un dato messaggio della coda, incluso il primo tentativo.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-150">When a queue trigger function fails, Azure Functions retries that function up to five times for a given queue message, including the first try.</span></span> <span data-ttu-id="2e1e4-151">Se tutti i cinque tentativi hanno esito negativo, il runtime di Funzioni aggiunge un messaggio a un'archiviazione code denominata *&lt;originalqueuename>-poison*.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-151">If all five attempts fail, the functions runtime adds a message to a queue storage named *&lt;originalqueuename>-poison*.</span></span> <span data-ttu-id="2e1e4-152">È possibile scrivere una funzione per elaborare i messaggi dalla coda non elaborabile archiviandoli o inviando una notifica della necessità di un intervento manuale.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-152">You can write a function to process messages from the poison queue by logging them or sending a  notification that manual attention is needed.</span></span> 

<span data-ttu-id="2e1e4-153">Per gestire manualmente i messaggi non elaborabili, controllare `dequeueCount` nel messaggio della coda. Vedere [Metadati del trigger della coda](#meta).</span><span class="sxs-lookup"><span data-stu-id="2e1e4-153">To handle poison messages manually, check the `dequeueCount` of the queue message (see [Queue trigger metadata](#meta)).</span></span>

<a name="output"></a>

## <a name="queue-storage-output-binding"></a><span data-ttu-id="2e1e4-154">Associazione di output dell'archiviazione code</span><span class="sxs-lookup"><span data-stu-id="2e1e4-154">Queue storage output binding</span></span>
<span data-ttu-id="2e1e4-155">L'associazione di output dell'archiviazione code di Azure consente di scrivere i messaggi in una coda.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-155">The Azure queue storage output binding enables you to write messages to a queue.</span></span> 

<span data-ttu-id="2e1e4-156">Definire un'associazione di output in coda usando la scheda **Integrazione** nel portale Funzioni.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-156">Define a queue output binding using the **Integrate** tab in the Functions portal.</span></span> <span data-ttu-id="2e1e4-157">Il portale crea la definizione seguente nella sezione **associazioni** di *function.json*:</span><span class="sxs-lookup"><span data-stu-id="2e1e4-157">The portal creates the following definition in the  **bindings** section of *function.json*:</span></span>

```json
{
   "type": "queue",
   "direction": "out",
   "name": "<The name used to identify the trigger data in your code>",
   "queueName": "<Name of queue to write to>",
   "connection":"<Name of app setting - see below>"
}
```

* <span data-ttu-id="2e1e4-158">La proprietà `connection` deve contenere il nome di un'impostazione app che contiene una stringa di connessione alla risorsa di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-158">The `connection` property must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="2e1e4-159">Nel portale di Azure l'editor standard disponibile nella scheda **Integrazione** configura questa impostazione app quando si sceglie un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-159">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

<a name="outputusage"></a>

## <a name="using-a-queue-output-binding"></a><span data-ttu-id="2e1e4-160">Uso dell'associazione di output della coda</span><span class="sxs-lookup"><span data-stu-id="2e1e4-160">Using a queue output binding</span></span>
<span data-ttu-id="2e1e4-161">Nelle funzioni Node.js si accede alla coda di output usando `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-161">In Node.js functions, you access the output queue using `context.bindings.<name>`.</span></span>

<span data-ttu-id="2e1e4-162">Nelle funzioni .NET è anche possibile eseguire l'output in uno dei tipi seguenti.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-162">In .NET functions, you can output to any of the following types.</span></span> <span data-ttu-id="2e1e4-163">Quando vi è un parametro di tipo `T`, `T` deve essere uno dei tipi di output supportati, ad esempio `string` o un oggetto POCO.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-163">When there is a type parameter `T`, `T` must be one of the supported output types, such as `string` or a POCO.</span></span>

* <span data-ttu-id="2e1e4-164">`out T`, serializzato come JSON</span><span class="sxs-lookup"><span data-stu-id="2e1e4-164">`out T` (serialized as JSON)</span></span>
* `out string`
* `out byte[]`
* <span data-ttu-id="2e1e4-165">`out` [`CloudQueueMessage`]</span><span class="sxs-lookup"><span data-stu-id="2e1e4-165">`out` [`CloudQueueMessage`]</span></span> 
* `ICollector<T>`
* `IAsyncCollector<T>`
* [`CloudQueue`](/dotnet/api/microsoft.windowsazure.storage.queue.cloudqueue)

<span data-ttu-id="2e1e4-166">È anche possibile usare il tipo restituito del metodo come associazione di output.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-166">You can also use the method return type as the output binding.</span></span>

<a name="outputsample"></a>

## <a name="queue-output-sample"></a><span data-ttu-id="2e1e4-167">Esempio di output in coda</span><span class="sxs-lookup"><span data-stu-id="2e1e4-167">Queue output sample</span></span>
<span data-ttu-id="2e1e4-168">*function.json* seguente definisce un trigger HTTP e un'associazione di output della coda:</span><span class="sxs-lookup"><span data-stu-id="2e1e4-168">The following *function.json* defines an HTTP trigger with a queue output binding:</span></span>

```json
{
  "bindings": [
    {
      "type": "httpTrigger",
      "direction": "in",
      "authLevel": "function",
      "name": "input"
    },
    {
      "type": "http",
      "direction": "out",
      "name": "return"
    },
    {
      "type": "queue",
      "direction": "out",
      "name": "$return",
      "queueName": "outqueue",
      "connection": "MyStorageConnectionString",
    }
  ]
}
``` 

<span data-ttu-id="2e1e4-169">Vedere l'esempio specifico del linguaggio che restituisce un messaggio in coda con il payload HTTP in ingresso.</span><span class="sxs-lookup"><span data-stu-id="2e1e4-169">See the language-specific sample that outputs a queue message with the incoming HTTP payload.</span></span>

* [<span data-ttu-id="2e1e4-170">C#</span><span class="sxs-lookup"><span data-stu-id="2e1e4-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="2e1e4-171">Node.js</span><span class="sxs-lookup"><span data-stu-id="2e1e4-171">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="queue-output-sample-in-c"></a><span data-ttu-id="2e1e4-172">Esempio di output della coda in C#</span><span class="sxs-lookup"><span data-stu-id="2e1e4-172">Queue output sample in C#</span></span> #

```cs
// C# example of HTTP trigger binding to a custom POCO, with a queue output binding
public class CustomQueueMessage
{
    public string PersonName { get; set; }
    public string Title { get; set; }
}

public static CustomQueueMessage Run(CustomQueueMessage input, TraceWriter log)
{
    return input;
}
```

<span data-ttu-id="2e1e4-173">Per inviare più messaggi, usare `ICollector`:</span><span class="sxs-lookup"><span data-stu-id="2e1e4-173">To send multiple messages, use an `ICollector`:</span></span>

```cs
public static void Run(CustomQueueMessage input, ICollector<CustomQueueMessage> myQueueItem, TraceWriter log)
{
    myQueueItem.Add(input);
    myQueueItem.Add(new CustomQueueMessage { PersonName = "You", Title = "None" });
}
```

<a name="outnodejs"></a>

### <a name="queue-output-sample-in-nodejs"></a><span data-ttu-id="2e1e4-174">Esempio di output della coda in Node.js</span><span class="sxs-lookup"><span data-stu-id="2e1e4-174">Queue output sample in Node.js</span></span>

```javascript
module.exports = function (context, input) {
    context.done(null, input.body);
};
```

<span data-ttu-id="2e1e4-175">Oppure, per inviare più messaggi,</span><span class="sxs-lookup"><span data-stu-id="2e1e4-175">Or, to send multiple messages,</span></span>

```javascript
module.exports = function(context) {
    // Define a message array for the myQueueItem output binding. 
    context.bindings.myQueueItem = ["message 1","message 2"];
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="2e1e4-176">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2e1e4-176">Next steps</span></span>

<span data-ttu-id="2e1e4-177">Per un esempio di funzione che usa trigger e associazioni della coda, vedere [Creare una funzione di Azure connessa a un servizio di Azure](functions-create-an-azure-connected-function.md).</span><span class="sxs-lookup"><span data-stu-id="2e1e4-177">For an example of a function that uses queue storage triggers and bindings, see [Create an Azure Function connected to an Azure service](functions-create-an-azure-connected-function.md).</span></span>

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

<!-- LINKS -->

["CloudQueueMessage"]: /dotnet/api/microsoft.windowsazure.storage.queue.cloudqueuemessage
