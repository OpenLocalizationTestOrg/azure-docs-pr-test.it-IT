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
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-php"></a><span data-ttu-id="3f534-104">Come tooUse Twilio per funzionalità voce ed SMS in PHP</span><span class="sxs-lookup"><span data-stu-id="3f534-104">How tooUse Twilio for Voice and SMS Capabilities in PHP</span></span>
<span data-ttu-id="3f534-105">Questa guida illustra come tooperform attività di programmazione comuni con hello Twilio API del servizio in Azure.</span><span class="sxs-lookup"><span data-stu-id="3f534-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="3f534-106">scenari di Hello trattati includono una telefonata e inviare un messaggio breve servizio SMS (Message).</span><span class="sxs-lookup"><span data-stu-id="3f534-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="3f534-107">Per ulteriori informazioni su Twilio e l'utilizzo di audio e SMS nelle applicazioni, vedere hello [passaggi successivi](#NextSteps) sezione.</span><span class="sxs-lookup"><span data-stu-id="3f534-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="3f534-108"><a id="WhatIs"></a>Informazioni su Twilio</span><span class="sxs-lookup"><span data-stu-id="3f534-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="3f534-109">Twilio è accensione hello futuro delle comunicazioni aziendali, l'abilitazione di vocale tooembed gli sviluppatori, VoIP e nelle applicazioni di messaggistica.</span><span class="sxs-lookup"><span data-stu-id="3f534-109">Twilio is powering hello future of business communications, enabling developers tooembed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="3f534-110">Essi virtualizzare tutta l'infrastruttura necessaria in un ambiente globale, basato su cloud, esporlo tramite API di comunicazione Twilio hello.</span><span class="sxs-lookup"><span data-stu-id="3f534-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through hello Twilio communications API platform.</span></span> <span data-ttu-id="3f534-111">Le applicazioni sono toobuild semplice e scalabile.</span><span class="sxs-lookup"><span data-stu-id="3f534-111">Applications are simple toobuild and scalable.</span></span> <span data-ttu-id="3f534-112">Offre flessibilità, grazie a un modello di prezzi con pagamento al consumo, e l'affidabilità del cloud.</span><span class="sxs-lookup"><span data-stu-id="3f534-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="3f534-113">**Twilio vocale** consente toomake le applicazioni e ricevere chiamate telefoniche.</span><span class="sxs-lookup"><span data-stu-id="3f534-113">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="3f534-114">**SMS Twilio** consente toosend l'applicazione e ricevere messaggi di testo.</span><span class="sxs-lookup"><span data-stu-id="3f534-114">**Twilio SMS** enables your application toosend and receive text messages.</span></span> <span data-ttu-id="3f534-115">**Twilio Client** consente le chiamate VoIP toomake da qualsiasi telefono, tablet o browser e supporta WebRTC.</span><span class="sxs-lookup"><span data-stu-id="3f534-115">**Twilio Client** allows you toomake VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="3f534-116"><a id="Pricing"></a>Prezzi e offerte speciali di Twilio</span><span class="sxs-lookup"><span data-stu-id="3f534-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="3f534-117">I clienti di Azure riceveranno un' [offerta speciale](http://www.twilio.com/azure): $ 10 di credito Twilio all'aggiornamento dell'account Twilio.</span><span class="sxs-lookup"><span data-stu-id="3f534-117">Azure customers receive a [special offer](http://www.twilio.com/azure): complimentary $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="3f534-118">Il credito di Twilio può essere applicato tooany Twilio utilizzo ($10 credito equivalente toosending fino a 1.000 messaggi SMS o alla ricezione di too1000 in ingresso minuti vocale, a seconda della posizione di hello della destinazione e numero di messaggio o una chiamata telefonica).</span><span class="sxs-lookup"><span data-stu-id="3f534-118">This Twilio Credit can be applied tooany Twilio usage ($10 credit equivalent toosending as many as 1,000 SMS messages or receiving up too1000 inbound Voice minutes, depending on hello location of your phone number and message or call destination).</span></span> <span data-ttu-id="3f534-119">Per riscattare il credito Twilio e iniziare a utilizzare il servizio, visitare la pagina [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span><span class="sxs-lookup"><span data-stu-id="3f534-119">Redeem this Twilio credit and get started at: [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span></span>

<span data-ttu-id="3f534-120">Twilio è un servizio con pagamento in base al consumo.</span><span class="sxs-lookup"><span data-stu-id="3f534-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="3f534-121">Non prevede spese iniziali ed è possibile chiudere l'account in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="3f534-121">There are no set-up fees and you can close your account at any time.</span></span> <span data-ttu-id="3f534-122">Per altre informazioni, vedere la pagina [Twilio Pricing][twilio_pricing] (Prezzi di Twilio).</span><span class="sxs-lookup"><span data-stu-id="3f534-122">You can find more details at [Twilio Pricing][twilio_pricing].</span></span>

## <span data-ttu-id="3f534-123"><a id="Concepts"></a>Concetti</span><span class="sxs-lookup"><span data-stu-id="3f534-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="3f534-124">API di Twilio Hello è un'API RESTful che fornisce funzionalità SMS e vocale per le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="3f534-124">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="3f534-125">Le librerie client sono disponibili in più lingue. Per un elenco, vedere [Twilio API Libraries][twilio_libraries] (Librerie dell'API Twilio).</span><span class="sxs-lookup"><span data-stu-id="3f534-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="3f534-126">Gli aspetti chiave di hello Twilio API sono verbi Twilio e Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="3f534-126">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="3f534-127"><a id="Verbs"></a>Verbi Twilio</span><span class="sxs-lookup"><span data-stu-id="3f534-127"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="3f534-128">Hello API utilizza Twilio verbi. ad esempio, hello  **&lt;pronuncia&gt;**  verbo indica Twilio tooaudibly inviare un messaggio in una chiamata.</span><span class="sxs-lookup"><span data-stu-id="3f534-128">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="3f534-129">Hello seguito è riportato un elenco dei verbi di Twilio.</span><span class="sxs-lookup"><span data-stu-id="3f534-129">hello following is a list of Twilio verbs.</span></span> <span data-ttu-id="3f534-130">Informazioni sui hello altri verbi tramite [la documentazione del linguaggio di Markup Twilio](http://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="3f534-130">Learn about hello other verbs and capabilities via [Twilio Markup Language documentation](http://www.twilio.com/docs/api/twiml).</span></span>

* <span data-ttu-id="3f534-131">**&lt;Connessione&gt;**: connette phone tooanother di hello chiamante.</span><span class="sxs-lookup"><span data-stu-id="3f534-131">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="3f534-132">**&lt;Raccogliere&gt;**: raccoglie cifre immesse sul tastierino telefonico hello.</span><span class="sxs-lookup"><span data-stu-id="3f534-132">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="3f534-133">**&lt;Hangup&gt;**: termina una chiamata.</span><span class="sxs-lookup"><span data-stu-id="3f534-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="3f534-134">**&lt;Play&gt;**: riproduce un file audio.</span><span class="sxs-lookup"><span data-stu-id="3f534-134">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="3f534-135">**&lt;Pause&gt;**: attende in modo silenzioso per un numero di secondi specificato.</span><span class="sxs-lookup"><span data-stu-id="3f534-135">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="3f534-136">**&lt;Record&gt;**: registra la voce del chiamante hello e restituisce un URL di un file che contenga la registrazione di hello.</span><span class="sxs-lookup"><span data-stu-id="3f534-136">**&lt;Record&gt;**: Records hello caller's voice and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="3f534-137">**&lt;Reindirizzare&gt;**: trasferisce il controllo di una telefonata o SMS toohello TwiML in un URL diverso.</span><span class="sxs-lookup"><span data-stu-id="3f534-137">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="3f534-138">**&lt;Rifiutare&gt;**: rifiuta un fax in ingresso chiamare tooyour Twilio numero senza fatturazione si</span><span class="sxs-lookup"><span data-stu-id="3f534-138">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you</span></span>
* <span data-ttu-id="3f534-139">**&lt;Ad esempio&gt;**: converte toospeech di testo che viene effettuata una chiamata.</span><span class="sxs-lookup"><span data-stu-id="3f534-139">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="3f534-140">**&lt;Sms&gt;**: invia un SMS.</span><span class="sxs-lookup"><span data-stu-id="3f534-140">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="3f534-141"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="3f534-141"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="3f534-142">TwiML è un set di istruzioni basato su XML in base a verbi Twilio hello che informano Twilio come tooprocess una telefonata o SMS.</span><span class="sxs-lookup"><span data-stu-id="3f534-142">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="3f534-143">Ad esempio, hello seguente TwiML conversione testo hello **Hello World** toospeech.</span><span class="sxs-lookup"><span data-stu-id="3f534-143">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="3f534-144">Quando l'applicazione chiama hello API Twilio, uno dei parametri di API hello è URL hello che restituisce una risposta TwiML hello.</span><span class="sxs-lookup"><span data-stu-id="3f534-144">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="3f534-145">A scopo di sviluppo, è possibile utilizzare le risposte TwiML hello tooprovide URL fornito Twilio utilizzate dalle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="3f534-145">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="3f534-146">È anche possibile ospitare le proprie URL tooproduce hello TwiML risposte e un'altra opzione consiste hello toouse **TwiMLResponse** oggetto.</span><span class="sxs-lookup"><span data-stu-id="3f534-146">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello **TwiMLResponse** object.</span></span>

<span data-ttu-id="3f534-147">Per altre informazioni sui verbi Twilio, i relativi attributi e il codice TwiML, vedere [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="3f534-147">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="3f534-148">Per ulteriori informazioni su hello Twilio API, vedere [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="3f534-148">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="3f534-149"><a id="CreateAccount"></a>Creare un account Twilio</span><span class="sxs-lookup"><span data-stu-id="3f534-149"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="3f534-150">Quando sarai pronto tooget un account di Twilio, iscriversi al [provare Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="3f534-150">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="3f534-151">È possibile iniziare con un account gratuito ed eseguire l'aggiornamento in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="3f534-151">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="3f534-152">Quando si effettua l'iscrizione a un account Twilio, si riceverà un ID account e un token di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="3f534-152">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="3f534-153">Entrambi saranno necessari toomake Twilio API chiamate.</span><span class="sxs-lookup"><span data-stu-id="3f534-153">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="3f534-154">non autorizzato tooprevent tooyour account di accesso, proteggere il token di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="3f534-154">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="3f534-155">L'ID account e l'autenticazione token possono essere visualizzati in hello [pagina account di Twilio][twilio_account]nella hello caselle **SID di ACCOUNT** e **Authentication TOKEN**, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="3f534-155">Your account ID and authentication token are viewable at hello [Twilio account page][twilio_account], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="3f534-156"><a id="create_app"></a>Creare un'applicazione PHP</span><span class="sxs-lookup"><span data-stu-id="3f534-156"><a id="create_app"></a>Create a PHP Application</span></span>
<span data-ttu-id="3f534-157">Un'applicazione PHP che utilizza il servizio di Twilio hello ed è in esecuzione in Azure non è diversa rispetto a qualsiasi altra applicazione PHP che utilizza il servizio di Twilio hello.</span><span class="sxs-lookup"><span data-stu-id="3f534-157">A PHP application that uses hello Twilio service and is running in Azure is no different than any other PHP application that uses hello Twilio service.</span></span> <span data-ttu-id="3f534-158">Mentre i servizi di Twilio basato su REST possono essere chiamati da PHP in diversi modi, in questo articolo è incentrato sul come toouse Twilio servizi con [libreria Twilio per PHP da GitHub][twilio_php].</span><span class="sxs-lookup"><span data-stu-id="3f534-158">While Twilio services are REST-based and can be called from PHP in several ways, this article will focus on how toouse Twilio services with [Twilio library for PHP from GitHub][twilio_php].</span></span> <span data-ttu-id="3f534-159">Per ulteriori informazioni sull'utilizzo della libreria di hello Twilio per PHP, vedere [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].</span><span class="sxs-lookup"><span data-stu-id="3f534-159">For more information about using hello Twilio library for PHP, see [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].</span></span>

<span data-ttu-id="3f534-160">Istruzioni dettagliate per la compilazione e distribuzione di un tooAzure applicazione Twilio/PHP sono disponibili in [come tooMake un Twilio tramite chiamata telefonica in un'applicazione PHP in Azure][howto_phonecall_php].</span><span class="sxs-lookup"><span data-stu-id="3f534-160">Detailed instructions for building and deploying a Twilio/PHP application tooAzure are available at [How tooMake a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="3f534-161"><a id="configure_app"></a>Configurare le librerie di Twilio tooUse dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="3f534-161"><a id="configure_app"></a>Configure Your Application tooUse Twilio Libraries</span></span>
<span data-ttu-id="3f534-162">È possibile configurare la libreria di Twilio applicazione hello toouse per PHP in due modi:</span><span class="sxs-lookup"><span data-stu-id="3f534-162">You can configure your application toouse hello Twilio library for PHP in two ways:</span></span>

1. <span data-ttu-id="3f534-163">Scaricare libreria Twilio hello for PHP da GitHub ([https://github.com/twilio/twilio-php][twilio_php]) e aggiungere hello **servizi** applicazione tooyour directory.</span><span class="sxs-lookup"><span data-stu-id="3f534-163">Download hello Twilio library for PHP from GitHub ([https://github.com/twilio/twilio-php][twilio_php]) and add hello **Services** directory tooyour application.</span></span>
   
    <span data-ttu-id="3f534-164">-OPPURE-</span><span class="sxs-lookup"><span data-stu-id="3f534-164">-OR-</span></span>
2. <span data-ttu-id="3f534-165">Come un pacchetto di PERA, installare libreria Twilio hello per PHP.</span><span class="sxs-lookup"><span data-stu-id="3f534-165">Install hello Twilio library for PHP as a PEAR package.</span></span> <span data-ttu-id="3f534-166">Può essere installato con hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="3f534-166">It can be installed with hello following commands:</span></span>
   
        $ pear channel-discover twilio.github.com/pear
        $ pear install twilio/Services_Twilio

<span data-ttu-id="3f534-167">Dopo aver installato libreria Twilio hello per PHP, è possibile aggiungere un **require_once** istruzione nella parte superiore di hello del PHP file libreria hello tooreference:</span><span class="sxs-lookup"><span data-stu-id="3f534-167">Once you have installed hello Twilio library for PHP, you can then add a **require_once** statement at hello top of your PHP files tooreference hello library:</span></span>

        require_once 'Services/Twilio.php';

<span data-ttu-id="3f534-168">Per ulteriori informazioni, vedere [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].</span><span class="sxs-lookup"><span data-stu-id="3f534-168">For more information, see [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].</span></span>

## <span data-ttu-id="3f534-169"><a id="howto_make_call"></a>Procedura: Effettuare una chiamata in uscita</span><span class="sxs-lookup"><span data-stu-id="3f534-169"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="3f534-170">Hello seguente viene illustrato in uscita toomake chiamare utilizzando hello **Services_Twilio** classe.</span><span class="sxs-lookup"><span data-stu-id="3f534-170">hello following shows how toomake an outgoing call using hello **Services_Twilio** class.</span></span> <span data-ttu-id="3f534-171">Questo codice usa anche un hello tooreturn sito Twilio fornita risposta Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="3f534-171">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="3f534-172">Sostituire i valori per hello **da** e **a** i numeri di telefono e assicurarsi che si verifichino hello **da** numero di telefono per il codice di hello Twilio account toorunning precedente.</span><span class="sxs-lookup"><span data-stu-id="3f534-172">Substitute your values for hello **From** and **To** phone numbers, and ensure that you verify hello **From** phone number for your Twilio account prior toorunning hello code.</span></span>

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

<span data-ttu-id="3f534-173">Come accennato, questo codice Usa un hello tooreturn sito fornito Twilio TwiML risposta.</span><span class="sxs-lookup"><span data-stu-id="3f534-173">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="3f534-174">È possibile utilizzare la propria hello tooprovide sito TwiML risposta. Per ulteriori informazioni, vedere [come tooProvide TwiML risposte da un sito Web di](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="3f534-174">You could instead use your own site tooprovide hello TwiML response; for more information, see [How tooProvide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span></span>

* <span data-ttu-id="3f534-175">**Nota**: tootroubleshoot errori di convalida certificato SSL, vedere [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span><span class="sxs-lookup"><span data-stu-id="3f534-175">**Note**: tootroubleshoot SSL certificate validation errors, see [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span></span> 

## <span data-ttu-id="3f534-176"><a id="howto_send_sms"></a>Procedura: Inviare un messaggio SMS</span><span class="sxs-lookup"><span data-stu-id="3f534-176"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="3f534-177">Hello seguente viene illustrato come un messaggio SMS utilizzando toosend hello **Services_Twilio** classe.</span><span class="sxs-lookup"><span data-stu-id="3f534-177">hello following shows how toosend an SMS message using hello **Services_Twilio** class.</span></span> <span data-ttu-id="3f534-178">Hello **da** numero fornito dal Twilio per versione di valutazione account toosend messaggi SMS.</span><span class="sxs-lookup"><span data-stu-id="3f534-178">hello **From** number is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="3f534-179">Hello **a** numero deve essere verificato per il codice di hello Twilio account toorunning precedente.</span><span class="sxs-lookup"><span data-stu-id="3f534-179">hello **To** number must be verified for your Twilio account prior toorunning hello code.</span></span>

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

## <span data-ttu-id="3f534-180"><a id="howto_provide_twiml_responses"></a>Procedura: Fornire risposte TwiML dal proprio sito Web</span><span class="sxs-lookup"><span data-stu-id="3f534-180"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="3f534-181">Quando l'applicazione avvia toohello una chiamata API di Twilio, Twilio invierà l'URL tooa richiesta è previsto tooreturn una risposta TwiML.</span><span class="sxs-lookup"><span data-stu-id="3f534-181">When your application initiates a call toohello Twilio API, Twilio will send your request tooa URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="3f534-182">esempio di Hello viene utilizzata l'URL fornito Twilio hello [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="3f534-182">hello example above uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="3f534-183">(Mentre TwiML è progettato per l'utilizzo da Twilio, è possibile visualizzare hello nel browser.</span><span class="sxs-lookup"><span data-stu-id="3f534-183">(While TwiML is designed for use by Twilio, you can view hello it in your browser.</span></span> <span data-ttu-id="3f534-184">Ad esempio, fare clic su [http://twimlets.com/message] [ twimlet_message_url] toosee vuota `<Response>` elemento; ad esempio, fare clic su [http://twimlets.com/message? Messaggio % 5B0 %5D = Hello % 20World] [ twimlet_message_url_hello_world] toosee un `<Response>` elemento che contiene un `<Say>` elemento.)</span><span class="sxs-lookup"><span data-stu-id="3f534-184">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] toosee a `<Response>` element that contains a `<Say>` element.)</span></span>

<span data-ttu-id="3f534-185">Anziché basarsi sul URL fornito Twilio hello, è possibile creare un sito che restituisce le risposte HTTP.</span><span class="sxs-lookup"><span data-stu-id="3f534-185">Instead of relying on hello Twilio-provided URL, you can create your own site that returns HTTP responses.</span></span> <span data-ttu-id="3f534-186">È possibile creare il sito di hello in qualsiasi linguaggio che restituisce le risposte XML. In questo argomento si presuppone che verranno utilizzati hello toocreate PHP TwiML.</span><span class="sxs-lookup"><span data-stu-id="3f534-186">You can create hello site in any language that returns XML responses; this topic assumes you'll be using PHP toocreate hello TwiML.</span></span>

<span data-ttu-id="3f534-187">Hello seguente PHP pagina risultati in una risposta TwiML indicante **Hello World** chiamata hello.</span><span class="sxs-lookup"><span data-stu-id="3f534-187">hello following PHP page results in a TwiML response that says **Hello World** on hello call.</span></span>

    <?php    
        header("content-type: text/xml");    
        echo "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n";
    ?>
    <Response>    
        <Say>Hello world.</Say>
    </Response>

<span data-ttu-id="3f534-188">Come si può notare dal precedente esempio di hello, hello TwiML risposta è semplicemente un documento XML.</span><span class="sxs-lookup"><span data-stu-id="3f534-188">As you can see from hello example above, hello TwiML response is simply an XML document.</span></span> <span data-ttu-id="3f534-189">libreria di Twilio Hello per PHP contiene classi che generano TwiML automaticamente.</span><span class="sxs-lookup"><span data-stu-id="3f534-189">hello Twilio library for PHP contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="3f534-190">esempio Hello seguente produce risposta equivalente hello, come illustrato in precedenza, ma utilizza hello **servizi\_Twilio\_Twiml** classe nella libreria di Twilio hello per PHP:</span><span class="sxs-lookup"><span data-stu-id="3f534-190">hello example below produces hello equivalent response as shown above, but uses hello **Services\_Twilio\_Twiml** class in hello Twilio library for PHP:</span></span>

    require_once('Services/Twilio.php');

    $response = new Services_Twilio_Twiml();
    $response->say("Hello world.");
    print $response;

<span data-ttu-id="3f534-191">Per altre informazioni su TwiML, vedere [https://www.twilio.com/docs/api/twiml][twiml_reference].</span><span class="sxs-lookup"><span data-stu-id="3f534-191">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span></span> 

<span data-ttu-id="3f534-192">Dopo aver creato la pagina PHP imposta tooprovide TwiML risposte, usare hello URL della pagina PHP hello come hello URL passato hello `Services_Twilio->account->calls->create` metodo.</span><span class="sxs-lookup"><span data-stu-id="3f534-192">Once you have your PHP page set up tooprovide TwiML responses, use hello URL of hello PHP page as hello URL passed into hello  `Services_Twilio->account->calls->create`  method.</span></span> <span data-ttu-id="3f534-193">Ad esempio, se si dispone di un'applicazione Web denominata **MyTwiML** tooan distribuito Azure servizio ospitato e hello nome della pagina PHP hello **mytwiml.php**, hello URL può essere passato troppo **Services_ Twilio -> account -> chiamate -> creare** come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="3f534-193">For example, if you have a Web application named **MyTwiML** deployed tooan Azure hosted service, and hello name of hello PHP page is **mytwiml.php**, hello URL can be passed too **Services_Twilio->account->calls->create**  as shown in hello following example:</span></span>

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

<span data-ttu-id="3f534-194">Per ulteriori informazioni sull'utilizzo di Twilio in Azure con PHP, vedere [come tooMake un Twilio tramite chiamata telefonica in un'applicazione PHP in Azure][howto_phonecall_php].</span><span class="sxs-lookup"><span data-stu-id="3f534-194">For additional information about using Twilio in Azure with PHP, see [How tooMake a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="3f534-195"><a id="AdditionalServices"></a>Procedura: Utilizzare servizi Twilio aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="3f534-195"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="3f534-196">Inoltre toohello esempi riportati di seguito, che twilio offre API basata sul web che è possibile utilizzare altre funzionalità di Twilio tooleverage dall'applicazione Azure.</span><span class="sxs-lookup"><span data-stu-id="3f534-196">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="3f534-197">Per informazioni dettagliate, vedere hello [documentazione dell'API di Twilio][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="3f534-197">For full details, see hello [Twilio API documentation][twilio_api_documentation].</span></span>

## <span data-ttu-id="3f534-198"><a id="NextSteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3f534-198"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="3f534-199">Dopo aver appreso nozioni di base di hello di hello Twilio servizio, seguire questi toolearn collegamenti più:</span><span class="sxs-lookup"><span data-stu-id="3f534-199">Now that you've learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="3f534-200">[Twilio Security Guidelines][twilio_security_guidelines] (Linee guida sulla sicurezza di Twilio)</span><span class="sxs-lookup"><span data-stu-id="3f534-200">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="3f534-201">[Twilio HowTo's and Example Code][twilio_howtos] (Procedure e codice di esempio di Twilio)</span><span class="sxs-lookup"><span data-stu-id="3f534-201">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="3f534-202">[Twilio Quickstart Tutorials][twilio_quickstarts] (Esercitazioni con guide rapide su Twilio)</span><span class="sxs-lookup"><span data-stu-id="3f534-202">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="3f534-203">[Twilio on GitHub][twilio_on_github] (Twilio su GitHub)</span><span class="sxs-lookup"><span data-stu-id="3f534-203">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="3f534-204">[Comunicare tooTwilio supporto][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="3f534-204">[Talk tooTwilio Support][twilio_support]</span></span>

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
