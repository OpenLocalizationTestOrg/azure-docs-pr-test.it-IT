---
title: associazioni di archiviazione della coda funzioni aaaAzure | Documenti Microsoft
description: Comprendere come toouse di archiviazione di Azure attiva e le associazioni in funzioni di Azure.
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
ms.openlocfilehash: 438b4f63e823149072c86fdefa7e15bfd2a2c4df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-queue-storage-bindings"></a><span data-ttu-id="b93ec-104">Associazione dell'archiviazione code di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="b93ec-104">Azure Functions Queue Storage bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="b93ec-105">Questo articolo viene descritto come associazioni di archiviazione Azure coda tooconfigure e codice nelle funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="b93ec-105">This article describes how tooconfigure and code Azure Queue storage bindings in Azure Functions.</span></span> <span data-ttu-id="b93ec-106">Funzioni di Azure supporta il trigger e le associazioni di output per le code di Azure.</span><span class="sxs-lookup"><span data-stu-id="b93ec-106">Azure Functions supports trigger and output bindings for Azure queues.</span></span> <span data-ttu-id="b93ec-107">Per le funzionalità disponibili in tutte le associazioni, vedere [Concetti di Trigger e associazioni di Funzioni di Azure](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="b93ec-107">For features that are available in all bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="queue-storage-trigger"></a><span data-ttu-id="b93ec-108">Trigger per l'archiviazione code</span><span class="sxs-lookup"><span data-stu-id="b93ec-108">Queue storage trigger</span></span>
<span data-ttu-id="b93ec-109">trigger di archiviazione di Azure coda Hello consente si toomonitor di archiviazione di Accodamento di nuovi messaggi e reagire toothem.</span><span class="sxs-lookup"><span data-stu-id="b93ec-109">hello Azure Queue storage trigger enables you toomonitor a queue storage for new messages and react toothem.</span></span> 

<span data-ttu-id="b93ec-110">Definire un trigger di coda utilizzando hello **integrazione** scheda nel portale le funzioni hello.</span><span class="sxs-lookup"><span data-stu-id="b93ec-110">Define a queue trigger using hello **Integrate** tab in hello Functions portal.</span></span> <span data-ttu-id="b93ec-111">portale Hello crea hello seguente definizione di hello **associazioni** sezione *function.json*:</span><span class="sxs-lookup"><span data-stu-id="b93ec-111">hello portal creates hello following definition in hello  **bindings** section of *function.json*:</span></span>

```json
{
    "type": "queueTrigger",
    "direction": "in",
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "queueName": "<Name of queue toopoll>",
    "connection":"<Name of app setting - see below>"
}
```

* <span data-ttu-id="b93ec-112">Hello `connection` proprietà deve contenere il nome di hello di un'impostazione di app che contiene una stringa di connessione di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b93ec-112">hello `connection` property must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="b93ec-113">Nel portale di Azure hello, hello editor standard di hello **integrazione** scheda configura questa impostazione di app per l'utente quando si seleziona un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b93ec-113">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

<span data-ttu-id="b93ec-114">È possibile specificare impostazioni aggiuntive un [host.json file](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) toofurther ottimizzare i trigger di archiviazione della coda.</span><span class="sxs-lookup"><span data-stu-id="b93ec-114">Additional settings can be provided in a [host.json file](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) toofurther fine-tune queue storage triggers.</span></span> <span data-ttu-id="b93ec-115">Ad esempio, è possibile modificare l'intervallo di polling della coda hello in host.json.</span><span class="sxs-lookup"><span data-stu-id="b93ec-115">For example, you can change hello queue polling interval in host.json.</span></span>

<a name="triggerusage"></a>

## <a name="using-a-queue-trigger"></a><span data-ttu-id="b93ec-116">Uso di un trigger della coda</span><span class="sxs-lookup"><span data-stu-id="b93ec-116">Using a queue trigger</span></span>
<span data-ttu-id="b93ec-117">Nelle funzioni di Node.js, accedere utilizzando dati di hello coda `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="b93ec-117">In Node.js functions, access hello queue data using `context.bindings.<name>`.</span></span>


<span data-ttu-id="b93ec-118">Nelle funzioni .NET, accedere payload coda hello utilizzando un parametro di metodo, ad esempio `CloudQueueMessage paramName`.</span><span class="sxs-lookup"><span data-stu-id="b93ec-118">In .NET functions, access hello queue payload using a method parameter such as `CloudQueueMessage paramName`.</span></span> <span data-ttu-id="b93ec-119">In questo caso, `paramName` hello valore specificato in hello [configurazione trigger](#trigger).</span><span class="sxs-lookup"><span data-stu-id="b93ec-119">Here, `paramName` is hello value you specified in hello [trigger configuration](#trigger).</span></span> <span data-ttu-id="b93ec-120">messaggio della coda può essere deserializzato tooany di hello seguenti tipi:</span><span class="sxs-lookup"><span data-stu-id="b93ec-120">hello queue message can be deserialized tooany of hello following types:</span></span>

* <span data-ttu-id="b93ec-121">Oggetto POCO.</span><span class="sxs-lookup"><span data-stu-id="b93ec-121">POCO object.</span></span> <span data-ttu-id="b93ec-122">Utilizzare se il payload di coda hello è un oggetto JSON.</span><span class="sxs-lookup"><span data-stu-id="b93ec-122">Use if hello queue payload is a JSON object.</span></span> <span data-ttu-id="b93ec-123">il runtime di funzioni Hello deserializza payload hello in oggetto POCO hello.</span><span class="sxs-lookup"><span data-stu-id="b93ec-123">hello Functions runtime deserializes hello payload into hello POCO object.</span></span> 
* `string`
* `byte[]`
* [`CloudQueueMessage`]

<a name="meta"></a>

### <a name="queue-trigger-metadata"></a><span data-ttu-id="b93ec-124">Metadati del trigger della coda</span><span class="sxs-lookup"><span data-stu-id="b93ec-124">Queue trigger metadata</span></span>
<span data-ttu-id="b93ec-125">trigger coda Hello fornisce diverse proprietà di metadati.</span><span class="sxs-lookup"><span data-stu-id="b93ec-125">hello queue trigger provides several metadata properties.</span></span> <span data-ttu-id="b93ec-126">Queste proprietà possono essere usate come parte delle espressioni di associazione in altre associazioni o come parametri nel codice.</span><span class="sxs-lookup"><span data-stu-id="b93ec-126">These properties can be used as part of binding expressions in other bindings or as parameters in your code.</span></span> <span data-ttu-id="b93ec-127">i valori Hello hanno hello stessa semantica [ `CloudQueueMessage` ].</span><span class="sxs-lookup"><span data-stu-id="b93ec-127">hello values have hello same semantics as [`CloudQueueMessage`].</span></span>

* <span data-ttu-id="b93ec-128">**QueueTrigger**: payload della coda, se si tratta di una stringa valida</span><span class="sxs-lookup"><span data-stu-id="b93ec-128">**QueueTrigger** - queue payload (if a valid string)</span></span>
* <span data-ttu-id="b93ec-129">**DequeueCount**: digitare `int`.</span><span class="sxs-lookup"><span data-stu-id="b93ec-129">**DequeueCount** - Type `int`.</span></span> <span data-ttu-id="b93ec-130">Hello numero di volte in cui che il messaggio è stato rimosso dalla coda.</span><span class="sxs-lookup"><span data-stu-id="b93ec-130">hello number of times this message has been dequeued.</span></span>
* <span data-ttu-id="b93ec-131">**ExpirationTime**: digitare `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="b93ec-131">**ExpirationTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="b93ec-132">tempo di Hello la scadenza di tale messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="b93ec-132">hello time that hello message expires.</span></span>
* <span data-ttu-id="b93ec-133">**Id**: digitare `string`.</span><span class="sxs-lookup"><span data-stu-id="b93ec-133">**Id** - Type `string`.</span></span> <span data-ttu-id="b93ec-134">ID del messaggio in coda.</span><span class="sxs-lookup"><span data-stu-id="b93ec-134">Queue message ID.</span></span>
* <span data-ttu-id="b93ec-135">**InsertionTime**: digitare `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="b93ec-135">**InsertionTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="b93ec-136">tempo di Hello toohello coda è stato aggiunto il messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="b93ec-136">hello time that hello message was added toohello queue.</span></span>
* <span data-ttu-id="b93ec-137">**NextVisibleTime** - Tipo `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="b93ec-137">**NextVisibleTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="b93ec-138">tempo di Hello tale messaggio sarà successivamente visibile.</span><span class="sxs-lookup"><span data-stu-id="b93ec-138">hello time that hello message will next be visible.</span></span>
* <span data-ttu-id="b93ec-139">**PopReceipt**: digitare `string`.</span><span class="sxs-lookup"><span data-stu-id="b93ec-139">**PopReceipt** - Type `string`.</span></span> <span data-ttu-id="b93ec-140">ricezione del messaggio Hello.</span><span class="sxs-lookup"><span data-stu-id="b93ec-140">hello message's pop receipt.</span></span>

<span data-ttu-id="b93ec-141">Vedere come toouse hello i metadati della coda in [esempio Trigger](#triggersample).</span><span class="sxs-lookup"><span data-stu-id="b93ec-141">See how toouse hello queue metadata in [Trigger sample](#triggersample).</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="b93ec-142">Esempio di trigger</span><span class="sxs-lookup"><span data-stu-id="b93ec-142">Trigger sample</span></span>
<span data-ttu-id="b93ec-143">Si supponga di avere seguito function.json hello che definisce un trigger di coda:</span><span class="sxs-lookup"><span data-stu-id="b93ec-143">Suppose you have hello following function.json that defines a queue trigger:</span></span>

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

<span data-ttu-id="b93ec-144">Vedere l'esempio specifico del linguaggio di hello che recupera e registra i metadati della coda.</span><span class="sxs-lookup"><span data-stu-id="b93ec-144">See hello language-specific sample that retrieves and logs queue metadata.</span></span>

* [<span data-ttu-id="b93ec-145">C#</span><span class="sxs-lookup"><span data-stu-id="b93ec-145">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="b93ec-146">Node.js</span><span class="sxs-lookup"><span data-stu-id="b93ec-146">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="b93ec-147">Esempio di trigger in C#</span><span class="sxs-lookup"><span data-stu-id="b93ec-147">Trigger sample in C#</span></span> #
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

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="b93ec-148">Esempio di trigger in Node.js</span><span class="sxs-lookup"><span data-stu-id="b93ec-148">Trigger sample in Node.js</span></span>

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

### <a name="handling-poison-queue-messages"></a><span data-ttu-id="b93ec-149">Gestione di messaggi della coda non elaborabili</span><span class="sxs-lookup"><span data-stu-id="b93ec-149">Handling poison queue messages</span></span>
<span data-ttu-id="b93ec-150">Quando una funzione di attivazione coda ha esito negativo, le funzioni di Azure Ritenta la funzione di toofive volte per un messaggio nella coda specificata, inclusi hello innanzitutto provare.</span><span class="sxs-lookup"><span data-stu-id="b93ec-150">When a queue trigger function fails, Azure Functions retries that function up toofive times for a given queue message, including hello first try.</span></span> <span data-ttu-id="b93ec-151">Se tutti e cinque i tentativi hanno esito negativo, il runtime di funzioni hello aggiunge una tooa coda di archiviazione denominata  *&lt;originalqueuename >-non elaborabile*.</span><span class="sxs-lookup"><span data-stu-id="b93ec-151">If all five attempts fail, hello functions runtime adds a message tooa queue storage named *&lt;originalqueuename>-poison*.</span></span> <span data-ttu-id="b93ec-152">È possibile scrivere messaggi tooprocess un funzione dalla coda non elaborabile hello registrarle o inviando una notifica che è necessario un intervento manuale.</span><span class="sxs-lookup"><span data-stu-id="b93ec-152">You can write a function tooprocess messages from hello poison queue by logging them or sending a  notification that manual attention is needed.</span></span> 

<span data-ttu-id="b93ec-153">i messaggi non elaborabili toohandle controllare manualmente, hello `dequeueCount` di messaggio della coda hello (vedere [i metadati della coda trigger](#meta)).</span><span class="sxs-lookup"><span data-stu-id="b93ec-153">toohandle poison messages manually, check hello `dequeueCount` of hello queue message (see [Queue trigger metadata](#meta)).</span></span>

<a name="output"></a>

## <a name="queue-storage-output-binding"></a><span data-ttu-id="b93ec-154">Associazione di output dell'archiviazione code</span><span class="sxs-lookup"><span data-stu-id="b93ec-154">Queue storage output binding</span></span>
<span data-ttu-id="b93ec-155">Hello l'archiviazione delle code di Azure output associazione consente toowrite messaggi tooa coda.</span><span class="sxs-lookup"><span data-stu-id="b93ec-155">hello Azure queue storage output binding enables you toowrite messages tooa queue.</span></span> 

<span data-ttu-id="b93ec-156">Definire una coda di associazione di output utilizzando hello **integrazione** scheda nel portale le funzioni hello.</span><span class="sxs-lookup"><span data-stu-id="b93ec-156">Define a queue output binding using hello **Integrate** tab in hello Functions portal.</span></span> <span data-ttu-id="b93ec-157">portale Hello crea hello seguente definizione di hello **associazioni** sezione *function.json*:</span><span class="sxs-lookup"><span data-stu-id="b93ec-157">hello portal creates hello following definition in hello  **bindings** section of *function.json*:</span></span>

```json
{
   "type": "queue",
   "direction": "out",
   "name": "<hello name used tooidentify hello trigger data in your code>",
   "queueName": "<Name of queue toowrite to>",
   "connection":"<Name of app setting - see below>"
}
```

* <span data-ttu-id="b93ec-158">Hello `connection` proprietà deve contenere il nome di hello di un'impostazione di app che contiene una stringa di connessione di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b93ec-158">hello `connection` property must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="b93ec-159">Nel portale di Azure hello, hello editor standard di hello **integrazione** scheda configura questa impostazione di app per l'utente quando si seleziona un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b93ec-159">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

<a name="outputusage"></a>

## <a name="using-a-queue-output-binding"></a><span data-ttu-id="b93ec-160">Uso dell'associazione di output della coda</span><span class="sxs-lookup"><span data-stu-id="b93ec-160">Using a queue output binding</span></span>
<span data-ttu-id="b93ec-161">Nelle funzioni di Node.js, accedere coda di output di hello utilizzando `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="b93ec-161">In Node.js functions, you access hello output queue using `context.bindings.<name>`.</span></span>

<span data-ttu-id="b93ec-162">Nelle funzioni .NET, è possibile creare tooany dei seguenti tipi di hello.</span><span class="sxs-lookup"><span data-stu-id="b93ec-162">In .NET functions, you can output tooany of hello following types.</span></span> <span data-ttu-id="b93ec-163">Quando è un parametro di tipo `T`, `T` deve essere uno dei tipi di output di hello è supportato, ad esempio `string` o un POCO.</span><span class="sxs-lookup"><span data-stu-id="b93ec-163">When there is a type parameter `T`, `T` must be one of hello supported output types, such as `string` or a POCO.</span></span>

* <span data-ttu-id="b93ec-164">`out T`, serializzato come JSON</span><span class="sxs-lookup"><span data-stu-id="b93ec-164">`out T` (serialized as JSON)</span></span>
* `out string`
* `out byte[]`
* <span data-ttu-id="b93ec-165">`out` [`CloudQueueMessage`]</span><span class="sxs-lookup"><span data-stu-id="b93ec-165">`out` [`CloudQueueMessage`]</span></span> 
* `ICollector<T>`
* `IAsyncCollector<T>`
* [`CloudQueue`](/dotnet/api/microsoft.windowsazure.storage.queue.cloudqueue)

<span data-ttu-id="b93ec-166">È inoltre possibile utilizzare il tipo restituito del metodo di hello come hello associazione di output.</span><span class="sxs-lookup"><span data-stu-id="b93ec-166">You can also use hello method return type as hello output binding.</span></span>

<a name="outputsample"></a>

## <a name="queue-output-sample"></a><span data-ttu-id="b93ec-167">Esempio di output in coda</span><span class="sxs-lookup"><span data-stu-id="b93ec-167">Queue output sample</span></span>
<span data-ttu-id="b93ec-168">esempio Hello *function.json* definisce un trigger HTTP e una coda di associazione di output:</span><span class="sxs-lookup"><span data-stu-id="b93ec-168">hello following *function.json* defines an HTTP trigger with a queue output binding:</span></span>

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

<span data-ttu-id="b93ec-169">Vedere l'esempio specifico del linguaggio hello che restituisce un messaggio nella coda con payload HTTP in ingresso hello.</span><span class="sxs-lookup"><span data-stu-id="b93ec-169">See hello language-specific sample that outputs a queue message with hello incoming HTTP payload.</span></span>

* [<span data-ttu-id="b93ec-170">C#</span><span class="sxs-lookup"><span data-stu-id="b93ec-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="b93ec-171">Node.js</span><span class="sxs-lookup"><span data-stu-id="b93ec-171">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="queue-output-sample-in-c"></a><span data-ttu-id="b93ec-172">Esempio di output della coda in C#</span><span class="sxs-lookup"><span data-stu-id="b93ec-172">Queue output sample in C#</span></span> #

```cs
// C# example of HTTP trigger binding tooa custom POCO, with a queue output binding
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

<span data-ttu-id="b93ec-173">toosend più messaggi, utilizzare un `ICollector`:</span><span class="sxs-lookup"><span data-stu-id="b93ec-173">toosend multiple messages, use an `ICollector`:</span></span>

```cs
public static void Run(CustomQueueMessage input, ICollector<CustomQueueMessage> myQueueItem, TraceWriter log)
{
    myQueueItem.Add(input);
    myQueueItem.Add(new CustomQueueMessage { PersonName = "You", Title = "None" });
}
```

<a name="outnodejs"></a>

### <a name="queue-output-sample-in-nodejs"></a><span data-ttu-id="b93ec-174">Esempio di output della coda in Node.js</span><span class="sxs-lookup"><span data-stu-id="b93ec-174">Queue output sample in Node.js</span></span>

```javascript
module.exports = function (context, input) {
    context.done(null, input.body);
};
```

<span data-ttu-id="b93ec-175">In alternativa, toosend più messaggi,</span><span class="sxs-lookup"><span data-stu-id="b93ec-175">Or, toosend multiple messages,</span></span>

```javascript
module.exports = function(context) {
    // Define a message array for hello myQueueItem output binding. 
    context.bindings.myQueueItem = ["message 1","message 2"];
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="b93ec-176">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b93ec-176">Next steps</span></span>

<span data-ttu-id="b93ec-177">Per un esempio di una funzione che utilizza i trigger di archiviazione della coda e le associazioni, vedere [un tooan funzione Azure connesso il servizio di Azure creare](functions-create-an-azure-connected-function.md).</span><span class="sxs-lookup"><span data-stu-id="b93ec-177">For an example of a function that uses queue storage triggers and bindings, see [Create an Azure Function connected tooan Azure service](functions-create-an-azure-connected-function.md).</span></span>

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

<!-- LINKS -->

["CloudQueueMessage"]: /dotnet/api/microsoft.windowsazure.storage.queue.cloudqueuemessage
