---
title: aaaHow toomake una telefonata da Twilio (PHP) | Documenti Microsoft
description: Informazioni su come messaggio di toomake una telefonata e inviare un SMS con il servizio API di Twilio hello in Azure. Esempi per un'applicazione PHP.
documentationcenter: php
services: 
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: 44e35adc-be06-4700-beee-8c9e2c20c540
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: e6fecc345bf9ae787d14d533bd8d96b175c2453b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomake-a-phone-call-using-twilio-in-a-php-application-on-azure"></a><span data-ttu-id="6ac63-104">Come tooMake un Twilio tramite chiamata telefonica in un'applicazione PHP in Azure</span><span class="sxs-lookup"><span data-stu-id="6ac63-104">How tooMake a Phone Call Using Twilio in a PHP Application on Azure</span></span>
<span data-ttu-id="6ac63-105">Hello seguente esempio viene illustrato come usare Twilio toomake una chiamata da una pagina web PHP ospitato in Azure.</span><span class="sxs-lookup"><span data-stu-id="6ac63-105">hello following example shows you how you can use Twilio toomake a call from a PHP web page hosted in Azure.</span></span> <span data-ttu-id="6ac63-106">un'applicazione Hello risultante utente verrà chiesto hello di valori di chiamata telefonica, come illustrato nella seguente cattura di schermata hello.</span><span class="sxs-lookup"><span data-stu-id="6ac63-106">hello resulting application will prompt hello user for phone call values, as shown in hello following screen shot.</span></span>

![Modulo di chiamata di Azure con Twilio e PHP][twilio_php]

<span data-ttu-id="6ac63-108">È necessario seguente hello toodo codice hello toouse in questo argomento:</span><span class="sxs-lookup"><span data-stu-id="6ac63-108">You'll need toodo hello following toouse hello code in this topic:</span></span>

1. <span data-ttu-id="6ac63-109">Ottenere un account Twilio e un token di autenticazione dalla [console di Twilio][twilio_console].</span><span class="sxs-lookup"><span data-stu-id="6ac63-109">Acquire a Twilio account and authentication token from your [Twilio Console][twilio_console].</span></span> <span data-ttu-id="6ac63-110">tooget introduttiva Twilio, valutare al prezzo [http://www.twilio.com/pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="6ac63-110">tooget started with Twilio, evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="6ac63-111">Per effettuare l'iscrizione e ottenere un account di valutazione gratuito, vedere la pagina [https://www.twilio.com/try-twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="6ac63-111">You can sign up for a trial account at [https://www.twilio.com/try-twilio][try_twilio].</span></span>
2. <span data-ttu-id="6ac63-112">Ottenere hello [libreria Twilio per PHP](https://github.com/twilio/twilio-php) o installato come un pacchetto di PERA.</span><span class="sxs-lookup"><span data-stu-id="6ac63-112">Obtain hello [Twilio library for PHP](https://github.com/twilio/twilio-php) or install it as a PEAR package.</span></span> <span data-ttu-id="6ac63-113">Per ulteriori informazioni, vedere hello [file readme](https://github.com/twilio/twilio-php/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="6ac63-113">For more information, see hello [readme file](https://github.com/twilio/twilio-php/blob/master/README.md).</span></span>
3. <span data-ttu-id="6ac63-114">Installare hello Azure SDK per PHP.</span><span class="sxs-lookup"><span data-stu-id="6ac63-114">Install hello Azure SDK for PHP.</span></span> <span data-ttu-id="6ac63-115">Per una panoramica di hello SDK e istruzioni su come installarlo, vedere [configurare hello Azure SDK per PHP](app-service-web/web-sites-php-mysql-deploy-use-git.md)</span><span class="sxs-lookup"><span data-stu-id="6ac63-115">For an overview of hello SDK and instructions on installing it, see [Set up hello Azure SDK for PHP](app-service-web/web-sites-php-mysql-deploy-use-git.md)</span></span>

## <a name="create-a-web-form-for-making-a-call"></a><span data-ttu-id="6ac63-116">Creare un modulo Web per effettuare una chiamata</span><span class="sxs-lookup"><span data-stu-id="6ac63-116">Create a web form for making a call</span></span>
<span data-ttu-id="6ac63-117">Hello HTML seguente codice viene illustrato come una pagina web toobuild (**callform.html**) che recupera i dati utente per effettuare una chiamata:</span><span class="sxs-lookup"><span data-stu-id="6ac63-117">hello following HTML code shows how toobuild a web page (**callform.html**) that retrieves user data for making a call:</span></span>

```html
<!DOCTYPE html>
<html>
<head>
  <title>Automated call form</title>
</head>
<body>
  <h1>Automated Call Form</h1>
  <p>Fill in all fields and click <b>Make this call</b>.</p>
  <form action="makecall.php" method="post">
    <table>
      <tr>
        <td>To:</td>
        <td><input name="callTo" size="50" type="text" value=""></td>
      </tr>
      <tr>
        <td>From:</td>
        <td><input name="callFrom" size="50" type="text" value=""></td>
      </tr>
      <tr>
        <td>Call message:</td>
        <td><input name="callText" size="100" type="text" value="Hello. This is hello call text. Good bye."></td>
      </tr>
      <tr>
        <td colspan="2"><input type="submit" value="Make this call"></td>
      </tr>
    </table>
  </form><br>
</body>
</html>
```

## <a name="create-hello-code-toomake-hello-call"></a><span data-ttu-id="6ac63-118">Creare una chiamata di hello toomake codice hello</span><span class="sxs-lookup"><span data-stu-id="6ac63-118">Create hello code toomake hello call</span></span>
<span data-ttu-id="6ac63-119">Hello seguente codice mostra come toobuild **makecall.php**, che viene chiamato quando l'utente hello invia il form di hello visualizzato da **callform.html**.</span><span class="sxs-lookup"><span data-stu-id="6ac63-119">hello following code shows how toobuild **makecall.php**, which is called when hello user submits hello form displayed by **callform.html**.</span></span> <span data-ttu-id="6ac63-120">codice Hello riportato di seguito crea messaggio hello e genera l'errore chiamata hello.</span><span class="sxs-lookup"><span data-stu-id="6ac63-120">hello code shown below creates hello call message and generates hello call.</span></span> <span data-ttu-id="6ac63-121">Inoltre, essere toouse che l'account di Twilio e l'autenticazione del token da hello [Twilio Console] [ twilio_console] anziché i valori segnaposto hello assegnati troppo**$sid** e **$token** codice hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="6ac63-121">Also, be sure toouse your Twilio account and authentication token from hello [Twilio Console][twilio_console] instead of hello placeholder values assigned too**$sid** and **$token** in hello code below.</span></span>

```html
<html>
<head><title>Making call...</title></head>
<body>
<p>Your call is being made.</p>

<?php
require_once 'path/to/vendor/autoload.php';

$sid   = "your_account_sid";
$token = "your_authentication_token";

$from_number = $_POST['callFrom']; // Calls must be made from a registered Twilio number.
$to_number   = $_POST['callTo'];
$message     = $_POST['callText'];

$client = new Twilio\Rest\Client($sid, $token);

$call = $client->calls->create(
            $to_number,
            $from_number,
            array('url' => http://twimlets.com/message?Message=' . urlencode($message))
        );

echo "Call status: " . $call->status . "<br />";
echo "URI resource: " . $call->uri . "<br />";
?>
</body>
</html>
```

<span data-ttu-id="6ac63-122">Inoltre toomaking hello chiamata, **makecall.php** Visualizza alcuni metadati di chiamata, come illustrato nell'immagine di hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="6ac63-122">In addition toomaking hello call, **makecall.php** displays some call metadata, as is shown in hello image below.</span></span> <span data-ttu-id="6ac63-123">Per altre informazioni sui metadati della chiamata, vedere [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties].</span><span class="sxs-lookup"><span data-stu-id="6ac63-123">For more information about call metadata, see [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties].</span></span>

![Risposta a chiamata di Azure tramite Twilio e PHP][twilio_php_response]

## <a name="run-hello-application"></a><span data-ttu-id="6ac63-125">Eseguire un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="6ac63-125">Run hello application</span></span>
<span data-ttu-id="6ac63-126">passaggio successivo Hello è toodeploy il tooAzure applicazione siti Web.</span><span class="sxs-lookup"><span data-stu-id="6ac63-126">hello next step is toodeploy your application tooAzure Websites.</span></span> <span data-ttu-id="6ac63-127">Hello articoli seguenti contengono informazioni hello per la creazione di un sito Web e la distribuzione del codice con Git, FTP o WebMatrix (ma non tutte le informazioni in ogni articolo sono rilevante):</span><span class="sxs-lookup"><span data-stu-id="6ac63-127">hello following articles contain hello information for creating a website and deploying your code with Git, FTP, or WebMatrix (though not all information in each article is relevant):</span></span>

* [<span data-ttu-id="6ac63-128">Creare un sito Web di Azure PHP-MySQL e distribuirlo tramite Git</span><span class="sxs-lookup"><span data-stu-id="6ac63-128">Create a PHP-MySQL Azure Web Site and deploy using Git</span></span>](app-service-web/web-sites-php-mysql-deploy-use-git.md)
* [<span data-ttu-id="6ac63-129">Creare un sito Web di Azure PHP-MySQL e distribuirlo tramite FTP</span><span class="sxs-lookup"><span data-stu-id="6ac63-129">Create a PHP-MySQL Azure Web Site and Deploy Using FTP</span></span>](app-service-web/web-sites-php-mysql-deploy-use-ftp.md)

## <a name="next-steps"></a><span data-ttu-id="6ac63-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6ac63-130">Next steps</span></span>
<span data-ttu-id="6ac63-131">Questo codice è stato fornito tooshow di funzionalità di base tramite Twilio in PHP in Azure.</span><span class="sxs-lookup"><span data-stu-id="6ac63-131">This code was provided tooshow you basic functionality using Twilio in PHP on Azure.</span></span> <span data-ttu-id="6ac63-132">Prima di distribuire tooAzure nell'ambiente di produzione, è consigliabile tooadd più la gestione degli errori o altre funzionalità.</span><span class="sxs-lookup"><span data-stu-id="6ac63-132">Before deploying tooAzure in production, you may want tooadd more error handling or other features.</span></span> <span data-ttu-id="6ac63-133">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="6ac63-133">For example:</span></span>

* <span data-ttu-id="6ac63-134">Anziché utilizzare un web form, è possibile usare BLOB di archiviazione di Azure o i numeri di telefono toostore Database SQL e chiamare testo.</span><span class="sxs-lookup"><span data-stu-id="6ac63-134">Instead of using a web form, you could use Azure storage blobs or SQL Database toostore phone numbers and call text.</span></span> <span data-ttu-id="6ac63-135">Per informazioni sull'uso dei BLOB di archiviazione di Azure in PHP, vedere [Come usare l'archiviazione BLOB da PHP][howto_blob_storage_php].</span><span class="sxs-lookup"><span data-stu-id="6ac63-135">For information about using Azure storage blobs in PHP, see [Using Azure Storage with PHP Applications][howto_blob_storage_php].</span></span> <span data-ttu-id="6ac63-136">Per informazioni sull'uso di database SQL in PHP, vedere [Raccolte di connessioni per database SQL e Server SQL][howto_sql_azure_php].</span><span class="sxs-lookup"><span data-stu-id="6ac63-136">For information about using SQL Database in PHP, see [Using SQL Database with PHP Applications][howto_sql_azure_php].</span></span>
* <span data-ttu-id="6ac63-137">Hello **makecall.php** codice Usa l'URL fornito Twilio ([http://twimlets.com/message][twimlet_message_url]) tooprovide una risposta di Twilio Markup Language (TwiML) che indica la modalità di Twilio tooproceed con chiamata hello.</span><span class="sxs-lookup"><span data-stu-id="6ac63-137">hello **makecall.php** code uses Twilio-provided URL ([http://twimlets.com/message][twimlet_message_url]) tooprovide a Twilio Markup Language (TwiML) response that informs Twilio how tooproceed with hello call.</span></span> <span data-ttu-id="6ac63-138">Ad esempio, può contenere i hello TwiML che viene restituito un `<Say>` verbo risultante in testo non viene pronunciata toohello chiamata destinatario.</span><span class="sxs-lookup"><span data-stu-id="6ac63-138">For example, hello TwiML that is returned can contain a `<Say>` verb that results in text being spoken toohello call recipient.</span></span> <span data-ttu-id="6ac63-139">Anziché utilizzare l'URL fornito Twilio hello, è possibile creare una richiesta del tooTwilio toorespond proprio servizio. Per ulteriori informazioni, vedere [come tooUse Twilio per funzionalità voce ed SMS in PHP][howto_twilio_voice_sms_php].</span><span class="sxs-lookup"><span data-stu-id="6ac63-139">Instead of using hello Twilio-provided URL, you could build your own service toorespond tooTwilio's request; for more information, see [How tooUse Twilio for Voice and SMS Capabilities in PHP][howto_twilio_voice_sms_php].</span></span> <span data-ttu-id="6ac63-140">Per altre informazioni su TwiML, vedere la pagina [http://www.twilio.com/docs/api/twiml][twiml] e per altre informazioni su `<Say>` e altri verbi Twilio, vedere la pagina [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span><span class="sxs-lookup"><span data-stu-id="6ac63-140">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml], and more information about `<Say>` and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>
* <span data-ttu-id="6ac63-141">Leggere le indicazioni sulla sicurezza in hello Twilio [https://www.twilio.com/docs/security][twilio_docs_security].</span><span class="sxs-lookup"><span data-stu-id="6ac63-141">Read hello Twilio security guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>

<span data-ttu-id="6ac63-142">Per altre informazioni su Twilio, vedere [https://www.twilio.com/docs][twilio_docs].</span><span class="sxs-lookup"><span data-stu-id="6ac63-142">For additional information about Twilio, see [https://www.twilio.com/docs][twilio_docs].</span></span>

## <a name="see-also"></a><span data-ttu-id="6ac63-143">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="6ac63-143">See Also</span></span>
* [<span data-ttu-id="6ac63-144">Come tooUse Twilio per funzionalità voce ed SMS in PHP</span><span class="sxs-lookup"><span data-stu-id="6ac63-144">How tooUse Twilio for Voice and SMS Capabilities in PHP</span></span>](partner-twilio-php-how-to-use-voice-sms.md)

[twilio_console]: https://www.twilio.com/console
[twilio_pricing]: http://www.twilio.com/pricing
[try_twilio]: http://www.twilio.com/try-twilio
[twilio_api]: http://www.twilio.com/docs/api
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified
[twimlet_message_url]: http://twimlets.com/message
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api_service]: http://api.twilio.com
[build_php_azure_app]: http://azurephp.interoperabilitybridges.com/articles/build-and-deploy-a-windows-azure-php-application
[howto_twilio_voice_sms_php]: partner-twilio-php-how-to-use-voice-sms.md
[howto_blob_storage_php]: http://azure.microsoft.com/documentation/articles/storage-php-how-to-use-blobs/
[howto_sql_azure_php]: http://azure.microsoft.com/documentation/articles/sql-database-php-how-to-use/
[twilio_call_properties]: https://www.twilio.com/docs/api/rest/call#instance-properties
[twilio_docs_security]: http://www.twilio.com/docs/security
[twilio_docs]: http://www.twilio.com/docs
[twilio_say]: http://www.twilio.com/docs/api/twiml/say
[ssl_validation]: http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html
[twilio_php]: ./media/partner-twilio-php-make-phone-call/WA_TwilioPHPCallForm.jpg
[twilio_php_response]: ./media/partner-twilio-php-make-phone-call/WA_TwilioPHPMakeCall.jpg
[website-git]: ./web-sites/web-sites-php-mysql-deploy-use-git.md
[website-ftp]: ./web-sites/web-sites-php-mysql-deploy-use-ftp.md
[twilio_php_github]: https://github.com/twilio/twilio-php
