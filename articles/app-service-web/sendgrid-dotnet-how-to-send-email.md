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
# <a name="how-toosend-email-using-sendgrid-with-azure"></a>Come tooSend SendGrid tramite posta elettronica con Azure
## <a name="overview"></a>Panoramica
Questa guida illustra come tooperform attività di programmazione comuni con di SendGrid tramite posta elettronica del servizio in Azure. Hello esempi sono scritti in C\# e supporta .NET Standard 1.3. scenari di Hello trattati includono la costruzione di posta elettronica, l'invio di posta elettronica, l'aggiunta di allegati e l'abilitazione di posta elettronica diversi e impostazioni di verifica. Per ulteriori informazioni su SendGrid e l'invio di posta elettronica, vedere hello [passaggi successivi] [ Next steps] sezione.

## <a name="what-is-hello-sendgrid-email-service"></a>Che cos'è il servizio di posta elettronica SendGrid hello?
SendGrid è un [servizio di posta elettronica basato sul cloud] che offre [recapito affidabile di messaggi di posta elettronica transazionali], scalabilità e analisi in tempo reale, oltre ad API flessibili che agevolano l'integrazione personalizzata. I casi d'uso comuni di SendGrid includono:

* Automaticamente l'invio di conferme di recapito o toocustomers conferme di acquisto.
* Amministrazione di liste di distribuzione per inviare mensilmente volantini e promozioni ai clienti.
* Raccolta di metriche in tempo reale per elementi quali email bloccate ed engagement del cliente.
* Inoltro di richieste dei clienti.
* Elaborazione di messaggi di posta elettronica in arrivo.

Per altre informazioni visitare [https://sendgrid.com](https://sendgrid.com) o la [libreria C#][sendgrid-csharp] di SendGrid nel repository GitHub.

## <a name="create-a-sendgrid-account"></a>Creazione di un account SendGrid
[!INCLUDE [sendgrid-sign-up](../../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-net-class-library"></a>Fare riferimento a hello libreria di classi .NET SendGrid
Hello [il pacchetto SendGrid NuGet](https://www.nuget.org/packages/Sendgrid) è hello più semplice modo tooget hello API SendGrid e tooconfigure l'applicazione con tutte le dipendenze. NuGet è un estensione inclusi con Microsoft Visual Studio 2015 e versioni successive che rende facile tooinstall e aggiornamento di librerie e strumenti di Visual Studio.

> [!NOTE]
> tooinstall NuGet se si esegue una versione di Visual Studio precedenti a Visual Studio 2015, visitare [http://www.nuget.org](http://www.nuget.org), fare clic su hello **installare NuGet** pulsante.
>
>

hello tooinstall nell'applicazione, il pacchetto SendGrid NuGet hello seguenti:

1. Fare clic su **Nuovo progetto** e selezionare un **modello**.

   ![Creare un nuovo progetto][create-new-project]
2. In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Riferimenti** e scegliere **Gestisci pacchetti NuGet**.

   ![pacchetto NuGet di SendGrid][SendGrid-NuGet-package]
3. Cercare **SendGrid** e seleziona hello **SendGrid** elemento nell'elenco dei risultati.
4. Selezionare versione stabile più recente di hello del pacchetto Nuget hello hello versione elenco a discesa toobe in grado di toowork con modello a oggetti hello e API illustrate in questo articolo.

   ![Pacchetto SendGrid][sendgrid-package]
5. Fare clic su **installare** toocomplete hello installazione e quindi chiudere questa finestra di dialogo.

La libreria della classe .NET di SendGrid è denominata **SendGrid**. Contiene hello spazi dei nomi seguenti:

* **SendGrid** per la comunicazione con l'API di SendGrid.
* **SendGrid.Helpers.Mail** helper tooeasily metodi creare oggetti SendGridMessage che specificano come messaggi di posta elettronica toosend.

Aggiungere hello seguente top toohello dichiarazioni dello spazio dei nomi di codice di qualsiasi file c# in cui si desidera che il servizio posta elettronica SendGrid di tooprogrammatically accesso hello.

    using SendGrid;
    using SendGrid.Helpers.Mail;

## <a name="how-to-create-an-email"></a>Procedura: Creare un messaggio di posta elettronica
Hello utilizzare **SendGridMessage** toocreate un messaggio di posta elettronica dell'oggetto. Una volta creato l'oggetto messaggio hello, è possibile impostare le proprietà e metodi, incluso il mittente di posta elettronica hello, destinatario di posta elettronica, hello e soggetto hello e corpo del messaggio di posta elettronica hello.

Hello esempio seguente viene illustrato come un oggetto di posta elettronica completamente popolato toocreate:

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

Per altre informazioni su tutte le proprietà e i metodi supportati dal tipo **SendGrid**, vedere [sendgrid-csharp][sendgrid-csharp] in GitHub.

## <a name="how-to-send-an-email"></a>Procedura: Inviare un messaggio di posta elettronica
Dopo aver creato un'email, è possibile inviarla tramite l'API di SendGrid. In alternativa è possibile usare la [libreria integrata di .NET][NET-library].

Per inviare email, è necessario specificare la chiave API di SendGrid. Se è necessario informazioni dettagliate su come tooconfigure chiavi API, visitare le chiavi API di SendGrid [documentazione][documentation].

È possibile archiviare le credenziali tramite il portale di Azure facendo clic su impostazioni dell'applicazione e aggiungere coppie chiave/valore di hello in impostazioni App.

 ![Impostazioni app di Azure][azure_app_settings]

 Quindi, è possibile accedervi come indicato di seguito:

    var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
    var client = new SendGridClient(apiKey);

Hello seguono esempi Mostra come un messaggio utilizzando toosend hello API Web.

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

## <a name="how-to-add-an-attachment"></a>Procedura: Aggiungere un allegato
È possibile aggiungere allegati tooa messaggio dal chiamante hello **AddAttachment** metodo e specificando almeno hello nome e il file con codifica Base64 di contenuto si desidera tooattach. È possibile includere più allegati chiamando questo metodo una volta per ogni file desiderato tooattach o utilizzando hello **AddAttachments** metodo. Hello di esempio seguente viene illustrato come aggiungere un messaggio tooa allegato:

    var banner2 = new Attachment()
    {
        Content = Convert.ToBase64String(raw_content),
        Type = "image/png",
        Filename = "banner2.png",
        Disposition = "inline",
        ContentId = "Banner 2"
    };
    msg.AddAttachment(banner2);

## <a name="how-to-use-mail-settings-tooenable-footers-tracking-and-analytics"></a>Procedura: utilizzare piè di pagina tooenable impostazioni posta elettronica, il rilevamento e analitica
SendGrid fornisce funzionalità di posta elettronica aggiuntivo tramite l'utilizzo di hello delle impostazioni di posta elettronica e le impostazioni di rilevamento. Queste impostazioni possono essere aggiunti tooan messaggio tooenable specifiche funzionalità di posta elettronica, ad esempio fare clic su rilevamento, Google analitica, sottoscrizione di rilevamento e così via. Per un elenco completo delle App, vedere hello [impostazioni documentazione][settings-documentation].

Le app possono essere applicate troppo**SendGrid** utilizzando i metodi implementati come parte di hello messaggi di posta elettronica **SendGridMessage** classe. Hello negli esempi seguenti illustrano piè di pagina hello e fare clic su Verifica filtri:

Hello negli esempi seguenti illustrano piè di pagina hello e fare clic su Verifica filtri:

### <a name="footer-settings"></a>Impostazioni del piè di pagina
    msg.SetFooterSetting(
                         true,
                         "Some Footer HTML",
                         "<strong>Some Footer Text</strong>");

### <a name="click-tracking"></a>Monitoraggio dei clic
    msg.SetClickTracking(true);

## <a name="how-to-use-additional-sendgrid-services"></a>Procedura: Usare servizi aggiuntivi forniti da SendGrid
SendGrid offre diverse API e ai webhook, che è possibile utilizzare la funzionalità aggiuntive di tooleverage all'interno dell'applicazione Azure. Per ulteriori informazioni, vedere hello [riferimento all'API SendGrid][SendGrid API documentation].

## <a name="next-steps"></a>Passaggi successivi
Ora che si è appreso nozioni di base di hello di hello servizio di posta elettronica di SendGrid, seguire questi ulteriori toolearn di collegamenti.

* Repository della libreria C\# di SendGrid: [sendgrid-csharp][sendgrid-csharp]
* Documentazione relativa all'API SendGrid: <https://sendgrid.com/docs>

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

