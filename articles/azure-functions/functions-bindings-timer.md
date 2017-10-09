---
title: trigger di timer funzioni aaaAzure | Documenti Microsoft
description: Comprendere come toouse timer attivi nelle funzioni di Azure.
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
ms.openlocfilehash: 17fca22372dbc55d4684c8c099cc97923a7d3cf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-timer-trigger"></a><span data-ttu-id="b4b2a-104">Trigger timer in Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="b4b2a-104">Azure Functions timer trigger</span></span>

[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="b4b2a-105">Questo articolo spiega come tooconfigure e il codice di timer attivi nelle funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="b4b2a-105">This article explains how tooconfigure and code timer triggers in Azure Functions.</span></span> <span data-ttu-id="b4b2a-106">Funzioni di Azure è dotata di un binding trigger timer che consente di eseguire il codice della funzione secondo una pianificazione definita.</span><span class="sxs-lookup"><span data-stu-id="b4b2a-106">Azure Functions has a timer trigger binding that lets you run your function code based on a defined schedule.</span></span> 

<span data-ttu-id="b4b2a-107">Hello timer trigger supporta la scalabilità orizzontale a più istanze. Una singola istanza di una particolare funzione timer viene eseguita su tutte le istanze.</span><span class="sxs-lookup"><span data-stu-id="b4b2a-107">hello timer trigger supports multi-instance scale-out. A single instance of a particular timer function is run across all instances.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a id="trigger"></a>

## <a name="timer-trigger"></a><span data-ttu-id="b4b2a-108">Trigger timer</span><span class="sxs-lookup"><span data-stu-id="b4b2a-108">Timer trigger</span></span>
<span data-ttu-id="b4b2a-109">timer trigger tooa funzione Hello utilizza hello seguente oggetto JSON nella hello `bindings` matrice function.json:</span><span class="sxs-lookup"><span data-stu-id="b4b2a-109">hello timer trigger tooa function uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "schedule": "<CRON expression - see below>",
    "name": "<Name of trigger parameter in function signature>",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="b4b2a-110">valore di Hello `schedule` è un [espressione CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) che include questi sei campi:</span><span class="sxs-lookup"><span data-stu-id="b4b2a-110">hello value of `schedule` is a [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that includes these six fields:</span></span> 

    {second} {minute} {hour} {day} {month} {day-of-week}
&nbsp;
>[!NOTE]   
><span data-ttu-id="b4b2a-111">Molti di espressioni cron hello disponibili online omettere hello `{second}` campo.</span><span class="sxs-lookup"><span data-stu-id="b4b2a-111">Many of hello cron expressions you find online omit hello `{second}` field.</span></span> <span data-ttu-id="b4b2a-112">Se si copia da una di esse, è necessario tooadjust per hello aggiuntivo `{second}` campo.</span><span class="sxs-lookup"><span data-stu-id="b4b2a-112">If you copy from one of them, you need tooadjust for hello extra `{second}` field.</span></span> <span data-ttu-id="b4b2a-113">Per esempi specifici, vedere [Esempi di pianificazione](#examples) di seguito.</span><span class="sxs-lookup"><span data-stu-id="b4b2a-113">For specific examples, see [Schedule examples](#examples) below.</span></span>

<span data-ttu-id="b4b2a-114">fuso orario predefinito di Hello utilizzato con le espressioni CRON hello è Coordinated Universal Time (UTC).</span><span class="sxs-lookup"><span data-stu-id="b4b2a-114">hello default time zone used with hello CRON expressions is Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="b4b2a-115">toohave l'espressione CRON basata su un altro fuso orario, creare una nuova impostazione di app per l'app di funzione denominata `WEBSITE_TIME_ZONE`.</span><span class="sxs-lookup"><span data-stu-id="b4b2a-115">toohave your CRON expression based on another time zone, create a new app setting for your function app named `WEBSITE_TIME_ZONE`.</span></span> <span data-ttu-id="b4b2a-116">Nome valore toohello hello del set di hello desiderato fuso orario, come illustrato nell'hello [indice fuso orario Microsoft](https://msdn.microsoft.com/library/ms912391.aspx).</span><span class="sxs-lookup"><span data-stu-id="b4b2a-116">Set hello value toohello name of hello desired time zone as shown in hello [Microsoft Time Zone Index](https://msdn.microsoft.com/library/ms912391.aspx).</span></span> 

<span data-ttu-id="b4b2a-117">Ad esempio, *Ora solare fuso orientale* (EST) è UTC-05:00.</span><span class="sxs-lookup"><span data-stu-id="b4b2a-117">For example, *Eastern Standard Time* is UTC-05:00.</span></span> <span data-ttu-id="b4b2a-118">toohave il timer di trigger attivati in 10:00 AM EST ogni giorno, utilizzare hello espressione CRON che tengono conto del fuso orario UTC seguente:</span><span class="sxs-lookup"><span data-stu-id="b4b2a-118">toohave your timer trigger fire at 10:00 AM EST every day, use hello following CRON expression that accounts for UTC time zone:</span></span>

```json
"schedule": "0 0 15 * * *",
``` 

<span data-ttu-id="b4b2a-119">In alternativa, è possibile aggiungere una nuova impostazione di app per app di funzione denominata `WEBSITE_TIME_ZONE` e impostare il valore di hello troppo**ora solare fuso orientale**.</span><span class="sxs-lookup"><span data-stu-id="b4b2a-119">Alternatively, you could add a new app setting for your function app named `WEBSITE_TIME_ZONE` and set hello value too**Eastern Standard Time**.</span></span>  <span data-ttu-id="b4b2a-120">Hello CRON espressione seguente può essere quindi utilizzato per 10:00 AM EST:</span><span class="sxs-lookup"><span data-stu-id="b4b2a-120">Then hello following CRON expression could be used for 10:00 AM EST:</span></span> 

```json
"schedule": "0 0 10 * * *",
``` 


<a name="examples"></a>

## <a name="schedule-examples"></a><span data-ttu-id="b4b2a-121">Esempi di pianificazione</span><span class="sxs-lookup"><span data-stu-id="b4b2a-121">Schedule examples</span></span>
<span data-ttu-id="b4b2a-122">Ecco alcuni esempi di espressioni CRON è possibile utilizzare per hello `schedule` proprietà.</span><span class="sxs-lookup"><span data-stu-id="b4b2a-122">Here are some samples of CRON expressions you can use for hello `schedule` property.</span></span> 

<span data-ttu-id="b4b2a-123">una volta ogni cinque minuti tootrigger:</span><span class="sxs-lookup"><span data-stu-id="b4b2a-123">tootrigger once every five minutes:</span></span>

```json
"schedule": "0 */5 * * * *"
```

<span data-ttu-id="b4b2a-124">tootrigger una volta in ogni ora di inizio hello:</span><span class="sxs-lookup"><span data-stu-id="b4b2a-124">tootrigger once at hello top of every hour:</span></span>

```json
"schedule": "0 0 * * * *",
```

<span data-ttu-id="b4b2a-125">una volta ogni due ore tootrigger:</span><span class="sxs-lookup"><span data-stu-id="b4b2a-125">tootrigger once every two hours:</span></span>

```json
"schedule": "0 0 */2 * * *",
```

<span data-ttu-id="b4b2a-126">tootrigger una volta ogni ora da too5 09: 00 PM:</span><span class="sxs-lookup"><span data-stu-id="b4b2a-126">tootrigger once every hour from 9 AM too5 PM:</span></span>

```json
"schedule": "0 0 9-17 * * *",
```

<span data-ttu-id="b4b2a-127">tootrigger in ogni giorno alle 9.30:</span><span class="sxs-lookup"><span data-stu-id="b4b2a-127">tootrigger At 9:30 AM every day:</span></span>

```json
"schedule": "0 30 9 * * *",
```

<span data-ttu-id="b4b2a-128">tootrigger alle 9:30 AM ogni giorno della settimana:</span><span class="sxs-lookup"><span data-stu-id="b4b2a-128">tootrigger At 9:30 AM every weekday:</span></span>

```json
"schedule": "0 30 9 * * 1-5",
```

<a name="usage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="b4b2a-129">Uso dei trigger</span><span class="sxs-lookup"><span data-stu-id="b4b2a-129">Trigger usage</span></span>
<span data-ttu-id="b4b2a-130">Quando viene richiamata una funzione di trigger timer, hello [oggetto timer](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) viene passata alla funzione hello.</span><span class="sxs-lookup"><span data-stu-id="b4b2a-130">When a timer trigger function is invoked, hello [timer object](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) is passed into hello function.</span></span> <span data-ttu-id="b4b2a-131">Hello JSON seguente è una rappresentazione di esempio dell'oggetto timer hello.</span><span class="sxs-lookup"><span data-stu-id="b4b2a-131">hello following JSON is an example representation of hello timer object.</span></span> 

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

## <a name="trigger-sample"></a><span data-ttu-id="b4b2a-132">Esempio di trigger</span><span class="sxs-lookup"><span data-stu-id="b4b2a-132">Trigger sample</span></span>
<span data-ttu-id="b4b2a-133">Si supponga di avere seguito trigger timer in hello hello `bindings` matrice function.json:</span><span class="sxs-lookup"><span data-stu-id="b4b2a-133">Suppose you have hello following timer trigger in hello `bindings` array of function.json:</span></span>

```json
{
    "schedule": "0 */5 * * * *",
    "name": "myTimer",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="b4b2a-134">Vedere l'esempio specifico del linguaggio hello che legge timer hello toosee oggetto se è in esecuzione in ritardo.</span><span class="sxs-lookup"><span data-stu-id="b4b2a-134">See hello language-specific sample that reads hello timer object toosee whether it's running late.</span></span>

* [<span data-ttu-id="b4b2a-135">C#</span><span class="sxs-lookup"><span data-stu-id="b4b2a-135">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="b4b2a-136">F#</span><span class="sxs-lookup"><span data-stu-id="b4b2a-136">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="b4b2a-137">Node.JS</span><span class="sxs-lookup"><span data-stu-id="b4b2a-137">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="b4b2a-138">Esempio di trigger in C#</span><span class="sxs-lookup"><span data-stu-id="b4b2a-138">Trigger sample in C#</span></span> #
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

### <a name="trigger-sample-in-f"></a><span data-ttu-id="b4b2a-139">Esempio di trigger in F#</span><span class="sxs-lookup"><span data-stu-id="b4b2a-139">Trigger sample in F#</span></span> #
```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter ) =
    if (myTimer.IsPastDue) then
        log.Info("F# function is running late.")
    let now = DateTime.Now.ToLongTimeString()
    log.Info(sprintf "F# function executed at %s!" now)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="b4b2a-140">Esempio di trigger in Node.js</span><span class="sxs-lookup"><span data-stu-id="b4b2a-140">Trigger sample in Node.js</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="b4b2a-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b4b2a-141">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

