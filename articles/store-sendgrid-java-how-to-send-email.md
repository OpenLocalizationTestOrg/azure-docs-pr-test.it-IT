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
# <a name="how-toosend-email-using-sendgrid-from-java"></a>Come tooSend posta elettronica usando SendGrid da Java
Questa guida illustra come tooperform attività di programmazione comuni con di SendGrid tramite posta elettronica del servizio in Azure. esempi di Hello sono scritti in Java. Hello scenari trattati includono **la costruzione di posta elettronica**, **l'invio di posta elettronica**, **aggiungere allegati**, **utilizzando filtri**e **l'aggiornamento delle proprietà**. Per ulteriori informazioni su SendGrid e l'invio di posta elettronica, vedere hello [passaggi successivi](#next-steps) sezione.

## <a name="what-is-hello-sendgrid-email-service"></a>Che cos'è il servizio di posta elettronica SendGrid hello?
SendGrid è un [servizio di posta elettronica basato sul cloud] che offre [recapito affidabile di messaggi di posta elettronica transazionali], scalabilità e analisi in tempo reale, oltre ad API flessibili che agevolano l'integrazione personalizzata. Gli scenari di utilizzo comuni di SendGrid includono:

* Inviare automaticamente toocustomers conferme di recapito
* Amministrazione di liste di distribuzione per l'invio mensile ai clienti di volantini elettronici e offerte speciali
* Raccolta di metriche in tempo reale per elementi quali indirizzi di posta elettronica bloccati e velocità di risposta al cliente
* Generazione di report toohelp identificare le tendenze
* Inoltro di richieste dei clienti
* Notifiche di posta elettronica dall'applicazione

Per altre informazioni, visitare il sito <http://sendgrid.com>.

## <a name="create-a-sendgrid-account"></a>Creare un account SendGrid
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="how-to-use-hello-javaxmail-libraries"></a>Procedura: utilizzare le librerie di hello javax. Mail
Ottenere le librerie javax. Mail hello, ad esempio da <http://www.oracle.com/technetwork/java/javamail> e importarli nel codice. A livello generale, hello processo per l'uso di hello javax. Mail libreria toosend messaggio di posta elettronica tramite SMTP è toodo hello seguente:

1. Specificare i valori di SMTP hello, incluso il server SMTP hello, ovvero per SendGrid smtp.sendgrid.net.

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

1. Estendere hello *javax.mail.Authenticator* (classe) e nell'implementazione del *getPasswordAuthentication* metodo, restituire il nome utente di SendGrid e la password.  

       private class SMTPAuthenticator extends javax.mail.Authenticator {
       public PasswordAuthentication getPasswordAuthentication() {
          String username = SMTP_AUTH_USER;
          String password = SMTP_AUTH_PWD;
          return new PasswordAuthentication(username, password);
       }
2. Creare una sessione di posta autenticata mediante un oggetto *javax.mail.Session* .  

       Authenticator auth = new SMTPAuthenticator();
       Session mailSession = Session.getDefaultInstance(properties, auth);
3. Creare il messaggio e assegnare i valori relativi ai campi **A**, **Da**, **Oggetto** e contenuto. Come illustrato nell'hello [procedura: creare un messaggio di posta elettronica](#how-to-create-an-email) sezione.
4. Inviare il messaggio hello tramite un *javax.mail.Transport* oggetto. Come illustrato nell'hello [How To: inviare un messaggio di posta elettronica] [Procedura: inviare un messaggio di posta elettronica] sezione.

## <a name="how-to-create-an-email"></a>Procedura: Creare un messaggio di posta elettronica
Hello seguito è riportato come toospecify valori per un messaggio di posta elettronica.

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
Hello seguente mostra come toosend un messaggio di posta elettronica.

    Transport transport = mailSession.getTransport();
    // Connect hello transport object.
    transport.connect();
    // Send hello message.
    transport.sendMessage(message, message.getAllRecipients());
    // Close hello connection.
    transport.close();

## <a name="how-to-add-an-attachment"></a>Procedura: Aggiungere un allegato
Hello codice seguente illustra come tooadd un allegato.

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

## <a name="how-to-use-filters-tooenable-footers-tracking-and-analytics"></a>Procedura: utilizzare i filtri tooenable piè di pagina, il rilevamento e analitica
SendGrid fornisce funzionalità di posta elettronica aggiuntive tramite l'utilizzo di hello di *filtri*. Si tratta di impostazioni che è possibile aggiungere il messaggio di posta elettronica tooan per abilitare le funzionalità specifiche, quali l'abilitazione di fare clic su rilevamento, Google analitica, di rilevamento, sottoscrizione e così via. Per un elenco completo dei filtri, vedere le [impostazioni dei filtri][Filter Settings].

* esempio Hello viene illustrato come applicare i filtri che generano testo HTML visualizzato nella parte inferiore di hello del messaggio di posta elettronica hello inviato tooinsert un piè di pagina.

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"footer\":
          {\"settings\":
          {\"enable\":1,\"text/html\":
          \"<html><b>Thank you</b> for your business.</html>\"}}}}");
* Un altro esempio di filtro è quello per il monitoraggio dei clic. Si supponga che il testo del messaggio di posta elettronica contiene un collegamento ipertestuale, ad esempio hello seguenti e si desidera hello tootrack fare clic su frequenza:

      messagePart.setContent(
          "Hello,
          <p>This is hello body of hello message. Visit
          <a href='http://www.contoso.com'>http://www.contoso.com</a>.</p>
          Thank you.",
          "text/html");
* hello tooenable fare clic su verifica, utilizzare hello seguente codice:

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"clicktrack\":
          {\"settings\":
          {\"enable\":1}}}}");

## <a name="how-to-update-email-properties"></a>Procedura: Aggiornare le proprietà dei messaggi di posta elettronica
Alcune proprietà del messaggio di posta elettronica può essere sovrascritto usando  **impostare*proprietà** * o aggiunti utilizzando  **aggiungere*proprietà** *.

Ad esempio, toospecify **ReplyTo** indirizzi, utilizzare la seguente hello:

    InternetAddress addresses[] =
        { new InternetAddress("john@contoso.com"),
          new InternetAddress("wendy@contoso.com") };

    message.setReplyTo(addresses);

tooadd un **Cc** seguente di hello destinatario, utilizzare:

    message.addRecipient(Message.RecipientType.CC, new
    InternetAddress("john@contoso.com"));

## <a name="how-to-use-additional-sendgrid-services"></a>Procedura: Usare servizi aggiuntivi forniti da SendGrid
SendGrid offre API basata sul web che è possibile utilizzare altre funzionalità di SendGrid tooleverage dall'applicazione Azure. Per informazioni dettagliate, vedere hello [documentazione dell'API SendGrid][SendGrid API documentation].

## <a name="next-steps"></a>Passaggi successivi
Ora che si è appreso nozioni di base di hello di hello servizio di posta elettronica di SendGrid, seguire questi ulteriori toolearn di collegamenti.

* Esempio che illustra l'uso di SendGrid in una distribuzione di Azure: [come toosend di posta elettronica usando SendGrid da Java in una distribuzione di Azure](store-sendgrid-java-how-to-send-email-example.md)
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
