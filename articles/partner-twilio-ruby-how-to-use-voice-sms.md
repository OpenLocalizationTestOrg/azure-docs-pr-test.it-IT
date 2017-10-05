---
title: "Come usare Twilio per le funzionalità voce e SMS (Ruby) | Microsoft Docs"
description: Informazioni su come effettuare una chiamata telefonica e inviare un SMS con il servizio API Twilio API in Azure. Gli esempi di codice sono scritti in Ruby.
services: 
documentationcenter: ruby
author: devinrader
manager: twilio
editor: 
ms.assetid: 60e512f6-fa47-47c0-aedc-f19bb72a1158
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 11/25/2014
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: 69e50e7fe0e1f302e96c309878b8dea6869dff4a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-in-ruby"></a><span data-ttu-id="e9c9d-104">Come usare Twilio per le funzionalità voce ed SMS in Ruby</span><span class="sxs-lookup"><span data-stu-id="e9c9d-104">How to Use Twilio for Voice and SMS Capabilities in Ruby</span></span>
<span data-ttu-id="e9c9d-105">In questa guida viene illustrato come eseguire attività di programmazione comuni con il servizio API Twilio in Azure.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="e9c9d-106">Gli scenari presentati includono la composizione di una chiamata telefonica e l'invio di un messaggio SMS (Short Message Service).</span><span class="sxs-lookup"><span data-stu-id="e9c9d-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="e9c9d-107">Per altre informazioni su Twilio e sull'utilizzo delle funzionalità voce ed SMS nelle applicazioni, vedere la sezione [Passaggi successivi](#NextSteps) .</span><span class="sxs-lookup"><span data-stu-id="e9c9d-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="e9c9d-108"><a id="WhatIs"></a>Informazioni su Twilio</span><span class="sxs-lookup"><span data-stu-id="e9c9d-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="e9c9d-109">Twilio è un'API per servizi Web di telefonia che consente di usare le competenze e i linguaggi Web esistenti per sviluppare applicazioni SMS e vocali.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills to build voice and SMS applications.</span></span> <span data-ttu-id="e9c9d-110">Twilio è un servizio di terze parti. Non si tratta di una funzionalità di Azure, né di un prodotto Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="e9c9d-111">**Twilio Voice** consente alle applicazioni di effettuare e ricevere chiamate telefoniche.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-111">**Twilio Voice** allows your applications to make and receive phone calls.</span></span> <span data-ttu-id="e9c9d-112">**Twilio SMS** consente alle applicazioni di inviare e ricevere SMS.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-112">**Twilio SMS** allows your applications to make and receive SMS messages.</span></span> <span data-ttu-id="e9c9d-113">**Twilio Client** consente alle applicazioni di abilitare le comunicazioni vocali utilizzando le connessioni Internet esistenti, comprese le connessioni mobili.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-113">**Twilio Client** allows your applications to enable voice communication using existing Internet connections, including mobile connections.</span></span>

## <span data-ttu-id="e9c9d-114"><a id="Pricing"></a>Prezzi e offerte speciali di Twilio</span><span class="sxs-lookup"><span data-stu-id="e9c9d-114"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="e9c9d-115">Per altre informazioni, vedere la pagina [Twilio Pricing][twilio_pricing] (Prezzi di Twilio).</span><span class="sxs-lookup"><span data-stu-id="e9c9d-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="e9c9d-116">Per i clienti di Azure è disponibile un'[offerta speciale][special_offer]: un credito gratuito per 1000 SMS o 1000 minuti di connessioni in entrata.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="e9c9d-117">Per avvalersi dell'offerta o per altre informazioni, visitare il sito Web all'indirizzo [http://ahoy.twilio.com/azure][special_offer].</span><span class="sxs-lookup"><span data-stu-id="e9c9d-117">To sign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>  

## <span data-ttu-id="e9c9d-118"><a id="Concepts"></a>Concetti</span><span class="sxs-lookup"><span data-stu-id="e9c9d-118"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="e9c9d-119">L'API Twilio è un'API RESTful che fornisce funzionalità voce ed SMS per le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-119">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="e9c9d-120">Le librerie client sono disponibili in più lingue. Per un elenco, vedere [Twilio API Libraries][twilio_libraries] (Librerie dell'API Twilio).</span><span class="sxs-lookup"><span data-stu-id="e9c9d-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

### <span data-ttu-id="e9c9d-121"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="e9c9d-121"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="e9c9d-122">TwiML è un set di istruzioni basate su XML che indicano a Twilio come elaborare una chiamata o un SMS.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-122">TwiML is a set of XML-based instructions that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="e9c9d-123">Ad esempio, il codice TwiML seguente effettua la sintesi vocale del testo **Hello World** .</span><span class="sxs-lookup"><span data-stu-id="e9c9d-123">As an example, the following TwiML would convert the text **Hello World** to speech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="e9c9d-124">Tutti i documenti TwiML dispongono di un elemento radice `<Response>`,</span><span class="sxs-lookup"><span data-stu-id="e9c9d-124">All TwiML documents have `<Response>` as their root element.</span></span> <span data-ttu-id="e9c9d-125">da cui è possibile utilizzare i verbi Twilio per definire il comportamento dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-125">From there, you use Twilio Verbs to define the behavior of your application.</span></span>

### <span data-ttu-id="e9c9d-126"><a id="Verbs"></a>Verbi TwiML</span><span class="sxs-lookup"><span data-stu-id="e9c9d-126"><a id="Verbs"></a>TwiML Verbs</span></span>
<span data-ttu-id="e9c9d-127">I verbi Twilio sono tag XML che indicano a Twilio le **azioni da eseguire**.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-127">Twilio Verbs are XML tags that tell Twilio what to **do**.</span></span> <span data-ttu-id="e9c9d-128">Il verbo **&lt;Say&gt;**, ad esempio, indica a Twilio di recapitare un messaggio acustico in una chiamata.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-128">For example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span> 

<span data-ttu-id="e9c9d-129">Di seguito è riportato un elenco dei verbi Twilio.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-129">The following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="e9c9d-130">**&lt;Dial&gt;**: connette il chiamante a un altro telefono.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-130">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="e9c9d-131">**&lt;Gather&gt;**: raccoglie i numeri digitati sulla tastiera del telefono.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-131">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="e9c9d-132">**&lt;Hangup&gt;**: termina una chiamata.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-132">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="e9c9d-133">**&lt;Play&gt;**: riproduce un file audio.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-133">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="e9c9d-134">**&lt;Pause&gt;**: attende in modo silenzioso per un numero di secondi specificato.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="e9c9d-135">**&lt;Record&gt;**: registra la voce del chiamante e restituisce l'URL del file contenente la registrazione.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-135">**&lt;Record&gt;**: Records the caller's voice and returns a URL of a file that contains the recording.</span></span>
* <span data-ttu-id="e9c9d-136">**&lt;Redirect&gt;**: trasferisce il controllo di una chiamata o di un SMS al codice TwiML presso un URL diverso.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-136">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="e9c9d-137">**&lt;Reject&gt;**: rifiuta una chiamata in arrivo al numero Twilio senza alcun addebito.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-137">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you</span></span>
* <span data-ttu-id="e9c9d-138">**&lt;Say&gt;**: effettua la sintesi vocale del testo durante una chiamata.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-138">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="e9c9d-139">**&lt;Sms&gt;**: invia un SMS.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-139">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

<span data-ttu-id="e9c9d-140">Per altre informazioni sui verbi Twilio, i relativi attributi e il codice TwiML, vedere [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="e9c9d-140">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="e9c9d-141">Per altre informazioni sull'API Twilio, vedere [Twilio API][twilio_api] (API Twilio).</span><span class="sxs-lookup"><span data-stu-id="e9c9d-141">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="e9c9d-142"><a id="CreateAccount"></a>Creare un account Twilio</span><span class="sxs-lookup"><span data-stu-id="e9c9d-142"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="e9c9d-143">Se si desidera creare un account Twilio, iscriversi nella pagina [Try Twilio][try_twilio] (Provare Twilio).</span><span class="sxs-lookup"><span data-stu-id="e9c9d-143">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="e9c9d-144">È possibile iniziare con un account gratuito ed eseguire l'aggiornamento in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-144">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="e9c9d-145">Quando si effettua l'iscrizione a Twilio si riceve un numero di telefono gratuito per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-145">When you sign up for a Twilio account, you'll get a free phone number for your application.</span></span> <span data-ttu-id="e9c9d-146">Si ricevono inoltre il SID dell'account e un token di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-146">You'll also receive an account SID and an auth token.</span></span> <span data-ttu-id="e9c9d-147">Entrambe queste informazioni sono necessarie per effettuare chiamate all'API Twilio.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-147">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="e9c9d-148">Per prevenire accessi autorizzati all'account, conservare il token di autenticazione in un luogo sicuro.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-148">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="e9c9d-149">Il SID account e il token di autorizzazione sono visualizzabili nella [pagina dell'account Twilio][twilio_account], rispettivamente nei campi **ACCOUNT SID** (SID ACCOUNT) e **AUTH TOKEN** (TOKEN AUTORIZZAZIONE).</span><span class="sxs-lookup"><span data-stu-id="e9c9d-149">Your account SID and auth token are viewable at the [Twilio account page][twilio_account], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

### <span data-ttu-id="e9c9d-150"><a id="VerifyPhoneNumbers"></a>Verificare i numeri di telefono</span><span class="sxs-lookup"><span data-stu-id="e9c9d-150"><a id="VerifyPhoneNumbers"></a>Verify Phone Numbers</span></span>
<span data-ttu-id="e9c9d-151">Oltre al numero assegnato da Twilio, è possibile verificare altri numeri di cui si abbia il controllo, ad esempio quello del cellulare o quello dell'abitazione, per usarli nelle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-151">In addition to the number you are given by Twilio, you can also verify numbers that you control (i.e. your cell phone or home phone number) for use in your applications.</span></span> 

<span data-ttu-id="e9c9d-152">Per informazioni su come verificare un numero di telefono, vedere [Manage Numbers][verify_phone] (Gestire i numeri).</span><span class="sxs-lookup"><span data-stu-id="e9c9d-152">For information on how to verify a phone number, see [Manage Numbers][verify_phone].</span></span>

## <span data-ttu-id="e9c9d-153"><a id="create_app"></a>Creare un'applicazione Ruby</span><span class="sxs-lookup"><span data-stu-id="e9c9d-153"><a id="create_app"></a>Create a Ruby Application</span></span>
<span data-ttu-id="e9c9d-154">Un'applicazione Ruby che usa il servizio Twilio e viene eseguita in Azure non è diversa da qualsiasi altra applicazione Ruby che usa il servizio Twilio.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-154">A Ruby application that uses the Twilio service and is running in Azure is no different than any other Ruby application that uses the Twilio service.</span></span> <span data-ttu-id="e9c9d-155">Anche se i servizi Twilio sono di tipo RESTful e possono essere chiamati da Ruby in molti modi, in questo articolo verrà illustrato solo come usare i servizi Twilio con la [libreria helper Twilio per Ruby][twilio_ruby].</span><span class="sxs-lookup"><span data-stu-id="e9c9d-155">While Twilio services are RESTful and can be called from Ruby in several ways, this article will focus on how to use Twilio services with [Twilio helper library for Ruby][twilio_ruby].</span></span>

<span data-ttu-id="e9c9d-156">Prima di tutto, [configurare una nuova VM Linux in Azure][azure_vm_setup] che funga da host per la nuova applicazione Web Ruby.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-156">First, [set-up a new Azure Linux VM][azure_vm_setup] to act as a host for your new Ruby web application.</span></span> <span data-ttu-id="e9c9d-157">Ignorare i passaggi relativi alla creazione di un'app Rails e configurare semplicemente la VM.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-157">Ignore the steps involving the creation of a Rails app, just set-up the VM.</span></span> <span data-ttu-id="e9c9d-158">Assicurarsi di creare un endpoint con porta esterna 80 e porta interna 5000.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-158">Make sure you create an Endpoint with an external port of 80 and an internal port of 5000.</span></span>

<span data-ttu-id="e9c9d-159">Negli esempi che seguono verrà usato [Sinatra][sinatra], un framework Web molto semplice per Ruby.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-159">In the examples below, we will be using [Sinatra][sinatra], a very simple web framework for Ruby.</span></span> <span data-ttu-id="e9c9d-160">È comunque possibile utilizzare la libreria helper Twilio per Ruby con qualsiasi altro web framework, compreso Ruby on Rails.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-160">But you can certainly use the Twilio helper library for Ruby with any other web framework, including Ruby on Rails.</span></span>

<span data-ttu-id="e9c9d-161">Connettersi tramite SSH alla nuova macchina virtuale e creare una directory per la nuova app.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-161">SSH into your new VM and create a directory for your new app.</span></span> <span data-ttu-id="e9c9d-162">All'interno di tale directory creare un file denominato Gemfile e copiare al suo interno il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="e9c9d-162">Inside that directory, create a file called Gemfile and copy the following code into it:</span></span>

    source 'https://rubygems.org'
    gem 'sinatra'
    gem 'thin'

<span data-ttu-id="e9c9d-163">Nella riga di comando eseguire `bundle install`.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-163">On the command line run `bundle install`.</span></span> <span data-ttu-id="e9c9d-164">Le dipendenze precedenti verranno installate.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-164">This will install the dependencies above.</span></span> <span data-ttu-id="e9c9d-165">Quindi, creare un file denominato `web.rb`.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-165">Next create a file called `web.rb`.</span></span> <span data-ttu-id="e9c9d-166">in cui risiederà il codice per l'app Web.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-166">This will be where the code for your web app lives.</span></span> <span data-ttu-id="e9c9d-167">Copiare nel file il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="e9c9d-167">Paste the following code into it:</span></span>

    require 'sinatra'

    get '/' do
        "Hello Monkey!"
    end

<span data-ttu-id="e9c9d-168">A questo punto dovrebbe essere possibile eseguire il comando `ruby web.rb -p 5000`.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-168">At this point you should be able the run the command `ruby web.rb -p 5000`.</span></span> <span data-ttu-id="e9c9d-169">Verrà avviato un server Web di dimensioni ridotte sulla porta 5000.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-169">This will spin-up a small web server on port 5000.</span></span> <span data-ttu-id="e9c9d-170">Dovrebbe essere possibile passare all'app nel browser visitando l'URL configurato per la macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-170">You should be able to browse to this app in your browser by visiting the URL you set-up for your Azure VM.</span></span> <span data-ttu-id="e9c9d-171">Non appena è possibile raggiungere l'app Web nel browser, è possibile iniziare a creare un'app Twilio.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-171">Once you can reach your web app in the browser, you're ready to start building a Twilio app.</span></span>

## <span data-ttu-id="e9c9d-172"><a id="configure_app"></a>Configurare l'applicazione per utilizzare Twilio</span><span class="sxs-lookup"><span data-stu-id="e9c9d-172"><a id="configure_app"></a>Configure Your Application to Use Twilio</span></span>
<span data-ttu-id="e9c9d-173">È possibile configurare l'app Web per utilizzare la libreria Twilio aggiornando il `Gemfile` includendo la seguente riga:</span><span class="sxs-lookup"><span data-stu-id="e9c9d-173">You can configure your web app to use the Twilio library by updating your `Gemfile` to include this line:</span></span>

    gem 'twilio-ruby'

<span data-ttu-id="e9c9d-174">Nella riga di comando, eseguire `bundle install`.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-174">On the command line, run `bundle install`.</span></span> <span data-ttu-id="e9c9d-175">A questo punto, aprire `web.rb` e includere la riga nella parte superiore:</span><span class="sxs-lookup"><span data-stu-id="e9c9d-175">Now open `web.rb` and including this line at the top:</span></span>

    require 'twilio-ruby'

<span data-ttu-id="e9c9d-176">È ora possibile usare la libreria helper Twilio per Ruby nell'app Web.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-176">You're now all set to use the Twilio helper library for Ruby in your web app.</span></span>

## <span data-ttu-id="e9c9d-177"><a id="howto_make_call"></a>Procedura: Effettuare una chiamata in uscita</span><span class="sxs-lookup"><span data-stu-id="e9c9d-177"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="e9c9d-178">Di seguito è illustrato come effettuare una chiamata in uscita.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-178">The following shows how to make an outgoing call.</span></span> <span data-ttu-id="e9c9d-179">I principali concetti illustrati includono l'utilizzo della libreria helper Twilio per Ruby per effettuare chiamate API REST e per il rendering di TwiML.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-179">Key concepts include using the Twilio helper library for Ruby to make REST API calls and rendering TwiML.</span></span> <span data-ttu-id="e9c9d-180">Sostituire i valori per i numeri di telefono **From** e **To** e assicurarsi di verificare il numero di telefono in **From** per l'account Twilio prima di eseguire il codice.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-180">Substitute your values for the **From** and **To** phone numbers, and ensure that you verify the **From** phone number for your Twilio account prior to running the code.</span></span>

<span data-ttu-id="e9c9d-181">Aggiungere a `web.md`la funzione seguente:</span><span class="sxs-lookup"><span data-stu-id="e9c9d-181">Add this function to `web.md`:</span></span>

    # Set your account ID and authentication token.
    sid = "your_twilio_account_sid";
    token = "your_twilio_authentication_token";

    # The number of the phone initiating the the call.
    # This should either be a Twilio number or a number that you've verified
    from = "NNNNNNNNNNN";

    # The number of the phone receiving call.
    to = "NNNNNNNNNNN";

    # Use the Twilio-provided site for the TwiML response.
    url = "http://yourdomain.cloudapp.net/voice_url";

    get '/make_call' do
      # Create the call client.
      client = Twilio::REST::Client.new(sid, token);

      # Make the call
      client.account.calls.create(to: to, from: from, url: url)
    end

    post '/voice_url' do
      "<Response>
         <Say>Hello Monkey!</Say>
       </Response>"
    end

<span data-ttu-id="e9c9d-182">Aprendo `http://yourdomain.cloudapp.net/make_call` in un browser verrà attivata la chiamata all'API Twilio per l'esecuzione della chiamata telefonica.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-182">If you open-up `http://yourdomain.cloudapp.net/make_call` in a browser, that will trigger the call to the Twilio API to make the phone call.</span></span> <span data-ttu-id="e9c9d-183">I primi due parametri in `client.account.calls.create` sono facilmente comprensibili: il numero da cui proviene la chiamata è `from` e il numero a cui è diretta è `to`.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-183">The first two parameters in `client.account.calls.create` are fairly self-explanatory: the number the call is `from` and the number the call is `to`.</span></span> 

<span data-ttu-id="e9c9d-184">Il terzo parametro (`url`) è l'URL utilizzato da Twilio per richiedere istruzioni sulle operazioni da eseguire dopo la connessione della chiamata.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-184">The third parameter (`url`) is the URL that Twilio requests to get instructions on what to do once the call is connected.</span></span> <span data-ttu-id="e9c9d-185">In questo caso verrà configurato un URL (`http://yourdomain.cloudapp.net`) che restituisce un documento TwiML molto semplice e utilizza il verbo `<Say>` per effettuare la sintesi vocale del testo e pronunciare la frase "Hello Monkey" per il destinatario della chiamata.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-185">In this case we set-up a URL (`http://yourdomain.cloudapp.net`) that returns a simple TwiML document and uses the `<Say>` verb to do some text-to-speech and say "Hello Monkey" to the person recieving the call.</span></span>

## <span data-ttu-id="e9c9d-186"><a id="howto_recieve_sms"></a>Procedura: Ricevere un messaggio SMS</span><span class="sxs-lookup"><span data-stu-id="e9c9d-186"><a id="howto_recieve_sms"></a>How to: Recieve an SMS message</span></span>
<span data-ttu-id="e9c9d-187">Nell'esempio precedente è stata avviata una chiamata telefonica **in uscita** .</span><span class="sxs-lookup"><span data-stu-id="e9c9d-187">In the previous example we initiated an **outgoing** phone call.</span></span> <span data-ttu-id="e9c9d-188">Questa volta verrà utilizzato il numero ricevuto da Twilio dopo l'iscrizione per elaborare un SMS **in arrivo** .</span><span class="sxs-lookup"><span data-stu-id="e9c9d-188">This time, let's use the phone number that Twilio gave us during sign-up to process an **incoming** SMS message.</span></span>

<span data-ttu-id="e9c9d-189">Prima di tutto, accedere al [dashboard Twilio][twilio_account].</span><span class="sxs-lookup"><span data-stu-id="e9c9d-189">First, log-in to your [Twilio dashboard][twilio_account].</span></span> <span data-ttu-id="e9c9d-190">Fare clic su "Numbers" sulla barra di spostamento superiore e quindi fare clic sul numero ricevuto da Twilio.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-190">Click on "Numbers" in the top nav and then click on the Twilio number you were provided.</span></span> <span data-ttu-id="e9c9d-191">Verranno visualizzati due URL che è possibile configurare,</span><span class="sxs-lookup"><span data-stu-id="e9c9d-191">You'll see two URLs that you can configure.</span></span> <span data-ttu-id="e9c9d-192">uno per le richieste vocali e uno per le richieste SMS.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-192">A Voice Request URL and an SMS Request URL.</span></span> <span data-ttu-id="e9c9d-193">Si tratta degli URL chiamati da Twilio ogni volta che viene inviato un SMS o viene effettuata una chiamata telefonica verso il proprio numero.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-193">These are the URLs that Twilio calls whenever a phone call is made or an SMS is sent to your number.</span></span> <span data-ttu-id="e9c9d-194">Gli URL sono noti anche come "hook Web".</span><span class="sxs-lookup"><span data-stu-id="e9c9d-194">The URLs are also known as "web hooks".</span></span>

<span data-ttu-id="e9c9d-195">Per elaborare gli SMS in arrivo è necessario aggiornare l'URL in `http://yourdomain.cloudapp.net/sms_url`.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-195">We would like to process incoming SMS messages, so let's update the URL to `http://yourdomain.cloudapp.net/sms_url`.</span></span> <span data-ttu-id="e9c9d-196">Effettuare la modifica e fare clic su Save Changes nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-196">Go ahead and click Save Changes at the bottom of the page.</span></span> <span data-ttu-id="e9c9d-197">Tornare a `web.rb` e programmare l'applicazione per la gestione dell'operazione seguente:</span><span class="sxs-lookup"><span data-stu-id="e9c9d-197">Now, back in `web.rb` let's program our application to handle this:</span></span>

    post '/sms_url' do
      "<Response>
         <Message>Hey, thanks for the ping! Twilio and Azure rock!</Message>
       </Response>"
    end

<span data-ttu-id="e9c9d-198">Dopo aver apportato la modifica, riavviare l'app Web.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-198">After making the change, make sure to re-start your web app.</span></span> <span data-ttu-id="e9c9d-199">Prendere il telefono e inviare un SMS al proprio numero Twilio.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-199">Now, take out your phone and send an SMS to your Twilio number.</span></span> <span data-ttu-id="e9c9d-200">Si dovrebbe ricevere un SMS di risposta con il testo "Hey, thanks for the ping!</span><span class="sxs-lookup"><span data-stu-id="e9c9d-200">You should promptly get an SMS response that says "Hey, thanks for the ping!</span></span> <span data-ttu-id="e9c9d-201">Twilio and Azure rock!".</span><span class="sxs-lookup"><span data-stu-id="e9c9d-201">Twilio and Azure rock!".</span></span>

## <span data-ttu-id="e9c9d-202"><a id="additional_services"></a>Procedura: Utilizzare servizi Twilio aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="e9c9d-202"><a id="additional_services"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="e9c9d-203">Oltre agli esempi illustrati in questa pagina, Twilio offre API basate su Web che è possibile utilizzare per sfruttare altre funzionalità di Twilio dall'applicazione Azure.</span><span class="sxs-lookup"><span data-stu-id="e9c9d-203">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="e9c9d-204">Per informazioni dettagliate, vedere la [documentazione sull'API Twilio][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="e9c9d-204">For full details, see the [Twilio API documentation][twilio_api_documentation].</span></span>

### <span data-ttu-id="e9c9d-205"><a id="NextSteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e9c9d-205"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="e9c9d-206">Dopo aver appreso le nozioni di base sul servizio Twilio, utilizzare i collegamenti seguenti per ulteriori informazioni:</span><span class="sxs-lookup"><span data-stu-id="e9c9d-206">Now that you've learned the basics of the Twilio service, follow these links to learn more:</span></span>

* <span data-ttu-id="e9c9d-207">[Twilio Security Guidelines][twilio_security_guidelines] (Linee guida sulla sicurezza di Twilio)</span><span class="sxs-lookup"><span data-stu-id="e9c9d-207">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="e9c9d-208">[Twilio HowTos and Example Code (Procedure e codice di esempio di Twilio)][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="e9c9d-208">[Twilio HowTos and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="e9c9d-209">[Twilio Quickstart Tutorials][twilio_quickstarts] (Esercitazioni con guide rapide su Twilio)</span><span class="sxs-lookup"><span data-stu-id="e9c9d-209">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="e9c9d-210">[Twilio on GitHub][twilio_on_github] (Twilio su GitHub)</span><span class="sxs-lookup"><span data-stu-id="e9c9d-210">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="e9c9d-211">[Talk to Twilio Support][twilio_support] (Contattare il supporto di Twilio)</span><span class="sxs-lookup"><span data-stu-id="e9c9d-211">[Talk to Twilio Support][twilio_support]</span></span>

[twilio_ruby]: https://www.twilio.com/docs/ruby/install





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
[sinatra]: http://www.sinatrarb.com/
[azure_vm_setup]: http://www.windowsazure.com/develop/ruby/tutorials/web-app-with-linux-vm/
