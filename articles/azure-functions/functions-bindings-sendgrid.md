---
title: associazioni di funzioni SendGrid aaaAzure | Documenti Microsoft
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
ms.openlocfilehash: 10a3837875eb6ae18e6c789bcf64cc401cf5f26a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-sendgrid-bindings"></a><span data-ttu-id="4ee94-103">Associazioni di SendGrid di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="4ee94-103">Azure Functions SendGrid bindings</span></span>

<span data-ttu-id="4ee94-104">Questo articolo viene illustrato come tooconfigure e di lavoro con le associazioni di SendGrid in funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ee94-104">This article explains how tooconfigure and work with SendGrid bindings in Azure Functions.</span></span> <span data-ttu-id="4ee94-105">Con SendGrid, è possibile utilizzare posta elettronica personalizzato toosend funzioni di Azure a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="4ee94-105">With SendGrid, you can use Azure Functions toosend customized email programmatically.</span></span>

<span data-ttu-id="4ee94-106">Questo articolo contiene le informazioni di riferimento per gli sviluppatori di Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ee94-106">This article is reference information for Azure Functions developers.</span></span> <span data-ttu-id="4ee94-107">Nuove funzioni tooAzure, iniziare con hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="4ee94-107">If you're new tooAzure Functions, start with hello following resources:</span></span>

<span data-ttu-id="4ee94-108">[Creare la prima funzione di Azure](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="4ee94-108">[Create your first Azure Function](functions-create-first-azure-function.md).</span></span> 
<span data-ttu-id="4ee94-109">Informazioni di riferimento per sviluppatori su [C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md) o [Node](functions-reference-node.md).</span><span class="sxs-lookup"><span data-stu-id="4ee94-109">[C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md), or [Node](functions-reference-node.md) developer references.</span></span>

## <a name="functionjson-for-sendgrid-bindings"></a><span data-ttu-id="4ee94-110">function.json per associazioni di SendGrid</span><span class="sxs-lookup"><span data-stu-id="4ee94-110">function.json for SendGrid bindings</span></span>

<span data-ttu-id="4ee94-111">Funzioni di Azure offre associazioni di output per SendGrid.</span><span class="sxs-lookup"><span data-stu-id="4ee94-111">Azure Functions provides an output binding for SendGrid.</span></span> <span data-ttu-id="4ee94-112">Hello SendGrid output associazione consente toocreate e invia posta elettronica a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="4ee94-112">hello SendGrid output binding enables you toocreate and send email programmatically.</span></span> 

<span data-ttu-id="4ee94-113">associazione di SendGrid Hello supporta hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="4ee94-113">hello SendGrid binding supports hello following properties:</span></span>

- <span data-ttu-id="4ee94-114">`name`: Obbligatorio - nome della variabile hello utilizzati nel codice della funzione per richiesta hello o il corpo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="4ee94-114">`name` : Required - hello variable name used in function code for hello request or request body.</span></span> <span data-ttu-id="4ee94-115">Questo valore è ```$return``` quando viene restituito un solo valore.</span><span class="sxs-lookup"><span data-stu-id="4ee94-115">This value is ```$return``` when there is only one return value.</span></span> 
- <span data-ttu-id="4ee94-116">`type`: Obbligatorio - deve essere impostato troppo "sendGrid".</span><span class="sxs-lookup"><span data-stu-id="4ee94-116">`type` : Required - must be set too"sendGrid."</span></span>
- <span data-ttu-id="4ee94-117">`direction`: Obbligatorio - deve essere impostato troppo "out".</span><span class="sxs-lookup"><span data-stu-id="4ee94-117">`direction` : Required - must be set too"out."</span></span>
- <span data-ttu-id="4ee94-118">`apiKey`: Obbligatorio - deve essere set toohello nome della chiave API archiviato nelle impostazioni dell'app dell'App di funzione hello.</span><span class="sxs-lookup"><span data-stu-id="4ee94-118">`apiKey` : Required - must be set toohello name of your API key stored in hello Function App's app settings.</span></span>
- <span data-ttu-id="4ee94-119">`to`: hello indirizzo di posta elettronica del destinatario.</span><span class="sxs-lookup"><span data-stu-id="4ee94-119">`to` : hello recipient's email address.</span></span>
- <span data-ttu-id="4ee94-120">`from`: hello indirizzo di posta elettronica del mittente.</span><span class="sxs-lookup"><span data-stu-id="4ee94-120">`from` : hello sender's email address.</span></span>
- <span data-ttu-id="4ee94-121">`subject`: oggetto hello del messaggio di posta elettronica hello.</span><span class="sxs-lookup"><span data-stu-id="4ee94-121">`subject` : hello subject of hello email.</span></span>
- <span data-ttu-id="4ee94-122">`text`: hello contenuto messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="4ee94-122">`text` : hello email content.</span></span>

<span data-ttu-id="4ee94-123">**function.json** di esempio:</span><span class="sxs-lookup"><span data-stu-id="4ee94-123">Example of **function.json**:</span></span>

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
> <span data-ttu-id="4ee94-124">Funzioni di Azure archivia le informazioni di connessione e le chiavi API come impostazioni dell'app in modo che non vengano controllate nel repository di controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="4ee94-124">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="4ee94-125">In questo modo viene garantita la protezione delle informazioni riservate.</span><span class="sxs-lookup"><span data-stu-id="4ee94-125">This action safeguards your sensitive information.</span></span>
>
>

## <a name="c-example-of-hello-sendgrid-output-binding"></a><span data-ttu-id="4ee94-126">Associazione di output di esempio c# di hello SendGrid</span><span class="sxs-lookup"><span data-stu-id="4ee94-126">C# example of hello SendGrid output binding</span></span>

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

## <a name="node-example-of-hello-sendgrid-output-binding"></a><span data-ttu-id="4ee94-127">Nodo di hello SendGrid output di esempio di associazione</span><span class="sxs-lookup"><span data-stu-id="4ee94-127">Node example of hello SendGrid output binding</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="4ee94-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4ee94-128">Next steps</span></span>
<span data-ttu-id="4ee94-129">Per informazioni sulle altre associazioni e i trigger per Funzioni di Azure, vedere</span><span class="sxs-lookup"><span data-stu-id="4ee94-129">For information about other bindings and triggers for Azure Functions, see</span></span> 
- [<span data-ttu-id="4ee94-130">Guida di riferimento per gli sviluppatori di trigger e associazioni di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="4ee94-130">Azure Functions triggers and bindings developer reference</span></span>](functions-triggers-bindings.md)

- <span data-ttu-id="4ee94-131">[Procedure consigliate per le funzioni di Azure](functions-best-practices.md) sono elencate alcune procedure toouse di procedure consigliate durante la creazione di funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ee94-131">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices toouse when creating Azure Functions.</span></span>

- <span data-ttu-id="4ee94-132">La [guida di riferimento per gli sviluppatori di Funzioni di Azure](functions-reference.md) contiene informazioni di riferimento per programmatori in merito alla codifica delle funzioni e alla definizione di trigger e associazioni.</span><span class="sxs-lookup"><span data-stu-id="4ee94-132">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>
