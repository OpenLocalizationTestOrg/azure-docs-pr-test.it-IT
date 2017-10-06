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
# <a name="how-toosend-email-using-sendgrid-from-nodejs"></a><span data-ttu-id="23ef5-104">Come messaggio di posta elettronica usando SendGrid da Node.js tooSend</span><span class="sxs-lookup"><span data-stu-id="23ef5-104">How tooSend Email Using SendGrid from Node.js</span></span>
<span data-ttu-id="23ef5-105">Questa guida illustra come tooperform attività di programmazione comuni con di SendGrid tramite posta elettronica del servizio in Azure.</span><span class="sxs-lookup"><span data-stu-id="23ef5-105">This guide demonstrates how tooperform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="23ef5-106">esempi di Hello vengono scritti utilizzando hello API Node.js.</span><span class="sxs-lookup"><span data-stu-id="23ef5-106">hello samples are written using hello Node.js API.</span></span> <span data-ttu-id="23ef5-107">Hello scenari trattati includono **la costruzione di posta elettronica**, **l'invio di posta elettronica**, **aggiungere allegati**, **utilizzando filtri**e **l'aggiornamento delle proprietà**.</span><span class="sxs-lookup"><span data-stu-id="23ef5-107">hello scenarios covered include **constructing email**, **sending email**, **adding attachments**, **using filters**, and **updating properties**.</span></span> <span data-ttu-id="23ef5-108">Per ulteriori informazioni su SendGrid e l'invio di posta elettronica, vedere hello [passaggi successivi](#next-steps) sezione.</span><span class="sxs-lookup"><span data-stu-id="23ef5-108">For more information on SendGrid and sending email, see hello [Next Steps](#next-steps) section.</span></span>

## <a name="what-is-hello-sendgrid-email-service"></a><span data-ttu-id="23ef5-109">Che cos'è il servizio di posta elettronica SendGrid hello?</span><span class="sxs-lookup"><span data-stu-id="23ef5-109">What is hello SendGrid Email Service?</span></span>
<span data-ttu-id="23ef5-110">SendGrid è un [servizio di posta elettronica basato sul cloud] che offre [recapito affidabile di messaggi di posta elettronica transazionali], scalabilità e analisi in tempo reale, oltre ad API flessibili che agevolano l'integrazione personalizzata.</span><span class="sxs-lookup"><span data-stu-id="23ef5-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="23ef5-111">Gli scenari di utilizzo comuni di SendGrid includono:</span><span class="sxs-lookup"><span data-stu-id="23ef5-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="23ef5-112">Inviare automaticamente toocustomers conferme di recapito</span><span class="sxs-lookup"><span data-stu-id="23ef5-112">Automatically sending receipts toocustomers</span></span>
* <span data-ttu-id="23ef5-113">Amministrazione di liste di distribuzione per l'invio mensile ai clienti di volantini elettronici e offerte speciali</span><span class="sxs-lookup"><span data-stu-id="23ef5-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="23ef5-114">Raccolta di metriche in tempo reale per elementi quali indirizzi di posta elettronica bloccati e velocità di risposta al cliente</span><span class="sxs-lookup"><span data-stu-id="23ef5-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="23ef5-115">Generazione di report toohelp identificare le tendenze</span><span class="sxs-lookup"><span data-stu-id="23ef5-115">Generating reports toohelp identify trends</span></span>
* <span data-ttu-id="23ef5-116">Inoltro di richieste dei clienti</span><span class="sxs-lookup"><span data-stu-id="23ef5-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="23ef5-117">Notifiche di posta elettronica dall'applicazione</span><span class="sxs-lookup"><span data-stu-id="23ef5-117">Email notifications from your application</span></span>

<span data-ttu-id="23ef5-118">Per altre informazioni, vedere [https://sendgrid.com](https://sendgrid.com).</span><span class="sxs-lookup"><span data-stu-id="23ef5-118">For more information, see [https://sendgrid.com](https://sendgrid.com).</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="23ef5-119">Creazione di un account SendGrid</span><span class="sxs-lookup"><span data-stu-id="23ef5-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-nodejs-module"></a><span data-ttu-id="23ef5-120">Hello riferimento modulo Node.js di SendGrid</span><span class="sxs-lookup"><span data-stu-id="23ef5-120">Reference hello SendGrid Node.js Module</span></span>
<span data-ttu-id="23ef5-121">modulo di SendGrid Hello per Node.js può essere installata tramite Gestione pacchetti di nodi hello (npm) utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="23ef5-121">hello SendGrid module for Node.js can be installed through hello node package manager (npm) by using hello following command:</span></span>

    npm install sendgrid

<span data-ttu-id="23ef5-122">Dopo l'installazione, è possibile richiedere modulo hello nell'applicazione utilizzando hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="23ef5-122">After installation, you can require hello module in your application by using hello following code:</span></span>

    var sendgrid = require('sendgrid')(sendgrid_username, sendgrid_password);

<span data-ttu-id="23ef5-123">hello esportati dal modulo di SendGrid Hello **SendGrid** e **posta elettronica** funzioni.</span><span class="sxs-lookup"><span data-stu-id="23ef5-123">hello SendGrid module exports hello **SendGrid** and **Email** functions.</span></span>
<span data-ttu-id="23ef5-124">**SendGrid** è responsabile dell'invio di e-mail tramite API Web, mentre **Email** incapsula un'e-mail.</span><span class="sxs-lookup"><span data-stu-id="23ef5-124">**SendGrid** is responsible for sending email through Web API, while **Email** encapsulates an email message.</span></span>

## <a name="how-to-create-an-email"></a><span data-ttu-id="23ef5-125">Procedura: Creare un messaggio di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="23ef5-125">How to: Create an Email</span></span>
<span data-ttu-id="23ef5-126">Creazione di un messaggio di posta elettronica utilizzando il modulo di SendGrid hello comporta innanzitutto la creazione di un messaggio di posta elettronica funzione hello del messaggio di posta elettronica e quindi inviarlo tramite hello SendGrid funzione.</span><span class="sxs-lookup"><span data-stu-id="23ef5-126">Creating an email message using hello SendGrid module involves first creating an email message using hello Email function, and then sending it using hello SendGrid function.</span></span> <span data-ttu-id="23ef5-127">Hello Ecco un esempio di creazione di un nuovo messaggio di posta elettronica di hello funzione:</span><span class="sxs-lookup"><span data-stu-id="23ef5-127">hello following is an example of creating a new message using hello Email function:</span></span>

    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

<span data-ttu-id="23ef5-128">È inoltre possibile specificare un messaggio HTML per i client che lo supportano, impostando la proprietà html hello.</span><span class="sxs-lookup"><span data-stu-id="23ef5-128">You can also specify an HTML message for clients that support it by setting hello html property.</span></span> <span data-ttu-id="23ef5-129">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="23ef5-129">For example:</span></span>

    html: This is a sample <b>HTML<b> email message.

<span data-ttu-id="23ef5-130">Impostazione delle proprietà di testo e html entrambi hello fornisce normale fallback al contenuto di testo per i client che non è in grado di supportare i messaggi HTML.</span><span class="sxs-lookup"><span data-stu-id="23ef5-130">Setting both hello text and html properties provides graceful fallback to text content for clients that cannot support HTML messages.</span></span>

<span data-ttu-id="23ef5-131">Per ulteriori informazioni su tutte le proprietà supportate da hello funzione posta elettronica, vedere [sendgrid nodejs][sendgrid-nodejs].</span><span class="sxs-lookup"><span data-stu-id="23ef5-131">For more information on all properties supported by hello Email function, see [sendgrid-nodejs][sendgrid-nodejs].</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="23ef5-132">Procedura: Inviare un messaggio di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="23ef5-132">How to: Send an Email</span></span>
<span data-ttu-id="23ef5-133">Dopo aver creato un messaggio di posta elettronica utilizzando hello funzione posta elettronica, è possibile inviare tramite l'API Web fornita da SendGrid hello.</span><span class="sxs-lookup"><span data-stu-id="23ef5-133">After creating an email message using hello Email function, you can send it using hello Web API provided by SendGrid.</span></span> 

### <a name="web-api"></a><span data-ttu-id="23ef5-134">API Web</span><span class="sxs-lookup"><span data-stu-id="23ef5-134">Web API</span></span>
    sendgrid.send(email, function(err, json){
        if(err) { return console.error(err); }
        console.log(json);
    });

> [!NOTE]
> <span data-ttu-id="23ef5-135">Mentre hello esempi sopra viene visualizzato il passaggio in una funzione di oggetto e il callback di posta elettronica, è possibile richiamare direttamente la funzione di invio hello specificando direttamente le proprietà di messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="23ef5-135">While hello above examples show passing in an email object and callback function, you can also directly invoke hello send function by directly specifying email properties.</span></span> <span data-ttu-id="23ef5-136">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="23ef5-136">For example:</span></span>  
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

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="23ef5-137">Procedura: Aggiungere un allegato</span><span class="sxs-lookup"><span data-stu-id="23ef5-137">How to: Add an Attachment</span></span>
<span data-ttu-id="23ef5-138">È possibile aggiungere allegati tooa messaggio specificando i nomi dei file hello e percorsi in hello **file** proprietà.</span><span class="sxs-lookup"><span data-stu-id="23ef5-138">Attachments can be added tooa message by specifying hello file name(s) and path(s) in hello **files** property.</span></span> <span data-ttu-id="23ef5-139">Hello di esempio seguente viene illustrato l'invio di un allegato:</span><span class="sxs-lookup"><span data-stu-id="23ef5-139">hello following example demonstrates sending an attachment:</span></span>

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
> <span data-ttu-id="23ef5-140">Quando si utilizza hello **file** proprietà hello file deve essere accessibile tramite [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile).</span><span class="sxs-lookup"><span data-stu-id="23ef5-140">When using hello **files** property, hello file must be accessible through [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile).</span></span> <span data-ttu-id="23ef5-141">Se il file hello desiderato tooattach è ospitato in archiviazione di Azure, ad esempio in un contenitore Blob, è prima necessario copiare archiviazione toolocal nel file hello o tooan unità Azure prima di poter essere inviato come allegato utilizzando hello **file** proprietà.</span><span class="sxs-lookup"><span data-stu-id="23ef5-141">If hello file you wish tooattach is hosted in Azure Storage, such as in a Blob container, you must first copy hello file toolocal storage or tooan Azure drive before it can be sent as an attachment using hello **files** property.</span></span>
> 
> 

## <a name="how-to-use-filters-tooenable-footers-and-tracking"></a><span data-ttu-id="23ef5-142">Procedura: utilizzare i filtri tooEnable piè di pagina e rilevamento</span><span class="sxs-lookup"><span data-stu-id="23ef5-142">How to: Use Filters tooEnable Footers and Tracking</span></span>
<span data-ttu-id="23ef5-143">SendGrid fornisce funzionalità di posta elettronica aggiuntivo tramite l'utilizzo di hello dei filtri.</span><span class="sxs-lookup"><span data-stu-id="23ef5-143">SendGrid provides additional email functionality through hello use of filters.</span></span> <span data-ttu-id="23ef5-144">Si tratta di impostazioni che è possibile aggiungere il messaggio di posta elettronica tooan per abilitare le funzionalità specifiche, quali l'abilitazione di fare clic su rilevamento, Google analitica, di rilevamento, sottoscrizione e così via.</span><span class="sxs-lookup"><span data-stu-id="23ef5-144">These are settings that can be added tooan email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="23ef5-145">Per un elenco completo dei filtri, vedere le [impostazioni dei filtri][Filter Settings].</span><span class="sxs-lookup"><span data-stu-id="23ef5-145">For a full list of filters, see [Filter Settings][Filter Settings].</span></span>

<span data-ttu-id="23ef5-146">I filtri possono essere applicati tooa messaggio utilizzando hello **filtri** proprietà.</span><span class="sxs-lookup"><span data-stu-id="23ef5-146">Filters can be applied tooa message by using hello **filters** property.</span></span>
<span data-ttu-id="23ef5-147">Ogni filtro è specificato da un hash che contiene impostazioni specifiche del filtro.</span><span class="sxs-lookup"><span data-stu-id="23ef5-147">Each filter is specified by a hash containing filter-specific settings.</span></span>
<span data-ttu-id="23ef5-148">Hello negli esempi seguenti illustrano piè di pagina hello e fare clic su Verifica filtri:</span><span class="sxs-lookup"><span data-stu-id="23ef5-148">hello following examples demonstrate hello footer and click tracking filters:</span></span>

### <a name="footer"></a><span data-ttu-id="23ef5-149">Piè di pagina</span><span class="sxs-lookup"><span data-stu-id="23ef5-149">Footer</span></span>
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

### <a name="click-tracking"></a><span data-ttu-id="23ef5-150">Monitoraggio dei clic</span><span class="sxs-lookup"><span data-stu-id="23ef5-150">Click Tracking</span></span>
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

## <a name="how-to-update-email-properties"></a><span data-ttu-id="23ef5-151">Procedura: Aggiornare le proprietà dei messaggi di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="23ef5-151">How to: Update Email Properties</span></span>
<span data-ttu-id="23ef5-152">Alcune proprietà del messaggio di posta elettronica può essere sovrascritto usando  **impostare*proprietà** * o aggiunti utilizzando  **aggiungere*proprietà** *.</span><span class="sxs-lookup"><span data-stu-id="23ef5-152">Some email properties can be overwritten using **set*Property*** or appended using **add*Property***.</span></span> <span data-ttu-id="23ef5-153">Ad esempio, è possibile aggiungere altri destinatari usando</span><span class="sxs-lookup"><span data-stu-id="23ef5-153">For example, you can add additional recipients by using</span></span>

    email.addTo('jeff@contoso.com');

<span data-ttu-id="23ef5-154">oppure impostare un filtro utilizzando</span><span class="sxs-lookup"><span data-stu-id="23ef5-154">or set a filter by using</span></span>

    email.addFilter('footer', 'enable', 1);
    email.addFilter('footer', 'text/html', '<strong>boo</strong>');

<span data-ttu-id="23ef5-155">Per ulteriori informazioni, vedere [sendgrid nodejs][sendgrid-nodejs].</span><span class="sxs-lookup"><span data-stu-id="23ef5-155">For more information, see [sendgrid-nodejs][sendgrid-nodejs].</span></span>

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="23ef5-156">Procedura: Usare servizi aggiuntivi forniti da SendGrid</span><span class="sxs-lookup"><span data-stu-id="23ef5-156">How to: Use Additional SendGrid Services</span></span>
<span data-ttu-id="23ef5-157">SendGrid offre API basata sul web che è possibile utilizzare altre funzionalità di SendGrid tooleverage dall'applicazione Azure.</span><span class="sxs-lookup"><span data-stu-id="23ef5-157">SendGrid offers web-based APIs that you can use tooleverage additional SendGrid functionality from your Azure application.</span></span> <span data-ttu-id="23ef5-158">Per informazioni dettagliate, vedere hello [documentazione dell'API SendGrid][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="23ef5-158">For full details, see hello [SendGrid API documentation][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="23ef5-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="23ef5-159">Next Steps</span></span>
<span data-ttu-id="23ef5-160">Ora che si è appreso nozioni di base di hello di hello servizio di posta elettronica di SendGrid, seguire questi ulteriori toolearn di collegamenti.</span><span class="sxs-lookup"><span data-stu-id="23ef5-160">Now that you've learned hello basics of hello SendGrid Email service, follow these links toolearn more.</span></span>

* <span data-ttu-id="23ef5-161">Repository di moduli SendGrid Node.js: [sendgrid nodejs][sendgrid-nodejs]</span><span class="sxs-lookup"><span data-stu-id="23ef5-161">SendGrid Node.js module repository: [sendgrid-nodejs][sendgrid-nodejs]</span></span>
* <span data-ttu-id="23ef5-162">Documentazione relativa all'API SendGrid: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="23ef5-162">SendGrid API documentation: <https://sendgrid.com/docs></span></span>
* <span data-ttu-id="23ef5-163">Offerta speciale SendGrid per i clienti di Azure: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)</span><span class="sxs-lookup"><span data-stu-id="23ef5-163">SendGrid special offer for Azure customers: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)</span></span>

[special offer]: https://sendgrid.com/windowsazure.html
[sendgrid-nodejs]: https://github.com/sendgrid/sendgrid-nodejs
[Filter Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs
[servizio di posta elettronica basato sul cloud]: https://sendgrid.com/email-solutions
[recapito affidabile di messaggi di posta elettronica transazionali]: https://sendgrid.com/transactional-email
