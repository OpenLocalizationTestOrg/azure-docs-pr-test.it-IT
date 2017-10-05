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
# <a name="how-to-send-email-using-sendgrid-from-java"></a>Come inviare messaggi di posta elettronica usando SendGrid da Java
Questa guida illustra come eseguire attività di programmazione comuni con il servizio di posta elettronica SendGrid in Azure. Gli esempi sono scritti in Java. Gli scenari presentati includono **creazione di messaggi di posta elettronica**, **invio di messaggi di posta elettronica**, **aggiunta di allegati**, **uso di filtri** e **aggiornamento delle proprietà**. Per altre informazioni su SendGrid e sull'invio di messaggi di posta elettronica, vedere la sezione [Passaggi successivi](#next-steps) .

## <a name="what-is-the-sendgrid-email-service"></a>Informazioni sul servizio di posta elettronica SendGrid
SendGrid è un [servizio di posta elettronica basato sul cloud] che offre [recapito affidabile di messaggi di posta elettronica transazionali], scalabilità e analisi in tempo reale, oltre ad API flessibili che agevolano l'integrazione personalizzata. Gli scenari di utilizzo comuni di SendGrid includono:

* Invio automatico di ricevute ai clienti
* Amministrazione di liste di distribuzione per l'invio mensile ai clienti di volantini elettronici e offerte speciali
* Raccolta di metriche in tempo reale per elementi quali indirizzi di posta elettronica bloccati e velocità di risposta al cliente
* Generazione di report per agevolare l'identificazione delle tendenze
* Inoltro di richieste dei clienti
* Notifiche di posta elettronica dall'applicazione

Per altre informazioni, visitare il sito <http://sendgrid.com>.

## <a name="create-a-sendgrid-account"></a>Creare un account SendGrid
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="how-to-use-the-javaxmail-libraries"></a>Procedura: Usare le librerie javax.mail
Ottenere le librerie javax.mail, ad esempio da <http://www.oracle.com/technetwork/java/javamail> e importarle nel codice. Ad alto livello, la procedura per usare la libreria javax.mail per l'invio di messaggio di posta elettronica mediante SMTP è la seguente:

1. Specificare i valori SMTP, compreso il server SMTP, che per SendGrid è smtp.sendgrid.net.

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

1. Estendere la classe *javax.mail.Authenticator* e nella propria implementazione del metodo *getPasswordAuthentication* restituire il nome utente e la password di SendGrid.  

       private class SMTPAuthenticator extends javax.mail.Authenticator {
       public PasswordAuthentication getPasswordAuthentication() {
          String username = SMTP_AUTH_USER;
          String password = SMTP_AUTH_PWD;
          return new PasswordAuthentication(username, password);
       }
2. Creare una sessione di posta autenticata mediante un oggetto *javax.mail.Session* .  

       Authenticator auth = new SMTPAuthenticator();
       Session mailSession = Session.getDefaultInstance(properties, auth);
3. Creare il messaggio e assegnare i valori relativi ai campi **A**, **Da**, **Oggetto** e contenuto. Questa operazione è illustrata nella sezione [Procedura: Creare un'e-mail](#how-to-create-an-email) .
4. Inviare il messaggio tramite un oggetto *javax.mail.Transport* . Questa operazione è illustrata nella sezione [Procedura: Inviare un messaggio di posta elettronica][Procedura: Inviare un messaggio di posta elettronica].

## <a name="how-to-create-an-email"></a>Procedura: Creare un messaggio di posta elettronica
Il codice seguente illustra come specificare i valori per un messaggio di posta elettronica.

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

## <a name="how-to-send-an-email"></a>Procedura: Inviare un messaggio di posta elettronica
Il codice seguente illustra come inviare un messaggio di posta elettronica.

    Transport transport = mailSession.getTransport();
    // Connect the transport object.
    transport.connect();
    // Send the message.
    transport.sendMessage(message, message.getAllRecipients());
    // Close the connection.
    transport.close();

## <a name="how-to-add-an-attachment"></a>Procedura: Aggiungere un allegato
Il codice seguente illustra come aggiungere un allegato.

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

## <a name="how-to-use-filters-to-enable-footers-tracking-and-analytics"></a>Procedura: Usare filtri per abilitare piè di pagina, monitoraggio e analisi
SendGrid fornisce funzionalità di posta elettronica aggiuntive attraverso l'utilizzo di *filtri*. Si tratta di impostazioni che è possibile aggiungere a un messaggio di posta elettronica per abilitare funzionalità specifiche, ad esempio il monitoraggio del clic, Google Analytics, il monitoraggio delle sottoscrizioni e così via. Per un elenco completo dei filtri, vedere le [impostazioni dei filtri][Filter Settings].

* Il codice seguente illustra come inserire un filtro per piè di pagina che provoca la visualizzazione di testo in formato HTML in fondo al messaggio di posta elettronica inviato.

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"footer\":
          {\"settings\":
          {\"enable\":1,\"text/html\":
          \"<html><b>Thank you</b> for your business.</html>\"}}}}");
* Un altro esempio di filtro è quello per il monitoraggio dei clic. Si supponga ad esempio che il testo del messaggio di posta elettronica contenga un collegamento ipertestuale come il seguente e che si voglia monitorare il tasso di clic:

      messagePart.setContent(
          "Hello,
          <p>This is the body of the message. Visit
          <a href='http://www.contoso.com'>http://www.contoso.com</a>.</p>
          Thank you.",
          "text/html");
* Per abilitare il monitoraggio dei clic, usare il codice seguente:

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"clicktrack\":
          {\"settings\":
          {\"enable\":1}}}}");

## <a name="how-to-update-email-properties"></a>Procedura: Aggiornare le proprietà dei messaggi di posta elettronica
Alcune proprietà del messaggio di posta elettronica può essere sovrascritto usando  **impostare*proprietà** * o aggiunti utilizzando  **aggiungere*proprietà** *.

Ad esempio, per specificare indirizzi **Rispondi a** , usare il codice seguente:

    InternetAddress addresses[] =
        { new InternetAddress("john@contoso.com"),
          new InternetAddress("wendy@contoso.com") };

    message.setReplyTo(addresses);

Per aggiungere un destinatario **Cc** , usare il codice seguente:

    message.addRecipient(Message.RecipientType.CC, new
    InternetAddress("john@contoso.com"));

## <a name="how-to-use-additional-sendgrid-services"></a>Procedura: Usare servizi aggiuntivi forniti da SendGrid
SendGrid offre API basate sul Web che è possibile usare per sfruttare altre funzionalità di SendGrid dall'applicazione Azure. Per informazioni dettagliate, vedere la [documentazione sull'API SendGrid][SendGrid API documentation].

## <a name="next-steps"></a>Passaggi successivi
A questo punto, dopo aver appreso le nozioni di base del servizio di posta elettronica SendGrid, è possibile usare i collegamenti seguenti per ottenere altre informazioni.

* Esempio che illustra l'uso di SendGrid in una distribuzione Azure: [Come inviare messaggi di posta elettronica usando SendGrid da Java in una distribuzione Azure](store-sendgrid-java-how-to-send-email-example.md)
* SDK Java per SendGrid: <https://sendgrid.com/docs/Code_Examples/java.html>
* Documentazione relativa all'API SendGrid: <https://sendgrid.com/docs/API_Reference/index.html>
* Offerta speciale SendGrid per i clienti di Azure: <https://sendgrid.com/windowsazure.html>

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
