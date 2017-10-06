---
title: aaaHow tooUse Twilio per vocali e SMS (Ruby) | Documenti Microsoft
description: Informazioni su come messaggio di toomake una telefonata e inviare un SMS con il servizio API di Twilio hello in Azure. Gli esempi di codice sono scritti in Ruby.
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
ms.openlocfilehash: aca5ccb4663ff03c9c1f39c848469415f06dfb45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-ruby"></a><span data-ttu-id="17de2-104">Come tooUse Twilio per funzionalità voce ed SMS in Ruby</span><span class="sxs-lookup"><span data-stu-id="17de2-104">How tooUse Twilio for Voice and SMS Capabilities in Ruby</span></span>
<span data-ttu-id="17de2-105">Questa guida illustra come tooperform attività di programmazione comuni con hello Twilio API del servizio in Azure.</span><span class="sxs-lookup"><span data-stu-id="17de2-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="17de2-106">scenari di Hello trattati includono una telefonata e inviare un messaggio breve servizio SMS (Message).</span><span class="sxs-lookup"><span data-stu-id="17de2-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="17de2-107">Per ulteriori informazioni su Twilio e l'utilizzo di audio e SMS nelle applicazioni, vedere hello [passaggi successivi](#NextSteps) sezione.</span><span class="sxs-lookup"><span data-stu-id="17de2-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="17de2-108"><a id="WhatIs"></a>Informazioni su Twilio</span><span class="sxs-lookup"><span data-stu-id="17de2-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="17de2-109">Twilio è un'API web-servizio di telefonia che consente di utilizzare i linguaggi web esistenti e vocale toobuild competenze e le applicazioni di SMS.</span><span class="sxs-lookup"><span data-stu-id="17de2-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills toobuild voice and SMS applications.</span></span> <span data-ttu-id="17de2-110">Twilio è un servizio di terze parti. Non si tratta di una funzionalità di Azure, né di un prodotto Microsoft.</span><span class="sxs-lookup"><span data-stu-id="17de2-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="17de2-111">**Twilio vocale** consente toomake le applicazioni e ricevere chiamate telefoniche.</span><span class="sxs-lookup"><span data-stu-id="17de2-111">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="17de2-112">**SMS Twilio** consente toomake le applicazioni e la ricezione di messaggi SMS.</span><span class="sxs-lookup"><span data-stu-id="17de2-112">**Twilio SMS** allows your applications toomake and receive SMS messages.</span></span> <span data-ttu-id="17de2-113">**Twilio Client** consente alle applicazioni comunicazioni vocali tooenable tramite connessioni Internet esistenti, incluse le connessioni per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="17de2-113">**Twilio Client** allows your applications tooenable voice communication using existing Internet connections, including mobile connections.</span></span>

## <span data-ttu-id="17de2-114"><a id="Pricing"></a>Prezzi e offerte speciali di Twilio</span><span class="sxs-lookup"><span data-stu-id="17de2-114"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="17de2-115">Per altre informazioni, vedere la pagina [Twilio Pricing][twilio_pricing] (Prezzi di Twilio).</span><span class="sxs-lookup"><span data-stu-id="17de2-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="17de2-116">Per i clienti di Azure è disponibile un'[offerta speciale][special_offer]: un credito gratuito per 1000 SMS o 1000 minuti di connessioni in entrata.</span><span class="sxs-lookup"><span data-stu-id="17de2-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="17de2-117">toosign per questa offerta o ottenere ulteriori informazioni, visitare [http://ahoy.twilio.com/azure][special_offer].</span><span class="sxs-lookup"><span data-stu-id="17de2-117">toosign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>  

## <span data-ttu-id="17de2-118"><a id="Concepts"></a>Concetti</span><span class="sxs-lookup"><span data-stu-id="17de2-118"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="17de2-119">API di Twilio Hello è un'API RESTful che fornisce funzionalità SMS e vocale per le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="17de2-119">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="17de2-120">Le librerie client sono disponibili in più lingue. Per un elenco, vedere [Twilio API Libraries][twilio_libraries] (Librerie dell'API Twilio).</span><span class="sxs-lookup"><span data-stu-id="17de2-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

### <span data-ttu-id="17de2-121"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="17de2-121"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="17de2-122">TwiML è un set di istruzioni basato su XML che informano Twilio come tooprocess una telefonata o SMS.</span><span class="sxs-lookup"><span data-stu-id="17de2-122">TwiML is a set of XML-based instructions that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="17de2-123">Ad esempio, hello seguente TwiML conversione testo hello **Hello World** toospeech.</span><span class="sxs-lookup"><span data-stu-id="17de2-123">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="17de2-124">Tutti i documenti TwiML dispongono di un elemento radice `<Response>`,</span><span class="sxs-lookup"><span data-stu-id="17de2-124">All TwiML documents have `<Response>` as their root element.</span></span> <span data-ttu-id="17de2-125">Da qui, utilizzare il comportamento di hello toodefine Twilio verbi dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="17de2-125">From there, you use Twilio Verbs toodefine hello behavior of your application.</span></span>

### <span data-ttu-id="17de2-126"><a id="Verbs"></a>Verbi TwiML</span><span class="sxs-lookup"><span data-stu-id="17de2-126"><a id="Verbs"></a>TwiML Verbs</span></span>
<span data-ttu-id="17de2-127">I verbi di Twilio sono tag XML in cui indicare Twilio troppo**si**.</span><span class="sxs-lookup"><span data-stu-id="17de2-127">Twilio Verbs are XML tags that tell Twilio what too**do**.</span></span> <span data-ttu-id="17de2-128">Ad esempio, hello  **&lt;pronuncia&gt;**  verbo indica Twilio tooaudibly inviare un messaggio in una chiamata.</span><span class="sxs-lookup"><span data-stu-id="17de2-128">For example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span> 

<span data-ttu-id="17de2-129">Hello seguito è riportato un elenco dei verbi di Twilio.</span><span class="sxs-lookup"><span data-stu-id="17de2-129">hello following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="17de2-130">**&lt;Connessione&gt;**: connette phone tooanother di hello chiamante.</span><span class="sxs-lookup"><span data-stu-id="17de2-130">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="17de2-131">**&lt;Raccogliere&gt;**: raccoglie cifre immesse sul tastierino telefonico hello.</span><span class="sxs-lookup"><span data-stu-id="17de2-131">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="17de2-132">**&lt;Hangup&gt;**: termina una chiamata.</span><span class="sxs-lookup"><span data-stu-id="17de2-132">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="17de2-133">**&lt;Play&gt;**: riproduce un file audio.</span><span class="sxs-lookup"><span data-stu-id="17de2-133">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="17de2-134">**&lt;Pause&gt;**: attende in modo silenzioso per un numero di secondi specificato.</span><span class="sxs-lookup"><span data-stu-id="17de2-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="17de2-135">**&lt;Record&gt;**: registra la voce del chiamante hello e restituisce un URL di un file che contenga la registrazione di hello.</span><span class="sxs-lookup"><span data-stu-id="17de2-135">**&lt;Record&gt;**: Records hello caller's voice and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="17de2-136">**&lt;Reindirizzare&gt;**: trasferisce il controllo di una telefonata o SMS toohello TwiML in un URL diverso.</span><span class="sxs-lookup"><span data-stu-id="17de2-136">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="17de2-137">**&lt;Rifiutare&gt;**: rifiuta un fax in ingresso chiamare tooyour Twilio numero senza fatturazione si</span><span class="sxs-lookup"><span data-stu-id="17de2-137">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you</span></span>
* <span data-ttu-id="17de2-138">**&lt;Ad esempio&gt;**: converte toospeech di testo che viene effettuata una chiamata.</span><span class="sxs-lookup"><span data-stu-id="17de2-138">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="17de2-139">**&lt;Sms&gt;**: invia un SMS.</span><span class="sxs-lookup"><span data-stu-id="17de2-139">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

<span data-ttu-id="17de2-140">Per altre informazioni sui verbi Twilio, i relativi attributi e il codice TwiML, vedere [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="17de2-140">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="17de2-141">Per ulteriori informazioni su hello Twilio API, vedere [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="17de2-141">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="17de2-142"><a id="CreateAccount"></a>Creare un account Twilio</span><span class="sxs-lookup"><span data-stu-id="17de2-142"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="17de2-143">Quando sarai pronto tooget un account di Twilio, iscriversi al [provare Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="17de2-143">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="17de2-144">È possibile iniziare con un account gratuito ed eseguire l'aggiornamento in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="17de2-144">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="17de2-145">Quando si effettua l'iscrizione a Twilio si riceve un numero di telefono gratuito per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="17de2-145">When you sign up for a Twilio account, you'll get a free phone number for your application.</span></span> <span data-ttu-id="17de2-146">Si ricevono inoltre il SID dell'account e un token di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="17de2-146">You'll also receive an account SID and an auth token.</span></span> <span data-ttu-id="17de2-147">Entrambi saranno necessari toomake Twilio API chiamate.</span><span class="sxs-lookup"><span data-stu-id="17de2-147">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="17de2-148">non autorizzato tooprevent tooyour account di accesso, proteggere il token di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="17de2-148">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="17de2-149">Il SID dell'account e un token di autorizzazione possono essere visualizzati in hello [pagina account di Twilio][twilio_account]nella hello campi con etichettati **SID di ACCOUNT** e **Authentication TOKEN** , rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="17de2-149">Your account SID and auth token are viewable at hello [Twilio account page][twilio_account], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

### <span data-ttu-id="17de2-150"><a id="VerifyPhoneNumbers"></a>Verificare i numeri di telefono</span><span class="sxs-lookup"><span data-stu-id="17de2-150"><a id="VerifyPhoneNumbers"></a>Verify Phone Numbers</span></span>
<span data-ttu-id="17de2-151">Numero di toohello aggiunta che viene fornita da Twilio, è inoltre possibile verificare i numeri di controllo (ad esempio il telefono cellulare o home numero di telefono) per l'utilizzo nelle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="17de2-151">In addition toohello number you are given by Twilio, you can also verify numbers that you control (i.e. your cell phone or home phone number) for use in your applications.</span></span> 

<span data-ttu-id="17de2-152">Per informazioni su come tooverify un numero di telefono, vedere [gestire numeri][verify_phone].</span><span class="sxs-lookup"><span data-stu-id="17de2-152">For information on how tooverify a phone number, see [Manage Numbers][verify_phone].</span></span>

## <span data-ttu-id="17de2-153"><a id="create_app"></a>Creare un'applicazione Ruby</span><span class="sxs-lookup"><span data-stu-id="17de2-153"><a id="create_app"></a>Create a Ruby Application</span></span>
<span data-ttu-id="17de2-154">Un'applicazione Ruby che utilizza il servizio di Twilio hello ed è in esecuzione in Azure non è diversa rispetto a qualsiasi altra applicazione che utilizza il servizio di Twilio hello Ruby.</span><span class="sxs-lookup"><span data-stu-id="17de2-154">A Ruby application that uses hello Twilio service and is running in Azure is no different than any other Ruby application that uses hello Twilio service.</span></span> <span data-ttu-id="17de2-155">Mentre Twilio servizi RESTful possono essere chiamati da Ruby in diversi modi, in questo articolo è incentrato sul come toouse Twilio servizi con [libreria helper Twilio per Ruby][twilio_ruby].</span><span class="sxs-lookup"><span data-stu-id="17de2-155">While Twilio services are RESTful and can be called from Ruby in several ways, this article will focus on how toouse Twilio services with [Twilio helper library for Ruby][twilio_ruby].</span></span>

<span data-ttu-id="17de2-156">Prima di tutto, [configurazione una nuova macchina virtuale Linux di Azure] [ azure_vm_setup] tooact come host per la nuova applicazione web Ruby.</span><span class="sxs-lookup"><span data-stu-id="17de2-156">First, [set-up a new Azure Linux VM][azure_vm_setup] tooact as a host for your new Ruby web application.</span></span> <span data-ttu-id="17de2-157">Ignorare i passaggi di hello che implicano hello creazione di un'app, guide appena hello di configurazione macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="17de2-157">Ignore hello steps involving hello creation of a Rails app, just set-up hello VM.</span></span> <span data-ttu-id="17de2-158">Assicurarsi di creare un endpoint con porta esterna 80 e porta interna 5000.</span><span class="sxs-lookup"><span data-stu-id="17de2-158">Make sure you create an Endpoint with an external port of 80 and an internal port of 5000.</span></span>

<span data-ttu-id="17de2-159">Negli esempi di hello riportato di seguito, che verrà usato [Sinatra][sinatra], un framework web molto semplice per Ruby.</span><span class="sxs-lookup"><span data-stu-id="17de2-159">In hello examples below, we will be using [Sinatra][sinatra], a very simple web framework for Ruby.</span></span> <span data-ttu-id="17de2-160">Ma è possibile utilizzare libreria helper di Twilio hello per Ruby con qualsiasi altro framework web, come Ruby on Guide.</span><span class="sxs-lookup"><span data-stu-id="17de2-160">But you can certainly use hello Twilio helper library for Ruby with any other web framework, including Ruby on Rails.</span></span>

<span data-ttu-id="17de2-161">Connettersi tramite SSH alla nuova macchina virtuale e creare una directory per la nuova app.</span><span class="sxs-lookup"><span data-stu-id="17de2-161">SSH into your new VM and create a directory for your new app.</span></span> <span data-ttu-id="17de2-162">All'interno di tale directory, creare un file denominato Gemfile e copia hello seguente codice al suo interno:</span><span class="sxs-lookup"><span data-stu-id="17de2-162">Inside that directory, create a file called Gemfile and copy hello following code into it:</span></span>

    source 'https://rubygems.org'
    gem 'sinatra'
    gem 'thin'

<span data-ttu-id="17de2-163">Nella riga di comando hello eseguire `bundle install`.</span><span class="sxs-lookup"><span data-stu-id="17de2-163">On hello command line run `bundle install`.</span></span> <span data-ttu-id="17de2-164">Dipendenze di hello precedente verrà installato.</span><span class="sxs-lookup"><span data-stu-id="17de2-164">This will install hello dependencies above.</span></span> <span data-ttu-id="17de2-165">Quindi, creare un file denominato `web.rb`.</span><span class="sxs-lookup"><span data-stu-id="17de2-165">Next create a file called `web.rb`.</span></span> <span data-ttu-id="17de2-166">Si tratterà in cui si trova il codice hello per le app web.</span><span class="sxs-lookup"><span data-stu-id="17de2-166">This will be where hello code for your web app lives.</span></span> <span data-ttu-id="17de2-167">Incollare hello seguente codice al suo interno:</span><span class="sxs-lookup"><span data-stu-id="17de2-167">Paste hello following code into it:</span></span>

    require 'sinatra'

    get '/' do
        "Hello Monkey!"
    end

<span data-ttu-id="17de2-168">A questo punto dovrebbe essere comando hello hello in grado di eseguire `ruby web.rb -p 5000`.</span><span class="sxs-lookup"><span data-stu-id="17de2-168">At this point you should be able hello run hello command `ruby web.rb -p 5000`.</span></span> <span data-ttu-id="17de2-169">Verrà avviato un server Web di dimensioni ridotte sulla porta 5000.</span><span class="sxs-lookup"><span data-stu-id="17de2-169">This will spin-up a small web server on port 5000.</span></span> <span data-ttu-id="17de2-170">Dovrebbe essere in grado di toobrowse toothis app nel browser, visitare l'URL di hello configurazione per la macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="17de2-170">You should be able toobrowse toothis app in your browser by visiting hello URL you set-up for your Azure VM.</span></span> <span data-ttu-id="17de2-171">Una volta che è possibile raggiungere l'app web nel browser hello, si è pronti toostart creazione di un'app di Twilio.</span><span class="sxs-lookup"><span data-stu-id="17de2-171">Once you can reach your web app in hello browser, you're ready toostart building a Twilio app.</span></span>

## <span data-ttu-id="17de2-172"><a id="configure_app"></a>Configurare l'applicazione tooUse Twilio</span><span class="sxs-lookup"><span data-stu-id="17de2-172"><a id="configure_app"></a>Configure Your Application tooUse Twilio</span></span>
<span data-ttu-id="17de2-173">È possibile configurare la libreria di Twilio web app toouse hello aggiornando il `Gemfile` tooinclude questa riga:</span><span class="sxs-lookup"><span data-stu-id="17de2-173">You can configure your web app toouse hello Twilio library by updating your `Gemfile` tooinclude this line:</span></span>

    gem 'twilio-ruby'

<span data-ttu-id="17de2-174">Nella riga di comando hello, eseguire `bundle install`.</span><span class="sxs-lookup"><span data-stu-id="17de2-174">On hello command line, run `bundle install`.</span></span> <span data-ttu-id="17de2-175">Aprire quindi `web.rb` e tra la riga nella parte superiore di hello:</span><span class="sxs-lookup"><span data-stu-id="17de2-175">Now open `web.rb` and including this line at hello top:</span></span>

    require 'twilio-ruby'

<span data-ttu-id="17de2-176">Si è ora tutti i set di libreria di supporto toouse hello Twilio per Ruby in app web.</span><span class="sxs-lookup"><span data-stu-id="17de2-176">You're now all set toouse hello Twilio helper library for Ruby in your web app.</span></span>

## <span data-ttu-id="17de2-177"><a id="howto_make_call"></a>Procedura: Effettuare una chiamata in uscita</span><span class="sxs-lookup"><span data-stu-id="17de2-177"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="17de2-178">Hello seguente viene illustrato come chiamare toomake in uscita.</span><span class="sxs-lookup"><span data-stu-id="17de2-178">hello following shows how toomake an outgoing call.</span></span> <span data-ttu-id="17de2-179">Concetti principali includono l'utilizzo di libreria di supporto di hello Twilio per Ruby toomake chiamate API REST e TwiML di rendering.</span><span class="sxs-lookup"><span data-stu-id="17de2-179">Key concepts include using hello Twilio helper library for Ruby toomake REST API calls and rendering TwiML.</span></span> <span data-ttu-id="17de2-180">Sostituire i valori per hello **da** e **a** i numeri di telefono e assicurarsi che si verifichino hello **da** numero di telefono per il codice di hello Twilio account toorunning precedente.</span><span class="sxs-lookup"><span data-stu-id="17de2-180">Substitute your values for hello **From** and **To** phone numbers, and ensure that you verify hello **From** phone number for your Twilio account prior toorunning hello code.</span></span>

<span data-ttu-id="17de2-181">Aggiungere la seguente funzione troppo`web.md`:</span><span class="sxs-lookup"><span data-stu-id="17de2-181">Add this function too`web.md`:</span></span>

    # Set your account ID and authentication token.
    sid = "your_twilio_account_sid";
    token = "your_twilio_authentication_token";

    # hello number of hello phone initiating hello hello call.
    # This should either be a Twilio number or a number that you've verified
    from = "NNNNNNNNNNN";

    # hello number of hello phone receiving call.
    too= "NNNNNNNNNNN";

    # Use hello Twilio-provided site for hello TwiML response.
    url = "http://yourdomain.cloudapp.net/voice_url";

    get '/make_call' do
      # Create hello call client.
      client = Twilio::REST::Client.new(sid, token);

      # Make hello call
      client.account.calls.create(to: to, from: from, url: url)
    end

    post '/voice_url' do
      "<Response>
         <Say>Hello Monkey!</Say>
       </Response>"
    end

<span data-ttu-id="17de2-182">Se remoto aprire `http://yourdomain.cloudapp.net/make_call` in un browser, che attiverà hello chiamata toohello Twilio API toomake hello telefonata.</span><span class="sxs-lookup"><span data-stu-id="17de2-182">If you open-up `http://yourdomain.cloudapp.net/make_call` in a browser, that will trigger hello call toohello Twilio API toomake hello phone call.</span></span> <span data-ttu-id="17de2-183">Hello i primi due parametri in `client.account.calls.create` sono di chiara interpretazione: hello numero hello chiamata `from` ed è chiamata hello numero hello `to`.</span><span class="sxs-lookup"><span data-stu-id="17de2-183">hello first two parameters in `client.account.calls.create` are fairly self-explanatory: hello number hello call is `from` and hello number hello call is `to`.</span></span> 

<span data-ttu-id="17de2-184">terzo parametro Hello (`url`) è l'URL di hello che Twilio istruzioni tooget su quali toodo le richieste una volta chiamata hello è connesso.</span><span class="sxs-lookup"><span data-stu-id="17de2-184">hello third parameter (`url`) is hello URL that Twilio requests tooget instructions on what toodo once hello call is connected.</span></span> <span data-ttu-id="17de2-185">In questo caso è senza un URL (`http://yourdomain.cloudapp.net`) che restituisce un documento TwiML semplice e Usa hello `<Say>` toodo verbo alcune sintesi vocale e ad esempio "Hello Monkey" toohello destinatario hello chiamare.</span><span class="sxs-lookup"><span data-stu-id="17de2-185">In this case we set-up a URL (`http://yourdomain.cloudapp.net`) that returns a simple TwiML document and uses hello `<Say>` verb toodo some text-to-speech and say "Hello Monkey" toohello person recieving hello call.</span></span>

## <span data-ttu-id="17de2-186"><a id="howto_recieve_sms"></a>Procedura: Ricevere un messaggio SMS</span><span class="sxs-lookup"><span data-stu-id="17de2-186"><a id="howto_recieve_sms"></a>How to: Recieve an SMS message</span></span>
<span data-ttu-id="17de2-187">Nell'esempio precedente hello è stato avviato un **in uscita** telefonata.</span><span class="sxs-lookup"><span data-stu-id="17de2-187">In hello previous example we initiated an **outgoing** phone call.</span></span> <span data-ttu-id="17de2-188">Questa volta, consente di usare il numero di telefono hello Twilio ha restituito durante l'iscrizione tooprocess un **in ingresso** messaggio SMS.</span><span class="sxs-lookup"><span data-stu-id="17de2-188">This time, let's use hello phone number that Twilio gave us during sign-up tooprocess an **incoming** SMS message.</span></span>

<span data-ttu-id="17de2-189">In primo luogo, accesso tooyour [dashboard Twilio][twilio_account].</span><span class="sxs-lookup"><span data-stu-id="17de2-189">First, log-in tooyour [Twilio dashboard][twilio_account].</span></span> <span data-ttu-id="17de2-190">Fare clic su "Numeri" nella barra di spostamento superiore di hello e quindi fare clic su hello numero Twilio che sono state fornite.</span><span class="sxs-lookup"><span data-stu-id="17de2-190">Click on "Numbers" in hello top nav and then click on hello Twilio number you were provided.</span></span> <span data-ttu-id="17de2-191">Verranno visualizzati due URL che è possibile configurare,</span><span class="sxs-lookup"><span data-stu-id="17de2-191">You'll see two URLs that you can configure.</span></span> <span data-ttu-id="17de2-192">uno per le richieste vocali e uno per le richieste SMS.</span><span class="sxs-lookup"><span data-stu-id="17de2-192">A Voice Request URL and an SMS Request URL.</span></span> <span data-ttu-id="17de2-193">Si tratta di URL hello effettuate chiamate Twilio ogni volta che una chiamata telefonica o un SMS inviato tooyour numero.</span><span class="sxs-lookup"><span data-stu-id="17de2-193">These are hello URLs that Twilio calls whenever a phone call is made or an SMS is sent tooyour number.</span></span> <span data-ttu-id="17de2-194">Hello URL sono noti anche come "web hook".</span><span class="sxs-lookup"><span data-stu-id="17de2-194">hello URLs are also known as "web hooks".</span></span>

<span data-ttu-id="17de2-195">Desideriamo tooprocess messaggi in arrivo di SMS, questo punto aggiornare hello URL troppo`http://yourdomain.cloudapp.net/sms_url`.</span><span class="sxs-lookup"><span data-stu-id="17de2-195">We would like tooprocess incoming SMS messages, so let's update hello URL too`http://yourdomain.cloudapp.net/sms_url`.</span></span> <span data-ttu-id="17de2-196">Procedere facendo clic su Salva modifiche nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="17de2-196">Go ahead and click Save Changes at hello bottom of hello page.</span></span> <span data-ttu-id="17de2-197">Tornare `web.rb` toohandle l'applicazione si programma in questo:</span><span class="sxs-lookup"><span data-stu-id="17de2-197">Now, back in `web.rb` let's program our application toohandle this:</span></span>

    post '/sms_url' do
      "<Response>
         <Message>Hey, thanks for hello ping! Twilio and Azure rock!</Message>
       </Response>"
    end

<span data-ttu-id="17de2-198">Dopo aver apportato modifiche hello, assicurarsi che toore-inizio l'app web.</span><span class="sxs-lookup"><span data-stu-id="17de2-198">After making hello change, make sure toore-start your web app.</span></span> <span data-ttu-id="17de2-199">A questo punto, estrarre il telefono e inviare un numero di Twilio di tooyour SMS.</span><span class="sxs-lookup"><span data-stu-id="17de2-199">Now, take out your phone and send an SMS tooyour Twilio number.</span></span> <span data-ttu-id="17de2-200">È necessario ottenere immediatamente una risposta SMS che afferma "Hey, grazie per il ping di hello!</span><span class="sxs-lookup"><span data-stu-id="17de2-200">You should promptly get an SMS response that says "Hey, thanks for hello ping!</span></span> <span data-ttu-id="17de2-201">Twilio and Azure rock!".</span><span class="sxs-lookup"><span data-stu-id="17de2-201">Twilio and Azure rock!".</span></span>

## <span data-ttu-id="17de2-202"><a id="additional_services"></a>Procedura: Utilizzare servizi Twilio aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="17de2-202"><a id="additional_services"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="17de2-203">Inoltre toohello esempi riportati di seguito, che twilio offre API basata sul web che è possibile utilizzare altre funzionalità di Twilio tooleverage dall'applicazione Azure.</span><span class="sxs-lookup"><span data-stu-id="17de2-203">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="17de2-204">Per informazioni dettagliate, vedere hello [documentazione dell'API di Twilio][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="17de2-204">For full details, see hello [Twilio API documentation][twilio_api_documentation].</span></span>

### <span data-ttu-id="17de2-205"><a id="NextSteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="17de2-205"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="17de2-206">Dopo aver appreso nozioni di base di hello di hello Twilio servizio, seguire questi toolearn collegamenti più:</span><span class="sxs-lookup"><span data-stu-id="17de2-206">Now that you've learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="17de2-207">[Twilio Security Guidelines][twilio_security_guidelines] (Linee guida sulla sicurezza di Twilio)</span><span class="sxs-lookup"><span data-stu-id="17de2-207">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="17de2-208">[Twilio HowTos and Example Code (Procedure e codice di esempio di Twilio)][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="17de2-208">[Twilio HowTos and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="17de2-209">[Twilio Quickstart Tutorials][twilio_quickstarts] (Esercitazioni con guide rapide su Twilio)</span><span class="sxs-lookup"><span data-stu-id="17de2-209">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="17de2-210">[Twilio on GitHub][twilio_on_github] (Twilio su GitHub)</span><span class="sxs-lookup"><span data-stu-id="17de2-210">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="17de2-211">[Comunicare tooTwilio supporto][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="17de2-211">[Talk tooTwilio Support][twilio_support]</span></span>

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
