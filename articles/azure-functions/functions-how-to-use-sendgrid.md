---
title: aaaHow toouse SendGrid nelle funzioni di Azure | Documenti Microsoft
description: Viene illustrato come toouse SendGrid nelle funzioni di Azure
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 01/31/2017
ms.author: rachelap
ms.openlocfilehash: a0ffdae04e5924c773d2d26427626fc1f570f7ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-sendgrid-in-azure-functions"></a>Come toouse SendGrid nelle funzioni di Azure

## <a name="sendgrid-overview"></a>Panoramica di SendGrid

Azure supporta funzioni SendGrid output associazioni tooenable i messaggi di posta elettronica toosend funzioni con poche righe di codice e un account di SendGrid.

API di SendGrid toouse hello in una funzione di Azure, è necessario disporre di un [account SendGrid](http://SendGrid.com). Inoltre, è necessario disporre di una chiave dell'API di SendGrid. Accedi tooyour account SendGrid e fare clic su **impostazioni** quindi **chiave API** chiave toogenerate un'API. Fare in modo che questa chiave sia disponibile per l'uso nel passaggio successivo.

Si è ora pronto toocreate un'app di Azure (funzione).

## <a name="create-an-azure-function-app"></a>Creare un'app per le funzioni di Azure 

Le app per le funzioni di Azure sono contenitori per uno o più funzioni di Azure. Le funzioni di Azure sono solo delle funzioni. Ogni funzione di Azure è abbinato tooone trigger, che è un evento che causa toorun funzione hello.
Ogni funzione può contenere diverse associazioni di input oppure output. Le associazioni sono servizi che è possibile usare in una funzione. SendGrid è un output di associazione è possibile utilizzare posta elettronica toosend. 

1. Accedi al portale di Azure toohello e [creare un'App di Azure funzione](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) oppure aprire un'app di funzione esistente. 
2. Creare una funzione di Azure. tookeep è semplice, scegliere un trigger manuale e c#. 

 ![Creare una funzione di Azure](./media/functions-how-to-use-sendgrid/functions-new-function-manual-trigger-page.png)

## <a name="configure-sendgrid-for-use-in-an-azure-function-app"></a>Configurare SendGrid per l'uso in un'app per le funzioni di Azure

È necessario archiviare la chiave API SendGrid come un toouse impostazione app in una funzione. campo di Hello ApiKey non è la chiave API SendGrid effettiva, ma un'impostazione di app definire che rappresenta la chiave API effettiva. Per sicurezza si esegue questo tipo di archiviazione della chiave, poiché è separata da qualsiasi codice o file che potrebbe essere archiviato nel controllo del codice sorgente.

- Creare una chiave **AppSettings** in **Impostazioni applicazione** dell'app per le funzioni.

 ![Creare una funzione di Azure](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-api-key-app-settings.png)

## <a name="configure-sendgrid-output-bindings"></a>Configurare le associazioni di output di SendGrid

SendGrid è disponibile come associazione di output della funzione di Azure. associazione di output toocreate un SendGrid:

1. Passare toohello **integrazione** scheda della funzione hello in hello portale di Azure.
2. Fare clic su **nuovo Output** toocreate un SendGrid associazione di output.
3. Compilare hello **chiave API** e **nome del parametro messaggio** proprietà. Se si desidera, è possibile immettere hello ora altre proprietà, o le code invece. Queste impostazioni possono essere usate come impostazioni predefinite.

 ![Configurare le associazioni di output di SendGrid](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-output-bindings.png)

Aggiunta di una funzione di tooa associazione crea un file denominato **function.json** nella cartella della funzione. Questo file contiene tutti hello stesse informazioni, vedere in hello Azure funzione **integrazione** scheda, ma in Json formato. Hello impostazione **ApiKey**, **messaggio**, e **da** campi creano hello seguenti voci hello **function.json** file: 

```json
{
  "bindings": [    
    {
      "type": "sendGrid",
      "name": "message",
      "apiKey": "SendGridKey",
      "direction": "out",
      "from": "azure@contoso.com"
    }
  ],
  "disabled": false
}
```

Se lo si preferisce, è possibile modificare direttamente questo file.

Ora che è creato e configurato hello App di funzione e la funzione, è possibile scrivere un messaggio di posta elettronica toosend codice hello.

## <a name="write-code-that-creates-and-sends-email"></a>Scrivere il codice che crea e invia email

Hello API SendGrid contiene tutti i comandi hello è necessario toocreate e inviare un messaggio di posta elettronica.  

- Sostituire il codice di hello nella funzione hello con hello seguente codice:

```cs
#r "SendGrid"
using System;
using SendGrid.Helpers.Mail;

public static void Run(TraceWriter log, string input, out Mail message)
{
    message = new Mail
    {        
        Subject = "Azure news"          
    };

    var personalization = new Personalization();
    // change tooemail of recipient
    personalization.AddTo(new Email("MoreEmailPlease@contoso.com"));   

    Content content = new Content
    {
        Type = "text/plain",
        Value = input
    };
    message.AddContent(content);
    message.AddPersonalization(personalization);
}
```

Si noti hello prima riga contiene hello ```#r``` direttiva che fa riferimento all'assembly SendGrid hello. Successivamente, è possibile utilizzare un ```using``` toomore istruzione accedere facilmente agli oggetti di hello nello spazio dei nomi. Nel codice hello, creare istanze di ```Mail```, ```Personalization```, e ```Content``` oggetti hello API SendGrid che compongono e-mail hello. Quando viene restituito il messaggio hello, SendGrid lo recapita. 

Hello firma della funzione contiene inoltre un ulteriore parametro di tipo out ```Mail``` denominato ```message```. Le associazioni di input e output si esprimono come parametri di funzione nel codice. 

2. Testare il codice facendo clic su **Test** e provochi un messaggio hello **corpo della richiesta** campo, quindi fare clic su hello **eseguire** pulsante.

 ![Testare il codice](./media/functions-how-to-use-sendgrid/functions-develop-test-sendgrid.png)

3. Verificare che SendGrid inviato tramite posta elettronica hello tooverify di posta elettronica. E deve passare toohello indirizzo nel codice hello dal passaggio 1 e contiene il messaggio hello da hello **corpo della richiesta**.

## <a name="next-steps"></a>Passaggi successivi
In questo articolo ha dimostrato come toouse hello toocreate servizio SendGrid e inviare posta elettronica. toolearn ulteriori informazioni sull'utilizzo delle funzioni di Azure nelle app di Windows, vedere hello seguenti argomenti: 

- [Procedure consigliate per le funzioni di Azure](functions-best-practices.md) sono elencate alcune procedure toouse di procedure consigliate durante la creazione di funzioni di Azure.

- La [guida di riferimento per gli sviluppatori di Funzioni di Azure](functions-reference.md) contiene informazioni di riferimento per programmatori in merito alla codifica delle funzioni e alla definizione di trigger e associazioni.

- [Test di Funzioni di Azure](functions-test-a-function.md) descrive diversi strumenti e tecniche per il test delle funzioni.