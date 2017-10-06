---
title: hello toouse aaaHow SendGrid servizio di posta elettronica (Node.js) | Documenti Microsoft
description: Informazioni su come inviare posta elettronica con il servizio di posta elettronica SendGrid hello in Azure. Scritto utilizzando API Node.js hello esempi di codice.
services: 
documentationcenter: nodejs
author: erikre
manager: wpickett
editor: 
ms.assetid: cac444b4-26b0-45ea-9c3d-eca28d57dacb
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 01/05/2016
ms.author: erikre
ms.openlocfilehash: fd617b6aaa656e7b5dd51c51ebb0db1e848450f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-from-nodejs"></a>Come messaggio di posta elettronica usando SendGrid da Node.js tooSend
Questa guida illustra come tooperform attività di programmazione comuni con di SendGrid tramite posta elettronica del servizio in Azure. esempi di Hello vengono scritti utilizzando hello API Node.js. Hello scenari trattati includono **la costruzione di posta elettronica**, **l'invio di posta elettronica**, **aggiungere allegati**, **utilizzando filtri**e **l'aggiornamento delle proprietà**. Per ulteriori informazioni su SendGrid e l'invio di posta elettronica, vedere hello [passaggi successivi](#next-steps) sezione.

## <a name="what-is-hello-sendgrid-email-service"></a>Che cos'è il servizio di posta elettronica SendGrid hello?
SendGrid è un [servizio di posta elettronica basato sul cloud] che offre [recapito affidabile di messaggi di posta elettronica transazionali], scalabilità e analisi in tempo reale, oltre ad API flessibili che agevolano l'integrazione personalizzata. Gli scenari di utilizzo comuni di SendGrid includono:

* Inviare automaticamente toocustomers conferme di recapito
* Amministrazione di liste di distribuzione per l'invio mensile ai clienti di volantini elettronici e offerte speciali
* Raccolta di metriche in tempo reale per elementi quali indirizzi di posta elettronica bloccati e velocità di risposta al cliente
* Generazione di report toohelp identificare le tendenze
* Inoltro di richieste dei clienti
* Notifiche di posta elettronica dall'applicazione

Per altre informazioni, vedere [https://sendgrid.com](https://sendgrid.com).

## <a name="create-a-sendgrid-account"></a>Creazione di un account SendGrid
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-nodejs-module"></a>Hello riferimento modulo Node.js di SendGrid
modulo di SendGrid Hello per Node.js può essere installata tramite Gestione pacchetti di nodi hello (npm) utilizzando hello comando seguente:

    npm install sendgrid

Dopo l'installazione, è possibile richiedere modulo hello nell'applicazione utilizzando hello seguente codice:

    var sendgrid = require('sendgrid')(sendgrid_username, sendgrid_password);

hello esportati dal modulo di SendGrid Hello **SendGrid** e **posta elettronica** funzioni.
**SendGrid** è responsabile dell'invio di e-mail tramite API Web, mentre **Email** incapsula un'e-mail.

## <a name="how-to-create-an-email"></a>Procedura: Creare un messaggio di posta elettronica
Creazione di un messaggio di posta elettronica utilizzando il modulo di SendGrid hello comporta innanzitutto la creazione di un messaggio di posta elettronica funzione hello del messaggio di posta elettronica e quindi inviarlo tramite hello SendGrid funzione. Hello Ecco un esempio di creazione di un nuovo messaggio di posta elettronica di hello funzione:

    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

È inoltre possibile specificare un messaggio HTML per i client che lo supportano, impostando la proprietà html hello. ad esempio:

    html: This is a sample <b>HTML<b> email message.

Impostazione delle proprietà di testo e html entrambi hello fornisce normale fallback al contenuto di testo per i client che non è in grado di supportare i messaggi HTML.

Per ulteriori informazioni su tutte le proprietà supportate da hello funzione posta elettronica, vedere [sendgrid nodejs][sendgrid-nodejs].

## <a name="how-to-send-an-email"></a>Procedura: Inviare un messaggio di posta elettronica
Dopo aver creato un messaggio di posta elettronica utilizzando hello funzione posta elettronica, è possibile inviare tramite l'API Web fornita da SendGrid hello. 

### <a name="web-api"></a>API Web
    sendgrid.send(email, function(err, json){
        if(err) { return console.error(err); }
        console.log(json);
    });

> [!NOTE]
> Mentre hello esempi sopra viene visualizzato il passaggio in una funzione di oggetto e il callback di posta elettronica, è possibile richiamare direttamente la funzione di invio hello specificando direttamente le proprietà di messaggio di posta elettronica. ad esempio:  
> 
> `````
> sendgrid.send({
> to: 'john@contoso.com',
> from: 'anna@contoso.com',
> subject: 'test mail',
> text: 'This is a sample email message.'
> });
> `````
> 
> 

## <a name="how-to-add-an-attachment"></a>Procedura: Aggiungere un allegato
È possibile aggiungere allegati tooa messaggio specificando i nomi dei file hello e percorsi in hello **file** proprietà. Hello di esempio seguente viene illustrato l'invio di un allegato:

    sendgrid.send({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.',
        files: [
            {
                filename:     '',           // required only if file.content is used.
                contentType:  '',           // optional
                cid:          '',           // optional, used toospecify cid for inline content
                path:         '',           //
                url:          '',           // == One of these three options is required
                content:      ('' | Buffer) //
            }
        ],
    });

> [!NOTE]
> Quando si utilizza hello **file** proprietà hello file deve essere accessibile tramite [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile). Se il file hello desiderato tooattach è ospitato in archiviazione di Azure, ad esempio in un contenitore Blob, è prima necessario copiare archiviazione toolocal nel file hello o tooan unità Azure prima di poter essere inviato come allegato utilizzando hello **file** proprietà.
> 
> 

## <a name="how-to-use-filters-tooenable-footers-and-tracking"></a>Procedura: utilizzare i filtri tooEnable piè di pagina e rilevamento
SendGrid fornisce funzionalità di posta elettronica aggiuntivo tramite l'utilizzo di hello dei filtri. Si tratta di impostazioni che è possibile aggiungere il messaggio di posta elettronica tooan per abilitare le funzionalità specifiche, quali l'abilitazione di fare clic su rilevamento, Google analitica, di rilevamento, sottoscrizione e così via. Per un elenco completo dei filtri, vedere le [impostazioni dei filtri][Filter Settings].

I filtri possono essere applicati tooa messaggio utilizzando hello **filtri** proprietà.
Ogni filtro è specificato da un hash che contiene impostazioni specifiche del filtro.
Hello negli esempi seguenti illustrano piè di pagina hello e fare clic su Verifica filtri:

### <a name="footer"></a>Piè di pagina
    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

    email.setFilters({
        'footer': {
            'settings': {
                'enable': 1,
                'text/plain': 'This is a text footer.'
            }
        }
    });

    sendgrid.send(email);

### <a name="click-tracking"></a>Monitoraggio dei clic
    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

    email.setFilters({
        'clicktrack': {
            'settings': {
                'enable': 1
            }
        }
    });

    sendgrid.send(email);

## <a name="how-to-update-email-properties"></a>Procedura: Aggiornare le proprietà dei messaggi di posta elettronica
Alcune proprietà del messaggio di posta elettronica può essere sovrascritto usando  **impostare*proprietà** * o aggiunti utilizzando  **aggiungere*proprietà** *. Ad esempio, è possibile aggiungere altri destinatari usando

    email.addTo('jeff@contoso.com');

oppure impostare un filtro utilizzando

    email.addFilter('footer', 'enable', 1);
    email.addFilter('footer', 'text/html', '<strong>boo</strong>');

Per ulteriori informazioni, vedere [sendgrid nodejs][sendgrid-nodejs].

## <a name="how-to-use-additional-sendgrid-services"></a>Procedura: Usare servizi aggiuntivi forniti da SendGrid
SendGrid offre API basata sul web che è possibile utilizzare altre funzionalità di SendGrid tooleverage dall'applicazione Azure. Per informazioni dettagliate, vedere hello [documentazione dell'API SendGrid][SendGrid API documentation].

## <a name="next-steps"></a>Passaggi successivi
Ora che si è appreso nozioni di base di hello di hello servizio di posta elettronica di SendGrid, seguire questi ulteriori toolearn di collegamenti.

* Repository di moduli SendGrid Node.js: [sendgrid nodejs][sendgrid-nodejs]
* Documentazione relativa all'API SendGrid: <https://sendgrid.com/docs>
* Offerta speciale SendGrid per i clienti di Azure: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)

[special offer]: https://sendgrid.com/windowsazure.html
[sendgrid-nodejs]: https://github.com/sendgrid/sendgrid-nodejs
[Filter Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs
[servizio di posta elettronica basato sul cloud]: https://sendgrid.com/email-solutions
[recapito affidabile di messaggi di posta elettronica transazionali]: https://sendgrid.com/transactional-email
