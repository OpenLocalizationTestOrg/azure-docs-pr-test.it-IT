---
title: hello toouse aaaHow SendGrid servizio di posta elettronica (PHP) | Documenti Microsoft
description: Informazioni su come inviare posta elettronica con il servizio di posta elettronica SendGrid hello in Azure. Gli esempi di codice sono scritti in PHP.
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
ms.openlocfilehash: 0076e56dc185cb8f52e629395e7d2c143cb5cfa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-sendgrid-email-service-from-php"></a><span data-ttu-id="d3ff9-104">Come tooUse hello SendGrid servizio di posta elettronica da PHP</span><span class="sxs-lookup"><span data-stu-id="d3ff9-104">How tooUse hello SendGrid Email Service from PHP</span></span>
<span data-ttu-id="d3ff9-105">Questa guida illustra come attività di programmazione comuni tooperform con SendGrid hello posta elettronica del servizio in Azure.</span><span class="sxs-lookup"><span data-stu-id="d3ff9-105">This guide demonstrates how tooperform common programming tasks with hello SendGrid email service on Azure.</span></span> <span data-ttu-id="d3ff9-106">Hello esempi sono scritti in PHP.</span><span class="sxs-lookup"><span data-stu-id="d3ff9-106">hello samples are written in PHP.</span></span>
<span data-ttu-id="d3ff9-107">Hello scenari trattati includono **la costruzione di posta elettronica**, **l'invio di posta elettronica**, e **aggiungere allegati**.</span><span class="sxs-lookup"><span data-stu-id="d3ff9-107">hello scenarios covered include **constructing email**, **sending email**, and **adding attachments**.</span></span> <span data-ttu-id="d3ff9-108">Per ulteriori informazioni su SendGrid e l'invio di posta elettronica, vedere hello [passaggi successivi](#next-steps) sezione.</span><span class="sxs-lookup"><span data-stu-id="d3ff9-108">For more information on SendGrid and sending email, see hello [Next Steps](#next-steps) section.</span></span>

## <a name="what-is-hello-sendgrid-email-service"></a><span data-ttu-id="d3ff9-109">Che cos'è il servizio di posta elettronica SendGrid hello?</span><span class="sxs-lookup"><span data-stu-id="d3ff9-109">What is hello SendGrid Email Service?</span></span>
<span data-ttu-id="d3ff9-110">SendGrid è un [servizio di posta elettronica basato sul cloud] che offre [recapito affidabile di messaggi di posta elettronica transazionali], scalabilità e analisi in tempo reale, oltre ad API flessibili che agevolano l'integrazione personalizzata.</span><span class="sxs-lookup"><span data-stu-id="d3ff9-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="d3ff9-111">Gli scenari di utilizzo comuni di SendGrid includono:</span><span class="sxs-lookup"><span data-stu-id="d3ff9-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="d3ff9-112">Inviare automaticamente toocustomers conferme di recapito</span><span class="sxs-lookup"><span data-stu-id="d3ff9-112">Automatically sending receipts toocustomers</span></span>
* <span data-ttu-id="d3ff9-113">Amministrazione di liste di distribuzione per l'invio mensile ai clienti di volantini elettronici e offerte speciali</span><span class="sxs-lookup"><span data-stu-id="d3ff9-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="d3ff9-114">Raccolta di metriche in tempo reale per elementi quali indirizzi di posta elettronica bloccati e velocità di risposta al cliente</span><span class="sxs-lookup"><span data-stu-id="d3ff9-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="d3ff9-115">Generazione di report toohelp identificare le tendenze</span><span class="sxs-lookup"><span data-stu-id="d3ff9-115">Generating reports toohelp identify trends</span></span>
* <span data-ttu-id="d3ff9-116">Inoltro di richieste dei clienti</span><span class="sxs-lookup"><span data-stu-id="d3ff9-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="d3ff9-117">Notifiche di posta elettronica dall'applicazione</span><span class="sxs-lookup"><span data-stu-id="d3ff9-117">Email notifications from your application</span></span>

<span data-ttu-id="d3ff9-118">Per altre informazioni, vedere [https://sendgrid.com][https://sendgrid.com].</span><span class="sxs-lookup"><span data-stu-id="d3ff9-118">For more information, see [https://sendgrid.com][https://sendgrid.com].</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="d3ff9-119">Creazione di un account SendGrid</span><span class="sxs-lookup"><span data-stu-id="d3ff9-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="using-sendgrid-from-your-php-application"></a><span data-ttu-id="d3ff9-120">Utilizzo di SendGrid dall'applicazione PHP</span><span class="sxs-lookup"><span data-stu-id="d3ff9-120">Using SendGrid from your PHP Application</span></span>
<span data-ttu-id="d3ff9-121">L'uso di SendGrid in un'applicazione PHP di Azure non richiede speciali attività di configurazione o di scrittura del codice.</span><span class="sxs-lookup"><span data-stu-id="d3ff9-121">Using SendGrid in an Azure PHP application requires no special configuration or coding.</span></span> <span data-ttu-id="d3ff9-122">Poiché SendGrid è un servizio, è possibile accedervi in hello esattamente allo stesso modo da un'applicazione cloud perché è possibile da un'applicazione locale.</span><span class="sxs-lookup"><span data-stu-id="d3ff9-122">Because SendGrid is a service, it can be accessed in exactly hello same way from a cloud application as it can from an on-premises application.</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="d3ff9-123">Procedura: Inviare un messaggio di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="d3ff9-123">How to: Send an Email</span></span>
<span data-ttu-id="d3ff9-124">È possibile inviare tramite posta elettronica tramite SMTP o hello Web API fornite da SendGrid.</span><span class="sxs-lookup"><span data-stu-id="d3ff9-124">You can send email using either SMTP or hello Web API provided by SendGrid.</span></span>

### <a name="smtp-api"></a><span data-ttu-id="d3ff9-125">API SMTP</span><span class="sxs-lookup"><span data-stu-id="d3ff9-125">SMTP API</span></span>
<span data-ttu-id="d3ff9-126">hello SendGrid SMTP API, utilizzare posta elettronica toosend *Swift Mailer*, una raccolta basata su componenti per l'invio di messaggi di posta elettronica da applicazioni PHP.</span><span class="sxs-lookup"><span data-stu-id="d3ff9-126">toosend email using hello SendGrid SMTP API, use *Swift Mailer*, a component-based library for sending emails from PHP applications.</span></span> <span data-ttu-id="d3ff9-127">È possibile scaricare hello *Swift Mailer* libreria da [http://swiftmailer.org/download] [ http://swiftmailer.org/download] v5.3.0 (utilizzare [Composer] tooinstall SWIFT Mailer).</span><span class="sxs-lookup"><span data-stu-id="d3ff9-127">You can download hello *Swift Mailer* library from [http://swiftmailer.org/download][http://swiftmailer.org/download] v5.3.0 (use [Composer] tooinstall Swift Mailer).</span></span> <span data-ttu-id="d3ff9-128">L'invio di posta elettronica con la libreria hello comporta la creazione di istanze di <span class="auto-style2">Swift\_SmtpTransport</span>, <span class="auto-style2">Swift\_Mailer</span>, e <span class="auto-style2">Swift\_messaggio </span> classi, impostare le proprietà appropriate e chiamare il <span class="auto-style2">Swift\_Mailer::send</span> metodo.</span><span class="sxs-lookup"><span data-stu-id="d3ff9-128">Sending email with hello library involves creating instances of the <span class="auto-style2">Swift\_SmtpTransport</span>, <span class="auto-style2">Swift\_Mailer</span>, and <span class="auto-style2">Swift\_Message</span> classes, setting the appropriate properties, and calling the <span class="auto-style2">Swift\_Mailer::send</span> method.</span></span>

    <?php
     include_once "vendor/autoload.php";
     /*
      * Create hello body of hello message (a plain-text and an HTML version).
      * $text is your plain-text email
      * $html is your html version of hello email
      * If hello receiver is able tooview html emails then only hello html
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
     $from = array('someone@example.com' => 'Name tooAppear');
     // Email recipients
     $too= array(
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

     // attach hello body of hello email
     $message->setFrom($from);
     $message->setBody($html, 'text/html');
     $message->setTo($to);
     $message->addPart($text, 'text/plain');

     // send message
     if ($recipients = $swift->send($message, $failures))
     {
         // This will let us know how many users received this message
         echo 'Message sent out too'.$recipients.' users';
     }
     // something went wrong =(
     else
     {
         echo "Something went wrong - ";
         print_r($failures);
     }

### <a name="web-api"></a><span data-ttu-id="d3ff9-129">API Web</span><span class="sxs-lookup"><span data-stu-id="d3ff9-129">Web API</span></span>
<span data-ttu-id="d3ff9-130">Usare PHP [curl funzione] [ curl function] tramite posta elettronica toosend hello SendGrid Web API.</span><span class="sxs-lookup"><span data-stu-id="d3ff9-130">Use PHP's [curl function][curl function] toosend email using hello SendGrid Web API.</span></span>

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

     // Tell curl toouse HTTP POST
     curl_setopt ($session, CURLOPT_POST, true);

     // Tell curl that this is hello body of hello POST
     curl_setopt ($session, CURLOPT_POSTFIELDS, $params);

     // Tell curl not tooreturn headers, but do return hello response
     curl_setopt($session, CURLOPT_HEADER, false);
     curl_setopt($session, CURLOPT_RETURNTRANSFER, true);

     // obtain response
     $response = curl_exec($session);
     curl_close($session);

     // print everything out
     print_r($response);

<span data-ttu-id="d3ff9-131">API Web di SendGrid è molto simile tooa API REST, se non è realmente un'API RESTful poiché la maggior parte delle chiamate, entrambi OTTERRÀ e verbi POST possono essere utilizzati indifferentemente.</span><span class="sxs-lookup"><span data-stu-id="d3ff9-131">SendGrid's Web API is very similar tooa REST API, though it is not truly a RESTful API since, in most calls, both GET and POST verbs can be used interchangeably.</span></span>

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="d3ff9-132">Procedura: Aggiungere un allegato</span><span class="sxs-lookup"><span data-stu-id="d3ff9-132">How to: Add an Attachment</span></span>
### <a name="smtp-api"></a><span data-ttu-id="d3ff9-133">API SMTP</span><span class="sxs-lookup"><span data-stu-id="d3ff9-133">SMTP API</span></span>
<span data-ttu-id="d3ff9-134">Invio di un allegato con hello SMTP API comporta una riga aggiuntiva dello script di esempio di codice toohello per l'invio di un messaggio di posta elettronica con Mailer Swift.</span><span class="sxs-lookup"><span data-stu-id="d3ff9-134">Sending an attachment using hello SMTP API involves one additional line of code toohello example script for sending an email with Swift Mailer.</span></span>

    <?php
     include_once "vendor/autoload.php";
     /*
      * Create hello body of hello message (a plain-text and an HTML version).
      * $text is your plain-text email
      * $html is your html version of hello email
      * If hello reciever is able tooview html emails then only hello html
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
     $from = array('someone@example.com' => 'Name tooAppear');

     // Email recipients
     $too= array(
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

     // attach hello body of hello email
     $message->setFrom($from);
     $message->setBody($html, 'text/html');
     $message->setTo($to);
     $message->addPart($text, 'text/plain');
     $message->attach(Swift_Attachment::fromPath("path\to\file")->setFileName("file_name"));

     // send message
     if ($recipients = $swift->send($message, $failures))
     {
          // This will let us know how many users received this message
          echo 'Message sent out too'.$recipients.' users';
     }
     // something went wrong =(
     else
     {
          echo "Something went wrong - ";
          print_r($failures);
     }

<span data-ttu-id="d3ff9-135">riga di codice aggiuntivo Hello è come segue:</span><span class="sxs-lookup"><span data-stu-id="d3ff9-135">hello additional line of code is as follows:</span></span>

     $message->attach(Swift_Attachment::fromPath("path\to\file")->setFileName('file_name'));

<span data-ttu-id="d3ff9-136">Questa riga di codice chiamate hello attach (metodo) nei <span class="auto-style2">Swift\_messaggio</span> dell'oggetto e viene utilizzato il metodo statico <span class="auto-style2">fromPath</span> sul <span class="auto-style2">Swift\_allegato</span>classe tooget e collegare un messaggio di tooa file.</span><span class="sxs-lookup"><span data-stu-id="d3ff9-136">This line of code calls hello attach method on the <span class="auto-style2">Swift\_Message</span> object and uses static method <span class="auto-style2">fromPath</span> on the <span class="auto-style2">Swift\_Attachment</span> class tooget and attach a file tooa message.</span></span>

### <a name="web-api"></a><span data-ttu-id="d3ff9-137">API Web</span><span class="sxs-lookup"><span data-stu-id="d3ff9-137">Web API</span></span>
<span data-ttu-id="d3ff9-138">L'invio di un allegato utilizzando hello API Web è molto simile toosending un messaggio di posta elettronica utilizzando hello API Web.</span><span class="sxs-lookup"><span data-stu-id="d3ff9-138">Sending an attachment using hello Web API is very similar toosending an email using hello Web API.</span></span> <span data-ttu-id="d3ff9-139">Tuttavia, si noti che nell'esempio hello seguente, la matrice di parametri hello deve contenere questo elemento:</span><span class="sxs-lookup"><span data-stu-id="d3ff9-139">However, note that in hello example that follows, hello parameter array must contain this element:</span></span>

    'files['.$fileName.']' => '@'.$filePath.'/'.$fileName

<span data-ttu-id="d3ff9-140">Esempio:</span><span class="sxs-lookup"><span data-stu-id="d3ff9-140">Example:</span></span>

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
         'html' => '<p> hello HTML </p>',
         'text' => 'hello plain text',
         'from' => 'anna@contoso.com',
         'files['.$fileName.']' => '@'.$filePath.'/'.$fileName
     );

     print_r($params);

     $request = $url.'api/mail.send.json';

     // Generate curl request
     $session = curl_init($request);

     // Tell curl toouse HTTP POST
     curl_setopt ($session, CURLOPT_POST, true);

     // Tell curl that this is hello body of hello POST
     curl_setopt ($session, CURLOPT_POSTFIELDS, $params);

     // Tell curl not tooreturn headers, but do return hello response
     curl_setopt($session, CURLOPT_HEADER, false);
     curl_setopt($session, CURLOPT_RETURNTRANSFER, true);

     // obtain response
     $response = curl_exec($session);
     curl_close($session);

     // print everything out
     print_r($response);

## <a name="how-to-use-filters-tooenable-footers-tracking-and-analytics"></a><span data-ttu-id="d3ff9-141">Procedura: utilizzare i filtri tooEnable piè di pagina, il rilevamento e Analitica</span><span class="sxs-lookup"><span data-stu-id="d3ff9-141">How to: Use Filters tooEnable Footers, Tracking, and Analytics</span></span>
<span data-ttu-id="d3ff9-142">SendGrid fornisce funzionalità di posta elettronica aggiuntivo tramite l'utilizzo di hello del 'filtri'.</span><span class="sxs-lookup"><span data-stu-id="d3ff9-142">SendGrid provides additional email functionality through hello use of 'filters'.</span></span> <span data-ttu-id="d3ff9-143">Si tratta di impostazioni che è possibile aggiungere il messaggio di posta elettronica tooan per abilitare le funzionalità specifiche, quali l'abilitazione di fare clic su rilevamento, Google analitica, di rilevamento, sottoscrizione e così via.</span><span class="sxs-lookup"><span data-stu-id="d3ff9-143">These are settings that can be added tooan email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span>

<span data-ttu-id="d3ff9-144">I filtri possono essere applicati tooa messaggio utilizzando proprietà filtri hello.</span><span class="sxs-lookup"><span data-stu-id="d3ff9-144">Filters can be applied tooa message by using hello filters property.</span></span> <span data-ttu-id="d3ff9-145">Ogni filtro è specificato da un hash che contiene impostazioni specifiche del filtro.</span><span class="sxs-lookup"><span data-stu-id="d3ff9-145">Each filter is specified by a hash containing filter-specific settings.</span></span> <span data-ttu-id="d3ff9-146">Nell'esempio seguente Abilita il filtro di piè di pagina hello e specifica un messaggio di testo che verrà aggiunto toohello inferiore del messaggio di posta elettronica hello.</span><span class="sxs-lookup"><span data-stu-id="d3ff9-146">The following example enables hello footer filter and specifies a text message that will be appended toohello bottom of hello email message.</span></span>
<span data-ttu-id="d3ff9-147">Per questo esempio si userà la [libreria sendgrid-php].</span><span class="sxs-lookup"><span data-stu-id="d3ff9-147">For this example we will use [sendgrid-php library].</span></span>
<span data-ttu-id="d3ff9-148">Utilizzare [Composer] tooinstall libreria:</span><span class="sxs-lookup"><span data-stu-id="d3ff9-148">Use [Composer] tooinstall library:</span></span>

    php composer.phar require sendgrid/sendgrid 2.1.1

<span data-ttu-id="d3ff9-149">Esempio:</span><span class="sxs-lookup"><span data-stu-id="d3ff9-149">Example:</span></span>    

    <?php
     /*
      * This example is used for sendgrid-php V2.1.1 (https://github.com/sendgrid/sendgrid-php/tree/v2.1.1)
      */
     include "vendor/autoload.php";

     $email = new SendGrid\Email();
     // hello list of addresses this message will be sent to
     // [This list is used for sending multiple emails using just ONE request tooSendGrid]
     $toList = array('john@contoso.com', 'anna@contoso.com');

     // Specify hello names of hello recipients
     $nameList = array('Name 1', 'Name 2');

     // Used as an example of variable substitution
     $timeList = array('4 PM', '5 PM');

     // Set all of hello above variables
     $email->setTos($toList);
     $email->addSubstitution('-name-', $nameList);
     $email->addSubstitution('-time-', $timeList);

     // Specify that this is an initial contact message
     $email->addCategory("initial");

     // You can optionally setup individual filters here, in this example, we have
     // enabled hello footer filter
     $email->addFilter('footer', 'enable', 1);
     $email->addFilter('footer', "text/plain", "Thank you for your business");
     $email->addFilter('footer', "text/html", "Thank you for your business");

     // hello subject of your email
     $subject = 'Example SendGrid Email';

     // Where is this message coming from. For example, this message can be from
     // support@yourcompany.com, info@yourcompany.com
     $from = 'someone@example.com';

     // If you do not specify a sender list above, you can specifiy hello user here. If
     // a sender list IS specified above, this email address becomes irrelevant.
     $too= 'john@contoso.com';

     # Create hello body of hello message (a plain-text and an HTML version).
     # text is your plain-text email
     # html is your html version of hello email
     # if hello receiver is able tooview html emails then only hello html
     # email will be displayed

     /*
      * Note hello variable substitution here =)
      */
     $text = "
     Hello -name-,
     Thank you for your interest in our products. We have set up an appointment toocall you at -time- EST toodiscuss your needs in more detail.
     Regards,
     Fred";

     $html = "
     <html>
     <head></head>
     <body>
     <p>Hello -name-,<br>
     Thank you for your interest in our products. We have set up an appointment
     toocall you at -time- EST toodiscuss your needs in more detail.

     Regards,

     Fred<br>
     </p>
     </body>
     </html>";

     // set subject
     $email->setSubject($subject);

     // attach hello body of hello email
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

## <a name="next-steps"></a><span data-ttu-id="d3ff9-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d3ff9-150">Next Steps</span></span>
<span data-ttu-id="d3ff9-151">Ora che si è appreso nozioni di base di hello di hello servizio di posta elettronica di SendGrid, seguire questi ulteriori toolearn di collegamenti.</span><span class="sxs-lookup"><span data-stu-id="d3ff9-151">Now that you've learned hello basics of hello SendGrid Email service, follow these links toolearn more.</span></span>

* <span data-ttu-id="d3ff9-152">Documentazione relativa a SendGrid: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="d3ff9-152">SendGrid documentation: <https://sendgrid.com/docs></span></span>
* <span data-ttu-id="d3ff9-153">Libreria PHP di SendGrid: <https://github.com/sendgrid/sendgrid-php></span><span class="sxs-lookup"><span data-stu-id="d3ff9-153">SendGrid PHP library: <https://github.com/sendgrid/sendgrid-php></span></span>
* <span data-ttu-id="d3ff9-154">Offerta speciale SendGrid per i clienti di Azure: <https://sendgrid.com/windowsazure.html></span><span class="sxs-lookup"><span data-stu-id="d3ff9-154">SendGrid special offer for Azure customers: <https://sendgrid.com/windowsazure.html></span></span>

<span data-ttu-id="d3ff9-155">Per ulteriori informazioni, vedere anche hello [Centro sviluppatori PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="d3ff9-155">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[https://sendgrid.com]: https://sendgrid.com
[https://sendgrid.com/transactional-email/pricing]: https://sendgrid.com/transactional-email/pricing
[special offer]: https://www.sendgrid.com/windowsazure.html
[Packaging and Deploying PHP Applications for Azure]: http://msdn.microsoft.com/library/windowsazure/hh674499(v=VS.103).aspx
[http://swiftmailer.org/download]: http://swiftmailer.org/download
[curl function]: http://php.net/curl
[servizio di posta elettronica basato sul cloud]: https://sendgrid.com/email-solutions
[recapito affidabile di messaggi di posta elettronica transazionali]: https://sendgrid.com/transactional-email
[libreria sendgrid-php]: https://github.com/sendgrid/sendgrid-php/tree/v2.1.1
[Composer]: https://getcomposer.org/download/
