---
title: Associazione di Twilio in Funzioni di Azure | Documentazione Microsoft
description: Informazioni su come usare le associazioni di Twilio in Funzioni di Azure.
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
ms.openlocfilehash: 870e47ec7f8ce41ee4acadc7b8ed59298958acbe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="send-sms-messages-from-azure-functions-using-the-twilio-output-binding"></a><span data-ttu-id="93faf-104">Inviare messaggi SMS da Funzioni di Azure usando il binding di output di Twilio</span><span class="sxs-lookup"><span data-stu-id="93faf-104">Send SMS messages from Azure Functions using the Twilio output binding</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="93faf-105">Questo articolo illustra come configurare e usare le associazioni di Twilio in Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="93faf-105">This article explains how to configure and use Twilio bindings with Azure Functions.</span></span> 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="93faf-106">Funzioni di Azure supporta le associazioni output di Twilio per consentire alle funzioni di inviare messaggi SMS con poche righe di codice e un account di [Twilio](https://www.twilio.com/).</span><span class="sxs-lookup"><span data-stu-id="93faf-106">Azure Functions supports Twilio output bindings to enable your functions to send SMS text messages with a few lines of code and a [Twilio](https://www.twilio.com/) account.</span></span> 

## <a name="functionjson-for-the-twilio-output-binding"></a><span data-ttu-id="93faf-107">File function.json per il binding di output di Twilio</span><span class="sxs-lookup"><span data-stu-id="93faf-107">function.json for the Twilio output binding</span></span>
<span data-ttu-id="93faf-108">Il file function.json specifica le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="93faf-108">The function.json file provides the following properties:</span></span>

* <span data-ttu-id="93faf-109">`name` : nome della variabile usato nel codice della funzione per il messaggio SMS di Twilio.</span><span class="sxs-lookup"><span data-stu-id="93faf-109">`name` : Variable name used in function code for the Twilio SMS text message.</span></span>
* <span data-ttu-id="93faf-110">`type` : deve essere impostato su *"twilioSms"*.</span><span class="sxs-lookup"><span data-stu-id="93faf-110">`type` : must be set to *"twilioSms"*.</span></span>
* <span data-ttu-id="93faf-111">`accountSid` : questo valore deve essere impostato sul nome di un'impostazione dell'app che contiene il SID account di Twilio.</span><span class="sxs-lookup"><span data-stu-id="93faf-111">`accountSid` : This value must be set to the name of an App Setting that holds your Twilio Account Sid.</span></span>
* <span data-ttu-id="93faf-112">`authToken` : questo valore deve essere impostato sul nome di un'impostazione dell'app che contiene il token di autenticazione di Twilio.</span><span class="sxs-lookup"><span data-stu-id="93faf-112">`authToken` : This value must be set to the name of an App Setting that holds your Twilio authentication token.</span></span>
* <span data-ttu-id="93faf-113">`to` : questo valore viene impostato sul numero di telefono a cui viene inviato il messaggio SMS.</span><span class="sxs-lookup"><span data-stu-id="93faf-113">`to` : This value is set to the phone number that the SMS text is sent to.</span></span>
* <span data-ttu-id="93faf-114">`from` : questo valore viene impostato sul numero di telefono da cui viene inviato il messaggio SMS.</span><span class="sxs-lookup"><span data-stu-id="93faf-114">`from` : This value is set to the phone number that the SMS text is sent from.</span></span>
* <span data-ttu-id="93faf-115">`direction` : deve essere impostato su *"out"*.</span><span class="sxs-lookup"><span data-stu-id="93faf-115">`direction` : must be set to *"out"*.</span></span>
* <span data-ttu-id="93faf-116">`body` : questo valore può essere usato per codificare il messaggio SMS se non occorre impostarlo dinamicamente nel codice per la funzione.</span><span class="sxs-lookup"><span data-stu-id="93faf-116">`body` : This value can be used to hard code the SMS text message if you don't need to set it dynamically in the code for your function.</span></span> 

<span data-ttu-id="93faf-117">Function.json di esempio:</span><span class="sxs-lookup"><span data-stu-id="93faf-117">Example function.json:</span></span>

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


## <a name="example-c-queue-trigger-with-twilio-output-binding"></a><span data-ttu-id="93faf-118">Esempio di trigger della coda C# con l'associazione output di Twilio</span><span class="sxs-lookup"><span data-stu-id="93faf-118">Example C# queue trigger with Twilio output binding</span></span>
#### <a name="synchronous"></a><span data-ttu-id="93faf-119">Sincrono</span><span class="sxs-lookup"><span data-stu-id="93faf-119">Synchronous</span></span>
<span data-ttu-id="93faf-120">Questo esempio di codice sincrono per un trigger della coda di Archiviazione di Azure usa un parametro out per inviare un messaggio di testo a un cliente che ha effettuato un ordine.</span><span class="sxs-lookup"><span data-stu-id="93faf-120">This synchronous example code for an Azure Storage queue trigger uses an out parameter to send a text message to a customer who placed an order.</span></span>

```cs
#r "Newtonsoft.Json"
#r "Twilio.Api"

using System;
using Newtonsoft.Json;
using Twilio;

public static void Run(string myQueueItem, out SMSMessage message,  TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a JSON string representing an order that contains the name of a 
    // customer and a mobile number to send text updates to.
    dynamic order = JsonConvert.DeserializeObject(myQueueItem);
    string msg = "Hello " + order.name + ", thank you for your order.";

    // Even if you want to use a hard coded message and number in the binding, you must at least 
    // initialize the SMSMessage variable.
    message = new SMSMessage();

    // A dynamic message can be set instead of the body in the output binding. In this example, we use 
    // the order information to personalize a text message to the mobile number provided for
    // order status updates.
    message.Body = msg;
    message.To = order.mobileNumber;
}
```

#### <a name="asynchronous"></a><span data-ttu-id="93faf-121">Asincrono</span><span class="sxs-lookup"><span data-stu-id="93faf-121">Asynchronous</span></span>
<span data-ttu-id="93faf-122">Questo esempio di codice asincrono per un trigger della coda di Archiviazione di Azure invia un messaggio di testo a un cliente che ha effettuato un ordine.</span><span class="sxs-lookup"><span data-stu-id="93faf-122">This asynchronous example code for an Azure Storage queue trigger sends a text message to a customer who placed an order.</span></span>

```cs
#r "Newtonsoft.Json"
#r "Twilio.Api"

using System;
using Newtonsoft.Json;
using Twilio;

public static async Task Run(string myQueueItem, IAsyncCollector<SMSMessage> message,  TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a JSON string representing an order that contains the name of a 
    // customer and a mobile number to send text updates to.
    dynamic order = JsonConvert.DeserializeObject(myQueueItem);
    string msg = "Hello " + order.name + ", thank you for your order.";

    // Even if you want to use a hard coded message and number in the binding, you must at least 
    // initialize the SMSMessage variable.
    SMSMessage smsText = new SMSMessage();

    // A dynamic message can be set instead of the body in the output binding. In this example, we use 
    // the order information to personalize a text message to the mobile number provided for
    // order status updates.
    smsText.Body = msg;
    smsText.To = order.mobileNumber;

    await message.AddAsync(smsText);
}
```

## <a name="example-nodejs-queue-trigger-with-twilio-output-binding"></a><span data-ttu-id="93faf-123">Esempio di trigger della coda Node.js con l'associazione output di Twilio</span><span class="sxs-lookup"><span data-stu-id="93faf-123">Example Node.js queue trigger with Twilio output binding</span></span>
<span data-ttu-id="93faf-124">Questo esempio di Node.js invia un messaggio di testo a un cliente che ha effettuato un ordine.</span><span class="sxs-lookup"><span data-stu-id="93faf-124">This Node.js example sends a text message to a customer who placed an order.</span></span>

```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);

    // In this example the queue item is a JSON string representing an order that contains the name of a 
    // customer and a mobile number to send text updates to.
    var msg = "Hello " + myQueueItem.name + ", thank you for your order.";

    // Even if you want to use a hard coded message and number in the binding, you must at least 
    // initialize the message binding.
    context.bindings.message = {};

    // A dynamic message can be set instead of the body in the output binding. In this example, we use 
    // the order information to personalize a text message to the mobile number provided for
    // order status updates.
    context.bindings.message = {
        body : msg,
        to : myQueueItem.mobileNumber
    };

    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="93faf-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="93faf-125">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

