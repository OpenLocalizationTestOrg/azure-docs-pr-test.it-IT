---
title: "Come usare Twilio per le funzionalità voce e SMS (PHP) | Microsoft Docs"
description: Informazioni su come effettuare una chiamata telefonica e inviare un SMS con il servizio API Twilio API in Azure. Gli esempi di codice sono scritti in PHP.
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
ms.openlocfilehash: bd50eac7390e8639f77894689388e6926cdb619c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-in-php"></a><span data-ttu-id="8dc20-104">Come usare Twilio per le funzionalità voce ed SMS in PHP</span><span class="sxs-lookup"><span data-stu-id="8dc20-104">How to Use Twilio for Voice and SMS Capabilities in PHP</span></span>
<span data-ttu-id="8dc20-105">In questa guida viene illustrato come eseguire attività di programmazione comuni con il servizio API Twilio in Azure.</span><span class="sxs-lookup"><span data-stu-id="8dc20-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="8dc20-106">Gli scenari presentati includono la composizione di una chiamata telefonica e l'invio di un messaggio SMS (Short Message Service).</span><span class="sxs-lookup"><span data-stu-id="8dc20-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="8dc20-107">Per altre informazioni su Twilio e sull'utilizzo delle funzionalità voce ed SMS nelle applicazioni, vedere la sezione [Passaggi successivi](#NextSteps) .</span><span class="sxs-lookup"><span data-stu-id="8dc20-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="8dc20-108"><a id="WhatIs"></a>Informazioni su Twilio</span><span class="sxs-lookup"><span data-stu-id="8dc20-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="8dc20-109">Twilio è una tecnologia all'avanguardia per le comunicazioni aziendali che consente agli sviluppatori di incorporare funzionalità voce, VoIP e di messaggistica nelle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="8dc20-109">Twilio is powering the future of business communications, enabling developers to embed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="8dc20-110">Consente di virtualizzare tutta l'infrastruttura necessaria in un ambiente globale basato su cloud, esponendolo attraverso la piattaforma API per le comunicazioni Twilio.</span><span class="sxs-lookup"><span data-stu-id="8dc20-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through the Twilio communications API platform.</span></span> <span data-ttu-id="8dc20-111">Le applicazioni sono scalabili e facili da compilare.</span><span class="sxs-lookup"><span data-stu-id="8dc20-111">Applications are simple to build and scalable.</span></span> <span data-ttu-id="8dc20-112">Offre flessibilità, grazie a un modello di prezzi con pagamento al consumo, e l'affidabilità del cloud.</span><span class="sxs-lookup"><span data-stu-id="8dc20-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="8dc20-113">**Twilio Voice** consente alle applicazioni di effettuare e ricevere chiamate telefoniche.</span><span class="sxs-lookup"><span data-stu-id="8dc20-113">**Twilio Voice** allows your applications to make and receive phone calls.</span></span> <span data-ttu-id="8dc20-114">**Twilio SMS** consente alle applicazioni di inviare e ricevere messaggi di testo.</span><span class="sxs-lookup"><span data-stu-id="8dc20-114">**Twilio SMS** enables your application to send and receive text messages.</span></span> <span data-ttu-id="8dc20-115">**Twilio Client** consente di effettuare chiamate VoIP da qualsiasi telefono, tablet o browser e supporta WebRTC.</span><span class="sxs-lookup"><span data-stu-id="8dc20-115">**Twilio Client** allows you to make VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="8dc20-116"><a id="Pricing"></a>Prezzi e offerte speciali di Twilio</span><span class="sxs-lookup"><span data-stu-id="8dc20-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="8dc20-117">I clienti di Azure riceveranno un' [offerta speciale](http://www.twilio.com/azure): $ 10 di credito Twilio all'aggiornamento dell'account Twilio.</span><span class="sxs-lookup"><span data-stu-id="8dc20-117">Azure customers receive a [special offer](http://www.twilio.com/azure): complimentary $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="8dc20-118">Il credito Twilio può essere applicato a qualsiasi utilizzo di Twilio ($ 10 di credito equivalgono all'invio di 1.000 SMS o a 1.000 minuti voce per le chiamate in entrata, a seconda della località del numero di telefono, del messaggio o della destinazione della chiamata).</span><span class="sxs-lookup"><span data-stu-id="8dc20-118">This Twilio Credit can be applied to any Twilio usage ($10 credit equivalent to sending as many as 1,000 SMS messages or receiving up to 1000 inbound Voice minutes, depending on the location of your phone number and message or call destination).</span></span> <span data-ttu-id="8dc20-119">Per riscattare il credito Twilio e iniziare a utilizzare il servizio, visitare la pagina [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span><span class="sxs-lookup"><span data-stu-id="8dc20-119">Redeem this Twilio credit and get started at: [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span></span>

<span data-ttu-id="8dc20-120">Twilio è un servizio con pagamento in base al consumo.</span><span class="sxs-lookup"><span data-stu-id="8dc20-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="8dc20-121">Non prevede spese iniziali ed è possibile chiudere l'account in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="8dc20-121">There are no set-up fees and you can close your account at any time.</span></span> <span data-ttu-id="8dc20-122">Per altre informazioni, vedere la pagina [Twilio Pricing][twilio_pricing] (Prezzi di Twilio).</span><span class="sxs-lookup"><span data-stu-id="8dc20-122">You can find more details at [Twilio Pricing][twilio_pricing].</span></span>

## <span data-ttu-id="8dc20-123"><a id="Concepts"></a>Concetti</span><span class="sxs-lookup"><span data-stu-id="8dc20-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="8dc20-124">L'API Twilio è un'API RESTful che fornisce funzionalità voce ed SMS per le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="8dc20-124">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="8dc20-125">Le librerie client sono disponibili in più lingue. Per un elenco, vedere [Twilio API Libraries][twilio_libraries] (Librerie dell'API Twilio).</span><span class="sxs-lookup"><span data-stu-id="8dc20-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="8dc20-126">I concetti principali dell'API Twilio sono costituiti dai verbi Twilio e dal linguaggio di markup Twilio (Twilio Markup Language, TwiML).</span><span class="sxs-lookup"><span data-stu-id="8dc20-126">Key aspects of the Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="8dc20-127"><a id="Verbs"></a>Verbi Twilio</span><span class="sxs-lookup"><span data-stu-id="8dc20-127"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="8dc20-128">Nell'API vengono usati i verbi di Twilio: il verbo **&lt;Say&gt;**, ad esempio, indica a Twilio di recapitare un messaggio acustico in una chiamata.</span><span class="sxs-lookup"><span data-stu-id="8dc20-128">The API makes use of Twilio verbs; for example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span>

<span data-ttu-id="8dc20-129">Di seguito è riportato un elenco dei verbi Twilio.</span><span class="sxs-lookup"><span data-stu-id="8dc20-129">The following is a list of Twilio verbs.</span></span> <span data-ttu-id="8dc20-130">Per altre informazioni su altri verbi e funzionalità, vedere la [documentazione relativa a Twilio Markup Language](http://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="8dc20-130">Learn about the other verbs and capabilities via [Twilio Markup Language documentation](http://www.twilio.com/docs/api/twiml).</span></span>

* <span data-ttu-id="8dc20-131">**&lt;Dial&gt;**: connette il chiamante a un altro telefono.</span><span class="sxs-lookup"><span data-stu-id="8dc20-131">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="8dc20-132">**&lt;Gather&gt;**: raccoglie i numeri digitati sulla tastiera del telefono.</span><span class="sxs-lookup"><span data-stu-id="8dc20-132">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="8dc20-133">**&lt;Hangup&gt;**: termina una chiamata.</span><span class="sxs-lookup"><span data-stu-id="8dc20-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="8dc20-134">**&lt;Play&gt;**: riproduce un file audio.</span><span class="sxs-lookup"><span data-stu-id="8dc20-134">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="8dc20-135">**&lt;Pause&gt;**: attende in modo silenzioso per un numero di secondi specificato.</span><span class="sxs-lookup"><span data-stu-id="8dc20-135">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="8dc20-136">**&lt;Record&gt;**: registra la voce del chiamante e restituisce l'URL del file contenente la registrazione.</span><span class="sxs-lookup"><span data-stu-id="8dc20-136">**&lt;Record&gt;**: Records the caller's voice and returns a URL of a file that contains the recording.</span></span>
* <span data-ttu-id="8dc20-137">**&lt;Redirect&gt;**: trasferisce il controllo di una chiamata o di un SMS al codice TwiML presso un URL diverso.</span><span class="sxs-lookup"><span data-stu-id="8dc20-137">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="8dc20-138">**&lt;Reject&gt;**: rifiuta una chiamata in arrivo al numero Twilio senza alcun addebito.</span><span class="sxs-lookup"><span data-stu-id="8dc20-138">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you</span></span>
* <span data-ttu-id="8dc20-139">**&lt;Say&gt;**: effettua la sintesi vocale del testo durante una chiamata.</span><span class="sxs-lookup"><span data-stu-id="8dc20-139">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="8dc20-140">**&lt;Sms&gt;**: invia un SMS.</span><span class="sxs-lookup"><span data-stu-id="8dc20-140">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="8dc20-141"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="8dc20-141"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="8dc20-142">TwiML è un set di istruzioni basate su XML e sui verbi Twilio che indicano a Twilio come elaborare una chiamata o un SMS.</span><span class="sxs-lookup"><span data-stu-id="8dc20-142">TwiML is a set of XML-based instructions based on the Twilio verbs that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="8dc20-143">Ad esempio, il codice TwiML seguente effettua la sintesi vocale del testo **Hello World** .</span><span class="sxs-lookup"><span data-stu-id="8dc20-143">As an example, the following TwiML would convert the text **Hello World** to speech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="8dc20-144">Quando l'applicazione chiama l'API Twilio, uno dei parametri dell'API è l'URL che restituisce la risposta TwiML.</span><span class="sxs-lookup"><span data-stu-id="8dc20-144">When your application calls the Twilio API, one of the API parameters is the URL that returns the TwiML response.</span></span> <span data-ttu-id="8dc20-145">Ai fini dello sviluppo, è possibile utilizzare gli URL offerti da Twilio per fornire le risposte TwiML utilizzate dalle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="8dc20-145">For development purposes, you can use Twilio-provided URLs to provide the TwiML responses used by your applications.</span></span> <span data-ttu-id="8dc20-146">È inoltre possibile ospitare gli URL per produrre le risposte TwiML oppure utilizzare l'oggetto **TwiMLResponse** .</span><span class="sxs-lookup"><span data-stu-id="8dc20-146">You could also host your own URLs to produce the TwiML responses, and another option is to use the **TwiMLResponse** object.</span></span>

<span data-ttu-id="8dc20-147">Per altre informazioni sui verbi Twilio, i relativi attributi e il codice TwiML, vedere [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="8dc20-147">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="8dc20-148">Per altre informazioni sull'API Twilio, vedere [Twilio API][twilio_api] (API Twilio).</span><span class="sxs-lookup"><span data-stu-id="8dc20-148">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="8dc20-149"><a id="CreateAccount"></a>Creare un account Twilio</span><span class="sxs-lookup"><span data-stu-id="8dc20-149"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="8dc20-150">Se si desidera creare un account Twilio, iscriversi nella pagina [Try Twilio][try_twilio] (Provare Twilio).</span><span class="sxs-lookup"><span data-stu-id="8dc20-150">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="8dc20-151">È possibile iniziare con un account gratuito ed eseguire l'aggiornamento in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="8dc20-151">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="8dc20-152">Quando si effettua l'iscrizione a un account Twilio, si riceverà un ID account e un token di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="8dc20-152">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="8dc20-153">Entrambe queste informazioni sono necessarie per effettuare chiamate all'API Twilio.</span><span class="sxs-lookup"><span data-stu-id="8dc20-153">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="8dc20-154">Per prevenire accessi autorizzati all'account, conservare il token di autenticazione in un luogo sicuro.</span><span class="sxs-lookup"><span data-stu-id="8dc20-154">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="8dc20-155">L'ID account e il token di autorizzazione sono visualizzabili nella [pagina dell'account Twilio][twilio_account], rispettivamente nei campi **ACCOUNT SID** (SID ACCOUNT) e **AUTH TOKEN** (TOKEN AUTORIZZAZIONE).</span><span class="sxs-lookup"><span data-stu-id="8dc20-155">Your account ID and authentication token are viewable at the [Twilio account page][twilio_account], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="8dc20-156"><a id="create_app"></a>Creare un'applicazione PHP</span><span class="sxs-lookup"><span data-stu-id="8dc20-156"><a id="create_app"></a>Create a PHP Application</span></span>
<span data-ttu-id="8dc20-157">Un'applicazione PHP che usa il servizio Twilio e viene eseguita in Azure non è diversa da qualsiasi altra applicazione PHP che usa il servizio Twilio.</span><span class="sxs-lookup"><span data-stu-id="8dc20-157">A PHP application that uses the Twilio service and is running in Azure is no different than any other PHP application that uses the Twilio service.</span></span> <span data-ttu-id="8dc20-158">Mentre i servizi di Twilio basato su REST possono essere chiamati da PHP in diversi modi, questo articolo è incentrato sull'utilizzo di servizi di Twilio con [libreria Twilio per PHP da GitHub][twilio_php].</span><span class="sxs-lookup"><span data-stu-id="8dc20-158">While Twilio services are REST-based and can be called from PHP in several ways, this article will focus on how to use Twilio services with [Twilio library for PHP from GitHub][twilio_php].</span></span> <span data-ttu-id="8dc20-159">Per ulteriori informazioni sull'utilizzo della libreria di Twilio per PHP, vedere [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].</span><span class="sxs-lookup"><span data-stu-id="8dc20-159">For more information about using the Twilio library for PHP, see [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].</span></span>

<span data-ttu-id="8dc20-160">Istruzioni dettagliate per la compilazione e distribuzione di un'applicazione di Twilio/PHP in Azure sono disponibili in [come rendere un Twilio tramite chiamata telefonica in un'applicazione PHP in Azure][howto_phonecall_php].</span><span class="sxs-lookup"><span data-stu-id="8dc20-160">Detailed instructions for building and deploying a Twilio/PHP application to Azure are available at [How to Make a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="8dc20-161"><a id="configure_app"></a>Configurare l'applicazione per l'uso delle librerie Twilio</span><span class="sxs-lookup"><span data-stu-id="8dc20-161"><a id="configure_app"></a>Configure Your Application to Use Twilio Libraries</span></span>
<span data-ttu-id="8dc20-162">È possibile configurare l'applicazione in modo che usi la libreria Twilio per PHP in due modi:</span><span class="sxs-lookup"><span data-stu-id="8dc20-162">You can configure your application to use the Twilio library for PHP in two ways:</span></span>

1. <span data-ttu-id="8dc20-163">Scaricare la libreria di Twilio per PHP da GitHub ([https://github.com/twilio/twilio-php][twilio_php]) e aggiungere il **servizi** directory all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8dc20-163">Download the Twilio library for PHP from GitHub ([https://github.com/twilio/twilio-php][twilio_php]) and add the **Services** directory to your application.</span></span>
   
    <span data-ttu-id="8dc20-164">-OPPURE-</span><span class="sxs-lookup"><span data-stu-id="8dc20-164">-OR-</span></span>
2. <span data-ttu-id="8dc20-165">Installare la libreria Twilio per PHP come pacchetto PEAR.</span><span class="sxs-lookup"><span data-stu-id="8dc20-165">Install the Twilio library for PHP as a PEAR package.</span></span> <span data-ttu-id="8dc20-166">È possibile eseguire l'installazione tramite i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="8dc20-166">It can be installed with the following commands:</span></span>
   
        $ pear channel-discover twilio.github.com/pear
        $ pear install twilio/Services_Twilio

<span data-ttu-id="8dc20-167">Dopo avere installato la libreria Twilio per PHP, sarà possibile aggiungere un'istruzione **require_once** nella parte superiore del file PHP, in modo che faccia riferimento alla libreria:</span><span class="sxs-lookup"><span data-stu-id="8dc20-167">Once you have installed the Twilio library for PHP, you can then add a **require_once** statement at the top of your PHP files to reference the library:</span></span>

        require_once 'Services/Twilio.php';

<span data-ttu-id="8dc20-168">Per ulteriori informazioni, vedere [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].</span><span class="sxs-lookup"><span data-stu-id="8dc20-168">For more information, see [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].</span></span>

## <span data-ttu-id="8dc20-169"><a id="howto_make_call"></a>Procedura: Effettuare una chiamata in uscita</span><span class="sxs-lookup"><span data-stu-id="8dc20-169"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="8dc20-170">Di seguito è illustrato come effettuare una chiamata in uscita tramite la classe **Services_Twilio**.</span><span class="sxs-lookup"><span data-stu-id="8dc20-170">The following shows how to make an outgoing call using the **Services_Twilio** class.</span></span> <span data-ttu-id="8dc20-171">Questo codice utilizza inoltre un sito fornito da Twilio per restituire la risposta TwiML (Twilio Markup Language).</span><span class="sxs-lookup"><span data-stu-id="8dc20-171">This code also uses a Twilio-provided site to return the Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="8dc20-172">Sostituire i valori per i numeri di telefono **From** e **To** e assicurarsi di verificare il numero di telefono in **From** per l'account Twilio prima di eseguire il codice.</span><span class="sxs-lookup"><span data-stu-id="8dc20-172">Substitute your values for the **From** and **To** phone numbers, and ensure that you verify the **From** phone number for your Twilio account prior to running the code.</span></span>

    // Include the Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";

    // The number of the phone initiating the the call.
    $from_number = "NNNNNNNNNNN";

    // The number of the phone receiving call.
    $to_number = "NNNNNNNNNNN";

    // Use the Twilio-provided site for the TwiML response.
    $url = "http://twimlets.com/message";

    // The phone message text.
    $message = "Hello world.";

    // Create the call client.
    $client = new Services_Twilio($sid, $token, $version);

    //Make the call.
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

<span data-ttu-id="8dc20-173">Come indicato in precedenza, questo codice utilizza un sito fornito da Twilio per restituire la risposta TwiML.</span><span class="sxs-lookup"><span data-stu-id="8dc20-173">As mentioned, this code uses a Twilio-provided site to return the TwiML response.</span></span> <span data-ttu-id="8dc20-174">Per fornire la risposta TwiML è inoltre possibile usare il proprio sito. Per altre informazioni, vedere [Come fornire risposte TwiML dal proprio sito Web](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="8dc20-174">You could instead use your own site to provide the TwiML response; for more information, see [How to Provide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span></span>

* <span data-ttu-id="8dc20-175">**Nota**: per risolvere errori di convalida del certificato SSL, vedere [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span><span class="sxs-lookup"><span data-stu-id="8dc20-175">**Note**: To troubleshoot SSL certificate validation errors, see [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span></span> 

## <span data-ttu-id="8dc20-176"><a id="howto_send_sms"></a>Procedura: Inviare un messaggio SMS</span><span class="sxs-lookup"><span data-stu-id="8dc20-176"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="8dc20-177">Nella schermata seguente è illustrato come inviare un SMS tramite la classe **Services_Twilio**.</span><span class="sxs-lookup"><span data-stu-id="8dc20-177">The following shows how to send an SMS message using the **Services_Twilio** class.</span></span> <span data-ttu-id="8dc20-178">Il numero in **From** per l'invio di messaggi SMS con gli account di valutazione è fornito da Twilio.</span><span class="sxs-lookup"><span data-stu-id="8dc20-178">The **From** number is provided by Twilio for trial accounts to send SMS messages.</span></span> <span data-ttu-id="8dc20-179">Il numero in **To** deve essere verificato per l'account Twilio prima di eseguire il codice.</span><span class="sxs-lookup"><span data-stu-id="8dc20-179">The **To** number must be verified for your Twilio account prior to running the code.</span></span>

    // Include the Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";


    $from_number = "NNNNNNNNNNN"; // With trial account, texts can only be sent from your Twilio number.
    $to_number = "NNNNNNNNNNN";
    $message = "Hello world.";

    // Create the call client.
    $client = new Services_Twilio($sid, $token, $version);

    // Send the SMS message.
    try
    {
        $client->$client->account->messages->sendMessage($from_number, $to_number, $message);
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

## <span data-ttu-id="8dc20-180"><a id="howto_provide_twiml_responses"></a>Procedura: Fornire risposte TwiML dal proprio sito Web</span><span class="sxs-lookup"><span data-stu-id="8dc20-180"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="8dc20-181">Quando l'applicazione avvia una chiamata all'API Twilio, Twilio invia la richiesta a un URL che deve restituire una risposta TwiML.</span><span class="sxs-lookup"><span data-stu-id="8dc20-181">When your application initiates a call to the Twilio API, Twilio will send your request to a URL that is expected to return a TwiML response.</span></span> <span data-ttu-id="8dc20-182">Nell'esempio precedente viene usato l'URL fornito da Twilio [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="8dc20-182">The example above uses the Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="8dc20-183">Poiché TwiML è progettato per essere usato da Twilio, è possibile visualizzarlo nel browser.</span><span class="sxs-lookup"><span data-stu-id="8dc20-183">(While TwiML is designed for use by Twilio, you can view the it in your browser.</span></span> <span data-ttu-id="8dc20-184">Ad esempio, fare clic su [http://twimlets.com/message][twimlet_message_url] per visualizzare un elemento `<Response>` vuoto oppure fare clic su [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] per visualizzare un elemento `<Response>` contenente un elemento `<Say>`.</span><span class="sxs-lookup"><span data-stu-id="8dc20-184">For example, click [http://twimlets.com/message][twimlet_message_url] to see an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] to see a `<Response>` element that contains a `<Say>` element.)</span></span>

<span data-ttu-id="8dc20-185">Anziché utilizzare l'URL fornito da Twilio, è possibile creare un sito personalizzato che restituisce risposte HTTP.</span><span class="sxs-lookup"><span data-stu-id="8dc20-185">Instead of relying on the Twilio-provided URL, you can create your own site that returns HTTP responses.</span></span> <span data-ttu-id="8dc20-186">È possibile creare il sito in qualsiasi linguaggio che restituisca risposte XML. In questo argomento si presuppone che si userà PHP per creare TwiML.</span><span class="sxs-lookup"><span data-stu-id="8dc20-186">You can create the site in any language that returns XML responses; this topic assumes you'll be using PHP to create the TwiML.</span></span>

<span data-ttu-id="8dc20-187">La pagina PHP seguente crea una risposta TwiML che pronuncia **Hello World** nella chiamata.</span><span class="sxs-lookup"><span data-stu-id="8dc20-187">The following PHP page results in a TwiML response that says **Hello World** on the call.</span></span>

    <?php    
        header("content-type: text/xml");    
        echo "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n";
    ?>
    <Response>    
        <Say>Hello world.</Say>
    </Response>

<span data-ttu-id="8dc20-188">Come si evince dal codice riportato sopra, la risposta TwiML è semplicemente un documento XML.</span><span class="sxs-lookup"><span data-stu-id="8dc20-188">As you can see from the example above, the TwiML response is simply an XML document.</span></span> <span data-ttu-id="8dc20-189">La libreria Twilio per PHP contiene le classi che consentono di generare automaticamente le istruzioni TwiML.</span><span class="sxs-lookup"><span data-stu-id="8dc20-189">The Twilio library for PHP contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="8dc20-190">Nell'esempio seguente viene creata la stessa risposta descritta sopra, ma usando la classe **Services\_Twilio\_Twiml** nella libreria Twilio per PHP:</span><span class="sxs-lookup"><span data-stu-id="8dc20-190">The example below produces the equivalent response as shown above, but uses the **Services\_Twilio\_Twiml** class in the Twilio library for PHP:</span></span>

    require_once('Services/Twilio.php');

    $response = new Services_Twilio_Twiml();
    $response->say("Hello world.");
    print $response;

<span data-ttu-id="8dc20-191">Per altre informazioni su TwiML, vedere [https://www.twilio.com/docs/api/twiml][twiml_reference].</span><span class="sxs-lookup"><span data-stu-id="8dc20-191">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span></span> 

<span data-ttu-id="8dc20-192">Dopo aver configurato la pagina PHP in modo da fornire risposte TwiML, usare l'URL della pagina PHP come URL trasmesso nel metodo `Services_Twilio->account->calls->create`.</span><span class="sxs-lookup"><span data-stu-id="8dc20-192">Once you have your PHP page set up to provide TwiML responses, use the URL of the PHP page as the URL passed into the  `Services_Twilio->account->calls->create`  method.</span></span> <span data-ttu-id="8dc20-193">Se, ad esempio, si dispone di un'applicazione Web chiamata **MyTwiML** distribuita in un servizio ospitato in Azure e il nome della pagina PHP è **mytwiml.php**, è possibile trasmettere l'URL a **Services_Twilio->account->calls->create**, come mostrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="8dc20-193">For example, if you have a Web application named **MyTwiML** deployed to an Azure hosted service, and the name of the PHP page is **mytwiml.php**, the URL can be passed to  **Services_Twilio->account->calls->create**  as shown in the following example:</span></span>

    require_once 'Services/Twilio.php';

    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";
    $from_number = "NNNNNNNNNNN";
    $to_number = "NNNNNNNNNNN";
    $url = "http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.php";

    // The phone message text.
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

<span data-ttu-id="8dc20-194">Per ulteriori informazioni sull'utilizzo di Twilio in Azure con PHP, vedere [come rendere un Twilio tramite chiamata telefonica in un'applicazione PHP in Azure][howto_phonecall_php].</span><span class="sxs-lookup"><span data-stu-id="8dc20-194">For additional information about using Twilio in Azure with PHP, see [How to Make a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="8dc20-195"><a id="AdditionalServices"></a>Procedura: Utilizzare servizi Twilio aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="8dc20-195"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="8dc20-196">Oltre agli esempi illustrati in questa pagina, Twilio offre API basate su Web che è possibile utilizzare per sfruttare altre funzionalità di Twilio dall'applicazione Azure.</span><span class="sxs-lookup"><span data-stu-id="8dc20-196">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="8dc20-197">Per informazioni dettagliate, vedere la [documentazione sull'API Twilio][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="8dc20-197">For full details, see the [Twilio API documentation][twilio_api_documentation].</span></span>

## <span data-ttu-id="8dc20-198"><a id="NextSteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8dc20-198"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="8dc20-199">Dopo aver appreso le nozioni di base sul servizio Twilio, utilizzare i collegamenti seguenti per ulteriori informazioni:</span><span class="sxs-lookup"><span data-stu-id="8dc20-199">Now that you've learned the basics of the Twilio service, follow these links to learn more:</span></span>

* <span data-ttu-id="8dc20-200">[Twilio Security Guidelines][twilio_security_guidelines] (Linee guida sulla sicurezza di Twilio)</span><span class="sxs-lookup"><span data-stu-id="8dc20-200">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="8dc20-201">[Twilio HowTo's and Example Code][twilio_howtos] (Procedure e codice di esempio di Twilio)</span><span class="sxs-lookup"><span data-stu-id="8dc20-201">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="8dc20-202">[Twilio Quickstart Tutorials][twilio_quickstarts] (Esercitazioni con guide rapide su Twilio)</span><span class="sxs-lookup"><span data-stu-id="8dc20-202">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="8dc20-203">[Twilio on GitHub][twilio_on_github] (Twilio su GitHub)</span><span class="sxs-lookup"><span data-stu-id="8dc20-203">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="8dc20-204">[Talk to Twilio Support][twilio_support] (Contattare il supporto di Twilio)</span><span class="sxs-lookup"><span data-stu-id="8dc20-204">[Talk to Twilio Support][twilio_support]</span></span>

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
