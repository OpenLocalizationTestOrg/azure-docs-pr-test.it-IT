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
# <a name="azure-functions-sendgrid-bindings"></a>Associazioni di SendGrid di Funzioni di Azure

Questo articolo viene illustrato come tooconfigure e di lavoro con le associazioni di SendGrid in funzioni di Azure. Con SendGrid, è possibile utilizzare posta elettronica personalizzato toosend funzioni di Azure a livello di codice.

Questo articolo contiene le informazioni di riferimento per gli sviluppatori di Funzioni di Azure. Nuove funzioni tooAzure, iniziare con hello seguenti risorse:

[Creare la prima funzione di Azure](functions-create-first-azure-function.md). 
Informazioni di riferimento per sviluppatori su [C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md) o [Node](functions-reference-node.md).

## <a name="functionjson-for-sendgrid-bindings"></a>function.json per associazioni di SendGrid

Funzioni di Azure offre associazioni di output per SendGrid. Hello SendGrid output associazione consente toocreate e invia posta elettronica a livello di codice. 

associazione di SendGrid Hello supporta hello le proprietà seguenti:

- `name`: Obbligatorio - nome della variabile hello utilizzati nel codice della funzione per richiesta hello o il corpo della richiesta. Questo valore è ```$return``` quando viene restituito un solo valore. 
- `type`: Obbligatorio - deve essere impostato troppo "sendGrid".
- `direction`: Obbligatorio - deve essere impostato troppo "out".
- `apiKey`: Obbligatorio - deve essere set toohello nome della chiave API archiviato nelle impostazioni dell'app dell'App di funzione hello.
- `to`: hello indirizzo di posta elettronica del destinatario.
- `from`: hello indirizzo di posta elettronica del mittente.
- `subject`: oggetto hello del messaggio di posta elettronica hello.
- `text`: hello contenuto messaggio di posta elettronica.

**function.json** di esempio:

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
> Funzioni di Azure archivia le informazioni di connessione e le chiavi API come impostazioni dell'app in modo che non vengano controllate nel repository di controllo del codice sorgente. In questo modo viene garantita la protezione delle informazioni riservate.
>
>

## <a name="c-example-of-hello-sendgrid-output-binding"></a>Associazione di output di esempio c# di hello SendGrid

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

## <a name="node-example-of-hello-sendgrid-output-binding"></a>Nodo di hello SendGrid output di esempio di associazione

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

## <a name="next-steps"></a>Passaggi successivi
Per informazioni sulle altre associazioni e i trigger per Funzioni di Azure, vedere 
- [Guida di riferimento per gli sviluppatori di trigger e associazioni di Funzioni di Azure](functions-triggers-bindings.md)

- [Procedure consigliate per le funzioni di Azure](functions-best-practices.md) sono elencate alcune procedure toouse di procedure consigliate durante la creazione di funzioni di Azure.

- La [guida di riferimento per gli sviluppatori di Funzioni di Azure](functions-reference.md) contiene informazioni di riferimento per programmatori in merito alla codifica delle funzioni e alla definizione di trigger e associazioni.
