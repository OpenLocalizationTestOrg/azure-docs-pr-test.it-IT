---
title: store-sendgrid-java-how-to-send-email-example
description: Come inviare messaggi di posta elettronica usando SendGrid da Java in una distribuzione Azure
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
ms.openlocfilehash: d80d7d9c54bad12a4d26d8623eeccdf9bc2a743a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-send-email-using-sendgrid-from-java-in-an-azure-deployment"></a><span data-ttu-id="388f4-103">Come inviare messaggi di posta elettronica usando SendGrid da Java in una distribuzione Azure</span><span class="sxs-lookup"><span data-stu-id="388f4-103">How to Send Email Using SendGrid from Java in an Azure Deployment</span></span>
<span data-ttu-id="388f4-104">L'esempio seguente illustra come è possibile usare SendGrid per inviare messaggi di posta elettronica da una pagina Web ospitata in Azure.</span><span class="sxs-lookup"><span data-stu-id="388f4-104">The following example shows you how you can use SendGrid to send emails from a web page hosted in Azure.</span></span> <span data-ttu-id="388f4-105">L'applicazione risultante chiederà all'utente di inserire i valori relativi al messaggio di posta elettronica, come illustrato nella schermata seguente.</span><span class="sxs-lookup"><span data-stu-id="388f4-105">The resulting application will prompt the user for email values, as shown in the following screen shot.</span></span>

![Modulo per la posta elettronica][emailform]

<span data-ttu-id="388f4-107">Il messaggio di posta elettronica finale dovrebbe essere simile a quello riportato nella schermata seguente.</span><span class="sxs-lookup"><span data-stu-id="388f4-107">The resulting email will look similar to the following screen shot.</span></span>

![Messaggio di posta elettronica][emailsent]

<span data-ttu-id="388f4-109">Per usare il codice in questo argomento è necessario eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="388f4-109">You'll need to do the following to use the code in this topic:</span></span>

1. <span data-ttu-id="388f4-110">Ottenere i file JAR di javax.mail, ad esempio da <http://www.oracle.com/technetwork/java/javamail/index.html>.</span><span class="sxs-lookup"><span data-stu-id="388f4-110">Obtain the javax.mail JARs, for example from <http://www.oracle.com/technetwork/java/javamail/index.html>.</span></span>
2. <span data-ttu-id="388f4-111">Aggiungere i file JAR al percorso di compilazione Java.</span><span class="sxs-lookup"><span data-stu-id="388f4-111">Add the JARs to your Java build path.</span></span>
3. <span data-ttu-id="388f4-112">Se si usa Eclipse per creare l'applicazione Java, è possibile includere le librerie SendGrid nel file di distribuzione dell'applicazione (WAR) usando l'assembly di distribuzione di Eclipse.</span><span class="sxs-lookup"><span data-stu-id="388f4-112">If you are using Eclipse to create this Java application, you can include the SendGrid libraries in your application deployment file (WAR) using Eclipse's deployment assembly feature.</span></span> <span data-ttu-id="388f4-113">Se non si usa Eclipse per creare l'applicazione Java, verificare che le librerie siano incluse nello stesso ruolo di Azure dell'applicazione Java e che sia stato aggiunto al percorso della classe dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="388f4-113">If you are not using Eclipse to create this Java application, ensure the libraries are included within the same Azure role as your Java application, and added to the class path of your application.</span></span>

<span data-ttu-id="388f4-114">Per poter inviare i messaggi di posta elettronica è inoltre necessario disporre di un nome utente e una password di SendGrid.</span><span class="sxs-lookup"><span data-stu-id="388f4-114">You must also have your own SendGrid username and password, to be able to send the email.</span></span> <span data-ttu-id="388f4-115">Per iniziare a usare SendGrid, vedere [Come inviare messaggi di posta elettronica usando SendGrid da Java](store-sendgrid-java-how-to-send-email.md).</span><span class="sxs-lookup"><span data-stu-id="388f4-115">To get started with SendGrid, see [How to send email using SendGrid from Java](store-sendgrid-java-how-to-send-email.md).</span></span>

<span data-ttu-id="388f4-116">Se non si usa Eclipse, è inoltre consigliabile consultare l'argomento [Creazione di un'applicazione Hello World per Azure in Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944)o acquisire familiarità con altre tecniche per l'hosting di applicazioni Java in Azure.</span><span class="sxs-lookup"><span data-stu-id="388f4-116">Additionally, familiarity with the information at [Creating a Hello World Application for Azure in Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944), or with other techniques for hosting Java applications in Azure if you are not using Eclipse, is highly recommended.</span></span>

## <a name="create-a-web-form-for-sending-email"></a><span data-ttu-id="388f4-117">Creare un modulo Web per l'invio di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="388f4-117">Create a web form for sending email</span></span>
<span data-ttu-id="388f4-118">Nel codice seguente viene illustrato come creare un modulo Web per recuperare i dati utente per l'invio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="388f4-118">The following code shows how to create a web form to retrieve user data for sending email.</span></span> <span data-ttu-id="388f4-119">Per gli scopi di questa esercitazione il file JSP è denominato **emailform.jsp**.</span><span class="sxs-lookup"><span data-stu-id="388f4-119">For purposes of this content, the JSP file is named **emailform.jsp**.</span></span>

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

## <a name="create-the-code-to-send-the-email"></a><span data-ttu-id="388f4-120">Creare il codice per l'invio della posta elettronica</span><span class="sxs-lookup"><span data-stu-id="388f4-120">Create the code to send the email</span></span>
<span data-ttu-id="388f4-121">Il codice seguente, chiamato quando si completa il modulo in emailform.jsp, crea il messaggio di posta elettronica e lo invia.</span><span class="sxs-lookup"><span data-stu-id="388f4-121">The following code, which is called when you complete the form in emailform.jsp, creates the email message and sends it.</span></span> <span data-ttu-id="388f4-122">Per gli scopi di questa esercitazione il file JSP è denominato **sendemail.jsp**.</span><span class="sxs-lookup"><span data-stu-id="388f4-122">For purposes of this content, the JSP file is named **sendemail.jsp**.</span></span>

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

         // The SendGrid SMTP server.
         String SMTP_HOST_NAME = "smtp.sendgrid.net";

         Properties properties;

         properties = new Properties();

         // Specify SMTP values.
         properties.put("mail.transport.protocol", "smtp");
         properties.put("mail.smtp.host", SMTP_HOST_NAME);
         properties.put("mail.smtp.port", 587);
         properties.put("mail.smtp.auth", "true");

         // Display the email fields entered by the user. 
         out.println("Value entered for email Subject: " + request.getParameter("emailSubject") + "<br/>");        
         out.println("Value entered for email      To: " + request.getParameter("emailTo") + "<br/>");
         out.println("Value entered for email    From: " + request.getParameter("emailFrom") + "<br/>");
         out.println("Value entered for email    Text: " + "<br/>" + request.getParameter("emailText") + "<br/>");

         // Create the authenticator object.
         Authenticator authenticator = new SMTPAuthenticator();

         // Create the mail session object.
         Session mailSession;
         mailSession = Session.getDefaultInstance(properties, authenticator);

         // Display debug information to stdout, useful when using the
         // compute emulator during development.
         mailSession.setDebug(true);

         // Create the message and message part objects.
         MimeMessage message;
         Multipart multipart;
         MimeBodyPart messagePart; 

         message = new MimeMessage(mailSession);

         multipart = new MimeMultipart("alternative");
         messagePart = new MimeBodyPart();
         messagePart.setContent(request.getParameter("emailText"), "text/html");
         multipart.addBodyPart(messagePart);            

         // Specify the email To, From, Subject and Content. 
         message.setFrom(new InternetAddress(request.getParameter("emailFrom")));
         message.addRecipient(Message.RecipientType.TO, new InternetAddress(request.getParameter("emailTo")));
         message.setSubject(request.getParameter("emailSubject")); 
         message.setContent(multipart);

         // Uncomment the following if you want to add a footer.
         // message.addHeader("X-SMTPAPI", "{\"filters\": {\"footer\": {\"settings\": {\"enable\":1,\"text/html\": \"<html>This is my <b>email footer</b>.</html>\"}}}}");

         // Uncomment the following if you want to enable click tracking.
         // message.addHeader("X-SMTPAPI", "{\"filters\": {\"clicktrack\": {\"settings\": {\"enable\":1}}}}");

         Transport transport;
         transport = mailSession.getTransport();
         // Connect the transport object.
         transport.connect();
         // Send the message.
         transport.sendMessage(message,  message.getRecipients(Message.RecipientType.TO));
         // Close the connection.
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

<span data-ttu-id="388f4-123">Oltre a inviare la posta elettronica emailform.jsp fornisce un risultato all'utente. Nella schermata di seguito viene visualizzato un esempio:</span><span class="sxs-lookup"><span data-stu-id="388f4-123">In addition to sending the email, emailform.jsp provides a result for the user; an example is the following screen shot:</span></span>

![Risultato invio posta elettronica][emailresult]

## <a name="next-steps"></a><span data-ttu-id="388f4-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="388f4-125">Next steps</span></span>
<span data-ttu-id="388f4-126">Distribuire l'applicazione sull'emulatore di calcolo e, dall'interno di un browser, eseguire emailform.jsp, immettere i valori nel modulo, fare clic su **Send this email**e quindi visualizzare i risultati in sendemail.jsp.</span><span class="sxs-lookup"><span data-stu-id="388f4-126">Deploy your application to the compute emulator and within a browser run emailform.jsp, enter values in the form, click **Send this email**, and then see results in sendemail.jsp.</span></span>

<span data-ttu-id="388f4-127">Questo codice ha lo scopo di illustrare come usare SendGrid con Java in Azure.</span><span class="sxs-lookup"><span data-stu-id="388f4-127">This code was provided to show you how to use SendGrid in Java on Azure.</span></span> <span data-ttu-id="388f4-128">Prima di eseguire la distribuzione in Azure in produzione, può essere necessario aggiungere ulteriori funzionalità per la gestione degli errori o per altri scopi.</span><span class="sxs-lookup"><span data-stu-id="388f4-128">Before deploying to Azure in production, you may want to add more error handling or other features.</span></span> <span data-ttu-id="388f4-129">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="388f4-129">For example:</span></span> 

* <span data-ttu-id="388f4-130">Anziché usare un modulo Web, è possibile usare l'archiviazione BLOB o un database SQL di Azure per l'archiviazione di indirizzi e messaggi di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="388f4-130">You could use Azure storage blobs or SQL Database to store email addresses and email messages, instead of using a web form.</span></span> <span data-ttu-id="388f4-131">Per informazioni sull'uso dei BLOB di archiviazione di Azure in Java, vedere [Come usare il servizio di archiviazione BLOB da Java](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/).</span><span class="sxs-lookup"><span data-stu-id="388f4-131">For information about using Azure storage blobs in Java, see [How to Use the Blob Storage Service from Java](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/).</span></span> <span data-ttu-id="388f4-132">Per informazioni sull'uso dei database SQL in Java, vedere [Uso di database SQL in Java](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/).</span><span class="sxs-lookup"><span data-stu-id="388f4-132">For information about using SQL Database in Java, see [Using SQL Database in Java](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/).</span></span>
* <span data-ttu-id="388f4-133">È possibile usare `RoleEnvironment.getConfigurationSettings` per recuperare il nome utente e la password di SendGrid dalle impostazioni di configurazione della distribuzione, anziché usare il modulo Web per recuperare questi valori.</span><span class="sxs-lookup"><span data-stu-id="388f4-133">You could use `RoleEnvironment.getConfigurationSettings` to retrieve the SendGrid username and password from your deployment's configuration settings, instead of using the web form to retrieve those values.</span></span> <span data-ttu-id="388f4-134">Per informazioni sulla classe `RoleEnvironment`, vedere [Uso della libreria di runtime del servizio Azure in JSP](http://msdn.microsoft.com/library/windowsazure/hh690948) e la documentazione sul pacchetto della libreria di runtime del servizio Azure all'indirizzo <http://dl.windowsazure.com/javadoc>.</span><span class="sxs-lookup"><span data-stu-id="388f4-134">For information about the `RoleEnvironment` class, see [Using the Azure Service Runtime Library in JSP](http://msdn.microsoft.com/library/windowsazure/hh690948) and the Azure Service Runtime package documentation at <http://dl.windowsazure.com/javadoc>.</span></span>
* <span data-ttu-id="388f4-135">Per altre informazioni sull'uso di SendGrid in Java, vedere [Come inviare messaggi di posta elettronica usando SendGrid da Java](store-sendgrid-java-how-to-send-email.md).</span><span class="sxs-lookup"><span data-stu-id="388f4-135">For more information about using SendGrid in Java, see [How to send email using SendGrid from Java](store-sendgrid-java-how-to-send-email.md).</span></span>

[emailform]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailform.jpg
[emailsent]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailSent.jpg
[emailresult]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaResult.jpg
