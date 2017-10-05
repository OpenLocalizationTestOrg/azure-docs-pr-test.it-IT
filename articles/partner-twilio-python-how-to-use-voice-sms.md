---
title: "Come usare Twilio per le funzionalità voce ed SMS (Python) | Microsoft Docs"
description: Informazioni su come effettuare una chiamata telefonica e inviare un SMS con il servizio API Twilio API in Azure. Gli esempi di codice sono scritti in Python.
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
ms.openlocfilehash: f4a02bb7a7c46e7a0e3c75b870c522eae8294339
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-in-python"></a><span data-ttu-id="c5841-104">Come usare Twilio per le funzionalità voce ed SMS in Python</span><span class="sxs-lookup"><span data-stu-id="c5841-104">How to Use Twilio for Voice and SMS Capabilities in Python</span></span>
<span data-ttu-id="c5841-105">In questa guida viene illustrato come eseguire attività di programmazione comuni con il servizio API Twilio in Azure.</span><span class="sxs-lookup"><span data-stu-id="c5841-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="c5841-106">Gli scenari presentati includono la composizione di una chiamata telefonica e l'invio di un messaggio SMS (Short Message Service).</span><span class="sxs-lookup"><span data-stu-id="c5841-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="c5841-107">Per altre informazioni su Twilio e sull'utilizzo delle funzionalità voce ed SMS nelle applicazioni, vedere la sezione [Passaggi successivi](#NextSteps) .</span><span class="sxs-lookup"><span data-stu-id="c5841-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="c5841-108"><a id="WhatIs"></a>Informazioni su Twilio</span><span class="sxs-lookup"><span data-stu-id="c5841-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="c5841-109">Twilio è una tecnologia all'avanguardia per le comunicazioni aziendali che consente agli sviluppatori di incorporare funzionalità voce, VoIP e di messaggistica nelle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="c5841-109">Twilio is powering the future of business communications, enabling developers to embed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="c5841-110">Consente di virtualizzare tutta l'infrastruttura necessaria in un ambiente globale basato su cloud, esponendolo attraverso la piattaforma API per le comunicazioni Twilio.</span><span class="sxs-lookup"><span data-stu-id="c5841-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through the Twilio communications API platform.</span></span> <span data-ttu-id="c5841-111">Le applicazioni sono scalabili e facili da compilare.</span><span class="sxs-lookup"><span data-stu-id="c5841-111">Applications are simple to build and scalable.</span></span> <span data-ttu-id="c5841-112">Offre flessibilità, grazie a un modello di prezzi con pagamento al consumo, e l'affidabilità del cloud.</span><span class="sxs-lookup"><span data-stu-id="c5841-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="c5841-113">**Twilio Voice** consente alle applicazioni di effettuare e ricevere chiamate telefoniche.</span><span class="sxs-lookup"><span data-stu-id="c5841-113">**Twilio Voice** allows your applications to make and receive phone calls.</span></span>
<span data-ttu-id="c5841-114">**Twilio SMS** consente alle applicazioni di inviare e ricevere messaggi di testo.</span><span class="sxs-lookup"><span data-stu-id="c5841-114">**Twilio SMS** enables your application to send and receive text messages.</span></span>
<span data-ttu-id="c5841-115">**Twilio Client** consente di effettuare chiamate VoIP da qualsiasi telefono, tablet o browser e supporta WebRTC.</span><span class="sxs-lookup"><span data-stu-id="c5841-115">**Twilio Client** allows you to make VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="c5841-116"><a id="Pricing"></a>Prezzi e offerte speciali di Twilio</span><span class="sxs-lookup"><span data-stu-id="c5841-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="c5841-117">I clienti di Azure ricevono un'[offerta speciale][special_offer]: $ 10 di credito Twilio quando si esegue l'aggiornamento dell'account Twilio.</span><span class="sxs-lookup"><span data-stu-id="c5841-117">Azure customers receive a [special offer][special_offer] $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="c5841-118">Il credito Twilio può essere applicato a qualsiasi utilizzo di Twilio ($ 10 di credito equivalgono all'invio di 1.000 SMS o a 1.000 minuti voce per le chiamate in entrata, a seconda della località del numero di telefono, del messaggio o della destinazione della chiamata).</span><span class="sxs-lookup"><span data-stu-id="c5841-118">This Twilio Credit can be applied to any Twilio usage ($10 credit equivalent to sending as many as 1,000 SMS messages or receiving up to 1000 inbound Voice minutes, depending on the location of your phone number and message or call destination).</span></span> <span data-ttu-id="c5841-119">Riscattare il [credito Twilio][special_offer] e iniziare a usare il servizio.</span><span class="sxs-lookup"><span data-stu-id="c5841-119">Redeem this [Twilio credit][special_offer] and get started.</span></span>

<span data-ttu-id="c5841-120">Twilio è un servizio con pagamento in base al consumo.</span><span class="sxs-lookup"><span data-stu-id="c5841-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="c5841-121">Non prevede spese iniziali ed è possibile chiudere l'account in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="c5841-121">There are no set-up fees and you can close your account at any time.</span></span> <span data-ttu-id="c5841-122">Per altre informazioni, vedere la pagina [Twilio Pricing][twilio_pricing] (Prezzi di Twilio).</span><span class="sxs-lookup"><span data-stu-id="c5841-122">You can find more details at [Twilio Pricing][twilio_pricing].</span></span>

## <span data-ttu-id="c5841-123"><a id="Concepts"></a>Concetti</span><span class="sxs-lookup"><span data-stu-id="c5841-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="c5841-124">L'API Twilio è un'API RESTful che fornisce funzionalità voce ed SMS per le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="c5841-124">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="c5841-125">Le librerie client sono disponibili in più lingue. Per un elenco, vedere [Twilio API Libraries][twilio_libraries] (Librerie dell'API Twilio).</span><span class="sxs-lookup"><span data-stu-id="c5841-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="c5841-126">I concetti principali dell'API Twilio sono costituiti dai verbi Twilio e dal linguaggio di markup Twilio (Twilio Markup Language, TwiML).</span><span class="sxs-lookup"><span data-stu-id="c5841-126">Key aspects of the Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="c5841-127"><a id="Verbs"></a>Verbi Twilio</span><span class="sxs-lookup"><span data-stu-id="c5841-127"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="c5841-128">Nell'API vengono usati i verbi di Twilio: il verbo **&lt;Say&gt;**, ad esempio, indica a Twilio di recapitare un messaggio acustico in una chiamata.</span><span class="sxs-lookup"><span data-stu-id="c5841-128">The API makes use of Twilio verbs; for example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span>

<span data-ttu-id="c5841-129">Di seguito è riportato un elenco dei verbi Twilio.</span><span class="sxs-lookup"><span data-stu-id="c5841-129">The following is a list of Twilio verbs.</span></span> <span data-ttu-id="c5841-130">Per altre informazioni su altri verbi e funzionalità, vedere la [documentazione relativa al linguaggio di markup Twilio][twiml].</span><span class="sxs-lookup"><span data-stu-id="c5841-130">Learn about the other verbs and capabilities via [Twilio Markup Language documentation][twiml].</span></span>

* <span data-ttu-id="c5841-131">**&lt;Dial&gt;**: connette il chiamante a un altro telefono.</span><span class="sxs-lookup"><span data-stu-id="c5841-131">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="c5841-132">**&lt;Gather&gt;**: raccoglie i numeri digitati sulla tastiera del telefono.</span><span class="sxs-lookup"><span data-stu-id="c5841-132">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="c5841-133">**&lt;Hangup&gt;**: termina una chiamata.</span><span class="sxs-lookup"><span data-stu-id="c5841-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="c5841-134">**&lt;Pause&gt;**: attende in modo silenzioso per un numero di secondi specificato.</span><span class="sxs-lookup"><span data-stu-id="c5841-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="c5841-135">**&lt;Play&gt;**: riproduce un file audio.</span><span class="sxs-lookup"><span data-stu-id="c5841-135">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="c5841-136">**&lt;Queue&gt;**: aggiunge l'elemento a una coda di chiamanti.</span><span class="sxs-lookup"><span data-stu-id="c5841-136">**&lt;Queue&gt;**: Add the to a queue of callers.</span></span>
* <span data-ttu-id="c5841-137">**&lt;Record&gt;**: registra la voce del chiamante e restituisce l'URL del file contenente la registrazione.</span><span class="sxs-lookup"><span data-stu-id="c5841-137">**&lt;Record&gt;**: Records the voice of the caller and returns a URL of a file that contains the recording.</span></span>
* <span data-ttu-id="c5841-138">**&lt;Redirect&gt;**: trasferisce il controllo di una chiamata o di un SMS al codice TwiML presso un URL diverso.</span><span class="sxs-lookup"><span data-stu-id="c5841-138">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="c5841-139">**&lt;Reject&gt;**: rifiuta una chiamata in arrivo al numero Twilio senza alcun addebito.</span><span class="sxs-lookup"><span data-stu-id="c5841-139">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you.</span></span>
* <span data-ttu-id="c5841-140">**&lt;Say&gt;**: effettua la sintesi vocale del testo durante una chiamata.</span><span class="sxs-lookup"><span data-stu-id="c5841-140">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="c5841-141">**&lt;Sms&gt;**: invia un SMS.</span><span class="sxs-lookup"><span data-stu-id="c5841-141">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="c5841-142"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="c5841-142"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="c5841-143">TwiML è un set di istruzioni basate su XML e sui verbi Twilio che indicano a Twilio come elaborare una chiamata o un SMS.</span><span class="sxs-lookup"><span data-stu-id="c5841-143">TwiML is a set of XML-based instructions based on the Twilio verbs that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="c5841-144">Ad esempio, il codice TwiML seguente effettua la sintesi vocale del testo **Hello World** .</span><span class="sxs-lookup"><span data-stu-id="c5841-144">As an example, the following TwiML would convert the text **Hello World** to speech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

<span data-ttu-id="c5841-145">Quando l'applicazione chiama l'API Twilio, uno dei parametri dell'API è l'URL che restituisce la risposta TwiML.</span><span class="sxs-lookup"><span data-stu-id="c5841-145">When your application calls the Twilio API, one of the API parameters is the URL that returns the TwiML response.</span></span> <span data-ttu-id="c5841-146">Ai fini dello sviluppo, è possibile utilizzare gli URL offerti da Twilio per fornire le risposte TwiML utilizzate dalle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="c5841-146">For development purposes, you can use Twilio-provided URLs to provide the TwiML responses used by your applications.</span></span> <span data-ttu-id="c5841-147">È inoltre possibile ospitare gli URL per generare le risposte TwiML. In alternativa, usare l'oggetto `TwiMLResponse`.</span><span class="sxs-lookup"><span data-stu-id="c5841-147">You could also host your own URLs to produce the TwiML responses, and another option is to use the `TwiMLResponse` object.</span></span>

<span data-ttu-id="c5841-148">Per altre informazioni sui verbi Twilio, i relativi attributi e il codice TwiML, vedere [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="c5841-148">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="c5841-149">Per altre informazioni sull'API Twilio, vedere [Twilio API][twilio_api] (API Twilio).</span><span class="sxs-lookup"><span data-stu-id="c5841-149">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="c5841-150"><a id="CreateAccount"></a>Creare un account Twilio</span><span class="sxs-lookup"><span data-stu-id="c5841-150"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="c5841-151">Se si desidera creare un account Twilio, iscriversi nella pagina relativa alla [registrazione gratuita di Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="c5841-151">When you are ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="c5841-152">È possibile iniziare con un account gratuito ed eseguire l'aggiornamento in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="c5841-152">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="c5841-153">Quando si effettua l'iscrizione a un account Twilio, si riceveranno il SID account e un token di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c5841-153">When you sign up for a Twilio account, you receive an account SID and an authentication token.</span></span> <span data-ttu-id="c5841-154">Entrambe queste informazioni sono necessarie per effettuare chiamate all'API Twilio.</span><span class="sxs-lookup"><span data-stu-id="c5841-154">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="c5841-155">Per prevenire accessi autorizzati all'account, conservare il token di autenticazione in un luogo sicuro.</span><span class="sxs-lookup"><span data-stu-id="c5841-155">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="c5841-156">Il SID dell'account e il token di autorizzazione sono visualizzabili nella [console di Twilio][twilio_console], rispettivamente nei campi **ACCOUNT SID** (SID ACCOUNT) e **AUTH TOKEN** (TOKEN AUTORIZZAZIONE).</span><span class="sxs-lookup"><span data-stu-id="c5841-156">Your account SID and authentication token are viewable in the [Twilio Console][twilio_console], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="c5841-157"><a id="create_app"></a>Creare un'applicazione Python</span><span class="sxs-lookup"><span data-stu-id="c5841-157"><a id="create_app"></a>Create a Python Application</span></span>
<span data-ttu-id="c5841-158">Un'applicazione Python che usa il servizio Twilio e viene eseguita in Azure non è diversa da qualsiasi altra applicazione Python che usa il servizio Twilio.</span><span class="sxs-lookup"><span data-stu-id="c5841-158">A Python application that uses the Twilio service and is running in Azure is no different than any other Python application that uses the Twilio service.</span></span> <span data-ttu-id="c5841-159">Benché i servizi Twilio siano basati su REST e possano essere chiamati da Python in diversi modi, questo articolo illustra solo come usare i servizi Twilio con la [libreria Twilio per Python da GitHub][twilio_python].</span><span class="sxs-lookup"><span data-stu-id="c5841-159">While Twilio services are REST-based and can be called from Python in several ways, this article will focus on how to use Twilio services with [Twilio library for Python from GitHub][twilio_python].</span></span> <span data-ttu-id="c5841-160">Per altre informazioni sull'uso della libreria Twilio per Python, vedere [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].</span><span class="sxs-lookup"><span data-stu-id="c5841-160">For more information about using the Twilio library for Python, see [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].</span></span>

<span data-ttu-id="c5841-161">In primo luogo, [configurare una nuova macchina virtuale Linux in Azure][azure_vm_setup] che funga da host per la nuova applicazione Web Python.</span><span class="sxs-lookup"><span data-stu-id="c5841-161">First, [set-up a new Azure Linux VM][azure_vm_setup] to act as a host for your new Python web application.</span></span> <span data-ttu-id="c5841-162">Quando la macchina virtuale è in esecuzione, è necessario esporla su una porta pubblica, come descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="c5841-162">Once the Virtual Machine is running, you will need to expose your application on a public port as described below.</span></span>

### <a name="add-an-incoming-rule"></a><span data-ttu-id="c5841-163">Aggiungere una regola in ingresso</span><span class="sxs-lookup"><span data-stu-id="c5841-163">Add An Incoming Rule</span></span>
  1. <span data-ttu-id="c5841-164">Passare alla pagina [Gruppo di sicurezza di rete][azure_nsg].</span><span class="sxs-lookup"><span data-stu-id="c5841-164">Go to the [Network Security Group][azure_nsg] page.</span></span>
  2. <span data-ttu-id="c5841-165">Selezionare il gruppo di sicurezza di rete corrispondente alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c5841-165">Select the Network Security Group that corresponds with your Virtual Machine.</span></span>
  3. <span data-ttu-id="c5841-166">Aggiungere una **Regola in uscita** per la **porta 80**.</span><span class="sxs-lookup"><span data-stu-id="c5841-166">Add and **Outgoing Rule** for **port 80**.</span></span> <span data-ttu-id="c5841-167">Verificare di consentire l'ingresso da qualsiasi indirizzo.</span><span class="sxs-lookup"><span data-stu-id="c5841-167">Be sure to allow incoming from any address.</span></span>

### <a name="set-the-dns-name-label"></a><span data-ttu-id="c5841-168">Impostare l'etichetta del nome DNS</span><span class="sxs-lookup"><span data-stu-id="c5841-168">Set the DNS Name Label</span></span>
  1. <span data-ttu-id="c5841-169">Passare alla pagina [Indirizzi IP pubblici][azure_ips].</span><span class="sxs-lookup"><span data-stu-id="c5841-169">Go to the [The Public IP Adresses][azure_ips] page.</span></span>
  2. <span data-ttu-id="c5841-170">Selezionare l'indirizzo IP corrispondente alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c5841-170">Select the Public IP that correspends with your Virtual Machine.</span></span>
  3. <span data-ttu-id="c5841-171">Impostare **Etichetta del nome DNS** nella sezione **Configurazione**.</span><span class="sxs-lookup"><span data-stu-id="c5841-171">Set the **DNS Name Label** in the **Configuration** section.</span></span> <span data-ttu-id="c5841-172">Nel caso di questo esempio, verrà visualizzata una dicitura simile a *etichetta-dominio*.centralus.cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="c5841-172">In the case of this example it will look something like this *your-domain-label*.centralus.cloudapp.azure.com</span></span>

<span data-ttu-id="c5841-173">Quando si è in grado di connettersi alla macchina virtuale tramite SSH, è possibile installare il framework Web scelto. In Python i due framework più noti sono [Flask](http://flask.pocoo.org/) e [Django](https://www.djangoproject.com).</span><span class="sxs-lookup"><span data-stu-id="c5841-173">Once you are able to connect through SSH to the Virtual Machine you can install the Web Framework of your choice (the two most well known in Python being [Flask](http://flask.pocoo.org/) and [Django](https://www.djangoproject.com)).</span></span> <span data-ttu-id="c5841-174">Per installarne uno è sufficiente eseguire il comando `pip install`.</span><span class="sxs-lookup"><span data-stu-id="c5841-174">You can install either of them just by running the `pip install` command.</span></span>

<span data-ttu-id="c5841-175">Tenere presente che la macchina virtuale è stata configurata per consentire il traffico solo sulla porta 80.</span><span class="sxs-lookup"><span data-stu-id="c5841-175">Keep in mind that we configured the Virtual Machine to allow traffic only on port 80.</span></span> <span data-ttu-id="c5841-176">Di conseguenza, verificare di configurare l'applicazione per l'uso di questa porta.</span><span class="sxs-lookup"><span data-stu-id="c5841-176">So make sure to configure the application to use this port.</span></span>

## <span data-ttu-id="c5841-177"><a id="configure_app"></a>Configurare l'applicazione per l'uso delle librerie Twilio</span><span class="sxs-lookup"><span data-stu-id="c5841-177"><a id="configure_app"></a>Configure Your Application to Use Twilio Libraries</span></span>
<span data-ttu-id="c5841-178">È possibile configurare l'applicazione per l'uso della libreria Twilio per Python in due modi:</span><span class="sxs-lookup"><span data-stu-id="c5841-178">You can configure your application to use the Twilio library for Python in two ways:</span></span>

* <span data-ttu-id="c5841-179">Installare la libreria Twilio per Python come pacchetto Pip.</span><span class="sxs-lookup"><span data-stu-id="c5841-179">Install the Twilio library for Python as a Pip package.</span></span> <span data-ttu-id="c5841-180">È possibile eseguire l'installazione tramite i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c5841-180">It can be installed with the following commands:</span></span>
   
        $ pip install twilio

    <span data-ttu-id="c5841-181">-OPPURE-</span><span class="sxs-lookup"><span data-stu-id="c5841-181">-OR-</span></span>

* <span data-ttu-id="c5841-182">Scaricare la libreria Twilio per Python da GitHub ([https://github.com/twilio/twilio-python][twilio_python]) e installarla nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="c5841-182">Download the Twilio library for Python from GitHub ([https://github.com/twilio/twilio-python][twilio_python]) and install it like this:</span></span>

        $ python setup.py install

<span data-ttu-id="c5841-183">Dopo avere installato la libreria Twilio per Python, è possibile usare il comando `import` per importarla nei file Python:</span><span class="sxs-lookup"><span data-stu-id="c5841-183">Once you have installed the Twilio library for Python, you can then `import` it in your Python files:</span></span>

        import twilio

<span data-ttu-id="c5841-184">Per altre informazioni, vedere [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].</span><span class="sxs-lookup"><span data-stu-id="c5841-184">For more information, see [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].</span></span>

## <span data-ttu-id="c5841-185"><a id="howto_make_call"></a>Procedura: Effettuare una chiamata in uscita</span><span class="sxs-lookup"><span data-stu-id="c5841-185"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="c5841-186">Di seguito è illustrato come effettuare una chiamata in uscita.</span><span class="sxs-lookup"><span data-stu-id="c5841-186">The following shows how to make an outgoing call.</span></span> <span data-ttu-id="c5841-187">Questo codice utilizza inoltre un sito fornito da Twilio per restituire la risposta TwiML (Twilio Markup Language).</span><span class="sxs-lookup"><span data-stu-id="c5841-187">This code also uses a Twilio-provided site to return the Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="c5841-188">Sostituire i valori di **from_number** e **to_number** relativi ai numeri di telefono e, prima di eseguire il codice, verificare il numero di telefono specificato in **from_number** per l'account Twilio.</span><span class="sxs-lookup"><span data-stu-id="c5841-188">Substitute your values for the **from_number** and **to_number** phone numbers, and ensure that you've verified the **from_number** phone number for your Twilio account before running the code.</span></span>

    from urllib.parse import urlencode

    # Import the Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    # The number of the phone initiating the the call.
    # This should either be a Twilio number or a number that you've verified
    from_number = "NNNNNNNNNNN"

    # The number of the phone receiving call.
    to_number = "NNNNNNNNNNN"

    # Use the Twilio-provided site for the TwiML response.
    url = "http://twimlets.com/message?"

    # The phone message text.
    message = "Hello world."

    # Initialize the Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make the call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url + urlencode({'Message': message}))
    print(call.sid)

<span data-ttu-id="c5841-189">Come indicato in precedenza, questo codice utilizza un sito fornito da Twilio per restituire la risposta TwiML.</span><span class="sxs-lookup"><span data-stu-id="c5841-189">As mentioned, this code uses a Twilio-provided site to return the TwiML response.</span></span> <span data-ttu-id="c5841-190">Per fornire la risposta TwiML è inoltre possibile usare il proprio sito. Per altre informazioni, vedere [Come fornire risposte TwiML dal proprio sito Web](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="c5841-190">You could instead use your own site to provide the TwiML response; for more information, see [How to Provide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="c5841-191"><a id="howto_send_sms"></a>Procedura: Inviare un messaggio SMS</span><span class="sxs-lookup"><span data-stu-id="c5841-191"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="c5841-192">La schermata seguente mostra come inviare un messaggio SMS tramite la classe `TwilioRestClient`.</span><span class="sxs-lookup"><span data-stu-id="c5841-192">The following shows how to send an SMS message using the `TwilioRestClient` class.</span></span> <span data-ttu-id="c5841-193">Il numero riportato in **from_number** per l'invio di messaggi SMS con gli account di valutazione è fornito da Twilio.</span><span class="sxs-lookup"><span data-stu-id="c5841-193">The **from_number** number is provided by Twilio for trial accounts to send SMS messages.</span></span> <span data-ttu-id="c5841-194">Il numero riportato in **to_number** deve essere verificato per l'account Twilio prima di eseguire il codice.</span><span class="sxs-lookup"><span data-stu-id="c5841-194">The **to_number** number must be verified for your Twilio account before running the code.</span></span>

    # Import the Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    from_number = "NNNNNNNNNNN"  # With trial account, texts can only be sent from your Twilio number.
    to_number = "NNNNNNNNNNN"
    message = "Hello world."

    # Initialize the Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Send the SMS message.
    message = client.messages.create(to=to_number,
                                     from_=from_number,
                                     body=message)

## <span data-ttu-id="c5841-195"><a id="howto_provide_twiml_responses"></a>Procedura: Fornire risposte TwiML dal proprio sito Web</span><span class="sxs-lookup"><span data-stu-id="c5841-195"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="c5841-196">Quando l'applicazione avvia una chiamata all'API Twilio, Twilio invia la richiesta a un URL che deve restituire una risposta TwiML.</span><span class="sxs-lookup"><span data-stu-id="c5841-196">When your application initiates a call to the Twilio API, Twilio will send your request to a URL that is expected to return a TwiML response.</span></span> <span data-ttu-id="c5841-197">Nell'esempio precedente viene usato l'URL fornito da Twilio [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="c5841-197">The example above uses the Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="c5841-198">Poiché TwiML è stato progettato per essere usato da Twilio, è possibile visualizzarlo nel browser.</span><span class="sxs-lookup"><span data-stu-id="c5841-198">(While TwiML is designed for use by Twilio, you can view it in your browser.</span></span> <span data-ttu-id="c5841-199">Ad esempio, fare clic su [http://twimlets.com/message][twimlet_message_url] per visualizzare un elemento `<Response>` vuoto oppure fare clic su [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] per visualizzare un elemento `<Response>` contenente un elemento `<Say>`.</span><span class="sxs-lookup"><span data-stu-id="c5841-199">For example, click [http://twimlets.com/message][twimlet_message_url] to see an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] to see a `<Response>` element that contains a `<Say>` element.)</span></span>

<span data-ttu-id="c5841-200">Anziché utilizzare l'URL fornito da Twilio, è possibile creare un sito personalizzato che restituisce risposte HTTP.</span><span class="sxs-lookup"><span data-stu-id="c5841-200">Instead of relying on the Twilio-provided URL, you can create your own site that returns HTTP responses.</span></span> <span data-ttu-id="c5841-201">È possibile creare il sito in qualsiasi linguaggio che restituisca risposte XML. In questo argomento si presuppone che per la creazione di TwiML venga usato Python.</span><span class="sxs-lookup"><span data-stu-id="c5841-201">You can create the site in any language that returns XML responses; this topic assumes you will be using Python to create the TwiML.</span></span>

<span data-ttu-id="c5841-202">Negli esempi seguenti viene generata una risposta TwiML **Hello World** nella chiamata.</span><span class="sxs-lookup"><span data-stu-id="c5841-202">The following examples will output a TwiML response that says **Hello World** on the call.</span></span>

<span data-ttu-id="c5841-203">Con Flask:</span><span class="sxs-lookup"><span data-stu-id="c5841-203">With Flask:</span></span>

    from flask import Response
    @app.route("/")
    def hello():
        xml = '<Response><Say>Hello world.</Say></Response>'
        return Response(xml, mimetype='text/xml')

<span data-ttu-id="c5841-204">Con Django:</span><span class="sxs-lookup"><span data-stu-id="c5841-204">With Django:</span></span>

    from django.http import HttpResponse
    def hello(request):
        xml = '<Response><Say>Hello world.</Say></Response>'
        return HttpResponse(xml, content_type='text/xml')

<span data-ttu-id="c5841-205">Come si evince dal codice riportato sopra, la risposta TwiML è semplicemente un documento XML.</span><span class="sxs-lookup"><span data-stu-id="c5841-205">As you can see from the example above, the TwiML response is simply an XML document.</span></span> <span data-ttu-id="c5841-206">La libreria Twilio per Python contiene le classi che consentono di generare automaticamente le istruzioni TwiML.</span><span class="sxs-lookup"><span data-stu-id="c5841-206">The Twilio library for Python contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="c5841-207">Nell'esempio seguente viene generata la stessa risposta descritta sopra, ma usando il modulo `twiml` nella libreria Twilio per Python:</span><span class="sxs-lookup"><span data-stu-id="c5841-207">The example below produces the equivalent response as shown above, but uses the `twiml` module in the Twilio library for Python:</span></span>

    from twilio import twiml

    response = twiml.Response()
    response.say("Hello world.")
    print(str(response))

<span data-ttu-id="c5841-208">Per altre informazioni su TwiML, vedere [https://www.twilio.com/docs/api/twiml][twiml_reference].</span><span class="sxs-lookup"><span data-stu-id="c5841-208">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span></span>

<span data-ttu-id="c5841-209">Dopo aver configurato l'applicazione Python in modo da fornire risposte TwiML, usare l'URL di tale applicazione come URL trasmesso nel metodo `client.calls.create`.</span><span class="sxs-lookup"><span data-stu-id="c5841-209">Once you have your Python application set up to provide TwiML responses, use the URL of the application as the URL passed into the `client.calls.create`  method.</span></span> <span data-ttu-id="c5841-210">Se, ad esempio, si dispone di un'applicazione Web denominata **MyTwiML** distribuita in un servizio ospitato in Azure, è possibile usare il relativo URL come webhook, come mostrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="c5841-210">For example, if you have a Web application named **MyTwiML** deployed to an Azure hosted service, you can use its url as webhook as shown in the following example:</span></span>

    from twilio.rest import TwilioRestClient

    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"
    from_number = "NNNNNNNNNNN"
    to_number = "NNNNNNNNNNN"
    url = "http://your-domain-label.centralus.cloudapp.azure.com/MyTwiML/"

    # Initialize the Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make the call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url)
    print(call.sid)

## <span data-ttu-id="c5841-211"><a id="AdditionalServices"></a>Procedura: Utilizzare servizi Twilio aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="c5841-211"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="c5841-212">Oltre agli esempi illustrati in questa pagina, Twilio offre API basate su Web che è possibile utilizzare per sfruttare altre funzionalità di Twilio dall'applicazione Azure.</span><span class="sxs-lookup"><span data-stu-id="c5841-212">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="c5841-213">Per informazioni dettagliate, vedere la [documentazione sull'API Twilio][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="c5841-213">For full details, see the [Twilio API documentation][twilio_api].</span></span>

## <span data-ttu-id="c5841-214"><a id="NextSteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c5841-214"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="c5841-215">A questo punto, dopo aver appreso le nozioni di base del servizio Twilio, usare i collegamenti seguenti per altre informazioni:</span><span class="sxs-lookup"><span data-stu-id="c5841-215">Now that you have learned the basics of the Twilio service, follow these links to learn more:</span></span>

* <span data-ttu-id="c5841-216">[Twilio Security Guidelines][twilio_security_guidelines] (Linee guida sulla sicurezza di Twilio)</span><span class="sxs-lookup"><span data-stu-id="c5841-216">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="c5841-217">[Twilio HowTo Guides and Example Code][twilio_howtos] (Procedure e codice di esempio su Twilio)</span><span class="sxs-lookup"><span data-stu-id="c5841-217">[Twilio HowTo Guides and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="c5841-218">[Twilio Quickstart Tutorials][twilio_quickstarts] (Esercitazioni con guide rapide su Twilio)</span><span class="sxs-lookup"><span data-stu-id="c5841-218">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span>
* <span data-ttu-id="c5841-219">[Twilio on GitHub][twilio_on_github] (Twilio su GitHub)</span><span class="sxs-lookup"><span data-stu-id="c5841-219">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="c5841-220">[Talk to Twilio Support][twilio_support] (Contattare il supporto di Twilio)</span><span class="sxs-lookup"><span data-stu-id="c5841-220">[Talk to Twilio Support][twilio_support]</span></span>

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
