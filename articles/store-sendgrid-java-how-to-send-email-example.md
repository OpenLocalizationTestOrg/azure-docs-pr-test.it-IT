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
# <a name="how-toosend-email-using-sendgrid-from-java-in-an-azure-deployment"></a><span data-ttu-id="bc4b7-103">Come tooSend posta elettronica usando SendGrid da Java in una distribuzione di Azure</span><span class="sxs-lookup"><span data-stu-id="bc4b7-103">How tooSend Email Using SendGrid from Java in an Azure Deployment</span></span>
<span data-ttu-id="bc4b7-104">Hello seguente esempio viene illustrato come utilizzare messaggi di posta elettronica toosend SendGrid da una pagina web ospitata in Azure.</span><span class="sxs-lookup"><span data-stu-id="bc4b7-104">hello following example shows you how you can use SendGrid toosend emails from a web page hosted in Azure.</span></span> <span data-ttu-id="bc4b7-105">un'applicazione Hello risultante utente verrà chiesto hello di valori di posta elettronica, come illustrato nella seguente cattura di schermata hello.</span><span class="sxs-lookup"><span data-stu-id="bc4b7-105">hello resulting application will prompt hello user for email values, as shown in hello following screen shot.</span></span>

![Modulo per la posta elettronica][emailform]

<span data-ttu-id="bc4b7-107">Hello risultante posta elettronica avrà un aspetto simile toohello seguente cattura di schermata.</span><span class="sxs-lookup"><span data-stu-id="bc4b7-107">hello resulting email will look similar toohello following screen shot.</span></span>

![Messaggio di posta elettronica][emailsent]

<span data-ttu-id="bc4b7-109">È necessario seguente hello toodo codice hello toouse in questo argomento:</span><span class="sxs-lookup"><span data-stu-id="bc4b7-109">You'll need toodo hello following toouse hello code in this topic:</span></span>

1. <span data-ttu-id="bc4b7-110">Ottenere hello JAR javax. Mail, ad esempio da <http://www.oracle.com/technetwork/java/javamail/index.html>.</span><span class="sxs-lookup"><span data-stu-id="bc4b7-110">Obtain hello javax.mail JARs, for example from <http://www.oracle.com/technetwork/java/javamail/index.html>.</span></span>
2. <span data-ttu-id="bc4b7-111">Aggiungere hello JAR tooyour percorso di compilazione Java.</span><span class="sxs-lookup"><span data-stu-id="bc4b7-111">Add hello JARs tooyour Java build path.</span></span>
3. <span data-ttu-id="bc4b7-112">Se si usa Eclipse toocreate questa applicazione Java, è possibile includere le librerie di SendGrid hello nel file di distribuzione dell'applicazione (WAR) con funzionalità di distribuzione di assembly di Eclipse.</span><span class="sxs-lookup"><span data-stu-id="bc4b7-112">If you are using Eclipse toocreate this Java application, you can include hello SendGrid libraries in your application deployment file (WAR) using Eclipse's deployment assembly feature.</span></span> <span data-ttu-id="bc4b7-113">Se non si utilizza Eclipse toocreate questa applicazione Java, verificare che le librerie di hello sono incluse nell'hello stesso ruolo di Azure come percorso di classe Java toohello dell'applicazione e aggiunta dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bc4b7-113">If you are not using Eclipse toocreate this Java application, ensure hello libraries are included within hello same Azure role as your Java application, and added toohello class path of your application.</span></span>

<span data-ttu-id="bc4b7-114">È inoltre necessario proprio nome utente di SendGrid e la password, messaggio di posta elettronica hello in grado di toosend toobe.</span><span class="sxs-lookup"><span data-stu-id="bc4b7-114">You must also have your own SendGrid username and password, toobe able toosend hello email.</span></span> <span data-ttu-id="bc4b7-115">tooget avviato con SendGrid, vedere [come toosend di posta elettronica usando SendGrid da Java](store-sendgrid-java-how-to-send-email.md).</span><span class="sxs-lookup"><span data-stu-id="bc4b7-115">tooget started with SendGrid, see [How toosend email using SendGrid from Java](store-sendgrid-java-how-to-send-email.md).</span></span>

<span data-ttu-id="bc4b7-116">Inoltre, avere familiarità con informazioni hello [la creazione di un'applicazione Hello World per Azure in Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944), o con altre tecniche per l'hosting di applicazioni Java in Azure se non si usa Eclipse, è consigliabile.</span><span class="sxs-lookup"><span data-stu-id="bc4b7-116">Additionally, familiarity with hello information at [Creating a Hello World Application for Azure in Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944), or with other techniques for hosting Java applications in Azure if you are not using Eclipse, is highly recommended.</span></span>

## <a name="create-a-web-form-for-sending-email"></a><span data-ttu-id="bc4b7-117">Creare un modulo Web per l'invio di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="bc4b7-117">Create a web form for sending email</span></span>
<span data-ttu-id="bc4b7-118">Hello seguente codice mostra come toocreate un web form tooretrieve dati dell'utente per l'invio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="bc4b7-118">hello following code shows how toocreate a web form tooretrieve user data for sending email.</span></span> <span data-ttu-id="bc4b7-119">Ai fini di questo contenuto, denominato file JSP hello **emailform.jsp**.</span><span class="sxs-lookup"><span data-stu-id="bc4b7-119">For purposes of this content, hello JSP file is named **emailform.jsp**.</span></span>

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

## <a name="create-hello-code-toosend-hello-email"></a><span data-ttu-id="bc4b7-120">Creare messaggio di posta elettronica hello toosend codice hello</span><span class="sxs-lookup"><span data-stu-id="bc4b7-120">Create hello code toosend hello email</span></span>
<span data-ttu-id="bc4b7-121">Hello codice riportato di seguito, viene chiamato quando si completa il modulo hello in emailform.jsp, crea il messaggio di posta elettronica hello e lo invia.</span><span class="sxs-lookup"><span data-stu-id="bc4b7-121">hello following code, which is called when you complete hello form in emailform.jsp, creates hello email message and sends it.</span></span> <span data-ttu-id="bc4b7-122">Ai fini di questo contenuto, denominato file JSP hello **sendemail.jsp**.</span><span class="sxs-lookup"><span data-stu-id="bc4b7-122">For purposes of this content, hello JSP file is named **sendemail.jsp**.</span></span>

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

<span data-ttu-id="bc4b7-123">Messaggio di posta elettronica hello toosending emailform.jsp fornisce inoltre un risultato per utente hello. un esempio è hello cattura di schermata seguente:</span><span class="sxs-lookup"><span data-stu-id="bc4b7-123">In addition toosending hello email, emailform.jsp provides a result for hello user; an example is hello following screen shot:</span></span>

![Risultato invio posta elettronica][emailresult]

## <a name="next-steps"></a><span data-ttu-id="bc4b7-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bc4b7-125">Next steps</span></span>
<span data-ttu-id="bc4b7-126">Distribuire l'emulatore di calcolo toohello applicazione e in un browser eseguire emailform.jsp, immettere i valori in formato hello, fare clic su **inviare questo messaggio di posta elettronica**e quindi visualizzare i risultati in sendemail.jsp.</span><span class="sxs-lookup"><span data-stu-id="bc4b7-126">Deploy your application toohello compute emulator and within a browser run emailform.jsp, enter values in hello form, click **Send this email**, and then see results in sendemail.jsp.</span></span>

<span data-ttu-id="bc4b7-127">Questo codice è stato fornito tooshow è come toouse SendGrid in Java in Azure.</span><span class="sxs-lookup"><span data-stu-id="bc4b7-127">This code was provided tooshow you how toouse SendGrid in Java on Azure.</span></span> <span data-ttu-id="bc4b7-128">Prima di distribuire tooAzure nell'ambiente di produzione, è consigliabile tooadd più la gestione degli errori o altre funzionalità.</span><span class="sxs-lookup"><span data-stu-id="bc4b7-128">Before deploying tooAzure in production, you may want tooadd more error handling or other features.</span></span> <span data-ttu-id="bc4b7-129">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="bc4b7-129">For example:</span></span> 

* <span data-ttu-id="bc4b7-130">È possibile utilizzare i BLOB di archiviazione di Azure o indirizzi di posta elettronica Database SQL toostore e messaggi di posta elettronica, anziché utilizzare un web form.</span><span class="sxs-lookup"><span data-stu-id="bc4b7-130">You could use Azure storage blobs or SQL Database toostore email addresses and email messages, instead of using a web form.</span></span> <span data-ttu-id="bc4b7-131">Per informazioni sull'utilizzo di BLOB di archiviazione di Azure in Java, vedere [come tooUse hello servizio di archiviazione Blob da Java](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/).</span><span class="sxs-lookup"><span data-stu-id="bc4b7-131">For information about using Azure storage blobs in Java, see [How tooUse hello Blob Storage Service from Java](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/).</span></span> <span data-ttu-id="bc4b7-132">Per informazioni sull'uso dei database SQL in Java, vedere [Uso di database SQL in Java](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/).</span><span class="sxs-lookup"><span data-stu-id="bc4b7-132">For information about using SQL Database in Java, see [Using SQL Database in Java](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/).</span></span>
* <span data-ttu-id="bc4b7-133">È possibile utilizzare `RoleEnvironment.getConfigurationSettings` tooretrieve hello SendGrid username e password da impostazioni di configurazione della distribuzione, anziché utilizzare hello web form tooretrieve tali valori.</span><span class="sxs-lookup"><span data-stu-id="bc4b7-133">You could use `RoleEnvironment.getConfigurationSettings` tooretrieve hello SendGrid username and password from your deployment's configuration settings, instead of using hello web form tooretrieve those values.</span></span> <span data-ttu-id="bc4b7-134">Per informazioni su hello `RoleEnvironment` classe, vedere [Using hello libreria di Runtime del servizio di Azure in JSP](http://msdn.microsoft.com/library/windowsazure/hh690948) e la documentazione di pacchetto di Runtime del servizio Azure hello in <http://dl.windowsazure.com/javadoc>.</span><span class="sxs-lookup"><span data-stu-id="bc4b7-134">For information about hello `RoleEnvironment` class, see [Using hello Azure Service Runtime Library in JSP](http://msdn.microsoft.com/library/windowsazure/hh690948) and hello Azure Service Runtime package documentation at <http://dl.windowsazure.com/javadoc>.</span></span>
* <span data-ttu-id="bc4b7-135">Per ulteriori informazioni sull'uso di SendGrid in linguaggio, vedere [come toosend di posta elettronica usando SendGrid da Java](store-sendgrid-java-how-to-send-email.md).</span><span class="sxs-lookup"><span data-stu-id="bc4b7-135">For more information about using SendGrid in Java, see [How toosend email using SendGrid from Java](store-sendgrid-java-how-to-send-email.md).</span></span>

[emailform]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailform.jpg
[emailsent]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailSent.jpg
[emailresult]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaResult.jpg
