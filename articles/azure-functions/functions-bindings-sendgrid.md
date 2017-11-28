---
title: Associazioni di SendGrid di Funzioni di Azure | Microsoft Docs
description: Riferimento per le associazioni di SendGrid di Funzioni di Azure
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/16/2017
ms.author: rachelap
ms.openlocfilehash: 445a40a884e648cdb2a57f8ef43bed4f8a3efcf2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-sendgrid-bindings"></a><span data-ttu-id="a189a-103">Associazioni di SendGrid di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="a189a-103">Azure Functions SendGrid bindings</span></span>

<span data-ttu-id="a189a-104">Questo articolo illustra come configurare e usare le associazioni SendGrid in Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="a189a-104">This article explains how to configure and work with SendGrid bindings in Azure Functions.</span></span> <span data-ttu-id="a189a-105">Con Sendgrid è possibile usare Funzioni di Azure per inviare messaggi di posta elettronica personalizzati a livello programmatico.</span><span class="sxs-lookup"><span data-stu-id="a189a-105">With SendGrid, you can use Azure Functions to send customized email programmatically.</span></span>

<span data-ttu-id="a189a-106">Questo articolo contiene le informazioni di riferimento per gli sviluppatori di Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="a189a-106">This article is reference information for Azure Functions developers.</span></span> <span data-ttu-id="a189a-107">Se non si ha familiarità con le Funzioni di Azure, iniziare con le seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="a189a-107">If you're new to Azure Functions, start with the following resources:</span></span>

<span data-ttu-id="a189a-108">[Creare la prima funzione di Azure](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="a189a-108">[Create your first Azure Function](functions-create-first-azure-function.md).</span></span> 
<span data-ttu-id="a189a-109">Informazioni di riferimento per sviluppatori su [C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md) o [Node](functions-reference-node.md).</span><span class="sxs-lookup"><span data-stu-id="a189a-109">[C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md), or [Node](functions-reference-node.md) developer references.</span></span>

## <a name="functionjson-for-sendgrid-bindings"></a><span data-ttu-id="a189a-110">function.json per associazioni di SendGrid</span><span class="sxs-lookup"><span data-stu-id="a189a-110">function.json for SendGrid bindings</span></span>

<span data-ttu-id="a189a-111">Funzioni di Azure offre associazioni di output per SendGrid.</span><span class="sxs-lookup"><span data-stu-id="a189a-111">Azure Functions provides an output binding for SendGrid.</span></span> <span data-ttu-id="a189a-112">L'associazione di output di SendGrid consente di creare e inviare messaggi di posta elettronica a livello programmatico.</span><span class="sxs-lookup"><span data-stu-id="a189a-112">The SendGrid output binding enables you to create and send email programmatically.</span></span> 

<span data-ttu-id="a189a-113">L'associazione SendGrid supporta le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="a189a-113">The SendGrid binding supports the following properties:</span></span>

- <span data-ttu-id="a189a-114">`name`: obbligatoria. Nome della variabile usato nel codice della funzione per la richiesta o il corpo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="a189a-114">`name` : Required - the variable name used in function code for the request or request body.</span></span> <span data-ttu-id="a189a-115">Questo valore è ```$return``` quando viene restituito un solo valore.</span><span class="sxs-lookup"><span data-stu-id="a189a-115">This value is ```$return``` when there is only one return value.</span></span> 
- <span data-ttu-id="a189a-116">`type`: obbligatoria. Deve essere impostata su "sendGrid".</span><span class="sxs-lookup"><span data-stu-id="a189a-116">`type` : Required - must be set to "sendGrid."</span></span>
- <span data-ttu-id="a189a-117">`direction`: obbligatoria. Deve essere impostata su "out".</span><span class="sxs-lookup"><span data-stu-id="a189a-117">`direction` : Required - must be set to "out."</span></span>
- <span data-ttu-id="a189a-118">`apiKey`: obbligatoria. Deve essere impostato sul nome della chiave API archiviato nelle impostazioni app dell'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="a189a-118">`apiKey` : Required - must be set to the name of your API key stored in the Function App's app settings.</span></span>
- <span data-ttu-id="a189a-119">`to`: indirizzo di posta elettronica del destinatario.</span><span class="sxs-lookup"><span data-stu-id="a189a-119">`to` : the recipient's email address.</span></span>
- <span data-ttu-id="a189a-120">`from`: indirizzo di posta elettronica del mittente.</span><span class="sxs-lookup"><span data-stu-id="a189a-120">`from` : the sender's email address.</span></span>
- <span data-ttu-id="a189a-121">`subject`: l'oggetto del messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="a189a-121">`subject` : the subject of the email.</span></span>
- <span data-ttu-id="a189a-122">`text`: il contenuto del messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="a189a-122">`text` : the email content.</span></span>

<span data-ttu-id="a189a-123">**function.json** di esempio:</span><span class="sxs-lookup"><span data-stu-id="a189a-123">Example of **function.json**:</span></span>

```json 
{
    "bindings": [
        {
            "name": "$return",
            "type": "sendGrid",
            "direction": "out",
            "apiKey" : "MySendGridKey",
            "to": "{ToEmail}",
            "from": "{FromEmail}",
            "subject": "SendGrid output bindings"
        }
    ]
}
```

> [!NOTE]
> <span data-ttu-id="a189a-124">Funzioni di Azure archivia le informazioni di connessione e le chiavi API come impostazioni dell'app in modo che non vengano controllate nel repository di controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="a189a-124">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="a189a-125">In questo modo viene garantita la protezione delle informazioni riservate.</span><span class="sxs-lookup"><span data-stu-id="a189a-125">This action safeguards your sensitive information.</span></span>
>
>

## <a name="c-example-of-the-sendgrid-output-binding"></a><span data-ttu-id="a189a-126">C# di esempio dell'associazione di output SendGrid</span><span class="sxs-lookup"><span data-stu-id="a189a-126">C# example of the SendGrid output binding</span></span>

```csharp
#r "SendGrid"
using System;
using SendGrid.Helpers.Mail;

public static Mail Run(TraceWriter log, string input, out Mail message)
{
     message = new Mail
    {        
        Subject = "Azure news"          
    };

    var personalization = new Personalization();
    personalization.AddTo(new Email("recipient@contoso.com"));   

    Content content = new Content
    {
        Type = "text/plain",
        Value = input
    };
    message.AddContent(content);
    message.AddPersonalization(personalization);
}
```

## <a name="node-example-of-the-sendgrid-output-binding"></a><span data-ttu-id="a189a-127">Nodo di esempio dell'associazione di output SendGrid</span><span class="sxs-lookup"><span data-stu-id="a189a-127">Node example of the SendGrid output binding</span></span>

```javascript
module.exports = function (context, input) {    
    var message = {
         "personalizations": [ { "to": [ { "email": "sample@sample.com" } ] } ],
        from: "sender@contoso.com",        
        subject: "Azure news",
        content: [{
            type: 'text/plain',
            value: input
        }]
    };

    context.done(null, message);
};

```

## <a name="next-steps"></a><span data-ttu-id="a189a-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a189a-128">Next steps</span></span>
<span data-ttu-id="a189a-129">Per informazioni sulle altre associazioni e i trigger per Funzioni di Azure, vedere</span><span class="sxs-lookup"><span data-stu-id="a189a-129">For information about other bindings and triggers for Azure Functions, see</span></span> 
- [<span data-ttu-id="a189a-130">Guida di riferimento per gli sviluppatori di trigger e associazioni di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="a189a-130">Azure Functions triggers and bindings developer reference</span></span>](functions-triggers-bindings.md)

- <span data-ttu-id="a189a-131">L'articolo [Procedure consigliate per le funzioni di Azure](functions-best-practices.md) elenca alcune procedure consigliate da usare durante la creazione di Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="a189a-131">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices to use when creating Azure Functions.</span></span>

- <span data-ttu-id="a189a-132">La [guida di riferimento per gli sviluppatori di Funzioni di Azure](functions-reference.md) contiene informazioni di riferimento per programmatori in merito alla codifica delle funzioni e alla definizione di trigger e associazioni.</span><span class="sxs-lookup"><span data-stu-id="a189a-132">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>
