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
# <a name="azure-functions-timer-trigger"></a>Trigger timer in Funzioni di Azure

[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Questo articolo spiega come tooconfigure e il codice di timer attivi nelle funzioni di Azure. Funzioni di Azure è dotata di un binding trigger timer che consente di eseguire il codice della funzione secondo una pianificazione definita. 

Hello timer trigger supporta la scalabilità orizzontale a più istanze. Una singola istanza di una particolare funzione timer viene eseguita su tutte le istanze.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a id="trigger"></a>

## <a name="timer-trigger"></a>Trigger timer
timer trigger tooa funzione Hello utilizza hello seguente oggetto JSON nella hello `bindings` matrice function.json:

```json
{
    "schedule": "<CRON expression - see below>",
    "name": "<Name of trigger parameter in function signature>",
    "type": "timerTrigger",
    "direction": "in"
}
```

valore di Hello `schedule` è un [espressione CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) che include questi sei campi: 

    {second} {minute} {hour} {day} {month} {day-of-week}
&nbsp;
>[!NOTE]   
>Molti di espressioni cron hello disponibili online omettere hello `{second}` campo. Se si copia da una di esse, è necessario tooadjust per hello aggiuntivo `{second}` campo. Per esempi specifici, vedere [Esempi di pianificazione](#examples) di seguito.

fuso orario predefinito di Hello utilizzato con le espressioni CRON hello è Coordinated Universal Time (UTC). toohave l'espressione CRON basata su un altro fuso orario, creare una nuova impostazione di app per l'app di funzione denominata `WEBSITE_TIME_ZONE`. Nome valore toohello hello del set di hello desiderato fuso orario, come illustrato nell'hello [indice fuso orario Microsoft](https://msdn.microsoft.com/library/ms912391.aspx). 

Ad esempio, *Ora solare fuso orientale* (EST) è UTC-05:00. toohave il timer di trigger attivati in 10:00 AM EST ogni giorno, utilizzare hello espressione CRON che tengono conto del fuso orario UTC seguente:

```json
"schedule": "0 0 15 * * *",
``` 

In alternativa, è possibile aggiungere una nuova impostazione di app per app di funzione denominata `WEBSITE_TIME_ZONE` e impostare il valore di hello troppo**ora solare fuso orientale**.  Hello CRON espressione seguente può essere quindi utilizzato per 10:00 AM EST: 

```json
"schedule": "0 0 10 * * *",
``` 


<a name="examples"></a>

## <a name="schedule-examples"></a>Esempi di pianificazione
Ecco alcuni esempi di espressioni CRON è possibile utilizzare per hello `schedule` proprietà. 

una volta ogni cinque minuti tootrigger:

```json
"schedule": "0 */5 * * * *"
```

tootrigger una volta in ogni ora di inizio hello:

```json
"schedule": "0 0 * * * *",
```

una volta ogni due ore tootrigger:

```json
"schedule": "0 0 */2 * * *",
```

tootrigger una volta ogni ora da too5 09: 00 PM:

```json
"schedule": "0 0 9-17 * * *",
```

tootrigger in ogni giorno alle 9.30:

```json
"schedule": "0 30 9 * * *",
```

tootrigger alle 9:30 AM ogni giorno della settimana:

```json
"schedule": "0 30 9 * * 1-5",
```

<a name="usage"></a>

## <a name="trigger-usage"></a>Uso dei trigger
Quando viene richiamata una funzione di trigger timer, hello [oggetto timer](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) viene passata alla funzione hello. Hello JSON seguente è una rappresentazione di esempio dell'oggetto timer hello. 

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

## <a name="trigger-sample"></a>Esempio di trigger
Si supponga di avere seguito trigger timer in hello hello `bindings` matrice function.json:

```json
{
    "schedule": "0 */5 * * * *",
    "name": "myTimer",
    "type": "timerTrigger",
    "direction": "in"
}
```

Vedere l'esempio specifico del linguaggio hello che legge timer hello toosee oggetto se è in esecuzione in ritardo.

* [C#](#triggercsharp)
* [F#](#triggerfsharp)
* [Node.JS](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>Esempio di trigger in C# #
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

### <a name="trigger-sample-in-f"></a>Esempio di trigger in F# #
```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter ) =
    if (myTimer.IsPastDue) then
        log.Info("F# function is running late.")
    let now = DateTime.Now.ToLongTimeString()
    log.Info(sprintf "F# function executed at %s!" now)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a>Esempio di trigger in Node.js
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

## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

