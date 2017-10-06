---
title: aaastore-sendgrid-Java-How-to-Send-email-example
description: Come toosend di posta elettronica usando SendGrid da Java in una distribuzione di Azure
services: 
documentationcenter: java
author: thinkingserious
manager: sendgrid
editor: mollybos
ms.assetid: af096a73-6985-4350-92e4-ce1722c8d72f
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 10/30/2014
ms.author: vibhork;dominic.may@sendgrid.com;elmer.thomas@sendgrid.com
ms.openlocfilehash: 51fde1fc71467f8252532b30d2f87856ec25067b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-from-java-in-an-azure-deployment"></a>Come tooSend posta elettronica usando SendGrid da Java in una distribuzione di Azure
Hello seguente esempio viene illustrato come utilizzare messaggi di posta elettronica toosend SendGrid da una pagina web ospitata in Azure. un'applicazione Hello risultante utente verrà chiesto hello di valori di posta elettronica, come illustrato nella seguente cattura di schermata hello.

![Modulo per la posta elettronica][emailform]

Hello risultante posta elettronica avrà un aspetto simile toohello seguente cattura di schermata.

![Messaggio di posta elettronica][emailsent]

È necessario seguente hello toodo codice hello toouse in questo argomento:

1. Ottenere hello JAR javax. Mail, ad esempio da <http://www.oracle.com/technetwork/java/javamail/index.html>.
2. Aggiungere hello JAR tooyour percorso di compilazione Java.
3. Se si usa Eclipse toocreate questa applicazione Java, è possibile includere le librerie di SendGrid hello nel file di distribuzione dell'applicazione (WAR) con funzionalità di distribuzione di assembly di Eclipse. Se non si utilizza Eclipse toocreate questa applicazione Java, verificare che le librerie di hello sono incluse nell'hello stesso ruolo di Azure come percorso di classe Java toohello dell'applicazione e aggiunta dell'applicazione.

È inoltre necessario proprio nome utente di SendGrid e la password, messaggio di posta elettronica hello in grado di toosend toobe. tooget avviato con SendGrid, vedere [come toosend di posta elettronica usando SendGrid da Java](store-sendgrid-java-how-to-send-email.md).

Inoltre, avere familiarità con informazioni hello [la creazione di un'applicazione Hello World per Azure in Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944), o con altre tecniche per l'hosting di applicazioni Java in Azure se non si usa Eclipse, è consigliabile.

## <a name="create-a-web-form-for-sending-email"></a>Creare un modulo Web per l'invio di posta elettronica
Hello seguente codice mostra come toocreate un web form tooretrieve dati dell'utente per l'invio di posta elettronica. Ai fini di questo contenuto, denominato file JSP hello **emailform.jsp**.

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
        pageEncoding="ISO-8859-1" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Email form</title>
    </head>
    <body>
     <p>Fill in all fields and click <b>Send this email</b>.</p>
     <br/>
      <form action="sendemail.jsp" method="post">
       <table>
         <tr>
           <td>To:</td>
           <td><input type="text" size=50 name="emailTo">
           </td>
         </tr>
         <tr>
           <td>From:</td>
           <td><input type="text" size=50 name="emailFrom">
           </td>
         </tr>
         <tr>
           <td>Subject:</td>
           <td><input type="text" size=100 name="emailSubject" value="My email subject">
           </td>
         </tr>
         <tr>
           <td>Text:</td>
           <td><input type="text" size=400 name="emailText" value="Hello,<p>This is my message.</p>Thank you." />
           </td>
         </tr>
         <tr>
           <td>SendGrid user name:</td>
           <td><input type="text" name="sendGridUser">
           </td>
         </tr>
         <tr>
           <td>SendGrid password:</td>
           <td><input type="password" name="sendGridPassword">
           </td>
         </tr>
         <tr>
           <td colspan=2><input type="submit" value="Send this email">
           </td>
         </tr>
       </table>
     </form>
     <br/>
    </body>
    </html>

## <a name="create-hello-code-toosend-hello-email"></a>Creare messaggio di posta elettronica hello toosend codice hello
Hello codice riportato di seguito, viene chiamato quando si completa il modulo hello in emailform.jsp, crea il messaggio di posta elettronica hello e lo invia. Ai fini di questo contenuto, denominato file JSP hello **sendemail.jsp**.

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
        pageEncoding="ISO-8859-1" import="javax.activation.*, javax.mail.*, javax.mail.internet.*, java.util.Date, java.util.Properties" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Email processing happens here</title>
    </head>
    <body>
        <b>This is my send mail page.</b><p/>
     <%

     final String sendGridUser = request.getParameter("sendGridUser");
     final String sendGridPassword = request.getParameter("sendGridPassword");

     class SMTPAuthenticator extends Authenticator
     {
       public PasswordAuthentication getPasswordAuthentication()
       {
            String username = sendGridUser;
            String password = sendGridPassword;

            return new PasswordAuthentication(username, password);   
       }
     }
     try
     {

         // hello SendGrid SMTP server.
         String SMTP_HOST_NAME = "smtp.sendgrid.net";

         Properties properties;

         properties = new Properties();

         // Specify SMTP values.
         properties.put("mail.transport.protocol", "smtp");
         properties.put("mail.smtp.host", SMTP_HOST_NAME);
         properties.put("mail.smtp.port", 587);
         properties.put("mail.smtp.auth", "true");

         // Display hello email fields entered by hello user. 
         out.println("Value entered for email Subject: " + request.getParameter("emailSubject") + "<br/>");        
         out.println("Value entered for email      To: " + request.getParameter("emailTo") + "<br/>");
         out.println("Value entered for email    From: " + request.getParameter("emailFrom") + "<br/>");
         out.println("Value entered for email    Text: " + "<br/>" + request.getParameter("emailText") + "<br/>");

         // Create hello authenticator object.
         Authenticator authenticator = new SMTPAuthenticator();

         // Create hello mail session object.
         Session mailSession;
         mailSession = Session.getDefaultInstance(properties, authenticator);

         // Display debug information toostdout, useful when using the
         // compute emulator during development.
         mailSession.setDebug(true);

         // Create hello message and message part objects.
         MimeMessage message;
         Multipart multipart;
         MimeBodyPart messagePart; 

         message = new MimeMessage(mailSession);

         multipart = new MimeMultipart("alternative");
         messagePart = new MimeBodyPart();
         messagePart.setContent(request.getParameter("emailText"), "text/html");
         multipart.addBodyPart(messagePart);            

         // Specify hello email To, From, Subject and Content. 
         message.setFrom(new InternetAddress(request.getParameter("emailFrom")));
         message.addRecipient(Message.RecipientType.TO, new InternetAddress(request.getParameter("emailTo")));
         message.setSubject(request.getParameter("emailSubject")); 
         message.setContent(multipart);

         // Uncomment hello following if you want tooadd a footer.
         // message.addHeader("X-SMTPAPI", "{\"filters\": {\"footer\": {\"settings\": {\"enable\":1,\"text/html\": \"<html>This is my <b>email footer</b>.</html>\"}}}}");

         // Uncomment hello following if you want tooenable click tracking.
         // message.addHeader("X-SMTPAPI", "{\"filters\": {\"clicktrack\": {\"settings\": {\"enable\":1}}}}");

         Transport transport;
         transport = mailSession.getTransport();
         // Connect hello transport object.
         transport.connect();
         // Send hello message.
         transport.sendMessage(message,  message.getRecipients(Message.RecipientType.TO));
         // Close hello connection.
         transport.close();

        out.println("<p>Email processing completed.</p>");

     }
     catch (Exception e)
     {
         out.println("<p>Exception encountered: " + 
                            e.getMessage()     +
                            "</p>");   
     }
    %>

    </body>
    </html>

Messaggio di posta elettronica hello toosending emailform.jsp fornisce inoltre un risultato per utente hello. un esempio è hello cattura di schermata seguente:

![Risultato invio posta elettronica][emailresult]

## <a name="next-steps"></a>Passaggi successivi
Distribuire l'emulatore di calcolo toohello applicazione e in un browser eseguire emailform.jsp, immettere i valori in formato hello, fare clic su **inviare questo messaggio di posta elettronica**e quindi visualizzare i risultati in sendemail.jsp.

Questo codice è stato fornito tooshow è come toouse SendGrid in Java in Azure. Prima di distribuire tooAzure nell'ambiente di produzione, è consigliabile tooadd più la gestione degli errori o altre funzionalità. ad esempio: 

* È possibile utilizzare i BLOB di archiviazione di Azure o indirizzi di posta elettronica Database SQL toostore e messaggi di posta elettronica, anziché utilizzare un web form. Per informazioni sull'utilizzo di BLOB di archiviazione di Azure in Java, vedere [come tooUse hello servizio di archiviazione Blob da Java](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/). Per informazioni sull'uso dei database SQL in Java, vedere [Uso di database SQL in Java](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/).
* È possibile utilizzare `RoleEnvironment.getConfigurationSettings` tooretrieve hello SendGrid username e password da impostazioni di configurazione della distribuzione, anziché utilizzare hello web form tooretrieve tali valori. Per informazioni su hello `RoleEnvironment` classe, vedere [Using hello libreria di Runtime del servizio di Azure in JSP](http://msdn.microsoft.com/library/windowsazure/hh690948) e la documentazione di pacchetto di Runtime del servizio Azure hello in <http://dl.windowsazure.com/javadoc>.
* Per ulteriori informazioni sull'uso di SendGrid in linguaggio, vedere [come toosend di posta elettronica usando SendGrid da Java](store-sendgrid-java-how-to-send-email.md).

[emailform]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailform.jpg
[emailsent]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailSent.jpg
[emailresult]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaResult.jpg
