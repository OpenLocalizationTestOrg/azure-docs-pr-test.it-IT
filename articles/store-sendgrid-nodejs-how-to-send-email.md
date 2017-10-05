---
title: Come usare il servizio di e-mail SendGrid (Node.js) | Microsoft Docs
description: Informazioni su come inviare messaggi di posta elettronica con il servizio di posta elettronica SendGrid disponibile in Azure. Gli esempi di codice sono scritti mediante l'API Node.js.
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
ms.openlocfilehash: 327cea3a24cc47a9cc463b37cc2346ebc475ef7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-send-email-using-sendgrid-from-nodejs"></a><span data-ttu-id="6fca2-104">Come inviare messaggi di posta elettronica usando SendGrid da Node.js</span><span class="sxs-lookup"><span data-stu-id="6fca2-104">How to Send Email Using SendGrid from Node.js</span></span>
<span data-ttu-id="6fca2-105">Questa guida illustra come eseguire attività di programmazione comuni con il servizio di posta elettronica SendGrid in Azure.</span><span class="sxs-lookup"><span data-stu-id="6fca2-105">This guide demonstrates how to perform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="6fca2-106">Gli esempi sono scritti usando l'API Node.js.</span><span class="sxs-lookup"><span data-stu-id="6fca2-106">The samples are written using the Node.js API.</span></span> <span data-ttu-id="6fca2-107">Gli scenari presentati includono **creazione di messaggi di posta elettronica**, **invio di messaggi di posta elettronica**, **aggiunta di allegati**, **uso di filtri** e **aggiornamento delle proprietà**.</span><span class="sxs-lookup"><span data-stu-id="6fca2-107">The scenarios covered include **constructing email**, **sending email**, **adding attachments**, **using filters**, and **updating properties**.</span></span> <span data-ttu-id="6fca2-108">Per altre informazioni su SendGrid e sull'invio della posta elettronica, vedere la sezione [Passaggi successivi](#next-steps) .</span><span class="sxs-lookup"><span data-stu-id="6fca2-108">For more information on SendGrid and sending email, see the [Next Steps](#next-steps) section.</span></span>

## <a name="what-is-the-sendgrid-email-service"></a><span data-ttu-id="6fca2-109">Informazioni sul servizio di posta elettronica SendGrid</span><span class="sxs-lookup"><span data-stu-id="6fca2-109">What is the SendGrid Email Service?</span></span>
<span data-ttu-id="6fca2-110">SendGrid è un [servizio di posta elettronica basato sul cloud] che offre [recapito affidabile di messaggi di posta elettronica transazionali], scalabilità e analisi in tempo reale, oltre ad API flessibili che agevolano l'integrazione personalizzata.</span><span class="sxs-lookup"><span data-stu-id="6fca2-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="6fca2-111">Gli scenari di utilizzo comuni di SendGrid includono:</span><span class="sxs-lookup"><span data-stu-id="6fca2-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="6fca2-112">Invio automatico di ricevute ai clienti</span><span class="sxs-lookup"><span data-stu-id="6fca2-112">Automatically sending receipts to customers</span></span>
* <span data-ttu-id="6fca2-113">Amministrazione di liste di distribuzione per l'invio mensile ai clienti di volantini elettronici e offerte speciali</span><span class="sxs-lookup"><span data-stu-id="6fca2-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="6fca2-114">Raccolta di metriche in tempo reale per elementi quali indirizzi di posta elettronica bloccati e velocità di risposta al cliente</span><span class="sxs-lookup"><span data-stu-id="6fca2-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="6fca2-115">Generazione di report per agevolare l'identificazione delle tendenze</span><span class="sxs-lookup"><span data-stu-id="6fca2-115">Generating reports to help identify trends</span></span>
* <span data-ttu-id="6fca2-116">Inoltro di richieste dei clienti</span><span class="sxs-lookup"><span data-stu-id="6fca2-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="6fca2-117">Notifiche di posta elettronica dall'applicazione</span><span class="sxs-lookup"><span data-stu-id="6fca2-117">Email notifications from your application</span></span>

<span data-ttu-id="6fca2-118">Per altre informazioni, vedere [https://sendgrid.com](https://sendgrid.com).</span><span class="sxs-lookup"><span data-stu-id="6fca2-118">For more information, see [https://sendgrid.com](https://sendgrid.com).</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="6fca2-119">Creazione di un account SendGrid</span><span class="sxs-lookup"><span data-stu-id="6fca2-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="reference-the-sendgrid-nodejs-module"></a><span data-ttu-id="6fca2-120">Riferimento al modulo SendGrid per Node.js</span><span class="sxs-lookup"><span data-stu-id="6fca2-120">Reference the SendGrid Node.js Module</span></span>
<span data-ttu-id="6fca2-121">Il modulo SendGrid per Node.js può essere installato con il programma di gestione dei pacchetti per Node.js (npm) usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6fca2-121">The SendGrid module for Node.js can be installed through the node package manager (npm) by using the following command:</span></span>

    npm install sendgrid

<span data-ttu-id="6fca2-122">Dopo l'installazione, è possibile includere il modulo nell'applicazione usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6fca2-122">After installation, you can require the module in your application by using the following code:</span></span>

    var sendgrid = require('sendgrid')(sendgrid_username, sendgrid_password);

<span data-ttu-id="6fca2-123">Il modulo SendGrid esporta le funzioni **SendGrid** ed **Email**.</span><span class="sxs-lookup"><span data-stu-id="6fca2-123">The SendGrid module exports the **SendGrid** and **Email** functions.</span></span>
<span data-ttu-id="6fca2-124">**SendGrid** è responsabile dell'invio di e-mail tramite API Web, mentre **Email** incapsula un'e-mail.</span><span class="sxs-lookup"><span data-stu-id="6fca2-124">**SendGrid** is responsible for sending email through Web API, while **Email** encapsulates an email message.</span></span>

## <a name="how-to-create-an-email"></a><span data-ttu-id="6fca2-125">Procedura: Creare un messaggio di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="6fca2-125">How to: Create an Email</span></span>
<span data-ttu-id="6fca2-126">Creare un messaggio di posta elettronica usando il modulo SendGrid è una procedura in due fasi. La prima consiste nel creare il messaggio usando la funzione Email, la seconda nell'inviarlo usando la funzione SendGrid.</span><span class="sxs-lookup"><span data-stu-id="6fca2-126">Creating an email message using the SendGrid module involves first creating an email message using the Email function, and then sending it using the SendGrid function.</span></span> <span data-ttu-id="6fca2-127">Di seguito è riportato un esempio di codice per la creazione di un nuovo messaggio mediante la funzione Email:</span><span class="sxs-lookup"><span data-stu-id="6fca2-127">The following is an example of creating a new message using the Email function:</span></span>

    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

<span data-ttu-id="6fca2-128">È inoltre possibile specificare un messaggio HTML per i client che li supportano, configurando la proprietà html.</span><span class="sxs-lookup"><span data-stu-id="6fca2-128">You can also specify an HTML message for clients that support it by setting the html property.</span></span> <span data-ttu-id="6fca2-129">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="6fca2-129">For example:</span></span>

    html: This is a sample <b>HTML<b> email message.

<span data-ttu-id="6fca2-130">Impostando sia la proprietà text che la proprietà html è possibile implementare il fallback graduale a contenuto testuale per i client che non supportano i messaggi HTML.</span><span class="sxs-lookup"><span data-stu-id="6fca2-130">Setting both the text and html properties provides graceful fallback to text content for clients that cannot support HTML messages.</span></span>

<span data-ttu-id="6fca2-131">Per ulteriori informazioni su tutte le proprietà supportate dalla funzione di posta elettronica, vedere [sendgrid nodejs][sendgrid-nodejs].</span><span class="sxs-lookup"><span data-stu-id="6fca2-131">For more information on all properties supported by the Email function, see [sendgrid-nodejs][sendgrid-nodejs].</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="6fca2-132">Procedura: Inviare un messaggio di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="6fca2-132">How to: Send an Email</span></span>
<span data-ttu-id="6fca2-133">Dopo aver creato un messaggio di posta elettronica usando la funzione Email, è possibile inviarlo tramite SMTP o con l'API Web fornita da SendGrid.</span><span class="sxs-lookup"><span data-stu-id="6fca2-133">After creating an email message using the Email function, you can send it using the Web API provided by SendGrid.</span></span> 

### <a name="web-api"></a><span data-ttu-id="6fca2-134">API Web</span><span class="sxs-lookup"><span data-stu-id="6fca2-134">Web API</span></span>
    sendgrid.send(email, function(err, json){
        if(err) { return console.error(err); }
        console.log(json);
    });

> [!NOTE]
> <span data-ttu-id="6fca2-135">Sebbene gli esempi precedenti illustrino il passaggio di un oggetto di posta elettronica e una funzione di richiamata, è inoltre possibile richiamare direttamente la funzione send specificando direttamente le proprietà dei messaggi di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="6fca2-135">While the above examples show passing in an email object and callback function, you can also directly invoke the send function by directly specifying email properties.</span></span> <span data-ttu-id="6fca2-136">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="6fca2-136">For example:</span></span>  
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

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="6fca2-137">Procedura: Aggiungere un allegato</span><span class="sxs-lookup"><span data-stu-id="6fca2-137">How to: Add an Attachment</span></span>
<span data-ttu-id="6fca2-138">Per aggiungere allegati a un messaggio, specificare i nomi e i percorsi dei file nella proprietà **files**.</span><span class="sxs-lookup"><span data-stu-id="6fca2-138">Attachments can be added to a message by specifying the file name(s) and path(s) in the **files** property.</span></span> <span data-ttu-id="6fca2-139">Nell'esempio seguente viene illustrato l'invio di un allegato:</span><span class="sxs-lookup"><span data-stu-id="6fca2-139">The following example demonstrates sending an attachment:</span></span>

    sendgrid.send({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.',
        files: [
            {
                filename:     '',           // required only if file.content is used.
                contentType:  '',           // optional
                cid:          '',           // optional, used to specify cid for inline content
                path:         '',           //
                url:          '',           // == One of these three options is required
                content:      ('' | Buffer) //
            }
        ],
    });

> [!NOTE]
> <span data-ttu-id="6fca2-140">Quando si usa la proprietà **files**, il file deve essere accessibile tramite [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile).</span><span class="sxs-lookup"><span data-stu-id="6fca2-140">When using the **files** property, the file must be accessible through [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile).</span></span> <span data-ttu-id="6fca2-141">Se il file da allegare è ospitato in Archiviazione di Azure, ad esempio in un contenitore BLOB, prima di poterlo inviare come allegato usando la proprietà **files** è necessario copiarlo nell'archiviazione locale o in un'unità Azure.</span><span class="sxs-lookup"><span data-stu-id="6fca2-141">If the file you wish to attach is hosted in Azure Storage, such as in a Blob container, you must first copy the file to local storage or to an Azure drive before it can be sent as an attachment using the **files** property.</span></span>
> 
> 

## <a name="how-to-use-filters-to-enable-footers-and-tracking"></a><span data-ttu-id="6fca2-142">Procedura: Usare filtri per abilitare piè di pagina e monitoraggio</span><span class="sxs-lookup"><span data-stu-id="6fca2-142">How to: Use Filters to Enable Footers and Tracking</span></span>
<span data-ttu-id="6fca2-143">SendGrid fornisce funzionalità di posta elettronica aggiuntive attraverso l'uso di filtri.</span><span class="sxs-lookup"><span data-stu-id="6fca2-143">SendGrid provides additional email functionality through the use of filters.</span></span> <span data-ttu-id="6fca2-144">Si tratta di impostazioni che è possibile aggiungere a un messaggio di posta elettronica per abilitare funzionalità specifiche, ad esempio il monitoraggio del clic, Google Analytics, il monitoraggio delle sottoscrizioni e così via.</span><span class="sxs-lookup"><span data-stu-id="6fca2-144">These are settings that can be added to an email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="6fca2-145">Per un elenco completo dei filtri, vedere le [impostazioni dei filtri][Filter Settings].</span><span class="sxs-lookup"><span data-stu-id="6fca2-145">For a full list of filters, see [Filter Settings][Filter Settings].</span></span>

<span data-ttu-id="6fca2-146">È possibile applicare filtri a un messaggio usando la proprietà **filters**.</span><span class="sxs-lookup"><span data-stu-id="6fca2-146">Filters can be applied to a message by using the **filters** property.</span></span>
<span data-ttu-id="6fca2-147">Ogni filtro è specificato da un hash che contiene impostazioni specifiche del filtro.</span><span class="sxs-lookup"><span data-stu-id="6fca2-147">Each filter is specified by a hash containing filter-specific settings.</span></span>
<span data-ttu-id="6fca2-148">Negli esempi seguenti vengono illustrati i filtri per abilitare il piè di pagina e per il monitoraggio dei clic:</span><span class="sxs-lookup"><span data-stu-id="6fca2-148">The following examples demonstrate the footer and click tracking filters:</span></span>

### <a name="footer"></a><span data-ttu-id="6fca2-149">Piè di pagina</span><span class="sxs-lookup"><span data-stu-id="6fca2-149">Footer</span></span>
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

### <a name="click-tracking"></a><span data-ttu-id="6fca2-150">Monitoraggio dei clic</span><span class="sxs-lookup"><span data-stu-id="6fca2-150">Click Tracking</span></span>
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

## <a name="how-to-update-email-properties"></a><span data-ttu-id="6fca2-151">Procedura: Aggiornare le proprietà dei messaggi di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="6fca2-151">How to: Update Email Properties</span></span>
<span data-ttu-id="6fca2-152">Alcune proprietà del messaggio di posta elettronica può essere sovrascritto usando  **impostare*proprietà** * o aggiunti utilizzando  **aggiungere*proprietà** *.</span><span class="sxs-lookup"><span data-stu-id="6fca2-152">Some email properties can be overwritten using **set*Property*** or appended using **add*Property***.</span></span> <span data-ttu-id="6fca2-153">Ad esempio, è possibile aggiungere altri destinatari usando</span><span class="sxs-lookup"><span data-stu-id="6fca2-153">For example, you can add additional recipients by using</span></span>

    email.addTo('jeff@contoso.com');

<span data-ttu-id="6fca2-154">oppure impostare un filtro utilizzando</span><span class="sxs-lookup"><span data-stu-id="6fca2-154">or set a filter by using</span></span>

    email.addFilter('footer', 'enable', 1);
    email.addFilter('footer', 'text/html', '<strong>boo</strong>');

<span data-ttu-id="6fca2-155">Per ulteriori informazioni, vedere [sendgrid nodejs][sendgrid-nodejs].</span><span class="sxs-lookup"><span data-stu-id="6fca2-155">For more information, see [sendgrid-nodejs][sendgrid-nodejs].</span></span>

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="6fca2-156">Procedura: Usare servizi aggiuntivi forniti da SendGrid</span><span class="sxs-lookup"><span data-stu-id="6fca2-156">How to: Use Additional SendGrid Services</span></span>
<span data-ttu-id="6fca2-157">SendGrid offre API basate sul Web che è possibile usare per sfruttare altre funzionalità di SendGrid dall'applicazione Azure.</span><span class="sxs-lookup"><span data-stu-id="6fca2-157">SendGrid offers web-based APIs that you can use to leverage additional SendGrid functionality from your Azure application.</span></span> <span data-ttu-id="6fca2-158">Per informazioni dettagliate, vedere la [documentazione sull'API SendGrid][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="6fca2-158">For full details, see the [SendGrid API documentation][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="6fca2-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6fca2-159">Next Steps</span></span>
<span data-ttu-id="6fca2-160">A questo punto, dopo aver appreso le nozioni di base del servizio di posta elettronica SendGrid, usare i collegamenti seguenti per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="6fca2-160">Now that you've learned the basics of the SendGrid Email service, follow these links to learn more.</span></span>

* <span data-ttu-id="6fca2-161">Repository di moduli SendGrid Node.js: [sendgrid nodejs][sendgrid-nodejs]</span><span class="sxs-lookup"><span data-stu-id="6fca2-161">SendGrid Node.js module repository: [sendgrid-nodejs][sendgrid-nodejs]</span></span>
* <span data-ttu-id="6fca2-162">Documentazione relativa all'API SendGrid: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="6fca2-162">SendGrid API documentation: <https://sendgrid.com/docs></span></span>
* <span data-ttu-id="6fca2-163">Offerta speciale SendGrid per i clienti di Azure: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)</span><span class="sxs-lookup"><span data-stu-id="6fca2-163">SendGrid special offer for Azure customers: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)</span></span>

[special offer]: https://sendgrid.com/windowsazure.html
[sendgrid-nodejs]: https://github.com/sendgrid/sendgrid-nodejs
[Filter Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs
<span data-ttu-id="6fca2-164">[servizio di posta elettronica basato sul cloud]: https://sendgrid.com/email-solutions</span><span class="sxs-lookup"><span data-stu-id="6fca2-164">[cloud-based email service]: https://sendgrid.com/email-solutions</span></span>
<span data-ttu-id="6fca2-165">[recapito affidabile di messaggi di posta elettronica transazionali]: https://sendgrid.com/transactional-email</span><span class="sxs-lookup"><span data-stu-id="6fca2-165">[transactional email delivery]: https://sendgrid.com/transactional-email</span></span>
