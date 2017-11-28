---
title: "Come usare Twilio per le funzionalità voce e SMS (.NET) | Microsoft Docs"
description: Informazioni su come effettuare una chiamata telefonica e inviare un SMS con il servizio API Twilio API in Azure. Esempi di codice scritti in .NET.
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
ms.openlocfilehash: 1442e3af26ae87e645cf207228ed1197b2afdd4d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-from-azure"></a><span data-ttu-id="01e91-104">Come usare Twilio per le funzionalità voce ed SMS da Azure</span><span class="sxs-lookup"><span data-stu-id="01e91-104">How to use Twilio for voice and SMS capabilities from Azure</span></span>
<span data-ttu-id="01e91-105">In questa guida viene illustrato come eseguire attività di programmazione comuni con il servizio API Twilio in Azure.</span><span class="sxs-lookup"><span data-stu-id="01e91-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="01e91-106">Gli scenari presentati includono la composizione di una chiamata telefonica e l'invio di un messaggio SMS (Short Message Service).</span><span class="sxs-lookup"><span data-stu-id="01e91-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="01e91-107">Per altre informazioni su Twilio e sull'utilizzo delle funzionalità voce ed SMS nelle applicazioni, vedere la sezione [Passaggi successivi](#NextSteps) .</span><span class="sxs-lookup"><span data-stu-id="01e91-107">For more information on Twilio and using voice and SMS in your applications, see the [Next steps](#NextSteps) section.</span></span>

## <span data-ttu-id="01e91-108"><a id="WhatIs"></a>Informazioni su Twilio</span><span class="sxs-lookup"><span data-stu-id="01e91-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="01e91-109">Twilio è una tecnologia all'avanguardia per le comunicazioni aziendali che consente agli sviluppatori di incorporare funzionalità voce, VoIP e di messaggistica nelle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="01e91-109">Twilio is powering the future of business communications, enabling developers to embed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="01e91-110">Consente di virtualizzare tutta l'infrastruttura necessaria in un ambiente globale basato su cloud, esponendolo attraverso la piattaforma API per le comunicazioni Twilio.</span><span class="sxs-lookup"><span data-stu-id="01e91-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through the Twilio communications API platform.</span></span> <span data-ttu-id="01e91-111">Le applicazioni sono scalabili e facili da compilare.</span><span class="sxs-lookup"><span data-stu-id="01e91-111">Applications are simple to build and scalable.</span></span> <span data-ttu-id="01e91-112">Offre flessibilità, grazie a un modello di prezzi con pagamento in base al consumo, e l'affidabilità del cloud.</span><span class="sxs-lookup"><span data-stu-id="01e91-112">Enjoy flexibility with pay-as-you-go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="01e91-113">**Twilio Voice** consente alle applicazioni di effettuare e ricevere chiamate telefoniche.</span><span class="sxs-lookup"><span data-stu-id="01e91-113">**Twilio Voice** allows your applications to make and receive phone calls.</span></span> <span data-ttu-id="01e91-114">**Twilio SMS** consente alle applicazioni di inviare e ricevere SMS.</span><span class="sxs-lookup"><span data-stu-id="01e91-114">**Twilio SMS** enables your applications to send and receive SMS messages.</span></span> <span data-ttu-id="01e91-115">**Twilio Client** consente di effettuare chiamate VoIP da qualsiasi telefono, tablet o browser e supporta WebRTC.</span><span class="sxs-lookup"><span data-stu-id="01e91-115">**Twilio Client** allows you to make VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="01e91-116"><a id="Pricing"></a>Prezzi e offerte speciali di Twilio</span><span class="sxs-lookup"><span data-stu-id="01e91-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="01e91-117">I clienti di Azure riceveranno un' [offerta speciale](http://www.twilio.com/azure): $ 10 di credito Twilio all'aggiornamento dell'account Twilio.</span><span class="sxs-lookup"><span data-stu-id="01e91-117">Azure customers receive a [special offer](http://www.twilio.com/azure): complimentary $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="01e91-118">Il credito Twilio può essere applicato a qualsiasi utilizzo di Twilio ($ 10 di credito equivalgono all'invio di 1.000 SMS o a 1.000 minuti voce per le chiamate in entrata, a seconda della località del numero di telefono, del messaggio o della destinazione della chiamata).</span><span class="sxs-lookup"><span data-stu-id="01e91-118">This Twilio Credit can be applied to any Twilio usage ($10 credit equivalent to sending as many as 1,000 SMS messages or receiving up to 1000 inbound Voice minutes, depending on the location of your phone number and message or call destination).</span></span> <span data-ttu-id="01e91-119">Per riscattare il credito Twilio e iniziare a utilizzare il servizio, visitare la pagina all'indirizzo [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span><span class="sxs-lookup"><span data-stu-id="01e91-119">Redeem this Twilio credit and get started at [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span></span>

<span data-ttu-id="01e91-120">Twilio è un servizio con pagamento in base al consumo.</span><span class="sxs-lookup"><span data-stu-id="01e91-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="01e91-121">Non prevede spese iniziali ed è possibile chiudere l'account in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="01e91-121">There are no set-up fees, and you can close your account at any time.</span></span> <span data-ttu-id="01e91-122">Per altre informazioni, vedere la pagina relativa ai [prezzi di Twilio](http://www.twilio.com/voice/pricing).</span><span class="sxs-lookup"><span data-stu-id="01e91-122">You can find more details at [Twilio Pricing](http://www.twilio.com/voice/pricing).</span></span>

## <span data-ttu-id="01e91-123"><a id="Concepts"></a>Concetti</span><span class="sxs-lookup"><span data-stu-id="01e91-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="01e91-124">L'API Twilio è un'API RESTful che fornisce funzionalità voce ed SMS per le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="01e91-124">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="01e91-125">Le librerie client sono disponibili in più lingue. Per un elenco, vedere [Twilio API Libraries][twilio_libraries] (Librerie dell'API Twilio).</span><span class="sxs-lookup"><span data-stu-id="01e91-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="01e91-126">I concetti principali dell'API Twilio sono costituiti dai verbi Twilio e dal linguaggio di markup Twilio (Twilio Markup Language, TwiML).</span><span class="sxs-lookup"><span data-stu-id="01e91-126">Key aspects of the Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="01e91-127"><a id="Verbs"></a>Verbi Twilio</span><span class="sxs-lookup"><span data-stu-id="01e91-127"><a id="Verbs"></a>Twilio verbs</span></span>
<span data-ttu-id="01e91-128">Nell'API vengono usati i verbi di Twilio: il verbo **&lt;Say&gt;**, ad esempio, indica a Twilio di recapitare un messaggio acustico in una chiamata.</span><span class="sxs-lookup"><span data-stu-id="01e91-128">The API makes use of Twilio verbs; for example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span>

<span data-ttu-id="01e91-129">Di seguito è riportato un elenco dei verbi Twilio.</span><span class="sxs-lookup"><span data-stu-id="01e91-129">The following is a list of Twilio verbs.</span></span>  <span data-ttu-id="01e91-130">Per altre informazioni su altri verbi e funzionalità, vedere la [documentazione relativa a Twilio Markup Language](http://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="01e91-130">Learn about the other verbs and capabilities via [Twilio Markup Language documentation](http://www.twilio.com/docs/api/twiml).</span></span>

* <span data-ttu-id="01e91-131">**&lt;Dial&gt;**: connette il chiamante a un altro telefono.</span><span class="sxs-lookup"><span data-stu-id="01e91-131">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="01e91-132">**&lt;Gather&gt;**: raccoglie i numeri digitati sulla tastiera del telefono.</span><span class="sxs-lookup"><span data-stu-id="01e91-132">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="01e91-133">**&lt;Hangup&gt;**: termina una chiamata.</span><span class="sxs-lookup"><span data-stu-id="01e91-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="01e91-134">**&lt;Play&gt;**: riproduce un file audio.</span><span class="sxs-lookup"><span data-stu-id="01e91-134">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="01e91-135">**&lt;Pause&gt;**: attende in modo silenzioso per un numero di secondi specificato.</span><span class="sxs-lookup"><span data-stu-id="01e91-135">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="01e91-136">**&lt;Record&gt;**: registra la voce del chiamante e restituisce l'URL del file contenente la registrazione.</span><span class="sxs-lookup"><span data-stu-id="01e91-136">**&lt;Record&gt;**: Records the caller's voice and returns an URL of a file that contains the recording.</span></span>
* <span data-ttu-id="01e91-137">**&lt;Redirect&gt;**: trasferisce il controllo di una chiamata o di un SMS al codice TwiML presso un URL diverso.</span><span class="sxs-lookup"><span data-stu-id="01e91-137">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="01e91-138">**&lt;Reject&gt;**: rifiuta una chiamata in arrivo al numero Twilio senza alcun addebito.</span><span class="sxs-lookup"><span data-stu-id="01e91-138">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you</span></span>
* <span data-ttu-id="01e91-139">**&lt;Say&gt;**: effettua la sintesi vocale del testo durante una chiamata.</span><span class="sxs-lookup"><span data-stu-id="01e91-139">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="01e91-140">**&lt;Sms&gt;**: invia un SMS.</span><span class="sxs-lookup"><span data-stu-id="01e91-140">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="01e91-141"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="01e91-141"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="01e91-142">TwiML è un set di istruzioni basate su XML e sui verbi Twilio che indicano a Twilio come elaborare una chiamata o un SMS.</span><span class="sxs-lookup"><span data-stu-id="01e91-142">TwiML is a set of XML-based instructions based on the Twilio verbs that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="01e91-143">Ad esempio, il codice TwiML seguente effettua la sintesi vocale del testo **Hello World** .</span><span class="sxs-lookup"><span data-stu-id="01e91-143">As an example, the following TwiML would convert the text **Hello World** to speech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

<span data-ttu-id="01e91-144">Quando l'applicazione chiama l'API Twilio, uno dei parametri dell'API è l'URL che restituisce la risposta TwiML.</span><span class="sxs-lookup"><span data-stu-id="01e91-144">When your application calls the Twilio API, one of the API parameters is the URL that returns the TwiML response.</span></span> <span data-ttu-id="01e91-145">Ai fini dello sviluppo, è possibile utilizzare gli URL offerti da Twilio per fornire le risposte TwiML utilizzate dalle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="01e91-145">For development purposes, you can use Twilio-provided URLs to provide the TwiML responses used by your applications.</span></span> <span data-ttu-id="01e91-146">È inoltre possibile ospitare gli URL per produrre le risposte TwiML oppure utilizzare l'oggetto **TwiMLResponse** .</span><span class="sxs-lookup"><span data-stu-id="01e91-146">You could also host your own URLs to produce the TwiML responses, and another option is to use the **TwiMLResponse** object.</span></span>

<span data-ttu-id="01e91-147">Per altre informazioni sui verbi Twilio, i relativi attributi e il codice TwiML, vedere [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="01e91-147">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="01e91-148">Per altre informazioni sull'API Twilio, vedere [Twilio API][twilio_api] (API Twilio).</span><span class="sxs-lookup"><span data-stu-id="01e91-148">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="01e91-149"><a id="CreateAccount"></a>Creare un account Twilio</span><span class="sxs-lookup"><span data-stu-id="01e91-149"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="01e91-150">Se si desidera creare un account Twilio, iscriversi nella pagina [Try Twilio][try_twilio] (Provare Twilio).</span><span class="sxs-lookup"><span data-stu-id="01e91-150">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="01e91-151">È possibile iniziare con un account gratuito ed eseguire l'aggiornamento in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="01e91-151">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="01e91-152">Quando si effettua l'iscrizione a un account Twilio, si riceverà un ID account e un token di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="01e91-152">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="01e91-153">Entrambe queste informazioni sono necessarie per effettuare chiamate all'API Twilio.</span><span class="sxs-lookup"><span data-stu-id="01e91-153">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="01e91-154">Per prevenire accessi autorizzati all'account, conservare il token di autenticazione in un luogo sicuro.</span><span class="sxs-lookup"><span data-stu-id="01e91-154">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="01e91-155">L'ID account e il token di autorizzazione sono visualizzabili nella [pagina dell'account Twilio][twilio_account], rispettivamente nei campi **ACCOUNT SID** (SID ACCOUNT) e **AUTH TOKEN** (TOKEN AUTORIZZAZIONE).</span><span class="sxs-lookup"><span data-stu-id="01e91-155">Your account ID and authentication token are viewable at the [Twilio account page][twilio_account], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="01e91-156"><a id="create_app"></a>Creare un'applicazione Azure</span><span class="sxs-lookup"><span data-stu-id="01e91-156"><a id="create_app"></a>Create an Azure Application</span></span>
<span data-ttu-id="01e91-157">Un'applicazione Azure che ospita un'applicazione compatibile con Twilio non è diversa da qualsiasi altra applicazione Azure.</span><span class="sxs-lookup"><span data-stu-id="01e91-157">An Azure application that hosts a Twilio enabled application is no different from any other Azure application.</span></span> <span data-ttu-id="01e91-158">Aggiungere la libreria Twilio .NET e configurare il ruolo per l'uso delle librerie Twilio .NET.</span><span class="sxs-lookup"><span data-stu-id="01e91-158">You add the Twilio .NET library and configure the role to use the Twilio .NET libraries.</span></span>
<span data-ttu-id="01e91-159">Per informazioni sulla creazione di un progetto Azure iniziale, vedere [Creazione di un progetto Azure con Visual Studio][vs_project].</span><span class="sxs-lookup"><span data-stu-id="01e91-159">For information on creating an initial Azure project, see [Creating an Azure project with Visual Studio][vs_project].</span></span>

## <span data-ttu-id="01e91-160"><a id="configure_app"></a>Configurare l'applicazione per l'uso delle librerie Twilio</span><span class="sxs-lookup"><span data-stu-id="01e91-160"><a id="configure_app"></a>Configure Your Application to use Twilio Libraries</span></span>
<span data-ttu-id="01e91-161">Twilio fornisce un set di librerie helper .NET che copre vari aspetti di Twilio per fornire modi semplici e pratici per interagire con l'API REST di Twilio e il client Twilio per generare risposte TwiML.</span><span class="sxs-lookup"><span data-stu-id="01e91-161">Twilio provides a set of .NET helper libraries that wrap various aspects of Twilio to provide simple and easy ways to interact with the Twilio REST API and Twilio Client to generate TwiML responses.</span></span>

<span data-ttu-id="01e91-162">Twilio offre cinque librerie per sviluppatori .NET:</span><span class="sxs-lookup"><span data-stu-id="01e91-162">Twilio provides five libraries for .NET developers:</span></span>
<span data-ttu-id="01e91-163">Libreria</span><span class="sxs-lookup"><span data-stu-id="01e91-163">Library</span></span>|<span data-ttu-id="01e91-164">Descrizione</span><span class="sxs-lookup"><span data-stu-id="01e91-164">Description</span></span>
---|---
<span data-ttu-id="01e91-165">Twilio.API</span><span class="sxs-lookup"><span data-stu-id="01e91-165">Twilio.API</span></span>|<span data-ttu-id="01e91-166">La libreria Twilio di base che include l'API REST Twilio in una libreria .NET intuitiva.</span><span class="sxs-lookup"><span data-stu-id="01e91-166">The core Twilio library that wraps the Twilio REST API in a friendly .NET library.</span></span> <span data-ttu-id="01e91-167">Questa libreria è disponibile per .NET, Silverlight e Windows Phone 7.</span><span class="sxs-lookup"><span data-stu-id="01e91-167">This library is available for .NET, Silverlight, and Windows Phone 7.</span></span>
<span data-ttu-id="01e91-168">Twilio.TwiML</span><span class="sxs-lookup"><span data-stu-id="01e91-168">Twilio.TwiML</span></span>|<span data-ttu-id="01e91-169">Fornisce un modo intuitivo per generare il markup TwiML in .NET.</span><span class="sxs-lookup"><span data-stu-id="01e91-169">Provides a .NET friendly way to generate TwiML markup.</span></span>
<span data-ttu-id="01e91-170">Twilio.MVC</span><span class="sxs-lookup"><span data-stu-id="01e91-170">Twilio.MVC</span></span>|<span data-ttu-id="01e91-171">Per gli sviluppatori che usano ASP.NET MVC, questa libreria include un controller TwilioController, una classe ActionResult TwiML e un attributo di convalida della richiesta.</span><span class="sxs-lookup"><span data-stu-id="01e91-171">For developers using ASP.NET MVC, this library includes a TwilioController, TwiML ActionResult, and request validation attribute.</span></span>
<span data-ttu-id="01e91-172">Twilio.WebMatrix</span><span class="sxs-lookup"><span data-stu-id="01e91-172">Twilio.WebMatrix</span></span>|<span data-ttu-id="01e91-173">Per gli sviluppatori che utilizzano lo strumento di sviluppo WebMatrix gratuito di Microsoft, questa libreria contiene gli helper della sintassi Razor per varie azioni Twilio.</span><span class="sxs-lookup"><span data-stu-id="01e91-173">For developers using Microsoft's free WebMatrix development tool, this library contains Razor syntax helpers for various Twilio actions.</span></span>
<span data-ttu-id="01e91-174">Twilio.Client.Capability</span><span class="sxs-lookup"><span data-stu-id="01e91-174">Twilio.Client.Capability</span></span>|<span data-ttu-id="01e91-175">Contiene il generatore di token Capability per l'utilizzo con l'SDK JavaScript per il client Twilio.</span><span class="sxs-lookup"><span data-stu-id="01e91-175">Contains the Capability token generator for use with the Twilio Client JavaScript SDK.</span></span>

<span data-ttu-id="01e91-176">Si noti che tutte le librerie richiedono .NET 3.5, Silverlight 4 o Windows Phone 7 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="01e91-176">Note that all libraries require .NET 3.5, Silverlight 4, or Windows Phone 7 or later.</span></span>

<span data-ttu-id="01e91-177">Nell'esempio illustrato in questa guida viene usata la libreria Twilio.API.</span><span class="sxs-lookup"><span data-stu-id="01e91-177">The samples provided in this guide use the Twilio.API library.</span></span>

<span data-ttu-id="01e91-178">Le librerie possono essere [installate tramite l'estensione Gestione pacchetti NuGet](http://www.twilio.com/docs/csharp/install) disponibile per Visual Studio da 2010 a 2015.</span><span class="sxs-lookup"><span data-stu-id="01e91-178">The libraries can be [installed using the NuGet package manager extension](http://www.twilio.com/docs/csharp/install) available for Visual Studio 2010 up to 2015.</span></span>  <span data-ttu-id="01e91-179">Il codice sorgente è ospitato in [GitHub][twilio_github_repo], che include un wiki contenente la documentazione completa per l'uso delle librerie.</span><span class="sxs-lookup"><span data-stu-id="01e91-179">The source code is hosted on [GitHub][twilio_github_repo], which includes a Wiki that contains complete documentation for using the libraries.</span></span>

<span data-ttu-id="01e91-180">Per impostazione predefinita, con Microsoft Visual Studio 2010 viene installata la versione 1.2 di NuGet.</span><span class="sxs-lookup"><span data-stu-id="01e91-180">By default, Microsoft Visual Studio 2010 installs version 1.2 of NuGet.</span></span> <span data-ttu-id="01e91-181">L'installazione delle librerie Twilio richiede NuGet 1.6 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="01e91-181">Installing the Twilio libraries requires version 1.6 of NuGet or higher.</span></span> <span data-ttu-id="01e91-182">Per informazioni sull'installazione o l'aggiornamento di NuGet, vedere [http://nuget.org/][nuget].</span><span class="sxs-lookup"><span data-stu-id="01e91-182">For information on installing or updating NuGet, see [http://nuget.org/][nuget].</span></span>

> [!NOTE]
> <span data-ttu-id="01e91-183">Per installare la versione più recente di NuGet, è innanzitutto necessario disinstallare la versione caricata tramite Gestione estensioni di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="01e91-183">To install the latest version of NuGet, you must first uninstall the loaded version using the Visual Studio Extension Manager.</span></span> <span data-ttu-id="01e91-184">A questo scopo, è necessario eseguire Visual Studio come amministratore.</span><span class="sxs-lookup"><span data-stu-id="01e91-184">To do so, you must run Visual Studio as administrator.</span></span> <span data-ttu-id="01e91-185">In caso contrario, il pulsante Disinstalla è disabilitato.</span><span class="sxs-lookup"><span data-stu-id="01e91-185">Otherwise, the Uninstall button is disabled.</span></span>
>
>

### <span data-ttu-id="01e91-186"><a id="use_nuget"></a>Per aggiungere le librerie Twilio al progetto di Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="01e91-186"><a id="use_nuget"></a>To add the Twilio libraries to your Visual Studio project:</span></span>
1. <span data-ttu-id="01e91-187">Aprire la soluzione in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="01e91-187">Open your solution in Visual Studio.</span></span>
2. <span data-ttu-id="01e91-188">Fare clic con il pulsante destro del mouse su **Riferimenti**.</span><span class="sxs-lookup"><span data-stu-id="01e91-188">Right-click **References**.</span></span>
3. <span data-ttu-id="01e91-189">Scegliere **Gestisci pacchetti NuGet...**</span><span class="sxs-lookup"><span data-stu-id="01e91-189">Click **Manage NuGet Packages...**</span></span>
4. <span data-ttu-id="01e91-190">Fare clic su **Online**.</span><span class="sxs-lookup"><span data-stu-id="01e91-190">Click **Online**.</span></span>
5. <span data-ttu-id="01e91-191">Nella casella di ricerca online digitare *twilio*.</span><span class="sxs-lookup"><span data-stu-id="01e91-191">In the search online box, type *twilio*.</span></span>
6. <span data-ttu-id="01e91-192">Fare clic su **Install** sul pacchetto Twilio.</span><span class="sxs-lookup"><span data-stu-id="01e91-192">Click **Install** on the Twilio package.</span></span>

## <span data-ttu-id="01e91-193"><a id="howto_make_call"></a>Procedura: Effettuare una chiamata in uscita</span><span class="sxs-lookup"><span data-stu-id="01e91-193"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="01e91-194">Di seguito è illustrato come effettuare una chiamata in uscita usando la classe **CallResource**.</span><span class="sxs-lookup"><span data-stu-id="01e91-194">The following shows how to make an outgoing call using the **CallResource** class.</span></span> <span data-ttu-id="01e91-195">Questo codice utilizza inoltre un sito fornito da Twilio per restituire la risposta TwiML (Twilio Markup Language).</span><span class="sxs-lookup"><span data-stu-id="01e91-195">This code also uses a Twilio-provided site to return the Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="01e91-196">Sostituire i valori di **to** e **from** relativi ai numeri di telefono e, prima di eseguire il codice, verificare il numero di telefono specificato in **from** per l'account Twilio.</span><span class="sxs-lookup"><span data-stu-id="01e91-196">Substitute your values for the **to** and **from** phone numbers, and ensure that you verify the **from** phone number for your Twilio account before running the code.</span></span>

    // Use your account SID and authentication token instead
    // of the placeholders shown here.
    const string accountSID = "your_twilio_account";
    const string authToken = "your_twilio_authentication_token";

    // Initialize the TwilioClient.
    TwilioClient.Init(accountSID, authToken);

    // Use the Twilio-provided site for the TwiML response.
    var url = "http://twimlets.com/message";
    url = $"{url}?Message%5B0%5D=Hello%20World";

    // Set the call From, To, and URL values to use for the call.
    // This sample uses the sandbox number provided by
    // Twilio to make the call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri(url));
        }

<span data-ttu-id="01e91-197">Per altre informazioni sui parametri passati al metodo **CallResource.Create**, vedere [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span><span class="sxs-lookup"><span data-stu-id="01e91-197">For more information about the parameters passed in to the **CallResource.Create** method, see [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span></span>

<span data-ttu-id="01e91-198">Come indicato in precedenza, questo codice utilizza un sito fornito da Twilio per restituire la risposta TwiML.</span><span class="sxs-lookup"><span data-stu-id="01e91-198">As mentioned, this code uses a Twilio-provided site to return the TwiML response.</span></span> <span data-ttu-id="01e91-199">Per fornire la risposta TwiML, è tuttavia possibile utilizzare il proprio sito.</span><span class="sxs-lookup"><span data-stu-id="01e91-199">You could instead use your own site to provide the TwiML response.</span></span> <span data-ttu-id="01e91-200">Per altre informazioni, vedere [How to: Provide TwiML responses from your own website](#howto_provide_twiml_responses) (Procedura: Fornire risposte TwiML dal proprio sito Web).</span><span class="sxs-lookup"><span data-stu-id="01e91-200">For more information, see [How to: Provide TwiML responses from your own website](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="01e91-201"><a id="howto_send_sms"></a>Procedura: Inviare un messaggio SMS</span><span class="sxs-lookup"><span data-stu-id="01e91-201"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="01e91-202">Nella schermata seguente è illustrato come inviare un messaggio SMS tramite la classe **MessageResource**.</span><span class="sxs-lookup"><span data-stu-id="01e91-202">The following screenshot shows how to send an SMS message using the **MessageResource**  class.</span></span> <span data-ttu-id="01e91-203">Il numero in **from** per l'invio di messaggi SMS con gli account di valutazione è fornito da Twilio.</span><span class="sxs-lookup"><span data-stu-id="01e91-203">The **from** number is provided by Twilio for trial accounts to send SMS messages.</span></span> <span data-ttu-id="01e91-204">Il numero in **to** deve essere verificato per l'account Twilio prima di eseguire il codice.</span><span class="sxs-lookup"><span data-stu-id="01e91-204">The **to** number must be verified for your Twilio account before you run the code.</span></span>

    // Use your account SID and authentication token instead
    // of the placeholders shown here.
    const string accountSID = "your_twilio_account";
    const string authToken = "your_twilio_authentication_token";

    // Initialize the TwilioClient.
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
        // An exception occurred making the REST call
        Console.WriteLine(ex.Message);
    }

## <span data-ttu-id="01e91-205"><a id="howto_provide_twiml_responses"></a>Procedura: Fornire risposte TwiML dal proprio sito Web</span><span class="sxs-lookup"><span data-stu-id="01e91-205"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own website</span></span>
<span data-ttu-id="01e91-206">Quando l'applicazione avvia una chiamata all'API Twilio, ad esempio tramite il metodo **CallResource.Create**, Twilio invia la richiesta a un URL che deve restituire una risposta TwiML.</span><span class="sxs-lookup"><span data-stu-id="01e91-206">When your application initiates a call to the Twilio API - for example, via the **CallResource.Create** method - Twilio sends your request to an URL that is expected to return a TwiML response.</span></span> <span data-ttu-id="01e91-207">L'esempio in [Procedura: Effettuare una chiamata in uscita](#howto_make_call) usa l'URL fornito da Twilio [http://twimlets.com/message][twimlet_message_url] per restituire la risposta.</span><span class="sxs-lookup"><span data-stu-id="01e91-207">The example in [How to: Make an outgoing call](#howto_make_call) uses the Twilio-provided URL [http://twimlets.com/message][twimlet_message_url] to return the response.</span></span>

> [!NOTE]
> <span data-ttu-id="01e91-208">Poiché TwiML è progettato per essere utilizzato da servizi Web, è possibile visualizzare il codice TwiML nel browser.</span><span class="sxs-lookup"><span data-stu-id="01e91-208">While TwiML is designed for use by web services, you can view the TwiML in your browser.</span></span> <span data-ttu-id="01e91-209">Ad esempio, fare clic su [http://twimlets.com/message][twimlet_message_url] per visualizzare un elemento &lt;Response&gt; vuoto oppure fare clic su [http://twimlets.com/message?Message%5B0%5D=Hello%20World](http://twimlets.com/message?Message%5B0%5D=Hello%20World) per visualizzare un elemento &lt;Response&gt; contenente un elemento &lt;Say&gt;.</span><span class="sxs-lookup"><span data-stu-id="01e91-209">For example, click [http://twimlets.com/message][twimlet_message_url] to see an empty &lt;Response&gt; element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World](http://twimlets.com/message?Message%5B0%5D=Hello%20World) to see a &lt;Response&gt; element that contains a &lt;Say&gt; element.</span></span>
>
>

<span data-ttu-id="01e91-210">Anziché utilizzare l'URL fornito da Twilio, è possibile creare un sito Web personalizzato che restituisce risposte HTTP.</span><span class="sxs-lookup"><span data-stu-id="01e91-210">Instead of relying on the Twilio-provided URL, you can create your own URL site that returns HTTP responses.</span></span> <span data-ttu-id="01e91-211">Il sito può essere creato in un linguaggio qualsiasi purché restituisca risposte HTTP.</span><span class="sxs-lookup"><span data-stu-id="01e91-211">You can create the site in any language that returns HTTP responses.</span></span> <span data-ttu-id="01e91-212">In questo argomento si presuppone che l'URL verrà ospitato da un gestore generico ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="01e91-212">This topic assumes you'll be hosting the URL from an ASP.NET generic handler.</span></span>

<span data-ttu-id="01e91-213">Il gestore ASP.NET seguente crea una risposta TwiML che pronuncia **Hello World** nella chiamata.</span><span class="sxs-lookup"><span data-stu-id="01e91-213">The following ASP.NET Handler crafts a TwiML response that says **Hello World** on the call.</span></span>

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
    
<span data-ttu-id="01e91-214">Come si evince dal codice riportato sopra, la risposta TwiML è semplicemente un documento XML.</span><span class="sxs-lookup"><span data-stu-id="01e91-214">As you can see from the example above, the TwiML response is simply an XML document.</span></span> <span data-ttu-id="01e91-215">La libreria Twilio.TwiML contiene le classi che consentono di generare automaticamente le istruzioni TwiML.</span><span class="sxs-lookup"><span data-stu-id="01e91-215">The Twilio.TwiML library contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="01e91-216">Nell'esempio seguente viene creata la stessa risposta descritta sopra, ma usando la classe **VoiceResponse**.</span><span class="sxs-lookup"><span data-stu-id="01e91-216">The example below produces the equivalent response as shown above, but uses the **VoiceResponse** class.</span></span>

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

<span data-ttu-id="01e91-217">Per ulteriori informazioni su TwiML, vedere [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="01e91-217">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml).</span></span>

<span data-ttu-id="01e91-218">Dopo avere configurato un modo per fornire risposte TwiML, è possibile passare l'URL nel metodo **CallResource.Create** .</span><span class="sxs-lookup"><span data-stu-id="01e91-218">Once you have set up a way to provide TwiML responses, you can pass that URL to the **CallResource.Create** method.</span></span> <span data-ttu-id="01e91-219">Se, ad esempio, si dispone di un'applicazione Web denominata MyTwiML distribuita in un servizio cloud di Azure e il nome del gestore ASP.NET è mytwiml.ashx, è possibile passare l'URL a **CallResource.Create** come illustrato nell'esempio di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="01e91-219">For example, if you have a web application named MyTwiML deployed to an Azure cloud service, and the name of your ASP.NET Handler is mytwiml.ashx, the URL can be passed to **CallResource.Create** as shown in the following code sample:</span></span>

    // This sample uses the sandbox number provided by Twilio to make the call.
    // Place the call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.ashx"));
        }

<span data-ttu-id="01e91-220">Per altre informazioni sull'utilizzo di Twilio in Azure con ASP.NET, vedere [Come effettuare una chiamata tramite Twilio in un ruolo Web in Azure][howto_phonecall_dotnet].</span><span class="sxs-lookup"><span data-stu-id="01e91-220">For additional information about using Twilio on Azure with ASP.NET, see [How to make a phone call using Twilio in a web role on Azure][howto_phonecall_dotnet].</span></span>

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
