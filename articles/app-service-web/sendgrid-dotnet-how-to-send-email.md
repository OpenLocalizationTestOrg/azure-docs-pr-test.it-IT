---
title: Come usare il servizio e-mail SendGrid (.NET) | Microsoft Docs
description: Informazioni su come inviare messaggi di posta elettronica con il servizio di posta elettronica SendGrid disponibile in Azure. Gli esempi di codice sono scritti in C# mediante l'API .NET.
services: app-service-web
documentationcenter: .net
author: thinkingserious
manager: erikre
editor: 
ms.assetid: 21bf4028-9046-476b-9799-3d3082a0f84c
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/15/2017
ms.author: dx@sendgrid.com
ms.openlocfilehash: b3a48b3c838763b022a18e55817ec7455fe94c85
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-send-email-using-sendgrid-with-azure"></a><span data-ttu-id="54939-104">Come inviare messaggi di posta elettronica usando SendGrid con Azure</span><span class="sxs-lookup"><span data-stu-id="54939-104">How to Send Email Using SendGrid with Azure</span></span>
## <a name="overview"></a><span data-ttu-id="54939-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="54939-105">Overview</span></span>
<span data-ttu-id="54939-106">Questa guida illustra come eseguire attività di programmazione comuni con il servizio di posta elettronica SendGrid in Azure.</span><span class="sxs-lookup"><span data-stu-id="54939-106">This guide demonstrates how to perform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="54939-107">Gli esempi sono scritti in C\# e supportano .NET Standard 1.3.</span><span class="sxs-lookup"><span data-stu-id="54939-107">The samples are written in C\# and supports .NET Standard 1.3.</span></span> <span data-ttu-id="54939-108">Gli scenari presentati includono la creazione e l'invio di messaggi di posta elettronica, l'aggiunta di allegati e l'abilitazione di diverse impostazioni di posta elettronica e rilevamento.</span><span class="sxs-lookup"><span data-stu-id="54939-108">The scenarios covered include constructing email, sending email, adding attachments, and enabling various mail and tracking settings.</span></span> <span data-ttu-id="54939-109">Per altre informazioni su SendGrid e sull'invio di email vedere la sezione [Passaggi successivi][Next steps].</span><span class="sxs-lookup"><span data-stu-id="54939-109">For more information on SendGrid and sending email, see the [Next steps][Next steps] section.</span></span>

## <a name="what-is-the-sendgrid-email-service"></a><span data-ttu-id="54939-110">Informazioni sul servizio di posta elettronica SendGrid</span><span class="sxs-lookup"><span data-stu-id="54939-110">What is the SendGrid Email Service?</span></span>
<span data-ttu-id="54939-111">SendGrid è un [servizio di posta elettronica basato sul cloud] che offre [recapito affidabile di messaggi di posta elettronica transazionali], scalabilità e analisi in tempo reale, oltre ad API flessibili che agevolano l'integrazione personalizzata.</span><span class="sxs-lookup"><span data-stu-id="54939-111">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="54939-112">I casi d'uso comuni di SendGrid includono:</span><span class="sxs-lookup"><span data-stu-id="54939-112">Common SendGrid use cases include:</span></span>

* <span data-ttu-id="54939-113">Invio automatico di ricevute o conferme di acquisto ai clienti.</span><span class="sxs-lookup"><span data-stu-id="54939-113">Automatically sending receipts or purchase confirmations to customers.</span></span>
* <span data-ttu-id="54939-114">Amministrazione di liste di distribuzione per inviare mensilmente volantini e promozioni ai clienti.</span><span class="sxs-lookup"><span data-stu-id="54939-114">Administering distribution lists for sending customers monthly fliers and promotions.</span></span>
* <span data-ttu-id="54939-115">Raccolta di metriche in tempo reale per elementi quali email bloccate ed engagement del cliente.</span><span class="sxs-lookup"><span data-stu-id="54939-115">Collecting real-time metrics for things like blocked email and customer engagement.</span></span>
* <span data-ttu-id="54939-116">Inoltro di richieste dei clienti.</span><span class="sxs-lookup"><span data-stu-id="54939-116">Forwarding customer inquiries.</span></span>
* <span data-ttu-id="54939-117">Elaborazione di messaggi di posta elettronica in arrivo.</span><span class="sxs-lookup"><span data-stu-id="54939-117">Processing incoming emails.</span></span>

<span data-ttu-id="54939-118">Per altre informazioni visitare [https://sendgrid.com](https://sendgrid.com) o la [libreria C#][sendgrid-csharp] di SendGrid nel repository GitHub.</span><span class="sxs-lookup"><span data-stu-id="54939-118">For more information, visit [https://sendgrid.com](https://sendgrid.com) or SendGrid's [C# library][sendgrid-csharp] GitHub repo.</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="54939-119">Creazione di un account SendGrid</span><span class="sxs-lookup"><span data-stu-id="54939-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../../includes/sendgrid-sign-up.md)]

## <a name="reference-the-sendgrid-net-class-library"></a><span data-ttu-id="54939-120">Fare riferimento alla libreria di classi .NET di SendGrid</span><span class="sxs-lookup"><span data-stu-id="54939-120">Reference the SendGrid .NET Class Library</span></span>
<span data-ttu-id="54939-121">Il [pacchetto NuGet di SendGrid](https://www.nuget.org/packages/Sendgrid) è il modo più semplice per recuperare l'API SendGrid e configurare l'applicazione con tutte le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="54939-121">The [SendGrid NuGet package](https://www.nuget.org/packages/Sendgrid) is the easiest way to get the SendGrid API and to configure your application with all dependencies.</span></span> <span data-ttu-id="54939-122">NuGet è un'estensione di Visual Studio inclusa in Microsoft Visual Studio 2015 e versioni successive che semplifica l'installazione e l'aggiornamento di librerie e strumenti.</span><span class="sxs-lookup"><span data-stu-id="54939-122">NuGet is a Visual Studio extension included with Microsoft Visual Studio 2015 and above that makes it easy to install and update libraries and tools.</span></span>

> [!NOTE]
> <span data-ttu-id="54939-123">Per installare NuGet se si esegue una versione di Visual Studio precedente rispetto a Visual Studio 2015, visitare il sito [http://www.nuget.org](http://www.nuget.org)e fare clic su **Install NuGet** .</span><span class="sxs-lookup"><span data-stu-id="54939-123">To install NuGet if you are running a version of Visual Studio earlier than Visual Studio 2015, visit [http://www.nuget.org](http://www.nuget.org), and click the **Install NuGet** button.</span></span>
>
>

<span data-ttu-id="54939-124">Per installare il pacchetto NuGet di SendGrid, eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="54939-124">To install the SendGrid NuGet package in your application, do the following:</span></span>

1. <span data-ttu-id="54939-125">Fare clic su **Nuovo progetto** e selezionare un **modello**.</span><span class="sxs-lookup"><span data-stu-id="54939-125">Click on **New Project** and select a **Template**.</span></span>

   ![Creare un nuovo progetto][create-new-project]
2. <span data-ttu-id="54939-127">In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Riferimenti** e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="54939-127">In **Solution Explorer**, right-click **References**, then click **Manage NuGet Packages**.</span></span>

   ![pacchetto NuGet di SendGrid][SendGrid-NuGet-package]
3. <span data-ttu-id="54939-129">Cercare **SendGrid** e selezionare la voce **SendGrid** nell'elenco dei risultati.</span><span class="sxs-lookup"><span data-stu-id="54939-129">Search for **SendGrid** and select the **SendGrid** item in the results list.</span></span>
4. <span data-ttu-id="54939-130">Selezionare la più recente versione stabile del pacchetto NuGet nell'elenco a discesa della versione per poter usare il modello a oggetti e le API indicati in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="54939-130">Select the latest stable version of the Nuget package from the version dropdown to be able to work with the object model and APIs demonstrated in this article.</span></span>

   ![Pacchetto SendGrid][sendgrid-package]
5. <span data-ttu-id="54939-132">Fare clic su **Installa** per completare l'installazione, quindi chiudere questa finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="54939-132">Click **Install** to complete the installation, and then close this dialog.</span></span>

<span data-ttu-id="54939-133">La libreria della classe .NET di SendGrid è denominata **SendGrid**.</span><span class="sxs-lookup"><span data-stu-id="54939-133">SendGrid's .NET class library is called **SendGrid**.</span></span> <span data-ttu-id="54939-134">Include gli spazi dei nomi seguenti:</span><span class="sxs-lookup"><span data-stu-id="54939-134">It contains the following namespaces:</span></span>

* <span data-ttu-id="54939-135">**SendGrid** per la comunicazione con l'API di SendGrid.</span><span class="sxs-lookup"><span data-stu-id="54939-135">**SendGrid** for communicating with SendGrid’s API.</span></span>
* <span data-ttu-id="54939-136">**SendGrid.Helpers.Mail** per i metodi helper per creare facilmente oggetti SendGridMessage che specificano come inviare email.</span><span class="sxs-lookup"><span data-stu-id="54939-136">**SendGrid.Helpers.Mail** for helper methods to easily create SendGridMessage objects that specify how to send emails.</span></span>

<span data-ttu-id="54939-137">Aggiungere le seguenti dichiarazioni dello spazio dei nomi del codice all'inizio del file C# in cui si desidera accedere al servizio di posta elettronica SendGrid a livello di codice:</span><span class="sxs-lookup"><span data-stu-id="54939-137">Add the following code namespace declarations to the top of any C# file in which you want to programmatically access the SendGrid email service.</span></span>

    using SendGrid;
    using SendGrid.Helpers.Mail;

## <a name="how-to-create-an-email"></a><span data-ttu-id="54939-138">Procedura: Creare un messaggio di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="54939-138">How to: Create an Email</span></span>
<span data-ttu-id="54939-139">Usare l'oggetto **SendGridMessage** per creare un messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="54939-139">Use the **SendGridMessage** object to create an email message.</span></span> <span data-ttu-id="54939-140">Dopo aver creato l'oggetto, è possibile impostare proprietà e metodi, inclusi il mittente, il destinatario, l'oggetto e il corpo del messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="54939-140">Once the message object is created, you can set properties and methods, including the email sender, the email recipient, and the subject and body of the email.</span></span>

<span data-ttu-id="54939-141">Nell'esempio seguente viene illustrato come creare un oggetto di posta elettronica completamente popolato:</span><span class="sxs-lookup"><span data-stu-id="54939-141">The following example demonstrates how to create a fully populated email object:</span></span>

    var msg = new SendGridMessage();

    msg.SetFrom(new EmailAddress("dx@example.com", "SendGrid DX Team"));

    var recipients = new List<EmailAddress>
    {
        new EmailAddress("jeff@example.com", "Jeff Smith"),
        new EmailAddress("anna@example.com", "Anna Lidman"),
        new EmailAddress("peter@example.com", "Peter Saddow")
    };
    msg.AddTos(recipients);

    msg.SetSubject("Testing the SendGrid C# Library");

    msg.AddContent(MimeType.Text, "Hello World plain text!");
    msg.AddContent(MimeType.Html, "<p>Hello World!</p>");

<span data-ttu-id="54939-142">Per altre informazioni su tutte le proprietà e i metodi supportati dal tipo **SendGrid**, vedere [sendgrid-csharp][sendgrid-csharp] in GitHub.</span><span class="sxs-lookup"><span data-stu-id="54939-142">For more information on all properties and methods supported by the **SendGrid** type, see [sendgrid-csharp][sendgrid-csharp] on GitHub.</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="54939-143">Procedura: Inviare un messaggio di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="54939-143">How to: Send an Email</span></span>
<span data-ttu-id="54939-144">Dopo aver creato un'email, è possibile inviarla tramite l'API di SendGrid.</span><span class="sxs-lookup"><span data-stu-id="54939-144">After creating an email message, you can send it using SendGrid's API.</span></span> <span data-ttu-id="54939-145">In alternativa è possibile usare la [libreria integrata di .NET][NET-library].</span><span class="sxs-lookup"><span data-stu-id="54939-145">Alternatively, you may use [.NET's built in library][NET-library].</span></span>

<span data-ttu-id="54939-146">Per inviare email, è necessario specificare la chiave API di SendGrid.</span><span class="sxs-lookup"><span data-stu-id="54939-146">Sending email requires that you supply your SendGrid API Key.</span></span> <span data-ttu-id="54939-147">Per informazioni dettagliate su come configurare le chiavi API, consultare la [documentazione][documentation] sulle chiavi API di SendGrid.</span><span class="sxs-lookup"><span data-stu-id="54939-147">If you need details about how to configure API Keys, please visit SendGrid's API Keys [documentation][documentation].</span></span>

<span data-ttu-id="54939-148">È possibile archiviare queste credenziali tramite il portale di Azure facendo clic su Impostazioni applicazione e aggiungendo le coppie chiave-valore nella sezione Impostazioni app.</span><span class="sxs-lookup"><span data-stu-id="54939-148">You may store these credentials via your Azure Portal by clicking Application settings and adding the key/value pairs under App settings.</span></span>

 ![Impostazioni app di Azure][azure_app_settings]

 <span data-ttu-id="54939-150">Quindi, è possibile accedervi come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="54939-150">Then, you may access them as follows:</span></span>

    var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
    var client = new SendGridClient(apiKey);

<span data-ttu-id="54939-151">Gli esempi seguenti mostrano come inviare un messaggio con l'API Web.</span><span class="sxs-lookup"><span data-stu-id="54939-151">The following examples show how to send a message using the Web API.</span></span>

    using System;
    using System.Threading.Tasks;
    using SendGrid;
    using SendGrid.Helpers.Mail;

    namespace Example
    {
        internal class Example
        {
            private static void Main()
            {
                Execute().Wait();
            }

            static async Task Execute()
            {
                var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
                var client = new SendGridClient(apiKey);
                var msg = new SendGridMessage()
                {
                    From = new EmailAddress("test@example.com", "DX Team"),
                    Subject = "Hello World from the SendGrid CSharp SDK!",
                    PlainTextContent = "Hello, Email!",
                    HtmlContent = "<strong>Hello, Email!</strong>"
                };
                msg.AddTo(new EmailAddress("test@example.com", "Test User"));
                var response = await client.SendEmailAsync(msg);
            }
        }
    }

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="54939-152">Procedura: Aggiungere un allegato</span><span class="sxs-lookup"><span data-stu-id="54939-152">How to: Add an attachment</span></span>
<span data-ttu-id="54939-153">Per aggiungere allegati a un messaggio, chiamare il metodo **AddAttachment** e specificare almeno il nome del file e il contenuto con codifica Base64 da allegare.</span><span class="sxs-lookup"><span data-stu-id="54939-153">Attachments can be added to a message by calling the **AddAttachment** method and minimally specifying the file name and Base64 encoded content you want to attach.</span></span> <span data-ttu-id="54939-154">È possibile includere più allegati chiamando questo metodo una volta per ogni file che si desidera allegare o usando il metodo **AddAttachments**.</span><span class="sxs-lookup"><span data-stu-id="54939-154">You can include multiple attachments by calling this method once for each file you wish to attach or by using the **AddAttachments** method.</span></span> <span data-ttu-id="54939-155">Nell'esempio seguente viene illustrata l'aggiunta di un allegato a un messaggio:</span><span class="sxs-lookup"><span data-stu-id="54939-155">The following example demonstrates adding an attachment to a message:</span></span>

    var banner2 = new Attachment()
    {
        Content = Convert.ToBase64String(raw_content),
        Type = "image/png",
        Filename = "banner2.png",
        Disposition = "inline",
        ContentId = "Banner 2"
    };
    msg.AddAttachment(banner2);

## <a name="how-to-use-mail-settings-to-enable-footers-tracking-and-analytics"></a><span data-ttu-id="54939-156">Procedura: Usare le impostazioni della posta elettronica per abilitare piè di pagina, rilevamento e analisi</span><span class="sxs-lookup"><span data-stu-id="54939-156">How to: Use mail settings to enable footers, tracking, and analytics</span></span>
<span data-ttu-id="54939-157">SendGrid offre funzionalità email aggiuntive tramite l'uso di impostazioni della posta elettronica e di rilevamento.</span><span class="sxs-lookup"><span data-stu-id="54939-157">SendGrid provides additional email functionality through the use of mail settings and tracking settings.</span></span> <span data-ttu-id="54939-158">Si tratta di impostazioni che è possibile aggiungere a un' email per abilitare funzionalità specifiche come il rilevamento dei clic, Google Analytics, il rilevamento delle sottoscrizioni e così via.</span><span class="sxs-lookup"><span data-stu-id="54939-158">These settings can be added to an email message to enable specific functionality such as click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="54939-159">Per un elenco completo delle app, vedere la [documentazione sulle impostazioni][settings-documentation].</span><span class="sxs-lookup"><span data-stu-id="54939-159">For a full list of apps, see the [Settings Documentation][settings-documentation].</span></span>

<span data-ttu-id="54939-160">Per applicare le app alle email di **SendGrid**, usare i metodi implementati come parte della classe **SendGridMessage**.</span><span class="sxs-lookup"><span data-stu-id="54939-160">Apps can be applied to **SendGrid** email messages using methods implemented as part of the **SendGridMessage** class.</span></span> <span data-ttu-id="54939-161">Negli esempi seguenti vengono illustrati i filtri per abilitare il piè di pagina e per il monitoraggio dei clic:</span><span class="sxs-lookup"><span data-stu-id="54939-161">The following examples demonstrate the footer and click tracking filters:</span></span>

<span data-ttu-id="54939-162">Negli esempi seguenti vengono illustrati i filtri per abilitare il piè di pagina e per il monitoraggio dei clic:</span><span class="sxs-lookup"><span data-stu-id="54939-162">The following examples demonstrate the footer and click tracking filters:</span></span>

### <a name="footer-settings"></a><span data-ttu-id="54939-163">Impostazioni del piè di pagina</span><span class="sxs-lookup"><span data-stu-id="54939-163">Footer settings</span></span>
    msg.SetFooterSetting(
                         true,
                         "Some Footer HTML",
                         "<strong>Some Footer Text</strong>");

### <a name="click-tracking"></a><span data-ttu-id="54939-164">Monitoraggio dei clic</span><span class="sxs-lookup"><span data-stu-id="54939-164">Click tracking</span></span>
    msg.SetClickTracking(true);

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="54939-165">Procedura: Usare servizi aggiuntivi forniti da SendGrid</span><span class="sxs-lookup"><span data-stu-id="54939-165">How to: Use Additional SendGrid Services</span></span>
<span data-ttu-id="54939-166">SendGrid offre diverse API e webhook che si possono usare per sfruttare altre funzionalità dell'applicazione Azure.</span><span class="sxs-lookup"><span data-stu-id="54939-166">SendGrid offers several APIs and webhooks that you can use to leverage additional functionality within your Azure application.</span></span> <span data-ttu-id="54939-167">Per maggiori dettagli, vedere il [riferimento all'API SendGrid][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="54939-167">For more details, see the [SendGrid API Reference][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="54939-168">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="54939-168">Next steps</span></span>
<span data-ttu-id="54939-169">A questo punto, dopo aver appreso le nozioni di base del servizio di posta elettronica SendGrid, usare i collegamenti seguenti per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="54939-169">Now that you've learned the basics of the SendGrid Email service, follow these links to learn more.</span></span>

* <span data-ttu-id="54939-170">Repository della libreria C\# di SendGrid: [sendgrid-csharp][sendgrid-csharp]</span><span class="sxs-lookup"><span data-stu-id="54939-170">SendGrid C\# library repo: [sendgrid-csharp][sendgrid-csharp]</span></span>
* <span data-ttu-id="54939-171">Documentazione relativa all'API SendGrid: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="54939-171">SendGrid API documentation: <https://sendgrid.com/docs></span></span>

[Next steps]: #next-steps
[What is the SendGrid Email Service?]: #whatis
[Create a SendGrid Account]: #createaccount
[Reference the SendGrid .NET Class Library]: #reference
[How to: Create an Email]: #createemail
[How to: Send an Email]: #sendemail
[How to: Add an Attachment]: #addattachment
[How to: Use Filters to Enable Footers, Tracking, and Analytics]: #usefilters
[How to: Use Additional SendGrid Services]: #useservices

[create-new-project]: ./media/sendgrid-dotnet-how-to-send-email/new-project.png
[SendGrid-NuGet-package]: ./media/sendgrid-dotnet-how-to-send-email/reference.png
[sendgrid-package]: ./media/sendgrid-dotnet-how-to-send-email/sendgrid-package.png
[azure_app_settings]: ./media/sendgrid-dotnet-how-to-send-email/azure-app-settings.png
[sendgrid-csharp]: https://github.com/sendgrid/sendgrid-csharp
[SMTP vs. Web API]: https://sendgrid.com/docs/Integrate/index.html
[App Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs/API_Reference/api_v3.html
[NET-library]: https://sendgrid.com/docs/Integrate/Code_Examples/v2_Mail/csharp.html#-Using-NETs-Builtin-SMTP-Library
[documentation]: https://sendgrid.com/docs/Classroom/Send/api_keys.html
[settings-documentation]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html

<span data-ttu-id="54939-172">[servizio di posta elettronica basato sul cloud]: https://sendgrid.com/solutions</span><span class="sxs-lookup"><span data-stu-id="54939-172">[cloud-based email service]: https://sendgrid.com/solutions</span></span>
<span data-ttu-id="54939-173">[recapito affidabile di messaggi di posta elettronica transazionali]: https://sendgrid.com/use-cases/transactional-email</span><span class="sxs-lookup"><span data-stu-id="54939-173">[transactional email delivery]: https://sendgrid.com/use-cases/transactional-email</span></span>

