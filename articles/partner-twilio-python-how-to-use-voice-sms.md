---
title: aaaHow tooUse Twilio per vocali e SMS (Python) | Documenti Microsoft
description: Informazioni su come messaggio di toomake una telefonata e inviare un SMS con il servizio API di Twilio hello in Azure. Gli esempi di codice sono scritti in Python.
services: 
documentationcenter: python
author: devinrader
manager: twilio
editor: 
ms.assetid: 561bc75b-4ac4-40ba-bcba-48e901f27cc3
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2015
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: 1f16a107d95c94589b8d61a0971c5b62d639c571
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-python"></a><span data-ttu-id="556d0-104">Come tooUse Twilio per funzionalità voce ed SMS in Python</span><span class="sxs-lookup"><span data-stu-id="556d0-104">How tooUse Twilio for Voice and SMS Capabilities in Python</span></span>
<span data-ttu-id="556d0-105">Questa guida illustra come tooperform attività di programmazione comuni con hello Twilio API del servizio in Azure.</span><span class="sxs-lookup"><span data-stu-id="556d0-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="556d0-106">scenari di Hello trattati includono una telefonata e inviare un messaggio breve servizio SMS (Message).</span><span class="sxs-lookup"><span data-stu-id="556d0-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="556d0-107">Per ulteriori informazioni su Twilio e l'utilizzo di audio e SMS nelle applicazioni, vedere hello [passaggi successivi](#NextSteps) sezione.</span><span class="sxs-lookup"><span data-stu-id="556d0-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="556d0-108"><a id="WhatIs"></a>Informazioni su Twilio</span><span class="sxs-lookup"><span data-stu-id="556d0-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="556d0-109">Twilio è accensione hello futuro delle comunicazioni aziendali, l'abilitazione di vocale tooembed gli sviluppatori, VoIP e nelle applicazioni di messaggistica.</span><span class="sxs-lookup"><span data-stu-id="556d0-109">Twilio is powering hello future of business communications, enabling developers tooembed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="556d0-110">Essi virtualizzare tutta l'infrastruttura necessaria in un ambiente globale, basato su cloud, esporlo tramite API di comunicazione Twilio hello.</span><span class="sxs-lookup"><span data-stu-id="556d0-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through hello Twilio communications API platform.</span></span> <span data-ttu-id="556d0-111">Le applicazioni sono toobuild semplice e scalabile.</span><span class="sxs-lookup"><span data-stu-id="556d0-111">Applications are simple toobuild and scalable.</span></span> <span data-ttu-id="556d0-112">Offre flessibilità, grazie a un modello di prezzi con pagamento al consumo, e l'affidabilità del cloud.</span><span class="sxs-lookup"><span data-stu-id="556d0-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="556d0-113">**Twilio vocale** consente toomake le applicazioni e ricevere chiamate telefoniche.</span><span class="sxs-lookup"><span data-stu-id="556d0-113">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span>
<span data-ttu-id="556d0-114">**SMS Twilio** consente toosend l'applicazione e ricevere messaggi di testo.</span><span class="sxs-lookup"><span data-stu-id="556d0-114">**Twilio SMS** enables your application toosend and receive text messages.</span></span>
<span data-ttu-id="556d0-115">**Twilio Client** consente le chiamate VoIP toomake da qualsiasi telefono, tablet o browser e supporta WebRTC.</span><span class="sxs-lookup"><span data-stu-id="556d0-115">**Twilio Client** allows you toomake VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="556d0-116"><a id="Pricing"></a>Prezzi e offerte speciali di Twilio</span><span class="sxs-lookup"><span data-stu-id="556d0-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="556d0-117">I clienti di Azure ricevono un'[offerta speciale][special_offer]: $ 10 di credito Twilio quando si esegue l'aggiornamento dell'account Twilio.</span><span class="sxs-lookup"><span data-stu-id="556d0-117">Azure customers receive a [special offer][special_offer] $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="556d0-118">Il credito di Twilio può essere applicato tooany Twilio utilizzo ($10 credito equivalente toosending fino a 1.000 messaggi SMS o alla ricezione di too1000 in ingresso minuti vocale, a seconda della posizione di hello della destinazione e numero di messaggio o una chiamata telefonica).</span><span class="sxs-lookup"><span data-stu-id="556d0-118">This Twilio Credit can be applied tooany Twilio usage ($10 credit equivalent toosending as many as 1,000 SMS messages or receiving up too1000 inbound Voice minutes, depending on hello location of your phone number and message or call destination).</span></span> <span data-ttu-id="556d0-119">Riscattare il [credito Twilio][special_offer] e iniziare a usare il servizio.</span><span class="sxs-lookup"><span data-stu-id="556d0-119">Redeem this [Twilio credit][special_offer] and get started.</span></span>

<span data-ttu-id="556d0-120">Twilio è un servizio con pagamento in base al consumo.</span><span class="sxs-lookup"><span data-stu-id="556d0-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="556d0-121">Non prevede spese iniziali ed è possibile chiudere l'account in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="556d0-121">There are no set-up fees and you can close your account at any time.</span></span> <span data-ttu-id="556d0-122">Per altre informazioni, vedere la pagina [Twilio Pricing][twilio_pricing] (Prezzi di Twilio).</span><span class="sxs-lookup"><span data-stu-id="556d0-122">You can find more details at [Twilio Pricing][twilio_pricing].</span></span>

## <span data-ttu-id="556d0-123"><a id="Concepts"></a>Concetti</span><span class="sxs-lookup"><span data-stu-id="556d0-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="556d0-124">API di Twilio Hello è un'API RESTful che fornisce funzionalità SMS e vocale per le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="556d0-124">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="556d0-125">Le librerie client sono disponibili in più lingue. Per un elenco, vedere [Twilio API Libraries][twilio_libraries] (Librerie dell'API Twilio).</span><span class="sxs-lookup"><span data-stu-id="556d0-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="556d0-126">Gli aspetti chiave di hello Twilio API sono verbi Twilio e Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="556d0-126">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="556d0-127"><a id="Verbs"></a>Verbi Twilio</span><span class="sxs-lookup"><span data-stu-id="556d0-127"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="556d0-128">Hello API utilizza Twilio verbi. ad esempio, hello  **&lt;pronuncia&gt;**  verbo indica Twilio tooaudibly inviare un messaggio in una chiamata.</span><span class="sxs-lookup"><span data-stu-id="556d0-128">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="556d0-129">Hello seguito è riportato un elenco dei verbi di Twilio.</span><span class="sxs-lookup"><span data-stu-id="556d0-129">hello following is a list of Twilio verbs.</span></span> <span data-ttu-id="556d0-130">Informazioni sui hello altri verbi tramite [la documentazione del linguaggio di Markup Twilio][twiml].</span><span class="sxs-lookup"><span data-stu-id="556d0-130">Learn about hello other verbs and capabilities via [Twilio Markup Language documentation][twiml].</span></span>

* <span data-ttu-id="556d0-131">**&lt;Connessione&gt;**: connette phone tooanother di hello chiamante.</span><span class="sxs-lookup"><span data-stu-id="556d0-131">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="556d0-132">**&lt;Raccogliere&gt;**: raccoglie cifre immesse sul tastierino telefonico hello.</span><span class="sxs-lookup"><span data-stu-id="556d0-132">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="556d0-133">**&lt;Hangup&gt;**: termina una chiamata.</span><span class="sxs-lookup"><span data-stu-id="556d0-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="556d0-134">**&lt;Pause&gt;**: attende in modo silenzioso per un numero di secondi specificato.</span><span class="sxs-lookup"><span data-stu-id="556d0-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="556d0-135">**&lt;Play&gt;**: riproduce un file audio.</span><span class="sxs-lookup"><span data-stu-id="556d0-135">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="556d0-136">**&lt;Coda&gt;**: aggiungere hello tooa coda dei chiamanti.</span><span class="sxs-lookup"><span data-stu-id="556d0-136">**&lt;Queue&gt;**: Add hello tooa queue of callers.</span></span>
* <span data-ttu-id="556d0-137">**&lt;Record&gt;**: registra vocale hello del chiamante hello e restituisce un URL di un file che contenga la registrazione di hello.</span><span class="sxs-lookup"><span data-stu-id="556d0-137">**&lt;Record&gt;**: Records hello voice of hello caller and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="556d0-138">**&lt;Reindirizzare&gt;**: trasferisce il controllo di una telefonata o SMS toohello TwiML in un URL diverso.</span><span class="sxs-lookup"><span data-stu-id="556d0-138">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="556d0-139">**&lt;Rifiutare&gt;**: rifiuta un fax in ingresso chiamare tooyour Twilio numero senza fatturazione si.</span><span class="sxs-lookup"><span data-stu-id="556d0-139">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you.</span></span>
* <span data-ttu-id="556d0-140">**&lt;Ad esempio&gt;**: converte toospeech di testo che viene effettuata una chiamata.</span><span class="sxs-lookup"><span data-stu-id="556d0-140">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="556d0-141">**&lt;Sms&gt;**: invia un SMS.</span><span class="sxs-lookup"><span data-stu-id="556d0-141">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="556d0-142"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="556d0-142"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="556d0-143">TwiML è un set di istruzioni basato su XML in base a verbi Twilio hello che informano Twilio come tooprocess una telefonata o SMS.</span><span class="sxs-lookup"><span data-stu-id="556d0-143">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="556d0-144">Ad esempio, hello seguente TwiML conversione testo hello **Hello World** toospeech.</span><span class="sxs-lookup"><span data-stu-id="556d0-144">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

<span data-ttu-id="556d0-145">Quando l'applicazione chiama hello API Twilio, uno dei parametri di API hello è URL hello che restituisce una risposta TwiML hello.</span><span class="sxs-lookup"><span data-stu-id="556d0-145">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="556d0-146">A scopo di sviluppo, è possibile utilizzare le risposte TwiML hello tooprovide URL fornito Twilio utilizzate dalle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="556d0-146">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="556d0-147">È anche possibile ospitare le proprie URL tooproduce hello TwiML risposte e un'altra opzione consiste hello toouse `TwiMLResponse` oggetto.</span><span class="sxs-lookup"><span data-stu-id="556d0-147">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello `TwiMLResponse` object.</span></span>

<span data-ttu-id="556d0-148">Per altre informazioni sui verbi Twilio, i relativi attributi e il codice TwiML, vedere [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="556d0-148">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="556d0-149">Per ulteriori informazioni su hello Twilio API, vedere [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="556d0-149">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="556d0-150"><a id="CreateAccount"></a>Creare un account Twilio</span><span class="sxs-lookup"><span data-stu-id="556d0-150"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="556d0-151">Quando si è pronti tooget un account di Twilio, iscriversi al [provare Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="556d0-151">When you are ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="556d0-152">È possibile iniziare con un account gratuito ed eseguire l'aggiornamento in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="556d0-152">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="556d0-153">Quando si effettua l'iscrizione a un account Twilio, si riceveranno il SID account e un token di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="556d0-153">When you sign up for a Twilio account, you receive an account SID and an authentication token.</span></span> <span data-ttu-id="556d0-154">Entrambi saranno necessari toomake Twilio API chiamate.</span><span class="sxs-lookup"><span data-stu-id="556d0-154">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="556d0-155">non autorizzato tooprevent tooyour account di accesso, proteggere il token di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="556d0-155">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="556d0-156">Il SID dell'account e un token di autenticazione sono visibili in hello [Twilio Console][twilio_console]nella hello caselle **SID di ACCOUNT** e **Authentication TOKEN**, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="556d0-156">Your account SID and authentication token are viewable in hello [Twilio Console][twilio_console], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="556d0-157"><a id="create_app"></a>Creare un'applicazione Python</span><span class="sxs-lookup"><span data-stu-id="556d0-157"><a id="create_app"></a>Create a Python Application</span></span>
<span data-ttu-id="556d0-158">Un'applicazione Python che utilizza il servizio di Twilio hello ed è in esecuzione in Azure non è diversa rispetto a qualsiasi altra applicazione Python che utilizza il servizio di Twilio hello.</span><span class="sxs-lookup"><span data-stu-id="556d0-158">A Python application that uses hello Twilio service and is running in Azure is no different than any other Python application that uses hello Twilio service.</span></span> <span data-ttu-id="556d0-159">Mentre i servizi di Twilio basato su REST possono essere chiamati da Python in diversi modi, in questo articolo è incentrato sul come toouse Twilio servizi con [libreria Twilio per Python da GitHub][twilio_python].</span><span class="sxs-lookup"><span data-stu-id="556d0-159">While Twilio services are REST-based and can be called from Python in several ways, this article will focus on how toouse Twilio services with [Twilio library for Python from GitHub][twilio_python].</span></span> <span data-ttu-id="556d0-160">Per ulteriori informazioni sull'utilizzo della libreria di hello Twilio per Python, vedere [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].</span><span class="sxs-lookup"><span data-stu-id="556d0-160">For more information about using hello Twilio library for Python, see [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].</span></span>

<span data-ttu-id="556d0-161">Innanzitutto, [configurazione una nuova macchina virtuale Linux di Azure] [azure_vm_setup] tooact come host per la nuova applicazione web di Python.</span><span class="sxs-lookup"><span data-stu-id="556d0-161">First, [set-up a new Azure Linux VM][azure_vm_setup] tooact as a host for your new Python web application.</span></span> <span data-ttu-id="556d0-162">Una volta hello macchina virtuale è in esecuzione, sarà necessario tooexpose dell'applicazione su una porta pubblica come descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="556d0-162">Once hello Virtual Machine is running, you will need tooexpose your application on a public port as described below.</span></span>

### <a name="add-an-incoming-rule"></a><span data-ttu-id="556d0-163">Aggiungere una regola in ingresso</span><span class="sxs-lookup"><span data-stu-id="556d0-163">Add An Incoming Rule</span></span>
  1. <span data-ttu-id="556d0-164">Passare toohello [Network Security Group] [azure_nsg] pagina.</span><span class="sxs-lookup"><span data-stu-id="556d0-164">Go toohello [Network Security Group][azure_nsg] page.</span></span>
  2. <span data-ttu-id="556d0-165">Selezionare hello Network Security Group corrispondente con la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="556d0-165">Select hello Network Security Group that corresponds with your Virtual Machine.</span></span>
  3. <span data-ttu-id="556d0-166">Aggiungere una **Regola in uscita** per la **porta 80**.</span><span class="sxs-lookup"><span data-stu-id="556d0-166">Add and **Outgoing Rule** for **port 80**.</span></span> <span data-ttu-id="556d0-167">Impossibile verificare tooallow in ingresso da qualsiasi indirizzo.</span><span class="sxs-lookup"><span data-stu-id="556d0-167">Be sure tooallow incoming from any address.</span></span>

### <a name="set-hello-dns-name-label"></a><span data-ttu-id="556d0-168">Impostare l'etichetta del nome DNS hello</span><span class="sxs-lookup"><span data-stu-id="556d0-168">Set hello DNS Name Label</span></span>
  1. <span data-ttu-id="556d0-169">Passare toohello [hello indirizzi IP pubblici] [azure_ips] pagina.</span><span class="sxs-lookup"><span data-stu-id="556d0-169">Go toohello [hello Public IP Adresses][azure_ips] page.</span></span>
  2. <span data-ttu-id="556d0-170">Selezionare hello IP pubblico che correspends con la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="556d0-170">Select hello Public IP that correspends with your Virtual Machine.</span></span>
  3. <span data-ttu-id="556d0-171">Set hello **etichetta del nome DNS** in hello **configurazione** sezione.</span><span class="sxs-lookup"><span data-stu-id="556d0-171">Set hello **DNS Name Label** in hello **Configuration** section.</span></span> <span data-ttu-id="556d0-172">Nel caso di hello di questo esempio avrà un aspetto simile al seguente *l'etichetta di dominio*. centralus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="556d0-172">In hello case of this example it will look something like this *your-domain-label*.centralus.cloudapp.azure.com</span></span>

<span data-ttu-id="556d0-173">Quando si è in grado di tooconnect tramite SSH toohello macchina virtuale è possibile installare hello Framework Web di propria scelta (hello due più noti in fase di Python [pallone](http://flask.pocoo.org/) e [Django](https://www.djangoproject.com)).</span><span class="sxs-lookup"><span data-stu-id="556d0-173">Once you are able tooconnect through SSH toohello Virtual Machine you can install hello Web Framework of your choice (hello two most well known in Python being [Flask](http://flask.pocoo.org/) and [Django](https://www.djangoproject.com)).</span></span> <span data-ttu-id="556d0-174">È possibile installare una di esse semplicemente eseguendo hello `pip install` comando.</span><span class="sxs-lookup"><span data-stu-id="556d0-174">You can install either of them just by running hello `pip install` command.</span></span>

<span data-ttu-id="556d0-175">Tenere presente che è stato configurato il traffico tooallow hello macchine virtuali solo sulla porta 80.</span><span class="sxs-lookup"><span data-stu-id="556d0-175">Keep in mind that we configured hello Virtual Machine tooallow traffic only on port 80.</span></span> <span data-ttu-id="556d0-176">Verificare pertanto che tooconfigure hello applicazione toouse questa porta.</span><span class="sxs-lookup"><span data-stu-id="556d0-176">So make sure tooconfigure hello application toouse this port.</span></span>

## <span data-ttu-id="556d0-177"><a id="configure_app"></a>Configurare le librerie di Twilio tooUse dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="556d0-177"><a id="configure_app"></a>Configure Your Application tooUse Twilio Libraries</span></span>
<span data-ttu-id="556d0-178">È possibile configurare la libreria di Twilio applicazione hello toouse per Python in due modi:</span><span class="sxs-lookup"><span data-stu-id="556d0-178">You can configure your application toouse hello Twilio library for Python in two ways:</span></span>

* <span data-ttu-id="556d0-179">Installare libreria Twilio hello per Python come pacchetto Pip.</span><span class="sxs-lookup"><span data-stu-id="556d0-179">Install hello Twilio library for Python as a Pip package.</span></span> <span data-ttu-id="556d0-180">Può essere installato con hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="556d0-180">It can be installed with hello following commands:</span></span>
   
        $ pip install twilio

    <span data-ttu-id="556d0-181">-OPPURE-</span><span class="sxs-lookup"><span data-stu-id="556d0-181">-OR-</span></span>

* <span data-ttu-id="556d0-182">Scaricare una libreria di Twilio hello per Python da GitHub ([https://github.com/twilio/twilio-python][twilio_python]) e installarlo simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="556d0-182">Download hello Twilio library for Python from GitHub ([https://github.com/twilio/twilio-python][twilio_python]) and install it like this:</span></span>

        $ python setup.py install

<span data-ttu-id="556d0-183">Dopo aver installato libreria Twilio hello per Python, è quindi possibile `import` in file Python:</span><span class="sxs-lookup"><span data-stu-id="556d0-183">Once you have installed hello Twilio library for Python, you can then `import` it in your Python files:</span></span>

        import twilio

<span data-ttu-id="556d0-184">Per altre informazioni, vedere [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].</span><span class="sxs-lookup"><span data-stu-id="556d0-184">For more information, see [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].</span></span>

## <span data-ttu-id="556d0-185"><a id="howto_make_call"></a>Procedura: Effettuare una chiamata in uscita</span><span class="sxs-lookup"><span data-stu-id="556d0-185"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="556d0-186">Hello seguente viene illustrato come chiamare toomake in uscita.</span><span class="sxs-lookup"><span data-stu-id="556d0-186">hello following shows how toomake an outgoing call.</span></span> <span data-ttu-id="556d0-187">Questo codice usa anche un hello tooreturn sito Twilio fornita risposta Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="556d0-187">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="556d0-188">Sostituire i valori per hello **from_number** e **to_number** i numeri di telefono e assicurarsi di aver verificato hello **from_number** numero di telefono per l'account di Twilio prima di eseguire il codice hello.</span><span class="sxs-lookup"><span data-stu-id="556d0-188">Substitute your values for hello **from_number** and **to_number** phone numbers, and ensure that you've verified hello **from_number** phone number for your Twilio account before running hello code.</span></span>

    from urllib.parse import urlencode

    # Import hello Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    # hello number of hello phone initiating hello hello call.
    # This should either be a Twilio number or a number that you've verified
    from_number = "NNNNNNNNNNN"

    # hello number of hello phone receiving call.
    to_number = "NNNNNNNNNNN"

    # Use hello Twilio-provided site for hello TwiML response.
    url = "http://twimlets.com/message?"

    # hello phone message text.
    message = "Hello world."

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make hello call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url + urlencode({'Message': message}))
    print(call.sid)

<span data-ttu-id="556d0-189">Come accennato, questo codice Usa un hello tooreturn sito fornito Twilio TwiML risposta.</span><span class="sxs-lookup"><span data-stu-id="556d0-189">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="556d0-190">È possibile utilizzare la propria hello tooprovide sito TwiML risposta. Per ulteriori informazioni, vedere [come tooProvide TwiML risposte da un sito Web di](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="556d0-190">You could instead use your own site tooprovide hello TwiML response; for more information, see [How tooProvide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="556d0-191"><a id="howto_send_sms"></a>Procedura: Inviare un messaggio SMS</span><span class="sxs-lookup"><span data-stu-id="556d0-191"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="556d0-192">Hello seguente viene illustrato come un messaggio SMS utilizzando toosend hello `TwilioRestClient` classe.</span><span class="sxs-lookup"><span data-stu-id="556d0-192">hello following shows how toosend an SMS message using hello `TwilioRestClient` class.</span></span> <span data-ttu-id="556d0-193">Hello **from_number** numero fornito dal Twilio per versione di valutazione account toosend messaggi SMS.</span><span class="sxs-lookup"><span data-stu-id="556d0-193">hello **from_number** number is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="556d0-194">Hello **to_number** numero deve essere verificato per l'account di Twilio prima di eseguire codice hello.</span><span class="sxs-lookup"><span data-stu-id="556d0-194">hello **to_number** number must be verified for your Twilio account before running hello code.</span></span>

    # Import hello Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    from_number = "NNNNNNNNNNN"  # With trial account, texts can only be sent from your Twilio number.
    to_number = "NNNNNNNNNNN"
    message = "Hello world."

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Send hello SMS message.
    message = client.messages.create(to=to_number,
                                     from_=from_number,
                                     body=message)

## <span data-ttu-id="556d0-195"><a id="howto_provide_twiml_responses"></a>Procedura: Fornire risposte TwiML dal proprio sito Web</span><span class="sxs-lookup"><span data-stu-id="556d0-195"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="556d0-196">Quando l'applicazione avvia toohello una chiamata API di Twilio, Twilio invierà l'URL tooa richiesta è previsto tooreturn una risposta TwiML.</span><span class="sxs-lookup"><span data-stu-id="556d0-196">When your application initiates a call toohello Twilio API, Twilio will send your request tooa URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="556d0-197">esempio di Hello viene utilizzata l'URL fornito Twilio hello [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="556d0-197">hello example above uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="556d0-198">Poiché TwiML è stato progettato per essere usato da Twilio, è possibile visualizzarlo nel browser.</span><span class="sxs-lookup"><span data-stu-id="556d0-198">(While TwiML is designed for use by Twilio, you can view it in your browser.</span></span> <span data-ttu-id="556d0-199">Ad esempio, fare clic su [http://twimlets.com/message] [ twimlet_message_url] toosee vuota `<Response>` elemento; ad esempio, fare clic su [http://twimlets.com/message? Messaggio % 5B0 %5D = Hello % 20World] [ twimlet_message_url_hello_world] toosee un `<Response>` elemento che contiene un `<Say>` elemento.)</span><span class="sxs-lookup"><span data-stu-id="556d0-199">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] toosee a `<Response>` element that contains a `<Say>` element.)</span></span>

<span data-ttu-id="556d0-200">Anziché basarsi sul URL fornito Twilio hello, è possibile creare un sito che restituisce le risposte HTTP.</span><span class="sxs-lookup"><span data-stu-id="556d0-200">Instead of relying on hello Twilio-provided URL, you can create your own site that returns HTTP responses.</span></span> <span data-ttu-id="556d0-201">È possibile creare il sito di hello in qualsiasi linguaggio che restituisce le risposte XML. In questo argomento si presuppone che si userà hello toocreate Python TwiML.</span><span class="sxs-lookup"><span data-stu-id="556d0-201">You can create hello site in any language that returns XML responses; this topic assumes you will be using Python toocreate hello TwiML.</span></span>

<span data-ttu-id="556d0-202">Hello negli esempi seguenti genera una risposta TwiML che afferma **Hello World** chiamata hello.</span><span class="sxs-lookup"><span data-stu-id="556d0-202">hello following examples will output a TwiML response that says **Hello World** on hello call.</span></span>

<span data-ttu-id="556d0-203">Con Flask:</span><span class="sxs-lookup"><span data-stu-id="556d0-203">With Flask:</span></span>

    from flask import Response
    @app.route("/")
    def hello():
        xml = '<Response><Say>Hello world.</Say></Response>'
        return Response(xml, mimetype='text/xml')

<span data-ttu-id="556d0-204">Con Django:</span><span class="sxs-lookup"><span data-stu-id="556d0-204">With Django:</span></span>

    from django.http import HttpResponse
    def hello(request):
        xml = '<Response><Say>Hello world.</Say></Response>'
        return HttpResponse(xml, content_type='text/xml')

<span data-ttu-id="556d0-205">Come si può notare dal precedente esempio di hello, hello TwiML risposta è semplicemente un documento XML.</span><span class="sxs-lookup"><span data-stu-id="556d0-205">As you can see from hello example above, hello TwiML response is simply an XML document.</span></span> <span data-ttu-id="556d0-206">libreria di Twilio Hello per Python contiene classi che generano TwiML automaticamente.</span><span class="sxs-lookup"><span data-stu-id="556d0-206">hello Twilio library for Python contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="556d0-207">Hello esempio riportato di seguito genera risposta equivalente hello, come illustrato in precedenza, ma utilizza hello `twiml` modulo nella libreria di Twilio hello per Python:</span><span class="sxs-lookup"><span data-stu-id="556d0-207">hello example below produces hello equivalent response as shown above, but uses hello `twiml` module in hello Twilio library for Python:</span></span>

    from twilio import twiml

    response = twiml.Response()
    response.say("Hello world.")
    print(str(response))

<span data-ttu-id="556d0-208">Per altre informazioni su TwiML, vedere [https://www.twilio.com/docs/api/twiml][twiml_reference].</span><span class="sxs-lookup"><span data-stu-id="556d0-208">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span></span>

<span data-ttu-id="556d0-209">Dopo aver creato l'applicazione Python imposta risposte TwiML tooprovide, utilizzare l'URL di hello di un'applicazione hello come hello URL passato hello `client.calls.create` metodo.</span><span class="sxs-lookup"><span data-stu-id="556d0-209">Once you have your Python application set up tooprovide TwiML responses, use hello URL of hello application as hello URL passed into hello `client.calls.create`  method.</span></span> <span data-ttu-id="556d0-210">Ad esempio, se si dispone di un'applicazione Web denominata **MyTwiML** tooan distribuito Azure servizio ospitato, è possibile usare il relativo url come webhook, come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="556d0-210">For example, if you have a Web application named **MyTwiML** deployed tooan Azure hosted service, you can use its url as webhook as shown in hello following example:</span></span>

    from twilio.rest import TwilioRestClient

    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"
    from_number = "NNNNNNNNNNN"
    to_number = "NNNNNNNNNNN"
    url = "http://your-domain-label.centralus.cloudapp.azure.com/MyTwiML/"

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make hello call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url)
    print(call.sid)

## <span data-ttu-id="556d0-211"><a id="AdditionalServices"></a>Procedura: Utilizzare servizi Twilio aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="556d0-211"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="556d0-212">Inoltre toohello esempi riportati di seguito, che twilio offre API basata sul web che è possibile utilizzare altre funzionalità di Twilio tooleverage dall'applicazione Azure.</span><span class="sxs-lookup"><span data-stu-id="556d0-212">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="556d0-213">Per informazioni dettagliate, vedere hello [documentazione dell'API di Twilio][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="556d0-213">For full details, see hello [Twilio API documentation][twilio_api].</span></span>

## <span data-ttu-id="556d0-214"><a id="NextSteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="556d0-214"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="556d0-215">Ora che si è appreso nozioni di base di hello di hello servizio Twilio, seguire questi toolearn collegamenti più:</span><span class="sxs-lookup"><span data-stu-id="556d0-215">Now that you have learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="556d0-216">[Twilio Security Guidelines][twilio_security_guidelines] (Linee guida sulla sicurezza di Twilio)</span><span class="sxs-lookup"><span data-stu-id="556d0-216">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="556d0-217">[Twilio HowTo Guides and Example Code][twilio_howtos] (Procedure e codice di esempio su Twilio)</span><span class="sxs-lookup"><span data-stu-id="556d0-217">[Twilio HowTo Guides and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="556d0-218">[Twilio Quickstart Tutorials][twilio_quickstarts] (Esercitazioni con guide rapide su Twilio)</span><span class="sxs-lookup"><span data-stu-id="556d0-218">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span>
* <span data-ttu-id="556d0-219">[Twilio on GitHub][twilio_on_github] (Twilio su GitHub)</span><span class="sxs-lookup"><span data-stu-id="556d0-219">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="556d0-220">[Comunicare tooTwilio supporto][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="556d0-220">[Talk tooTwilio Support][twilio_support]</span></span>

[special_offer]: http://ahoy.twilio.com/azure
[twilio_python]: https://github.com/twilio/twilio-python
[twilio_lib_docs]: http://readthedocs.org/docs/twilio-python/en/latest/index.html
[twilio_github_readme]: https://github.com/twilio/twilio-python/blob/master/README.md

[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World
[twiml_reference]: https://www.twilio.com/docs/api/twiml
[twilio_pricing]: http://www.twilio.com/pricing

[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_console]:  https://www.twilio.com/console
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
