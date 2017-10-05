---
title: Come effettuare una chiamata telefonica da Twilio (PHP) | Microsoft Docs
description: Informazioni su come effettuare una chiamata telefonica e inviare un SMS con il servizio API Twilio API in Azure. Esempi per un'applicazione PHP.
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
ms.openlocfilehash: f35450ace02727ddf392dbbe857b934a45ee022a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-make-a-phone-call-using-twilio-in-a-php-application-on-azure"></a><span data-ttu-id="901a6-104">Come effettuare una chiamata tramite Twilio in un'applicazione PHP in Azure</span><span class="sxs-lookup"><span data-stu-id="901a6-104">How to Make a Phone Call Using Twilio in a PHP Application on Azure</span></span>
<span data-ttu-id="901a6-105">Nell'esempio seguente viene illustrato come è possibile utilizzare Twilio per effettuare una chiamata da una pagina Web PHP ospitata in Azure.</span><span class="sxs-lookup"><span data-stu-id="901a6-105">The following example shows you how you can use Twilio to make a call from a PHP web page hosted in Azure.</span></span> <span data-ttu-id="901a6-106">L'applicazione risultante chiederà all'utente di inserire i valori relativi alla chiamata telefonica, come illustrato nella schermata seguente.</span><span class="sxs-lookup"><span data-stu-id="901a6-106">The resulting application will prompt the user for phone call values, as shown in the following screen shot.</span></span>

![Modulo di chiamata di Azure con Twilio e PHP][twilio_php]

<span data-ttu-id="901a6-108">Per usare il codice in questo argomento è necessario eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="901a6-108">You'll need to do the following to use the code in this topic:</span></span>

1. <span data-ttu-id="901a6-109">Ottenere un account Twilio e un token di autenticazione dalla [console di Twilio][twilio_console].</span><span class="sxs-lookup"><span data-stu-id="901a6-109">Acquire a Twilio account and authentication token from your [Twilio Console][twilio_console].</span></span> <span data-ttu-id="901a6-110">Per informazioni sui prezzi di Twilio, vedere la pagina [http://www.twilio.com/pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="901a6-110">To get started with Twilio, evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="901a6-111">Per effettuare l'iscrizione e ottenere un account di valutazione gratuito, vedere la pagina [https://www.twilio.com/try-twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="901a6-111">You can sign up for a trial account at [https://www.twilio.com/try-twilio][try_twilio].</span></span>
2. <span data-ttu-id="901a6-112">Ottenere la [libreria Twilio per PHP](https://github.com/twilio/twilio-php) o installarla come pacchetto PEAR.</span><span class="sxs-lookup"><span data-stu-id="901a6-112">Obtain the [Twilio library for PHP](https://github.com/twilio/twilio-php) or install it as a PEAR package.</span></span> <span data-ttu-id="901a6-113">Per altre informazioni, vedere il [file leggimi](https://github.com/twilio/twilio-php/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="901a6-113">For more information, see the [readme file](https://github.com/twilio/twilio-php/blob/master/README.md).</span></span>
3. <span data-ttu-id="901a6-114">Installare Azure SDK per PHP.</span><span class="sxs-lookup"><span data-stu-id="901a6-114">Install the Azure SDK for PHP.</span></span> <span data-ttu-id="901a6-115">Per informazioni generali sull'SDK e istruzioni per installarlo, vedere [Set up the Azure SDK for PHP](app-service-web/web-sites-php-mysql-deploy-use-git.md) (Configurare Azure SDK per PHP).</span><span class="sxs-lookup"><span data-stu-id="901a6-115">For an overview of the SDK and instructions on installing it, see [Set up the Azure SDK for PHP](app-service-web/web-sites-php-mysql-deploy-use-git.md)</span></span>

## <a name="create-a-web-form-for-making-a-call"></a><span data-ttu-id="901a6-116">Creare un modulo Web per effettuare una chiamata</span><span class="sxs-lookup"><span data-stu-id="901a6-116">Create a web form for making a call</span></span>
<span data-ttu-id="901a6-117">Il codice HTML seguente mostra come creare una pagina Web (**callform.html**) che consente di recuperare i dati utente per l'effettuazione di una chiamata:</span><span class="sxs-lookup"><span data-stu-id="901a6-117">The following HTML code shows how to build a web page (**callform.html**) that retrieves user data for making a call:</span></span>

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
        <td><input name="callText" size="100" type="text" value="Hello. This is the call text. Good bye."></td>
      </tr>
      <tr>
        <td colspan="2"><input type="submit" value="Make this call"></td>
      </tr>
    </table>
  </form><br>
</body>
</html>
```

## <a name="create-the-code-to-make-the-call"></a><span data-ttu-id="901a6-118">Creare il codice per l'esecuzione della chiamata</span><span class="sxs-lookup"><span data-stu-id="901a6-118">Create the code to make the call</span></span>
<span data-ttu-id="901a6-119">Il codice seguente illustra come compilare **makecall.php**, una pagina Web chiamata quando l'utente invia il modulo visualizzato da **callform.html**.</span><span class="sxs-lookup"><span data-stu-id="901a6-119">The following code shows how to build **makecall.php**, which is called when the user submits the form displayed by **callform.html**.</span></span> <span data-ttu-id="901a6-120">Il codice seguente crea il messaggio di chiamata e genera la chiamata.</span><span class="sxs-lookup"><span data-stu-id="901a6-120">The code shown below creates the call message and generates the call.</span></span> <span data-ttu-id="901a6-121">Accertarsi inoltre di usare l'account e il token di autenticazione Twilio ottenuti dalla [console di Twilio][twilio_console] anziché i valori segnaposto assegnati a **$sid** e **$token** nel codice seguente.</span><span class="sxs-lookup"><span data-stu-id="901a6-121">Also, be sure to use your Twilio account and authentication token from the [Twilio Console][twilio_console] instead of the placeholder values assigned to **$sid** and **$token** in the code below.</span></span>

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

<span data-ttu-id="901a6-122">Oltre a eseguire la chiamata, **makecall.php** visualizza alcuni metadati della chiamata, come mostrato nell'immagine seguente.</span><span class="sxs-lookup"><span data-stu-id="901a6-122">In addition to making the call, **makecall.php** displays some call metadata, as is shown in the image below.</span></span> <span data-ttu-id="901a6-123">Per altre informazioni sui metadati della chiamata, vedere [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties].</span><span class="sxs-lookup"><span data-stu-id="901a6-123">For more information about call metadata, see [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties].</span></span>

![Risposta a chiamata di Azure tramite Twilio e PHP][twilio_php_response]

## <a name="run-the-application"></a><span data-ttu-id="901a6-125">Eseguire l'applicazione</span><span class="sxs-lookup"><span data-stu-id="901a6-125">Run the application</span></span>
<span data-ttu-id="901a6-126">Il passaggio successivo consiste nel distribuire l'applicazione in Siti Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="901a6-126">The next step is to deploy your application to Azure Websites.</span></span> <span data-ttu-id="901a6-127">Gli articoli seguenti contengono informazioni sulla creazione di un sito Web e sulla distribuzione del codice con Git, FTP o WebMatrix, sebbene non tutte le informazioni incluse in ogni articolo siano rilevanti:</span><span class="sxs-lookup"><span data-stu-id="901a6-127">The following articles contain the information for creating a website and deploying your code with Git, FTP, or WebMatrix (though not all information in each article is relevant):</span></span>

* [<span data-ttu-id="901a6-128">Creare un sito Web di Azure PHP-MySQL e distribuirlo tramite Git</span><span class="sxs-lookup"><span data-stu-id="901a6-128">Create a PHP-MySQL Azure Web Site and deploy using Git</span></span>](app-service-web/web-sites-php-mysql-deploy-use-git.md)
* [<span data-ttu-id="901a6-129">Creare un sito Web di Azure PHP-MySQL e distribuirlo tramite FTP</span><span class="sxs-lookup"><span data-stu-id="901a6-129">Create a PHP-MySQL Azure Web Site and Deploy Using FTP</span></span>](app-service-web/web-sites-php-mysql-deploy-use-ftp.md)

## <a name="next-steps"></a><span data-ttu-id="901a6-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="901a6-130">Next steps</span></span>
<span data-ttu-id="901a6-131">Questo codice ha lo scopo di illustrare le funzionalità di base dell'utilizzo di Twilio con PHP in Azure.</span><span class="sxs-lookup"><span data-stu-id="901a6-131">This code was provided to show you basic functionality using Twilio in PHP on Azure.</span></span> <span data-ttu-id="901a6-132">Prima di eseguire la distribuzione in Azure in produzione, può essere necessario aggiungere ulteriori funzionalità per la gestione degli errori o per altri scopi.</span><span class="sxs-lookup"><span data-stu-id="901a6-132">Before deploying to Azure in production, you may want to add more error handling or other features.</span></span> <span data-ttu-id="901a6-133">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="901a6-133">For example:</span></span>

* <span data-ttu-id="901a6-134">Anziché utilizzare un modulo Web, è possibile utilizzare l'archiviazione BLOB o un database SQL di Azure per l'archiviazione di numeri di telefono e testo delle chiamate.</span><span class="sxs-lookup"><span data-stu-id="901a6-134">Instead of using a web form, you could use Azure storage blobs or SQL Database to store phone numbers and call text.</span></span> <span data-ttu-id="901a6-135">Per informazioni sull'uso dei BLOB di archiviazione di Azure in PHP, vedere [Come usare l'archiviazione BLOB da PHP][howto_blob_storage_php].</span><span class="sxs-lookup"><span data-stu-id="901a6-135">For information about using Azure storage blobs in PHP, see [Using Azure Storage with PHP Applications][howto_blob_storage_php].</span></span> <span data-ttu-id="901a6-136">Per informazioni sull'uso di database SQL in PHP, vedere [Raccolte di connessioni per database SQL e Server SQL][howto_sql_azure_php].</span><span class="sxs-lookup"><span data-stu-id="901a6-136">For information about using SQL Database in PHP, see [Using SQL Database with PHP Applications][howto_sql_azure_php].</span></span>
* <span data-ttu-id="901a6-137">Il codice **makecall.php** usa l'URL fornito da Twilio ([http://twimlets.com/message][twimlet_message_url]) per fornire una risposta TwiML (Twilio Markup Language) che indichi a Twilio come procedere con la chiamata.</span><span class="sxs-lookup"><span data-stu-id="901a6-137">The **makecall.php** code uses Twilio-provided URL ([http://twimlets.com/message][twimlet_message_url]) to provide a Twilio Markup Language (TwiML) response that informs Twilio how to proceed with the call.</span></span> <span data-ttu-id="901a6-138">Ad esempio, la risposta TwiML restituita può contenere un verbo `<Say>`, che offre una versione parlata del testo al destinatario della chiamata.</span><span class="sxs-lookup"><span data-stu-id="901a6-138">For example, the TwiML that is returned can contain a `<Say>` verb that results in text being spoken to the call recipient.</span></span> <span data-ttu-id="901a6-139">Anziché usare l'URL fornito da Twilio, è possibile creare un servizio personalizzato per rispondere alla richiesta di Twilio. Per altre informazioni, vedere [Come usare Twilio per le funzionalità voce ed SMS in PHP][howto_twilio_voice_sms_php].</span><span class="sxs-lookup"><span data-stu-id="901a6-139">Instead of using the Twilio-provided URL, you could build your own service to respond to Twilio's request; for more information, see [How to Use Twilio for Voice and SMS Capabilities in PHP][howto_twilio_voice_sms_php].</span></span> <span data-ttu-id="901a6-140">Per altre informazioni su TwiML, vedere la pagina [http://www.twilio.com/docs/api/twiml][twiml] e per altre informazioni su `<Say>` e altri verbi Twilio, vedere la pagina [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span><span class="sxs-lookup"><span data-stu-id="901a6-140">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml], and more information about `<Say>` and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>
* <span data-ttu-id="901a6-141">Leggere le linee guida sulla sicurezza di Twilio all'indirizzo [https://www.twilio.com/docs/security][twilio_docs_security].</span><span class="sxs-lookup"><span data-stu-id="901a6-141">Read the Twilio security guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>

<span data-ttu-id="901a6-142">Per altre informazioni su Twilio, vedere [https://www.twilio.com/docs][twilio_docs].</span><span class="sxs-lookup"><span data-stu-id="901a6-142">For additional information about Twilio, see [https://www.twilio.com/docs][twilio_docs].</span></span>

## <a name="see-also"></a><span data-ttu-id="901a6-143">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="901a6-143">See Also</span></span>
* [<span data-ttu-id="901a6-144">Come usare Twilio per le funzionalità voce ed SMS in PHP</span><span class="sxs-lookup"><span data-stu-id="901a6-144">How to Use Twilio for Voice and SMS Capabilities in PHP</span></span>](partner-twilio-php-how-to-use-voice-sms.md)

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
