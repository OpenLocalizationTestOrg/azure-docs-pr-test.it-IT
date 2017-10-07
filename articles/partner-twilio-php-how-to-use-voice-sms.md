---
title: aaaHow tooUse Twilio per vocali e SMS (PHP) | Documenti Microsoft
description: Informazioni su come messaggio di toomake una telefonata e inviare un SMS con il servizio API di Twilio hello in Azure. Gli esempi di codice sono scritti in PHP.
documentationcenter: php
services: 
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: 007f22e3-ac75-4868-8315-da000c2e0dd0
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 9354df8de694826a0ff7ea92620ec4d7e5c2fd70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-php"></a>Come tooUse Twilio per funzionalità voce ed SMS in PHP
Questa guida illustra come tooperform attività di programmazione comuni con hello Twilio API del servizio in Azure. scenari di Hello trattati includono una telefonata e inviare un messaggio breve servizio SMS (Message). Per ulteriori informazioni su Twilio e l'utilizzo di audio e SMS nelle applicazioni, vedere hello [passaggi successivi](#NextSteps) sezione.

## <a id="WhatIs"></a>Informazioni su Twilio
Twilio è accensione hello futuro delle comunicazioni aziendali, l'abilitazione di vocale tooembed gli sviluppatori, VoIP e nelle applicazioni di messaggistica. Essi virtualizzare tutta l'infrastruttura necessaria in un ambiente globale, basato su cloud, esporlo tramite API di comunicazione Twilio hello. Le applicazioni sono toobuild semplice e scalabile. Offre flessibilità, grazie a un modello di prezzi con pagamento al consumo, e l'affidabilità del cloud.

**Twilio vocale** consente toomake le applicazioni e ricevere chiamate telefoniche. **SMS Twilio** consente toosend l'applicazione e ricevere messaggi di testo. **Twilio Client** consente le chiamate VoIP toomake da qualsiasi telefono, tablet o browser e supporta WebRTC.

## <a id="Pricing"></a>Prezzi e offerte speciali di Twilio
I clienti di Azure riceveranno un' [offerta speciale](http://www.twilio.com/azure): $ 10 di credito Twilio all'aggiornamento dell'account Twilio. Il credito di Twilio può essere applicato tooany Twilio utilizzo ($10 credito equivalente toosending fino a 1.000 messaggi SMS o alla ricezione di too1000 in ingresso minuti vocale, a seconda della posizione di hello della destinazione e numero di messaggio o una chiamata telefonica). Per riscattare il credito Twilio e iniziare a utilizzare il servizio, visitare la pagina [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).

Twilio è un servizio con pagamento in base al consumo. Non prevede spese iniziali ed è possibile chiudere l'account in qualsiasi momento. Per altre informazioni, vedere la pagina [Twilio Pricing][twilio_pricing] (Prezzi di Twilio).

## <a id="Concepts"></a>Concetti
API di Twilio Hello è un'API RESTful che fornisce funzionalità SMS e vocale per le applicazioni. Le librerie client sono disponibili in più lingue. Per un elenco, vedere [Twilio API Libraries][twilio_libraries] (Librerie dell'API Twilio).

Gli aspetti chiave di hello Twilio API sono verbi Twilio e Twilio Markup Language (TwiML).

### <a id="Verbs"></a>Verbi Twilio
Hello API utilizza Twilio verbi. ad esempio, hello  **&lt;pronuncia&gt;**  verbo indica Twilio tooaudibly inviare un messaggio in una chiamata.

Hello seguito è riportato un elenco dei verbi di Twilio. Informazioni sui hello altri verbi tramite [la documentazione del linguaggio di Markup Twilio](http://www.twilio.com/docs/api/twiml).

* **&lt;Connessione&gt;**: connette phone tooanother di hello chiamante.
* **&lt;Raccogliere&gt;**: raccoglie cifre immesse sul tastierino telefonico hello.
* **&lt;Hangup&gt;**: termina una chiamata.
* **&lt;Play&gt;**: riproduce un file audio.
* **&lt;Pause&gt;**: attende in modo silenzioso per un numero di secondi specificato.
* **&lt;Record&gt;**: registra la voce del chiamante hello e restituisce un URL di un file che contenga la registrazione di hello.
* **&lt;Reindirizzare&gt;**: trasferisce il controllo di una telefonata o SMS toohello TwiML in un URL diverso.
* **&lt;Rifiutare&gt;**: rifiuta un fax in ingresso chiamare tooyour Twilio numero senza fatturazione si
* **&lt;Ad esempio&gt;**: converte toospeech di testo che viene effettuata una chiamata.
* **&lt;Sms&gt;**: invia un SMS.

### <a id="TwiML"></a>TwiML
TwiML è un set di istruzioni basato su XML in base a verbi Twilio hello che informano Twilio come tooprocess una telefonata o SMS.

Ad esempio, hello seguente TwiML conversione testo hello **Hello World** toospeech.

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

Quando l'applicazione chiama hello API Twilio, uno dei parametri di API hello è URL hello che restituisce una risposta TwiML hello. A scopo di sviluppo, è possibile utilizzare le risposte TwiML hello tooprovide URL fornito Twilio utilizzate dalle applicazioni. È anche possibile ospitare le proprie URL tooproduce hello TwiML risposte e un'altra opzione consiste hello toouse **TwiMLResponse** oggetto.

Per altre informazioni sui verbi Twilio, i relativi attributi e il codice TwiML, vedere [TwiML][twiml]. Per ulteriori informazioni su hello Twilio API, vedere [Twilio API][twilio_api].

## <a id="CreateAccount"></a>Creare un account Twilio
Quando sarai pronto tooget un account di Twilio, iscriversi al [provare Twilio][try_twilio]. È possibile iniziare con un account gratuito ed eseguire l'aggiornamento in un secondo momento.

Quando si effettua l'iscrizione a un account Twilio, si riceverà un ID account e un token di autenticazione. Entrambi saranno necessari toomake Twilio API chiamate. non autorizzato tooprevent tooyour account di accesso, proteggere il token di autenticazione. L'ID account e l'autenticazione token possono essere visualizzati in hello [pagina account di Twilio][twilio_account]nella hello caselle **SID di ACCOUNT** e **Authentication TOKEN**, rispettivamente.

## <a id="create_app"></a>Creare un'applicazione PHP
Un'applicazione PHP che utilizza il servizio di Twilio hello ed è in esecuzione in Azure non è diversa rispetto a qualsiasi altra applicazione PHP che utilizza il servizio di Twilio hello. Mentre i servizi di Twilio basato su REST possono essere chiamati da PHP in diversi modi, in questo articolo è incentrato sul come toouse Twilio servizi con [libreria Twilio per PHP da GitHub][twilio_php]. Per ulteriori informazioni sull'utilizzo della libreria di hello Twilio per PHP, vedere [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].

Istruzioni dettagliate per la compilazione e distribuzione di un tooAzure applicazione Twilio/PHP sono disponibili in [come tooMake un Twilio tramite chiamata telefonica in un'applicazione PHP in Azure][howto_phonecall_php].

## <a id="configure_app"></a>Configurare le librerie di Twilio tooUse dell'applicazione
È possibile configurare la libreria di Twilio applicazione hello toouse per PHP in due modi:

1. Scaricare libreria Twilio hello for PHP da GitHub ([https://github.com/twilio/twilio-php][twilio_php]) e aggiungere hello **servizi** applicazione tooyour directory.
   
    -OPPURE-
2. Come un pacchetto di PERA, installare libreria Twilio hello per PHP. Può essere installato con hello seguenti comandi:
   
        $ pear channel-discover twilio.github.com/pear
        $ pear install twilio/Services_Twilio

Dopo aver installato libreria Twilio hello per PHP, è possibile aggiungere un **require_once** istruzione nella parte superiore di hello del PHP file libreria hello tooreference:

        require_once 'Services/Twilio.php';

Per ulteriori informazioni, vedere [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].

## <a id="howto_make_call"></a>Procedura: Effettuare una chiamata in uscita
Hello seguente viene illustrato in uscita toomake chiamare utilizzando hello **Services_Twilio** classe. Questo codice usa anche un hello tooreturn sito Twilio fornita risposta Twilio Markup Language (TwiML). Sostituire i valori per hello **da** e **a** i numeri di telefono e assicurarsi che si verifichino hello **da** numero di telefono per il codice di hello Twilio account toorunning precedente.

    // Include hello Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";

    // hello number of hello phone initiating hello hello call.
    $from_number = "NNNNNNNNNNN";

    // hello number of hello phone receiving call.
    $to_number = "NNNNNNNNNNN";

    // Use hello Twilio-provided site for hello TwiML response.
    $url = "http://twimlets.com/message";

    // hello phone message text.
    $message = "Hello world.";

    // Create hello call client.
    $client = new Services_Twilio($sid, $token, $version);

    //Make hello call.
    try
    {
        $call = $client->account->calls->create(
            $from_number, 
            $to_number,
              $url.'?Message='.urlencode($message)
        );
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

Come accennato, questo codice Usa un hello tooreturn sito fornito Twilio TwiML risposta. È possibile utilizzare la propria hello tooprovide sito TwiML risposta. Per ulteriori informazioni, vedere [come tooProvide TwiML risposte da un sito Web di](#howto_provide_twiml_responses).

* **Nota**: tootroubleshoot errori di convalida certificato SSL, vedere [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation] 

## <a id="howto_send_sms"></a>Procedura: Inviare un messaggio SMS
Hello seguente viene illustrato come un messaggio SMS utilizzando toosend hello **Services_Twilio** classe. Hello **da** numero fornito dal Twilio per versione di valutazione account toosend messaggi SMS. Hello **a** numero deve essere verificato per il codice di hello Twilio account toorunning precedente.

    // Include hello Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";


    $from_number = "NNNNNNNNNNN"; // With trial account, texts can only be sent from your Twilio number.
    $to_number = "NNNNNNNNNNN";
    $message = "Hello world.";

    // Create hello call client.
    $client = new Services_Twilio($sid, $token, $version);

    // Send hello SMS message.
    try
    {
        $client->$client->account->messages->sendMessage($from_number, $to_number, $message);
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

## <a id="howto_provide_twiml_responses"></a>Procedura: Fornire risposte TwiML dal proprio sito Web
Quando l'applicazione avvia toohello una chiamata API di Twilio, Twilio invierà l'URL tooa richiesta è previsto tooreturn una risposta TwiML. esempio di Hello viene utilizzata l'URL fornito Twilio hello [http://twimlets.com/message][twimlet_message_url]. (Mentre TwiML è progettato per l'utilizzo da Twilio, è possibile visualizzare hello nel browser. Ad esempio, fare clic su [http://twimlets.com/message] [ twimlet_message_url] toosee vuota `<Response>` elemento; ad esempio, fare clic su [http://twimlets.com/message? Messaggio % 5B0 %5D = Hello % 20World] [ twimlet_message_url_hello_world] toosee un `<Response>` elemento che contiene un `<Say>` elemento.)

Anziché basarsi sul URL fornito Twilio hello, è possibile creare un sito che restituisce le risposte HTTP. È possibile creare il sito di hello in qualsiasi linguaggio che restituisce le risposte XML. In questo argomento si presuppone che verranno utilizzati hello toocreate PHP TwiML.

Hello seguente PHP pagina risultati in una risposta TwiML indicante **Hello World** chiamata hello.

    <?php    
        header("content-type: text/xml");    
        echo "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n";
    ?>
    <Response>    
        <Say>Hello world.</Say>
    </Response>

Come si può notare dal precedente esempio di hello, hello TwiML risposta è semplicemente un documento XML. libreria di Twilio Hello per PHP contiene classi che generano TwiML automaticamente. esempio Hello seguente produce risposta equivalente hello, come illustrato in precedenza, ma utilizza hello **servizi\_Twilio\_Twiml** classe nella libreria di Twilio hello per PHP:

    require_once('Services/Twilio.php');

    $response = new Services_Twilio_Twiml();
    $response->say("Hello world.");
    print $response;

Per altre informazioni su TwiML, vedere [https://www.twilio.com/docs/api/twiml][twiml_reference]. 

Dopo aver creato la pagina PHP imposta tooprovide TwiML risposte, usare hello URL della pagina PHP hello come hello URL passato hello `Services_Twilio->account->calls->create` metodo. Ad esempio, se si dispone di un'applicazione Web denominata **MyTwiML** tooan distribuito Azure servizio ospitato e hello nome della pagina PHP hello **mytwiml.php**, hello URL può essere passato troppo **Services_ Twilio -> account -> chiamate -> creare** come illustrato nell'esempio seguente hello:

    require_once 'Services/Twilio.php';

    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";
    $from_number = "NNNNNNNNNNN";
    $to_number = "NNNNNNNNNNN";
    $url = "http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.php";

    // hello phone message text.
    $message = "Hello world.";

    $client = new Services_Twilio($sid, $token, "2010-04-01");

    try
    {
        $call = $client->account->calls->create(
            $from_number, 
            $to_number,
              $url.'?Message='.urlencode($message)
        );
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

Per ulteriori informazioni sull'utilizzo di Twilio in Azure con PHP, vedere [come tooMake un Twilio tramite chiamata telefonica in un'applicazione PHP in Azure][howto_phonecall_php].

## <a id="AdditionalServices"></a>Procedura: Utilizzare servizi Twilio aggiuntivi
Inoltre toohello esempi riportati di seguito, che twilio offre API basata sul web che è possibile utilizzare altre funzionalità di Twilio tooleverage dall'applicazione Azure. Per informazioni dettagliate, vedere hello [documentazione dell'API di Twilio][twilio_api_documentation].

## <a id="NextSteps"></a>Passaggi successivi
Dopo aver appreso nozioni di base di hello di hello Twilio servizio, seguire questi toolearn collegamenti più:

* [Twilio Security Guidelines][twilio_security_guidelines] (Linee guida sulla sicurezza di Twilio)
* [Twilio HowTo's and Example Code][twilio_howtos] (Procedure e codice di esempio di Twilio)
* [Twilio Quickstart Tutorials][twilio_quickstarts] (Esercitazioni con guide rapide su Twilio) 
* [Twilio on GitHub][twilio_on_github] (Twilio su GitHub)
* [Comunicare tooTwilio supporto][twilio_support]

[twilio_php]: https://github.com/twilio/twilio-php
[twilio_lib_docs]: http://readthedocs.org/docs/twilio-php/en/latest/index.html
[twilio_github_readme]: https://github.com/twilio/twilio-php/blob/master/README.md
[ssl_validation]: http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html
[twilio_api_service]: https://api.twilio.com
[howto_phonecall_php]: partner-twilio-php-make-phone-call.md
[twilio_voice_request]: https://www.twilio.com/docs/api/twiml/twilio_request
[twilio_sms_request]: https://www.twilio.com/docs/api/twiml/sms/twilio_request
[misc_role_config_settings]: http://msdn.microsoft.com/library/windowsazure/hh690945.aspx
[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World
[twiml_reference]: https://www.twilio.com/docs/api/twiml
[twilio_pricing]: http://www.twilio.com/pricing
[special_offer]: http://ahoy.twilio.com/azure
[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_account]:  https://www.twilio.com/user/account
[verify_phone]: https://www.twilio.com/user/account/phone-numbers/verified#
[twilio_api_documentation]: http://www.twilio.com/api
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
