---
title: Trigger timer in Funzioni di Azure | Documentazione Microsoft
description: Informazioni su come usare trigger timer in Funzioni di Azure.
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: Funzioni di Azure, Funzioni, elaborazione eventi, calcolo dinamico, architettura senza server
ms.assetid: d2f013d1-f458-42ae-baf8-1810138118ac
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/27/2017
ms.author: glenga
ms.custom: 
ms.openlocfilehash: 6a97ab8508f889b77d064a5da70e3c726d62900c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-timer-trigger"></a><span data-ttu-id="e5dff-104">Trigger timer in Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="e5dff-104">Azure Functions timer trigger</span></span>

[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="e5dff-105">Questo articolo illustra come configurare trigger timer in Funzioni di Azure e su come scrivere il relativo codice.</span><span class="sxs-lookup"><span data-stu-id="e5dff-105">This article explains how to configure and code timer triggers in Azure Functions.</span></span> <span data-ttu-id="e5dff-106">Funzioni di Azure è dotata di un binding trigger timer che consente di eseguire il codice della funzione secondo una pianificazione definita.</span><span class="sxs-lookup"><span data-stu-id="e5dff-106">Azure Functions has a timer trigger binding that lets you run your function code based on a defined schedule.</span></span> 

<span data-ttu-id="e5dff-107">Il trigger timer supporta la scalabilità orizzontale a più istanze. Una singola istanza di una particolare funzione timer viene eseguita su tutte le istanze.</span><span class="sxs-lookup"><span data-stu-id="e5dff-107">The timer trigger supports multi-instance scale-out. A single instance of a particular timer function is run across all instances.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a id="trigger"></a>

## <a name="timer-trigger"></a><span data-ttu-id="e5dff-108">Trigger timer</span><span class="sxs-lookup"><span data-stu-id="e5dff-108">Timer trigger</span></span>
<span data-ttu-id="e5dff-109">Il trigger timer per una funzione usa l'oggetto JSON seguente nella matrice `bindings` di function.json:</span><span class="sxs-lookup"><span data-stu-id="e5dff-109">The timer trigger to a function uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "schedule": "<CRON expression - see below>",
    "name": "<Name of trigger parameter in function signature>",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="e5dff-110">Il valore di `schedule` è un'[espressione CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) che include i 6 campi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e5dff-110">The value of `schedule` is a [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that includes these six fields:</span></span> 

    {second} {minute} {hour} {day} {month} {day-of-week}
&nbsp;
>[!NOTE]   
><span data-ttu-id="e5dff-111">In molte delle espressioni CRON disponibili online il campo `{second}` viene omesso.</span><span class="sxs-lookup"><span data-stu-id="e5dff-111">Many of the cron expressions you find online omit the `{second}` field.</span></span> <span data-ttu-id="e5dff-112">Se si copia da una di esse, è necessario apportare una modifica per il campo `{second}` aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="e5dff-112">If you copy from one of them, you need to adjust for the extra `{second}` field.</span></span> <span data-ttu-id="e5dff-113">Per esempi specifici, vedere [Esempi di pianificazione](#examples) di seguito.</span><span class="sxs-lookup"><span data-stu-id="e5dff-113">For specific examples, see [Schedule examples](#examples) below.</span></span>

<span data-ttu-id="e5dff-114">Il fuso orario predefinito usato con le espressioni CRON è Coordinated Universal Time (UTC).</span><span class="sxs-lookup"><span data-stu-id="e5dff-114">The default time zone used with the CRON expressions is Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="e5dff-115">Per fare in modo che l'espressione CRON sia basata su un altro fuso orario, creare una nuova impostazione di app per l'app per le funzioni denominata `WEBSITE_TIME_ZONE`.</span><span class="sxs-lookup"><span data-stu-id="e5dff-115">To have your CRON expression based on another time zone, create a new app setting for your function app named `WEBSITE_TIME_ZONE`.</span></span> <span data-ttu-id="e5dff-116">Impostare il valore sul nome del fuso orario prescelto come illustrato nell'[indice dei fusi orari di Microsoft](https://msdn.microsoft.com/library/ms912391.aspx).</span><span class="sxs-lookup"><span data-stu-id="e5dff-116">Set the value to the name of the desired time zone as shown in the [Microsoft Time Zone Index](https://msdn.microsoft.com/library/ms912391.aspx).</span></span> 

<span data-ttu-id="e5dff-117">Ad esempio, *Ora solare fuso orientale* (EST) è UTC-05:00.</span><span class="sxs-lookup"><span data-stu-id="e5dff-117">For example, *Eastern Standard Time* is UTC-05:00.</span></span> <span data-ttu-id="e5dff-118">Per attivare il timer trigger ogni giorno alle 10:00 EST, usare la seguente espressione CRON che rappresenta il fuso orario UTC:</span><span class="sxs-lookup"><span data-stu-id="e5dff-118">To have your timer trigger fire at 10:00 AM EST every day, use the following CRON expression that accounts for UTC time zone:</span></span>

```json
"schedule": "0 0 15 * * *",
``` 

<span data-ttu-id="e5dff-119">In alternativa, è possibile aggiungere una nuova impostazione di app per l'app per le funzioni denominata `WEBSITE_TIME_ZONE` e impostare il valore su **Ora solare fuso orientale**.</span><span class="sxs-lookup"><span data-stu-id="e5dff-119">Alternatively, you could add a new app setting for your function app named `WEBSITE_TIME_ZONE` and set the value to **Eastern Standard Time**.</span></span>  <span data-ttu-id="e5dff-120">La seguente espressione CRON può quindi essere usata per 10:00 EST:</span><span class="sxs-lookup"><span data-stu-id="e5dff-120">Then the following CRON expression could be used for 10:00 AM EST:</span></span> 

```json
"schedule": "0 0 10 * * *",
``` 


<a name="examples"></a>

## <a name="schedule-examples"></a><span data-ttu-id="e5dff-121">Esempi di pianificazione</span><span class="sxs-lookup"><span data-stu-id="e5dff-121">Schedule examples</span></span>
<span data-ttu-id="e5dff-122">Di seguito sono riportati alcuni esempi di espressioni CRON che possibile usare per la proprietà `schedule`.</span><span class="sxs-lookup"><span data-stu-id="e5dff-122">Here are some samples of CRON expressions you can use for the `schedule` property.</span></span> 

<span data-ttu-id="e5dff-123">Per attivare una volta ogni 5 minuti:</span><span class="sxs-lookup"><span data-stu-id="e5dff-123">To trigger once every five minutes:</span></span>

```json
"schedule": "0 */5 * * * *"
```

<span data-ttu-id="e5dff-124">Per attivare una volta all'inizio di ogni ora:</span><span class="sxs-lookup"><span data-stu-id="e5dff-124">To trigger once at the top of every hour:</span></span>

```json
"schedule": "0 0 * * * *",
```

<span data-ttu-id="e5dff-125">Per attivare una volta ogni 2 ore:</span><span class="sxs-lookup"><span data-stu-id="e5dff-125">To trigger once every two hours:</span></span>

```json
"schedule": "0 0 */2 * * *",
```

<span data-ttu-id="e5dff-126">Per attivare una volta ogni ora dalle 9 alle 17:</span><span class="sxs-lookup"><span data-stu-id="e5dff-126">To trigger once every hour from 9 AM to 5 PM:</span></span>

```json
"schedule": "0 0 9-17 * * *",
```

<span data-ttu-id="e5dff-127">Per attivare alle 9:30 ogni giorno:</span><span class="sxs-lookup"><span data-stu-id="e5dff-127">To trigger At 9:30 AM every day:</span></span>

```json
"schedule": "0 30 9 * * *",
```

<span data-ttu-id="e5dff-128">Per attivare alle 9:30 ogni giorno feriale:</span><span class="sxs-lookup"><span data-stu-id="e5dff-128">To trigger At 9:30 AM every weekday:</span></span>

```json
"schedule": "0 30 9 * * 1-5",
```

<a name="usage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="e5dff-129">Utilizzo dei trigger</span><span class="sxs-lookup"><span data-stu-id="e5dff-129">Trigger usage</span></span>
<span data-ttu-id="e5dff-130">Quando viene richiamata una funzione di trigger timer, l'[oggetto timer](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) viene passato alla funzione.</span><span class="sxs-lookup"><span data-stu-id="e5dff-130">When a timer trigger function is invoked, the [timer object](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) is passed into the function.</span></span> <span data-ttu-id="e5dff-131">Il codice JSON seguente è una rappresentazione di esempio dell'oggetto timer.</span><span class="sxs-lookup"><span data-stu-id="e5dff-131">The following JSON is an example representation of the timer object.</span></span> 

```json
{
    "Schedule":{
    },
    "ScheduleStatus": {
        "Last":"2016-10-04T10:15:00.012699+00:00",
        "Next":"2016-10-04T10:20:00+00:00"
    },
    "IsPastDue":false
}
```

<a name="sample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="e5dff-132">Esempio di trigger</span><span class="sxs-lookup"><span data-stu-id="e5dff-132">Trigger sample</span></span>
<span data-ttu-id="e5dff-133">Si supponga che il trigger timer seguente sia presente nella matrice `bindings` di function.json:</span><span class="sxs-lookup"><span data-stu-id="e5dff-133">Suppose you have the following timer trigger in the `bindings` array of function.json:</span></span>

```json
{
    "schedule": "0 */5 * * * *",
    "name": "myTimer",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="e5dff-134">Vedere l'esempio specifico del linguaggio che legge l'oggetto timer per verificare se viene eseguito in ritardo.</span><span class="sxs-lookup"><span data-stu-id="e5dff-134">See the language-specific sample that reads the timer object to see whether it's running late.</span></span>

* [<span data-ttu-id="e5dff-135">C#</span><span class="sxs-lookup"><span data-stu-id="e5dff-135">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="e5dff-136">F#</span><span class="sxs-lookup"><span data-stu-id="e5dff-136">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="e5dff-137">Node.JS</span><span class="sxs-lookup"><span data-stu-id="e5dff-137">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="e5dff-138">Esempio di trigger in C#</span><span class="sxs-lookup"><span data-stu-id="e5dff-138">Trigger sample in C#</span></span> #
```csharp
public static void Run(TimerInfo myTimer, TraceWriter log)
{
    if(myTimer.IsPastDue)
    {
        log.Info("Timer is running late!");
    }
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}" );  
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a><span data-ttu-id="e5dff-139">Esempio di trigger in F#</span><span class="sxs-lookup"><span data-stu-id="e5dff-139">Trigger sample in F#</span></span> #
```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter ) =
    if (myTimer.IsPastDue) then
        log.Info("F# function is running late.")
    let now = DateTime.Now.ToLongTimeString()
    log.Info(sprintf "F# function executed at %s!" now)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="e5dff-140">Esempio di trigger in Node.js</span><span class="sxs-lookup"><span data-stu-id="e5dff-140">Trigger sample in Node.js</span></span>
```JavaScript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    if(myTimer.isPastDue)
    {
        context.log('Node.js is running late!');
    }
    context.log('Node.js timer trigger function ran!', timeStamp);   

    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="e5dff-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e5dff-141">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

