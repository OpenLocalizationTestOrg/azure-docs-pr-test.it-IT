---
title: hello toouse aaaHow SendGrid servizio di posta elettronica (linguaggio) | Documenti Microsoft
description: Informazioni su come inviare posta elettronica con il servizio di posta elettronica SendGrid hello in Azure. Gli esempi di codice sono scritti in Java.
services: 
documentationcenter: java
author: thinkingserious
manager: sendgrid
editor: mollybos
ms.assetid: cc75c43e-ede9-492b-98c2-9147fcb92c21
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 10/30/2014
ms.author: elmer.thomas@sendgrid.com; erika.berkland@sendgrid.com; vibhork
ms.openlocfilehash: 542ce0003e94fc8f5551487d5a3cd6f75d27e8cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-from-java"></a><span data-ttu-id="7afec-104">Come tooSend posta elettronica usando SendGrid da Java</span><span class="sxs-lookup"><span data-stu-id="7afec-104">How tooSend Email Using SendGrid from Java</span></span>
<span data-ttu-id="7afec-105">Questa guida illustra come tooperform attività di programmazione comuni con di SendGrid tramite posta elettronica del servizio in Azure.</span><span class="sxs-lookup"><span data-stu-id="7afec-105">This guide demonstrates how tooperform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="7afec-106">esempi di Hello sono scritti in Java.</span><span class="sxs-lookup"><span data-stu-id="7afec-106">hello samples are written in Java.</span></span> <span data-ttu-id="7afec-107">Hello scenari trattati includono **la costruzione di posta elettronica**, **l'invio di posta elettronica**, **aggiungere allegati**, **utilizzando filtri**e **l'aggiornamento delle proprietà**.</span><span class="sxs-lookup"><span data-stu-id="7afec-107">hello scenarios covered include **constructing email**, **sending email**, **adding attachments**, **using filters**, and **updating properties**.</span></span> <span data-ttu-id="7afec-108">Per ulteriori informazioni su SendGrid e l'invio di posta elettronica, vedere hello [passaggi successivi](#next-steps) sezione.</span><span class="sxs-lookup"><span data-stu-id="7afec-108">For more information on SendGrid and sending email, see hello [Next steps](#next-steps) section.</span></span>

## <a name="what-is-hello-sendgrid-email-service"></a><span data-ttu-id="7afec-109">Che cos'è il servizio di posta elettronica SendGrid hello?</span><span class="sxs-lookup"><span data-stu-id="7afec-109">What is hello SendGrid Email Service?</span></span>
<span data-ttu-id="7afec-110">SendGrid è un [servizio di posta elettronica basato sul cloud] che offre [recapito affidabile di messaggi di posta elettronica transazionali], scalabilità e analisi in tempo reale, oltre ad API flessibili che agevolano l'integrazione personalizzata.</span><span class="sxs-lookup"><span data-stu-id="7afec-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="7afec-111">Gli scenari di utilizzo comuni di SendGrid includono:</span><span class="sxs-lookup"><span data-stu-id="7afec-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="7afec-112">Inviare automaticamente toocustomers conferme di recapito</span><span class="sxs-lookup"><span data-stu-id="7afec-112">Automatically sending receipts toocustomers</span></span>
* <span data-ttu-id="7afec-113">Amministrazione di liste di distribuzione per l'invio mensile ai clienti di volantini elettronici e offerte speciali</span><span class="sxs-lookup"><span data-stu-id="7afec-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="7afec-114">Raccolta di metriche in tempo reale per elementi quali indirizzi di posta elettronica bloccati e velocità di risposta al cliente</span><span class="sxs-lookup"><span data-stu-id="7afec-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="7afec-115">Generazione di report toohelp identificare le tendenze</span><span class="sxs-lookup"><span data-stu-id="7afec-115">Generating reports toohelp identify trends</span></span>
* <span data-ttu-id="7afec-116">Inoltro di richieste dei clienti</span><span class="sxs-lookup"><span data-stu-id="7afec-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="7afec-117">Notifiche di posta elettronica dall'applicazione</span><span class="sxs-lookup"><span data-stu-id="7afec-117">Email notifications from your application</span></span>

<span data-ttu-id="7afec-118">Per altre informazioni, visitare il sito <http://sendgrid.com>.</span><span class="sxs-lookup"><span data-stu-id="7afec-118">For more information, see <http://sendgrid.com>.</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="7afec-119">Creare un account SendGrid</span><span class="sxs-lookup"><span data-stu-id="7afec-119">Create a SendGrid account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="how-to-use-hello-javaxmail-libraries"></a><span data-ttu-id="7afec-120">Procedura: utilizzare le librerie di hello javax. Mail</span><span class="sxs-lookup"><span data-stu-id="7afec-120">How to: Use hello javax.mail libraries</span></span>
<span data-ttu-id="7afec-121">Ottenere le librerie javax. Mail hello, ad esempio da <http://www.oracle.com/technetwork/java/javamail> e importarli nel codice.</span><span class="sxs-lookup"><span data-stu-id="7afec-121">Obtain hello javax.mail libraries, for example from <http://www.oracle.com/technetwork/java/javamail> and import them into your code.</span></span> <span data-ttu-id="7afec-122">A livello generale, hello processo per l'uso di hello javax. Mail libreria toosend messaggio di posta elettronica tramite SMTP è toodo hello seguente:</span><span class="sxs-lookup"><span data-stu-id="7afec-122">At a high-level, hello process for using hello javax.mail library toosend email using SMTP is toodo hello following:</span></span>

1. <span data-ttu-id="7afec-123">Specificare i valori di SMTP hello, incluso il server SMTP hello, ovvero per SendGrid smtp.sendgrid.net.</span><span class="sxs-lookup"><span data-stu-id="7afec-123">Specify hello SMTP values, including hello SMTP server, which for SendGrid is smtp.sendgrid.net.</span></span>

```
        import java.util.Properties;
        import javax.activation.*;
        import javax.mail.*;
        import javax.mail.internet.*;

        public class MyEmailer {
           private static final String SMTP_HOST_NAME = "smtp.sendgrid.net";
           private static final String SMTP_AUTH_USER = "your_sendgrid_username";
           private static final String SMTP_AUTH_PWD = "your_sendgrid_password";

           public static void main(String[] args) throws Exception{
               new MyEmailer().SendMail();
           }

           public void SendMail() throws Exception
           {
              Properties properties = new Properties();
                 properties.put("mail.transport.protocol", "smtp");
                 properties.put("mail.smtp.host", SMTP_HOST_NAME);
                 properties.put("mail.smtp.port", 587);
                 properties.put("mail.smtp.auth", "true");
                 // …
```

1. <span data-ttu-id="7afec-124">Estendere hello *javax.mail.Authenticator* (classe) e nell'implementazione del *getPasswordAuthentication* metodo, restituire il nome utente di SendGrid e la password.</span><span class="sxs-lookup"><span data-stu-id="7afec-124">Extend hello *javax.mail.Authenticator* class, and in your implementation of the *getPasswordAuthentication* method, return your SendGrid user name and password.</span></span>  

       private class SMTPAuthenticator extends javax.mail.Authenticator {
       public PasswordAuthentication getPasswordAuthentication() {
          String username = SMTP_AUTH_USER;
          String password = SMTP_AUTH_PWD;
          return new PasswordAuthentication(username, password);
       }
2. <span data-ttu-id="7afec-125">Creare una sessione di posta autenticata mediante un oggetto *javax.mail.Session* .</span><span class="sxs-lookup"><span data-stu-id="7afec-125">Create an authenticated email session through a *javax.mail.Session* object.</span></span>  

       Authenticator auth = new SMTPAuthenticator();
       Session mailSession = Session.getDefaultInstance(properties, auth);
3. <span data-ttu-id="7afec-126">Creare il messaggio e assegnare i valori relativi ai campi **A**, **Da**, **Oggetto** e contenuto.</span><span class="sxs-lookup"><span data-stu-id="7afec-126">Create your message and assign **To**, **From**, **Subject** and content values.</span></span> <span data-ttu-id="7afec-127">Come illustrato nell'hello [procedura: creare un messaggio di posta elettronica](#how-to-create-an-email) sezione.</span><span class="sxs-lookup"><span data-stu-id="7afec-127">This is shown in hello [How To: Create an Email](#how-to-create-an-email) section.</span></span>
4. <span data-ttu-id="7afec-128">Inviare il messaggio hello tramite un *javax.mail.Transport* oggetto.</span><span class="sxs-lookup"><span data-stu-id="7afec-128">Send hello message through a *javax.mail.Transport* object.</span></span> <span data-ttu-id="7afec-129">Come illustrato nell'hello [How To: inviare un messaggio di posta elettronica] [Procedura: inviare un messaggio di posta elettronica] sezione.</span><span class="sxs-lookup"><span data-stu-id="7afec-129">This is shown in hello [How To: Send an Email][How to: Send an Email] section.</span></span>

## <a name="how-to-create-an-email"></a><span data-ttu-id="7afec-130">Procedura: Creare un messaggio di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="7afec-130">How to: Create an email</span></span>
<span data-ttu-id="7afec-131">Hello seguito è riportato come toospecify valori per un messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="7afec-131">hello following shows how toospecify values for an email.</span></span>

    MimeMessage message = new MimeMessage(mailSession);
    Multipart multipart = new MimeMultipart("alternative");
    BodyPart part1 = new MimeBodyPart();
    part1.setText("Hello, Your Contoso order has shipped. Thank you, John");
    BodyPart part2 = new MimeBodyPart();
    part2.setContent(
        "<p>Hello,</p>
        <p>Your Contoso order has <b>shipped</b>.</p>
        <p>Thank you,<br>John</br></p>",
        "text/html");
    multipart.addBodyPart(part1);
    multipart.addBodyPart(part2);
    message.setFrom(new InternetAddress("john@contoso.com"));
    message.addRecipient(Message.RecipientType.TO,
       new InternetAddress("someone@example.com"));
    message.setSubject("Your recent order");
    message.setContent(multipart);

## <a name="how-to-send-an-email"></a><span data-ttu-id="7afec-132">Procedura: Inviare un messaggio di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="7afec-132">How to: Send an email</span></span>
<span data-ttu-id="7afec-133">Hello seguente mostra come toosend un messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="7afec-133">hello following shows how toosend an email.</span></span>

    Transport transport = mailSession.getTransport();
    // Connect hello transport object.
    transport.connect();
    // Send hello message.
    transport.sendMessage(message, message.getAllRecipients());
    // Close hello connection.
    transport.close();

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="7afec-134">Procedura: Aggiungere un allegato</span><span class="sxs-lookup"><span data-stu-id="7afec-134">How to: Add an attachment</span></span>
<span data-ttu-id="7afec-135">Hello codice seguente illustra come tooadd un allegato.</span><span class="sxs-lookup"><span data-stu-id="7afec-135">hello following code shows you how tooadd an attachment.</span></span>

    // Local file name and path.
    String attachmentName = "myfile.zip";
    String attachmentPath = "c:\\myfiles\\";
    MimeBodyPart attachmentPart = new MimeBodyPart();
    // Specify hello local file tooattach.
    DataSource source = new FileDataSource(attachmentPath + attachmentName);
    attachmentPart.setDataHandler(new DataHandler(source));
    // This example uses hello local file name as hello attachment name.
    // They could be different if you prefer.
    attachmentPart.setFileName(attachmentName);
    multipart.addBodyPart(attachmentPart);

## <a name="how-to-use-filters-tooenable-footers-tracking-and-analytics"></a><span data-ttu-id="7afec-136">Procedura: utilizzare i filtri tooenable piè di pagina, il rilevamento e analitica</span><span class="sxs-lookup"><span data-stu-id="7afec-136">How to: Use filters tooenable footers, tracking, and analytics</span></span>
<span data-ttu-id="7afec-137">SendGrid fornisce funzionalità di posta elettronica aggiuntive tramite l'utilizzo di hello di *filtri*.</span><span class="sxs-lookup"><span data-stu-id="7afec-137">SendGrid provides additional email functionality through hello use of *filters*.</span></span> <span data-ttu-id="7afec-138">Si tratta di impostazioni che è possibile aggiungere il messaggio di posta elettronica tooan per abilitare le funzionalità specifiche, quali l'abilitazione di fare clic su rilevamento, Google analitica, di rilevamento, sottoscrizione e così via.</span><span class="sxs-lookup"><span data-stu-id="7afec-138">These are settings that can be added tooan email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="7afec-139">Per un elenco completo dei filtri, vedere le [impostazioni dei filtri][Filter Settings].</span><span class="sxs-lookup"><span data-stu-id="7afec-139">For a full list of filters, see [Filter Settings][Filter Settings].</span></span>

* <span data-ttu-id="7afec-140">esempio Hello viene illustrato come applicare i filtri che generano testo HTML visualizzato nella parte inferiore di hello del messaggio di posta elettronica hello inviato tooinsert un piè di pagina.</span><span class="sxs-lookup"><span data-stu-id="7afec-140">hello following shows how tooinsert a footer filter that results in HTML text appearing at hello bottom of hello email being sent.</span></span>

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"footer\":
          {\"settings\":
          {\"enable\":1,\"text/html\":
          \"<html><b>Thank you</b> for your business.</html>\"}}}}");
* <span data-ttu-id="7afec-141">Un altro esempio di filtro è quello per il monitoraggio dei clic.</span><span class="sxs-lookup"><span data-stu-id="7afec-141">Another example of a filter is click tracking.</span></span> <span data-ttu-id="7afec-142">Si supponga che il testo del messaggio di posta elettronica contiene un collegamento ipertestuale, ad esempio hello seguenti e si desidera hello tootrack fare clic su frequenza:</span><span class="sxs-lookup"><span data-stu-id="7afec-142">Let’s say that your email text contains a hyperlink, such as hello following, and you want tootrack hello click rate:</span></span>

      messagePart.setContent(
          "Hello,
          <p>This is hello body of hello message. Visit
          <a href='http://www.contoso.com'>http://www.contoso.com</a>.</p>
          Thank you.",
          "text/html");
* <span data-ttu-id="7afec-143">hello tooenable fare clic su verifica, utilizzare hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="7afec-143">tooenable hello click tracking, use hello following code:</span></span>

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"clicktrack\":
          {\"settings\":
          {\"enable\":1}}}}");

## <a name="how-to-update-email-properties"></a><span data-ttu-id="7afec-144">Procedura: Aggiornare le proprietà dei messaggi di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="7afec-144">How to: Update email properties</span></span>
<span data-ttu-id="7afec-145">Alcune proprietà del messaggio di posta elettronica può essere sovrascritto usando  **impostare*proprietà** * o aggiunti utilizzando  **aggiungere*proprietà** *.</span><span class="sxs-lookup"><span data-stu-id="7afec-145">Some email properties can be overwritten using **set*Property*** or appended using **add*Property***.</span></span>

<span data-ttu-id="7afec-146">Ad esempio, toospecify **ReplyTo** indirizzi, utilizzare la seguente hello:</span><span class="sxs-lookup"><span data-stu-id="7afec-146">For example, toospecify **ReplyTo** addresses, use hello following:</span></span>

    InternetAddress addresses[] =
        { new InternetAddress("john@contoso.com"),
          new InternetAddress("wendy@contoso.com") };

    message.setReplyTo(addresses);

<span data-ttu-id="7afec-147">tooadd un **Cc** seguente di hello destinatario, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="7afec-147">tooadd a **Cc** recipient, use hello following:</span></span>

    message.addRecipient(Message.RecipientType.CC, new
    InternetAddress("john@contoso.com"));

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="7afec-148">Procedura: Usare servizi aggiuntivi forniti da SendGrid</span><span class="sxs-lookup"><span data-stu-id="7afec-148">How to: Use additional SendGrid services</span></span>
<span data-ttu-id="7afec-149">SendGrid offre API basata sul web che è possibile utilizzare altre funzionalità di SendGrid tooleverage dall'applicazione Azure.</span><span class="sxs-lookup"><span data-stu-id="7afec-149">SendGrid offers web-based APIs that you can use tooleverage additional SendGrid functionality from your Azure application.</span></span> <span data-ttu-id="7afec-150">Per informazioni dettagliate, vedere hello [documentazione dell'API SendGrid][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="7afec-150">For full details, see hello [SendGrid API documentation][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="7afec-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7afec-151">Next steps</span></span>
<span data-ttu-id="7afec-152">Ora che si è appreso nozioni di base di hello di hello servizio di posta elettronica di SendGrid, seguire questi ulteriori toolearn di collegamenti.</span><span class="sxs-lookup"><span data-stu-id="7afec-152">Now that you’ve learned hello basics of hello SendGrid Email service, follow these links toolearn more.</span></span>

* <span data-ttu-id="7afec-153">Esempio che illustra l'uso di SendGrid in una distribuzione di Azure: [come toosend di posta elettronica usando SendGrid da Java in una distribuzione di Azure](store-sendgrid-java-how-to-send-email-example.md)</span><span class="sxs-lookup"><span data-stu-id="7afec-153">Sample that demonstrates using SendGrid in an Azure deployment: [How toosend email using SendGrid from Java in an Azure deployment](store-sendgrid-java-how-to-send-email-example.md)</span></span>
* <span data-ttu-id="7afec-154">SDK Java per SendGrid: <https://sendgrid.com/docs/Code_Examples/java.html></span><span class="sxs-lookup"><span data-stu-id="7afec-154">SendGrid Java SDK: <https://sendgrid.com/docs/Code_Examples/java.html></span></span>
* <span data-ttu-id="7afec-155">Documentazione relativa all'API SendGrid: <https://sendgrid.com/docs/API_Reference/index.html></span><span class="sxs-lookup"><span data-stu-id="7afec-155">SendGrid API documentation: <https://sendgrid.com/docs/API_Reference/index.html></span></span>
* <span data-ttu-id="7afec-156">Offerta speciale SendGrid per i clienti di Azure: <https://sendgrid.com/windowsazure.html></span><span class="sxs-lookup"><span data-stu-id="7afec-156">SendGrid special offer for Azure customers: <https://sendgrid.com/windowsazure.html></span></span>

[http://sendgrid.com]: https://sendgrid.com
[http://sendgrid.com/pricing.html]: http://sendgrid.com/pricing.html
[http://www.sendgrid.com/azure.html]: https://www.sendgrid.com/windowsazure.html
[http://sendgrid.com/features]: https://sendgrid.com/features
[http://www.oracle.com/technetwork/java/javamail]: http://www.oracle.com/technetwork/java/javamail/index.html
[Filter Settings]: https://sendgrid.com/docs/API_Reference/Web_API/filter_settings.html
[SendGrid API documentation]: https://sendgrid.com/docs/API_Reference/index.html
[http://sendgrid.com/azure.html]: https://sendgrid.com/windowsazure.html
[servizio di posta elettronica basato sul cloud]: https://sendgrid.com/email-solutions
[recapito affidabile di messaggi di posta elettronica transazionali]: https://sendgrid.com/transactional-email
