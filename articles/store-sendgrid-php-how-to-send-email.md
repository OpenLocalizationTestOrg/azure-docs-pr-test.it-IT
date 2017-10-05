---
title: Come usare il servizio di e-mail SendGrid (PHP) | Microsoft Docs
description: Informazioni su come inviare messaggi di posta elettronica con il servizio di posta elettronica SendGrid disponibile in Azure. Gli esempi di codice sono scritti in PHP.
documentationcenter: php
services: 
manager: sendgrid
editor: mollybos
author: thinkingserious
ms.assetid: 51a9928a-4c9e-4b0a-aca8-9a408aeb6f47
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 10/30/2014
ms.author: elmer.thomas@sendgrid.com; erika.berkland@sendgrid.com; vibhork; matt.bernier@sendgrid.com
ms.openlocfilehash: 523b986f66a2e48685e9707903194856f0dcf4a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-sendgrid-email-service-from-php"></a><span data-ttu-id="4a6b3-104">Come usare il servizio di posta elettronica SendGrid da PHP</span><span class="sxs-lookup"><span data-stu-id="4a6b3-104">How to Use the SendGrid Email Service from PHP</span></span>
<span data-ttu-id="4a6b3-105">Questa guida illustra come eseguire attività di programmazione comuni con il servizio di posta elettronica SendGrid in Azure.</span><span class="sxs-lookup"><span data-stu-id="4a6b3-105">This guide demonstrates how to perform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="4a6b3-106">Gli esempi sono scritti in PHP.</span><span class="sxs-lookup"><span data-stu-id="4a6b3-106">The samples are written in PHP.</span></span>
<span data-ttu-id="4a6b3-107">Gli scenari presentati includono la **creazione dei messaggi di posta elettronica**, l'**invio di messaggi di posta elettronica**, e l'**aggiunta di allegati**.</span><span class="sxs-lookup"><span data-stu-id="4a6b3-107">The scenarios covered include **constructing email**, **sending email**, and **adding attachments**.</span></span> <span data-ttu-id="4a6b3-108">Per altre informazioni su SendGrid e sull'invio della posta elettronica, vedere la sezione [Passaggi successivi](#next-steps) .</span><span class="sxs-lookup"><span data-stu-id="4a6b3-108">For more information on SendGrid and sending email, see the [Next Steps](#next-steps) section.</span></span>

## <a name="what-is-the-sendgrid-email-service"></a><span data-ttu-id="4a6b3-109">Informazioni sul servizio di posta elettronica SendGrid</span><span class="sxs-lookup"><span data-stu-id="4a6b3-109">What is the SendGrid Email Service?</span></span>
<span data-ttu-id="4a6b3-110">SendGrid è un [servizio di posta elettronica basato sul cloud] che offre [recapito affidabile di messaggi di posta elettronica transazionali], scalabilità e analisi in tempo reale, oltre ad API flessibili che agevolano l'integrazione personalizzata.</span><span class="sxs-lookup"><span data-stu-id="4a6b3-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="4a6b3-111">Gli scenari di utilizzo comuni di SendGrid includono:</span><span class="sxs-lookup"><span data-stu-id="4a6b3-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="4a6b3-112">Invio automatico di ricevute ai clienti</span><span class="sxs-lookup"><span data-stu-id="4a6b3-112">Automatically sending receipts to customers</span></span>
* <span data-ttu-id="4a6b3-113">Amministrazione di liste di distribuzione per l'invio mensile ai clienti di volantini elettronici e offerte speciali</span><span class="sxs-lookup"><span data-stu-id="4a6b3-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="4a6b3-114">Raccolta di metriche in tempo reale per elementi quali indirizzi di posta elettronica bloccati e velocità di risposta al cliente</span><span class="sxs-lookup"><span data-stu-id="4a6b3-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="4a6b3-115">Generazione di report per agevolare l'identificazione delle tendenze</span><span class="sxs-lookup"><span data-stu-id="4a6b3-115">Generating reports to help identify trends</span></span>
* <span data-ttu-id="4a6b3-116">Inoltro di richieste dei clienti</span><span class="sxs-lookup"><span data-stu-id="4a6b3-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="4a6b3-117">Notifiche di posta elettronica dall'applicazione</span><span class="sxs-lookup"><span data-stu-id="4a6b3-117">Email notifications from your application</span></span>

<span data-ttu-id="4a6b3-118">Per altre informazioni, vedere [https://sendgrid.com][https://sendgrid.com].</span><span class="sxs-lookup"><span data-stu-id="4a6b3-118">For more information, see [https://sendgrid.com][https://sendgrid.com].</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="4a6b3-119">Creazione di un account SendGrid</span><span class="sxs-lookup"><span data-stu-id="4a6b3-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="using-sendgrid-from-your-php-application"></a><span data-ttu-id="4a6b3-120">Utilizzo di SendGrid dall'applicazione PHP</span><span class="sxs-lookup"><span data-stu-id="4a6b3-120">Using SendGrid from your PHP Application</span></span>
<span data-ttu-id="4a6b3-121">L'uso di SendGrid in un'applicazione PHP di Azure non richiede speciali attività di configurazione o di scrittura del codice.</span><span class="sxs-lookup"><span data-stu-id="4a6b3-121">Using SendGrid in an Azure PHP application requires no special configuration or coding.</span></span> <span data-ttu-id="4a6b3-122">Poiché SendGrid è un servizio, è possibile accedervi da un'applicazione cloud esattamente come da un'applicazione locale.</span><span class="sxs-lookup"><span data-stu-id="4a6b3-122">Because SendGrid is a service, it can be accessed in exactly the same way from a cloud application as it can from an on-premises application.</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="4a6b3-123">Procedura: Inviare un messaggio di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="4a6b3-123">How to: Send an Email</span></span>
<span data-ttu-id="4a6b3-124">È possibile inviare un messaggio di posta elettronica tramite SMTP o con l'API Web di SendGrid.</span><span class="sxs-lookup"><span data-stu-id="4a6b3-124">You can send email using either SMTP or the Web API provided by SendGrid.</span></span>

### <a name="smtp-api"></a><span data-ttu-id="4a6b3-125">API SMTP</span><span class="sxs-lookup"><span data-stu-id="4a6b3-125">SMTP API</span></span>
<span data-ttu-id="4a6b3-126">Per inviare un messaggio di posta elettronica tramite l'API SMTP di SendGrid, usare *Swift Mailer*, una libreria basata su componenti per l'invio di messaggi di posta elettronica da applicazioni PHP.</span><span class="sxs-lookup"><span data-stu-id="4a6b3-126">To send email using the SendGrid SMTP API, use *Swift Mailer*, a component-based library for sending emails from PHP applications.</span></span> <span data-ttu-id="4a6b3-127">Per scaricare la libreria *Swift Mailer*, accedere alla pagina [http://swiftmailer.org/download][http://swiftmailer.org/download] v5.3.0. Usare [Composer] per installare Swift Mailer.</span><span class="sxs-lookup"><span data-stu-id="4a6b3-127">You can download the *Swift Mailer* library from [http://swiftmailer.org/download][http://swiftmailer.org/download] v5.3.0 (use [Composer] to install Swift Mailer).</span></span> <span data-ttu-id="4a6b3-128">L'invio di e-mail tramite la libreria prevede la creazione di istanze delle classi <span class="auto-style2">Swift\_SmtpTransport</span>, <span class="auto-style2">Swift\_Mailer</span> e <span class="auto-style2">Swift\_Message</span>, l'impostazione delle proprietà appropriate e la chiamata del metodo <span class="auto-style2">Swift\_Mailer::send</span>.</span><span class="sxs-lookup"><span data-stu-id="4a6b3-128">Sending email with the library involves creating instances of the <span class="auto-style2">Swift\_SmtpTransport</span>, <span class="auto-style2">Swift\_Mailer</span>, and <span class="auto-style2">Swift\_Message</span> classes, setting the appropriate properties, and calling the <span class="auto-style2">Swift\_Mailer::send</span> method.</span></span>

    <?php
     include_once "vendor/autoload.php";
     /*
      * Create the body of the message (a plain-text and an HTML version).
      * $text is your plain-text email
      * $html is your html version of the email
      * If the receiver is able to view html emails then only the html
      * email will be displayed
      */
     $text = "Hi!\nHow are you?\n";
     $html = "<html>
           <head></head>
           <body>
               <p>Hi!<br>
                   How are you?<br>
               </p>
           </body>
           </html>";
     // This is your From email address
     $from = array('someone@example.com' => 'Name To Appear');
     // Email recipients
     $to = array(
           'john@contoso.com'=>'Destination 1 Name',
           'anna@contoso.com'=>'Destination 2 Name'
     );
     // Email subject
     $subject = 'Example PHP Email';

     // Login credentials
     $username = 'yoursendgridusername';
     $password = 'yourpassword';

     // Setup Swift mailer parameters
     $transport = Swift_SmtpTransport::newInstance('smtp.sendgrid.net', 587);
     $transport->setUsername($username);
     $transport->setPassword($password);
     $swift = Swift_Mailer::newInstance($transport);

     // Create a message (subject)
     $message = new Swift_Message($subject);

     // attach the body of the email
     $message->setFrom($from);
     $message->setBody($html, 'text/html');
     $message->setTo($to);
     $message->addPart($text, 'text/plain');

     // send message
     if ($recipients = $swift->send($message, $failures))
     {
         // This will let us know how many users received this message
         echo 'Message sent out to '.$recipients.' users';
     }
     // something went wrong =(
     else
     {
         echo "Something went wrong - ";
         print_r($failures);
     }

### <a name="web-api"></a><span data-ttu-id="4a6b3-129">API Web</span><span class="sxs-lookup"><span data-stu-id="4a6b3-129">Web API</span></span>
<span data-ttu-id="4a6b3-130">Usare la [funzione curl][curl function] di PHP per inviare messaggi di posta elettronica tramite l'API Web SendGrid.</span><span class="sxs-lookup"><span data-stu-id="4a6b3-130">Use PHP's [curl function][curl function] to send email using the SendGrid Web API.</span></span>

    <?php

     $url = 'https://api.sendgrid.com/';
     $user = 'USERNAME';
     $pass = 'PASSWORD';

     $params = array(
          'api_user' => $user,
          'api_key' => $pass,
          'to' => 'john@contoso.com',
          'subject' => 'testing from curl',
          'html' => 'testing body',
          'text' => 'testing body',
          'from' => 'anna@contoso.com',
       );

     $request = $url.'api/mail.send.json';

     // Generate curl request
     $session = curl_init($request);

     // Tell curl to use HTTP POST
     curl_setopt ($session, CURLOPT_POST, true);

     // Tell curl that this is the body of the POST
     curl_setopt ($session, CURLOPT_POSTFIELDS, $params);

     // Tell curl not to return headers, but do return the response
     curl_setopt($session, CURLOPT_HEADER, false);
     curl_setopt($session, CURLOPT_RETURNTRANSFER, true);

     // obtain response
     $response = curl_exec($session);
     curl_close($session);

     // print everything out
     print_r($response);

<span data-ttu-id="4a6b3-131">L'API Web di SendGrid è molto simile a un'API REST, sebbene non sia una vera API RESTful poiché nella maggior parte delle chiamate è possibile indifferentemente i verbi GET e POST.</span><span class="sxs-lookup"><span data-stu-id="4a6b3-131">SendGrid's Web API is very similar to a REST API, though it is not truly a RESTful API since, in most calls, both GET and POST verbs can be used interchangeably.</span></span>

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="4a6b3-132">Procedura: Aggiungere un allegato</span><span class="sxs-lookup"><span data-stu-id="4a6b3-132">How to: Add an Attachment</span></span>
### <a name="smtp-api"></a><span data-ttu-id="4a6b3-133">API SMTP</span><span class="sxs-lookup"><span data-stu-id="4a6b3-133">SMTP API</span></span>
<span data-ttu-id="4a6b3-134">L'invio di un allegato tramite l'API SMTP prevede una riga di codice aggiuntiva nello script di esempio per l'invio di un messaggio di posta elettronica con Swift Mailer.</span><span class="sxs-lookup"><span data-stu-id="4a6b3-134">Sending an attachment using the SMTP API involves one additional line of code to the example script for sending an email with Swift Mailer.</span></span>

    <?php
     include_once "vendor/autoload.php";
     /*
      * Create the body of the message (a plain-text and an HTML version).
      * $text is your plain-text email
      * $html is your html version of the email
      * If the reciever is able to view html emails then only the html
      * email will be displayed
      */
     $text = "Hi!\nHow are you?\n";
      $html = "<html>
          <head></head>
          <body>
             <p>Hi!<br>
                How are you?<br>
             </p>
          </body>
          </html>";

     // This is your From email address
     $from = array('someone@example.com' => 'Name To Appear');

     // Email recipients
     $to = array(
          'john@contoso.com'=>'Destination 1 Name',
          'anna@contoso.com'=>'Destination 2 Name'
     );
     // Email subject
     $subject = 'Example PHP Email';

     // Login credentials
     $username = 'yoursendgridusername';
     $password = 'yourpassword';

     // Setup Swift mailer parameters
     $transport = Swift_SmtpTransport::newInstance('smtp.sendgrid.net', 587);
     $transport->setUsername($username);
     $transport->setPassword($password);
     $swift = Swift_Mailer::newInstance($transport);

     // Create a message (subject)
     $message = new Swift_Message($subject);

     // attach the body of the email
     $message->setFrom($from);
     $message->setBody($html, 'text/html');
     $message->setTo($to);
     $message->addPart($text, 'text/plain');
     $message->attach(Swift_Attachment::fromPath("path\to\file")->setFileName("file_name"));

     // send message
     if ($recipients = $swift->send($message, $failures))
     {
          // This will let us know how many users received this message
          echo 'Message sent out to '.$recipients.' users';
     }
     // something went wrong =(
     else
     {
          echo "Something went wrong - ";
          print_r($failures);
     }

<span data-ttu-id="4a6b3-135">Di seguito è riportata la riga di codice aggiuntiva:</span><span class="sxs-lookup"><span data-stu-id="4a6b3-135">The additional line of code is as follows:</span></span>

     $message->attach(Swift_Attachment::fromPath("path\to\file")->setFileName('file_name'));

<span data-ttu-id="4a6b3-136">Questa riga di codice chiama il metodo attach sull'oggetto <span class="auto-style2">Swift\_Message</span> e usa il metodo statico <span class="auto-style2">fromPath</span> sulla classe <span class="auto-style2">Swift\_Attachment</span> per recuperare e allegare un file a un messaggio.</span><span class="sxs-lookup"><span data-stu-id="4a6b3-136">This line of code calls the attach method on the <span class="auto-style2">Swift\_Message</span> object and uses static method <span class="auto-style2">fromPath</span> on the <span class="auto-style2">Swift\_Attachment</span> class to get and attach a file to a message.</span></span>

### <a name="web-api"></a><span data-ttu-id="4a6b3-137">API Web</span><span class="sxs-lookup"><span data-stu-id="4a6b3-137">Web API</span></span>
<span data-ttu-id="4a6b3-138">L'invio di un allegato tramite l'API Web è molto simile all'invio di un messaggio di posta elettronica con l'API Web.</span><span class="sxs-lookup"><span data-stu-id="4a6b3-138">Sending an attachment using the Web API is very similar to sending an email using the Web API.</span></span> <span data-ttu-id="4a6b3-139">Si noti tuttavia che nell'esempio riportato di seguito, il parametro array deve contenere questo elemento:</span><span class="sxs-lookup"><span data-stu-id="4a6b3-139">However, note that in the example that follows, the parameter array must contain this element:</span></span>

    'files['.$fileName.']' => '@'.$filePath.'/'.$fileName

<span data-ttu-id="4a6b3-140">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a6b3-140">Example:</span></span>

    <?php

     $url = 'https://api.sendgrid.com/';
     $user = 'USERNAME';
     $pass = 'PASSWORD';

     $fileName = 'myfile';
     $filePath = dirname(__FILE__);

     $params = array(
         'api_user' => $user,
         'api_key' => $pass,
         'to' =>'john@contoso.com',
         'subject' => 'test of file sends',
         'html' => '<p> the HTML </p>',
         'text' => 'the plain text',
         'from' => 'anna@contoso.com',
         'files['.$fileName.']' => '@'.$filePath.'/'.$fileName
     );

     print_r($params);

     $request = $url.'api/mail.send.json';

     // Generate curl request
     $session = curl_init($request);

     // Tell curl to use HTTP POST
     curl_setopt ($session, CURLOPT_POST, true);

     // Tell curl that this is the body of the POST
     curl_setopt ($session, CURLOPT_POSTFIELDS, $params);

     // Tell curl not to return headers, but do return the response
     curl_setopt($session, CURLOPT_HEADER, false);
     curl_setopt($session, CURLOPT_RETURNTRANSFER, true);

     // obtain response
     $response = curl_exec($session);
     curl_close($session);

     // print everything out
     print_r($response);

## <a name="how-to-use-filters-to-enable-footers-tracking-and-analytics"></a><span data-ttu-id="4a6b3-141">Procedura: Usare filtri per abilitare piè di pagina, monitoraggio e analisi</span><span class="sxs-lookup"><span data-stu-id="4a6b3-141">How to: Use Filters to Enable Footers, Tracking, and Analytics</span></span>
<span data-ttu-id="4a6b3-142">SendGrid fornisce funzionalità di posta elettronica aggiuntive attraverso l'uso di "filtri".</span><span class="sxs-lookup"><span data-stu-id="4a6b3-142">SendGrid provides additional email functionality through the use of 'filters'.</span></span> <span data-ttu-id="4a6b3-143">Si tratta di impostazioni che è possibile aggiungere a un messaggio di posta elettronica per abilitare funzionalità specifiche, ad esempio il monitoraggio del clic, Google Analytics, il monitoraggio delle sottoscrizioni e così via.</span><span class="sxs-lookup"><span data-stu-id="4a6b3-143">These are settings that can be added to an email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span>

<span data-ttu-id="4a6b3-144">È possibile applicare filtri a un messaggio usando la proprietà filters.</span><span class="sxs-lookup"><span data-stu-id="4a6b3-144">Filters can be applied to a message by using the filters property.</span></span> <span data-ttu-id="4a6b3-145">Ogni filtro è specificato da un hash che contiene impostazioni specifiche del filtro.</span><span class="sxs-lookup"><span data-stu-id="4a6b3-145">Each filter is specified by a hash containing filter-specific settings.</span></span> <span data-ttu-id="4a6b3-146">Nell'esempio seguente viene abilitato il filtro piè di pagina e viene specificato un messaggio di testo che verrà aggiunto nella parte inferiore del messaggio di posta elettronica:</span><span class="sxs-lookup"><span data-stu-id="4a6b3-146">The following example enables the footer filter and specifies a text message that will be appended to the bottom of the email message.</span></span>
<span data-ttu-id="4a6b3-147">Per questo esempio si userà la [libreria sendgrid-php].</span><span class="sxs-lookup"><span data-stu-id="4a6b3-147">For this example we will use [sendgrid-php library].</span></span>
<span data-ttu-id="4a6b3-148">Usare [Composer] per installare la libreria:</span><span class="sxs-lookup"><span data-stu-id="4a6b3-148">Use [Composer] to install library:</span></span>

    php composer.phar require sendgrid/sendgrid 2.1.1

<span data-ttu-id="4a6b3-149">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4a6b3-149">Example:</span></span>    

    <?php
     /*
      * This example is used for sendgrid-php V2.1.1 (https://github.com/sendgrid/sendgrid-php/tree/v2.1.1)
      */
     include "vendor/autoload.php";

     $email = new SendGrid\Email();
     // The list of addresses this message will be sent to
     // [This list is used for sending multiple emails using just ONE request to SendGrid]
     $toList = array('john@contoso.com', 'anna@contoso.com');

     // Specify the names of the recipients
     $nameList = array('Name 1', 'Name 2');

     // Used as an example of variable substitution
     $timeList = array('4 PM', '5 PM');

     // Set all of the above variables
     $email->setTos($toList);
     $email->addSubstitution('-name-', $nameList);
     $email->addSubstitution('-time-', $timeList);

     // Specify that this is an initial contact message
     $email->addCategory("initial");

     // You can optionally setup individual filters here, in this example, we have
     // enabled the footer filter
     $email->addFilter('footer', 'enable', 1);
     $email->addFilter('footer', "text/plain", "Thank you for your business");
     $email->addFilter('footer', "text/html", "Thank you for your business");

     // The subject of your email
     $subject = 'Example SendGrid Email';

     // Where is this message coming from. For example, this message can be from
     // support@yourcompany.com, info@yourcompany.com
     $from = 'someone@example.com';

     // If you do not specify a sender list above, you can specifiy the user here. If
     // a sender list IS specified above, this email address becomes irrelevant.
     $to = 'john@contoso.com';

     # Create the body of the message (a plain-text and an HTML version).
     # text is your plain-text email
     # html is your html version of the email
     # if the receiver is able to view html emails then only the html
     # email will be displayed

     /*
      * Note the variable substitution here =)
      */
     $text = "
     Hello -name-,
     Thank you for your interest in our products. We have set up an appointment to call you at -time- EST to discuss your needs in more detail.
     Regards,
     Fred";

     $html = "
     <html>
     <head></head>
     <body>
     <p>Hello -name-,<br>
     Thank you for your interest in our products. We have set up an appointment
     to call you at -time- EST to discuss your needs in more detail.

     Regards,

     Fred<br>
     </p>
     </body>
     </html>";

     // set subject
     $email->setSubject($subject);

     // attach the body of the email
     $email->setFrom($from);
     $email->setHtml($html);
     $email->addTo($to);
     $email->setText($text);

     // Your SendGrid account credentials
     $username = 'sendgridusername@yourdomain.com';
     $password = 'example';

     // Create SendGrid object
     $sendgrid = new SendGrid($username, $password);

     // send message
     $response = $sendgrid->send($email);

     print_r($response);

## <a name="next-steps"></a><span data-ttu-id="4a6b3-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4a6b3-150">Next Steps</span></span>
<span data-ttu-id="4a6b3-151">A questo punto, dopo aver appreso le nozioni di base del servizio di posta elettronica SendGrid, usare i collegamenti seguenti per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="4a6b3-151">Now that you've learned the basics of the SendGrid Email service, follow these links to learn more.</span></span>

* <span data-ttu-id="4a6b3-152">Documentazione relativa a SendGrid: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="4a6b3-152">SendGrid documentation: <https://sendgrid.com/docs></span></span>
* <span data-ttu-id="4a6b3-153">Libreria PHP di SendGrid: <https://github.com/sendgrid/sendgrid-php></span><span class="sxs-lookup"><span data-stu-id="4a6b3-153">SendGrid PHP library: <https://github.com/sendgrid/sendgrid-php></span></span>
* <span data-ttu-id="4a6b3-154">Offerta speciale SendGrid per i clienti di Azure: <https://sendgrid.com/windowsazure.html></span><span class="sxs-lookup"><span data-stu-id="4a6b3-154">SendGrid special offer for Azure customers: <https://sendgrid.com/windowsazure.html></span></span>

<span data-ttu-id="4a6b3-155">Per ulteriori informazioni, vedere anche il [Centro per sviluppatori di PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="4a6b3-155">For more information, see also the [PHP Developer Center](/develop/php/).</span></span>

[https://sendgrid.com]: https://sendgrid.com
[https://sendgrid.com/transactional-email/pricing]: https://sendgrid.com/transactional-email/pricing
[special offer]: https://www.sendgrid.com/windowsazure.html
[Packaging and Deploying PHP Applications for Azure]: http://msdn.microsoft.com/library/windowsazure/hh674499(v=VS.103).aspx
[http://swiftmailer.org/download]: http://swiftmailer.org/download
[curl function]: http://php.net/curl
<span data-ttu-id="4a6b3-156">[servizio di posta elettronica basato sul cloud]: https://sendgrid.com/email-solutions</span><span class="sxs-lookup"><span data-stu-id="4a6b3-156">[cloud-based email service]: https://sendgrid.com/email-solutions</span></span>
<span data-ttu-id="4a6b3-157">[recapito affidabile di messaggi di posta elettronica transazionali]: https://sendgrid.com/transactional-email</span><span class="sxs-lookup"><span data-stu-id="4a6b3-157">[transactional email delivery]: https://sendgrid.com/transactional-email</span></span>
<span data-ttu-id="4a6b3-158">[libreria sendgrid-php]: https://github.com/sendgrid/sendgrid-php/tree/v2.1.1</span><span class="sxs-lookup"><span data-stu-id="4a6b3-158">[sendgrid-php library]: https://github.com/sendgrid/sendgrid-php/tree/v2.1.1</span></span>
<span data-ttu-id="4a6b3-159">[Composer]: https://getcomposer.org/download/</span><span class="sxs-lookup"><span data-stu-id="4a6b3-159">[Composer]: https://getcomposer.org/download/</span></span>
