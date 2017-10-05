---
title: Come usare il servizio e-mail SendGrid (Java) | Microsoft Docs
description: Informazioni su come inviare messaggi di posta elettronica con il servizio di posta elettronica SendGrid disponibile in Azure. Gli esempi di codice sono scritti in Java.
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
ms.openlocfilehash: 85a0e302626ca14ac039ee6f662f372ddbeb62c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-send-email-using-sendgrid-from-java"></a><span data-ttu-id="c81cc-104">Come inviare messaggi di posta elettronica usando SendGrid da Java</span><span class="sxs-lookup"><span data-stu-id="c81cc-104">How to Send Email Using SendGrid from Java</span></span>
<span data-ttu-id="c81cc-105">Questa guida illustra come eseguire attività di programmazione comuni con il servizio di posta elettronica SendGrid in Azure.</span><span class="sxs-lookup"><span data-stu-id="c81cc-105">This guide demonstrates how to perform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="c81cc-106">Gli esempi sono scritti in Java.</span><span class="sxs-lookup"><span data-stu-id="c81cc-106">The samples are written in Java.</span></span> <span data-ttu-id="c81cc-107">Gli scenari presentati includono **creazione di messaggi di posta elettronica**, **invio di messaggi di posta elettronica**, **aggiunta di allegati**, **uso di filtri** e **aggiornamento delle proprietà**.</span><span class="sxs-lookup"><span data-stu-id="c81cc-107">The scenarios covered include **constructing email**, **sending email**, **adding attachments**, **using filters**, and **updating properties**.</span></span> <span data-ttu-id="c81cc-108">Per altre informazioni su SendGrid e sull'invio di messaggi di posta elettronica, vedere la sezione [Passaggi successivi](#next-steps) .</span><span class="sxs-lookup"><span data-stu-id="c81cc-108">For more information on SendGrid and sending email, see the [Next steps](#next-steps) section.</span></span>

## <a name="what-is-the-sendgrid-email-service"></a><span data-ttu-id="c81cc-109">Informazioni sul servizio di posta elettronica SendGrid</span><span class="sxs-lookup"><span data-stu-id="c81cc-109">What is the SendGrid Email Service?</span></span>
<span data-ttu-id="c81cc-110">SendGrid è un [servizio di posta elettronica basato sul cloud] che offre [recapito affidabile di messaggi di posta elettronica transazionali], scalabilità e analisi in tempo reale, oltre ad API flessibili che agevolano l'integrazione personalizzata.</span><span class="sxs-lookup"><span data-stu-id="c81cc-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="c81cc-111">Gli scenari di utilizzo comuni di SendGrid includono:</span><span class="sxs-lookup"><span data-stu-id="c81cc-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="c81cc-112">Invio automatico di ricevute ai clienti</span><span class="sxs-lookup"><span data-stu-id="c81cc-112">Automatically sending receipts to customers</span></span>
* <span data-ttu-id="c81cc-113">Amministrazione di liste di distribuzione per l'invio mensile ai clienti di volantini elettronici e offerte speciali</span><span class="sxs-lookup"><span data-stu-id="c81cc-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="c81cc-114">Raccolta di metriche in tempo reale per elementi quali indirizzi di posta elettronica bloccati e velocità di risposta al cliente</span><span class="sxs-lookup"><span data-stu-id="c81cc-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="c81cc-115">Generazione di report per agevolare l'identificazione delle tendenze</span><span class="sxs-lookup"><span data-stu-id="c81cc-115">Generating reports to help identify trends</span></span>
* <span data-ttu-id="c81cc-116">Inoltro di richieste dei clienti</span><span class="sxs-lookup"><span data-stu-id="c81cc-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="c81cc-117">Notifiche di posta elettronica dall'applicazione</span><span class="sxs-lookup"><span data-stu-id="c81cc-117">Email notifications from your application</span></span>

<span data-ttu-id="c81cc-118">Per altre informazioni, visitare il sito <http://sendgrid.com>.</span><span class="sxs-lookup"><span data-stu-id="c81cc-118">For more information, see <http://sendgrid.com>.</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="c81cc-119">Creare un account SendGrid</span><span class="sxs-lookup"><span data-stu-id="c81cc-119">Create a SendGrid account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="how-to-use-the-javaxmail-libraries"></a><span data-ttu-id="c81cc-120">Procedura: Usare le librerie javax.mail</span><span class="sxs-lookup"><span data-stu-id="c81cc-120">How to: Use the javax.mail libraries</span></span>
<span data-ttu-id="c81cc-121">Ottenere le librerie javax.mail, ad esempio da <http://www.oracle.com/technetwork/java/javamail> e importarle nel codice.</span><span class="sxs-lookup"><span data-stu-id="c81cc-121">Obtain the javax.mail libraries, for example from <http://www.oracle.com/technetwork/java/javamail> and import them into your code.</span></span> <span data-ttu-id="c81cc-122">Ad alto livello, la procedura per usare la libreria javax.mail per l'invio di messaggio di posta elettronica mediante SMTP è la seguente:</span><span class="sxs-lookup"><span data-stu-id="c81cc-122">At a high-level, the process for using the javax.mail library to send email using SMTP is to do the following:</span></span>

1. <span data-ttu-id="c81cc-123">Specificare i valori SMTP, compreso il server SMTP, che per SendGrid è smtp.sendgrid.net.</span><span class="sxs-lookup"><span data-stu-id="c81cc-123">Specify the SMTP values, including the SMTP server, which for SendGrid is smtp.sendgrid.net.</span></span>

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

1. <span data-ttu-id="c81cc-124">Estendere la classe *javax.mail.Authenticator* e nella propria implementazione del metodo *getPasswordAuthentication* restituire il nome utente e la password di SendGrid.</span><span class="sxs-lookup"><span data-stu-id="c81cc-124">Extend the *javax.mail.Authenticator* class, and in your implementation of the *getPasswordAuthentication* method, return your SendGrid user name and password.</span></span>  

       private class SMTPAuthenticator extends javax.mail.Authenticator {
       public PasswordAuthentication getPasswordAuthentication() {
          String username = SMTP_AUTH_USER;
          String password = SMTP_AUTH_PWD;
          return new PasswordAuthentication(username, password);
       }
2. <span data-ttu-id="c81cc-125">Creare una sessione di posta autenticata mediante un oggetto *javax.mail.Session* .</span><span class="sxs-lookup"><span data-stu-id="c81cc-125">Create an authenticated email session through a *javax.mail.Session* object.</span></span>  

       Authenticator auth = new SMTPAuthenticator();
       Session mailSession = Session.getDefaultInstance(properties, auth);
3. <span data-ttu-id="c81cc-126">Creare il messaggio e assegnare i valori relativi ai campi **A**, **Da**, **Oggetto** e contenuto.</span><span class="sxs-lookup"><span data-stu-id="c81cc-126">Create your message and assign **To**, **From**, **Subject** and content values.</span></span> <span data-ttu-id="c81cc-127">Questa operazione è illustrata nella sezione [Procedura: Creare un'e-mail](#how-to-create-an-email) .</span><span class="sxs-lookup"><span data-stu-id="c81cc-127">This is shown in the [How To: Create an Email](#how-to-create-an-email) section.</span></span>
4. <span data-ttu-id="c81cc-128">Inviare il messaggio tramite un oggetto *javax.mail.Transport* .</span><span class="sxs-lookup"><span data-stu-id="c81cc-128">Send the message through a *javax.mail.Transport* object.</span></span> <span data-ttu-id="c81cc-129">Questa operazione è illustrata nella sezione [Procedura: Inviare un messaggio di posta elettronica][Procedura: Inviare un messaggio di posta elettronica].</span><span class="sxs-lookup"><span data-stu-id="c81cc-129">This is shown in the [How To: Send an Email][How to: Send an Email] section.</span></span>

## <a name="how-to-create-an-email"></a><span data-ttu-id="c81cc-130">Procedura: Creare un messaggio di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="c81cc-130">How to: Create an email</span></span>
<span data-ttu-id="c81cc-131">Il codice seguente illustra come specificare i valori per un messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="c81cc-131">The following shows how to specify values for an email.</span></span>

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

## <a name="how-to-send-an-email"></a><span data-ttu-id="c81cc-132">Procedura: Inviare un messaggio di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="c81cc-132">How to: Send an email</span></span>
<span data-ttu-id="c81cc-133">Il codice seguente illustra come inviare un messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="c81cc-133">The following shows how to send an email.</span></span>

    Transport transport = mailSession.getTransport();
    // Connect the transport object.
    transport.connect();
    // Send the message.
    transport.sendMessage(message, message.getAllRecipients());
    // Close the connection.
    transport.close();

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="c81cc-134">Procedura: Aggiungere un allegato</span><span class="sxs-lookup"><span data-stu-id="c81cc-134">How to: Add an attachment</span></span>
<span data-ttu-id="c81cc-135">Il codice seguente illustra come aggiungere un allegato.</span><span class="sxs-lookup"><span data-stu-id="c81cc-135">The following code shows you how to add an attachment.</span></span>

    // Local file name and path.
    String attachmentName = "myfile.zip";
    String attachmentPath = "c:\\myfiles\\";
    MimeBodyPart attachmentPart = new MimeBodyPart();
    // Specify the local file to attach.
    DataSource source = new FileDataSource(attachmentPath + attachmentName);
    attachmentPart.setDataHandler(new DataHandler(source));
    // This example uses the local file name as the attachment name.
    // They could be different if you prefer.
    attachmentPart.setFileName(attachmentName);
    multipart.addBodyPart(attachmentPart);

## <a name="how-to-use-filters-to-enable-footers-tracking-and-analytics"></a><span data-ttu-id="c81cc-136">Procedura: Usare filtri per abilitare piè di pagina, monitoraggio e analisi</span><span class="sxs-lookup"><span data-stu-id="c81cc-136">How to: Use filters to enable footers, tracking, and analytics</span></span>
<span data-ttu-id="c81cc-137">SendGrid fornisce funzionalità di posta elettronica aggiuntive attraverso l'utilizzo di *filtri*.</span><span class="sxs-lookup"><span data-stu-id="c81cc-137">SendGrid provides additional email functionality through the use of *filters*.</span></span> <span data-ttu-id="c81cc-138">Si tratta di impostazioni che è possibile aggiungere a un messaggio di posta elettronica per abilitare funzionalità specifiche, ad esempio il monitoraggio del clic, Google Analytics, il monitoraggio delle sottoscrizioni e così via.</span><span class="sxs-lookup"><span data-stu-id="c81cc-138">These are settings that can be added to an email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="c81cc-139">Per un elenco completo dei filtri, vedere le [impostazioni dei filtri][Filter Settings].</span><span class="sxs-lookup"><span data-stu-id="c81cc-139">For a full list of filters, see [Filter Settings][Filter Settings].</span></span>

* <span data-ttu-id="c81cc-140">Il codice seguente illustra come inserire un filtro per piè di pagina che provoca la visualizzazione di testo in formato HTML in fondo al messaggio di posta elettronica inviato.</span><span class="sxs-lookup"><span data-stu-id="c81cc-140">The following shows how to insert a footer filter that results in HTML text appearing at the bottom of the email being sent.</span></span>

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"footer\":
          {\"settings\":
          {\"enable\":1,\"text/html\":
          \"<html><b>Thank you</b> for your business.</html>\"}}}}");
* <span data-ttu-id="c81cc-141">Un altro esempio di filtro è quello per il monitoraggio dei clic.</span><span class="sxs-lookup"><span data-stu-id="c81cc-141">Another example of a filter is click tracking.</span></span> <span data-ttu-id="c81cc-142">Si supponga ad esempio che il testo del messaggio di posta elettronica contenga un collegamento ipertestuale come il seguente e che si voglia monitorare il tasso di clic:</span><span class="sxs-lookup"><span data-stu-id="c81cc-142">Let’s say that your email text contains a hyperlink, such as the following, and you want to track the click rate:</span></span>

      messagePart.setContent(
          "Hello,
          <p>This is the body of the message. Visit
          <a href='http://www.contoso.com'>http://www.contoso.com</a>.</p>
          Thank you.",
          "text/html");
* <span data-ttu-id="c81cc-143">Per abilitare il monitoraggio dei clic, usare il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="c81cc-143">To enable the click tracking, use the following code:</span></span>

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"clicktrack\":
          {\"settings\":
          {\"enable\":1}}}}");

## <a name="how-to-update-email-properties"></a><span data-ttu-id="c81cc-144">Procedura: Aggiornare le proprietà dei messaggi di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="c81cc-144">How to: Update email properties</span></span>
<span data-ttu-id="c81cc-145">Alcune proprietà del messaggio di posta elettronica può essere sovrascritto usando  **impostare*proprietà** * o aggiunti utilizzando  **aggiungere*proprietà** *.</span><span class="sxs-lookup"><span data-stu-id="c81cc-145">Some email properties can be overwritten using **set*Property*** or appended using **add*Property***.</span></span>

<span data-ttu-id="c81cc-146">Ad esempio, per specificare indirizzi **Rispondi a** , usare il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="c81cc-146">For example, to specify **ReplyTo** addresses, use the following:</span></span>

    InternetAddress addresses[] =
        { new InternetAddress("john@contoso.com"),
          new InternetAddress("wendy@contoso.com") };

    message.setReplyTo(addresses);

<span data-ttu-id="c81cc-147">Per aggiungere un destinatario **Cc** , usare il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="c81cc-147">To add a **Cc** recipient, use the following:</span></span>

    message.addRecipient(Message.RecipientType.CC, new
    InternetAddress("john@contoso.com"));

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="c81cc-148">Procedura: Usare servizi aggiuntivi forniti da SendGrid</span><span class="sxs-lookup"><span data-stu-id="c81cc-148">How to: Use additional SendGrid services</span></span>
<span data-ttu-id="c81cc-149">SendGrid offre API basate sul Web che è possibile usare per sfruttare altre funzionalità di SendGrid dall'applicazione Azure.</span><span class="sxs-lookup"><span data-stu-id="c81cc-149">SendGrid offers web-based APIs that you can use to leverage additional SendGrid functionality from your Azure application.</span></span> <span data-ttu-id="c81cc-150">Per informazioni dettagliate, vedere la [documentazione sull'API SendGrid][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="c81cc-150">For full details, see the [SendGrid API documentation][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="c81cc-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c81cc-151">Next steps</span></span>
<span data-ttu-id="c81cc-152">A questo punto, dopo aver appreso le nozioni di base del servizio di posta elettronica SendGrid, è possibile usare i collegamenti seguenti per ottenere altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="c81cc-152">Now that you’ve learned the basics of the SendGrid Email service, follow these links to learn more.</span></span>

* <span data-ttu-id="c81cc-153">Esempio che illustra l'uso di SendGrid in una distribuzione Azure: [Come inviare messaggi di posta elettronica usando SendGrid da Java in una distribuzione Azure](store-sendgrid-java-how-to-send-email-example.md)</span><span class="sxs-lookup"><span data-stu-id="c81cc-153">Sample that demonstrates using SendGrid in an Azure deployment: [How to send email using SendGrid from Java in an Azure deployment](store-sendgrid-java-how-to-send-email-example.md)</span></span>
* <span data-ttu-id="c81cc-154">SDK Java per SendGrid: <https://sendgrid.com/docs/Code_Examples/java.html></span><span class="sxs-lookup"><span data-stu-id="c81cc-154">SendGrid Java SDK: <https://sendgrid.com/docs/Code_Examples/java.html></span></span>
* <span data-ttu-id="c81cc-155">Documentazione relativa all'API SendGrid: <https://sendgrid.com/docs/API_Reference/index.html></span><span class="sxs-lookup"><span data-stu-id="c81cc-155">SendGrid API documentation: <https://sendgrid.com/docs/API_Reference/index.html></span></span>
* <span data-ttu-id="c81cc-156">Offerta speciale SendGrid per i clienti di Azure: <https://sendgrid.com/windowsazure.html></span><span class="sxs-lookup"><span data-stu-id="c81cc-156">SendGrid special offer for Azure customers: <https://sendgrid.com/windowsazure.html></span></span>

[http://sendgrid.com]: https://sendgrid.com
[http://sendgrid.com/pricing.html]: http://sendgrid.com/pricing.html
[http://www.sendgrid.com/azure.html]: https://www.sendgrid.com/windowsazure.html
[http://sendgrid.com/features]: https://sendgrid.com/features
[http://www.oracle.com/technetwork/java/javamail]: http://www.oracle.com/technetwork/java/javamail/index.html
[Filter Settings]: https://sendgrid.com/docs/API_Reference/Web_API/filter_settings.html
[SendGrid API documentation]: https://sendgrid.com/docs/API_Reference/index.html
[http://sendgrid.com/azure.html]: https://sendgrid.com/windowsazure.html
<span data-ttu-id="c81cc-157">[servizio di posta elettronica basato sul cloud]: https://sendgrid.com/email-solutions</span><span class="sxs-lookup"><span data-stu-id="c81cc-157">[cloud-based email service]: https://sendgrid.com/email-solutions</span></span>
<span data-ttu-id="c81cc-158">[recapito affidabile di messaggi di posta elettronica transazionali]: https://sendgrid.com/transactional-email</span><span class="sxs-lookup"><span data-stu-id="c81cc-158">[transactional email delivery]: https://sendgrid.com/transactional-email</span></span>
