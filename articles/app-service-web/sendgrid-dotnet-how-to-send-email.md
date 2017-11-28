---
title: hello toouse aaaHow SendGrid servizio di posta elettronica (.NET) | Documenti Microsoft
description: Informazioni su come inviare posta elettronica con il servizio di posta elettronica SendGrid hello in Azure. Esempi di codice scritti in c# e utilizzare hello API .NET.
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
ms.openlocfilehash: b3d77bb67898b991c7293e6b9086b263f6bcb755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-with-azure"></a><span data-ttu-id="89b4b-104">Come tooSend SendGrid tramite posta elettronica con Azure</span><span class="sxs-lookup"><span data-stu-id="89b4b-104">How tooSend Email Using SendGrid with Azure</span></span>
## <a name="overview"></a><span data-ttu-id="89b4b-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="89b4b-105">Overview</span></span>
<span data-ttu-id="89b4b-106">Questa guida illustra come tooperform attività di programmazione comuni con di SendGrid tramite posta elettronica del servizio in Azure.</span><span class="sxs-lookup"><span data-stu-id="89b4b-106">This guide demonstrates how tooperform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="89b4b-107">Hello esempi sono scritti in C\# e supporta .NET Standard 1.3.</span><span class="sxs-lookup"><span data-stu-id="89b4b-107">hello samples are written in C\# and supports .NET Standard 1.3.</span></span> <span data-ttu-id="89b4b-108">scenari di Hello trattati includono la costruzione di posta elettronica, l'invio di posta elettronica, l'aggiunta di allegati e l'abilitazione di posta elettronica diversi e impostazioni di verifica.</span><span class="sxs-lookup"><span data-stu-id="89b4b-108">hello scenarios covered include constructing email, sending email, adding attachments, and enabling various mail and tracking settings.</span></span> <span data-ttu-id="89b4b-109">Per ulteriori informazioni su SendGrid e l'invio di posta elettronica, vedere hello [passaggi successivi] [ Next steps] sezione.</span><span class="sxs-lookup"><span data-stu-id="89b4b-109">For more information on SendGrid and sending email, see hello [Next steps][Next steps] section.</span></span>

## <a name="what-is-hello-sendgrid-email-service"></a><span data-ttu-id="89b4b-110">Che cos'è il servizio di posta elettronica SendGrid hello?</span><span class="sxs-lookup"><span data-stu-id="89b4b-110">What is hello SendGrid Email Service?</span></span>
<span data-ttu-id="89b4b-111">SendGrid è un [servizio di posta elettronica basato sul cloud] che offre [recapito affidabile di messaggi di posta elettronica transazionali], scalabilità e analisi in tempo reale, oltre ad API flessibili che agevolano l'integrazione personalizzata.</span><span class="sxs-lookup"><span data-stu-id="89b4b-111">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="89b4b-112">I casi d'uso comuni di SendGrid includono:</span><span class="sxs-lookup"><span data-stu-id="89b4b-112">Common SendGrid use cases include:</span></span>

* <span data-ttu-id="89b4b-113">Automaticamente l'invio di conferme di recapito o toocustomers conferme di acquisto.</span><span class="sxs-lookup"><span data-stu-id="89b4b-113">Automatically sending receipts or purchase confirmations toocustomers.</span></span>
* <span data-ttu-id="89b4b-114">Amministrazione di liste di distribuzione per inviare mensilmente volantini e promozioni ai clienti.</span><span class="sxs-lookup"><span data-stu-id="89b4b-114">Administering distribution lists for sending customers monthly fliers and promotions.</span></span>
* <span data-ttu-id="89b4b-115">Raccolta di metriche in tempo reale per elementi quali email bloccate ed engagement del cliente.</span><span class="sxs-lookup"><span data-stu-id="89b4b-115">Collecting real-time metrics for things like blocked email and customer engagement.</span></span>
* <span data-ttu-id="89b4b-116">Inoltro di richieste dei clienti.</span><span class="sxs-lookup"><span data-stu-id="89b4b-116">Forwarding customer inquiries.</span></span>
* <span data-ttu-id="89b4b-117">Elaborazione di messaggi di posta elettronica in arrivo.</span><span class="sxs-lookup"><span data-stu-id="89b4b-117">Processing incoming emails.</span></span>

<span data-ttu-id="89b4b-118">Per altre informazioni visitare [https://sendgrid.com](https://sendgrid.com) o la [libreria C#][sendgrid-csharp] di SendGrid nel repository GitHub.</span><span class="sxs-lookup"><span data-stu-id="89b4b-118">For more information, visit [https://sendgrid.com](https://sendgrid.com) or SendGrid's [C# library][sendgrid-csharp] GitHub repo.</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="89b4b-119">Creazione di un account SendGrid</span><span class="sxs-lookup"><span data-stu-id="89b4b-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-net-class-library"></a><span data-ttu-id="89b4b-120">Fare riferimento a hello libreria di classi .NET SendGrid</span><span class="sxs-lookup"><span data-stu-id="89b4b-120">Reference hello SendGrid .NET Class Library</span></span>
<span data-ttu-id="89b4b-121">Hello [il pacchetto SendGrid NuGet](https://www.nuget.org/packages/Sendgrid) è hello più semplice modo tooget hello API SendGrid e tooconfigure l'applicazione con tutte le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="89b4b-121">hello [SendGrid NuGet package](https://www.nuget.org/packages/Sendgrid) is hello easiest way tooget hello SendGrid API and tooconfigure your application with all dependencies.</span></span> <span data-ttu-id="89b4b-122">NuGet è un estensione inclusi con Microsoft Visual Studio 2015 e versioni successive che rende facile tooinstall e aggiornamento di librerie e strumenti di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="89b4b-122">NuGet is a Visual Studio extension included with Microsoft Visual Studio 2015 and above that makes it easy tooinstall and update libraries and tools.</span></span>

> [!NOTE]
> <span data-ttu-id="89b4b-123">tooinstall NuGet se si esegue una versione di Visual Studio precedenti a Visual Studio 2015, visitare [http://www.nuget.org](http://www.nuget.org), fare clic su hello **installare NuGet** pulsante.</span><span class="sxs-lookup"><span data-stu-id="89b4b-123">tooinstall NuGet if you are running a version of Visual Studio earlier than Visual Studio 2015, visit [http://www.nuget.org](http://www.nuget.org), and click hello **Install NuGet** button.</span></span>
>
>

<span data-ttu-id="89b4b-124">hello tooinstall nell'applicazione, il pacchetto SendGrid NuGet hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="89b4b-124">tooinstall hello SendGrid NuGet package in your application, do hello following:</span></span>

1. <span data-ttu-id="89b4b-125">Fare clic su **Nuovo progetto** e selezionare un **modello**.</span><span class="sxs-lookup"><span data-stu-id="89b4b-125">Click on **New Project** and select a **Template**.</span></span>

   ![Creare un nuovo progetto][create-new-project]
2. <span data-ttu-id="89b4b-127">In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Riferimenti** e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="89b4b-127">In **Solution Explorer**, right-click **References**, then click **Manage NuGet Packages**.</span></span>

   ![pacchetto NuGet di SendGrid][SendGrid-NuGet-package]
3. <span data-ttu-id="89b4b-129">Cercare **SendGrid** e seleziona hello **SendGrid** elemento nell'elenco dei risultati.</span><span class="sxs-lookup"><span data-stu-id="89b4b-129">Search for **SendGrid** and select hello **SendGrid** item in the results list.</span></span>
4. <span data-ttu-id="89b4b-130">Selezionare versione stabile più recente di hello del pacchetto Nuget hello hello versione elenco a discesa toobe in grado di toowork con modello a oggetti hello e API illustrate in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="89b4b-130">Select hello latest stable version of hello Nuget package from hello version dropdown toobe able toowork with hello object model and APIs demonstrated in this article.</span></span>

   ![Pacchetto SendGrid][sendgrid-package]
5. <span data-ttu-id="89b4b-132">Fare clic su **installare** toocomplete hello installazione e quindi chiudere questa finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="89b4b-132">Click **Install** toocomplete hello installation, and then close this dialog.</span></span>

<span data-ttu-id="89b4b-133">La libreria della classe .NET di SendGrid è denominata **SendGrid**.</span><span class="sxs-lookup"><span data-stu-id="89b4b-133">SendGrid's .NET class library is called **SendGrid**.</span></span> <span data-ttu-id="89b4b-134">Contiene hello spazi dei nomi seguenti:</span><span class="sxs-lookup"><span data-stu-id="89b4b-134">It contains hello following namespaces:</span></span>

* <span data-ttu-id="89b4b-135">**SendGrid** per la comunicazione con l'API di SendGrid.</span><span class="sxs-lookup"><span data-stu-id="89b4b-135">**SendGrid** for communicating with SendGrid’s API.</span></span>
* <span data-ttu-id="89b4b-136">**SendGrid.Helpers.Mail** helper tooeasily metodi creare oggetti SendGridMessage che specificano come messaggi di posta elettronica toosend.</span><span class="sxs-lookup"><span data-stu-id="89b4b-136">**SendGrid.Helpers.Mail** for helper methods tooeasily create SendGridMessage objects that specify how toosend emails.</span></span>

<span data-ttu-id="89b4b-137">Aggiungere hello seguente top toohello dichiarazioni dello spazio dei nomi di codice di qualsiasi file c# in cui si desidera che il servizio posta elettronica SendGrid di tooprogrammatically accesso hello.</span><span class="sxs-lookup"><span data-stu-id="89b4b-137">Add hello following code namespace declarations toohello top of any C# file in which you want tooprogrammatically access hello SendGrid email service.</span></span>

    using SendGrid;
    using SendGrid.Helpers.Mail;

## <a name="how-to-create-an-email"></a><span data-ttu-id="89b4b-138">Procedura: Creare un messaggio di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="89b4b-138">How to: Create an Email</span></span>
<span data-ttu-id="89b4b-139">Hello utilizzare **SendGridMessage** toocreate un messaggio di posta elettronica dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="89b4b-139">Use hello **SendGridMessage** object toocreate an email message.</span></span> <span data-ttu-id="89b4b-140">Una volta creato l'oggetto messaggio hello, è possibile impostare le proprietà e metodi, incluso il mittente di posta elettronica hello, destinatario di posta elettronica, hello e soggetto hello e corpo del messaggio di posta elettronica hello.</span><span class="sxs-lookup"><span data-stu-id="89b4b-140">Once hello message object is created, you can set properties and methods, including hello email sender, hello email recipient, and hello subject and body of hello email.</span></span>

<span data-ttu-id="89b4b-141">Hello esempio seguente viene illustrato come un oggetto di posta elettronica completamente popolato toocreate:</span><span class="sxs-lookup"><span data-stu-id="89b4b-141">hello following example demonstrates how toocreate a fully populated email object:</span></span>

    var msg = new SendGridMessage();

    msg.SetFrom(new EmailAddress("dx@example.com", "SendGrid DX Team"));

    var recipients = new List<EmailAddress>
    {
        new EmailAddress("jeff@example.com", "Jeff Smith"),
        new EmailAddress("anna@example.com", "Anna Lidman"),
        new EmailAddress("peter@example.com", "Peter Saddow")
    };
    msg.AddTos(recipients);

    msg.SetSubject("Testing hello SendGrid C# Library");

    msg.AddContent(MimeType.Text, "Hello World plain text!");
    msg.AddContent(MimeType.Html, "<p>Hello World!</p>");

<span data-ttu-id="89b4b-142">Per altre informazioni su tutte le proprietà e i metodi supportati dal tipo **SendGrid**, vedere [sendgrid-csharp][sendgrid-csharp] in GitHub.</span><span class="sxs-lookup"><span data-stu-id="89b4b-142">For more information on all properties and methods supported by the **SendGrid** type, see [sendgrid-csharp][sendgrid-csharp] on GitHub.</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="89b4b-143">Procedura: Inviare un messaggio di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="89b4b-143">How to: Send an Email</span></span>
<span data-ttu-id="89b4b-144">Dopo aver creato un'email, è possibile inviarla tramite l'API di SendGrid.</span><span class="sxs-lookup"><span data-stu-id="89b4b-144">After creating an email message, you can send it using SendGrid's API.</span></span> <span data-ttu-id="89b4b-145">In alternativa è possibile usare la [libreria integrata di .NET][NET-library].</span><span class="sxs-lookup"><span data-stu-id="89b4b-145">Alternatively, you may use [.NET's built in library][NET-library].</span></span>

<span data-ttu-id="89b4b-146">Per inviare email, è necessario specificare la chiave API di SendGrid.</span><span class="sxs-lookup"><span data-stu-id="89b4b-146">Sending email requires that you supply your SendGrid API Key.</span></span> <span data-ttu-id="89b4b-147">Se è necessario informazioni dettagliate su come tooconfigure chiavi API, visitare le chiavi API di SendGrid [documentazione][documentation].</span><span class="sxs-lookup"><span data-stu-id="89b4b-147">If you need details about how tooconfigure API Keys, please visit SendGrid's API Keys [documentation][documentation].</span></span>

<span data-ttu-id="89b4b-148">È possibile archiviare le credenziali tramite il portale di Azure facendo clic su impostazioni dell'applicazione e aggiungere coppie chiave/valore di hello in impostazioni App.</span><span class="sxs-lookup"><span data-stu-id="89b4b-148">You may store these credentials via your Azure Portal by clicking Application settings and adding hello key/value pairs under App settings.</span></span>

 ![Impostazioni app di Azure][azure_app_settings]

 <span data-ttu-id="89b4b-150">Quindi, è possibile accedervi come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="89b4b-150">Then, you may access them as follows:</span></span>

    var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
    var client = new SendGridClient(apiKey);

<span data-ttu-id="89b4b-151">Hello seguono esempi Mostra come un messaggio utilizzando toosend hello API Web.</span><span class="sxs-lookup"><span data-stu-id="89b4b-151">hello following examples show how toosend a message using hello Web API.</span></span>

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
                    Subject = "Hello World from hello SendGrid CSharp SDK!",
                    PlainTextContent = "Hello, Email!",
                    HtmlContent = "<strong>Hello, Email!</strong>"
                };
                msg.AddTo(new EmailAddress("test@example.com", "Test User"));
                var response = await client.SendEmailAsync(msg);
            }
        }
    }

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="89b4b-152">Procedura: Aggiungere un allegato</span><span class="sxs-lookup"><span data-stu-id="89b4b-152">How to: Add an attachment</span></span>
<span data-ttu-id="89b4b-153">È possibile aggiungere allegati tooa messaggio dal chiamante hello **AddAttachment** metodo e specificando almeno hello nome e il file con codifica Base64 di contenuto si desidera tooattach.</span><span class="sxs-lookup"><span data-stu-id="89b4b-153">Attachments can be added tooa message by calling hello **AddAttachment** method and minimally specifying hello file name and Base64 encoded content you want tooattach.</span></span> <span data-ttu-id="89b4b-154">È possibile includere più allegati chiamando questo metodo una volta per ogni file desiderato tooattach o utilizzando hello **AddAttachments** metodo.</span><span class="sxs-lookup"><span data-stu-id="89b4b-154">You can include multiple attachments by calling this method once for each file you wish tooattach or by using hello **AddAttachments** method.</span></span> <span data-ttu-id="89b4b-155">Hello di esempio seguente viene illustrato come aggiungere un messaggio tooa allegato:</span><span class="sxs-lookup"><span data-stu-id="89b4b-155">hello following example demonstrates adding an attachment tooa message:</span></span>

    var banner2 = new Attachment()
    {
        Content = Convert.ToBase64String(raw_content),
        Type = "image/png",
        Filename = "banner2.png",
        Disposition = "inline",
        ContentId = "Banner 2"
    };
    msg.AddAttachment(banner2);

## <a name="how-to-use-mail-settings-tooenable-footers-tracking-and-analytics"></a><span data-ttu-id="89b4b-156">Procedura: utilizzare piè di pagina tooenable impostazioni posta elettronica, il rilevamento e analitica</span><span class="sxs-lookup"><span data-stu-id="89b4b-156">How to: Use mail settings tooenable footers, tracking, and analytics</span></span>
<span data-ttu-id="89b4b-157">SendGrid fornisce funzionalità di posta elettronica aggiuntivo tramite l'utilizzo di hello delle impostazioni di posta elettronica e le impostazioni di rilevamento.</span><span class="sxs-lookup"><span data-stu-id="89b4b-157">SendGrid provides additional email functionality through hello use of mail settings and tracking settings.</span></span> <span data-ttu-id="89b4b-158">Queste impostazioni possono essere aggiunti tooan messaggio tooenable specifiche funzionalità di posta elettronica, ad esempio fare clic su rilevamento, Google analitica, sottoscrizione di rilevamento e così via.</span><span class="sxs-lookup"><span data-stu-id="89b4b-158">These settings can be added tooan email message tooenable specific functionality such as click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="89b4b-159">Per un elenco completo delle App, vedere hello [impostazioni documentazione][settings-documentation].</span><span class="sxs-lookup"><span data-stu-id="89b4b-159">For a full list of apps, see hello [Settings Documentation][settings-documentation].</span></span>

<span data-ttu-id="89b4b-160">Le app possono essere applicate troppo**SendGrid** utilizzando i metodi implementati come parte di hello messaggi di posta elettronica **SendGridMessage** classe.</span><span class="sxs-lookup"><span data-stu-id="89b4b-160">Apps can be applied too**SendGrid** email messages using methods implemented as part of hello **SendGridMessage** class.</span></span> <span data-ttu-id="89b4b-161">Hello negli esempi seguenti illustrano piè di pagina hello e fare clic su Verifica filtri:</span><span class="sxs-lookup"><span data-stu-id="89b4b-161">hello following examples demonstrate hello footer and click tracking filters:</span></span>

<span data-ttu-id="89b4b-162">Hello negli esempi seguenti illustrano piè di pagina hello e fare clic su Verifica filtri:</span><span class="sxs-lookup"><span data-stu-id="89b4b-162">hello following examples demonstrate hello footer and click tracking filters:</span></span>

### <a name="footer-settings"></a><span data-ttu-id="89b4b-163">Impostazioni del piè di pagina</span><span class="sxs-lookup"><span data-stu-id="89b4b-163">Footer settings</span></span>
    msg.SetFooterSetting(
                         true,
                         "Some Footer HTML",
                         "<strong>Some Footer Text</strong>");

### <a name="click-tracking"></a><span data-ttu-id="89b4b-164">Monitoraggio dei clic</span><span class="sxs-lookup"><span data-stu-id="89b4b-164">Click tracking</span></span>
    msg.SetClickTracking(true);

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="89b4b-165">Procedura: Usare servizi aggiuntivi forniti da SendGrid</span><span class="sxs-lookup"><span data-stu-id="89b4b-165">How to: Use Additional SendGrid Services</span></span>
<span data-ttu-id="89b4b-166">SendGrid offre diverse API e ai webhook, che è possibile utilizzare la funzionalità aggiuntive di tooleverage all'interno dell'applicazione Azure.</span><span class="sxs-lookup"><span data-stu-id="89b4b-166">SendGrid offers several APIs and webhooks that you can use tooleverage additional functionality within your Azure application.</span></span> <span data-ttu-id="89b4b-167">Per ulteriori informazioni, vedere hello [riferimento all'API SendGrid][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="89b4b-167">For more details, see hello [SendGrid API Reference][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="89b4b-168">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="89b4b-168">Next steps</span></span>
<span data-ttu-id="89b4b-169">Ora che si è appreso nozioni di base di hello di hello servizio di posta elettronica di SendGrid, seguire questi ulteriori toolearn di collegamenti.</span><span class="sxs-lookup"><span data-stu-id="89b4b-169">Now that you've learned hello basics of hello SendGrid Email service, follow these links toolearn more.</span></span>

* <span data-ttu-id="89b4b-170">Repository della libreria C\# di SendGrid: [sendgrid-csharp][sendgrid-csharp]</span><span class="sxs-lookup"><span data-stu-id="89b4b-170">SendGrid C\# library repo: [sendgrid-csharp][sendgrid-csharp]</span></span>
* <span data-ttu-id="89b4b-171">Documentazione relativa all'API SendGrid: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="89b4b-171">SendGrid API documentation: <https://sendgrid.com/docs></span></span>

[Next steps]: #next-steps
[What is hello SendGrid Email Service?]: #whatis
[Create a SendGrid Account]: #createaccount
[Reference hello SendGrid .NET Class Library]: #reference
[How to: Create an Email]: #createemail
[How to: Send an Email]: #sendemail
[How to: Add an Attachment]: #addattachment
[How to: Use Filters tooEnable Footers, Tracking, and Analytics]: #usefilters
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

[servizio di posta elettronica basato sul cloud]: https://sendgrid.com/solutions
[recapito affidabile di messaggi di posta elettronica transazionali]: https://sendgrid.com/use-cases/transactional-email

