---
title: aaaHow tooUse Twilio per vocali e SMS (.NET) | Documenti Microsoft
description: Informazioni su come messaggio di toomake una telefonata e inviare un SMS con il servizio API di Twilio hello in Azure. Esempi di codice scritti in .NET.
services: 
documentationcenter: .net
author: devinrader
manager: twilio
editor: 
ms.assetid: 74d4f3c9-f1cb-4968-b744-36b32cd0e834
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/24/2015
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: f568da87ef15e9f540fee9674de31e983d4acb6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-from-azure"></a><span data-ttu-id="c1e90-104">Come toouse Twilio per funzionalità voce ed SMS da Azure</span><span class="sxs-lookup"><span data-stu-id="c1e90-104">How toouse Twilio for voice and SMS capabilities from Azure</span></span>
<span data-ttu-id="c1e90-105">Questa guida illustra come tooperform attività di programmazione comuni con hello Twilio API del servizio in Azure.</span><span class="sxs-lookup"><span data-stu-id="c1e90-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="c1e90-106">scenari di Hello trattati includono una telefonata e inviare un messaggio breve servizio SMS (Message).</span><span class="sxs-lookup"><span data-stu-id="c1e90-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="c1e90-107">Per ulteriori informazioni su Twilio e l'utilizzo di audio e SMS nelle applicazioni, vedere hello [passaggi successivi](#NextSteps) sezione.</span><span class="sxs-lookup"><span data-stu-id="c1e90-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next steps](#NextSteps) section.</span></span>

## <span data-ttu-id="c1e90-108"><a id="WhatIs"></a>Informazioni su Twilio</span><span class="sxs-lookup"><span data-stu-id="c1e90-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="c1e90-109">Twilio è accensione hello futuro delle comunicazioni aziendali, l'abilitazione di vocale tooembed gli sviluppatori, VoIP e nelle applicazioni di messaggistica.</span><span class="sxs-lookup"><span data-stu-id="c1e90-109">Twilio is powering hello future of business communications, enabling developers tooembed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="c1e90-110">Essi virtualizzare tutta l'infrastruttura necessaria in un ambiente globale, basato su cloud, esporlo tramite API di comunicazione Twilio hello.</span><span class="sxs-lookup"><span data-stu-id="c1e90-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through hello Twilio communications API platform.</span></span> <span data-ttu-id="c1e90-111">Le applicazioni sono toobuild semplice e scalabile.</span><span class="sxs-lookup"><span data-stu-id="c1e90-111">Applications are simple toobuild and scalable.</span></span> <span data-ttu-id="c1e90-112">Offre flessibilità, grazie a un modello di prezzi con pagamento in base al consumo, e l'affidabilità del cloud.</span><span class="sxs-lookup"><span data-stu-id="c1e90-112">Enjoy flexibility with pay-as-you-go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="c1e90-113">**Twilio vocale** consente toomake le applicazioni e ricevere chiamate telefoniche.</span><span class="sxs-lookup"><span data-stu-id="c1e90-113">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="c1e90-114">**SMS Twilio** consente toosend le applicazioni e la ricezione di messaggi SMS.</span><span class="sxs-lookup"><span data-stu-id="c1e90-114">**Twilio SMS** enables your applications toosend and receive SMS messages.</span></span> <span data-ttu-id="c1e90-115">**Twilio Client** consente le chiamate VoIP toomake da qualsiasi telefono, tablet o browser e supporta WebRTC.</span><span class="sxs-lookup"><span data-stu-id="c1e90-115">**Twilio Client** allows you toomake VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="c1e90-116"><a id="Pricing"></a>Prezzi e offerte speciali di Twilio</span><span class="sxs-lookup"><span data-stu-id="c1e90-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="c1e90-117">I clienti di Azure riceveranno un' [offerta speciale](http://www.twilio.com/azure): $ 10 di credito Twilio all'aggiornamento dell'account Twilio.</span><span class="sxs-lookup"><span data-stu-id="c1e90-117">Azure customers receive a [special offer](http://www.twilio.com/azure): complimentary $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="c1e90-118">Il credito di Twilio può essere applicato tooany Twilio utilizzo ($10 credito equivalente toosending fino a 1.000 messaggi SMS o alla ricezione di too1000 in ingresso minuti vocale, a seconda della posizione di hello della destinazione e numero di messaggio o una chiamata telefonica).</span><span class="sxs-lookup"><span data-stu-id="c1e90-118">This Twilio Credit can be applied tooany Twilio usage ($10 credit equivalent toosending as many as 1,000 SMS messages or receiving up too1000 inbound Voice minutes, depending on hello location of your phone number and message or call destination).</span></span> <span data-ttu-id="c1e90-119">Per riscattare il credito Twilio e iniziare a utilizzare il servizio, visitare la pagina all'indirizzo [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span><span class="sxs-lookup"><span data-stu-id="c1e90-119">Redeem this Twilio credit and get started at [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span></span>

<span data-ttu-id="c1e90-120">Twilio è un servizio con pagamento in base al consumo.</span><span class="sxs-lookup"><span data-stu-id="c1e90-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="c1e90-121">Non prevede spese iniziali ed è possibile chiudere l'account in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="c1e90-121">There are no set-up fees, and you can close your account at any time.</span></span> <span data-ttu-id="c1e90-122">Per altre informazioni, vedere la pagina relativa ai [prezzi di Twilio](http://www.twilio.com/voice/pricing).</span><span class="sxs-lookup"><span data-stu-id="c1e90-122">You can find more details at [Twilio Pricing](http://www.twilio.com/voice/pricing).</span></span>

## <span data-ttu-id="c1e90-123"><a id="Concepts"></a>Concetti</span><span class="sxs-lookup"><span data-stu-id="c1e90-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="c1e90-124">API di Twilio Hello è un'API RESTful che fornisce funzionalità SMS e vocale per le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="c1e90-124">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="c1e90-125">Le librerie client sono disponibili in più lingue. Per un elenco, vedere [Twilio API Libraries][twilio_libraries] (Librerie dell'API Twilio).</span><span class="sxs-lookup"><span data-stu-id="c1e90-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="c1e90-126">Gli aspetti chiave di hello Twilio API sono verbi Twilio e Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="c1e90-126">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="c1e90-127"><a id="Verbs"></a>Verbi Twilio</span><span class="sxs-lookup"><span data-stu-id="c1e90-127"><a id="Verbs"></a>Twilio verbs</span></span>
<span data-ttu-id="c1e90-128">Hello API utilizza Twilio verbi. ad esempio, hello  **&lt;pronuncia&gt;**  verbo indica Twilio tooaudibly inviare un messaggio in una chiamata.</span><span class="sxs-lookup"><span data-stu-id="c1e90-128">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="c1e90-129">Hello seguito è riportato un elenco dei verbi di Twilio.</span><span class="sxs-lookup"><span data-stu-id="c1e90-129">hello following is a list of Twilio verbs.</span></span>  <span data-ttu-id="c1e90-130">Informazioni sui hello altri verbi tramite [la documentazione del linguaggio di Markup Twilio](http://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="c1e90-130">Learn about hello other verbs and capabilities via [Twilio Markup Language documentation](http://www.twilio.com/docs/api/twiml).</span></span>

* <span data-ttu-id="c1e90-131">**&lt;Connessione&gt;**: connette phone tooanother di hello chiamante.</span><span class="sxs-lookup"><span data-stu-id="c1e90-131">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="c1e90-132">**&lt;Raccogliere&gt;**: raccoglie cifre immesse sul tastierino telefonico hello.</span><span class="sxs-lookup"><span data-stu-id="c1e90-132">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="c1e90-133">**&lt;Hangup&gt;**: termina una chiamata.</span><span class="sxs-lookup"><span data-stu-id="c1e90-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="c1e90-134">**&lt;Play&gt;**: riproduce un file audio.</span><span class="sxs-lookup"><span data-stu-id="c1e90-134">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="c1e90-135">**&lt;Pause&gt;**: attende in modo silenzioso per un numero di secondi specificato.</span><span class="sxs-lookup"><span data-stu-id="c1e90-135">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="c1e90-136">**&lt;Record&gt;**: registra una voce del chiamante hello e restituisce un URL di un file che contenga la registrazione di hello.</span><span class="sxs-lookup"><span data-stu-id="c1e90-136">**&lt;Record&gt;**: Records hello caller's voice and returns an URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="c1e90-137">**&lt;Reindirizzare&gt;**: trasferisce il controllo di una telefonata o SMS toohello TwiML in un URL diverso.</span><span class="sxs-lookup"><span data-stu-id="c1e90-137">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="c1e90-138">**&lt;Rifiutare&gt;**: rifiuta un fax in ingresso chiamare tooyour Twilio numero senza fatturazione si</span><span class="sxs-lookup"><span data-stu-id="c1e90-138">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you</span></span>
* <span data-ttu-id="c1e90-139">**&lt;Ad esempio&gt;**: converte toospeech di testo che viene effettuata una chiamata.</span><span class="sxs-lookup"><span data-stu-id="c1e90-139">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="c1e90-140">**&lt;Sms&gt;**: invia un SMS.</span><span class="sxs-lookup"><span data-stu-id="c1e90-140">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="c1e90-141"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="c1e90-141"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="c1e90-142">TwiML è un set di istruzioni basato su XML in base a verbi Twilio hello che informano Twilio come tooprocess una telefonata o SMS.</span><span class="sxs-lookup"><span data-stu-id="c1e90-142">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="c1e90-143">Ad esempio, hello seguente TwiML conversione testo hello **Hello World** toospeech.</span><span class="sxs-lookup"><span data-stu-id="c1e90-143">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

<span data-ttu-id="c1e90-144">Quando l'applicazione chiama hello API Twilio, uno dei parametri di API hello è URL hello che restituisce una risposta TwiML hello.</span><span class="sxs-lookup"><span data-stu-id="c1e90-144">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="c1e90-145">A scopo di sviluppo, è possibile utilizzare le risposte TwiML hello tooprovide URL fornito Twilio utilizzate dalle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="c1e90-145">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="c1e90-146">È anche possibile ospitare le proprie URL tooproduce hello TwiML risposte e un'altra opzione consiste hello toouse **TwiMLResponse** oggetto.</span><span class="sxs-lookup"><span data-stu-id="c1e90-146">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello **TwiMLResponse** object.</span></span>

<span data-ttu-id="c1e90-147">Per altre informazioni sui verbi Twilio, i relativi attributi e il codice TwiML, vedere [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="c1e90-147">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="c1e90-148">Per ulteriori informazioni su hello Twilio API, vedere [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="c1e90-148">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="c1e90-149"><a id="CreateAccount"></a>Creare un account Twilio</span><span class="sxs-lookup"><span data-stu-id="c1e90-149"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="c1e90-150">Quando sarai pronto tooget un account di Twilio, iscriversi al [provare Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="c1e90-150">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="c1e90-151">È possibile iniziare con un account gratuito ed eseguire l'aggiornamento in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="c1e90-151">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="c1e90-152">Quando si effettua l'iscrizione a un account Twilio, si riceverà un ID account e un token di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c1e90-152">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="c1e90-153">Entrambi saranno necessari toomake Twilio API chiamate.</span><span class="sxs-lookup"><span data-stu-id="c1e90-153">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="c1e90-154">non autorizzato tooprevent tooyour account di accesso, proteggere il token di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c1e90-154">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="c1e90-155">L'ID account e l'autenticazione token possono essere visualizzati in hello [pagina account di Twilio][twilio_account]nella hello caselle **SID di ACCOUNT** e **Authentication TOKEN**, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="c1e90-155">Your account ID and authentication token are viewable at hello [Twilio account page][twilio_account], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="c1e90-156"><a id="create_app"></a>Creare un'applicazione Azure</span><span class="sxs-lookup"><span data-stu-id="c1e90-156"><a id="create_app"></a>Create an Azure Application</span></span>
<span data-ttu-id="c1e90-157">Un'applicazione Azure che ospita un'applicazione compatibile con Twilio non è diversa da qualsiasi altra applicazione Azure.</span><span class="sxs-lookup"><span data-stu-id="c1e90-157">An Azure application that hosts a Twilio enabled application is no different from any other Azure application.</span></span> <span data-ttu-id="c1e90-158">Aggiungi libreria .NET di Twilio hello e configurare le librerie .NET di Twilio di hello ruolo toouse hello.</span><span class="sxs-lookup"><span data-stu-id="c1e90-158">You add hello Twilio .NET library and configure hello role toouse hello Twilio .NET libraries.</span></span>
<span data-ttu-id="c1e90-159">Per informazioni sulla creazione di un progetto Azure iniziale, vedere [Creazione di un progetto Azure con Visual Studio][vs_project].</span><span class="sxs-lookup"><span data-stu-id="c1e90-159">For information on creating an initial Azure project, see [Creating an Azure project with Visual Studio][vs_project].</span></span>

## <span data-ttu-id="c1e90-160"><a id="configure_app"></a>Configurare le librerie di Twilio toouse dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="c1e90-160"><a id="configure_app"></a>Configure Your Application toouse Twilio Libraries</span></span>
<span data-ttu-id="c1e90-161">Twilio fornisce un set di librerie di supporto .NET che eseguono il wrapping di vari aspetti di Twilio tooprovide modi molto semplice toointeract con hello API REST di Twilio e dei Twilio Client toogenerate TwiML risposte.</span><span class="sxs-lookup"><span data-stu-id="c1e90-161">Twilio provides a set of .NET helper libraries that wrap various aspects of Twilio tooprovide simple and easy ways toointeract with hello Twilio REST API and Twilio Client toogenerate TwiML responses.</span></span>

<span data-ttu-id="c1e90-162">Twilio offre cinque librerie per sviluppatori .NET:</span><span class="sxs-lookup"><span data-stu-id="c1e90-162">Twilio provides five libraries for .NET developers:</span></span>
<span data-ttu-id="c1e90-163">Libreria</span><span class="sxs-lookup"><span data-stu-id="c1e90-163">Library</span></span>|<span data-ttu-id="c1e90-164">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c1e90-164">Description</span></span>
---|---
<span data-ttu-id="c1e90-165">Twilio.API</span><span class="sxs-lookup"><span data-stu-id="c1e90-165">Twilio.API</span></span>|<span data-ttu-id="c1e90-166">Hello libreria principale di Twilio che esegue il wrapping di API REST di Twilio hello in una libreria .NET descrittiva.</span><span class="sxs-lookup"><span data-stu-id="c1e90-166">hello core Twilio library that wraps hello Twilio REST API in a friendly .NET library.</span></span> <span data-ttu-id="c1e90-167">Questa libreria è disponibile per .NET, Silverlight e Windows Phone 7.</span><span class="sxs-lookup"><span data-stu-id="c1e90-167">This library is available for .NET, Silverlight, and Windows Phone 7.</span></span>
<span data-ttu-id="c1e90-168">Twilio.TwiML</span><span class="sxs-lookup"><span data-stu-id="c1e90-168">Twilio.TwiML</span></span>|<span data-ttu-id="c1e90-169">Fornisce un codice di TwiML toogenerate modo descrittivo .NET.</span><span class="sxs-lookup"><span data-stu-id="c1e90-169">Provides a .NET friendly way toogenerate TwiML markup.</span></span>
<span data-ttu-id="c1e90-170">Twilio.MVC</span><span class="sxs-lookup"><span data-stu-id="c1e90-170">Twilio.MVC</span></span>|<span data-ttu-id="c1e90-171">Per gli sviluppatori che usano ASP.NET MVC, questa libreria include un controller TwilioController, una classe ActionResult TwiML e un attributo di convalida della richiesta.</span><span class="sxs-lookup"><span data-stu-id="c1e90-171">For developers using ASP.NET MVC, this library includes a TwilioController, TwiML ActionResult, and request validation attribute.</span></span>
<span data-ttu-id="c1e90-172">Twilio.WebMatrix</span><span class="sxs-lookup"><span data-stu-id="c1e90-172">Twilio.WebMatrix</span></span>|<span data-ttu-id="c1e90-173">Per gli sviluppatori che utilizzano lo strumento di sviluppo WebMatrix gratuito di Microsoft, questa libreria contiene gli helper della sintassi Razor per varie azioni Twilio.</span><span class="sxs-lookup"><span data-stu-id="c1e90-173">For developers using Microsoft's free WebMatrix development tool, this library contains Razor syntax helpers for various Twilio actions.</span></span>
<span data-ttu-id="c1e90-174">Twilio.Client.Capability</span><span class="sxs-lookup"><span data-stu-id="c1e90-174">Twilio.Client.Capability</span></span>|<span data-ttu-id="c1e90-175">Contiene generatore token hello di funzionalità per l'utilizzo con hello Twilio Client JavaScript SDK.</span><span class="sxs-lookup"><span data-stu-id="c1e90-175">Contains hello Capability token generator for use with hello Twilio Client JavaScript SDK.</span></span>

<span data-ttu-id="c1e90-176">Si noti che tutte le librerie richiedono .NET 3.5, Silverlight 4 o Windows Phone 7 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="c1e90-176">Note that all libraries require .NET 3.5, Silverlight 4, or Windows Phone 7 or later.</span></span>

<span data-ttu-id="c1e90-177">esempi di Hello forniti in questa Guida utilizzano libreria Twilio.API hello.</span><span class="sxs-lookup"><span data-stu-id="c1e90-177">hello samples provided in this guide use hello Twilio.API library.</span></span>

<span data-ttu-id="c1e90-178">possono essere librerie Hello [installato utilizzando l'estensione Gestione pacchetti NuGet di hello](http://www.twilio.com/docs/csharp/install) disponibile per Visual Studio 2010 up too2015.</span><span class="sxs-lookup"><span data-stu-id="c1e90-178">hello libraries can be [installed using hello NuGet package manager extension](http://www.twilio.com/docs/csharp/install) available for Visual Studio 2010 up too2015.</span></span>  <span data-ttu-id="c1e90-179">Hello codice sorgente è ospitato in [GitHub][twilio_github_repo], che include una pagina Wiki che contiene la documentazione completa per l'utilizzo di librerie hello.</span><span class="sxs-lookup"><span data-stu-id="c1e90-179">hello source code is hosted on [GitHub][twilio_github_repo], which includes a Wiki that contains complete documentation for using hello libraries.</span></span>

<span data-ttu-id="c1e90-180">Per impostazione predefinita, con Microsoft Visual Studio 2010 viene installata la versione 1.2 di NuGet.</span><span class="sxs-lookup"><span data-stu-id="c1e90-180">By default, Microsoft Visual Studio 2010 installs version 1.2 of NuGet.</span></span> <span data-ttu-id="c1e90-181">Installazione di librerie di Twilio hello richiede la versione 1.6 di NuGet.</span><span class="sxs-lookup"><span data-stu-id="c1e90-181">Installing hello Twilio libraries requires version 1.6 of NuGet or higher.</span></span> <span data-ttu-id="c1e90-182">Per informazioni sull'installazione o l'aggiornamento di NuGet, vedere [http://nuget.org/][nuget].</span><span class="sxs-lookup"><span data-stu-id="c1e90-182">For information on installing or updating NuGet, see [http://nuget.org/][nuget].</span></span>

> [!NOTE]
> <span data-ttu-id="c1e90-183">tooinstall hello più recente di NuGet, è necessario innanzitutto disinstallare hello versione caricata utilizzando hello Gestione estensioni di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c1e90-183">tooinstall hello latest version of NuGet, you must first uninstall hello loaded version using hello Visual Studio Extension Manager.</span></span> <span data-ttu-id="c1e90-184">toodo in tal caso, è necessario eseguire Visual Studio come amministratore.</span><span class="sxs-lookup"><span data-stu-id="c1e90-184">toodo so, you must run Visual Studio as administrator.</span></span> <span data-ttu-id="c1e90-185">In caso contrario, il pulsante di disinstallazione hello è disabilitato.</span><span class="sxs-lookup"><span data-stu-id="c1e90-185">Otherwise, hello Uninstall button is disabled.</span></span>
>
>

### <span data-ttu-id="c1e90-186"><a id="use_nuget"></a>tooadd hello Twilio librerie tooyour progetto di Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="c1e90-186"><a id="use_nuget"></a>tooadd hello Twilio libraries tooyour Visual Studio project:</span></span>
1. <span data-ttu-id="c1e90-187">Aprire la soluzione in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c1e90-187">Open your solution in Visual Studio.</span></span>
2. <span data-ttu-id="c1e90-188">Fare clic con il pulsante destro del mouse su **Riferimenti**.</span><span class="sxs-lookup"><span data-stu-id="c1e90-188">Right-click **References**.</span></span>
3. <span data-ttu-id="c1e90-189">Scegliere **Gestisci pacchetti NuGet...**</span><span class="sxs-lookup"><span data-stu-id="c1e90-189">Click **Manage NuGet Packages...**</span></span>
4. <span data-ttu-id="c1e90-190">Fare clic su **Online**.</span><span class="sxs-lookup"><span data-stu-id="c1e90-190">Click **Online**.</span></span>
5. <span data-ttu-id="c1e90-191">Nella casella di ricerca hello online, digitare *twilio*.</span><span class="sxs-lookup"><span data-stu-id="c1e90-191">In hello search online box, type *twilio*.</span></span>
6. <span data-ttu-id="c1e90-192">Fare clic su **installare** pacchetto Twilio hello.</span><span class="sxs-lookup"><span data-stu-id="c1e90-192">Click **Install** on hello Twilio package.</span></span>

## <span data-ttu-id="c1e90-193"><a id="howto_make_call"></a>Procedura: Effettuare una chiamata in uscita</span><span class="sxs-lookup"><span data-stu-id="c1e90-193"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="c1e90-194">Hello seguente viene illustrato in uscita toomake chiamare utilizzando hello **CallResource** classe.</span><span class="sxs-lookup"><span data-stu-id="c1e90-194">hello following shows how toomake an outgoing call using hello **CallResource** class.</span></span> <span data-ttu-id="c1e90-195">Questo codice usa anche un hello tooreturn sito Twilio fornita risposta Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="c1e90-195">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="c1e90-196">Sostituire i valori per hello **a** e **da** i numeri di telefono e assicurarsi che si verifichino hello **da** numero di telefono per l'account di Twilio prima di eseguire codice hello.</span><span class="sxs-lookup"><span data-stu-id="c1e90-196">Substitute your values for hello **to** and **from** phone numbers, and ensure that you verify hello **from** phone number for your Twilio account before running hello code.</span></span>

    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    const string accountSID = "your_twilio_account";
    const string authToken = "your_twilio_authentication_token";

    // Initialize hello TwilioClient.
    TwilioClient.Init(accountSID, authToken);

    // Use hello Twilio-provided site for hello TwiML response.
    var url = "http://twimlets.com/message";
    url = $"{url}?Message%5B0%5D=Hello%20World";

    // Set hello call From, To, and URL values toouse for hello call.
    // This sample uses hello sandbox number provided by
    // Twilio toomake hello call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri(url));
        }

<span data-ttu-id="c1e90-197">Per ulteriori informazioni sui parametri hello passato toohello **CallResource.Create** metodo, vedere [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span><span class="sxs-lookup"><span data-stu-id="c1e90-197">For more information about hello parameters passed in toohello **CallResource.Create** method, see [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span></span>

<span data-ttu-id="c1e90-198">Come accennato, questo codice Usa un hello tooreturn sito fornito Twilio TwiML risposta.</span><span class="sxs-lookup"><span data-stu-id="c1e90-198">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="c1e90-199">È possibile utilizzare la propria hello tooprovide sito TwiML risposta.</span><span class="sxs-lookup"><span data-stu-id="c1e90-199">You could instead use your own site tooprovide hello TwiML response.</span></span> <span data-ttu-id="c1e90-200">Per altre informazioni, vedere [How to: Provide TwiML responses from your own website](#howto_provide_twiml_responses) (Procedura: Fornire risposte TwiML dal proprio sito Web).</span><span class="sxs-lookup"><span data-stu-id="c1e90-200">For more information, see [How to: Provide TwiML responses from your own website](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="c1e90-201"><a id="howto_send_sms"></a>Procedura: Inviare un messaggio SMS</span><span class="sxs-lookup"><span data-stu-id="c1e90-201"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="c1e90-202">Hello schermata riportata di seguito viene illustrato come un messaggio SMS utilizzando toosend hello **MessageResource** classe.</span><span class="sxs-lookup"><span data-stu-id="c1e90-202">hello following screenshot shows how toosend an SMS message using hello **MessageResource**  class.</span></span> <span data-ttu-id="c1e90-203">Hello **da** numero fornito dal Twilio per versione di valutazione account toosend messaggi SMS.</span><span class="sxs-lookup"><span data-stu-id="c1e90-203">hello **from** number is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="c1e90-204">Hello **a** numero deve essere verificato per l'account di Twilio prima di eseguire codice hello.</span><span class="sxs-lookup"><span data-stu-id="c1e90-204">hello **to** number must be verified for your Twilio account before you run hello code.</span></span>

    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    const string accountSID = "your_twilio_account";
    const string authToken = "your_twilio_authentication_token";

    // Initialize hello TwilioClient.
    TwilioClient.Init(accountSID, authToken);

    try
    {
        // Send an SMS message.
        var message = MessageResource.Create(
            to: new PhoneNumber("+12069419717"),
            from: new PhoneNumber("+14155992671"),
            body: "This is my SMS message.");
    }
    catch (TwilioException ex)
    {
        // An exception occurred making hello REST call
        Console.WriteLine(ex.Message);
    }

## <span data-ttu-id="c1e90-205"><a id="howto_provide_twiml_responses"></a>Procedura: Fornire risposte TwiML dal proprio sito Web</span><span class="sxs-lookup"><span data-stu-id="c1e90-205"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own website</span></span>
<span data-ttu-id="c1e90-206">Quando l'applicazione avvia toohello una chiamata API di Twilio, ad esempio, tramite hello **CallResource.Create** metodo - Twilio invia l'URL tooan richiesta tooreturn prevista una risposta TwiML.</span><span class="sxs-lookup"><span data-stu-id="c1e90-206">When your application initiates a call toohello Twilio API - for example, via hello **CallResource.Create** method - Twilio sends your request tooan URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="c1e90-207">esempio Hello in [procedura: effettuare una chiamata in uscita](#howto_make_call) utilizza hello URL fornito Twilio [http://twimlets.com/message] [ twimlet_message_url] risposta hello tooreturn.</span><span class="sxs-lookup"><span data-stu-id="c1e90-207">hello example in [How to: Make an outgoing call](#howto_make_call) uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url] tooreturn hello response.</span></span>

> [!NOTE]
> <span data-ttu-id="c1e90-208">Mentre TwiML deve essere utilizzato dai servizi web, è possibile visualizzare hello TwiML nel browser.</span><span class="sxs-lookup"><span data-stu-id="c1e90-208">While TwiML is designed for use by web services, you can view hello TwiML in your browser.</span></span> <span data-ttu-id="c1e90-209">Ad esempio, fare clic su [http://twimlets.com/message] [ twimlet_message_url] toosee vuota &lt;risposta&gt; elemento; ad esempio, fare clic su [http://twimlets.com/message ? Messaggio % 5B0 %5D = Hello % 20World](http://twimlets.com/message?Message%5B0%5D=Hello%20World) toosee un &lt;risposta&gt; elemento che contiene un &lt;pronuncia&gt; elemento.</span><span class="sxs-lookup"><span data-stu-id="c1e90-209">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty &lt;Response&gt; element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World](http://twimlets.com/message?Message%5B0%5D=Hello%20World) toosee a &lt;Response&gt; element that contains a &lt;Say&gt; element.</span></span>
>
>

<span data-ttu-id="c1e90-210">Anziché basarsi sul URL fornito Twilio hello, è possibile creare un URL sito che restituisce le risposte HTTP.</span><span class="sxs-lookup"><span data-stu-id="c1e90-210">Instead of relying on hello Twilio-provided URL, you can create your own URL site that returns HTTP responses.</span></span> <span data-ttu-id="c1e90-211">È possibile creare il sito hello in qualsiasi linguaggio che restituisce le risposte HTTP.</span><span class="sxs-lookup"><span data-stu-id="c1e90-211">You can create hello site in any language that returns HTTP responses.</span></span> <span data-ttu-id="c1e90-212">Si presuppone che si sarà hosting hello URL da un gestore generico di ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c1e90-212">This topic assumes you'll be hosting hello URL from an ASP.NET generic handler.</span></span>

<span data-ttu-id="c1e90-213">Hello seguente gestore ASP.NET presenta una risposta TwiML che afferma **Hello World** chiamata hello.</span><span class="sxs-lookup"><span data-stu-id="c1e90-213">hello following ASP.NET Handler crafts a TwiML response that says **Hello World** on hello call.</span></span>

    using System.Text;
    using System.Web;

    namespace WebRole1
    {
        /// <summary>
        /// Summary description for Handler1
        /// </summary>
        public class Handler1 : IHttpHandler
        {
            public void ProcessRequest(HttpContext context)
            {
                const string twiMLResponse =
                    "<Response><Say>Hello World.</Say></Response>";
                
                context.Response.Clear();
                context.Response.ContentType = "text/xml";
                context.Response.ContentEncoding = Encoding.UTF8;
                context.Response.Write(twiMLResponse);
                context.Response.End();
            }

            public bool IsReusable
            {
                get
                {
                    return false;
                }
            }
        }
    }
    
<span data-ttu-id="c1e90-214">Come si può notare dal precedente esempio di hello, hello TwiML risposta è semplicemente un documento XML.</span><span class="sxs-lookup"><span data-stu-id="c1e90-214">As you can see from hello example above, hello TwiML response is simply an XML document.</span></span> <span data-ttu-id="c1e90-215">libreria Twilio.TwiML Hello contiene le classi che generano TwiML automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c1e90-215">hello Twilio.TwiML library contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="c1e90-216">Hello esempio riportato di seguito genera risposta equivalente hello, come illustrato in precedenza, ma utilizza hello **VoiceResponse** classe.</span><span class="sxs-lookup"><span data-stu-id="c1e90-216">hello example below produces hello equivalent response as shown above, but uses hello **VoiceResponse** class.</span></span>

    using System.Web;
    using Twilio.TwiML;

    namespace WebRole1
    {
        /// <summary>
        /// Summary description for Handler1
        /// </summary>
        public class Handler1 : IHttpHandler
        {

            public void ProcessRequest(HttpContext context)
            {
                var twiml = new VoiceResponse();
                twiml.Say("Hello World.");

                context.Response.Clear();
                context.Response.ContentType = "text/xml";
                context.Response.Write(twiml.ToString());
                context.Response.End();
            }

            public bool IsReusable
            {
                get
                {
                    return false;
                }
            }
        }
    }

<span data-ttu-id="c1e90-217">Per ulteriori informazioni su TwiML, vedere [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="c1e90-217">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml).</span></span>

<span data-ttu-id="c1e90-218">Dopo aver impostato le risposte di TwiML tooprovide un modo, è possibile passare tale toohello URL **CallResource.Create** metodo.</span><span class="sxs-lookup"><span data-stu-id="c1e90-218">Once you have set up a way tooprovide TwiML responses, you can pass that URL toohello **CallResource.Create** method.</span></span> <span data-ttu-id="c1e90-219">Ad esempio, se si dispone di un'applicazione web denominata tooan MyTwiML distribuiti servizio cloud di Azure e il nome di hello del gestore di ASP.NET è mytwiml.ashx, hello URL può essere passato troppo**CallResource.Create** come illustrato nel seguente codice hello esempio:</span><span class="sxs-lookup"><span data-stu-id="c1e90-219">For example, if you have a web application named MyTwiML deployed tooan Azure cloud service, and hello name of your ASP.NET Handler is mytwiml.ashx, hello URL can be passed too**CallResource.Create** as shown in hello following code sample:</span></span>

    // This sample uses hello sandbox number provided by Twilio toomake hello call.
    // Place hello call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.ashx"));
        }

<span data-ttu-id="c1e90-220">Per ulteriori informazioni sull'utilizzo di Twilio in Azure con ASP.NET, vedere [come toomake un telefono chiamata tramite Twilio in un ruolo web in Azure][howto_phonecall_dotnet].</span><span class="sxs-lookup"><span data-stu-id="c1e90-220">For additional information about using Twilio on Azure with ASP.NET, see [How toomake a phone call using Twilio in a web role on Azure][howto_phonecall_dotnet].</span></span>

[!INCLUDE [twilio-additional-services-and-next-steps](../includes/twilio-additional-services-and-next-steps.md)]

[howto_phonecall_dotnet]: partner-twilio-cloud-services-dotnet-phone-call-web-role.md

[twimlet_message_url]: http://twimlets.com/message

[twilio_rest_making_calls]: http://www.twilio.com/docs/api/rest/making-calls

[vs_project]:http://msdn.microsoft.com/library/windowsazure/ee405487.aspx
[nuget]:http://nuget.org/
[twilio_github_repo]:https://github.com/twilio/twilio-csharp

[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_account]:  https://www.twilio.com/console
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified
