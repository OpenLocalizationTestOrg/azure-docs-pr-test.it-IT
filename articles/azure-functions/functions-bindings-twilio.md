---
title: associazione di funzioni Twilio aaaAzure | Documenti Microsoft
description: Comprendere come le associazioni di Twilio toouse con funzioni di Azure.
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: Funzioni di Azure, Funzioni, elaborazione eventi, calcolo dinamico, architettura senza server
ms.assetid: a60263aa-3de9-4e1b-a2bb-0b52e70d559b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/20/2016
ms.author: wesmc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 882853947850e7d6795ca5b2f3fb6b9a83ede182
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="send-sms-messages-from-azure-functions-using-hello-twilio-output-binding"></a><span data-ttu-id="ae40e-104">Invio di messaggi SMS da funzioni di Azure utilizzando hello associazione di output Twilio</span><span class="sxs-lookup"><span data-stu-id="ae40e-104">Send SMS messages from Azure Functions using hello Twilio output binding</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="ae40e-105">Questo articolo viene illustrato come le associazioni di Twilio tooconfigure e l'utilizzo con le funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="ae40e-105">This article explains how tooconfigure and use Twilio bindings with Azure Functions.</span></span> 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="ae40e-106">Funzioni di Azure supporta Twilio output associazioni tooenable i messaggi di testo SMS toosend funzioni con poche righe di codice e un [Twilio](https://www.twilio.com/) account.</span><span class="sxs-lookup"><span data-stu-id="ae40e-106">Azure Functions supports Twilio output bindings tooenable your functions toosend SMS text messages with a few lines of code and a [Twilio](https://www.twilio.com/) account.</span></span> 

## <a name="functionjson-for-hello-twilio-output-binding"></a><span data-ttu-id="ae40e-107">Function.JSON per hello Twilio output associazione</span><span class="sxs-lookup"><span data-stu-id="ae40e-107">function.json for hello Twilio output binding</span></span>
<span data-ttu-id="ae40e-108">file function.json Hello fornisce hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="ae40e-108">hello function.json file provides hello following properties:</span></span>

* <span data-ttu-id="ae40e-109">`name`: Nome variabile utilizzato nel codice della funzione per hello messaggio Twilio SMS.</span><span class="sxs-lookup"><span data-stu-id="ae40e-109">`name` : Variable name used in function code for hello Twilio SMS text message.</span></span>
* <span data-ttu-id="ae40e-110">`type`: deve essere impostato troppo*"twilioSms"*.</span><span class="sxs-lookup"><span data-stu-id="ae40e-110">`type` : must be set too*"twilioSms"*.</span></span>
* <span data-ttu-id="ae40e-111">`accountSid`: Questo valore deve essere impostato toohello nome di un'impostazione di App che contiene il Sid di Account di Twilio.</span><span class="sxs-lookup"><span data-stu-id="ae40e-111">`accountSid` : This value must be set toohello name of an App Setting that holds your Twilio Account Sid.</span></span>
* <span data-ttu-id="ae40e-112">`authToken`: Questo valore deve essere impostato toohello nome di un'impostazione di App che contiene il token di autenticazione Twilio.</span><span class="sxs-lookup"><span data-stu-id="ae40e-112">`authToken` : This value must be set toohello name of an App Setting that holds your Twilio authentication token.</span></span>
* <span data-ttu-id="ae40e-113">`to`: Questo valore è impostato toohello numero di telefono inviato al testo SMS hello.</span><span class="sxs-lookup"><span data-stu-id="ae40e-113">`to` : This value is set toohello phone number that hello SMS text is sent to.</span></span>
* <span data-ttu-id="ae40e-114">`from`: Questo valore è impostato toohello numero di telefono inviato da testo SMS hello.</span><span class="sxs-lookup"><span data-stu-id="ae40e-114">`from` : This value is set toohello phone number that hello SMS text is sent from.</span></span>
* <span data-ttu-id="ae40e-115">`direction`: deve essere impostato troppo*"out"*.</span><span class="sxs-lookup"><span data-stu-id="ae40e-115">`direction` : must be set too*"out"*.</span></span>
* <span data-ttu-id="ae40e-116">`body`: Questo valore può essere utilizzato toohard codice hello messaggio SMS se non è necessario tooset in modo dinamico in hello del codice per la funzione.</span><span class="sxs-lookup"><span data-stu-id="ae40e-116">`body` : This value can be used toohard code hello SMS text message if you don't need tooset it dynamically in hello code for your function.</span></span> 

<span data-ttu-id="ae40e-117">Function.json di esempio:</span><span class="sxs-lookup"><span data-stu-id="ae40e-117">Example function.json:</span></span>

```json
{
  "type": "twilioSms",
  "name": "message",
  "accountSid": "TwilioAccountSid",
  "authToken": "TwilioAuthToken",
  "to": "+1704XXXXXXX",
  "from": "+1425XXXXXXX",
  "direction": "out",
  "body": "Azure Functions Testing"
}
```


## <a name="example-c-queue-trigger-with-twilio-output-binding"></a><span data-ttu-id="ae40e-118">Esempio di trigger della coda C# con l'associazione output di Twilio</span><span class="sxs-lookup"><span data-stu-id="ae40e-118">Example C# queue trigger with Twilio output binding</span></span>
#### <a name="synchronous"></a><span data-ttu-id="ae40e-119">Sincrono</span><span class="sxs-lookup"><span data-stu-id="ae40e-119">Synchronous</span></span>
<span data-ttu-id="ae40e-120">Questo codice di esempio sincrono per un trigger di coda di archiviazione di Azure Usa un fuori parametro toosend un cliente tooa messaggio di testo che ha effettuato un ordine.</span><span class="sxs-lookup"><span data-stu-id="ae40e-120">This synchronous example code for an Azure Storage queue trigger uses an out parameter toosend a text message tooa customer who placed an order.</span></span>

```cs
#r "Newtonsoft.Json"
#r "Twilio.Api"

using System;
using Newtonsoft.Json;
using Twilio;

public static void Run(string myQueueItem, out SMSMessage message,  TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a JSON string representing an order that contains hello name of a 
    // customer and a mobile number toosend text updates to.
    dynamic order = JsonConvert.DeserializeObject(myQueueItem);
    string msg = "Hello " + order.name + ", thank you for your order.";

    // Even if you want toouse a hard coded message and number in hello binding, you must at least 
    // initialize hello SMSMessage variable.
    message = new SMSMessage();

    // A dynamic message can be set instead of hello body in hello output binding. In this example, we use 
    // hello order information toopersonalize a text message toohello mobile number provided for
    // order status updates.
    message.Body = msg;
    message.too= order.mobileNumber;
}
```

#### <a name="asynchronous"></a><span data-ttu-id="ae40e-121">Asincrono</span><span class="sxs-lookup"><span data-stu-id="ae40e-121">Asynchronous</span></span>
<span data-ttu-id="ae40e-122">Questo codice di esempio asincrona per un trigger di coda di archiviazione di Azure invia un cliente tooa messaggio di testo che ha effettuato un ordine.</span><span class="sxs-lookup"><span data-stu-id="ae40e-122">This asynchronous example code for an Azure Storage queue trigger sends a text message tooa customer who placed an order.</span></span>

```cs
#r "Newtonsoft.Json"
#r "Twilio.Api"

using System;
using Newtonsoft.Json;
using Twilio;

public static async Task Run(string myQueueItem, IAsyncCollector<SMSMessage> message,  TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a JSON string representing an order that contains hello name of a 
    // customer and a mobile number toosend text updates to.
    dynamic order = JsonConvert.DeserializeObject(myQueueItem);
    string msg = "Hello " + order.name + ", thank you for your order.";

    // Even if you want toouse a hard coded message and number in hello binding, you must at least 
    // initialize hello SMSMessage variable.
    SMSMessage smsText = new SMSMessage();

    // A dynamic message can be set instead of hello body in hello output binding. In this example, we use 
    // hello order information toopersonalize a text message toohello mobile number provided for
    // order status updates.
    smsText.Body = msg;
    smsText.too= order.mobileNumber;

    await message.AddAsync(smsText);
}
```

## <a name="example-nodejs-queue-trigger-with-twilio-output-binding"></a><span data-ttu-id="ae40e-123">Esempio di trigger della coda Node.js con l'associazione output di Twilio</span><span class="sxs-lookup"><span data-stu-id="ae40e-123">Example Node.js queue trigger with Twilio output binding</span></span>
<span data-ttu-id="ae40e-124">In questo esempio Node.js invia un cliente tooa messaggio di testo che ha effettuato un ordine.</span><span class="sxs-lookup"><span data-stu-id="ae40e-124">This Node.js example sends a text message tooa customer who placed an order.</span></span>

```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);

    // In this example hello queue item is a JSON string representing an order that contains hello name of a 
    // customer and a mobile number toosend text updates to.
    var msg = "Hello " + myQueueItem.name + ", thank you for your order.";

    // Even if you want toouse a hard coded message and number in hello binding, you must at least 
    // initialize hello message binding.
    context.bindings.message = {};

    // A dynamic message can be set instead of hello body in hello output binding. In this example, we use 
    // hello order information toopersonalize a text message toohello mobile number provided for
    // order status updates.
    context.bindings.message = {
        body : msg,
        too: myQueueItem.mobileNumber
    };

    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="ae40e-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ae40e-125">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

