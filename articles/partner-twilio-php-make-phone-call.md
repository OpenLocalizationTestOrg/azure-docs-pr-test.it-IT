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
# <a name="how-toomake-a-phone-call-using-twilio-in-a-php-application-on-azure"></a>Come tooMake un Twilio tramite chiamata telefonica in un'applicazione PHP in Azure
Hello seguente esempio viene illustrato come usare Twilio toomake una chiamata da una pagina web PHP ospitato in Azure. un'applicazione Hello risultante utente verrà chiesto hello di valori di chiamata telefonica, come illustrato nella seguente cattura di schermata hello.

![Modulo di chiamata di Azure con Twilio e PHP][twilio_php]

È necessario seguente hello toodo codice hello toouse in questo argomento:

1. Ottenere un account Twilio e un token di autenticazione dalla [console di Twilio][twilio_console]. tooget introduttiva Twilio, valutare al prezzo [http://www.twilio.com/pricing][twilio_pricing]. Per effettuare l'iscrizione e ottenere un account di valutazione gratuito, vedere la pagina [https://www.twilio.com/try-twilio][try_twilio].
2. Ottenere hello [libreria Twilio per PHP](https://github.com/twilio/twilio-php) o installato come un pacchetto di PERA. Per ulteriori informazioni, vedere hello [file readme](https://github.com/twilio/twilio-php/blob/master/README.md).
3. Installare hello Azure SDK per PHP. Per una panoramica di hello SDK e istruzioni su come installarlo, vedere [configurare hello Azure SDK per PHP](app-service-web/web-sites-php-mysql-deploy-use-git.md)

## <a name="create-a-web-form-for-making-a-call"></a>Creare un modulo Web per effettuare una chiamata
Hello HTML seguente codice viene illustrato come una pagina web toobuild (**callform.html**) che recupera i dati utente per effettuare una chiamata:

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

## <a name="create-hello-code-toomake-hello-call"></a>Creare una chiamata di hello toomake codice hello
Hello seguente codice mostra come toobuild **makecall.php**, che viene chiamato quando l'utente hello invia il form di hello visualizzato da **callform.html**. codice Hello riportato di seguito crea messaggio hello e genera l'errore chiamata hello. Inoltre, essere toouse che l'account di Twilio e l'autenticazione del token da hello [Twilio Console] [ twilio_console] anziché i valori segnaposto hello assegnati troppo**$sid** e **$token** codice hello riportato di seguito.

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

Inoltre toomaking hello chiamata, **makecall.php** Visualizza alcuni metadati di chiamata, come illustrato nell'immagine di hello riportata di seguito. Per altre informazioni sui metadati della chiamata, vedere [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties].

![Risposta a chiamata di Azure tramite Twilio e PHP][twilio_php_response]

## <a name="run-hello-application"></a>Eseguire un'applicazione hello
passaggio successivo Hello è toodeploy il tooAzure applicazione siti Web. Hello articoli seguenti contengono informazioni hello per la creazione di un sito Web e la distribuzione del codice con Git, FTP o WebMatrix (ma non tutte le informazioni in ogni articolo sono rilevante):

* [Creare un sito Web di Azure PHP-MySQL e distribuirlo tramite Git](app-service-web/web-sites-php-mysql-deploy-use-git.md)
* [Creare un sito Web di Azure PHP-MySQL e distribuirlo tramite FTP](app-service-web/web-sites-php-mysql-deploy-use-ftp.md)

## <a name="next-steps"></a>Passaggi successivi
Questo codice è stato fornito tooshow di funzionalità di base tramite Twilio in PHP in Azure. Prima di distribuire tooAzure nell'ambiente di produzione, è consigliabile tooadd più la gestione degli errori o altre funzionalità. ad esempio:

* Anziché utilizzare un web form, è possibile usare BLOB di archiviazione di Azure o i numeri di telefono toostore Database SQL e chiamare testo. Per informazioni sull'uso dei BLOB di archiviazione di Azure in PHP, vedere [Come usare l'archiviazione BLOB da PHP][howto_blob_storage_php]. Per informazioni sull'uso di database SQL in PHP, vedere [Raccolte di connessioni per database SQL e Server SQL][howto_sql_azure_php].
* Hello **makecall.php** codice Usa l'URL fornito Twilio ([http://twimlets.com/message][twimlet_message_url]) tooprovide una risposta di Twilio Markup Language (TwiML) che indica la modalità di Twilio tooproceed con chiamata hello. Ad esempio, può contenere i hello TwiML che viene restituito un `<Say>` verbo risultante in testo non viene pronunciata toohello chiamata destinatario. Anziché utilizzare l'URL fornito Twilio hello, è possibile creare una richiesta del tooTwilio toorespond proprio servizio. Per ulteriori informazioni, vedere [come tooUse Twilio per funzionalità voce ed SMS in PHP][howto_twilio_voice_sms_php]. Per altre informazioni su TwiML, vedere la pagina [http://www.twilio.com/docs/api/twiml][twiml] e per altre informazioni su `<Say>` e altri verbi Twilio, vedere la pagina [http://www.twilio.com/docs/api/twiml/say][twilio_say].
* Leggere le indicazioni sulla sicurezza in hello Twilio [https://www.twilio.com/docs/security][twilio_docs_security].

Per altre informazioni su Twilio, vedere [https://www.twilio.com/docs][twilio_docs].

## <a name="see-also"></a>Vedere anche
* [Come tooUse Twilio per funzionalità voce ed SMS in PHP](partner-twilio-php-how-to-use-voice-sms.md)

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
